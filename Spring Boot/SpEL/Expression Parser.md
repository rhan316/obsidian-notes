*Expression Parser* to komponent odpowiedzialny za interpretowanie i analizowanie wyrażeń napisanych w języku SpEL. Innymi słowy, jest to narzędzie, które odczytuje wyrażenie w formie tekstowej, np. `T(java.lang.Math).random()` i zmienia je na coś, co aplikacja Spring potrafi zrozumieć i wykonać.

---
**Analogia - tłumacz w kuchni**
Wyobraź sobie, że gotujesz według przepisu, ale jest on zapisany w języku, którego nie znasz (np. francuskim). Aby ugotować danie, potrzebujesz tłumacza, który przekształci te instrukcje na coś, co rozumiesz i możesz wykonać.
- **Przepis** = wyrażenie SpEL (np. `2 + 2`, `T(java.lang.Math).random()`).
- **Tłumacz** = Expression Parser, który odczytuje przepis i mówi Ci, co zrobić.
- **Gotowe danie** = wynik działania wyrażenia.
---
**Jak działa Expression Parser w Spring Boot?**

*Tworzenie Parsera* - jest tworzony za pomocą obiektu klasy `SpelExpressionParser`, który jest dostarczany przez Spring. To właśnie ten obiekt analizuje i przetwarza tekstowe wyrażenia SpEL.
```
public class SpelDemo {
    public static void main(String[] args) {
    
        // Tworzenie parsera
        ExpressionParser parser = new SpelExpressionParser();

        // Parsowanie i ocena wyrażenia
        String expression = "'Hello World'.concat(' from SpEL')";
        String result = parser.parseExpression(expression).getValue(String.class);

        System.out.println(result); // Output: Hello World from SpEL
    }
}
```

*Analiza wyrażenia* - Gdy parser otrzyma wyrażenie, przekształca je w drzewo składniowe (ang. Abstract Syntax Tree, AST), które reprezentuje strukturę logiczną i operacje w wyrażeniu.

*Ocena (Evaluation)* - Po analizie parser przekazuje drzewo składniowe do obiektu `EvaluationContext`, który umożliwia wykonanie wyrażenia. `EvaluationContext` może być używany do dynamicznego odczytu lub modyfikacji danych, takich jak:
- Wartości pól obiektów.
- Metody.
- Kolekcji.
```
public class SpelContextDemo {
    public static void main(String[] args) {
    
        // Parser
        ExpressionParser parser = new SpelExpressionParser();

        // Obiekt EvaluationContext
        StandardEvaluationContext context = new StandardEvaluationContext();
        context.setVariable("name", "Spring");

        // Wyrażenie z użyciem kontekstu
        String expression = "'Hello ' + #name";
        String result = parser.parseExpression(expression).getValue(context, String.class);

        System.out.println(result); // Output: Hello Spring
    }
}
```
---
***Jak SpEL korzysta z Expression Parser w Spring Boot?***

1. **Adnotacje oparte na SpEL.** Kiedy używasz SpEL w Spring Boot (np. w adnotacjach `@Value`, lub `@PreAuthorize`), Spring automatycznie wykorzystuje wbudowany Expression Parser, aby przetworzyć i ocenić wyrażenie.
```
@Value("#{T(java.lang.Math).PI})
private double piValue;
```

2. **Bezpieczeństwo aplikacji** Parser jest również wykorzystywany w adnotacjach takich jak `@PreAuthorize`
```
@PreAuthorize("hasRole('ADMIN'))
public void adminOnlyAction() {
	// tylko dla admina aplikacji
}
```

3. **Warunki konfiguracji** SpEL parser umożliwia dynamiczne włączenie lub wyłączenie komponentów w zależności od warunków
`@ConditionalOnExpression("#{environment['feature.enabled'] == 'true'})`
---

**Dlaczego znajomość Expression Parser jest ważna?**
- Elastyczność = pozwala pisać dynamiczną logikę bez konieczności modyfikowania kodu.
- Efektywność = Expression Parser pozwala Springowi działać bardziej dynamicznie i konfigurowalnie.
- Zaawansowana funkcjonalność = znajomość parsera pozwala lepiej zrozumieć, jak Spring interpretuje wyrażenia w różnych kontekstach.
