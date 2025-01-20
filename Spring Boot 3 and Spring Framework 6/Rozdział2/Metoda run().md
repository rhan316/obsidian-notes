Kontener Spring'a zostaje odpalony po wywołaniu metody run().
```
@SpringBootApplication
public class MyStarterClass {
	public static void main(String[] args) {
		SpringApplication.run(MyStarterClass.class, args);
	}
}
```
Trzy rzeczy mogą się wydarzyć gdy metoda run() zostaje wywołana:
- Jeśli jest problem z konfiguracją - kontener nie zostaje uruchomiony i związku z tym aplikacja nie zostanie uruchomiona
- Gdy wszystko jest w porządku, kontener rozpoczyna pracę. Jeżeli jednak aplikacja korzysta np. z serwera Tomcat, to metoda run() będzie działała nawet po zakończeniu pracy metody main()
- Ta metoda może działać w nieskończoność, jeśli składniki aplikacji tego wymagają