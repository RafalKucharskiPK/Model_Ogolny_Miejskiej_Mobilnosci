# Ćwiczenie 1

korzystając z Miejskiego Systemu Informacji Prestrzennej (http://msip.um.krakow.pl/obserwatorium/)
Wybrać dowolną ulicę w Krakowie zaczynającą się taką samą literę jak Wasze imie i numer adresowy taki jak dwie ostatnie cyfry Waszego numer albumu.
Dla tego adresu proszę przygotować 3 wydruki dla otoczenia (r ~100m) tego adresu:
1. wybrane 3 warstwy wektorowe
2. wybraną warstwę rastrową
3. wybrane ciekawe informacje przydatne w projektowaniu.
Przedstawić w formie pliku pdf i przesłać na adres mailowy.

# Ćwiczenie 2

Dla dwóch warstw wektorowych:
* miejscowości na lubelszczyźnie wraz z populacją
* linie kolejowe

określić dla każdej linii kolejowej liczbę mieszkańców w promieniu 10 km

Narzędzia (PTV Visum).
Operacje:

* Import shapefile
  * linie jako links
  * odcinki jako stops
  * read additevely
* Calculate/Procedures create: Miscellaneous/Intersect
  * Target: _Links_ (koleje) Buffer size _10 000 m_
  * Source: _Stops_ (miejscowosci) Buffer size_0m_ 
  * Destination attribute ADDVAL1
 * Odczytaj wartości dla wybranych linii kolejowych
