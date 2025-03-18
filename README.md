# Serializacja i deserializacja danych

W programowaniu, także w języku Python, często spotyka się pojęcia serializacji i deserializacji. Te techniki są kluczowe, gdy chcemy zapisywać stan obiektu do pliku, aby móc go później odtworzyć, lub przesyłać dane między różnymi programami lub instancjami programu. 

## Serializacja (inaczej marshalling, pickling lub flattening) )
Serializacja, znana w Pythonie jako “piklowanie”, to proces konwersji obiektu w Pythonie do formatu bajtowego, który można zapisać na dysku lub przesłać przez sieć. Operacja ta umożliwia zapis stanu obiektu do pliku, co jest szczególnie przydatne w przypadku przechowywania złożonych struktur danych, takich jak listy, słowniki, a nawet instancje klas. Dane zapisane
w pliku mogą później posłużyć do odtworzenia stanu programu przy jego kolejnym uruchomieniu.

```python
import pickle

# Definicja prostego słownika
data = {"klucz": "wartość", "liczba": 42}

# Piklowanie danych do pliku
with open("data.pickle", "wb") as file:
    pickle.dump(data, file)  # Zapisuje obiekt data do pliku w formacie pickle
```

W powyższym przykładzie, używamy modułu pickle do serializacji słownika `data` i zapisujemy go do pliku `data.pickle`. Użycie trybu `wb` w funkcji `open` oznacza, że plik jest otwierany do zapisu w trybie binarnym, co jest wymagane przez proces piklowania.

## Deserializacja (inaczej demarshalling lub unpicking)
Deserializacja, czyli odpiklowanie, to proces odwrotny do serializacji. Polega na przekształceniu danych z formatu bajtowego z powrotem na obiekt Pythona. Dzięki temu możemy odtworzyć stan obiektu zapisanego wcześniej na dysku.

> ## Za pomocą modułu pickle należy deserializować dane pochodzące wyłącznie z zaufanego źródła. Deserializacja niezaufanych danych może wiązać się z poważnym zagrożeniem bezpieczeństwa dla systemu, na którym działa nasz program. Proces deserializacji danych umożliwia wykonanie dowolnego kodu. Kontrola danych przeznaczonych do deserializacji za pomocą modułu pickle to silny atut w rękach atakującego.

```python
import pickle

# Odpiklowanie danych z pliku
with open("data.pickle", "rb") as file:
    data_loaded = pickle.load(file)  # Odczytuje obiekt z pliku i przypisuje do zmiennej data_loaded

# Wyświetlanie załadowanych danych
print(data_loaded)  # Wyświetli: {'klucz': 'wartość', 'liczba': 42}
```

W powyższym fragmencie kodu, otwieramy plik `data.pickle` w trybie `rb` (czytanie w formacie binarnym) i używamy funkcji `pickle.load` do odczytania i deserializacji danych z pliku, a następnie przypisujemy je do zmiennej `data_loaded`.




Serializacja i deserializacja w Pythonie, znane jako piklowanie i odpiklowanie, są potężnymi narzędziami, umożliwiającymi zapis i odtwarzanie stanu obiektów. Dzięki tym procesom, możemy łatwo przechowywać złożone struktury danych lub przesyłać je między różnymi częściami aplikacji. 
> ### Ważne jest jednak, aby pamiętać o potencjalnych zagrożeniach bezpieczeństwa związanych z odczytem niezaufanych danych piklowanych, gdyż deserializacja niebezpiecznych danych może prowadzić do ataków lub niechcianych efektów w programie.

