Wyobraź sobie, że chcesz zbudować most nad rzeką. Most to konstrukcja, która może mieć różne rodzaje (np. wiszący, łukowy), a jednocześnie musi obsługiwać różne typy dróg (np. autostrada, ścieżka rowerowa).
Dzięki wzorcowi "Most", zamiast łączyć konkretny rodzaj mostu z konkretnym typem drogi w jednej konstrukcji, oddzielamy te dwie rzeczy: osobno definiujemy rodzaje mostów i osobno rodzaje dróg. Następnie łączymy je mostem - dosłownie i w przenośni.

---

***Problem, który rozwiązuje Most***
	Często w oprogramowaniu spotykamy się z sytuacją, w której hierarchię klasy (np. różne kształty, urządzenia itp.), ale ich konkretne implementacje zależą od wielu zmiennych czynników. Bez wzorca Most hierarchia klas może szybko stać się rozbudowana i trudna do zarządzania.
	Hierarchia klas dla kształtów: Koło, Kwadrat.
	Każdy kształt można renderować na różne sposoby: 2D, 3D.
Jeśli połączysz te dwa aspekty w jednej hierarchii, skończysz z klasami: Koło2D, Koło3D, Kwadrat2D, Kwadrat3D. itd.

***Rozwiązanie wzorca Most***
	Wzorzec Most rozdziela te dwie hierarchie:
	**Abstrakcja** - reprezentuje "wysokopoziomowy" byt (np. kształt).
	**Implementacja** - reprezentuje szczegóły techniczne (np. sposób renderowania).
Zamiast scalać te dwa aspekty w jednej hierarchii, tworzymy pomost między nimi. Abstrakcja deleguje implementacje szczegółów do osobnego obiektu.

---
***Składniki wzorca Most***

1. **Abstrakcja** - Reprezentuje wysokopoziomowy byt, który wykorzystuje implementację do wykonania swojej pracy. Zawiera referencję do obiektu implementacji.
2. **Rozszerzona abstrakcja** - Konkretny wariant abstrakcji, który korzysta z implementacji w specyficzny sposób.
3. **Implementor (Interfejs implementacji)** - Deklaruje metody, które muszą być zaimplementowane przez konkretne klasy implementacji. Działa jako pomost między abstrakcją a szczegółami technicznymi.
4. **Concrete Implementor (Konkretna implementacja)** - Dostarcza konkretne realizacje interfejsu Implementor.