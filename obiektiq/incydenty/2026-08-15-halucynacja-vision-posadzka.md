# Incydent 2026-08-15 — halucynacja modułu wizyjnego ObiektIQ

**Zgłoszenie:** Jarek Walicki. Sesja `s_1786775764807_5h1he`, wykonania n8n `32834` i `32835`.
**Workflow:** `ObiektIQ The AI Vision` (`FWcddsxM7cdrETVi`), węzeł `Gemini Vision Analysis`.
**Waga:** krytyczna — agent opisał awarię, której nie było, w obiekcie handlowym.

## Objaw

Użytkownik przysłał 3 zdjęcia starej, **suchej** posadzki z płytek w sklepie i zapytał wprost:
*„Sklep jak myc ta posadzka ?"*

Agent odpowiedział opisem nieistniejącego wycieku z regału chłodniczego, nakazał wystawić znak
„Mokra podłoga", wezwać serwis chłodni i usunąć krzesło z ciągu komunikacyjnego. Na pytanie
o mycie posadzki nie odpowiedział — odesłał użytkownika do agenta Jaro.

Po sprostowaniu użytkownika („nie ma krzesła i nie ma wycieku, posadzka jest sucha") agent
podał ogólny standard nadzoru nad firmą sprzątającą, ale **nadal nie ocenił stanu posadzki**.

## Lokalizacja błędu

Halucynacja powstała **w całości w węźle `Gemini Vision Analysis`**. Mózg ObketIQ nie zmyślał —
wiernie powtórzył opis, który dostał. Surowy output Vision z wykonania `32834`:

> Zbliżenie na plamy, rdzawe ślady i **zacieki** na płytkach przy podstawie regału chłodniczego.
> Ogólny widok alei ze **śladami po wycieku**, różnymi płytkami oraz zielonym krzesłem
> **blokującym przejście**.
> Realna usterka to ślady wycieku z chłodni oraz zastawione przejście.

Wniosek diagnostyczny: przy błędach opisu zdjęcia **najpierw czytaj `Prepare Vision for AI`**,
zanim ruszysz prompt Mózgu. Inaczej poprawia się warstwę, która nie zawiniła.

## Przyczyny źródłowe

1. **Priming listą zagrożeń.** Stary prompt nakazywał: *„zwróć szczególną uwagę na zagrożenia:
   zablokowane drzwi ppoz, zastawione drogi ewakuacyjne, zacieki, plesn…"*. Model dostał listę
   rzeczy do znalezienia i je znalazł. Na zdjęciu z plamami na płytkach „zaciek" jest
   najtańszą hipotezą, jaką można dopasować do polecenia.
2. **Brak rozdziału faktu od interpretacji.** Prompt prosił o „co widać", ale nie zabraniał
   dopowiadania przyczyny. Model przeszedł od plamy do niedrożnego odpływu parownika.
3. **Brak rozstrzygania mokre / suche.** Nie było kryterium odróżniającego kałużę od suchego
   przebarwienia — a to jedyna różnica między „ryzyko poślizgnięcia" a „stara fuga".
4. **Wymuszony poziom ryzyka.** Prompt żądał poziomu ryzyka zawsze, bez opcji „brak zagrożenia".
   Model musiał coś wyprodukować, więc wyprodukował.
5. **Brak protokołu oceny stanu posadzki.** Posadzki są deklarowaną mocną stroną ObiektIQ,
   a agent nie miał czym odpowiedzieć na faktyczne pytanie użytkownika.

## Naprawa

### 1. Prompt węzła `Gemini Vision Analysis` (opublikowany, wersja `e08053f7`)

Zmieniony **wyłącznie tekst promptu**. Struktura węzła, budowa `inline_data`, model i klucz
bez zmian. Wprowadzone reguły:

- **Zasada nadrzędna** — opisuj wyłącznie to, co widać. Plama nie jest wyciekiem, dopóki nie
  widać cieczy. Przedmiot przy ścianie nie blokuje przejścia, dopóki nie stoi w świetle drogi.
- **Mokre czy suche** — rozstrzygane zawsze i osobno, z kryteriami optycznymi (lustrzane
  odbicie i ciemny brzeg kałuży vs ostra stała krawędź suchej plamy). Przy braku pewności
  wymuszone `WILGOTNOŚĆ NIEROZSTRZYGNIĘTA`.
- **`BRAK WIDOCZNEGO ZAGROŻENIA`** jako dopuszczalny i oczekiwany poziom ryzyka. Wprost
  zapisane, że nadgorliwe zgłaszanie nieistniejących usterek jest poważniejszym błędem niż
  przeoczenie, bo manager traci zaufanie do narzędzia.
- **Lista zagrożeń przebudowana z „szukaj tego" na „wymieniaj tylko, gdy widać"**.
- **Nowy punkt `STAN POSADZKI`** — rodzaj i format okładziny, równość płaszczyzny (uskoki,
  klawiszowanie, zapadnięcia), stan fug, stan powierzchni, ślady dawnych napraw, wpusty i progi.
  Opisywany rzetelnie także wtedy, gdy nie ma żadnej usterki.

### 2. Doprecyzowanie zakresu roli — korekta Jarka w trakcie naprawy

Pierwsza wersja kart poszła **za daleko**: zawierała metodę mycia (pady miękkie, szczotki,
dobór chemii). Jarek uciął to jednoznacznie:

> ObiektIQ nie jest ekspertem posadzek. On ocenia to jako właściciel obiektu: czy posadzka
> jest umyta poprawnie, czy kafelki są w dobrym stanie, czy posadzka brudna. Jeżeli wyciek
> wody, to awaria lodówki i naprawa. Sama metoda jak myć — to Jaro albo Nexus.

Obowiązujący podział:

| Pytanie | Kto odpowiada |
|---|---|
| Czy ta posadzka jest umyta poprawnie? | **ObiektIQ** |
| W jakim stanie jest okładzina, czy płytki są sprawne? | **ObiektIQ** |
| Czy to jeszcze brud, czy już zużycie? | **ObiektIQ** |
| Widać ciecz — awaria urządzenia, kogo wezwać? | **ObiektIQ** (Hard FM, serwis z umowy) |
| Czym myć: pad, szczotka, gradacja, chemia, maszyna | **Jaro (J&G NexGen) / Nexus** |

Karty zostały przepisane na poziom oceny. Wskazanie specjalisty następuje **po** udzieleniu
oceny — odesłanie bez oceny jest błędem i to właśnie zrobił agent w tym incydencie.

### 3. Dwie karty w bazie wiedzy CORE (moduł 5, Typ wiedzy: Audyt)

- **Ocena posadzki oczami właściciela obiektu — czy umyta poprawnie i w jakim stanie są płytki.**
  Objawy nierzetelnego mycia rozpoznawalne bez wiedzy technicznej (ciemny pas przy cokołach,
  czysty środek płytki przy ciemnej siatce fug, smugi po kierunku jazdy, wilgotna posadzka po
  przejeździe). Opis stanu okładziny. Rozdzielenie utrzymania bieżącego od doczyszczania
  startowego. Rozstrzygnięcie plama sucha vs ciecz jako przełącznik: sprzątanie czy Hard FM.
- **Objawy źle dobranej technologii mycia — co manager rozpoznaje i komu zgłasza.** Rozpoznanie
  nawarstwionej pozostałości po chemii (matowa, lepka, szybko brudząca się, śliska po zmoczeniu)
  wraz z sekcją, czego z tych objawów **nie wolno** wywnioskować. Dobór chemii jawnie wyłączony
  z zakresu i skierowany do Jaro/Nexusa.

### 4. Pętla uczenia

- Wpis w LUKI WIEDZY (`Zrodlo = Obserwacja wlasna`, `Status = Karta gotowa`) z dowodem
  z wykonania i linkiem do karty CORE.
- Oba rekordy rozmowy w LOGU oznaczone `Ocena = Nauczone`, `Przeniesione do Luk = tak`,
  z wpisanym „Co powinno byc". Nie zaśmiecają raportu porannego.

## Iteracja 2 — retest 32845 i błąd odwrotny

Retest po pierwszej poprawce **usunął halucynację**: żadnego wycieku, plamy zaklasyfikowane
jako `SUCHE ZABRUDZENIE LUB ZUŻYCIE`, krzesło opisane neutralnie („zielone krzesło przy
regale"), bez przypisywania mu roli blokady.

**Pojawił się jednak błąd odwrotny — uspokojenie na wyrost.** Vision orzekł:

> (3) STAN POSADZKI: (…) **Płaszczyzna równa, brak ubytków i klawiszowania.**
> (5) RYZYKO: **BRAK WIDOCZNEGO ZAGROŻENIA.**

a Mózg to wzmocnił: *„Stan techniczny posadzki jest bezpieczny — płytki leżą równo, nie ma
ryzyka potknięcia"* oraz zbył łaty zdaniem *„z tym już nic nie zrobisz bez wymiany płytek"*.

Dostawszy prawo do odpowiedzi „brak zagrożenia", model zaczął jej używać jako wygodnego
domyślnego wniosku zamiast przejść przez realną kontrolę stanu.

### Ocena właściciela obiektu na tych samych zdjęciach (Jarek, 15.08.2026)

1. Płytki **nie są równe** i to widać.
2. Są płytki **z otworami**, najprawdopodobniej po zdemontowanym stelażu. Gromadzi się w nich
   brud i **trzeba je naprawić** — to ważne dla managera budynku.
3. **Różne kolory płytek** to ślad napraw i wymiany starych fragmentów, a **styk starej
   i nowej okładziny ma wyraźny kant**, czyli kolejny uskok.
4. **Rdza przy lodówkach** pochodzi prawdopodobnie od śrub osadzonych w płytkach, a plamy
   osadu to **złe mycie** — maszyna nie dojeżdża do rogu, drzwi urządzeń blokują bliski
   podjazd, firma **nie domywa kantów**, a za to się płaci. Poważny błąd higieniczny.

### Dlaczego uskok nie jest kwestią estetyki

- ssawa maszyny **podskakuje na uskoku** i przestaje zbierać wodę → zostaje brudna woda →
  mokra, śliska posadzka → upadek klienta
- nierówne fugi zatrzymują wodę po przejeździe maszyny → ten sam skutek
- **wózek z towarem podskakuje** na kancie → towar może się uszkodzić
- **osoba starsza szurająca nogami lub idąca z balkonikiem** zahacza o kant i przewraca się

### Poprawka (opublikowana, wersja `2b136b79`)

- **Zasada działa w obie strony.** Zdania „płaszczyzna równa", „brak ubytków", „brak ryzyka
  potknięcia" to twierdzenia o **braku** wady i wymagają takiego samego dowodu jak twierdzenie
  o wadzie. Gdy kąt zdjęcia lub oświetlenie nie pozwalają rozstrzygnąć — `NIE DA SIĘ OCENIĆ
  ZE ZDJĘCIA`, nigdy uspokajanie. Uspokojenie na wyrost jest groźniejsze niż fałszywy alarm,
  bo nie prowokuje weryfikacji.
- **Rozpisana lista kontrolna stanu posadzki** z wymuszoną odpowiedzią przy KAŻDYM punkcie:
  uskoki (ze szczególną uwagą na styk łat z posadzką oryginalną), klawiszowanie, otwory
  i ubytki po mocowaniach wraz z informacją, czy zbiera się w nich brud, fugi, powierzchnia,
  płytki odbiegające kolorem, rdzawe ślady wokół śrub, osad w narożnikach i pod krawędzią
  urządzeń, wpusty i progi. Zakaz pomijania punktu i zbiorczego „wszystko w porządku".
- **Uskok, wyrwa lub otwór w ciągu pieszym musi podnieść poziom ryzyka**, nawet gdy posadzka
  jest czysta.

Karta CORE rozbudowana o katalog uszkodzeń, skutki uskoku, otwory jako zadanie naprawcze
(punktowe uzupełnienie ubytku, a nie wymiana całej posadzki) oraz niedomyte kanty jako
najłatwiejszy do udowodnienia zarzut wobec wykonawcy. Druga luka zapisana w LUKI WIEDZY.

## Do wykonania przez Jarka

- [ ] **Retest po iteracji 2, w NOWEJ sesji.** Redis trzyma pamięć per `sessionId`, więc
      w dotychczasowej sesji stary opis zdjęć nadal siedzi w kontekście i może zaburzyć wynik.
      Oczekiwane: wypunktowane uskoki, otwory po mocowaniach i kant na styku łat; brak zdania
      o równej i bezpiecznej posadzce; podniesiony poziom ryzyka mimo czystości.
- [ ] Kontrolnie wysłać zdjęcie **faktycznego** zacieku albo zaklinowanych drzwi ppoż. —
      sprawdzić, czy `BRAK WIDOCZNEGO ZAGROŻENIA` nie tłumi realnych zgłoszeń.

## Znaleziska poboczne — do decyzji Jarka

### A. Skill `obiektiq-asystent` jest nieaktualny w opisie synchronizacji

Skill opisuje sync jako jeden workflow z węzłami `Get Embedding`, `Przygotuj Upsert`,
`Pinecone Upsert`, `Notion: Zapisz Namespace` i pełnym przebiegiem ~3 min dla 95 kart.
**Stan faktyczny na 15.08.2026:** sync jest inkrementalny i dwupoziomowy.

- `ObiektIQ: Notion → Pinecone (sync CORE)` (`YYbXOIaMlAoaUSpr`) pobiera karty filtrem
  `Gotowe do RAG = true` **AND** `Status ≠ Zsynchronizowany`, po czym woła w pętli
  subworkflow `ObiektIQ - Wektoryzacja SUB (ROBOT)` (`tRwt1hSWNcGt15iD`).
- Sub-workflow tnie kartę na chunki (1000 znaków, krok 850), embeduje przez
  `gemini-embedding-001` (3072), upsertuje do namespace `obiektiq-ai-vision-core`
  i ustawia `Status = Zsynchronizowany`.
- **Węzła zapisującego `Namespace Pinecone` już nie ma.** Puste pole na nowej karcie to
  norma, nie awaria — skill każe je traktować jako dowód udanego upsertu, co dziś wprowadza
  w błąd.

Skill wymaga aktualizacji w sekcjach „Sync wiedzy" i „Stan zweryfikowany".

### B. Edycja karty nie wraca do RAG bez ręcznego odblokowania

Skutek uboczny sync inkrementalnego: karta już zsynchronizowana ma `Status = Zsynchronizowany`
i filtr ją **pomija**, choćby treść zmieniła się całkowicie. Skill mówi „edycja karty nie
tworzy duplikatu, upsert nadpisuje" — to prawda tylko wtedy, gdy karta w ogóle zostanie
ponownie pobrana.

**Zasada operacyjna:** po każdej edycji karty ustaw `Status = Do synchronizacji`, inaczej
poprawka nigdy nie dojedzie do agenta. Wystąpiło to w tej naprawie — pierwsza wersja kart
zsynchronizowała się, a poprawione treści zostałyby pominięte.

### C. Sieroty na poziomie chunków (problem systemowy)

ID wektora to `notion::<pageId>::<index>`. Upsert nadpisuje tylko indeksy, które powstały
w nowym przebiegu. **Gdy skrócisz kartę, nadmiarowe chunki starej wersji zostają w Pinecone
i nadal są wyszukiwalne.**

Wystąpiło realnie: karta o objawach technologii spadła z 5 na 4 chunki, zostawiając
`notion::3bdbacc6-f800-8185-b1e4-d7825c4fd24c::4` ze starą treścią technologiczną — czyli
dokładnie z tym, co z zakresu ObiektIQ zostało usunięte. Obejście zastosowane teraz:
rozbudowa karty z powrotem do 5 chunków, co nadpisało sierotę (`upsertedCount: 5`).

To obejście, nie rozwiązanie. **Docelowo sub-workflow powinien przed upsertem kasować
chunki o indeksie ≥ liczby nowych chunków** (`POST /vectors/delete`). To dodanie węzła,
czyli zmiana struktury — czekam na Twoją zgodę, nie robię tego sam.

### D. Puste `modul` w metadanych wektora

W przebiegu `32841` metadana `modul` poszła jako pusty string, mimo że karta ma ustawiony
`Moduł = 5. Soft FM i sprzątanie`. Parent czyta `pick(props,'Moduł')` i najwyraźniej nie
trafia w kształt pola zwracany przez węzeł Notion. Nie blokuje wyszukiwania (liczy się `text`),
ale psuje filtrowanie po module. Do osobnego kroku.

### E. Mylące etykiety po Nexusie (nie ruszane)

Węzeł `Code: Merge Image Analysis` (ścieżka Drive) etykietuje opis jako
`[ANALIZA WIZUALNA GPT-4o]`, choć analizę robi Gemini. Mylące dla Mózgu i dla debugowania.
Poprawka wymaga tknięcia węzła spoza zakresu tej naprawy — do osobnego kroku.
