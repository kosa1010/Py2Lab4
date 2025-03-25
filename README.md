# Serializacja i deserializacja danych

W programowaniu, także w języku Python, często spotyka się pojęcia serializacji i deserializacji. Te techniki są kluczowe, gdy chcemy zapisywać stan obiektu do pliku, aby móc go później odtworzyć, lub przesyłać dane między różnymi programami lub instancjami programu. 

## Serializacja (inaczej marshalling, pickling lub flattening)
Serializacja, znana w Pythonie jako “piklowanie”, to proces konwersji obiektu w Pythonie do formatu bajtowego, który można zapisać na dysku lub przesłać przez sieć. Operacja ta umożliwia zapis stanu obiektu do pliku, co jest szczególnie przydatne w przypadku przechowywania złożonych struktur danych, takich jak listy, słowniki, a nawet instancje klas. Dane zapisane
w pliku mogą później posłużyć do odtworzenia stanu programu przy jego kolejnym uruchomieniu.

W Pythonie najpopularniejsze biblioteki do serializacji to:
* pickle - pozwala serializować i deserializować praktycznie dowolne obiekty Pythona.
* json - obsługuje tylko podstawowe typy danych (słowniki, listy, napisy, liczby, wartości logiczne i None), ale jest czytelny dla człowieka.

### Przykłady serializacji i deserializacji

Funkcja dumps() pozwala na serializację obiektu do ciągu bajtów. Ciąg bajtów można zapisać do pliku lub przesłać przez sieć.
```python
import pickle
phone_book = {"Jonna": "542124",
 "Maciej": "542323",
 }
bytes = pickle.dumps(phone_book)
```

Zapisanie danych do pliku możemy zrealizować za_pomocą funkcji `dump()`.
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

Jak zostało wspomniane wcześniej do serializacji podstawowych typów danych wystrczy wykorzystać bibliotekę `json` lecz nic nie stoi na przeszkodzie aby wykorzytać bibliotekę `pickle`. 

### Serializacja i deserializacja za pomocą `pickle`
```python
import pickle

# Tworzymy przykładowe dane
dane = {"imie": "Anna", "wiek": 25, "miasto": "Warszawa"}

# Serializacja do pliku
with open("dane.pkl", "wb") as plik:
    pickle.dump(dane, plik)

# Deserializacja z pliku
with open("dane.pkl", "rb") as plik:
    wczytane_dane = pickle.load(plik)

print(wczytane_dane)  # {'imie': 'Anna', 'wiek': 25, 'miasto': 'Warszawa'}
```
W powyższym kodzie należy wzrócic uwagę na:
* `pickle.dump(dane, plik)` zapisuje dane do pliku w postaci binarnej.
* `pickle.load(plik)` wczytuje dane z pliku i przywraca oryginalny obiekt.

### Serializacja i deserializacja za pomocą `json`
```python
import json

# Przykładowy obiekt Pythonowski
dane = {"nazwa": "Laptop", "cena": 3200.99, "dostepny": True}

# Serializacja do pliku JSON
with open("dane.json", "w") as plik:
    json.dump(dane, plik, indent=4)

# Deserializacja z pliku JSON
with open("dane.json", "r") as plik:
    wczytane_dane = json.load(plik)

print(wczytane_dane)  # {'nazwa': 'Laptop', 'cena': 3200.99, 'dostepny': True}
```
W powyższym kodzie należy wzrócic uwagę na:
* `json.dump(dane, plik, indent=4)` zapisuje dane do pliku w czytelnej formie.
* `json.load(plik)` odczytuje dane z pliku JSON.

### Serializacja złożonych obiektów (niestandardowa klasa)
```Python
import pickle

class Osoba:
    def __init__(self, imie, wiek):
        self.imie = imie
        self.wiek = wiek
    
    def __repr__(self):
        return f"Osoba(imie={self.imie}, wiek={self.wiek})"

# Tworzymy obiekt
osoba = Osoba("Jan", 30)

# Serializacja
with open("osoba.pkl", "wb") as plik:
    pickle.dump(osoba, plik)

# Deserializacja
with open("osoba.pkl", "rb") as plik:
    wczytana_osoba = pickle.load(plik)

print(wczytana_osoba)  # Osoba(imie=Jan, wiek=30)
```
Można serializować niestandardowe klasy w Pythonie przy użyciu `pickle`.
Należy jednak pamiętać, że `pickle` nie jest bezpieczne dla danych z niezaufanych źródeł.

Serializacja i deserializacja w Pythonie, są potężnymi narzędziami, umożliwiającymi zapis i odtwarzanie stanu obiektów. Dzięki tym procesom, możemy łatwo przechowywać złożone struktury danych lub przesyłać je między różnymi częściami aplikacji. 
> ### Ważne jest jednak, aby pamiętać o potencjalnych zagrożeniach bezpieczeństwa związanych z odczytem niezaufanych danych piklowanych, gdyż deserializacja niebezpiecznych danych może prowadzić do ataków lub niechcianych efektów w programie.

## Zadania do wykonania
:one: Serializacja i deserializacja JSON:
* Utwórz skrypt, który zapisuje listę produktów (każdy produkt to słownik zawierający nazwa, cena, dostepnosc) do pliku JSON i potem je z niego odczytuje.
  
:two: Serializacja i deserializacja klasy:
* Stwórz klasę Samochod z polami marka, model, rocznik i zapisz obiekt tej klasy do pliku `*.pickle`.
* Odczytaj obiekt z pliku i wyświetl jego wartości.
  
:three:Zastosowanie `json.dumps()` i `json.loads()`:
* Napisz program, który konwertuje słownik na format JSON przy użyciu `json.dumps()`, a następnie odczytuje go przy użyciu `json.loads()`.
  
:four:Obsługa błędów:
* Dodaj obsługę błędów dla przypadków, gdy plik nie istnieje lub dane są w niepoprawnym formacie.
