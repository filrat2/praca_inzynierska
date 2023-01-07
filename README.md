Wykrywanie farm fotowoltaicznych na podstawie danych teledetekcyjnych
================
Author: [Filip Ratajszczak](https://www.linkedin.com/in/filip-ratajszczak/)<br>
Affiliation: [Wydział Nauk Geograficznych i Geologicznych](https://wngig.amu.edu.pl/)<br>
Published: Jan. 7, 2023<br>

### Spis treści
* [Wstęp](#wstęp)
* [Cel pracy](#cel-pracy)
* [Planowane etapy pracy](#planowane-etapy-pracy)
* [Planowany efekt pracy](#planowany-efekt-pracy)
* [Dodatkowe źródła informacji](#dodatkowe-źródła-informacji)

## Wstęp

Tematem pracy inżynierskiej jest wykrywanie farm fotowoltaicznych
na podstawie danych teledetekcyjnych jednego lub dwóch pułapów (pułapu
satelitarnego lub pułapu satelitarnego i lotniczego). Praca zakłada
wykorzystanie nowoczesnych technologii (uczenia maszynowego (*ang. machine learning)* 
i/lub uczenia głębokiego (*ang. deep learning)*
w postaci sieci neuronowych (*ang. neural networks*)).

Następujące zmiany klimatyczne wymuszają transformację energetyczną,
która zakłada odejście od produkcji energii z paliw kopalnych na rzecz
odnawialnych źródeł energii i energetyki jądrowej. Proces ten jest
bardzo dynamiczny, więc obserwowanie zachodzących zmian jest ważne,
a zarazem bardzo trudne z powodu niejednolitej organizacji działania
władz samorządowych na różnych szczeblach podziału administracyjnego
w Polsce oraz występowania na terenie Polski różnych operatorów
energetycznych.

Wykorzystanie nowoczesnych metod detekcji pozwala na stosunkowo szybkie
wykrywanie różnego typu zmian masowych zachodzących na dużych
powierzchniach, nawet na powierzchni całej Ziemi. Rozwijające
się systemy obserwacji planety dostarczają coraz więcej danych, stale
skracane są czasy rewizyt oraz zwiększana jest rozdzielczość
przestrzenna w nowych, kolejnych misjach czy programach. Dane zostają
również coraz częściej uwalniane - udostępniane są do pobierania za
darmo, w przyjazny dla użytkownika sposób - za pomocą portali
internetowych takich jak np. [CREODIAS](https://creodias.eu/), bez
potrzeby pisania wniosków o dostęp do informacji.

W Bazie Danych Obiektów Topograficznych ([BDOT
10k](https://www.geoportal.gov.pl/dane/baza-danych-obiektow-topograficznych-bdot))
zawarte są dane na temat lokalizacji turbin wiatrowych w Polsce.
W oficjalnych, dostępnych w Polsce danych brakuje jednak informacji
na temat lokalizacji farm/elektrowni fotowoltaicznych. Wśród
nieoficjalnych źródeł danych informacje na ten temat można znaleźć
m.in. w projekcie społeczności internetowej
[OpenStreetMap](https://www.openstreetmap.org/) pod atrybutem/tagiem
[“solar”](https://wiki.openstreetmap.org/wiki/Tag:generator:source%3Dsolar),
dane te są jednak nieformalne, niepełne i nieaktualne.

### Możliwe problemy:

- różne układy współrzędnych wykorzystywanych danych (Ortofotomapa -
  [ETRF2000-PL / CS92](https://epsg.io/2180); Sentinel-2, PlanetScope -
  [WGS 84 / UTM zone 33N](https://epsg.io/32633); Google Satellite,
  Planet Basemaps, Bing Aerial, Mapbox Satellite itp. - [Web
  Mercator](https://epsg.io/3857))

- program Sentinel-2 oferuje tylko 4 kanały w rozdzielczości 10 m, a 10
  kanałów w rozdzielczości 20 m - możliwe, że konieczne będzie
  wykorzystanie kanałów o niższej (gorszej) rozdzielczości

- brak aktualnych ortofotomap

- podobna barwa farm fotowoltaicznych do innych obiektów
  antropogenicznych (np. szklarnie, zabudowa przemysłowa, place
  parkingowe itp.) lub czasami nawet gołe pola (przynajmniej
  na kompozycji RGB na podstawie danych Sentinel-2)

- różne typy pokrycia powierzchni pomiędzy modułami fotowoltaicznymi
  (trawa, goła gleba itp.), co może wpływać na wartości odbicia
  spektralnego w kanałach

- potrzeba dużej mocy obliczeniowej przy wykorzystaniu uczenia
  głębokiego (sieci neuronowych)

## Cel pracy

Celem pracy jest stworzenie algorytmu umożliwiającego wykrywanie farm
fotowoltaicznych na podstawie danych teledetekcyjnych na szczeblu
regionalnym lub krajowym, którego produktami będą przestrzenne dane
wektorowe lub rastrowe.

Zlokalizowane farmy (jako dane przestrzenne) mogą być wykorzystane
w wielu celach, np.:

- prowadzenie statystki energii odnawialnej w Polsce

- inwentaryzacja ilościowa i powierzchniowa farm fotowoltaicznych
  na różnych szczeblach podziału administracyjnego (gminnym, powiatowym,
  wojewódzkim, krajowym)

- szacowanie ilości energii jaką aktualnie takie instalacje wytwarzają
  na terenie danych jednostek podziału administracyjnego

- monitorowanie zachodzących zmian w wybranych interwałach czasowych
  (np. co rok) - uruchamianie algorytmu w regularnych odstępach czasu
  na podstawie najnowszych dostępnych danych

## Planowane etapy pracy

1.  Stworzenie zbioru danych testowych i treningowych na obszarze kafla
    T33UWV ze zbioru danych Sentinel-2 na podstawie rastrowych warstw
    sieciowych: ortofotomapy, Google Satellite, Bing Aerial, Mapbox
    Satellite, Planet Basemaps

2.  Stworzenie algorytmu uczenia maszynowego do wstępnego wykrywania
    farm fotowoltaicznych na obszarze kafla T33UWV ze zbioru danych
    Sentinel-2 (wykorzystywane dane: Sentinel-2, rozdzielczość 10 lub 20 m)

3.  Zależnie od czasu, w jakim zostanie zakończony etap drugi oraz jego
    wyników, możliwe są dwie ścieżki rozwoju pracy:

    3a. pobranie ortofotomapy (rozdzielczość 25 cm) dla obszarów
    wstępnie wytypowanych w etapie 2. za pomocą pakietu
    [rgugik](https://kadyb.github.io/rgugik/) (Dyba, Nowosad 2021);
    stworzenie algorytmu uczenia głębokiego do wykrywania dokładnych
    granic farm fotowoltaicznych

    3b. pobranie danych satelitarnych z programu PlanetScope
    (rozdzielczość 3 m) dla obszarów wstępnie wytypowanych 
    w etapie 2. za pomocą [Planet API](https://developers.planet.com/docs/apis/),
    stworzenie algorytmu uczenia maszynowego do wykrywania dokładnych
    granic farm fotowoltaicznych

4.  Wykorzystanie stworzonych algorytmów na większym obszarze, np. kilku
    kafli Sentinel-2 lub obszaru całej Polski

5.  Stworzenie produktów końcowych - danych przestrzennych
    reprezentujących farmy fotowoltaiczne

## Planowany efekt pracy

Planowanymi efektami pracy są:

- algorytm(y) umożliwiające wykrywanie farm fotowoltaicznych
  na podstawie danych teledetekcyjnych

- dane przestrzenne stworzone przez algorytm(y) na podstawie danych
  teledetekcyjnych: warstwa z obiektami o geometrii typu polygon
  lub warstwa rastrowa (powierzchniowa reprezentacja farm
  fotowoltaicznych) i/lub warstwa z obiektami o geometrii typu point
  (punktowa reprezentacja występowania farmy fotowoltaicznej w danym
  miejscu (centroidy obiektów o geometrii typu polygon))
</p>

## Dodatkowe źródła informacji

### Dane

- Program Sentinel-2 <br> [kanały
  Sentinel-2](https://docs.sentinel-hub.com/api/latest/data/sentinel-2-l2a/#available-bands-and-data)
  \| [CREODIAS](https://creodias.eu/)
- Program PlanetScope <br> [kanały
  PlanetScope](https://developers.planet.com/docs/apis/data/sensors/) \|
  [Planet](https://www.planet.com/?utm_source=google&utm_medium=paid-search&utm_campaign=discovery-brd&utm_content=homepage)
- Ortofotomapa GUGiK <br>
  [Ortofotomapa](https://www.geoportal.gov.pl/dane/ortofotomapa) \|
  [GUGiK](https://www.gov.pl/web/gugik)

### Literatura

- praca licencjacka [Detekcja kolektorów i paneli słonecznych
  na podstawie zdjęć lotniczych miasta Poznania z wykorzystaniem
  głębokich sieci
  neuronowych](https://github.com/DepartmentOfStatisticsPUE/prace-dyplomowe/blob/master/licencjat/2019-voss112124lic.pdf)
  (Voss 2019)
- praca magisterska [Wykorzystanie głębokich sieci neuronowych
  na potrzeby statystyki energii
  odnawialnej](https://github.com/DepartmentOfStatisticsPUE/prace-dyplomowe/blob/master/magisterskie/2021-voss.pdf)
  (Voss 2021)

