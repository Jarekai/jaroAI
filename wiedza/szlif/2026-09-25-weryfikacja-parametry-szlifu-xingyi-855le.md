# Weryfikacja: parametry szlifu Xingyi 855LE (spoiwo × twardość × RPM × posuw × docisk)

**Status:** SZKIC — **nie ładować do Notion/Pinecone** przed decyzjami z sekcji 5.
**Źródło:** tekst przysłany przez Jarka 2026-09-25 (opis 855LE + matryca parametrów + „Agent Mink.AI” + cytat Jarka).
**Werdykt:** fundament fizyczny jest **dobry**. Tekstu **nie wolno** wgrać w obecnej postaci — ani do jednego agenta, ani do wszystkich.
Ma trzy rodzaje problemów: (1) błędy merytoryczne sprzeczne z zatwierdzoną wiedzą NEXUS-a (NEX-DIAG-006),
(2) liczby maszyny niepotwierdzone przez Xingyi, (3) routing „do wszystkich agentów” łamie silosy.

---

## 1. Co jest poprawne — zostaje

| Teza | Ocena |
|---|---|
| Spoiwo dobiera się **przeciwnie** do twardości betonu: twardy → miękkie spoiwo, miękki/abrazyjny → twarde spoiwo | ✅ zasada podstawowa, poprawna |
| Za twarde spoiwo na twardym betonie → **szklenie diamentu** (ziarno się wygładza, spoiwo nie odsłania nowego) | ✅ |
| Miękki, piaszczysty beton „zjada” miękkie spoiwo → szybkie zużycie segmentu | ✅ |
| Kierunek zmian: gruba gradacja = większy docisk, niższe obroty; drobna gradacja = mniejszy docisk, wyższe obroty | ✅ jako **kierunek**, nie jako sztywne liczby |
| Za duży docisk na drobnej żywicy → przegrzanie, przypalenie, ciemne pola | ✅ zgodne z NEX-DIAG-006 §4.5.6 |
| Spadek napięcia zasilania → przeciążenie napędu; przekrój i długość kabla mają znaczenie | ✅ co do zasady (wartości — sekcja 3) |
| Po zadziałaniu zabezpieczenia przeciążeniowego — odłączyć i odczekać na ostygnięcie | ✅ co do zasady (czas — z instrukcji Xingyi) |
| Czyszczenie rzepów przed założeniem narzędzi | ✅ |

## 2. Błędy merytoryczne — do poprawy przed jakimkolwiek wgraniem

| # | Oryginał | Problem | Poprawka |
|---|---|---|---|
| 1 | „Pady żywiczne (Resin Pads)” dla narzędzi szlifierki | Łamie rozdzielenie światów z NEX-DIAG-006: **pady** = pielęgnacja; na szlifierce pracują **żywice / narzędzia żywiczne**. JARO i NEXUS nauczyłyby się mieszać szlif z pielęgnacją | „Narzędzia żywiczne (żywice)” w całym tekście |
| 2 | „ścinanie powłok”, „dajesz diamentowi rżnąć beton” | Zakaz słowa „tnie” o narzędziach posadzkowych | „zdejmuje materiał”, „szlifuje” |
| 3 | „Mikrotarcie żywicy całkowicie zamyka pory”, „tarcie zamyka pory betonu” | **Nieprawda.** Pory zamyka grouting i densyfikator; żywica wygładza. Ciepło to skutek uboczny, a jego nadmiar to wada (§4.5.6), nie mechanizm | „Żywica od 400# poleruje i wygładza. Pory zamyka grouting i densyfikacja, nie tarcie” |
| 4 | „Żywice wymagają temperatury i tarcia niezbędnych do utwardzenia” | Żywica niczego nie utwardza. Utwardza densyfikator krzemianowy | usunąć |
| 5 | Hybryda 200#: „zamknięcie porów po aplikacji krzemianu” | Densyfikator nie zamyka porów mechanicznie; kolejność (densyfikacja dopiero po sprawdzeniu i wyrównaniu) jest ważniejsza niż gradacja | „Densyfikator dopiero po umyciu i sprawdzeniu, że krok 1 i 2 jest domknięty” (§4.5.5) |
| 6 | Posuw rosnący do **25–28,3 m/min** przy 1500–3000# | 28,3 m/min to **maksimum mechaniczne** trakcji, nie parametr technologiczny. Sprzeczne z regułą czasu kontaktu (szybko = rozmazanie). Ryzyko: agent zaleca jazdę na maksimum | „Posuw stały i równy, praca na zakładkę. Wartość z instrukcji Xingyi / testu na obiekcie” — **do potwierdzenia** |
| 7 | „4 głowice przeciwbieżne **eliminują** swirl marks” | Ograniczają, nie eliminują. Najczęstsza przyczyna rys kolistych to zanieczyszczone narzędzia, pominięta gradacja i **brak mycia między krokami** | „ograniczają”; dopisać pułapkę niewidocznej rysy (§4.5.5) |
| 8 | „Polerowanie przy za niskich obrotach niszczy pory betonu” | Fizycznie bez sensu | „…nie domyka powierzchni, połysk wychodzi nierówny i mglisty” |
| 9 | Klasy B45+ / B15–B20 jako miara twardości | Klasa B to **wytrzymałość na ściskanie**, nie twardość powierzchni. Twardość ocenia się próbą zarysowania / Mohs / próbnym przejazdem | dopisać: „Klasa B to orientacja. Rozstrzyga próba zarysowania i próbny przejazd na 1–2 m²” |
| 10 | Cytat: hard beton 700–900 RPM; tabela: 350–800 RPM | Niespójne w jednym dokumencie | ujednolicić po potwierdzeniu przez Xingyi |
| 11 | Metal 70–120#: 1000–1400 RPM; hybryda 50–100#: 1200–1500 RPM | Zakresy się nakładają i nie wynikają z żadnego źródła | do potwierdzenia |
| 12 | Brak w całym tekście | Brak **mycia między krokami**, bramki kroku 1, groutingu, pomiaru DOI/Ra | dopisać odwołania do NEX-DIAG-006 |
| 13 | „skraca czas realizacji o połowę”, „wyklucza błędy ludzkie”, „rewolucja”, „nowy standard” | Niemierzalne obietnice. MING: **zero zmyślonych argumentów sprzedażowych** | usunąć lub zastąpić liczbą z pomiaru |
| 14 | Pozycja 3 przeciwwagi „do transportu i wymiany narzędzi” | Do transportu i wymiany podnosi się głowice; docisk nie ma tu znaczenia | do potwierdzenia z instrukcją |

## 3. Dane maszyny — NIEPOTWIERDZONE, tylko Xingyi może zatwierdzić

Każda liczba poniżej trafi do MING-a wyłącznie po potwierdzeniu przez Jane Ling / Elaine (obieg zatwierdzania z `ming-asystent`).

| Parametr | W tekście | Uwaga |
|---|---|---|
| Masa | 630 kg | potwierdzić |
| Moc | 18,5 kW (25 KM) | potwierdzić |
| Szerokość | „roboczej 834 mm (szlifowania 855 mm)” | **sprzeczne** — która jest szerokością szlifowania? |
| Obroty tarcz | 350–1950 RPM | potwierdzić; 1950 dla talerza planetarnego to dużo — może to obroty silnika, nie głowic? |
| Posuw | 0–28,3 m/min | potwierdzić |
| Docisk | 382 / 275,5 / 247 kg w 3 pozycjach | potwierdzić; czy to docisk na głowice czy rozkład masy? |
| Liczba głowic, S-type swing | 4, oscylacja | potwierdzić, czy 855LE ma oscylację |
| Min. napięcie | 320 V | potwierdzić z instrukcji |
| Kabel | Cu 10 mm² | zależy od długości — potrzebna tabela długość/przekrój od Xingyi |
| Inwerter 220 V `3.12.111.084` | — | **18,5 kW na 220 V jest mało prawdopodobne** jednofazowo — czy to 220 V trójfazowe (rynki pozaeuropejskie)? |
| Inwerter 380 V `3.12.111.016`, adapter 100 mm `3.22.115.003`, podkładki `3.22.117.001` | — | SKU — tylko z katalogu Xingyi |
| Stygnięcie po overload | 10–30 min | potwierdzić |

## 4. Routing — gdzie ta wiedza wolno trafić

„Do wszystkich agentów” jest sprzeczne z ustalonymi zasadami. Propozycja:

| Agent | Co dostaje | Dlaczego |
|---|---|---|
| **NEXUS** | tylko sekcję 1 (zasady fizyczne) po poprawkach z sekcji 2, **bez nazwy maszyny, bez SKU, bez „Mink.AI”** | NEXUS jest neutralny — zero marek z siebie |
| **MING** | sekcje 1 + 3 po zatwierdzeniu przez Xingyi | jedyny właściwy dom dla danych 855LE |
| **SONAR** | tylko sekcja 1, **bez żadnych danych Xingyi** | silos Orcas ↔ Xingyi; liczby Pioneer 860 wyłącznie od Cary Zhou |
| **JARO** | **nic** | JARO = pady i pielęgnacja; wiedza o szlifie w JARO to znany błąd („Jaro doradza szlifowanie zamiast padów”) |
| ObiektIQ | ewentualnie 3 zdania kontrolne dla zarządcy (połysk ≠ równość, pytaj o gradacje i pomiar) | zarządca nie steruje szlifierką |
| Anna, ARVIS, BHP | nic | poza domeną |

## 5. Decyzje potrzebne od Jarka

1. **Nazwa:** „Mink.AI” czy **MING**? W tekście jest Mink.AI — jeśli to literówka, poprawić wszędzie.
2. **Cytat Jarka:** tekst brzmi jak wygenerowany, a jest podpisany Twoim nazwiskiem. Zatwierdzasz go słowo w słowo po poprawkach 2, 3 i 6? Jeśli nie — nie wgrywamy cytatu.
3. **Wysłanie sekcji 3 do Jane Ling / Elaine** do potwierdzenia — tak/nie.
4. **Routing z sekcji 4** — akceptujesz?

Po odpowiedziach: czysta karta **CV-SZLIF-001** (część uniwersalna) + **MING-855LE-001** (część maszynowa), dopiero wtedy Notion → Pinecone.
