Jeśli chcesz przekonwertować wartość typu X do wartości typu Y, to skorzystaj z CAST().
bazowy syntax:
```
CAST(value, AS target_value)
CAST('12' AS INTEGER) => 12 jest typu text

Istnieje inny zapis CAST(): value::target_type
value::target_value
23.12::TEXT

'2024-10-23'::DATE
```