Aspect Oriented Programming (AOP), czyli programowanie zorientowane na aspekty, jest paradygmatem programowania, który pomaga oddzielić logię krzyżową od logiki aplikacji, dzięki czemu kod jest bardziej modularny i łatwiejszy do zarządzania.

AOP pozwala na oddzielenie logiki aplikacji od tzw. **obserwowalnych zachowań (concerns)** , takich jak:
- Logowanie
- Obsługa wyjątków
- Bezpieczeństwo
- Transakcje
- Caching

Dzięki AOP można dodać dodatkowe funkcjonalności bez modyfikowania kodu głównej aplikacji.

**Logika krzyżowa (cross-cutting concerns)** to rodzaj funkcjonalności w oprogramowaniu, która nie należy do głównej logiki biznesowej, ale jest konieczna w wielu miejscach systemu. Jest to kod, który "przecina" różne moduły aplikacji, ponieważ jest powtarzalny i dotyczy wielu funkcjonalności w systemie.


| Główne pojęcia AOP                       |
| ---------------------------------------- |
| Aspekty (Aspects)                        |
| Porady (Advices)                         |
| Punkty przecięcia (Join points)          |
| Wyrażenia punktów przecięcia (Pointcuts) |
| Weaving                                  |

**Aspects** => Aspekty to moduł zawierający kod, który implementuje logię krzyżową. Może zawierać zarówno kod do wykonywania, jak i reguły, kiedy ten kod ma być zastosowany

**Advices (What)** => To fragmenty kodu, które są wykonywane w określonych punktach w aplikacji (join points). Typowe rodzaje porad to:
1. *Before* - kod wykonywany przed metodą
2. *After* - kod wykonywany po zakończeniu metody
3. *Around* - kod otaczający metodę, czyli można wykonać coś przed i po niej (proxy)
4. After Returning - kod wykonywany po pomyślnym zakończeniu metody
5. After Throwing - kod wykonywany po rzuceniu wyjątku przez metodę

**Join Points (When)** => Punkty przecięcia to określone miejsca w aplikacji, gdzie może być wstrzyknięty kod aspektu, takie jak wywołania metod lub obsługa wyjątków

**Point cuts (Where-operational)** => Pointcuty są używane do określenia, gdzie advices powinny być stosowane. Wyrażają, jakie join pointy powinny być "złapane" i gdzie advices powinny być wstrzyknięte

**Weaving (How)** => Proces łączenia aspektów z głównym kodem aplikacji, aby wstrzyknąć odpowiednie advices. Może być wykonywane w różnych momentach:
1. *Compile-time* - podczas kompilacji kodu
2. *Load-time* - podczas ładowania klasy do JVM
3. *Run-time* - podczas wykonywania aplikacji

**AOP pomaga w modularnym zarządzaniu kodem, szczególnie tym, który jest wspólny dla wielu modułów aplikacji. Jest to często używane w ramach takich jak Spring, gdzie AOP jest zintegrowane, co umożliwia łatwe wdrażanie logiki krzyżowej w aplikacjach**

