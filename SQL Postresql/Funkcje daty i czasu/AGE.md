
Funkcja AGE() obejmuje dwa argumenty lub jeden.
Generuje symboliczny wynik wykorzystujący lata i miesiące.
Syntax:
	age(timestamp, timestamp)
	age(timestamp)
	
```
	SELECT age(timestamp '2015-01-15', timestamp '1972-12-28'); // 42 years 18 days
	SELECT age(timestamp '2007-10-07'); // 7 years 3 mons 7 days
	funkcja z 1 argumentem pobiera domyślnie aktualną datę
```

![[Pasted image 20241021155430.png]]