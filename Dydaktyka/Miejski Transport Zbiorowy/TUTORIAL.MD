## Miejski Transport Zbiorowy

# Rozpoczęcie

* Ściągnij licencję akademicką programu PTV Visum za pomocą http://cgi.ptvgroup.com/php/lng/vision_student_download.php?lng=en

* Sklonuj to repozytorium https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci (Zielony przycisk `Clone or Donwload` i potem `Download as ZIP`)

* Uruchom plik `MOMM.ver` - sprawdź czy działa



# Pomoce dydaktyczne

* Visum Quickstart `\Users\Public\Documents\PTV Vision\PTV Visum 17\Tutorial_Quickstart\Visum_Quickstart_POL.pdf`

* Kanał YouTube KST, WIL, PK : https://www.youtube.com/channel/UCJKrYB7gHr1tvpckGlkhNnQ/videos

 * [Instrukcja wykonania modelu](https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci/blob/master/Dydaktyka/PrognozowanieRuchu/TUTORIAL.MD)

* Artykuły [moje](https://scholar.google.pl/citations?hl=pl&user=z3bOMUAAAAAJ&view_op=list_works&sortby=pubdate)
 i zacnych kolegów [T Kulpa](https://scholar.google.pl/citations?user=S4x1MBcAAAAJ&hl=pl&oi=ao) [A Szarata](https://scholar.google.pl/citations?user=HisPuLQAAAAJ&hl=pl&oi=ao) [A Drabicki](https://www.researchgate.net/profile/Arkadiusz_Drabicki)
 


# 1. Praca z modelem - analiza sieci PrT

* Otworz [model bazowy](https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci/blob/master/MOMM/MOMM.vpdbx).
* Zbliż widok do zakresu modelu.
* Włącz tło mapowe i określ jakie to miasto.
* Kliknij wybrany węzeł *Node* w sieci i odczytaj jego koordynaty.
* Kliknij wybrany odcinek *Link* w sieci i odczytaj dla niego *TypeNo, Capacity, V0PrT, t0PrT*.
* Kliknij wybrany rejon komunikacyjny *Zone* i odczytaj jego produkcję i atrakcję w wybranej motywacji, oraz zmienne objaśniające modelu popytu (np. Liczba Mieszkańców).
* Znajdź węzeł o najwyższym numerze.
* Znajdź najdłuższy odcinek.
* Jaka jest całkwoita liczba ludności we wszystkich rejonach modelu
* Znajdż najkrótszą ścieżkę w sieci pomiedzy skrzyżowaniem Słoneczna/Witkowska, a rejonem nr 19.

# 2. Praca z modelem - analiza wyników PrT

* Otwórz wyniki obliczeń w scenariuszu 4: Wariant bazowy
* Wybierz opcję graficzną (*GPar*) "Potoki"
* Odczytaj dla wybranego odcinka o dużym potoku parametry *Volume PrT, VolCapRatio PrT, tCur, vCur*.
* Otwórz macierz dla której wykonany był rozkład:
** znajdź rejon o największej produkcji i największej atrakcji.
** znajdż parę rejonów o największej liczbie podróży.
* Odczytaj rozkład potoków (FlowBundle) w sieci dla:
** pary rejonów o największym potoku,
** rejonu o największej produkcji,
** odcinka o największym potoku.
* Odczytaj i zinterpretuj prace przewozową w pojazdogodzinach i pojazdokilometrach. Oblicz średnią długość i średni czas trwania podróży.

# 3. Praca z modelem - scenariusze zmian

* Na podstawie wyników obciążenia sieci zapropnuj nową inwestycję drogową.
* Zakoduj odpowiednie zmiany w sieci.
* Wykonaj rozkład ruchu.
* Odczytaj liczbę pojazdów na planowanym odcinku
* Pokaż wiązkę pojadów (*FLow Bundle*) dla planowanego odcinka.
* Określ zmianę w pracy przewozowej i prędkości średniej w sieci.

# 4. Praca z modelem - porównania

# 5. Praca z modelem - budowa własnego modelu

 * [Instrukcja wykonania modelu](https://github.com/RafalKucharskiPK/Model_Ogolny_Miejskiej_Mobilnosci/blob/master/Dydaktyka/PrognozowanieRuchu/TUTORIAL.MD)

