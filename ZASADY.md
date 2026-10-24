# Dyrygent Tabu — zasady (wersja robocza 0.1)

Półkooperacyjna gra muzyczna dla dwojga, na podstawie utworów klasycznych ze Spotify.
Wspólnie gracie przeciw grze: trzeba doprowadzić **koncert** do końca.
Jednocześnie każde z was zbiera **punkty osobiste** w pojedynku o tytuł **Maestro**.

---

## Role

- **Dyrygent** podaje wskazówki. Widzi kartę z odpowiedzią.
- **Słuchacz** zgaduje. Słyszy fragment utworu, ale nie widzi karty.

Na zwykłych kartach Dyrygentem jest osoba bez wykształcenia muzycznego, a Słuchaczem muzyczka.
Na kartach **popkultury** role się zamieniają (patrz niżej).

## Koncert

- Koncert to **10 utworów**.
- **Cierpliwość orkiestry** zaczyna od **6** (najwyżej 8).
- Gdy cierpliwość spadnie do **0**, koncert jest **odwołany**. Przegrywacie oboje i nikt nie zostaje Maestro.

## Przebieg rundy

### 1. Losowanie
Aplikacja losuje kartę. Dyrygent widzi kompozytora, tytuł, rok, słowa tabu i podpowiedzi
(fakty historyczne, biograficzne i popkulturowe).

### 2. Trzy etapy
| Etap | Fragment | Wskazówka Dyrygenta | Punkty za trafienie |
|---|---|---|---|
| 1 | 3 s | wskazówka nr 1 | 3 |
| 2 | 10 s | wskazówka nr 2 | 2 |
| 3 | 30 s | wskazówka nr 3 | 1 |

- Fragment zaczyna się od miejsca zapisanego na karcie (`start_s`), zwykle nie od słynnego początku.
- Słuchacz ma **jedną próbę na etap**. Pomyłka nie kosztuje cierpliwości, tylko przechodzicie do następnego etapu.
- Za trafienie oboje dostajecie te same punkty **Oklasków** (wynik drużynowy). Zgadywanie jest w pełni wspólne.
- **Częściowe trafienie:** jeśli w etapie 3 Słuchacz poda dobrego kompozytora, ale zły utwór, jest **1 Oklask**
  i cierpliwość nie spada.
- Brak trafienia po etapie 3: cierpliwość **−1**.

### 3. Faza „Gust” (po każdym utworze, ok. 10 s)
Każde z was w tajemnicy, na swoim telefonie:
1. ocenia utwór w skali **1–5**,
2. przewiduje ocenę drugiej osoby.

Po odsłonięciu każde dostaje **punkty osobiste** za swoje przewidywanie:

| Przewidywanie | Punkty |
|---|---|
| dokładnie (ocena 2–4) | 2 |
| dokładnie (ocena 1 lub 5) | 3 |
| pomyłka o 1 | 1 |
| pomyłka o więcej | 0 |

Za trafienie skrajnej oceny (1 lub 5) jest więcej punktów, więc opłaca się mieć zdanie, a nie ciągle dawać „3”.

**Harmonia:** jeśli oboje przewidzieliście dokładnie, cierpliwość orkiestry rośnie o **1**.

**Szkolna trauma:** przy kartach typu `repertuar` (utwory, które muzyczka grała w szkole) jej pytanie
brzmi: *„Jak bardzo nienawidziłaś to ćwiczyć?”* (1 = uwielbiałam, 5 = koszmar).
Drugi gracz przewiduje tę odpowiedź. Druga strona ocenia normalnie, czy utwór się podoba.

## Tabu, czyli czego Dyrygentowi nie wolno

- Nie wolno podać nazwiska kompozytora ani słów z tytułu (lista `tabu` na karcie).
- Nie wolno używać terminów muzycznych: *kompozytor, utwór, symfonia, koncert, sonata, opera, balet,
  melodia, nuta, tonacja, takt, orkiestra*, nazw instrumentów ani nazw epok (*barok, romantyzm…*).
- Nie wolno nucić, śpiewać ani wystukiwać rytmu.
- Wolno: historia, geografia, biografia, filmy, reklamy, anegdoty, skojarzenia.

**Słowo muzyczne:** raz na koncert każdy Dyrygent może użyć jednego zakazanego terminu muzycznego
(ale nigdy nazwiska ani tytułu).

Złamanie tabu: runda przepada, cierpliwość **−1**.

## Karty popkultury (zamiana ról)

Około 2 z 10 kart to utwory znane z filmów, reklam albo kreskówek. Na nich muzyczka jest Dyrygentem,
a druga osoba Słuchaczem. Obowiązują te same zasady tabu, więc żadnej teorii muzyki.

## Brawo! (dylemat półkooperacji)

Każde z was ma **3 żetony Brawo** na koncert i daje je drugiej osobie za świetną wskazówkę albo
imponujące trafienie. Każdy żeton daje:
- **+1 punkt osobisty** obdarowanemu,
- **+1 Oklask** drużynie.

Dając Brawo, pomagacie drużynie, ale zarazem dokładacie punkty rywalowi w pojedynku o Maestro.

## Koniec koncertu

**Wynik drużynowy** (Oklaski, ze zgadywania i z żetonów Brawo):

| Medal | Oklaski |
|---|---|
| Brąz | 15 |
| Srebro | 22 |
| Złoto | 28 |

*(Progi do kalibracji po kilku wieczorach. Maksimum to 30 ze zgadywania i 6 z żetonów Brawo.)*

**Maestro:** jeśli koncert się udał, osoba z większą liczbą punktów osobistych (Gust + Brawo + zadania)
nosi tytuł Maestro do następnej gry.

Aplikacja zapisuje też, na przyszłość, **współczynnik zgodności gustów** z każdego wieczoru
(korelacja ocen) oraz rekordy medali.

---

## Wariant opcjonalny: Tajne zadania

Na początku koncertu każde z was losuje tajne zadanie, warte **3 punkty osobiste**,
odsłaniane na końcu. Przykłady:

- *„Doprowadź do trafienia, używając wyłącznie wskazówki o jedzeniu.”*
- *„Wygraj rundę wskazówką o wojnie.”*
- *„Odgadnij utwór w etapie 1 dwa razy w jednym koncercie.”*
- *„Przewidź dokładnie ocenę 1 albo 5 drugiej osoby.”*

---

## Format karty (`dane/karty.json`)

```json
{
  "id": "smetana-weltawa",
  "typ": "standard",
  "kompozytor": "Bedřich Smetana",
  "tytul": "Wełtawa (z cyklu „Moja ojczyzna”)",
  "rok": 1874,
  "epoka": "romantyzm",
  "kraj": "Czechy",
  "spotify_uri": null,
  "start_s": 0,
  "tabu": ["Smetana", "Wełtawa", "Moja ojczyzna"],
  "podpowiedzi": ["…", "…", "…"],
  "do_weryfikacji": false
}
```

- `typ`: `standard` | `popkultura` (zamiana ról) | `repertuar` (szkolna trauma w fazie Gust).
- `start_s`: od której sekundy nagrania startuje fragment.
- `podpowiedzi`: gotowe fakty dla Dyrygenta. Można ich użyć albo mówić własnymi słowami.
- `do_weryfikacji`: `true`, dopóki fakty na karcie nie zostaną sprawdzone.
