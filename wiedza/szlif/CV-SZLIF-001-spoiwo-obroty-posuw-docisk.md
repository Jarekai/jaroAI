# CV-SZLIF-001 — Spoiwo, obroty, posuw i docisk przy szlifie betonu

**Status:** SZKIC do zatwierdzenia przez Jarka. Po zatwierdzeniu → Notion → Pinecone.
**Odbiorcy:** NEXUS, MING, SONAR (każdy własnym głosem). **Nie dla:** JARO, Anna, ARVIS, BHP.
**Zasada karty:** karta jest neutralna — bez nazwy maszyny, bez marki narzędzi, bez numerów części, bez liczb maszyny.
Liczby konkretnej maszyny podaje wyłącznie agent tej maszyny, z danych zatwierdzonych przez producenta.
**Powiązane:** NEX-DIAG-006 (połysk ≠ równość, pułapka niewidocznej rysy, żywice przegrzewane).

---

## 1. Dlaczego to ważne

Błędy na szlifie rzadko wynikają ze słabej maszyny. Najczęściej wynikają ze złego zestrojenia pięciu rzeczy:
twardości betonu, spoiwa segmentu, obrotów, prędkości jazdy i docisku.
Źle zestrojone dają trzy typowe skutki: szklenie diamentu, przeciążenie napędu i posadzkę, która się świeci, ale nie jest równa.

## 2. Spoiwo dobiera się przeciwnie do twardości betonu

| Beton | Spoiwo segmentu metalowego | Dlaczego |
|---|---|---|
| Twardy, utwardzany, z posypką, po densyfikacji | **miękkie** | beton musi ścierać spoiwo, żeby odsłaniało nowe ziarna diamentu |
| Średni | **średnie** | równowaga między zużyciem a wydajnością |
| Miękki, piaszczysty, abrazyjny, jastrych | **twarde** | luźny piasek szybko zjada miękkie spoiwo — segment znika zanim popracuje |

**Jak rozpoznać twardość:** klasa betonu (np. B25, B40) mówi o wytrzymałości na ściskanie, nie o twardości powierzchni — to tylko orientacja.
Rozstrzyga próba zarysowania i **próbny przejazd na 1–2 m²** z obserwacją: czy segment zdejmuje materiał, czy się ślizga.

**Szklenie diamentu:** za twarde spoiwo na twardym betonie. Diament wygładza się, spoiwo się nie ściera, nowe ziarna nie wychodzą.
Objawy: maszyna „pływa”, nie zdejmuje materiału, rośnie hałas i temperatura, segmenty błyszczą.
Korekta: miększe spoiwo; doraźnie — przetarcie segmentów na materiale ściernym (np. płyta ścierna, piaskowiec), żeby je odsłonić.

## 3. Kierunek zmian parametrów

| Etap | Obroty | Docisk | Prędkość jazdy |
|---|---|---|---|
| Metal gruby — zdejmowanie powłok, otwieranie betonu | niskie do średnich | **największy** | wolno — segment musi mieć czas pracy |
| Metal drobniejszy i hybryda — wyrównanie, usuwanie rys | średnie | średni | równo, na zakładkę |
| Żywica 50–200# — jeszcze szlifuje, usuwa ślad po metalu | średnie do wyższych | średni | równo, na zakładkę |
| Żywica od 400# — poleruje | wyższe | **mniejszy** | równo, bez pośpiechu |

To jest **kierunek**, nie tabela liczb. Konkretne wartości zależą od maszyny, narzędzi i betonu i podaje je agent danej maszyny.

**Prędkość jazdy nie rośnie dowolnie razem z gradacją.** Maksymalna prędkość maszyny to granica mechaniczna, nie parametr pracy.
Za szybki przejazd skraca czas kontaktu narzędzia z powierzchnią — zostają nierówności i niedopolerowane pola.

## 4. Czego żywica nie robi

- Żywica **nie tnie** i nie utwardza betonu.
- Tarcie żywicy **nie zamyka porów**. Pory zamyka grouting, a powierzchnię wzmacnia densyfikator.
- Ciepło przy żywicy to skutek uboczny. **Za dużo ciepła to wada:** za duży docisk, za mało wody, za długo w jednym miejscu →
  nadtopione spoiwo, oddawanie koloru, ciemne przypalone pola (NEX-DIAG-006 §4.5.6).
- Narzędzia na szlifierce to **metale, hybrydy i żywice**. Słowo „pady” rezerwujemy dla pielęgnacji gotowej posadzki.

## 5. Rysy koliste

Ruch planetarny głowic **ogranicza** rysy koliste, ale ich nie eliminuje. Najczęstsze przyczyny:
1. pominięta gradacja albo za krótki krok,
2. zabrudzone narzędzia, grys pod segmentem,
3. **brak mycia między krokami** — pył maskuje rysy, wychodzą dopiero przy polerowaniu, a wtedy trzeba wracać do metali (NEX-DIAG-006 §4.5.5).

**Myj posadzkę przed przejściem do następnej gradacji. Densyfikator dopiero po sprawdzeniu, że krok 1 i 2 są domknięte.**

## 6. Przeciążenie napędu

Typowe przyczyny: za duży docisk przy grubej gradacji, za twarde spoiwo (szklenie), za niskie napięcie zasilania, za długi lub za cienki kabel.
Po zadziałaniu zabezpieczenia: odłącz zasilanie, odczekaj na ostygnięcie zgodnie z instrukcją producenta, usuń przyczynę — a nie tylko skutek.
Minimalne napięcie, przekrój kabla i czas stygnięcia podaje **instrukcja danej maszyny** — karta ich nie zgaduje.

## 7. Zasady dla agentów

- NEXUS: mówi o fizyce i metodzie, **bez nazwy maszyny i marki narzędzi**, chyba że klient pyta wprost.
- MING / SONAR: mogą dołożyć liczby **swojej** maszyny, wyłącznie z danych zatwierdzonych przez producenta. Żadnych danych drugiej marki.
- Żaden agent nie obiecuje „skrócenia czasu o połowę” ani „wyeliminowania błędów” bez pomiaru.
- Ocena efektu: połysk to za mało — liczy się równość, DOI i chropowatość (NEX-DIAG-006 §4.5.1).
