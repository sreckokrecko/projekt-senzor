Projekt: Senzor V šoli smo dobili nalogo izdelati DIY senzor

Potrebni materiali: 2x RGB diodi

Arduino Uno

6x upor

Termistor

Senzor CCS811 (merjenje CO₂)

Senzor DHT11 (merjenje temperature in vlage)

CCS811 – senzor za CO₂ Najprej sva na protoboardu postavila senzor CCS811 in ga povezala z Arduinom. Pri povezovanju sva imela nekaj težav, saj nisva točno vedela, kam priključiti posamezne pine. Po nekaj iskanja po spletu sva ugotovila napako in jo popravila.

Nato sva napisala kodo za senzor in ga testirala. Na začetku senzor ni bil zaznan, zato sva še enkrat naložila program na Arduino. Po tem je deloval pravilno. Senzor sicer nima podane absolutne napake.

DHT11 – senzor za temperaturo in vlago Zatem sva priključila še senzor DHT11. Z njim sva imela več težav kot s prvim. V dokumentaciji so bili pini napačno označeni, zato sva potrebovala kar dve šolski uri, da sva ugotovila napako – pomagalo nama je iskanje pravilnega priklopa na YouTubu.

Ta senzor ima podano absolutno napako:

Temperatura: ±2 °C

Vlaga: ±5 %

Izdelava ohišja Ko sva rešila vse težave s senzorji, sva začela načrtovati ohišje. Najprej sva izmerila dimenzije LCD-ja in stikala, ki bosta nameščena na pokrov. Ohišje sva prilagodila velikosti Arduina.

LCD zaslon sva priključila brez težav. Nato sva dodala še RGB LED diodi. Ker na Arduinu ni bilo dovolj prostih pinov, sva naročila nov LCD z I2C vmesnikom.

Ko je bilo 3D natisnjeno ohišje pripravljeno, sva ugotovila, da je pokrov malenkost prevelik, zato sva ga pobrusila. Nato sva začela vstavljati preostale komponente. Sprva sva želela uporabiti perfboard, a zaradi prostorske omejitve to ni bilo možno.

Namesto tega sva uporabila termoskrčljive cevi in dvostranski lepilni trak. Pri senzorju CCS811 sva morala podaljšati nogice, ker so bile luknje v ohišju preveč narazen, nogice senzorja pa prekratke.

Arduino sva v škatlo pritrdila z dvostranskim trakom. Nato sva postopoma vgrajevala in povezovala vse komponente, da ne bi prišlo do zmede. Poskrbela sva tudi za urejeno razporeditev kablov ("cable management").

Na koncu sva napravo testirala in ugotovila, da deluje pravilno.

Opis delovanja naprave

Napravo vključimo s priklopom napetosti. Na LCD zaslonu se najprej prikaže napis: "Zagon sistema". Po približno dveh sekundah se aktivirata senzorja (DHT11 in CCS811) ter začneta z meritvami.

Na zaslonu se prikazujejo naslednji podatki:

Temperatura

Vlaga

Vsebnost CO₂ v zraku

Na straneh ohišja svetijo RGB diode, katerih barva prikazuje stanje meritve:

DHT11 (temperatura): Zelena: normalna sobna temperatura

Rdeča: previsoka temperatura

Modra: prenizka temperatura

CCS811 (CO₂): Zelena: normalna koncentracija CO₂

Oranžna: povišana (a še varna) vrednost

Rdeča: nevarno visoka vrednost CO₂

napravo izklopimo ko prekinemo napetost

komentar:
senzor nama je dal kar par izzivov ampak z malo pomoči sva jim bila kos, pri tej projektni nalogi sva dobila malo občutka koliko truda in enih živcev je potrebno da tako naprava začne delovati tako kot je treba 
naju je pa projekt naučil tudi kako efektivno delati s tistim kar imaš na voljo
sam senzor naju je presenetil saj sva mislila da bojo napake večje 
zelo sva zadovoljna in ponosna z izdelkom ki ga bova predstavila saj oba veva da je zanj šlo ogromno truda, razmišljanja, skrbi in potrpljenja
