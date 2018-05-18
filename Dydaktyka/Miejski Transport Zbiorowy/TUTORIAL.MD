## PROGNOZOWANIE RUCHU

# Rozpoczęcie

* Ściągnij licencję akademicką programu PTV Visum za pomocą http://cgi.ptvgroup.com/php/lng/vision_student_download.php?lng=en

* Sklonuj to repozytorium https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci (Zielony przycisk `Clone or Donwload` i potem `Download as ZIP`)

* Uruchom plik `MOMM.ver` - sprawdź czy działa


# Ćwiczenie testowe

* Wykonaj ćwiczenie pierwsze z http://www.zsk.pk.edu.pl/system/physicals/224/original/NiB_2018.pdf

# Pomoce dydaktyczne

* Visum Quickstart `\Users\Public\Documents\PTV Vision\PTV Visum 17\Tutorial_Quickstart\Visum_Quickstart_POL.pdf`

* Kanał YouTube KST, WIL, PK : https://www.youtube.com/channel/UCJKrYB7gHr1tvpckGlkhNnQ/videos

* Artykuły [moje](https://scholar.google.pl/citations?hl=pl&user=z3bOMUAAAAAJ&view_op=list_works&sortby=pubdate)
 i zacnych kolegów [T Kulpa](https://scholar.google.pl/citations?user=S4x1MBcAAAAJ&hl=pl&oi=ao) [A Szarata](https://scholar.google.pl/citations?user=HisPuLQAAAAJ&hl=pl&oi=ao) [A Drabicki](https://www.researchgate.net/profile/Arkadiusz_Drabicki)

# 1. Budowa modelu sieci

Otwieramy plik [MOMM_pusty.ver](https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci/blob/master/MOMM_pusty.ver)
Wybieramy miasto około 50k mieszkańców, samodzielne (nie będącego częścią aglomeracji). 
Zbliżamy obszar widoku do granic tego miasta (interesuje nas granica zabudowy, a nie administracyjna). Możemy pomijać pola, łątki i lasy w granicach, pomijamy rozległe wsie podmiejskie. Nie pomijamy podmiejskich stref przemysłowych, centrów handlowych.
Dla mia

## Podział na rejony komunikacyjne

[_FILM_](https://www.youtube.com/watch?v=byujp2ufNE0)

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

[_FILM_](https://www.youtube.com/watch?v=gIF1vGXIJOA)

Wszystkie skrzyżowania, rozjazdy, wloty do miasta, końce odcinków, itp.
Upraszczamy geometrię węzłów, rond, skrzyżowań do pojedynczych punktów.
Limit liczby węzłów *500*



### Odcinki 

[_FILM_](https://www.youtube.com/watch?v=47VBFejHEkg)
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

## Praca offline
[_FILM_](https://www.youtube.com/watch?v=UKozzlcnxPQ)

## Testy:

* Test spójności sieci: `Calculate -> Network Check...`
* Test macierzy kosztów. Użyj zestawiu procedur [P000005.xml](https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci/blob/master/MOMM/Procedures/P000005.xml) - przeciągnij i upuść do modelu, oblicz zestaw procedur (przycisk *Play*). Sprawdź macierze `10	TT0	t0 ; 11	TTC	tCur ; 12	DIS	Trip distance SO` pod kątem braku spójności. Wartość `999999` oznacza brak połączenia w danej relacji. Do dalszych prac konieczne jest poprawienie sieci (brak wartości `999999` w macierzy).

# 2. Wykonanie obliczeń w modelu

## Obliczenia

Po zdefiniowaniu zmiennych objaśniających rejonów (`LICZBA_MIESZKANCOW, MIEJSCA_PRACY_W_USLUGACH, MIEJSCA_PRACY_W_PRZEMYSLE, MIEJSCA_W_SZKOLACH`)
Wykonaj zestaw przygotowanych  procedur:
* Obliczenie macierzy kosztów
* Model popytu:
* Model generacji ruchu
* Model grawitacyjny (rozkładu podróży)
* Model wyboru środka transportu
* Rozkład ruchu na sieć (`PrTAssignment`)


## Wizualizacja wyników
Po wykonaniu sprawdź wyniki rozkładu ruchu, przeciągnij i upuść plik [Potoki.gpa](https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci/blob/master/MOMM/SharedData/Potoki.gpa) do programu. Odcinki powinny mieć grubości pokazujące wielkość potoku pojazdów.

## Wskaźniki modelu

Dodaj w dowonlym, widocznym miejscu obiekt `Territory` - jego parametry graficzne zawierają główne parametry modelu. Pracę przewozową w pojazdogodzinach, pojazdokilometrach, oraz prędkość średnią.

Interesują nas trzy podstawowe wskaźniki funkcjonowania sieci:
* Pojazdo-kilometry - całkowity dystans pokonywany przez pojazdy zaspokajające popyt na podróże (przejeżdzające ze źródła do celu).
* Pojazdo-godziny - całkowity czas podróży wszystkich pojazdó zaspokajające popyt na podróże (przejeżdzających ze źródła do celu).
* Średnia prędkość w sieci - iloraz pojazdokilometrów i pojazdo-godzin.


# 3. Prognozowanie z użyciem modelu

## Inwestycje drogowe

W osobnych plikach zapisz modyfikacje ukłądu drogowego. Zakoduj trzy osobne nowe inwestycje drogowe. Szukaj inwestycji rozwiązujących faktyczne porblemy komunikacyjne. Dobierz inwestycje tak, by skorzystała z niej jak największa liczba kierwców (pojazdów). Zaproponuj trzy inwestycje, z czego jedna lokalna o małej skali (łącznik, nowy krótki odcinek) a jedna o dużej (arteria, obwdnica, trasa śródmiejska). 
Wykonaj obliczenia rozkłądu ruchu na siec dla każdej ze zmodyfikowanych sieci i opisz w tabeli jej wpływ na wskaźniki funkcjonowania sieci.
Każdą z inwestycji zwizualizuj, oraz zapisz w osobnym pliku (`W1.ver, W2.ver, W3.ver`)

## Generatory ruchu

Zaproponuj lokalizacje w miejscie dla nowego:
* Centrum Handlowego (min. 500 miejsc pracy w usługach)
* Fabryki (min. 2 000 miejsc pracy w przemyśle)
* Osiedla mieszkaniowego (min. 2 000 mieszkańców).

Oszacuj wpływ realizacji tych inwestycji na wskaźniki sieci. 
Dla każdego z nich dodaj osobny rejon komunikacyjny, włącz go w konektorem w rozbudowaną sieć drogową.
Oblicz model popytu oraz rozkład ruchu na sieć.
Każdy wariant inwestycyjny zapisz w osobnym pliku i opisz w tabeli jego wpływ na wskaźniki funkcjonowania sieci.

## * Z użyciem scenario manager (opcjonalnie):


Scenariusze obliczamy w `Scenario Manager`.
Otwieramy kopię foldera `MOMM` , otwieramy plik `MOMM.vpdbx`, klikamy `Edit Base Version` otwieramy nasz plik, klikamy `Save`.
Każdy ze scenariuszy zapisujemy jako `Modification` w `ScenarioManager`, do każdego tworzymy scenario, wybierając zestaw procedur nr 1.


# Zaliczenie

W ramach zaliczenia prezentujemy:
* Podział na rejony komunikacyjne.
* Model sieci drogowej wraz z klasifykacją (struktura typów odcinków w sieci).
* Rozmieszczenie zmiennych objaśniających w sieci (miejsca pracy, mieszkańcy, itp.) z komenatrzem (gdzie mało, gdzie duże i dlaczego).
* Rozkład ruchu na sieć w wariancie bazowym z komentarzem (gdzie dużo pojazdów, gdzie zatłoczenie i dlaczego).
* Wskaźniki i obciążenia sieci dla trzech inwestycji z komentarzem (najlepsza, najgorsza, takie a nie inne efekty realizacji).
* Wskaźniki i obciążenia dla generatorów ruchu z komentarzem (gdzie i dlaczego budujemy, jaki to ma wpływ na sieć).
