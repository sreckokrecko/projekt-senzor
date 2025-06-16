# projekt-senzor
v šoli moramo narditi diy senzor oz napravo za merjenje
za izdelavo potrebujemo:
2 rgb diodi
arduino uno
6x upor
termistor
css 811 senzor

css 811 senzor
najprej sva postavila senzor za CO2 na protobord in pravilno povezala žičke v arduino
s tem sva imela nekaj težav ,ker nisva vedela kam grejo pini, zato sva pogledala na internet in čez nekaj časa  ugotovula naoako  ter jo popravila
nato sva napisala kodo za ta senzor in ga testirala
senzorja najprej ni zaznal, zato sva naložila program na arduino
sam senzor nima podane absolutne napake 


DHT11
po tem sva zvezala še senzor za temperaturo in vlago
s tem senzorjem sva imela večje težave
v dokumentaciji za senzor so bili pini narobe napisani, zato sva rabila dve šolski uri, da sva ugovotila težavo 
ugotovila sva, ko sva šla iskat pin na youtoube
senzor ima podano absolutno napako ± 2 stopinji celzija in ±5% za vlago 

po rešitvi težav z drugim senzorjem sva šla delat ohišje
zmerila sva mere lcdja in swica, ki bo prišel na pokrov
meritve za škatlo- velikost arduinota
po tem sva zvezala lcd, ki je delal brez težav
nato sva dodala še rgb ledici
nisva imela dovolj pinov na arduionotu, zato sva naročila nov lcd i2c vmesnikom
po tem sva dala 3D printat ohišje
pokrov od ohišja je prišel malo prevelik, zato sva ga zbrusila
nato sva začela vstavljati še ostale komponente v samo ohišje. najprej sva to hotela narediti z perfboardom ampak zaradi stiske s prostorom ni šlo.
zato sva uporabila tehniko s termoskrčkami in dvolepilnim trakom na senzorju ccs pa je bilo potrebno podalšati nogice saj so na ohišju luknjice preveč narazen senzor pa ima premale nogice.
arduino sva v škatlo fixirala z dvolepilnim trakom 
nato sva začela zlagati in vezati komponente v ohišje eno po eno da ni prišlo do zmede, in poskrbela za pregleden " cable management"
na koncu sva napravo testeriala in ugotovila da dela

opis delovanja:
napravo prižgemo z stikalom nato na liqid crystal zaslonu napise zagon sistema po dveh sekundah se senzorja prižgeta in začneta mirit na strneh se tudi prižgejo rgb diode ki 
