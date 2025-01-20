Kiedy żądanie HTTP trafia do Twojej aplikacji, jest ono przetwarzane w określonym porządku przez filtry w tzw. *Filter Chain*.

**Analogia koncertu**
1. *Kontrola biletu* - sprawdzają, czy w ogóle masz bilet.
2. *Kontrola tożsamości* - upewniają się, że bilet należy do Ciebie.
3. *Kontrola bezpieczeństwa* - sprawdzają, czy nie masz przy sobie zakazanych przedmiotów.
4. *Ostateczna autoryzacja* - wpuszczają Cię na odpowiedni sektor (VIP lub standardowy).

W Spring Security działa to podobnie:
1. *SecurityContextPersistenceFilter* - przywraca dane o użytkowniku (np. dane z sesji, jeśli są przechowywane).
2. *UsernamePasswordAuthenticationFilter* - obsługuje logowanie (np. sprawdza login i hasło).
3. *BearerTokenAuthencticationFilter* - sprawdza nagłówek HTTP pod kątem tokenu (np. JWT).
4. *ExceptionTranslationFilter* - przechwytuje błędy bezpieczeństwa i odpowiednio na nie reaguje.
5. *FilterSecurityInterceptor* - sprawdza, czy użytkownik ma prawo do danego zasobu.

Filtry są przetwarzane w ustalonej kolejności, a każdy filtr ma jedno zadanie. Gdy jeden strażnik (filtr) uzna, że żądanie nie spełnia wymagań, blokuje je i reszta filtrów nie jest już uruchamiana.