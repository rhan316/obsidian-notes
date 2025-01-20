```
T ---> Predicate<T> ---> boolean

@FunctionalInterface
public interface Predicate<T> {
	boolean test(T t)
	(...) ==> metody pomocnicze domyślne, statyczne
}

Predicate<Integer> over9000 = i -> i > 9_000;
Integer result = over9000.test(1_342) => false
```