Wyobraź sobie, że masz stare radio z wejściem tylko na kasety, ale chcesz słuchać muzyki ze swojego nowoczesnego telefonu. Nie da się, prawda? Potrzebujesz, *adaptera kasetowego*, który pozwoli ci podłączyć telefon do starego radia. Ten adapter "tłumaczy" nowoczesny sygnał z telefonu na format zrozumiały dla starego radia.

Wzorzec projektowy *Adapter* w programowaniu działa dokładnie tak samo - pozwala dwóm niekompatybilnym klasom współpracować ze sobą bez zmiany ich kodu.

---
**Struktura wzorca Adapter w Javie**

Adapter działa na zasadzie **pośrednika**, który "tłumaczy" wywołania jednej klasy na coś, co rozumie druga klasa, Składa się z:
- **Interfejsu docelowego (Target)** - to czego oczekuje kod, który korzysta z adaptera.
- **Klasy do zaadaptowania (Adaptee)** - to, co chcemy dostosować do nowego formatu.
- **Adaptera** - który przekształca jedno w drugie.

---
Załóżmy, że mamy system, który używa standardowego interfejsu `MediaPlayer`, ale dostaliśmy starą klasę `OldMusicPlayer`, która ma inny sposób odtwarzania muzyki. Zastosujemy wzorzec **Adapter**, aby połączyć nowoczesny system z przestarzałą klasą.

```java
// Nowoczesny system oczekuje klasy, która implementuje ten interfejs
interface MediaPlayer {
	void play(String audioType, String fileName);
}

// Stara klasa, która działa inaczej - ma swoją metodę playOldMusic()
class OldMusicPlayer {
	void playOldMusic(String fileName) {
		print("Odtwarzanie starego formatu: " + fileName);
	}
}

// Adapter tłumaczy wywołania MediaPlayer na format zrozumiały przez OldMediaPlayer
class MusicAdapter implements MediaPlayer {
	private OldMusicPlayer oldMusicPlayer;

	// Adapter przyjmuje obiekt starej klasy
	public MusicAdapter(OldMusicAdapter oldMusicAdapter) {
		this.oldMusicAdapter = oldMusicAdapter;
	}

	@Override
	public void play(String audioType, String fileName) {
		if (audioType.equalsIgnoreCase("oldFormat")) {
			- oldMusicPlayer.playOldMusic(fileName); // Przekierwoanie wywoływania starej metody
		} else {
			- print("Nieobsługiwany format: " + audioType);
		}
	}
}

```

#### Kiedy używać wzorca Adapter?
- Gdy masz stary kod, który nie pasuje do nowego systemu.
- Gdy chcesz połączyć dwie niekompatybilne klasy bez zmiany ich kodu.
- Gdy chcesz zapewnić elastyczność i rozszerzalność kodu.


#### Kluczowe wnioski
- Adapter to "tłumacz", który umożliwia współpracę niekompatybilnych klas.
- Nie zmieniamy istniejącego kodu - tylko dodajemy warstwę pośrednią.
- Wzorzec stosowany jest w bibliotekach, API, systemach legacy.