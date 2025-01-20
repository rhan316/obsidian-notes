
| Czym jest Bean?                                                                                                                |
| ------------------------------------------------------------------------------------------------------------------------------ |
| Bean to obiekt zarządzany prze kontener Spring IoC, stworzony zgodnie z metadanymi konfiguracji (np. XML <bean>, adnotacje)    |
| Metadane definiują klasę beana, jego właściwości (np. zakres, metoda inicjalizacji/destrukcji) oraz zależności (collaborators) |

---

| Właściwości beana                 | Opis                                                            |
| --------------------------------- | --------------------------------------------------------------- |
| Class                             | Typ klasy implementującej beana                                 |
| Name                              | Unikalny identyfikator (id lub alias) w kontenerze              |
| Scope                             | Zakres beana (np. singleton, prototype)                         |
| Constructor arguments             | Argumenty konstruktora używane podczas wstrzykiwania zależności |
| Autowiring mode                   | Określa sposób automatycznego łączenia zależności               |
| Lazy initialization               | Wskazuje, czy bean powinien być inicjowany leniwie              |
| Initialization/Destuction methods | Określają metody inicjalizacji i zniszczenia beana              |

---


|                     |                                                                                                                                                  |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Nadpisywanie beanów | Można nadpisać istniejące definicje beanów, ale jest to funkcja opcjonalna (zostanie usunięta w przyszłości)                                     |
| Nazywanie beanów    | Każdy bean ma unikalny identyfikator, który można nadać w XML (atrubuty id, name). Standart Java camelCase jest preferowany                      |
| Tworzenie beana     | 1. Konstruktor 2. Metoda fabryczna statyczna 3. Metoda fabryczna beana                                                                           |
| Aliasowanie beanów  | Bean może mieć aliasy (w XML poprzez <alias>), co jest przydatne w dużych systemach, gdzie różne komponenty odwołują się do tej samej zależności |
| Runtime Typ beana   | Rzeczywisty typ beana można sprawdzić przez BeanFactory.getType, uwzględniając fabryki i proxy AOP                                               |

