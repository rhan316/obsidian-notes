Adnotacje w Javie są jak naklejki z instrukcjami przyczepione do fragmentów kodu. Te "naklejki" pozwalają dostarczyć dodatkowe informacje o kodzie, które mogą być używane przez kompilator, frameworki lub narzędzia w czasie kompilacji albo wykonywania programu.

Porównajmy to do wysłania paczki pocztą. Na paczce możesz umieścić:
- Etykietę "FRAGILE" (delikatne), aby kurier wiedział, że trzeba obchodzić się z nią ostrożnie.
- "EXPRESS" (priorytet), aby paczka została dostarczona jak najszybciej.
- "RETRUN TO SENDER" (zwróć do nadawcy), aby paczka dostała zwrócona do nadawcy

***Po co są adnotacje?***
1. **Informowanie kompilatora** - Adnotacje takie jak `@Override` pomagają kompilatorowi sprawdzić poprawność kodu. Przykład: Jeśli oznaczysz metodę `@Override`, kompilator upewni się, że faktycznie nadpisujesz metodę z klasy bazowej.
2. **Sterowanie frameworkami** - Frameworki takie jak Spring, Hibernate czy JUnit, używają adnotacji do określenia, jak mają działać. Przykład: `@Autowired` wskazuje, że dany obiekt powinien zostać automatycznie wstrzyknięty (ang. DI).
3. **Generowanie kodu** - Adnotacje, takie jak `@Entity` w Hibernate, pozwalają frameworkowi generować kod potrzebny do działania aplikacji, np. mapowanie klas na tabele w bazie danych
4. **Metadane do przetwarzania w czasie wykonywania** - Dzięki mechanizmowi refleksji, adnotacje mogę być "odczytywane" w trakcie działania programu, co pozwala dynamicznie zmieniać zachowanie aplikacji. Przykład: W testach `@Test` pozwala zidentyfikować, które metody są testami.