
W JS występuje tak zwane dziedziczenie prototypowe. Oznacza to, że każdy obiekt dziedziczy właściwości i metody z innego obiektu - zwanego prototypem.

```
const tab = [1, 2, 3];
Object.getPrototypeOf(tab) === Array.prototype // True

const txt = "Zielony koń";
Object.getPrototypeOf(txt) === String.prototype // True

typeof Array.prototype // "object"
Object.getPrototypeOf(Array.prototype) === Object.prototype // True
```

W JavaScript prototypowa dziedziczenia działa na zasadzie łańcucha prototypów, a Object.prototype jest na końcu tego łańcucha. Oznacza to, że każdy obiekt ostatecznie dziedziczy właściwości i metody z Object.prototype, chyba że obiekt jest specjalnie utworzony bez prototypu.

```
Wszystkie obiekty w JS, które są utworzone na podstawie Object, dziedziczą z Object.prototype. Oznacza to, że mają dostęp do metod takich jak .toString(),
.hasOwnProperty(), .valueOf(), itd.

const person = {
	name: "Janusz"
};
Obiekt person dziedziczy właściwości i metody z Object.prototype.
console.log(person.hasOwnProperty("name")); // True
```