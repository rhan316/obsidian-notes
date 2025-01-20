Adnotacje:
- @Cacheable => Ta adnotacja jest używana, aby zapamiętać wynik metody. Jeśli metoda jest wywoływana z takimi samymi parametrami, wynik będzie pochodził z cache, zamiast wykonywać tę metodę ponownie.
- @CachePut => Adnotacja jest używana, aby zaktualizować istniejący cache. Metoda jest zawsze wykonywana, a wynik zapisywany jest w cache.
- @CacheEvict => Używana do usunięcia danych z cache. Może być to przydatne, gdy chcesz usunąć nieaktualne dane.

W Spring, aby wspierać cache'owanie, stosuje się mechanizm proxy. Mechanizm ten umożliwia tworzenie dynamicznych obiektów, które "oprawiają" rzeczywiste obiekty (np. beany) i dodają dodatkową logikę przed lub po wywołaniu danej metody. Działa to w następujący sposób:
1. Tworzenie proxy:
	  Kiedy tworzysz bean, który zawiera metody z adnotacjami cache'owania, Spring automatycznie tworzy proxy wokół tego beana. Może to być JDK dynamic proxy (jeśli klasa implementuje interfejs) lub CGLIB proxy (jeśli klasa nie implementuje interfejsu)
2. Zasada działania proxy:
		Kiedy wywołujesz metodę z adnotacja @Cacheable, nie wywołujesz tej metod bezpośrednio. Zamiast tego, wywołujesz metodę na proxy, które Spring stworzył dla beana.
		Proxy przejmuje kontrolę przed wywołaniem rzeczywistej metody i sprawdza, czzy wynik tej metody nie jest już w cache.
		Jeśli wartość dla danego klucza znajduje się w cache, proxy zwróci wynik z cache, a rzeczywista metoda nie zostanie w ogóle wywołana.
		Jeśli w cache nie ma wyniki, metoda jest wywoływana, a wynik jest zapisywany w cache.