Spring Security jest frameworkiem do zarządzania bezpieczeństwem aplikacji opartych o Java, w tym autoryzacji oraz uwierzytelnieniem użytkowników. W przypadku aplikacji serwletowych (często wykorzystywanych w Spring Boot), używa się standardu Java Servlet API.

*Podstawowe składowe architektury*

**Filter Chain (Łańcuch Filtrów)**
- Spring Security używa łańcucha filtrów (ang. SecurityFilterChain), który składa się z wielu filtrów (Filters). Filtry te działają jako pierwsza linia obrony, odpowiadają za różne aspekty związane z bezpieczeństwem, takie jak uwierzytelnienie, autoryzacja, ochrona przed atakami CSRF, itd.
- Każdy filtr ma określona odpowiedzialność. np. jeden filtr może służyć do uwierzytelnienia użytkowników, a inny do sprawdzania uprawnień

**DelegatingFilterProxy**
- To klasa, która pozwala Springowi włączyć zarządzanie filtrami w ramach standardowego cyklu życia aplikacji serwletowej. Jest to sposób na zintegrowanie filtrów Spring Security z serwerem aplikacji, takim jak Tomcat

**SecurityContextHolder**
- Kluczowy komponent, który przechowuje informacje o aktualnie uwierzytelnionym użytkowniku w postaci *SecurityContext*. Ten kontekst przechowuje obiekt *Authentication*, który zawiera szczegóły o użytkowniku (np. jego nazwę, hasło, role)
- Umożliwia dostęp do informacji o uwierzytelnieniu w dowolnym miejscu aplikacji

**AuthenticationManager i ProviderManager**
- Jest odpowiedzialny za przetwarzanie żądań uwierzytelnienia
- W Spring Security zazwyczaj używa się klasy *ProviderManager*, która deleguje przetwarzanie uwierzytelnienia do wielu *AuthenticationProvider*. Ten provider może odpowiadać za uwierzytelnienie oprate np. o bazę danych, LDAP, OAauth itd.

**Filters w Spring Security**
- *UsernamePasswordAuthenticationFilter* => służy do przetwarzania formularzy logowania (np. formularz z loginem i hasłem)
- *BasicAuthenticationFilter* => obsługuje uwierzytelnienie za pomocą nagłówka HTTP Basic
- *SecurityContextPersistenceFilter* => Przywraca *SecurityContext* dla każdego żądania i zapisuje go na koniec
- *ExceptionTranslationFiler* => przechowuje wyjątki związane z bezpieczeństwem i przekształca je w odpowiednie odpowiedzi HTTP

**Proces uwierzytelnienia**
- Kiedy użytkownik próbuje uzyskać dostęp do zasobu zabezpieczonego, żądanie przechodzi przez łańcuch filtrów
- Jeśli uwierzytelnienie jest wymagane, odpowiedni filtr (np. *UsernamePasswordAuthenticationFilter*) przechwytuje dane logowania użytkownika i przekazuje je do *AuthenticationManager*
- *AuthenticationManager* deleguje to do *AuthenticationProvider*, który weryfikuje dane (np. sprawdza hasło)
- Jeśli uwierzytelnienie się powiedzie, *Authentication* jest umieszczone w *SecurityContextHolder*, co oznacza, że użytkownik jest zalogowany

**Autoryzacja**
- Spring Security umożliwia autoryzację poprzez sprawdzanie, czy użytkownik posiada odpowiednie uprawnienia do wykonania danego działania
- Może być to zdefiniowane przez adnotacje w kodzie np. *@PreAuthorize("hasRole('Admin')")*, lub konfigurację w URL w *HttpSecurity* 

**Przepływ żądania**
1. Żądanie HTTP trafia do aplikacji serwletowej (np. Spring Boot)
2. Spring Security Filter Chain przechwytuje żądanie i przetwarza je przez kolejne filtry
3. Jeśli wymagana jest autoryzacja, filtr uwierzytelniający prosi użytkownika o dane logowania lub używa już istniejących danych w SecurityContext
4. Jeśli uwierzytelnienie i autoryzacja się powiodą, żądanie jest kierowane do kontrolera aplikacji, który zwraca odpowiednią odpowiedź

**Podsumowanie**

Architektura Spring Security dla aplikacji serwletowych jest oparta na filtrach, które współpracują ze sobą, aby zapewnić bezpieczeństwo aplikacji. Filtry te obsługują uwierzytelnienie, autoryzację, ochronę przed atakami i inne aspekty bezpieczeństwa. Komponenty takie jak *AuthenticationManager*, *SecurityContextHolder* czy różne filtry, działają razem, by zapewnić integralność i ochronę aplikacji przed nieautoryzowanym dostępem