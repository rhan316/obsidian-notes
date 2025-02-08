Co to znaczy "abstrakcyjne"?
Abstrakcja oznacza, że np. klasa to coś, co nie istnieje w pełni w samo w sobie - jest tylko planem lub szkicem. Np. *Mebel (klasa abstrakcyjna)* - nie może istnieć jako fizyczny obiekt. Nie możesz mieć "mebla" w pokoju, bo to pojęcia ogólne. Ale  *krzesło i stół (konkretne klasy dziedziczące po Mebel* mogą istnieć. Są to już konkretne meble, które można postawić w pokoju.

W Javie klasa abstrakcyjna jest deklarowana za pomocą słowa kluczowego `abstract`. Może zawierać: 
`Metody abstrakcyjne` - czyli metody, które nie mają ciała i muszą być zaimplementowane w klasach dziedziczących.
`Zwykłe metody` - które mają pełne ciała i mogą być używane przez klasy potomne.
`Pola` - czyli zmienne, które przechowują dane.

*Kiedy używać klas abstrakcyjnych?* 
Gdy chcesz zdefiniować wspólne zachowanie lub dane dla różnych klas, ale nie możesz z góry określić wszystkich szczegółów oraz kiedy potrzebujesz pewnego szkieletu, które inne klasy będą uzupełniać.
