## PROGNOZOWANIE RUCHU

# Rozpoczęcie

* Ściągnij licencję akademicką programu PTV Visum za pomocą http://cgi.ptvgroup.com/php/lng/vision_student_download.php?lng=en

* Sklonuj to repozytorium https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci (Zielony przycisk `Clone or Donwload` i potem `Download as ZIP`)

* Uruchom plik `MOMM.ver`

# Ćwiczenie testowe

* Wykonaj ćwiczenie pierwsze z http://www.zsk.pk.edu.pl/system/physicals/224/original/NiB_2018.pdf

# Pomoce dydaktyczne

* Visum Quickstart `\Users\Public\Documents\PTV Vision\PTV Visum 17\Tutorial_Quickstart\Visum_Quickstart_POL.pdf`

* Kanał YouTube KST, WIL, PK : https://www.youtube.com/channel/UCJKrYB7gHr1tvpckGlkhNnQ/videos

* Artykuły [moje](https://scholar.google.pl/citations?hl=pl&user=z3bOMUAAAAAJ&view_op=list_works&sortby=pubdate)
 i zacnych kolegów [T Kulpa](https://scholar.google.pl/citations?user=S4x1MBcAAAAJ&hl=pl&oi=ao) [A Szarata](https://scholar.google.pl/citations?user=HisPuLQAAAAJ&hl=pl&oi=ao) [A Drabicki](https://www.researchgate.net/profile/Arkadiusz_Drabicki)


## Podział na rejony komunikacyjne

[_FIlM_](https://www.youtube.com/watch?v=9jAzGmu1dKU)

* Ok 15-25 rejonów
* Rejony spójne, zbliżone kształtem do kwadratu, okręgu
* Granice: naturalne (rzeki, skarpy, itp.), drogi wysokiej klasy, kolej
* Rejony pokrywają granice miasta
* W miare możliwości spójne zagospodarowanie: rejon mieszkaniowy, mieszkaniowy intensywny (zabudowa wielopiętrowa), mieszkaniowy jednorodziny, usługowy, przemysłowy.
* Zieleń (parki, lasy, jeziora) nie ma znaczenia, tak czy inaczej nie generuje on ruchu
* Im gęstsza zabudowa (intensywność) tym gęstszy podział na rejony (mniejsze rejony).
* Skupiamy się na mieście, pomijamy wsie podmiejskie będące w granicach miasta.

### Zmienne objaśniające
Dla miasta określamy liczbę mieszkańców (wikipedia)
Zakładamy liczbę miejsc pracy na 40% liczby ludności (lub szukamy dokłądniejszych danych - GUS, UM, BIP itp.)
Zakładamy 60% miejsc pracy w usługach.
Zakładamy liczbę miejsc w szkołach równą 10% ludności 

Globalne wartości dzielimy uznaniowo pomiędzy rejony komunikacyjne na podstawie zagospodarowania. Szacujemy dla każdego rejonu:
* LICZBA_MIESZKANCOW	(na podstawie powierzchni zabudowy i jej instensywności - liczba kondygnacji)
* MIEJSCA_PRACY_W_USLUGACH	
*	MIEJSCA_PRACY_W_PRZEMYSLE	(na podstawie powierzchni przemysłowej i rodzaju działalności - magazyn a zakład produkcyjny)
* MIEJSCA_W_SZKOLACH	(na podstawie liczby szkół i danych o liczbie uczniów)

Wartości wpisujemy w `List(Zones) Wykaz(Rejony)` sprawdzając czy suma zgadza się z wartościami wejściowymi. 

## Sieć drogowa

Sieć drogowa reprezentowana jest przez graf skierowany, w którym węzły (`Nodes`) to skrzyżowania, rozjazdy, ronda, węzły, wloty dróg do granic miasta, a odcinki (`Links`) to ulice łączące sąsiednie węzły. Węzły domyślnie nie są parametryzowane, a dla odinków określone są typy (`LinkTypes`) o typowej: prędkości ruchu swobodnego (`V0PrT`) oraz przpeustowości (`CapPrT`).
Odwzorowujemy pełny układ uliczny miasta, pomijając tylko najmniej istotne odcinki. Nie kodujemy: - alejek parkowych, chodników, polnych dróg, deptaków, dojazdów do posesji, najmniej istotnych dróg dojazdowych, parkingów, ulic wewnątrz zakładów, galerii handlowych, itp.

### Węzły sieci drogowej
Wszystkie skrzyżowania, rozjazdy, wloty do miasta, końce odcinków, itp.
Upraszczamy geometrię węzłów, rond, skrzyżowań do pojedynczych punktów.
Limit liczby węzłów *500*

### Odcinki 
Odcinkami łączymy sąsiednie węzły. 
Odicnki są dwukierunkowe, mogą być asymetryczne.
Dla odcinków odzwierciedlamy geometrię (zakręty, łuki, itp.)
Określamy typy odcinków (wybrane z listy `LinkTypes`)
Ulice jednokierunkowe tworzymy zamykając wybrany kierunek i określając dla niego `TypeNo = 92 (Pieszo)` i `V0PrT=0`
Typowe błędy topologiczne, których należy unikać: http://intelligent-infrastructure.blogspot.com/2012/02/gis-shapefile-visum-transport-network.html

### Typy odcinków
Nie zmieniamy paramtrów w tabeli `LinkTypes`.
Wybieramy:
* prędkość (pierwsza część nazwy)
* liczbę pasów (druga część nazwy)
* klasę funkcjonalną (trzecia część nazwy)
_Prędkość_ identyfikujemy ograniczenia do 30km/h i niżej, oraz podwyższenia 70km/h
_Liczbę pasów_ identyfikujemy ze zdjęć satelitarnych

_Hierarchia sieci_ (na podstawie podkładu OSM):
* pomarańczowe, czerwone, fioletowe - Główne Ruchu Przyśpieszonego
* żółte - Główne
* białe grubsze - Zbiorcze
* białe cieńsze - Lokalne/Dojazdowe


## Podłączenia (konektory)
* Około 3 w każdym rejonie.
* Zawierają się w granicach rejonu (nie przekraczają granic rejonu).
* Każdy pomiędzy centroidą a węzłem
* Do mało istotnych węzłów.
* Nie mogą prowadzić do węzłów (skryżowań) dróg o klasie Z i wyższej
* Do mało istotnych skrzyżowań.
* Jeśli brakuje takich węzłów, dodajemy je (parkingi, ślepe uliczki, wjazdy do zakładów)
* Możemy podzielić odcinki niskich klas (`Split`) i stworzyć dodatkowy węzeł.
