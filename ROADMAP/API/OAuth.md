Masz konto na facebooku i chcesz zalogować się na nowej stronie internetowej, ale **nie chcesz podawać jej swojego hasła**.
Zamiast tego strona mówi:
"Hej, możesz zalogować się przez facebooka!"
Klikasz przycisk "Zaloguj się przez facebooka", Facebook pyta cię:
"Czy chcesz dać tej stronie dostęp do swojego konta?"
Jeśli się zgodzisz, FB *wyda tej stronie specjalny klucz (tzw. token)*, dzięki któremu strona może np. zobaczyć twoje imię i e-mail ale nie dostanie twojego hasła.
To właśnie robi OAuth!

#### OAuth w szczegółach
1. Użytkownik chce dać aplikacji dostęp do swojego konta (np. FB, Google, GitHub).
2. Aplikacja przekierowuje Cię na stronę dostawcy (np. FB), gdzie logujesz się **bez podawania hasła aplikacji**.
3. Dostawca (np. FB) daje aplikacji token - czyli klucz dostępu, który pozwala jej np. pobrać twoje dane.
4. Aplikacja może używać tego tokena, ale nie zna  twojego hasła!

***Co to jest OAuth 2.0?***
~={magenta}OAuth 2.0 to protokół autoryzacji, który pozwala aplikacjom uzyskać dostęp do zasobów użytkownika bez udostępniania jego hasła. Zamiast tego aplikacja dostaje token dostępu `access_token`, który pozwala na ograniczony dostęp do danych użytkownika.=~

***Główne cechy OAuth 2.0***
- Bezpieczeństwo - Brak potrzeby podawania hasła aplikacji trzeciej.
- Delegacja dostępu - Użytkownik może przyznać określone uprawnienia aplikacji.
- Wygoda - Logowanie jednym kliknięciem przez Google, Facebook itp.
- Obsługa różnych klientów - Web, Mobile, IoT.

***Role w OAuth 2.0***
1. **Resource Owner (Właściciel zasobu)** - np. użytkownik, który udziela dostępu do swojego konta.
2. **Client** - aplikacja, którą chcesz uzyskać dostęp do zasobów użytkownika.
3. **Authorization Server** - serwer, który uwierzytelnia użytkownika i akceptuje tokeny dostępu.
4. **Resource Server** - API, które przechowuje zasoby użytkownika i akceptuje `access_token`.

***Główne typu grantów w OAuth 2.0***

**Authorization Code (najbezpieczniejszy)** - Używany przez aplikacje webowe i mobilne - najczęściej stosowany w praktyce.
Przebieg:
1. Użytkownik jest przekierowany na stronę logowania dostawcy (np. Google)
2. Po zalogowaniu serwer zwraca *kod autoryzacyjny* (`authorization_code`)
3. Aplikacja wymienia ten kod na *token dostępu* (`access_token`)
Zalety: Bezpieczeństwo - `client_secret` nie jest ujawniany w frontendzie.

**Client Credentials (dla serwerów backendowych)** - Służy do uwierzytelniania serwer-serwer bez użytkownika.
Przebieg:
1. Aplikacja wysyła żądanie z `client_id` i `client_secret`
2. Serwer zwraca token dostępu `access_token`
Przykład: Mikroserwisy komunikujące się między sobą.

#### Jak wygląda przepływ Authorization Code?

***Użytkownik inicjuje logowanie***
Aplikacja przekierowuje użytkownika do dostawcy OAuth 2.0 (np. Google)
```bash
GET http://accounts.google.com/o/oauth2/auth?
	client_id=YOUR_CLIENT_ID
	&redirect_uri=YOUR_REDIRECT_URI
	&response_type=code
	&scope=email profile
```

***Użytkownik się loguje i zgadza się na dostęp***
Dostawca OAuth przekierowuje użytkownika do `redirect_uri` z `code`
`GET YOUR_REDIRECT_URI?code=AUTHORIZATION_CODE`

***Aplikacja wymienia `code` na `access_token`***
Aplikacja wysyła POST na serwer autoryzacyjny
```http
POST http://oauth2.googleapis.com/token
Content-Type: appliaction/x-www-form-urlencoded

client_id=YOUR_CLIENT_ID 
&client_secret=YOUR_CLIENT_SECRET 
&code=AUTHORIZATION_CODE 
&redirect_uri=YOUR_REDIRECT_URI 
&grant_type=authorization_code
```
*Serwer zwraca `access_token`*
```json
{
	"access_token": "ACCESS_TOKEN",
	"expires_in": 3600,
	"token_type": "Bearer",
	"refresh_token": "REFRESH_TOKEN"
}
```

***Aplikacja używa `access_token`, aby pobrać dane użytkownika***
```http
GET https://www.googleapis.com/oauth2/v2/userinfo
Authorization: Bearer ACCESS_TOKEN
```
Odpowiedź:
```json
{
	"id": "3261612626",
	"email": "user@example.com",
	"name": "John Doe"
}
```
***Dzięki temu aplikacja zna użytkownika, ale nigdy nie zna jego hasła!***

#### Co to jest Refresh Token?
`access_token` ma ograniczoną ważność (1 godz.)
Gdy wygaśnie, aplikacja może użyć `refresh_token`, by dostać nowy `access_token`.
```http
POST http://oauth2.googleapis.com/token
Content-Type: application/x-www-form-urlencoded 

client_id=YOUR_CLIENT_ID
&client_secret=YOUR_CLIENT_SECRET 
&refresh_token=REFRESH_TOKEN 
&grant_type=refresh_token
```

#### OAuth 2.0 vs OpenID Connect (OIDC)
OAuth 2.0 służy do autoryzacji (czy aplikacja ma dostęp?)
OpenID Connect (OIDC) rozszerza OAuth 2.0 o uwierzytelnienie (kim jest użytkownik?)

OIDC dodaje ID Token, które zawiera dane użytkownika.