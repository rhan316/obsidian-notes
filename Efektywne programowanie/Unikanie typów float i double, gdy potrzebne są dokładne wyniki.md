Float i double nie pozwalają na wyliczanie dokładnych wyników i nie powinny być stosowane tam, gdzie są potrzebne dokładne wyniki.

Do obliczeń finansowych korzystamy z BigDecimal, int lub long.

```
double funds = 1.00;  
int itemsBought = 0;  
  
for (double price = 0.10; funds >= price; price += 0.10) {  
    funds -= price;  
    itemsBought++;  
}  
  
System.out.println(itemsBought + " zakupionych towarów."); // 3  
System.out.println("Reszta: " + funds); // 0.399999999999  
System.out.println();  
  
// Zastosowanie BigDecimal  
  
final BigDecimal TEN_CENTS = new BigDecimal(".10");  
  
int items = 0;  
BigDecimal bdFunds = new BigDecimal("1.00");  
  
for (BigDecimal price = TEN_CENTS; bdFunds.compareTo(price) >= 0; price = price.add(TEN_CENTS)) {  
    bdFunds = bdFunds.subtract(price);  
    items++;  
}  
  
System.out.println(items + " zakupionych towarów."); // 4  
System.out.println("Reszta " + bdFunds); // 0.00
```

Zamiast korzystać z BigDecimal, możemy zastosować int lub long do obsługi wartości po przecinku.

```
int items = 0;
int funds = 100; // Zamiast 1zł zmieniamy ją na groszówki

for (int price = 10; funds >= price; price += 10) {
	funds -= price;
	items++;
}

items => 4
funds => 0
```