W Javie, korzystając z klasy `Executor` i jej rozszerzeń, można stworzyć różne rodzaje pul wątków (thread pools), dostosowane do specyficznych wymagań aplikacji. Zarządzanie wątkami przez pule pozwala na efektywną alokację zasobów i uniknięcie nadmiernej liczby wątków.

1. **Fixed Thread Pool (Stała liczba wątków)** Kiedy liczba zadań przekracza liczbę wątków w puli, nadmiarowe zadania są umieszczane w kolejce i czekają na dostępne wątki
	`ExecutorService fixedThreadPool = Executors.newFixedThreadPool(4)`
	Gdy znasz maksymalną liczbę jednoczesnych wątków. Do zadań o przewidywalnym obciążeniu i długości działania.

2. **Cached Thread Pool (Elastyczna pula)** Tworzy wątki w razie potrzeby, a nieużywane wątki są usuwane po pewnym czasie (domyślnie 60sec.). Maksymalna liczba wątków ograniczona jest jedynie przez zasoby systemowe. Zadania są natychmiast przydzielane do dostępnym wątków lub nowych wątków. `var cachedThreadPool = Executors.newCachedThreadPool();`

3. **Single Thread Executor (Pojedynczy wątek)** Gwarantuje, że zadania będą wykonywane sekwencyjnie przez jeden wątek. Zadania są umieszczane w kolejce, a każde z nich jest wykonywane jedno po drugim. `var singleThread = Executors.newSingleThreadExecutor();`

4. **Scheduled Thread Pool (Pula wątków z harmonogramem)** Umożliwia uruchamianie zadań w określonym czasie lub w regularnych odstępach czasu. Liczba wątków jest stała.                          `var scheduledThreadPool = Executors.newScheduledThreadPool(2);`

5. **Work-Stealing Pool (Pula o zmiennej liczbie wątków)** Wykorzystuje algorytm work-stealing, w którym wątki mogą "kraść" zadania z innych kolejek wątków. Liczba wątków jest dynamicznie dopasowywana do liczby dostępnych procesorów. Używa ForkJoinPool pod spodem.                  `var workStealingPool = Executors.newWorkStealingPool();`