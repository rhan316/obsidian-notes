

|         |                                                                                          |
| ------- | ---------------------------------------------------------------------------------------- |
| OR      | Zwraca wartość TRUE, jeśli przynajmniej jedno z wyrażeń jest prawdziwe                   |
| NOT     | Neguje wynik wyrażenia, zwraca TRUE, jeśli warunek jest prawdziwy                        |
| BETWEEN | Sprawdza, czy wartość mieści się w określonym przedziale(włączając to wartości brzegowe) |
| IN      | Sprawdza, czy wartość znajduje się w podanym zbiorze wartości                            |
| IS NULL | Sprawdza, czy wartość jest NULL(brak wartości)                                           |
| AND     | Zwraca wartość TRUE , jeśli oba wyrażenia są prawdziwe                                   |

ZASTOSOWANIE NAWIASÓW

```
SELECT
	klient, wojewodztwo, zakupionaIlosc
FROM 
	rejestZamowien
WHERE
	(wojewodztwo = 'lubelskie' OR wojewodztwo = 'mazowieckie')
AND
	zakupionaIlosc > 8
```
W pierwszej kolejności sprawdzone zostanie wyrażenie z operatorem OR, bo nawiasy mają pierwszeństwo

```
WHERE
	wojewodztwo = 'lubelskie'
OR
	(wojewodztwo = 'pomorskie' 
		AND (zakupionaIlosc >= 3 AND zakupionaIlosc <= 10))
```
W języku SQL pierwszeństwo ma prawdziwość wyrażenia zagnieżdżonego w najgłębiej osadzonym zestawie nawiasów, następnie są brane pod uwagę warunki ujęte w zewnętrznych nawiasach


OPERATOR BETWEEN

Operator ten pozwala skrócić wyrażenie zawierające operator AND, w którym występuje znak >= lub <=, do postaci prostego wyrażenia z jednym operatorem.

```
WHERE 
	ilosc >= 5
AND
	ilosc <= 20

Jest równoznaczne z tym zapisem:

WHERE
	ilosc BETWEEN 5 AND 20
```
Wymagana jest zawsze obecność operatora AND!

OPERATOR IN

Podobnie jak w BETWEEN

```
WHERE
	city = 'Zabrze'
OR
	city = 'Opole'

Zapis jest identyczny z tym:

WHERE
	city IN ('Zabrze', 'Opole')

Gdzie w nawiasie może być dowolna ilość argumentów
```