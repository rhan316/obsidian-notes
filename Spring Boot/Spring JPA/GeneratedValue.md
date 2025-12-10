Strategie generowania ID.

Każda encja JPA musi mieć **klucz główny**.
Spring ma to w dupie, JPA ma to w dupie - ale nie baza danych.

Dlatego robisz
```java
@Id
@GeneratedValue(strategy = GenerationType.X)
private Long id;
```
To `strategy` decyduje kto i jak generuje wartość ID.

#### `GenerationType.IDENTITY`
Najprostsze. Najbardziej prymitywne. Najwolniejsze dla masowych insertów.
ID generuje baza danych (np. AUTO_INCREMENT w MySQL, serial w Postgresql).
![[Pasted image 20251210111720.png]]

#### `GenerationType.SEQUENCE`
Zalecana strategia w 2025. Najszybsza. Najbardziej elastyczna.
ID generuje sekwencja w bazie (np. PostgreSQL, Oracle).
Hibernate może pobierać ID z wyprzedzeniem, co przyśpiesza inserty.
Np.
```txt
@Id
@SequenceGenerator(
	name = "user_seq",
	sequenceName = "user_sequence",
	allocationSize = 50
)
@GeneratedValue(
	strategy = GenerationType.SEQUENCE
	generator = "user_seq"
)
private Long id;
```

![[Pasted image 20251210112039.png]]

`GenerationType.TABLE - NIE UŻYWAJ!`
`GenerationType.AUTO - NIEW WARTO!`

![[Pasted image 20251210112739.png]]
