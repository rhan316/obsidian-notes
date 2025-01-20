```
Supplier<T> ---> T

@FunctionalInterface
public interface Supplier<T> {
	T get();
	(...) ==> metody pomocnicze domyślne, statyczne
}

Supplier<Double> random = () -> Math.random();
Double result = radom.get();
```