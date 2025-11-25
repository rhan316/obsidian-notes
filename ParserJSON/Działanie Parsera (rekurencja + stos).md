
Wyobraź sobie, że tokenizer daje nam sekwencję tokenów:
```json
{ "name": "Jan", "age": 20, "tags": ["A", "B"] }
```

### Główna funkcja parser -> parseValue()
```yaml
parseValue()

- jeśli currentToken == '{' -> parseObject()
- jeśli currentToken == '[' -> parseArray()
- jeśli STRING -> element: VALUE_STRING
- jeśli NUMBER -> element: VALUE_NUMBER
- jeśli TRUE/FALSE -> element: VALUE_BOOLEAN
- jeśli NULL -> element: VALUE_NULL
```

### Rekurencyjne parseObject()
```scss
parseObject():
    ┌───────────────────────────────┐
    │ Zapisz ELEMENT_OBJECT_START   │
    └───────────────────────────────┘
    Oczekuj tokenu '{'

    Nastepnie:
    ┌───────────────────────────────┐
    │  while token != '}'           │
    │     parseString() → KEY       │
    │     oczekuj ':'               │
    │     parseValue()              │ ← REKURENCJA
    │     jesli ',' → dalej         │
    └───────────────────────────────┘

    ┌───────────────────────────────┐
    │ Zapisz ELEMENT_OBJECT_END     │
    └───────────────────────────────┘
    
    Rekurencja pozwala przetwarzac zagniezdzone obiekty:
    { "a": {"b": {"c": 123 } } }
    Kazdy poziom { } to nowe wywolanie funkcji!
```

### Rekurencyjne parseArray()
```scss
parseArray():
    ┌───────────────────────────────┐
    │ Zapisz ELEMENT_ARRAY_START    │
    └───────────────────────────────┘
    Oczekuj tokenu '['

    ┌───────────────────────────────┐
    │ while token != ']'            │
    │    parseValue()               │ ← REKURENCJA
    │    jesli ',' → dalej          │
    └───────────────────────────────┘

    ┌───────────────────────────────┐
    │ Zapisz ELEMENT_ARRAY_END      │
    └───────────────────────────────┘
    Array tez moze trzymac obiekty, tablice, stringi - wszystko
    Dlatego parseArray() zawsze wywoluje parseValue()
```

### Diagram przepływu
```pgsql
                       +--------------------+
                       |    parseValue()    |
                       +----------+---------+
                                  |
          ---------------------------------------------------
          |           |             |            |          |
         '{'         '['          STRING       NUMBER      NULL/BOOL
          |           |             |            |          |
          v           v             v            v          v
+----------------+  +----------------+      +-----------------------+
|  parseObject() |  |  parseArray() |      |   element: VALUE_X    |
+-------+--------+  +--------+-------+      +-----------------------+
        |                    |
        |                    |
        v                    v
+----------------+   +------------------+
| LOOP over keys |   | LOOP over items  |
|  "key": value  |   |      value       |
+----------------+   +------------------+
       |                      |
       |                      |
       v                      v
+----------------+    +----------------+
|  parseValue()  |    | parseValue()   |
+----------------+    +----------------+
       ↑                      ↑
       |                      |
       +---------- REKURENCJA ---------+

```


