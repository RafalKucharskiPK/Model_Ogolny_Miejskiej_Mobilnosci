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

* Ok 15-25 rejonów
* Rejony spójne, zbliżone kształtem do kwadratu, okręgu
* Granice: naturalne (rzeki, skarpy, itp.), drogi wysokiej klasy, kolej
* Rejony pokrywają granice miasta
* W miare możliwości spójne zagospodarowanie: rejon mieszkaniowy, mieszkaniowy intensywny (zabudowa wielopiętrowa), mieszkaniowy jednorodziny, usługowy, przemysłowy.
* Zieleń (parki, lasy, jeziora) nie ma znaczenia, tak czy inaczej nie generuje on ruchu
* Im gęstsza zabudowa (intensywność) tym gęstszy podział na rejony (mniejsze rejony).
* Skupiamy się na mieście, pomijamy wsie podmiejskie będące w granicach miasta.

## Sieć drogowa

Sieć drogowa reprezentowana jest przez graf skierowany, w którym węzły (`Nodes`) to skrzyżowania, rozjazdy, ronda, węzły, wloty dróg do granic miasta, a odcinki (`Links`) to ulice łączące sąsiednie węzły. Węzły domyślnie nie są parametryzowane, a dla odinków określone są typy (`LinkTypes`) o typowej: prędkości ruchu swobodnego (`V0PrT`) 

## Podłączenia (konektory)
* Około 3 w każdym rejonie.
* Zawierają się w granicach rejonu (nie przekraczają granic rejonu).
* Każdy pomiędzy centroidą a węzłem
* Do mało istotnych węzłów.
* Nie mogą prowadzić do węzłów (skryżowań) dróg o klasie Z i wyższej
* Do mało istotnych skrzyżowań.
* Jeśli brakuje takich węzłów, dodajemy je (parkingi, ślepe uliczki, wjazdy do zakładów)
* Możemy podzielić odcinki niskich klas (`Split`) i stworzyć dodatkowy węzeł.
