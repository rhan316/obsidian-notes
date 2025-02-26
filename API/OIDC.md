***OpenID Connect (OIDC)*** to warstwa uwierzytelniania zabudowana na OAuth 2.0. Dzięki OIDC aplikacja może potwierdzić tożsamość użytkownika i uzyskać jego dane profilowe, takie jak e-mail czy imię.
- ***OAuth 2.0*** pozwala aplikacji uzyskać dostęp do zasobów użytkownika (np. jego plików na Google Drive).
- ***OIDC = OAuth 2.0 + uwierzytelnianie użytkownika + ID Token***


| Cecha           | OAuth 2.0                                                | OIDC                                                        |
| --------------- | -------------------------------------------------------- | ----------------------------------------------------------- |
| Cel             | Autoryzacja (czy aplikacja może mieć dostęp?)            | Uwierzytelnienie (kim jest użytkownik?) + Autoryzacja       |
| Zwracane tokeny | `access_token`, `refresh_token`                          | `access_token`, `refresh_token`, `id_token`                 |
| Używany do      | API dostępowe (np. Google Drive, GitHub API)             | Logowanie użytkowników                                      |
| Przykład        | Aplikacja może pobierać pliki użytkownika z Google Drive | Aplikacja wie, że użytkownik to "John Doe" i jaki ma e-mail |

#### Role w OIDC
Takie same jak w OAuth 2.0, plus dodatkowa warstwa uwierzytelniania:
- **End User (Użytkownik)** -> Osoba logująca się do aplikacji.
- **Relying Party (RP, Klient)** -> Aplikacja, która chce wiedzieć, kim jest użytkownik.
- **OpenID Provider (OP, Dostawca tożsamości)** -> Serwer uwierzytelniający, np. Google, Facebook, Microsoft.
- **Resource Server (Opcjonalnie)** -> Serwer przechowujący dane użytkownika

Np.
- Ty (End User) logujesz się do aplikacji
- Aplikacja (RP) przekierowuje Cię do Goodle (OP)
- Google uwierzytelnia Cię i zwraca ID Token z Twoimi danymi.
- Aplikacja na podstawie ID Tokena wie, kim jesteś.

#### Główne komponenty OIDC

***ID Token - Kluczowy element OIDC***
To token JWT `JSON Web Token`, który zawiera informacje o użytkowniku.
```json
{
	"iss": "https://accounts.google.com", // Kto wystawił token
	"sub": "61436126", // Unikalny identyfikator użytkownika
	"aud": "client_id_here", // Odbiorca tokena (nasza apliakcja)
	"exp": 26146246, // Data wygaśnięcia tokena
	"iat": 23522652, // Data wystawienia tokena
	"email": "user@example.com",
	"name": "John Doe",
	"picture": "https://example.com/avatar.jpg"
}
// Jest podpisywany kryptograficznie - aplikacja może zweryfikować jego autentyczność
```

***Discovery Endpoint***
OIDC dostarcza **dokument autokonfiguracji**, który ułatwia integrację.
`https://accounts.google.com/.well-known/openid-configuration`
Zawiera np. URL-e do endpointów uwierzytelnienia i pobierania tokenów.

***Standardowe zakresy (scopes)***
W OIDC możemy określić, jakie informacje o użytkowniku chcemy pobrać

| Scope     | Opis                                  |
| --------- | ------------------------------------- |
| `openid`  | Wymagany - informuje, że używamy OIDC |
| `profile` | Imię, nazwisko, avatar użytkownika    |
| `email`   | Adres e-mail                          |
| `phone`   | Numer telefonu                        |
| `address` | Adres zamieszkania                    |

### Jak wygląda przepływ w OpenID Connect (OIDC)?
OIDC korzysta z Authorization Code Flow (najbezpieczniejszy model).

***Użytkownik klika "Zaloguj się przez Google"***
Aplikacja przekierowuje go do dostawcy OIDC:
```bash
GET https://accounts.google.com/o/oauth2/auth?
    client_id=YOUR_CLIENT_ID
    &redirect_uri=YOUR_REDIRECT_URI
    &response_type=code
    &scope=openid email profile
```

***Użytkownik się loguje, Google zwraca `authorization_code`***
`GET YOUR_REDIRECT_URI&code=AUTHORIZATION_CODE`

***Aplikacja wymienia kod na `access_token` i `id_token`***
```http
POST https://oauth2.googleapis.com/token
Content-Type: application/x-www-form-urlencoded

client_id=YOUR_CLIENT_ID
&client_secret=YOUR_CLIENT_SECRET
&code=AUTHORIZATION_CODE
&redirect_uri=YOUR_REDIRECT_URI
&grant_type=authorization_code
```
Serwer zwraca:
```json
{
  "access_token": "ACCESS_TOKEN",
  "id_token": "ID_TOKEN",
  "expires_in": 3600,
  "token_type": "Bearer"
}
```

***Aplikacja odczytuje `id_token` i wie, kim jest użytkownik***
```http
GET https://www.googleapis.com/oauth2/v3/userinfo
Authorization: Bearer ACCESS_TOKEN
```
Odpowiedź:
```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "email": "user@example.com",
  "picture": "https://example.com/avatar.jpg"
}
```