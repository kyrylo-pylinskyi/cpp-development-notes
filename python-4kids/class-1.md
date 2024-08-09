# Wprowadzenie

## Dzień dobry
Dzień dobry! 
Mam na imię Kyrylo Pyliskyi i dzisiaj chciałbym opowiedzieć wam o języku Python i programowaniu.

1. **Kreatywność**:
   - Za pomocą programowania możesz realizować swoje pomysły.

2. **Rozwiązywanie problemów**:
   - Programowanie rozwija umiejętności analitycznego myślenia i logicznego rozumowania. 

3. **Możliwość tworzenia czegoś z niczego**:
   - Programowanie daje możliwość tworzenia nowych aplikacji, stron internetowych, gier, a nawet zaawansowanych systemów.

4. **Perspektywy zawodowe**:
   - Umiejętności programistyczne są bardzo cenione na rynku pracy, co zwiększa szanse na znalezienie dobrze płatnej pracy.
   - programowanie jest używane w niemal każdej dziedzinie.

5. **Rozwój technologii**:
   - Znajomość programowania pozwala lepiej rozumieć współczesny świat, który jest coraz bardziej zależny od technologii.
   - Możesz uczestniczyć w rozwijaniu nowych technologii, które mogą mieć znaczący wpływ na przyszłość.
## Czym jest Programowanie?
Programowanie to proces przetwarzania danych. 
Nasz mózg każdą sekundę przetwarza setki różnych informacji. Podobnie działają programy komputerowe - są one jak czarne skrzynki, do których podajemy dane, a w zamian otrzymujemy wynik. Programista to osoba, która tworzy te magiczne czarne skrzynki.

## Wysoki i niski poziom
Programowanie można podzielić na dwa poziomy:
- **Wysoki poziom:** Jest bardziej zrozumiały dla człowieka.
- **Niski poziom:** To poziom pracy z komputerem jak z maszyną, maszyna lepiej rozumie ten poziom.

Kiedy uruchamiamy program, 
komputer wczytuje instrukcje w języku wysokiego poziomu, podobnym do naszego języka, i zamienia je na komendy niskiego poziomu, które komputer rozumie lepiej. Ostatecznie komputer czyta zestaw zer i jedynek jako swoje instrukcje. 

Python jest językiem wysokiego poziomu.

# Język programowania Python
Podobnie jak używamy języków naturalnych, takich jak polski czy angielski, w rozmowie z komputerem używamy języków programowania. W tym kursie będziemy uczyć się języka Python.

- Python jest jednym z najlepszych wyborów dla początkujących.
- Składnia Pythona wygląda bardzo podobnie do języka angielskiego.
- Jest zaprojektowany tak, aby był łatwy do czytania.
- Program w języku Python często można czytać jak książkę.
- Python jest używany w wielu branżach - można programować gry komputerowe, a nawet roboty!

# Repl.it
Najłatwiejszym sposobem, aby zacząć programowanie, jest strona internetowa [repl.it](https://repl.it).

# Pierwszy program

**W pierwszym programie użyjemy standardowego zadania, tj. wydrukujemy linię "Hello World!" na konsoli.**

Aby wykonać to zadanie, należy przesłać **instrukcje** i **dane wejściowe** do maszyny.

Instrukcją (kodem), która przetworzy dane, jest **standardowa** **funkcja** **print()**.

Funkcja **print****()** wypisuje na konsolę elementy znajdujące się między nawiasami. Jeśli są dwa lub więcej elementów, należy je oddzielić przecinkami.

Danymi wejściowymi dla tej funkcji będzie linia **"Hello World**!". Aby jednak maszyna nas zrozumiała i dała poprawny wynik, trzeba jej powiedzieć, jakiego rodzaju są to dane. Rysując analogię do życia, odbieramy informacje za pomocą zmysłów: wzroku, słuchu, węchu itp., więc w programowaniu informacje pochodzą z różnych kanałów i mają różne typy. W naszym przypadku wiersz **"Hello World**!" ma **typ danych**, które przesyłamy - wiersz. Aby maszyna zrozumiała to poprawnie, konieczne jest zawinięcie**"**Hello World!" w pojedyncze lub podwójne cudzysłowy:

`"Hello World!"`
lub:
`'Hello World!'`

Teraz umieśćmy wiersz wewnątrz funkcji **print()**. Umieszczamy kursor w środkowej kolumnie i piszemy:

`print("Hello World!")`
lub:
`print('Hello World!')`

Pozostaje tylko uruchomić kod, klikając przycisk **"Run**" w górnej środkowej części

```python
print("Hello World!")
```

# Zmienne
Zmienne istnieją po to, żeby przechowywać różne wartości przez dłuższy czas i w odpowiednim momencie ich użyć. Na przykład możemy zapisać w programie imię naszego ulubionego bohatera.

**Przy budowaniu programów należy pamiętać, że kod jest wykonywany sekwencyjnie, czyli najpierw zostanie wykonany kod pierwszego wiersza, potem drugiego itd.**


```python
name = "Spider-man"
print(name)
```

Zmienna `name` jest ciągiem znaków, czyli tekstem.
Zmienimy wartość `name` i zobaczymy, co wyświetli konsola:

```python
name = "Aquaman"
print(name)
```

**W ten sposób zmienne znacznie ułatwiają pracę z kodem, czyniąc go _uniwersalnym_.**

**Bądź ostrożny podczas tworzenia zmiennych, ponieważ ich nazwy:**
- mogą zawierać tylko litery alfabetu łacińskiego, liczby i podkreślenia;
- muszą zaczynać się tylko od litery lub podkreślenia. Zabronione jest rozpoczynanie nazwy od cyfry.


Funkcja `print` daje możliwość wyświetlania zmiennych po kolei za pomocą przecinka. Zrobimy następną program:

```python
name = "Spider-man"
print(name, 22)
```

Możemy tworzyć zmienne liczbowe, np. `age`, i tak samo wyświetlać tę zmienną na konsoli:

```python
age = 22
print(age)
```

Zamiast używać magicznej liczby, damy jej nazwę `age`:

```python
name = "Spider-man"
age = 22
print(name, age) 
```

Każda zmienna jest tylko pojemnikiem i może przechowywać różne wartości, jak tekst czy liczby. Na przykład możemy zamienić imię i wiek miejscami:

```python
name = "Spider-man"
print(name)

name = 44
print(name)
```

# Typy danych
Każde dane mają różne typy, możemy sprawdzić typy za pomocą funkcji `type(var)`:

```python
name = "Super-man"
print(name)
print(type(name)) # <class, 'str'>

name = 55
print(name)
print(type(name)) # <class, 'int'>
```

# Dynamiczne typowanie

**dynamiczne typowanie jest jedną z głównych cech Pythona**

Jak zauważyliśmy, zmienna `name` zmieniła swój typ, gdy przypisaliśmy jej wartość liczbową. Tę cechę nazywamy dynamicznym typowaniem i jest to główna cecha języka Python.

# Wprowadzanie danych
Do swoich programów możemy wprowadzać różne dane z klawiatury podczas wykonania za pomocą funkcji `input()`:

```python
name = input()
print("name -", name)
```

Teraz po uruchomieniu programu możemy wpisać do konsoli imię bohatera z klawiatury. Po tym program kontynuuje swoje wykonanie i wypisze imię na konsolę.

Ale czegoś brakuje w naszym kodzie. Konsola nie powiedziała nam, jakich danych oczekuje. Tę wiadomość możemy wpisać do `input("message")`:

```python
name = input("Wprowadź imię superbohatera: ")
print("name -", name)
```

Spróbujemy dodać wiek naszemu superbohaterowi:

```python
name = input("Wprowadź imię superbohatera: ")
age = input("Wprowadź jego wiek: ")
print("name -", name, "wiek -", age)
```

**Jak widzimy, teraz każdy może pracować z naszym programem!**

---

W tej lekcji dowiedzieliśmy się, jak pracować z usługą repl.it i zaczęliśmy poznawać Pythona. Stworzyliśmy nasze pierwsze programy i uczyniliśmy je uniwersalnymi i zrozumiałymi. Nowe i jeszcze bardziej możliwości Pythona czekają na nas w kolejnych lekcjach!

---

### Dodatkowe wskazówki
- Staraj się angażować uczniów, pytając ich o przykłady z życia codziennego, które mogą porównać do programowania.
- Zachęcaj dzieci do eksperymentowania z kodem i zadawania pytań.
- Upewnij się, że wszyscy uczniowie mają dostęp do repl.it i potrafią się na nim poruszać.

Powodzenia na pierwszych zajęciach!