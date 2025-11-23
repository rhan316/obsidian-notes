W Pythonie metody instancji to zwykłe funkcje, które są umieszczone wewnątrz klasy, ale Py nie dodaje im automatycznie kontekstu obiektu.

Dlatego pierwszym argumentem metody musi być odniesienie do bieżącego obiektu, i tradycyjnie nazywamy ten argument `self`.

```python
class Person:
	def say_hello(self):
		print("Hello, I'm calling from:", self)

Kiedy wywołasz:

p = Person()
p.say_hello()

Python pod spodem robi:

Person.say_hello(p)
czyli przekazuje obiekt `p` jako pierwszy argument.
```

| Cecha                      | `this` w Javie              | `self` w Pythonie                        |
| -------------------------- | --------------------------- | ---------------------------------------- |
| Czy musi być jawne?        | Nie, dodawane automatycznie | Tak, musisz zapisać `self` jako argument |
| Czy jest słowem kluczowym? | Tak, zarezerwowane          | Nie, to tylko nazwa konwencji            |
| Czy można zmienić nazwę?   | Nie                         | Tak, ale nie powinno się                 |
| Skąd pochodzi?             | Język sam przekazuje        | Programista musi podać jako 1 argument   |
### Czemu Python wymaga jawnego `self`?
To jest bardzo w duchu Py: `Explicit is better than implicit`.

Korzyści:
- Lepsza czytelność i zrozumiałość -> każda metoda jasno pokazuje, że pracuje na obiekcie.
- Możesz łatwo tworzyć metody "statyczne" -> Po prostu nie dodajesz `self` ```
  class Math:
	  def add(a, b): // brak self -> metoda nie jest instancyjna
		  return a + b
W javie musisz deklarować static ```
