```
T ---> Function<T, R> ---> R

@FunctionalInterface
public interface Function<T, R> {
	R apply (T, t)
	(...) ==> metody pomocnicze domyślne, statyczne
}

Function<String, Integer> strLen = str -> str != null ? str.length() : 0;
Integer result = strLen.apply("Dom") => 3
```