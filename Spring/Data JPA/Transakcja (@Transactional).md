Transakcja to jednostka pracy, która jest wykonywana jako całość - albo wszystkie operacje wchodzące w skład transakcji zostaną wykonane pomyślnie, albo żadna z nich nie zostanie wykonana. Pojęcie to można streścić w słowach: ~={red}**ACID**=~:
1. ~={red} **Atomicity (Atomowość)=~ -->** transakcja jest niepodzielna, wszystko w niej wykonuje się jako całość lub nie wykonuje się wcale.
2. **~={red}Consistency (Spójność)=~ -->** transakcja doprowadza dane do stanu spójnego.
3. **~={red}Isolation (Izolacja)=~ -->** operacje w ramach jednej transakcji są odseparowane od innych transakcji, aby uniknąć niepożądanych skutków.
4. **~={red}Durability (Trwałość)=~ -->** po zakończeniu transakcji jej efekty są trwałe, nawet w przypadku awarii.

**Jak działa @Transactional?**
	Adnotacja *@Transactional* pozwala oznaczać metodę lub klasę jako objętą transakcją. Jeśli oznaczysz metodę tą adnotacją, wszystkie operacje na bazie danych, które są w niej wykonywane, zostaną otoczone jedną transakcją.

```
@Service
public class BankService {
	(...)

	@Transactional
	public void transferMoney(Long fromAccID, Long toAccID, BigDecimal amount) {
	
		fromAcc.withdraw(amount);
		toAcc.deposit(amount);
		
		repo.save(fromAcc);
		repo.save(toAcc);
	}
}
```
Metoda *transferMoney()* jest oznaczona jako transakcyjna:
- Jeśli którakolwiek operacja w tej metodzie zakończy się błędem, cała transakcja zostanie wycofana ~={red}(rollback)=~ i żadne zmiany nie zostaną zapisane w bazie danych.
- Jeśli wszystko pójdzie dobrze, zmiany zostaną zatwierdzone ~={red}(commit)=~.

Adnotacja @Transactional w Spring zapewnia łatwe zarządzanie transakcjami i pozwala na zachowanie spójności danych w aplikacjach. Dzięki tej adnotacji możesz:
- Ułatwić sobie zarządzanie transakcjami
- Zwiększyć bezpieczeństwo operacji na bazie danych
- Kontrolować poziom izolacji, propagację oraz inne właściwości transakcji

