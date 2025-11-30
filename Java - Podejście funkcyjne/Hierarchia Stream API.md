
Wszystko zaczyna się od *interfejsu bazowego:*
`BaseStream<T, S extends BaseStream<T, S>>`

To taki... fundament całej zabawy.
Na nim stoją wszystkie inne strumienie.
Pod nim masz już właściwe interfejsy:

### 1. Stream < T >
Dla obiektów.
Najczęściej używany - tu robisz mapy, filtry, flatMapy i całą resztę akrobacji.

### 2. Strumienie prymitywów
Bo Java kocha komplikować życie:
- IntStream
- LongStream
- DoubleStream
Dlaczego istnieją?
Bo wydajność. I bo boxing by cię zabił na dużych kolekcjach.

Każdy z nich rozszerza *BaseStream*, ale ma też własne, specyficzne metody typu `sum()`, `average()`, czyli te ich chore agregacje.

### 3. Specjalne podinterfejsy narzędziowe
Przy okazji, w dokumentacji (i twojej fizycznej pamięci RAM) siedzą też:
- `AutoCloseable` , bo strumienie mogą być zamykane
- `Iterator/Spliterator`, bo strumień musi jakoś przebierać dane.
Tak, strumienie potrafią wystawić `Spliterator` - i nie, nie musisz go tworzyć sam, chyba że naprawdę chcesz cierpieć.

