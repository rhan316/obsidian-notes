Gotujesz obiad składający się z kilku dań. Niektóre czynności możesz robić jednocześnie, np. gotowanie makaronu i pieczenie ciasta. Inne muszą być wykonywane w określonej kolejności - np. nie możesz polać spaghetti sosem, zanim sos się ugotuje.

1. **Callback** - to tak, jakbyś zostawił notatkę, żeby ktoś cię zawołał, gdy skończy gotować sos *(callback function)*. Problem w tym, że jeśli masz wiele dań, twoje notatki mogą się pomieszać (callback hell).
2. **Promises** - to bardziej obietnica od osoby gotującej: "Obiecuje, że sos będzie gotowy za 10 minut". Możesz użyć `.then()` na tej obietnicy, żeby zdecydować, co zrobić, gdy sos faktycznie się ugotuje.
3. **Async/await** - to jak pisanie planu działania w taki sposób, jakby wszystko działo się synchronicznie najpierw ugotuj sos, potem polej spaghetti. Wygląda to liniowo, ale w tle dzieją się asynchroniczne procesy.

`async` - Słowo kluczowe, które oznacza, że funkcja zwraca **Promise**. Dzięki temu JavaScript "wie", że coś w tej funkcji będzie asynchroniczne.

`await` - Słowo, które mówi: "Zatrzymaj wykonywanie tego fragmentu kodu, dopóki obietnica (Promise) się nie rozwiąże". Ale uwaga: JS nie zamraża całego programu, tylko tę jedną funkcję - reszta kodu może działać w tle.

```
function gotujMakaron() {

  return new Promise((resolve) => {

    setTimeout(() => {

      console.log("Makaron gotowy!");

      resolve("Makaron");

    }, 2000);

  });

}

  

function zrobSos() {

  return new Promise((resolve) => {

    setTimeout(() => {

      console.log("Sos gotowy!");

      resolve("Sos");

    }, 1000);

  });

}

  
  

async function prepareDinner() {

  const makaron = await gotujMakaron();

  const sos = await zrobSos();

  console.log(`Podajemy ${makaron} z ${sos}!`);

}

  

prepareDinner();
```

**Co się dzieje pod maską?**
- Gdy wywołujesz `await`, JS zatrzymuje działanie konkretnej funkcji (nie blokując całego programu!).
- Silnik JS w tle zajmuje się obietnicą (Promise) i wraca do kodu funkcji dopiero, gdy obietnica zostanie rozwiązana.
- Reszta kodu programu (np. inne funkcje, event loop) działa bez przerwy.

**Diagram**
1. *Start* -> Funkcja `async` uruchamia się.
2. *Napotyka* `await` -> Wykonanie tej funkcji zostaje odłożone na bok.
3. *Promise w tle* -> W tle działa np. timer `setTimeout`.
4. *Promise rozwiązany* -> Funkcja kontynuuje od miejsca, w którym się zatrzymała.