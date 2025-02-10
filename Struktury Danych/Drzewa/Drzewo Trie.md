Trie to specjalna struktura danych oparta o drzewie, służąca do efektywnego przechowywania i wyszukiwania ciągów znaków, takich jak słowa w słowniku. Jest często stosowana w systemach autouzupełniania, kompresji tekstu i przetwarzania języka naturalnego.

```
Jeśli flaga isEndOfWord jest true, to oznacza koniec danego wyrazu.

1. Dodajemy słowo "apple"
2. + "ape"
3. + "app"
4. + "car"
5. + "cap"



					(root)
				   /     \
				  (c)	  (a) ==> flaga isEndWord = false
				/			 \
			   (a)			  (p) => false
			  /	  \			/	\
			(r)	  (p)	 (e)	(p) => false, dla "app" => isEndWord = true
							   	  \
								  (l) => false
								    \
								     (e) ==> flaga isEndWord = true
```

#### Struktura węzła w Trie

Każdy węzeł w Trie reprezentuje pojedynczy znak i zawiera:
- *Mapę dzieci `children`*, która przechowuje odniesienia do kolejnych liter.
- *Flaga końcowa słowa `isEndOfWord`*, która oznacza, czy dany węzeł jest zakończeniem pełnego słowa.

```java
class TrieNode {
	Map<Character, TriNode> children = new HashMap<>();
	boolean isEndOfWord = false;
}
```

#### Dodawanie słów do Trie

```java
// Przechodzimy po znakach słowa i tworzymy brakujące więzły.

class Trie {
	private TrieNode root;

	public Trie() { root = new Trie(); }

	public void insert(String word) {
		TrieNode node = root;

		for (char c : word.toCharArray()) {
			node.childeren.putIfAbsent(c, new TrieNode());
			node = node.children.get(c); 
		}

		node.isEndOfWord = true;
	}
}
```

#### Wyszukiwanie słowa w Trie

```java

public boolean search(String word) {
	TrieNode node = root;

	for (char c : word.toCharArray()) {
		node = node.children.get(c);
		if (node == null) return false;
	}

	return node.isEndOfWord;
}
[^1]```

#### Usuwanie słowa z Trie

```java
// Rekurencyjnie usuwamy litery, jeśli nie są cześcią innych słów

public boolean delete(String word) { return delete(root, word, 0); }

private boolean delete(TrieNode node, String word, int index) {
	if (index == word.length()) {
		if (!node.isEndOfWord) return false;
		node.isEndOfWord = false;
		return node.children.isEmpty();
	}
}
```
