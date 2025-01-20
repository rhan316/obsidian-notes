**CyclicBarrier** jako linia startu.
Każdy rowerzysta (wątek) przyjeżdża do linii startu i musi zaczekać, aż wszyscy inni uczestnicy (inne wątki) dotrą na miejsce.
Dopiero gdy wszyscy rowerzyści dotrą do linii startu, bariera zostaje "przekroczona" (bariera pęka), a wszyscy startują jednocześnie.

***Jak to działa?***
Gdy tworzysz obiekt *CyclicBarrier*, określasz liczbę wątków (rowerzystów), które muszą dotrzeć do bariery, zanim ta się "otworzy".
`CyclicBarrier barrier = new CyclicBarrier(3);`

Wątki dołączają do bariery: Wątki "dołączają" do bariery, wywołując metodę `await()`.
`barrier.await()`;

Gdy ostatni wątek dotrze do bariery (wszyscy rowerzyści są na starcie), wszystkie wątki są zwalniane i mogą kontynuować pracę.

***Czym różni się CyclicBarrier od CountDownLatch?***
- *CountDownLatch* działa jak bariera jednorazowego użytku - po odliczeniu "do zera" bariera znika.
- *CyclicBarrier* może być używana wielokrotnie - po przekroczeniu bariery wątki mogą do niej wracać.

```
CyclicBarrier barier = new CyclicBarrier(3, () -> {
	print("Wszyscy dotarli, ruszamy razem!");
})

Runnable task = () -> {
	try {
		print(Thread.currentThread().getName() + " dotarł do bariery");
		barrier.await();
		print(Thread... + " rusza dalej");
	}
}
```