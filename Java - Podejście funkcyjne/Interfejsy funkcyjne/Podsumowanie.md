
```
1. Predicate<T>: Służy do tesowania, czy dany obiekt spełnia pewien warunek. Przyjmuje jeden argument i zwraca wartość typu boolean. "boolean test(T t)"

2. Consumer<T>: Reprezentuje operację, która przyjmuje jeden argument i nic nie zwraca (np.wykonanie działania na obiekcie). Służy do działań typu "przyjmij i wykonaj" "void accept(T t)"

3. Function<T, R>: Reprezentuje funkcję przekształcającą wartość wejściową typu T na wynik typu R. Przyjmuje jeden argument i zwraca wynik. 
 "R apply(T t)"

4. Supplier<T>: Służy do dostarczania obiektu określonego typu bez przyjmowania argumentów. Zwraca obiekt typu T. "T get()"
```