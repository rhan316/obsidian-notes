Wzorzec *Publisher - Subscriber* to rozwinięcie wzorca Obserwator (Observer), które wprowadza kilka kluczowych ulepszeń, szczególnie w systemach reaktywnych. W RxJava wzorzec ten jest fundamentem działania, umożliwiając pracę z *strumieniami danych* w sposób asynchroniczny i reaktywny.

**Na czym polega Publisher - Subscriber?**
W tym wzorcu występują 2 główne elementy:
1. ~={yellow}**Publisher (wydawca)** =~- Obiekt, który generuje zdarzenia lub dane. Jest odpowiedzialny za emitowanie tych danych w postaci strumienia.
2. ~={magenta}**Subscriber (subskrybent)**=~ - Obiekt, który rejestruje się w Publisherze i "subskrybuje" dane. Reaguje na dane lub zdarzenia emitowane przez Publisher.
Dodatkowo w RxJava istnieje mechanizm ~={green}*Subskrypcji (Subscription)*=~, który umożliwia kontrolowanie przepływu danych i rezygnacji z subskrypcji w dowolnym momencie.

**Jak to wygląda w praktyce?**
Wyobraź sobie, to jako relację między dostawcą gazet (Publisher) a prenumeratorem (Subscriber):
- ~={yellow}**Publisher (dostawca gazet)=~ regularnie wydaje nowe numery gazety**
- ~={magenta}**Subscriber (prenumerator)=~ subskrybuje gazetę, czyli zgłasza chęć jej otrzymania.
- ~={green}**Subscription (prenumerata)=~ Umowa między publisher a Subscriber. Prenumerator może z niej zrezygnować w dowolnym momencie.**

***RxJava i Publisher-Subscriber***
W RxJava wzorzec Publisher - Subscriber realizowany jest za pomocą:
- ~={yellow}*Publisher*=~ - W RxJava rolę Publisher pełni *Observable*, *Flowable* lub podobne obiekty (np. Single, Maybe, Completeable). Publisher emituje dane w formie strumienia.
- ~={magenta}*Subscriber*=~ - Subskrybentem jest obiekt implementujący interfejs *Observer* lub *Subscriber*. Sub reaguje na dane (onNext), błędy (onError) i zakończenie strumienia (onComplele).
- ~={green}*Subscription*=~ - Sub zarządza relacją między Publisher a Subscriber, umożliwiając np. zatrzymanie przesyłania danych.