Bloom filter to probabilistyczna struktura danych służąca do szybkiego sprawdzania przynależności elementu do zbioru.
Nigdy nie zwraca fałszywych negatywów (jeśli element nie należy do zbioru, Bloom filter to potwierdzi).
Może zwracać fałszywe pozytywy (możliwie, że element zostanie oznaczony jako obecny, mimo że go tam nie ma).

**Zastosowanie Bloom Filtera w praktyce**

- *Filtracja antyspamowa* - szybkie sprawdzanie, czy e-mail znajduje się na liście spamowej.
- *Cache validation* - pomoc w określeniu, czy warto odwoływać się do kosztownego cache'u.
- *Systemy rekomendacji* - wykluczanie elementów, które użytkownik już widział.
- *Bazy danych* - szybkie sprawdzanie obecności kluczy w dużych zbiorach danych.


