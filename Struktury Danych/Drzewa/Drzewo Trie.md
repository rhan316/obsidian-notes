Trie to specjalna struktura danych oparta o drzewie, służąca do efektywnego przechowywania i wyszukiwania ciągów znaków, takich jak słowa w słowniku. Jest często stosowana w systemach autouzupełniania, kompresji tekstu i przetwarzania języka naturalnego.

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
```