*Promise (obietnica)* to obiekt w JavaScript, który reprezentuje wartość, która może być dostępna teraz, w przyszłości lub nigdy. Promise służy do obsługi operacji asynchronicznych w bardziej czytelny sposób, eliminując potrzebę stosowania zagnieżdżonych callbacków (tzw. "callback hell").

**Stany Promise**
Promise może znajdować się w jednym z 3 stanów:
- **Pending (oczekujący)** - operacja jeszcze się nie zakończyła.
- **Fulfilled (zrealizowany)** - operacja zakończyła się sukcesem, a wynik jest dostępny.
- **Rejected (odrzucony)** - operacja zakończyła się błędem, a przyczyna jest dostępna.

```
const myPromise = new Promise((resolve, reject) => {
	const success = true; // Przykład warunku

	if (success) resolve("Operacja zakończona sukcesem");
	else reject("Wystąpił błąd");
});
```

**Obsługa Promise**
Do obsługi wyników Promise używa się metod `.then` i `.catch()`:
- `.then()` - wywoływane, gdy Promise zostanie zrealizowany (fulfilled).
- `.catch()` - gdy Promise zostanie odrzucony (rejected).
- `.finally()` - opcjonalnie, niezależnie od wyniku.

```
myPromise
  .then((result) => {
    console.log("Sukces:", result);
  })
  .catch((error) => {
    console.error("Błąd:", error);
  })
  .finally(() => {
    console.log("Operacja zakończona.");
  });

```

Promises są często używane z funkcjami asynchronicznymi, np. pobieranie danych z API
```
fetch("https://api.example.com/data")
  .then((response) => response.json())
  .then((data) => console.log(data))
  .catch((error) => console.error("Błąd:", error));

```

Można łączyć wiele Promise w sekwencję za pomocą `.then()`
```
myPromise
  .then((result) => {
    console.log(result);
    return new Promise((resolve) => resolve("Kolejna operacja zakończona"));
  })
  .then((nextResult) => {
    console.log(nextResult);
  })
  .catch((error) => {
    console.error("Błąd:", error);
  });

```

**Metody statyczne**
`Promise.all()` -> Uruchamia wiele Promise równocześnie i czeka na ich zakończenie.
`Promise.race()` -> Zwraca wynik pierwszego Promise, który zostanie rozwiązany. (zrealizowany lub odrzucony)
`Promise.allSettled()` -> Czeka na zakończenie wszystkich Promise, niezależnie od ich stanu.
`Promise.any()` - Zwraca wynik pierwszego spełnionego Promise. (zrealizowany)