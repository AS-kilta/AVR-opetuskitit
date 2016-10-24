# AVR-opetuskitit
Kokoelma Säätökerhon kasaamia AVR-pohjaisia opetuslankkuja.

Idea pohjautuu Konepajalla sijaitseviin kitteihin, joilla on harjoiteltu [peltoroboa](http://autsys.aalto.fi/en/FieldRE) varten.

Esikuvat: [KitA](https://github.com/saatokerho/AVR-opetuskitit/blob/master/photos/KitA.jpg), [KitB_1](https://github.com/saatokerho/AVR-opetuskitit/blob/master/photos/KitB_1.jpg), [KitB_2](https://github.com/saatokerho/AVR-opetuskitit/blob/master/photos/KitB_2.jpg) ja [KitC](https://github.com/saatokerho/AVR-opetuskitit/blob/master/photos/KitC.jpg)

Osat on hankittu pääasiassa [Futurlecilta](http://www.futurlec.com/) ja [Lawicelilta](http://www.lawicel-shop.se/). Futurlecin valikoimista löytyy useita hyviä, valmiiksi kasattuja ja edullisia moduleita.

Opetuskitit koostuvat Host-levystä ja erillisistä plug-and-code -moduleista.

## Nykytila
AVR-kittien tila käytiin läpi Säätöneuvolan inventaarion yhteydessä 15.2.2016. Kaikki osat löytyivät ja paketit vastaavat alkuperäisiä kuvauksia. Muuton yhteydessä kitit siirrettiin AS-mikroluokan lukittuun kaappiin.

## Historia
Alunperin opetuskitit tarkoitettiin Säätökerhon omaan käyttöön, mutta tähtäimessä oli saada AS:lle pakollinen parin opintopisteen mikrokontrollerien perusteet kurssi. Tavoite on saavutettu siinä määrin, että mikrokontrollerit ovat nykyisin yksi moduli Automaatio 1 kurssissa. Kurssin opetuksessa käytetään kuitenkin eri opetuskittejä.

### Alkuperäinen Roadmap
1. Rauta päätetty karkeasti; moduulien koko, muoto ja liittimien paikat, pohjalevyn materiaali, kiinnitystapa jne
2. Mikrokontrollerin piirilevy ja moduulien levyt suunniteltu
3. Ostetaan mikrokontrollerit ja perusosat (napit, ledit, moottorit ym.)
4. Valmistetaan runkomateriaalit (piirilevyt, pohjalevyt jne)
5. Kasataan olemassaolevista osista valmiit osaset (kolvataan levyt, ruuvaillaan pohjiin)
6. Kehitetään ja testaillaan softaa, tässä välissä soodan pitämä avr-opetusluento
7. Hommataan hienommat osat, kuten radiolinkit ja kiihtyvyysanturit, jos niitä ei aikataulussa saatu perusosien kera hankittua
8. Softaa loppuosille
9. Lopulta opetusluento koko hässäkästä

## Raudasta tarkemmin
Yksityiskohtaisempaa tietoa pakettien osista. Yksi kappale moduleja ja päälevy per paketti ellei toisin mainita.
  * [Sälää](#sälää)
  * [Pohja](#pohja)
  * [Päälauta](#päälauta)
  * [Keypad](#keypad)
  * [Valintamoduli](#valintamoduli)
  * [ADC-lauta](#adc-lauta)
  * [Servo](#servo)
  * [Moottori](#moottori)
  * [Etäisyyslauta](#etäisyyslauta)
  * [Heilumislauta](#heilumislauta)
  * [Zigbee](#zigbee)
  * [PC-puolen ZigBee](#pc-puolen-zigbee)

### Sälää
* virtalähde, 12V 2-3 A, 20€
* Y-haaroittimia tms. jakajia virtalähteelle, 5€
* laatikko, esim. etola, 5€
* kaapelia ja liittimiä, ~10e
* käyttöohjeet
* http://www.futurlec.com/ConnPolHead.shtml

Hinta yhteensä ~40e

* Piirilevyä tilataan jälkeenpäin
  * vaikea arvioida hintaa
  * protoillaan ekat koululla
  * ei kulu paljoa

### Pohja
* yksi per moduli, esim. protoshopista
* aluslevy 100x100x3mm akryyli
  * ((1.18 g) / (cm^3)) * ((100 mm) * (100 mm) * (3 mm)) = 35.4 grams
  * ~kympin/kilo
  * ((1.18 g) / (cm^3)) * ((100 mm) * (100 mm) * (3 mm)) * (10 (Euros / kg)) = 0.354 Euros
* laitteen kiinnitykseen 4x 3mm ruuvi, jotain 6mm pitkä
  * protoshop
  * ruuvit halpoja
  * spacerit (korokepalat) tarvittaessa <0,2e/kpl
* 4x sopiva kumitatti (ye:ltä)
* sopiva määrä tappeja (pitkä ruuvi?) yhteen kiinnittämiseksi
  * jotain 0,2e/kpl

Hinta yhteensä ~pari euroa

### Päälauta
* µC: http://www.pjrc.com/store/teensypp_pins.html $27
* (reset-nappi on teensyssä)
* 12V sisään
* 5V regulaattori, TODO
* virtaindikaattoriledi
* dataliittimet
  * Portit: A-F, 6 kpl, 10p
  * I2C: SCL, SDA, GND, +5V
  * SPI: SCLK, MOSI, MISO, SS, GND, +5V -- jospa jätetään tämä ihan omaan perusporttiinsa
  * USART: IN, OUT, GND, +5V -- miten erotellaan I2C:stä? maalataan vaikka
  * ISP, 2x3 piikkirima
  * JTAG: 10p
  * debuggausledit
    * 8x smd-led + etuvastus
    * 8p dip
* LCD: http://www.futurlec.com/LCDDisp.shtml, LCD16X2BL $7,9
  * 4x spacer+ruuvi
  * kaapeli
* LCD-panelin apulevy
  * 4bit tila
  * piirilevyä
  * 4x ruuvi+spacer+ruuvi
  * 10p liitin
  * 10k kontrastitrimmeri
  * bl-etuvastus
* Painikkeet: http://www.futurlec.com/Input_Pushbutton.shtml, $4,5 (kaapeli mukana)
  * liittimiä väyliin
  * 4x POLHDR4
  * 4x POLHDCON4
  * 1x PLHDPIN (paketissa 10 kpl)
* pohja 20x10cm, mukaan napit ja lcd? vai 30x10, ledit+lcd, napit+dipit

Hinta yhteensä ~55€

### Keypad
* http://www.futurlec.com/Mini_Keypad.shtml, $4,9
* 4x spacer+ruuvi
* kaapeli
* pohja

Hinta yhteensä ~5,5€

### Valintamoduli
* adc/pwm-pinnien valintaan, mikä mihinkin outputtiin
* ei erillistä aluslevyä
* piirilevyä
* 4x 10p uros
* 3x 8p dip
* 4x ruuvi+spacer+ruuvi

Hinta yhteensä ~7€

### ADC-lauta
* http://www.futurlec.com/Input_ADC.shtml, $7,9 (kaapeli mukana)
* pohja
* valintamoduli

Hinta yhteensä ~5,5€ + valintamoduli

### Servo
* http://www.futurlec.com/Servo_Motor.shtml, Miniature 60o $9,9
* pohja
* alumiinilevyä tms. kiinnitykseen
* adapteripiirilevy
  * 4x ruuvi+spacer+ruuvi
  * 10p uros
  * 3p uros
* pelkkä servo ja jotain kivaa siihen

Hinta yhteensä ~11€

### Moottori
* enkooderisetti 29,9€
* moottori 10,9€
  * 6V
  * 40mA @ 6V
  * 360mA stall @ 6V
* ohjain 17,6€
* pohja
* alumiinilevyä moottorin kiinnitykseen
* adapterilevy
  * 10p uros
  * ohjausjohdotus mietittävä
  * 4x ruuvi+spacer+ruuvi
  * virransyöttö

Hinta yhteensä ~72€

### Etäisyyslauta
* ir 11,5€
* uä 29,9€
* ir:lle jst-piuha 1,95€
* uä:lle raakaa johtoa
* adapterilevy
  * 10p liitin
  * analogi+i2c-liittimet
  * pari dippiä millä valitaan analogipinni (vaiko hyppylangalla kovakonffattava?)
  * ruuvi+spacer+ruuvi
* alumiinilevyä kiinnittelemiseen
* pohja

Hinta yhteensä ~50€

### Heilumislauta
* Pro-versioon
* IMU 33,2€
* levy
  * tuo tulee kiinni tähän, ei lisäruuveja
  * 10p liitin
  * 9pin + 4pin piikkirimat
  * 3,3v regu
* pohja

Hinta yhteensä ~40€

### ZigBee
* Pro-versioon
* XBee 21,5€
* piirilevyadapteri 7,2€
* pohja
* adapteri? uart... pelkkä liitin, ehkä

Hinta yhteensä ~30€

### PC-puolen ZigBee
* Pro
* XBee 21,5€
* explorer usb 20,1€
* näitä tarttee ehkä yhden vaan

Hinta yhteensä ~40,5€
