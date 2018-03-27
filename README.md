# Model_Ogolny_Miejskiej_Mobilnosci
## Ogólny model mobilności miejskiej dla miast małych i średnich - (c) Rafal Kucharski, Politechnika Krakowska, 2018

Model zawiera pliki edytowalne, oraz skompilowane dla modelu mobilności zapisane w programie PTV VISUM (ver. 17.01-05) www.ptvgroup.com/pl

## Licencja 

[licence](https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci/blob/master/LICENSE)

## Ogólny sposób użycia

Dla chcących poznać podstawy [github](https://guides.github.com/activities/hello-world/), dla innych po prostu klikamy zielone `Clone or Download` i `Download ZIP`
Dla chcących dodawać i edytować pliki zapraszam, proszę wówczas o stworzenie brancha wraz z opisem i pull request na merge do master (wprost przepiękna polszczyzna)

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

## Cytowanie 
Przy każdym uzyciu proszę cytować jako jako: *Kucharski R., 2018, Model Ogólny Miejskiej Mobilności, GitHub repository, DOI: 10.5281/zenodo.1208635* [![DOI](https://zenodo.org/badge/126968926.svg)](https://zenodo.org/badge/latestdoi/126968926) 





