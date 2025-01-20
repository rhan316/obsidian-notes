DispatcherServlet to centralny mechanizm obsługi żądań HTTP w Spring Framework.  Odpowiada za przekazywanie żądań do zarejestrowanych kontrolerów oraz obsługę wyjątków, mapowania, widoków i innych mechanizmów MVC.

==Główne zadania DispatcherServlet== 

1. **Routing (mapowanie żądań)**: DispatcherServlet wykorzystuje mapowanie żądań HTTP do odpowiednich metod kontrolerów. Te mapowania są definiowane za pomocą takich adnotacji jak @RequestMapping, @GetMapping, @PostMapping
2. **Obsługa wyjątków**: Obsługuje błędy i wyjątki przy użyciu komponentów takich jak @ExceptionHandler lub globalnych kontrolerów (@ControllerAdvice)
3. **Obsługa widoków**: W Spring MVC, DispatcherServlet może korzystać z **ViewResolverów** (np. Thymeleaf, JSP), aby generować widoki na podstawie nazw zwracanych przez kontrolery
4. **Serializacja i deserializacja**: W aplikacjach typu REST API DispatcherServlet automatycznie konwertuje dane (np. obiekty Java) na JSON/XML za pomocą konwerterów, takich jak Jackson
5. **Obsługa interceptora**: DispatcherServlet integruje się z mechanizmami **HandlerInterceptror**, które pozwalają na wykonywanie dodatkowych czynności przed lub po obsłużeniu żądania (np. autoryzacja, logowanie)