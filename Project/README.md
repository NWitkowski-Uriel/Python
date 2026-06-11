# Analiza giełdowa spółek GPW w Pythonie

Projekt zaliczeniowy z języka Python poświęcony podstawowej analizie danych giełdowych wybranych spółek notowanych na Giełdzie Papierów Wartościowych w Warszawie. Program pobiera dane historyczne z serwisu Yahoo Finance przy użyciu biblioteki `yfinance`, przetwarza je z wykorzystaniem `pandas`, a następnie generuje zestaw tabel i wykresów opisujących zachowanie cen akcji, stopy zwrotu, ryzyko oraz prostą strategię inwestycyjną opartą na przecięciu średnich kroczących.

## Autor

Nikodem Witkowski

## Cel projektu

Celem projektu jest pokazanie, jak za pomocą Pythona można przeprowadzić podstawową analizę finansową danych giełdowych. Projekt obejmuje zarówno pobranie danych, ich obróbkę tabelaryczną, jak i wizualizację wyników.

Analizowane są wybrane spółki GPW:

* CD Projekt — `CDR.WA`,
* PKO BP — `PKO.WA`,
* KGHM — `KGH.WA`,
* Orlen — `PKN.WA`,
* PGE — `PGE.WA`.

Dane są pobierane od dnia `2020-01-01` do najnowszej dostępnej daty.

## Zakres analizy

Projekt wykonuje następujące elementy:

1. Pobranie dziennych danych giełdowych z Yahoo Finance.
2. Zapis danych każdej spółki do pliku `.csv`.
3. Obliczenie dziennych stóp zwrotu.
4. Obliczenie skumulowanej stopy zwrotu.
5. Wyznaczenie średnich kroczących MA20, MA50 i MA200.
6. Obliczenie kroczącej zmienności rocznej w oknie 20 sesji.
7. Obliczenie obsunięcia kapitału, czyli drawdown.
8. Wyznaczenie macierzy korelacji dziennych stóp zwrotu.
9. Przygotowanie tabeli podsumowującej wyniki dla każdej spółki.
10. Porównanie rocznej stopy zwrotu i ryzyka.
11. Przetestowanie prostej strategii inwestycyjnej MA20/MA50.
12. Porównanie strategii MA20/MA50 ze strategią „kup i trzymaj”.

## Wykorzystywane biblioteki

Projekt korzysta z następujących bibliotek Pythona:

```python
numpy
pandas
matplotlib
yfinance
```

## Instalacja wymaganych bibliotek

Przed uruchomieniem projektu należy zainstalować wymagane pakiety:

```bash
pip install numpy pandas matplotlib yfinance
```

## Uruchomienie projektu

Plik projektu ma strukturę zgodną z notatnikiem lub skryptem wykonywanym sekcjami. Można go uruchomić w środowisku obsługującym komórki `# %%`, na przykład w Visual Studio Code, Jupyter Notebook albo JupyterLab.

Przykładowe uruchomienie w terminalu:

```bash
python Analysis
```

W przypadku zmiany nazwy pliku na `Analysis.py`:

```bash
python Analysis.py
```

## Struktura projektu

```text
Project/
│
├── Analysis
│   └── główny plik z kodem analizy giełdowej
│
└── wyniki_analizy_giełdowej/
    └── katalog z wygenerowanymi plikami CSV oraz wykresami PNG
```

## Generowane wyniki

Po uruchomieniu program tworzy katalog:

```text
wyniki_analizy_gieldowej/
```

W katalogu tym zapisywane są dane wejściowe, tabele podsumowujące oraz wykresy.

Przykładowe pliki wynikowe:

```text
01_ceny_zamkniecia.png
02_ceny_znormalizowane.png
03_srednie_kroczace_CDR_WA.png
04_dzienne_stopy_zwrotu.png
05_histogram_stop_zwrotu_CDR_WA.png
06_zmiennosc_kroczaca.png
07_obsuniecie_kapitalu.png
08_macierz_korelacji.csv
08_macierz_korelacji.png
09_podsumowanie.csv
10_ryzyko_vs_zwrot.png
11_strategia_ma_CDR_WA.png
12_podsumowanie_strategii.csv
```

## Opis wykonywanych analiz

### Ceny zamknięcia

Pierwsza część analizy przedstawia historyczne ceny zamknięcia akcji wybranych spółek. Pozwala to zobaczyć ogólny trend zmian cen w badanym okresie.

### Ceny znormalizowane

Ceny są normalizowane tak, aby pierwsza obserwacja była równa 100. Dzięki temu można porównać względną zmianę wartości różnych spółek niezależnie od ich początkowej ceny nominalnej.

### Średnie kroczące

Dla każdej spółki obliczane są średnie kroczące:

* MA20 — średnia z 20 sesji,
* MA50 — średnia z 50 sesji,
* MA200 — średnia z 200 sesji.

Średnie kroczące pozwalają wygładzić krótkoterminowe wahania cen i lepiej obserwować średnio- oraz długoterminowy trend.

### Dzienne stopy zwrotu

Projekt oblicza dzienne procentowe zmiany ceny zamknięcia. Stopy zwrotu są następnie przedstawiane na wykresach oraz histogramach, co pozwala porównać rozkład zmian cen dla poszczególnych spółek.

### Zmienność

Zmienność liczona jest jako odchylenie standardowe dziennych stóp zwrotu w oknie 20 sesji, przeskalowane do wartości rocznej przez czynnik `sqrt(252)`. Przyjęto 252 sesje jako przybliżoną liczbę dni giełdowych w roku.

### Obsunięcie kapitału

Drawdown pokazuje, o ile wartość inwestycji spadła względem wcześniejszego maksimum. Jest to jedna z podstawowych miar ryzyka, ponieważ pozwala ocenić największe historyczne spadki wartości kapitału.

### Korelacje

Projekt oblicza macierz korelacji dziennych stóp zwrotu analizowanych spółek. Pozwala to sprawdzić, które spółki zachowywały się podobnie, a które poruszały się bardziej niezależnie.

### Podsumowanie statystyczne

Dla każdej spółki wyznaczane są podstawowe statystyki:

* liczba sesji,
* cena początkowa,
* cena końcowa,
* całkowita stopa zwrotu,
* roczna stopa zwrotu,
* roczna zmienność,
* współczynnik Sharpe’a bez stopy wolnej od ryzyka,
* maksymalne obsunięcie kapitału.

### Strategia MA20/MA50

W projekcie testowana jest prosta strategia oparta na przecięciu średnich kroczących:

* pozycja jest otwierana, gdy MA20 > MA50,
* pozycja nie jest utrzymywana, gdy MA20 <= MA50.

Sygnał jest przesunięty o jeden dzień, aby uniknąć błędu patrzenia w przyszłość. Wynik strategii jest porównywany ze strategią „kup i trzymaj”.

## Uwagi

Projekt ma charakter dydaktyczny i nie stanowi rekomendacji inwestycyjnej. Wyniki zależą od analizowanego okresu, wyboru spółek oraz jakości danych pobranych z Yahoo Finance. Prosta strategia MA20/MA50 została użyta wyłącznie jako przykład implementacji podstawowej logiki inwestycyjnej w Pythonie.

## Możliwe rozszerzenia projektu

Projekt można rozbudować między innymi o:

* analizę większej liczby spółek,
* porównanie z indeksem WIG20,
* uwzględnienie dywidend,
* dodanie stopy wolnej od ryzyka do współczynnika Sharpe’a,
* testowanie innych strategii inwestycyjnych,
* analizę portfela złożonego z kilku spółek,
* interaktywne wykresy z użyciem biblioteki `plotly`,
* automatyczne generowanie raportu końcowego w formacie PDF lub HTML.

## Licencja

Projekt przygotowany jako projekt zaliczeniowy z Pythona.
