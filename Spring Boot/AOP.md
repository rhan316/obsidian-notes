~={red}**AOP** - *Aspect-Oriented Programming*=~
~={red}czyli podejście, które pozwala ci dodać zachowanie do istniejącego kodu bez jego modyfikacji.=~

```java
public void saveUser() {
	log.info("start");
	...
	log.info("end");
}
```
- metoda czysta
- logging w aspekcie
Bo człowieku... nikt nie chce powtarzać 200 razy tego samego kodu.
Spring robi to, tworząc **proxy** wokół twoich bean-ów.

### Dlaczego AOP jest fundamentem Spring-a?

Bo Spring to nie tylko DI i kontener IoC.
Spring to również:
- transakcje -> działają przez AOP
- bezpieczeństwo (Spring Security) -> AOP
- walidacja metod -> AOP
- cache (@Cacheable) -> AOP
- @Async -> AOP
- open-in-view -> AOP
- logowanie -> AOP
Jeśli coś w Spring-u "magicznie dzieje się przed/po metodzie...."
Zgadnij co? Tak. To AOP w swojej brudnej robocie.

### Słownik

**Aspect**
	Klasa, która zawiera logikę "obok" twojego kodu (np. logging, auditing).

**Advice**
	Co robisz i kiedy:
	*Before*
	*After*
	*AfterReturning*
	*AftherThrowning*
	*Around*

**Pointcut**
	Wyrażenie mówiące, do których metod się wstrzyknąć.
	Np. `@Pointcut("execution(* com.example.service.*.*(..))")`
	

**Join point**
	Konkretny punkt wykonania metody - miejsce, gdzie możesz podłączyć Advice.

**Weaving**
	Proces "owinięcia" metody w aspekt.

**Proxy**
	Obiekt pośredni, który odpala aspekt, a potem faktyczną metodę.

### Jak Spring realizuje AOP?

Spring nie używa pełnego AOP jak AspectJ.
Spring robi **proxy-based AOP**, czyli
- dla klas implementującej interfejs --> JDK dynamic proxies
- dla pozostałych --> CGLIB (tworzy subclass-ę w runtime)
To znaczy:
- działa tylko na publicznych metodach
- działa tylko dla bean-ów zarządzanych przez kontener IoC
- działa tylko, gdy metoda jest wywoływana z zewnątrz, nie z `this.sva()`

![[Pasted image 20251211121546.png]]

### Wady

![[Pasted image 20251211121716.png]]

### Praktyczne zastosowania

![[Pasted image 20251211121804.png]]
