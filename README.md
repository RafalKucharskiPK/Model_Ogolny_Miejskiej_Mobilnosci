# Model_Ogolny_Miejskiej_Mobilnosci
Ogólny model mobilności miejskiej dla miast małych i średnich zapisany w formie zbioru plików edytowalnych, oraz skompilowanych dla modelu mobilności zapisane w programie PTV VISUM (ver. 17.01-05) www.ptvgroup.com/pl
Do celów dydaktycznych, edukacyjnych, rozwojowych, badawczych i innych.
Zawiera:
* model dla miasta średniego w formie pliku .ver w wersji [pustej](https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci/blob/master/MOMM_pusty.ver) , oraz z przykładowym modelem dla [Gniezna](https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci/blob/master/MOMM.ver), 
* menadżer scenariuszy dla modelu Gniezna
* zbiór materiałów dydaktycznych
* zbiór edytowalnych otwartych plików z parametrami sieci, UDAs, procedurami, formułami modelu popytu, dla innych modeli (Kraków, Małopolska, Warszawa i inne)

## Ogólny sposób użycia

*Najprostszy* klikamy zielony przycisk `Clone or Download` i potem `Download ZIP` - mamy repozytorium na naszym komputerze, możemy go używać.
*Najlpeszy* Jest ot repozytorium github które pozwala na zarządzanie wersjami, pracę wspólną i ciągłą aktualizacje. Dla chcących poznać podstawy github [polecam](https://guides.github.com/activities/hello-world/), dla nieprogramistów polecam [GitHubDesktop](https://desktop.github.com)
*Jeszcze lepszy* Dla chcących dołączyć do tego pojektu (*collaborator*), dodawać, poprawiać i edytować pliki zapraszam. Proszę o kontakt mailowy rkucharski@pk.edu.pl, lub po prostu o: *stworzenie brancha wraz z commitami i opisem a potem pull request na merge do master* (wprost przepiękna polszczyzna :D)

# Zawartość


## Plik MOMM.ver
Plik MOMM.ver zawiera plik programu PTV VISUM możliwy do otwarcia przy użyciu wersji akademickiej porgramu do pobrania ze strony http://cgi.ptvgroup.com/php/lng/vision_student_download.php?lng=en

Model ten zawiera bazową sieć drogową dla:
* wybranego miasta (Gniezno), 
* sparametryzowaną zgodnie z typami odcinków określonymi w [link_types.net](https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci/blob/master/dane/srednie/link_types.net)
* z funkcjami oporu BPR3 dla wszystkich odcinków, zgodnie z [proecdures.xml](https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci/blob/master/dane/srednie/procedures.xml)
* z modelem popytu określonym w [dmd.dmd](https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci/blob/master/dane/srednie/dmd.dmd)
* o 9 motywacjach podróży 
```
D-P-D, D-I-P, D-N-D, D-U-D, D-I-D, NZD
```
* liczbie podróży określanej na podstawie zmiennych objaśniających rejonów 
```
LICZBA_MIEJSC_PRACY_OGOLEM
LICZBA_MIESZKANCOW
MIEJCA_PRACY_W_USLUGACH
MIEJSCA_NA_UCZELNIACH
MIEJSCA_PRACY_W_PRZEMYSLE
MIEJSCA_W_SZKOLACH
```
* parametrach modelu popytu określonych na poziomie `DemandStrata'

```
 | CODE | NAME | D_RUCHLIWOSC_DOBOWA | D_ASC | U_KZ | D_URANO | D_UPOPO | D_WSPNAPELNIENIA | D_MNOZNIKSEZONOWY |
| 01 D-P | Dom - Praca | 0.40 | 10 | 0.45 | 0.30 | 0.01 | 1.30 | 1.00 |
| 02 P-D | Praca - Dom | 0.35 | 10 | 0.45 | 0.00 | 0.32 | 1.30 | 1.00 |
| 03 D-N | Dom - Nauka | 0.10 | 10 | 0.80 | 0.15 | 0.01 | 1.30 | 1.00 |
 | 04 N-D | Nauka - Dom | 0.10 | 10 | 0.80 | 0.00 | 0.10 | 1.30 | 1.00 |
| 05 D-U | Dom - Uczelnia | 0.05 | 10 | 0.70 | 0.10 | 0.01 | 1.30 | 1.00 |
| 06 U-D | Uczelnia - Dom | 0.05 | 10 | 0.70 | 0.00 | 0.10 | 1.30 | 1.00 |
| 07 D-I | Dom - Inne | 0.20 | 10 | 0.30 | 0.10 | 0.10 | 1.30 | 1.00 |
 | 08 I-D | Inne - Dom | 0.25 | 10 | 0.30 | 0.00 | 0.15 | 1.30 | 1.00 |
 | 09 NZD | Nie związane z domem | 0.00 | 10 | 0.40 | 0.05 | 0.15 | 1.30 | 1.00 |
```

* zestawie procedur określonym w [proecdures.xml](https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci/blob/master/dane/srednie/procedures.xml)


## Folder MOMM - manadżer scenariuszy

W folderze tym znajduje się manadżer scenariuszy otwierany poprzez [MOMM.vpdbx](https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci/blob/master/MOMM/MOMM.vpdbx) 
base version to MOMM.ver (opisany powyżej).
* Podstawowe wskaźniki: 'PojKm, PojH, VŚrednia`
* Jedna modyfikacja zmiany w liczbie ludności
* Jedna modyfikacja zmiany w sieci (inwestycja drogowa)
* Trzy modyfikacje dla szczytu porannego, popołudniowego i doby
* Cztery scenariusze: bazowy, więcej ludności, nowa inwestycja, nowa inwestycja plus więcej ludności.

## Folder **dane**

Dane w formie edytowalnej (`link_types.net, procedures.xml, dmd.dmd`), w miarę dostępności z opisami  dla modeli:
* Opisanego powyżej
* Krakowa (2013)
* Warszawy (MTAW 2015)
* Regionalnego Modelu Ruchu (w ramach RID)
* zapraszam do dodawania swoich (po uprzednim upewnieniu się, że nie pójdziemy za to do więzienia)

## Folder dydaktyka

Z materiałami dydaktycznymi - opisy w odpowiednich folderach


## Cytowanie 
Przy każdym uzyciu proszę cytować jako jako: *Rafal Kucharski. (2018, March 27). RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci: First release (Version 0.0.1). Zenodo. http://doi.org/10.5281/zenodo.1208635* [![DOI](https://zenodo.org/badge/126968926.svg)](https://zenodo.org/badge/latestdoi/126968926) 

## Licencja 

[licence](https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci/blob/master/LICENSE)






