# Przygotowanie do poprawy — grupa 1

Materiał do ćwiczeń przed poprawą na podstawie dostarczonego wariantu A. Instrukcja zaliczenia zabrania AI podczas pracy ocenianej; przećwicz samodzielne wykonanie i stosuj zasady prowadzącego. To nie jest deklaracja samodzielnego wykonania pracy.

## Kolejność i miejsca zmian

1. Rozpakuj cały SZABLON-Projektu. Otwórz main.tex w TeXstudio. Ustaw LuaLaTeX i Biber. Najpierw skompiluj niezmieniony szablon.
2. W config/metadata.tex zmień istniejące wartości tytułu, autorów, daty i grupy (grupa laboratoryjna 1). Zachowaj nazwy poleceń szablonu. Nie wpisuj przykładowego numeru albumu jako swojego.
3. Skopiuj pomiary.csv obok main.tex, a sortowanie.png do chapters/. Zachowaj dokładne nazwy i wielkość liter.
4. Do preambuły main.tex, przed \\begin{document}, dodaj poniższe pakiety tylko jeśli nie są już ładowane przez config/project-style.sty:

```latex
\usepackage{pgfplots}
\pgfplotsset{compat=1.18}
\newcommand{\pomiar}[2]{\ensuremath{#1\,\mathrm{#2}}}
```

5. W chapters/05-weryfikacja-i-wyniki.tex zastąp przykładową treść kodem poniżej. Zachowaj istniejące dołączenie tego rozdziału w main.tex, nie dodawaj go drugi raz.

```latex
\chapter{Wyniki testów wydajności}
\label{chap:wyniki-poprawa}
Badamy \textbf{czas wykonania algorytmu sortowania}
przy \textit{rosnącej liczbie elementów}.
Dane pochodzą z dostarczonego pliku, nie z pomiarów wykonanych tutaj.
Wyniki zestawiono w tabeli~\ref{tab:pomiary-poprawa}.

\begin{table}[htbp]
\centering
\caption{Czas wykonania algorytmu sortowania}
\label{tab:pomiary-poprawa}
\begin{tabular}{rrr}
\toprule
Lp. & Liczba elementów $N$ [-] & Czas $t$ [ms] \\
\midrule
1 & 1000 & 1,2 \\
2 & 2000 & 2,9 \\
3 & 3000 & 5,3 \\
4 & 4000 & 8,7 \\
5 & 5000 & 13,1 \\
\bottomrule
\end{tabular}
\end{table}

\begin{figure}[htbp]
\centering
\includegraphics[width=0.5\textwidth]{chapters/sortowanie.png}
\caption{Przepływ danych: Dane, Aplikacja, Wynik}
\label{fig:przeplyw-poprawa}
\end{figure}
Rysunek~\ref{fig:przeplyw-poprawa} przedstawia przepływ danych.
Dokumentacja Pythona jest dostępna w~\cite{pythonDocsPoprawa},
a pomiar czasu opisuje dokumentacja modułu time~\cite{pythonTimePoprawa}.

\begin{figure}[htbp]
\centering
\begin{tikzpicture}
\begin{axis}[
width=0.85\linewidth,height=6cm,
xlabel={Liczba elementów $N$ [-]},
ylabel={Czas $t$ [ms]},
grid=major,scaled x ticks=false]
\addplot[blue,thick,mark=*]
table[col sep=comma,x=N,y=t_ms]{pomiary.csv};
\end{axis}
\end{tikzpicture}
\caption{Czas wykonania w zależności od liczby elementów}
\label{fig:wykres-poprawa}
\end{figure}
Wykres~\ref{fig:wykres-poprawa} przedstawia pięć punktów z CSV.
Przykładowe czasy: \pomiar{1{,}2}{ms},
\pomiar{2{,}9}{ms} oraz \pomiar{13{,}1}{ms}.
```

## Bibliografia

Dopisz do literatura.bib (nie usuwaj wpisów wykorzystywanych w innych rozdziałach). Otwórz źródła i zweryfikuj dane przed oddaniem; datę dostępu dodaj zgodnie z faktycznym dniem korzystania.

```bibtex
@online{pythonDocsPoprawa,
  title = {Python 3 Documentation},
  organization = {Python Software Foundation},
  url = {https://docs.python.org/3/}
}
@online{pythonTimePoprawa,
  title = {time --- Time access and conversions},
  organization = {Python Software Foundation},
  url = {https://docs.python.org/3/library/time.html}
}
```

Szablon już obsługuje bibliografię. Nie dodawaj drugiego printbibliography ani starego bibliography/bibliographystyle.

## Oświadczenie

Dostarczony oswiadczenie_ai.tex zawiera samotne polecenia `\begin` i `\end` oraz tekst `zawartość...`: to błędy, nie poprawne środowisko LaTeX. Zachowaj oryginał, popraw kopię według formularza prowadzącego. Nie podpisuj stwierdzenia o niekorzystaniu z AI dla materiału przygotowanego z pomocą AI. Ustal właściwy wariant oświadczenia z prowadzącym.

Plik ma leżeć obok main.tex. Dołącz go przed końcem dokumentu, w odpowiednim miejscu części końcowej, tylko raz:

```latex
\clearpage
\input{oswiadczenie_ai}
```

Nie umieszczaj drugiego begin{document} ani end{document} we fragmencie. Nie zastępuj automatycznie odrębnego oświadczenia szablonu bez sprawdzenia wymagań.

## Kompilacja i kontrola

Uruchamiaj z katalogu main.tex:

```text
lualatex main.tex
biber main
lualatex main.tex
lualatex main.tex
```

Sprawdź PDF: tytuł i własne dane; osobna strona oświadczenia; tabela 5 wierszy z podpisem nad nią; PNG o szerokości 0.5 textwidth; dwa cytowania i bibliografia; niebieski wykres z linią thick, znacznikami i siatką; trzy użycia pomiar. Nie może być ?? ani kluczy cytowań zamiast odwołań.

CSV: nagłówek to `N,t_ms`, nie `n,t_ms`. Wartości końcowe: (1000,1.2), (5000,13.1). Zachowaj kropki dziesiętne w CSV. PNG jest schematem przepływu, nie wykresem sortowania.

Oddaj dwa osobne pliki: ZIP całego projektu i wygenerowany PDF. Sam main.tex nie wystarczy. Nie usuwaj wymaganych plików szablonu.

## Ćwiczenie na 45 minut

0–8 min: uruchomienie szablonu i metadane; 8–18: rozdział i tabela; 18–27: rysunek i dwa źródła; 27–37: CSV i wykres; 37–40: polecenie dodatkowe; 40–45: kompilacja, kontrola i ZIP.

Ćwicz zmianę nazwy kolumny CSV i odpowiedniego x=..., szerokości rysunku, podpisu tabeli oraz jednostki polecenia pomiar. Umiej wyjaśnić: caption nadaje podpis, label zapamiętuje numer, ref go przywołuje; label figury/tabeli umieszcza się po caption. Preambuła definiuje pakiety i polecenia, rozdział zawiera treść.

Punktacja wariantu A: szablon/oświadczenie 4, formatowanie/tabela 4, rysunek/bibliografia 5, wykres 7, polecenie dodatkowe 5. Bez dodatkowego maksymalnie 20/25. Zakres poprawy potwierdza prowadzący.

Status: kod przygotowany jako materiał ćwiczeniowy; nie potwierdzono kompilacji końcowego projektu ani wyglądu PDF.
