# LaTeX — polecenia i przykłady

TeXstudio + MiKTeX · LuaLaTeX

Praktyczne polecenia: zastosowanie, miejsce użycia i kod dla szablonu SZABLON-Projektu.

## Spis treści

- [1. Gdzie zmieniać szablon](#temat-2)
- [2. Pakiety i ścieżki](#temat-3)
- [3. Tekst i nagłówki](#temat-4)
- [4. Listy i układ tekstu](#temat-5)
- [5. Matematyka: podstawy](#temat-6)
- [6. Matematyka: gotowe wzorce](#temat-7)
- [7. Tabela: podstawowy wzorzec](#temat-8)
- [8. Tabele: scalanie i długi tekst](#temat-9)
- [9. Rysunek z pliku i odwołania](#temat-10)
- [10. Kod Python i C](#temat-11)
- [11. TikZ: figury i połączenia](#temat-12)
- [12. TikZ: schemat sortowania](#temat-13)
- [13. PGFPlots: wykres funkcji](#temat-14)
- [14. PGFPlots: dwie serie z CSV](#temat-15)
- [15. Wykresy: szybkie modyfikacje](#temat-16)
- [16. Bibliografia i składanie plików](#temat-17)
- [17. Własne polecenia i Beamer](#temat-20)

<a id="temat-2"></a>

## 1. Gdzie zmieniać szablon

| Plik | Zastosowanie |
| --- | --- |
| main.tex | Łączy projekt; kolejność \\include, dodatki do preambuły. |
| config/metadata.tex | Tytuł, autor, album, przedmiot, data i przełączniki wykazów. |
| config/project-style.sty | Gotowy wygląd, pakiety i style listingów. Najczęściej tylko sprawdzasz zawartość. |
| chapters/03-koncepcja-i-projekt.tex | Możesz tu umieścić opis algorytmu i diagram. |
| chapters/04-realizacja.tex | Implementacja i listingi programów. |
| chapters/05-weryfikacja-i-wyniki.tex | Tabele, wykresy i ich omówienie. |
| literatura.bib | Wpisy bibliograficzne używane przez \\cite. |
| backmatter/\*.tex | Istniejące części końcowe projektu. |

### Metadane: zmieniasz wartość istniejącego polecenia

```latex
\newcommand{\projecttitle}{Analiza sortowania}
\newcommand{\coursetitle}{Narzędzia informatyczne}
\newcommand{\programme}{Informatyka}
\newcommand{\projectauthors}{%
  Szymon Głogowski & 123456 \\
}
\newcommand{\projectpdfauthors}{Szymon Głogowski}
\newcommand{\submissiondate}{22.11.2026}
\newcommand{\projectstatus}{draft}
```

Numer albumu jest przykładowy. W projectauthors znak & rozdziela kolumny, a \\\\ kończy wiersz; w projectpdfauthors wpisz zwykły tekst. Nie dopisuj drugiej definicji tego samego polecenia. Tryb final uruchamia kontrolę wymaganych metadanych.

### Wykazy: w metadata.tex zamień false na true

```latex
\newcommand{\showlistoffigures}{true}
\newcommand{\showlistoftables}{true}
\newcommand{\showlistoflistings}{true}
```

main.tex już generuje odpowiednie wykazy. Obiekty muszą mieć podpisy, a po zmianach trzeba ponowić kompilację.

<a id="temat-3"></a>

## 2. Pakiety i ścieżki

### Co jest już w przesłanym szablonie

graphicx, adjustbox, amsmath, booktabs, array, tabularx, longtable, siunitx, enumitem, caption, subcaption, listings, xcolor, hyperref, cleveref oraz biblatex z backendem biber. Nie dodawaj ich drugi raz, zwłaszcza z innymi opcjami.

### Dodatki do preambuły main.tex, gdy są potrzebne

```latex
\usepackage{config/project-style} % już istnieje
% Dopisz poniższe tylko raz, przed \begin{document}:
\usepackage{multirow} % scalanie wierszy tabeli
\usepackage{tikz}
\usetikzlibrary{positioning,shapes.geometric,arrows.meta}
\usepackage{pgfplots}
\pgfplotsset{compat=1.18}
% \usepackage{float} % tylko jeśli potrzebujesz [H]
```

W podobnym szablonie najpierw sprawdź, co jest załadowane. W pliku .sty pakiety są dodawane przez \\RequirePackage; przy zwykłej pracy w main.tex używaj \\usepackage.

### Przygotuj pliki: proste nazwy bez spacji

```text
main.tex
config/metadata.tex
chapters/04-realizacja.tex
chapters/05-weryfikacja-i-wyniki.tex
figures/wykres_sortowania.png
code/bubble_sort.py
code/max_element.c
data/dane_porownawcze.csv
data/dane_czasow.csv
```

To proponowane miejsca na kopie załączników, które sam dodasz do projektu. Zmień nazwy kopii: usuń „ (2)”, „ (4)” itp. Przykłady w poradniku zakładają właśnie taki układ.

```latex
\includegraphics{figures/wykres_sortowania.png}
\lstinputlisting{code/bubble_sort.py}
% Ścieżki w tych przykładach liczymy od katalogu main.tex.
% W LaTeX używaj /, nie windowsowego \ w ścieżkach.
```

Zmiana nazwy pliku wymaga zmiany odwołania w kodzie. Do kompilacji na innym komputerze potrzebujesz całego projektu, a nie samego main.tex.

<a id="temat-4"></a>

## 3. Tekst i nagłówki

### Treść rozdziału: struktura jest numerowana automatycznie

```latex
\chapter{Algorytmy sortowania}
\label{chap:sortowanie}
\section{Sortowanie bąbelkowe}
\label{sec:bubble}
\subsection{Zasada działania}
Porównujemy pary sąsiednich elementów.

Nowy akapit powstaje po pustym wierszu.
\subsubsection{Przykład}
Tekst przykładu.
```

W istniejącym pliku zazwyczaj zachowujesz jeden \\chapter i dopisujesz sekcje. Nie wpisuj numerów do tytułów: szablon sam utworzy np. 4.1 i 4.1.1. Polecenie \\section\*\{Tytuł\} tworzy sekcję bez numeru i domyślnie bez wpisu w spisie.

```latex
\textbf{pogrubienie}, \textit{kursywa}, \emph{wyróżnienie}
\texttt{nazwa funkcji}, \underline{podkreślenie}
\textcolor{blue}{niebieski tekst}
\enquote{Cytowany fragment}
Wartość wynosi 50\%, a nazwa to plik\_wynikowy.
Zapis R\&D, koszt 10\$, znak \# i nawiasy \{ \}.
Ukośnik: \textbackslash{}, tylda: \textasciitilde{}.
Daszek: \textasciicircum{}.
% Komentarz: od znaku procent do końca wiersza.
```

### Znaki, które najczęściej psują kompilację

| W kodzie tekstu | Co oznacza |
| --- | --- |
| % | Komentarz. Literalny procent pisz \\%. |
| & | Podział komórek tabeli. W zdaniu pisz \\&. |
| \_ oraz ^ | Indeks i potęga w matematyce. W nazwie pliku w tekście użyj \\\_ lub \\texttt z ucieczką. |
| \$ | Początek/koniec matematyki. Waluta: \\\$. |
| \{ i \} | Grupowanie argumentów; każda otwarta klamra musi być zamknięta. |

<a id="temat-5"></a>

## 4. Listy i układ tekstu

### Punkty, numeracja, opis pojęć

```latex
\begin{itemize}
  \item Prosta implementacja.
  \item Niska efektywność dla dużych danych.
\end{itemize}

\begin{enumerate}
  \item Porównaj sąsiadów.
  \item Zamień elementy, jeśli są w złej kolejności.
  \item Powtórz przebieg.
\end{enumerate}

\begin{description}
  \item[Wejście] Tablica liczb.
  \item[Wyjście] Tablica uporządkowana.
\end{description}
```

Lista wewnątrz \\item tworzy kolejny poziom. Każdy element zaczyna się od \\item; samo napisanie „1.” nie daje automatycznej numeracji.

```latex
% Opcje enumitem (pakiet już dostępny):
\begin{enumerate}[label=\alph*),start=3]
  \item Ten punkt otrzyma oznaczenie c).
\end{enumerate}

\noindent Akapit bez wcięcia.
Pierwszy wiersz.\\
Drugi wiersz tego samego akapitu.

\begin{center}Krótki tekst na środku.\end{center}
\begin{flushright}Tekst do prawej.\end{flushright}
\newpage % nowa strona
% \clearpage % nowa strona i umieszczenie zaległych figur/tabel
```

### Drobne rzeczy, które przydają się w praktyce

Tylda ~ daje spację nierozdzielającą: rys.~\\ref\{fig:czas\}, w~tabeli, 10~ms. Pusta linia daje nowy akapit. Sam Enter w kodzie zwykle daje tylko spację w PDF. Nie rób odstępów wieloma spacjami ani wieloma \\\\; do akapitów używaj pustej linii.

```latex
\footnote{Treść przypisu na dole strony.}
\url{https://example.com}
\href{https://example.com}{Opis odnośnika}
{\small Ten fragment jest mniejszy.} Dalej zwykły rozmiar.
```

<a id="temat-6"></a>

## 5. Matematyka: podstawy

### W zdaniu, osobno, z numerem

```latex
W najgorszym przypadku koszt wynosi $O(n^2)$.
Warunek zamiany to \(a_i > a_{i+1}\).

\[
  S = \sum_{i=1}^{n} a_i
\]

\begin{equation}
  C(n) = \frac{n(n-1)}{2}
  \label{eq:porownania}
\end{equation}
Wzór~\eqref{eq:porownania} opisuje liczbę porównań.
```

\\\[ ... \\\] nie numeruje. equation numeruje; etykieta jest wewnątrz równania. \\eqref dodaje nawiasy do numeru. Nie otaczaj equation znakami \$ ani \\\[. W szablonie numer równania obejmuje numer rozdziału.

| Chcę zapisać | Kod wewnątrz trybu matematycznego |
| --- | --- |
| Indeksy i potęgi | a\_i, a\_\{i+1\}, x^2, x^\{n+1\} |
| Ułamek i pierwiastek | \\frac\{a+b\}\{c\}, \\sqrt\{x\}, \\sqrt\[3\]\{x\} |
| Symbole greckie | \\alpha, \\beta, \\gamma, \\Delta, \\pi |
| Porównania | \\leq, \\geq, \\neq, \\approx, =, \<, \> |
| Zbiory i logika | x\\in A, A\\subseteq B, \\forall x, \\exists x |
| Strzałki i nieskończoność | \\to, \\Rightarrow, \\infty |
| Mnożenie i odstęp | a\\cdot b, a\\times b, a\\,b |
| Nawiasy dopasowane | \\left(\\frac\{a\}\{b\}\\right) |
| Funkcje i zwykły tekst | \\sin x, \\cos x, \\log n, \\text\{dla \} n\>0 |

Klamry w a\_\{i+1\} grupują cały indeks. Zapis a\_i+1 oznacza coś innego. Funkcje pisz \\sin i \\log, aby ich nazwy miały poprawną czcionkę i odstępy.

<a id="temat-7"></a>

## 6. Matematyka: gotowe wzorce

### Wzory wymagane w laboratorium

```latex
\[
S = \sum_{i=1}^{n} a_i
\]
\[
f(x)=x^3+2x^2-5x,\qquad f'(x)=3x^2+4x-5
\]
\[
\int_0^1 x^2\,\mathrm{d}x=\frac{1}{3}
\]
```

### Kilka równań: wyrównanie względem znaku =

```latex
\begin{align}
  f(x)  &= x^3+2x^2-5x \label{eq:funkcja} \\
  f'(x) &= 3x^2+4x-5   \label{eq:pochodna}
\end{align}
% align* zamiast align usuwa numerację obu wierszy.
% \notag przed \\ usuwa numer wybranego wiersza.
```

### Macierz, funkcja przedziałami, granica

```latex
\[
A=\begin{pmatrix}
1 & 2 \\
3 & 4
\end{pmatrix}
\qquad
|x|=\begin{cases}
x & \text{dla } x\geq 0, \\
-x & \text{dla } x<0.
\end{cases}
\]
\[
\lim_{n\to\infty}\frac{1}{n}=0,
\qquad \vec{v}=(v_1,v_2),\qquad \max_{1\leq i\leq n} a_i
\]
```

W align i macierzach & ustala wyrównanie/kolumny, a \\\\ kończy wiersz. Używaj amsmath, już obecnego w szablonie. Nie stosuj przestarzałego eqnarray.

### Liczby z jednostkami: siunitx już jest dostępny

```latex
Czas wynosi \qty{35.2}{\milli\second}.
Napięcie wynosi \qty{230}{\volt}, udział \qty{50}{\percent}.
Liczba: \num{12345.67}.
```

<a id="temat-8"></a>

## 7. Tabela: podstawowy wzorzec

Treść rozdziału. table daje podpis i numer obiektu, tabular ustala komórki. Dane są syntetycznymi wartościami dydaktycznymi z załączników.

```latex
\begin{table}[htbp]
  \centering
  \caption{Porównanie przykładowych wyników sortowania}
  \label{tab:sortowanie}
  \small
  \begin{tabular}{rrrrr}
    \toprule
    $n$ & Bubble [ms] & Insertion [ms]
        & Por. Bubble & Por. Insertion \\
    \midrule
    100  & 0,4   & 0,2   & 4950     & 2600 \\
    500  & 8,9   & 4,1   & 124750   & 65000 \\
    1000 & 35,2  & 16,3  & 499500   & 260000 \\
    2000 & 141,5 & 65,1  & 1999000  & 1040000 \\
    5000 & 883,7 & 406,4 & 12497500 & 6500000 \\
    \bottomrule
  \end{tabular}
\end{table}
Zestawienie podano w tabeli~\ref{tab:sortowanie}.
```

### Jak zmieniać kolumny i linie

| Składnia | Efekt |
| --- | --- |
| l / c / r | Kolumna do lewej / na środku / do prawej. |
| p\{4cm\} | Stała szerokość; długi tekst jest zawijany. |
| \|l\|c\|r\| | Pionowe kreski; linie poziome daje \\hline. |
| \\toprule, \\midrule, \\bottomrule | Linie booktabs: góra, pod nagłówkiem, dół. |
| & i \\\\ | Przejście do następnej komórki i koniec wiersza. |
| \\caption, \\label | Podpis, potem etykieta. Podpis tabeli zwykle nad nią. |

Przy 5 kolumnach zwykły wiersz ma 4 separatory &. „Extra alignment tab” często oznacza zbyt dużo & albo brak \\\\ w poprzednim wierszu. Nie mieszaj pionowych kresek z estetyką booktabs bez potrzeby.

<a id="temat-9"></a>

## 8. Tabele: scalanie i długi tekst

### Dwupoziomowy nagłówek: dodaj pakiet multirow

```latex
\begin{table}[htbp]
\centering
\caption{Czasy i liczby porównań}
\label{tab:scalona}
\begin{tabular}{|r|r|r|r|r|}
\hline
\multirow{2}{*}{$n$}
 & \multicolumn{2}{c|}{Czas [ms]}
 & \multicolumn{2}{c|}{Liczba porównań} \\
\cline{2-5}
 & Bubble & Insertion & Bubble & Insertion \\
\hline
100 & 0,4 & 0,2 & 4950 & 2600 \\
500 & 8,9 & 4,1 & 124750 & 65000 \\
\hline
\end{tabular}
\end{table}
```

\\multicolumn\{2\}\{c\|\}\{...\} zajmuje 2 kolumny. \\multirow\{2\}\{\*\}\{...\} zajmuje 2 wiersze. W drugim wierszu pozostaw pustą pierwszą komórkę, dlatego zaczyna się od &. \\cline\{2-5\} rysuje linię tylko pod kolumnami 2-5.

### Tabela na szerokość tekstu: tabularx

```latex
\begin{tabularx}{\linewidth}{lXr}
\toprule
Algorytm & Opis & Koszt \\
\midrule
Bubble & Porównuje sąsiednie elementy i zamienia je
         przy niewłaściwej kolejności. & $O(n^2)$ \\
\bottomrule
\end{tabularx}
```

X dobiera szerokość i zawija tekst. Otocz tę konstrukcję table, jeśli ma mieć podpis i numer. Do wielostronicowej tabeli służy longtable; nie umieszczaj jej wewnątrz table.

### Gdy tabela wychodzi za margines

Najpierw skróć nagłówki, użyj p\{...\}/X, zmniejsz lokalnie czcionkę przez \\small albo odstępy \\setlength\{\\tabcolsep\}\{4pt\} w grupie. Awaryjnie: \\resizebox\{\\linewidth\}\{!\}\{...tabular...\}; nadmierne skalowanie pogarsza czytelność.

<a id="temat-10"></a>

## 9. Rysunek z pliku i odwołania

### Kopia załączonego PNG w figures/wykres_sortowania.png

```latex
\begin{figure}[htbp]
  \centering
  \includegraphics[width=0.8\linewidth]
    {figures/wykres_sortowania.png}
  \caption{Przykładowa zależność czasu sortowania
           od liczby elementów}
  \label{fig:czas}
\end{figure}
Na rys.~\ref{fig:czas} pokazano dane dydaktyczne.
% W tym szablonie także: \cref{fig:czas}
```

Przykład wstawia gotową grafikę. Gdy zadanie wymaga PGFPlots lub TikZ, użyj odpowiedniego kodu, nie PNG. Dostarczony PNG pokazuje tylko Bubble Sort.

### Pomocnicze polecenie szablonu

```latex
% Zamiast \includegraphics, w tym samym figure:
\projectgraphic[width=0.8\linewidth]
  {figures/wykres_sortowania.png}
```

projectgraphic ogranicza maksymalny rozmiar i zachowuje proporcje. \\linewidth to szerokość aktualnego miejsca; \\textwidth to szerokość całego pola tekstu. Opcja height=... ustawia wysokość; przy width i height jednocześnie użyj keepaspectratio.

### Podpis → etykieta → odwołanie

```latex
\caption{Opis obiektu}
\label{fig:unikalna-nazwa}
% W dowolnym miejscu tekstu:
rys.~\ref{fig:unikalna-nazwa}
strona~\pageref{fig:unikalna-nazwa}
\cref{fig:unikalna-nazwa}
```

ref daje sam numer; cref dobiera też nazwę rodzaju obiektu. Prefiksy fig:, tab:, eq:, lst:, sec: pomagają zachować porządek. Każda etykieta musi być unikalna. Gdy pojawia się ??, skompiluj ponownie i sprawdź pisownię klucza.

### Dlaczego rysunek „ucieka”?

\[htbp\] dopuszcza kolejno miejsce w pobliżu kodu, górę, dół i osobną stronę z obiektami. To sugestia. \[H\] wymaga pakietu float i wymusza pozycję, ale może tworzyć duże puste obszary. \\clearpage wypisuje oczekujące obiekty i zaczyna nową stronę.

<a id="temat-11"></a>

## 10. Kod Python i C

### Wariant A: kod wpisany do rozdziału

```latex
\begin{lstlisting}[style=project-python,
  caption={Zamiana sąsiednich elementów},
  label={lst:zamiana}]
for i in range(len(a) - 1):
    if a[i] > a[i + 1]:
        a[i], a[i + 1] = a[i + 1], a[i]
\end{lstlisting}
Fragment pokazano w listingu~\ref{lst:zamiana}.
```

### Wariant B: kod pobierany z pliku

```latex
\lstinputlisting[
  style=project-python,
  caption={Sortowanie bąbelkowe},
  label={lst:bubble}
]{code/bubble_sort.py}

\lstinputlisting[
  style=project-c,
  caption={Wyszukiwanie maksimum},
  label={lst:max},
  firstline=1,lastline=12
]{code/max_element.c}
```

firstline i lastline wybierają wiersze pliku. Ich wartości dopasuj do faktycznej zawartości. Po zmianie pliku .py/.c zapisz go i ponownie kompiluj LaTeX. Listing pokazuje kod; nie uruchamia programu i nie wylicza wyniku.

### Opcje, które możesz dopisać do listingu

```latex
numbers=left,       % numery po lewej
firstnumber=1,      % początek numeracji
stepnumber=1,       % numeruj każdy wiersz
frame=single,       % ramka
breaklines=true,    % zawijaj długie linie
basicstyle=\ttfamily\small
```

Opcje oddzielaj przecinkami wewnątrz \[...\]. Szablon ma style project-python, project-c, project-cpp, project-matlab i project-shell. W lstlisting nie zamieniaj \_ na \\\_ ani % na \\%: treść jest kodem dosłownym. Nie pakuj lstlisting do argumentu \\textbf\{...\}.

<a id="temat-12"></a>

## 11. TikZ: figury i połączenia

Preambuła: tikz i biblioteki positioning, shapes.geometric, arrows.meta z części „Pakiety i ścieżki”. Treść rozdziału:

```latex
\begin{figure}[htbp]
\centering
\begin{tikzpicture}[
  node distance=10mm,
  box/.style={draw,rectangle,rounded corners,
              minimum width=35mm,minimum height=9mm},
  arr/.style={-{Stealth},thick}
]
  \node[box,fill=blue!10] (a) {Dane wejściowe};
  \node[box,below=of a] (b) {Przetwarzanie};
  \node[draw,ellipse,below=of b] (c) {Wynik};
  \draw[arr] (a) -- (b);
  \draw[arr] (b) -- node[right]{zapis} (c);
\end{tikzpicture}
\caption{Przepływ danych}
\label{fig:przeplyw}
\end{figure}
```

| Element | Co zmieniasz |
| --- | --- |
| \\node\[opcje\] (id) \{tekst\}; | Tworzy węzeł; id służy do połączeń i pozycjonowania. |
| rectangle / ellipse / diamond | Prostokąt, elipsa, romb. |
| below=of a / right=of a | Ułożenie względem węzła a; wymaga positioning. |
| draw, fill=green!15 | Obrys i wypełnienie. |
| text width=3cm, align=center | Zawijanie i wyrównanie tekstu w węźle. |
| (a.south), (b.north) | Dolna i górna kotwica węzła. |
| -- / \|- / -\| | Linia prosta / najpierw pionowo / najpierw poziomo. |

### Rysowanie we współrzędnych

```latex
\begin{tikzpicture}
\draw[->] (0,0) -- (3,0) node[right] {$x$};
\draw[blue,thick] (0,0) rectangle (2,1);
\draw[red] (1,2) circle (0.4);
\node at (1,0.5) {Prostokąt};
\end{tikzpicture}
```

Każde \\node i \\draw kończ średnikiem. Brak średnika często powoduje błąd dopiero przy następnej instrukcji.

<a id="temat-13"></a>

## 12. TikZ: schemat sortowania

Pełny wzorzec do ćwiczenia zmian węzłów i strzałek. Przebieg sprawdza wszystkie sąsiednie pary; jeśli wykonano zamianę, algorytm powtarza przebieg.

```latex
\begin{figure}[htbp]
\centering
\begin{tikzpicture}[
 node distance=9mm,
 op/.style={draw,rectangle,text width=42mm,
   align=center,minimum height=10mm},
 term/.style={draw,ellipse,minimum width=24mm,
   minimum height=8mm},
 dec/.style={draw,diamond,aspect=2,text width=27mm,
   align=center,inner sep=1pt},
 arr/.style={-{Stealth},thick}
]
\node[term] (start) {Start};
\node[op,below=of start] (input) {Pobierz tablicę};
\node[op,below=of input] (pass)
  {Wykonaj pełny przebieg porównań i zamian};
\node[dec,below=of pass] (test) {Czy wykonano zamianę?};
\node[term,below=of test] (stop) {Koniec};
\draw[arr] (start) -- (input);
\draw[arr] (input) -- (pass);
\draw[arr] (pass) -- (test);
\draw[arr] (test) -- node[right]{Nie} (stop);
\draw[arr] (test.east) -- ++(18mm,0)
  node[midway,below]{Tak} |- (pass.east);
\end{tikzpicture}
\caption{Schemat blokowy sortowania bąbelkowego}
\label{fig:schemat-bubble}
\end{figure}
Schemat przedstawiono na rys.~\ref{fig:schemat-bubble}.
```

### Jak dostosować schemat do innego zadania

Zmień tekst w \{...\}, kształt przez styl, odstępy przez node distance. Nowy węzeł potrzebuje unikalnego id i strzałek. Nie wystarczy zmienić podpisu „Tak/Nie”: sprawdź, czy kierunek strzałki odpowiada logice warunku.

Rozszerzenie n \< 2: po wczytaniu dodaj romb z tym warunkiem. Gałąź „Tak” prowadzi do końca, „Nie” do przebiegu. Zmniejsz text width lub odstępy, jeśli diagram przekracza marginesy; samo scale bez transform shape nie skaluje tekstów węzłów.

<a id="temat-14"></a>

## 13. PGFPlots: wykres funkcji

Preambuła: \\usepackage\{pgfplots\} i \\pgfplotsset\{compat=1.18\}. W treści używasz figure → tikzpicture → axis → addplot.

```latex
\begin{figure}[htbp]
\centering
\begin{tikzpicture}
\begin{axis}[
  width=0.85\linewidth,height=6cm,
  xlabel={$x$},ylabel={$f(x)$},
  domain=-2:4,samples=100,
  xmin=-2,xmax=4,
  grid=both,
  legend pos=north west
]
\addplot[blue,very thick] {x^2-2*x-3};
\addlegendentry{$f(x)=x^2-2x-3$}
\end{axis}
\end{tikzpicture}
\caption{Wykres funkcji kwadratowej}
\label{fig:funkcja}
\end{figure}
```

### Najważniejsza różnica: wzór osi a wzór obliczany

W xlabel/ylabel i legendzie możesz pisać LaTeX, np. \{\$x^2\$\}. W \{x^2-2\*x-3\} podajesz wyrażenie obliczane przez PGF: mnożenie zapisuj \*, potęgę ^. Dla pierwiastka użyj sqrt(x), dla e do potęgi exp(x), dla logarytmu ln(x). Funkcje sin/cos domyślnie liczą kąt w stopniach; dla argumentu w radianach można użyć sin(deg(x)).

| Opcja | Znaczenie |
| --- | --- |
| domain=-2:4 | Zakres argumentów obliczanej funkcji. |
| samples=100 | Liczba próbek funkcji; nie dodaje punktów do CSV. |
| xmin/xmax, ymin/ymax | Widoczny zakres osi; może ukryć część danych. |
| grid=major / both | Siatka główna / główna i pomocnicza. |
| very thick, dashed, red | Grubość, kreskowanie i kolor linii. |
| legend pos=north west | Legenda w lewym górnym rogu. |

Kontrola dla tej funkcji: minimum jest w (1, -4), miejsca zerowe w -1 i 3. Jeśli wykres wygląda inaczej, sprawdź wzór, mnożenie oraz zakres osi.

<a id="temat-15"></a>

## 14. PGFPlots: dwie serie z CSV

Skopiuj dane\_porownawcze (4).csv do data/dane\_porownawcze.csv. Plik ma przecinki między kolumnami i kropki dziesiętne. Pierwszy wiersz:

```csv
n,bubble_ms,insertion_ms,bubble_porownania,insertion_porownania
```

```latex
\begin{figure}[htbp]
\centering
\begin{tikzpicture}
\begin{axis}[
 width=0.85\linewidth,height=6cm,
 xlabel={Liczba elementów $n$},
 ylabel={Czas wykonania [ms]},
 grid=major,legend pos=north west,
 scaled x ticks=false
]
\addplot[blue,thick,mark=*]
 table[col sep=comma,x=n,y=bubble_ms]
 {data/dane_porownawcze.csv};
\addlegendentry{Bubble Sort}
\addplot[red,very thick,dashed,mark=square*]
 table[col sep=comma,x=n,y=insertion_ms]
 {data/dane_porownawcze.csv};
\addlegendentry{Insertion Sort}
\end{axis}
\end{tikzpicture}
\caption{Przykładowe czasy wykonania algorytmów sortowania}
\label{fig:csv}
\end{figure}
Na rys.~\ref{fig:csv} pokazano syntetyczne dane dydaktyczne.
```

### Co dokładnie zmieniasz w innym zadaniu

Ścieżka wybiera plik. x=n wybiera kolumnę argumentów, y=bubble\_ms kolumnę wyników. Nagłówki przepisz dokładnie. Drugie addplot dodaje drugą serię; legenda musi mieć tę samą kolejność. Każde addplot kończy się średnikiem.

### Kontrola danych i aktualizacji

Powinno być po 5 punktów każdej serii. Dla n=5000: Bubble 883,7 ms, Insertion 406,4 ms. Zmień jedną wartość w kopii CSV, zapisz i skompiluj. Po sprawdzeniu przywróć wartość. Nie wpisuj danych ręcznie, jeśli polecenie wymaga wczytywania z CSV.

<a id="temat-16"></a>

## 15. Wykresy: szybkie modyfikacje

### Drugi CSV ma inne nazwy kolumn: n i t_ms

```latex
% Wewnątrz istniejącego axis:
\addplot[thick,mark=*]
 table[col sep=comma,x=n,y=t_ms]{data/dane_czasow.csv};

% Liczby porównań z pliku porównawczego:
\addplot[blue,thick,mark=*]
 table[col sep=comma,x=n,y=bubble_porownania]
 {data/dane_porownawcze.csv};
% Zmień też ylabel na Liczba porównań.
% Dla drugiej serii użyj y=insertion_porownania.
```

| Chcę uzyskać | Co dopisać / zmienić |
| --- | --- |
| Same punkty | \\addplot\[only marks,mark=\*,mark size=2pt\] table ...; |
| Bez znaczników | \\addplot\[no marks,thick\] table ...; |
| Inny wygląd | thin, thick, very thick; dashed, dotted; blue, red. |
| Skala logarytmiczna | ymode=log w opcjach axis; wszystkie y muszą być dodatnie. |
| Legenda poza wykresem | legend style=\{at=\{(0.5,-0.22)\},anchor=north,legend columns=2\} |
| Podpisy zamiast addlegendentry | legend entries=\{Bubble Sort,Insertion Sort\} w axis. |
| Wykres słupkowy | ybar w opcjach axis; dopasuj szerokość słupków i znaczniki x. |
| Dane bez nagłówka | x index=0,y index=1 (indeksy kolumn od zera). |
| CSV rozdzielony średnikami | col sep=semicolon; przecinek dziesiętny wymaga osobnego ustawienia parsera. |

### Punkty zapisane bezpośrednio w kodzie

```latex
\addplot[thick,mark=*] coordinates {
 (100,0.4) (500,8.9) (1000,35.2)
};
```

coordinates przydaje się dla krótkiego przykładu, ale nie zastępuje wymaganego importu pliku. Opcja smooth wygładza połączenia; do tych danych najlepiej zachować zwykłe odcinki, aby nie sugerować dodatkowych wartości pomiarowych.

### Oddzielny plik z wykresem

```latex
% Zapisz samo tikzpicture w plots/porownanie.tex.
% W figure w rozdziale zamiast całego tikzpicture:
\input{plots/porownanie.tex}
```

<a id="temat-17"></a>

## 16. Bibliografia i składanie plików

### Cytowanie: szablon ma biblatex + Biber

```latex
% Treść rozdziału:
Opis składu dokumentów podano w pracy~\cite{lamport1994}.
% Wpis lamport1994 jest już w literatura.bib.

% Przykładowy nowy wpis w literatura.bib:
@book{ksiazka2026,
  author = {Jan Kowalski},
  title = {Przykładowa książka},
  year = {2026},
  publisher = {Przykładowe wydawnictwo}
}
```

Przykładowy wpis pokazuje składnię, nie jest rzeczywistą publikacją. Wstawiaj dane używanego źródła. Klucz po @book\{ musi być unikalny i zgodny z kluczem w \\cite. Kilku autorów oddziela się słowem and.

main.tex już zawiera \\addbibresource\{literatura.bib\} oraz \\printprojectbibliography. Nie dodawaj równocześnie \\bibliography i \\bibliographystyle ze starego sposobu pracy. Numeracja cytowań jest automatyczna; spis bibliografii jest uporządkowany według ustawień szablonu.

### Kompilacja z bibliografią

```text
lualatex main.tex
biber main
lualatex main.tex
lualatex main.tex
```

To kolejność narzędzi, którą możesz wykonać z menu TeXstudio. Jeśli po cytowaniu widzisz klucz zamiast numeru, sprawdź wpis .bib i uruchom Biber.

### Dołączanie rozdziału i małego fragmentu

```latex
% main.tex, w części listy rozdziałów:
\include{chapters/08-dodatek}
% chapters/08-dodatek.tex zaczyna się np.:
\chapter{Dodatek}

% Mały fragment w środku rozdziału:
\input{plots/porownanie.tex}
```

include rozpoczyna nową stronę i służy zwykle całym rozdziałom. input wstawia zawartość w bieżącym miejscu. Nie dopisuj nowego \\begin\{document\} w żadnym z tych plików. \\appendix w main.tex przełącza numerację kolejnych rozdziałów na litery.

<a id="temat-20"></a>

## 17. Własne polecenia i Beamer

### Własna komenda: mniej powtarzania

```latex
% Preambuła main.tex: nowa, unikalna nazwa polecenia
\newcommand{\zlozonosc}[1]{\ensuremath{O(#1)}}
% Treść:
Koszt wynosi \zlozonosc{n^2}.
% #1 to pierwszy argument. Nie redefiniuj istniejących
% poleceń szablonu przez kolejne \newcommand.
```

### Beamer: osobny dokument, jeśli zadanie tego wymaga

```latex
\documentclass{beamer}
\usepackage[polish]{babel}
\begin{document}
\begin{frame}{Tytuł slajdu}
  \begin{itemize}
    \item Pierwszy punkt.
    \item Drugi punkt.
  \end{itemize}
\end{frame}
\end{document}
```

Ten przykład uruchamia się jako osobny projekt, nie w rozdziale szablonu report. Przy kodzie dosłownym na slajdzie używa się frame z opcją \[fragile\].
