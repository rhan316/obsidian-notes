*InfluxDB* to baza danych zoptymalizowania do przechowywania szeregów czasowych (time series data). Używamy głównie do monitorowania, analizy i przechowywania danych zmieniających się w czasie, takich jak:
- **Dane IoT** (np. pomiary temp. z czujników),
- **Monitorowanie infrastruktury IT** (np. zużycie CPU, pamięci RAM),
- **Dane finansowe** (np. ceny akcji w czasie),
- **Dane meteo** (np. zmiany ciśnienia atmosferycznego).

### Dlaczego właśnie InfluxDB?
InfluxDB wyróżnia się wśród innych baz danych, ponieważ:
1. Szybkość - zoptymalizowana pod zapisywanie dużych ilości danych czasowych.
2. Wbudowane funkcje agregacji - ułatwia analizę danych bez konieczności korzystania z zewnętrznych narzędzi.
3. Efektywne przechowywanie danych - stare dane mogą być automatycznie agregowane lub usuwane.
4. Język InfluxDB - język zapytań podobny do SQL, ale dostosowany do danych szeregów czasowych.

### Jak działa InfluxDB?
Wyobraź sobie, że masz wielki zeszyt i zapisujesz w nim codziennie temperaturę na dworze. Każdy wpis składa się z:
- Czasu pomiaru (np. `2025-03-10 12:00:00`)
- Wartości (np. `21.5C`)
- Tagów (metadanych) (np. `location=Warsaw`)
InfluxDB robi dokładnie to samo, ale w sposób optymalny i bardzo wydajny.

### Struktura danych w InfluxDB
Dane przechowywane w InfluxDB mają format podobny do tabeli w Exelu:

| Czas                | Sensor  | Miasto     | Temperatura |
| ------------------- | ------- | ---------- | ----------- |
| 2025-03-10 12:00:00 | `DHT22` | `Warszawa` | `18.3`      |
| 2025-03-10 13:00:00 | `DHT22` | `Warszawa` | `19.63`     |
| 2025-03-10 14:00:00 | `DHT22` | `Warszawa` | `18.55`     |
Każdy wpis to punkt danych `data point`, który składa się z:
- `Timestamp (znacznik czasu)` - określa, kiedy pomiar został wykonany.
- `Fields (pola)` - wartości liczbowe, które zapisujemy (np. temperatura).
- `Tags (tagi)` - metadane (np. nazwa czujnika, lokalizacja).

#### WAŻNE! Tagi są indeksowane i pomagają w szybkim wyszukiwaniu danych, natomiast pola nie są indeksowane (są wartościami do przechowywania).

### Jak wygląda zapis danych?
Dane można zapisać w InfluxDB używając `Line protocol` - prostego formatu tekstowego.
```InfluxDB
temperature,city=Warszawa sensor=DHT22 value=21.5 1626126466
```
Rozbijmy to na części:
`temperature` -> nazwa pomiaru
`city=Warszawa` -> tag
`sensor=DHT22` -> tag
`value=21.5` -> pole
`1626126466` -> znacznik czasu UNIX (czas pomiaru w sekundach)

### Jak pobierać dane?
InfluxDB ma swój język zapytań **InfluxQL**, podobny do SQL, np:
```sql
SELECT value FROM temperature WHERE city='Warszawa' AND time > now() - 1h
```
To zapytanie zwróci temperatury z ostatniej godziny w Warszawie.

### Czym InfluxDB różni się od tradycyjnych baz danych?

| Cecha                                      | InfluxDB | MySQL/PostgreSQL               |
| ------------------------------------------ | -------- | ------------------------------ |
| Optymalizacja pod dane czasowe             | Tak      | Nie                            |
| Szybkie zapisywanie dużej ilości danych    | Tak      | Nie                            |
| Automatyczne agregacje i polityki retencji | Tak      | Nie                            |
| Brak konieczności schematu tabel           | Tak      | Nie (trzeba definiować tabele) |

