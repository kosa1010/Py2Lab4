#Serializacja i deserializacja danych

W programowaniu, także w języku Python, często spotyka się pojęcia serializacji i deserializacji. Te techniki są kluczowe, gdy chcemy zapisywać stan obiektu do pliku, aby móc go później odtworzyć, lub przesyłać dane między różnymi programami lub instancjami programu. 

##Serializacja (Piklowanie)
Serializacja, znana w Pythonie jako “piklowanie”, to proces konwersji obiektu w Pythonie do formatu bajtowego, który można zapisać na dysku lub przesłać przez sieć. Operacja ta umożliwia zapis stanu obiektu do pliku, co jest szczególnie przydatne w przypadku przechowywania złożonych struktur danych, takich jak listy, słowniki, a nawet instancje klas.

```python
import pickle

# Definicja prostej struktury danych
data = {"klucz": "wartość", "liczba": 42}

# Piklowanie danych do pliku
with open("data.pickle", "wb") as file:
    pickle.dump(data, file)  # Zapisuje obiekt data do pliku w formacie pickle
```

