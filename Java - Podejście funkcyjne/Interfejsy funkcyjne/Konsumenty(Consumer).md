```
T ---> Consumer<T>

@FunctionalInterface
public interface Consumer<T> {
	void accept(T t)
	(...) ==> metody pomocnicze domyślne, statyczne
}

Consumer<String> println = str -> System.out.println(str);
println.accept("Dom") => Dom
```