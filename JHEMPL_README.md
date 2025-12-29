
# Název projektu
### Webcraping a analýza pronájmů bytů ve Zlíně
Tento projekt slouží k získávání dat o pronájmech bytů z webu [Sreality.cz](https://www.sreality.cz) a následné analýze těchto dat.

#### README obsahuje:
* I.  Informace o projektu
* II. Pokus o interpretaci získaných a analyzovaných dat (stažených ke dni 22. prosince 2025)

# I. Informace o projektu
Program se skládá ze tří jednotlivých částí:

* Webscriping (Extraction)
* Transformace a číštění dat (Transformation)
* Datová analýza + jednoduché vizualizace

## 1. Webscriping
### A. Vytvoření scriptu pro stažení dat z webu 'www.sreality.cz'
- Extrakce informací:
  * Město
  * Ulice
  * Dispozice bytu
  * Rozměry bytu 
  * Cena pronájmu 
  * Odkaz na inzerát

### B. Export uložených dat do souboru _surova_data.csv a vytvoření pd.DataFrame

## 2. Transformace dat (& data cleaning)
### 2.1 Záklaní informace o datasetu za účelem zjištění úkolů pro data cleaning
### 2.2 Čištění dat: odstranění duplicit, nahrazení prázdných hodnot
### Export očištěných dat do souboru _zdrojova_data.csv.

## 3. Datová analýza a vizualizace dat

- Průměrná a mediánová cena pronájmu
- Porovnání cen podle dispozice
- Průměrná velikost bytů podle dispozice
- Identifikace ulic s nejvyšší koncentrací dražších bytů
- Grafy:
  - Sloupcové grafy (bar chart) 

## Požadavky
- Python 3.x
- Knihovny:
  - pandas
  - matplotlib
  - requests
  - beautifulsoup4

## Použití
1. Spustit buňky v Jupyter Notebooku.
2. Data uložena ve dvou souborech .csv: a) surová data, b) zdrojová data
3. Data se uloží do DataFrame `df_inzeraty`.
4. Provede se analýza a vizualizace dat.

## Autor
Jiří Hempl



# II. Pokus o interpretaci zjištěných a analyzovaných dat

### Poznámka:
* Níže uvedené komentáře zohledňují data stažená ze dne 23. 12. 2005. S ohledem na přesnost a objektivní posouzení jsou komentáře založeny pouze na zanalyzovaných datech, vyhýbají se spekulativním závěrům, které by zohledňovali externí proměnné např. (vyjma vývy k takové úvaze u otázky č. 5): lokalita, občanská vybavenost, demografické údaje, poptávka po pronájmech, stav nemovitosti atd, neboť nemáme k dispozici relevantí údaje, abychom je mohli do analýzy a komentářů zahrnout. Pakliže se tyto proměnné v komentáři objeví, jde o obecné konstatování.

* Extrahovaných inzerátů celkem 222, po očištění dat je přístupných 211 inzerátů

## Otázka č. 1
### Jaká je průměrná cena bytů, uveďte medián pro srovnání.
Průměrná cena pronájmu bytu je 14963 Kč, kdežto medián je 14000 Kč.
Průměr je vyšší než medián o 963 Kč (6.88 %).

__Interpretace:__ 
_Nižší hodnota mediánu oproti průměru naznačuje, že více než polovina bytů má nájem nižší než průměrná cena; jde o levné a středně drahé byty. Průměrná cena bytu je ovlivněna menším počtem (extrémně vůči průměrné ceně) vysokých nájmů, které tuto zvyšují._

## Otázka č. 2
### Jaká je průměrná cena bytů pro každou dispozici? Zobrazit i na grafu.
      Dispozice  Cena pronájmu (Kč/měsíc)
    0      3+kk                   21204.0
    1      4+kk                   18250.0
    2       4+1                   17946.0
    3       3+1                   17642.0
    4      2+kk                   15910.0
    5       2+1                   14795.0
    6       1+1                   12520.0
    7      1+kk                   11593.0
    8    pokoje                    7100.0

__Interpretace:__ _Průměrná výše nájmu u bytu s dispozicí 3+kk se nachází nad 21 tis Kč, jde o cenu výrazně vysoko nad průměrem; nabízená cena pronájmu za 3+kk je o 2 954 Kč dražší než za byt 4+kk, ačkoli 4+kk je v průměru o 5 m2 větší. Byty s dispozicí 3+1 a 4+1 mají podobnou průměrnou cenu, liší se cca 300 Kč, příčemž rozdíl v m2 je 30 m2 v prospěch bytu 4+kk. Nejblíže k průměrné ceně má byt s dispozicí 2+1. S ohledem na výsledek otázky č. 1 lze konstatovat, že pokoje, byty s dispozicí 1+kk, 1+1, 2+1 tvoří cca 50 % všech nabídek._

## Otázka č. 3
#### Jaká je průměrná velikost bytu pro každou dispozici? Zobrazte i na grafu.
          Dispozice  Rozměry bytu (m2)
    0       4+1              101.0
    1      4+kk               92.0
    2      3+kk               87.0
    3       3+1               71.0
    4       2+1               61.0
    5      2+kk               55.0
    6       1+1               37.0
    7      1+kk               33.0
    8    pokoje               18.0

__Interpretace:__ _Minimální rozdíl v rozloze bytu je mezi 1+kk a 1+1, rozdíl je v průměru o 4 m v prospěch bytu 1+1. U bytů 2+kk a 2+1 je to 6 m. Naopak největší rozdíl je mezi byty 3+kk a 3+1, v průměru 16m2._

## Otázka č. 4
#### Existuje ulice, kde jsou vyšší koncentrace dražších bytů? (Definujte "dražší" jako byty nad průměrnou cenou. Zobrazte top 5 ulic s nejvyšší průměrnou cenou.)

                 Ulice      Průměrný nájem
    0            Sýkory II         29000.0
    1  Jarolímkovo náměstí         25000.0
    2         Kpt. Nálepky         24000.0
    3               Mostní         23333.0
    4     Benešovo nábřeží         22250.0

__Interpretace:__ _Cena pronájmu bytu může být závislá na lokalitě, vybavenosti bytu, dostupnosti veřejné vybavenosti, přístupem k přírodě, bozpečnostní situací dané lokality, stavu nemovitosti atd._

## Otázka č. 5
#### Jaký typ dispozice je v daném městě nejčastěji inzerován? který typ dispozice to je? Proč myslíte, že tomu tak je? Graf bar chart nebo pie chart?

      Dispozice  Počet bytů  Podíl (%)
    0      1+kk          48      22.75
    1      2+kk          42      19.91
    2       2+1          35      16.59
    3       1+1          29      13.74
    4      3+kk          27      12.80
    5       3+1          19       9.00
    6    pokoje           5       2.37
    7       4+1           4       1.90
    8      4+kk           2       0.95

__Interpretace:__ _„Nejvíce nabízených bytů jsou byty s dispozicí 1+kk (48 inzerátů, 22,75 %) a 2+kk (42 inzerátů, 19,91 %) — dohromady tvoří cca 42 % všech nabídek. Menší dispozice obecně dominují v nabídce, což může být vysvětlováno tím, že tyto jednotky jsou obecně atraktivnější pro širší skupinu potenciálních nájemců a tvoří tak podstatnou část trhu._ 

Pokud jde o otázku "Proč je nejvíce nabízených bytů s dispozicemi 1+kk, 2+kk, lze říci následující:
* z pohledu pronajímatele může jít o zohlednění atraktivity těchto dispozic ze strany zájemců (singles, mladé páry, studenti, dojíždějící pracující), z tohoto důvodu to může být pro ně výhodná investiční příležitost: menší byty se snadněji pronajímají
* z pohledu zájemců (singles, mladé páry, studenti, dojíždějící pracující; lidi s omezeným rozpočtem atd. ) jde o vhodný způsob bydlení, a to z hlediska ceny a užitnosti bytu.

## Otázka č. 6
#### Existují inzerce bytů, které stojí více než 20 000 Kč? Pokud ano, jsou v této cenové hladině inzerovány i maximálně dvoupokojové byty?

  Ano, existují 3 inzerce bytů, které stojí více než 20 tis Kč,
byty s dispozicí 'pokoje', '1+kk', 1+1', '2+kk', '2+1' jsou uvedeny níže:

        Město	            Ulice	    Dispozice	 Rozměry bytu (m2)	Cena pronájmu (Kč/měsíc)	
    1  Zlín - Louky	  Zadní luhy	      2+kk            62	              21000.0	
    2  Zlín	          Nivy II	          2+1	          120	              20500.0	
    3  Luhačovice     Masarykova	      2+kk	          70	              25000.0	

NOTE: Chyba 120 m2?
__Interpretace:__ _Jedná se byty 2+kk a 2+1, skupin, které dohromady tvoří nejvíce nabídek. Cena pronájmu bytu může být závislá na lokalitě, vybavenosti bytu, dostupnosti veřejné vybavenosti, přístupem k přírodě, bozpečnostní situací dané lokality, stav nemovitosti  atd._

__Poznámka__ _Byt pod bodem 2 (index 1) má rozměr 120 m2. Zde je otázka jde o správný údaj anebo překlep. Původní údaj ponechán._

## Otázka č. 7
#### Zjisti minimální a maximální cenu inzerce pro každou cenu inzerce bytu. Která dispozice má největší rozptyl mezi maximální a minimální cenou inzerovanou cenou? (Zobraz i na grafu)
      Dispozice  Maximální cena  Minimální cena   Rozdíl
    5      3+kk         33000.0         12500.0  20500.0
    3      2+kk         25000.0          9500.0  15500.0
    4       3+1         26000.0         12500.0  13500.0
    2       2+1         20500.0         11000.0   9500.0
    0       1+1         16500.0          9500.0   7000.0
    1      1+kk         14900.0          7900.0   7000.0
    8    pokoje         10500.0          5000.0   5500.0
    6       4+1         20000.0         14885.0   5115.0
    7      4+kk         19000.0         17500.0   1500.0


__Interpretace:__ _Největší rozdíl cen v pronájmech je by bytů 3+kk, nejmenší u bytů s dispozicí 4+kk. Rozdíl v cenách může být způsobena: lokalitou, vybaveností bytu, dostupností veřejné vybavenosti, přístupem k přírodě, bezpečnostní situací dané lokality atd._

