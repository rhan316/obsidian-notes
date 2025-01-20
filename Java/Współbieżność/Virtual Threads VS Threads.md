**Klasyczne wątki VS Wirtualne wątki**

*Klasyczne wątki (Threads)*
- Każdy wątek jest mapowany na systemowy wątek OS.
- Wątki są ciężkie w użyciu - każdy wymaga dużych zasobów (stos, przełączanie kontekstu).
- Tworzenie tysięcy wątków jest kosztowne.

*Wirtualne wątki (Virtual Threads)*
 - Są lekkimi wątkami zarządzanymi przez JVM, a nie przez system operacyjny.
 - Tworzenie i zarządzanie tymi wątkami jest tanie, więc można uruchomić ich miliony.
 - Wykorzystują mechanizm współbieżności oparty na wywłaszczeniu, co pozwala na bardziej efektywne użycie procesora.

Virtual Threads należą głównie do wielowątkowości i współbieżności, ponieważ:
- Są wątkami (lekkimi) i wykorzystują mechanizmy znane z klasycznej wielowątkowości
- Są idealne do realizacji współbieżności, gdzie zadania przełączają się między sobą w optymalny sposób