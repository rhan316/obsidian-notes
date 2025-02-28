*Reagowanie na dane*

**Observer** "nasłuchuje" na dane emitowane przez Observable i reaguje na nie. Posiada 3 metody: `onNext, onError, onComplete`.

**Subscriber** to bardziej zaawansowany odpowiednik Observera, który jest używany np. z Flowable i obsługuje mechanizm *backpressure*.