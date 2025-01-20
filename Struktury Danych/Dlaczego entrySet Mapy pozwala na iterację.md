**Czym jest entrySet()?**
Metoda `entrySet()` w klasie `Map` zwraca widok (kolekcję) wpisów `Set<Map.Entry<K, V>>` reprezentujących wszystkie pary klucz-wartość w mapie.
`public abstract Set<Map.Entry<K, V>> entrySet();`

Zwracana wartość to instancja klasy implementującej interfejs `Set`, który z kolei implementuje `Collection`, a on implementuje `Iterable`.

`Set<Map.Entry<K, V>>` --> `Collection<Map.Entry<K, V>>` --> `Iterable<Map.Entry<K, V>>`
Dzięki temu obiekt zwrócony przez `entrySet()` jest iterowalny, mimo że sama mapa nie implementuje `Iterable`.