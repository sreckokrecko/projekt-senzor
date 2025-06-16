#include <DHT.h>
#include <Adafruit_CCS811.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

// ----- DHT11 -----
#define DHTPIN 2
#define DHTTYPE DHT11
DHT dht(DHTPIN, DHTTYPE);

// ----- CCS811 -----
Adafruit_CCS811 ccs;

// RGB LED 1 – temperatura
const int r1 = 9;
const int g1 = 10;
const int b1 = 11;

// RGB LED 2 – kakovost zraka
const int r2 = 5;
const int g2 = 6;
const int b2 = 3;

// LCD
LiquidCrystal_I2C lcd(0x27, 16, 2);

// Časovni števec
unsigned long prejsnjiDHTcas = 0;
unsigned long intervalDHT = 1000;
unsigned long prejsnjiCasBarve = 0;
unsigned long intervalBarve = 50;
unsigned long prejsnjiCasLCD = 0;
unsigned long intervalLCD = 1000;

float temp = 0.0, hum = 0.0;
uint16_t co2 = 0, tvoc = 0;

float trenutniRedT = 0, trenutniGreenT = 0, trenutniBlueT = 0;
float ciljniRedT = 0, ciljniGreenT = 0, ciljniBlueT = 0;

float trenutniRedA = 0, trenutniGreenA = 0, trenutniBlueA = 0;
float ciljniRedA = 0, ciljniGreenA = 0, ciljniBlueA = 0;

const float hitrostPrehoda = 0.1;

void setup() {
  Serial.begin(9600);
  dht.begin();

  pinMode(r1, OUTPUT); pinMode(g1, OUTPUT); pinMode(b1, OUTPUT);
  pinMode(r2, OUTPUT); pinMode(g2, OUTPUT); pinMode(b2, OUTPUT);

  if (!ccs.begin()) {
    Serial.println("Napaka: CCS811 senzor ni zaznan!");
    while (1);
  }

  lcd.init();
  lcd.backlight();
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Zagon sistema...");
  delay(1000);
  lcd.clear();
}

void loop() {
  unsigned long zdaj = millis();

  if (zdaj - prejsnjiDHTcas >= intervalDHT) {
    prejsnjiDHTcas = zdaj;
    float t = dht.readTemperature();
    float h = dht.readHumidity();

    if (!isnan(t)) temp = t;
    if (!isnan(h)) hum = h;

    izracunajCiljneBarveTemp();
  }

  if (ccs.available()) {
    if (!ccs.readData()) {
      co2 = ccs.geteCO2();
      tvoc = ccs.getTVOC();
      izracunajCiljneBarveCO2();
    }
  }

  if (zdaj - prejsnjiCasBarve >= intervalBarve) {
    prejsnjiCasBarve = zdaj;

    trenutniRedT = lerp(trenutniRedT, ciljniRedT, hitrostPrehoda);
    trenutniGreenT = lerp(trenutniGreenT, ciljniGreenT, hitrostPrehoda);
    trenutniBlueT = lerp(trenutniBlueT, ciljniBlueT, hitrostPrehoda);

    trenutniRedA = lerp(trenutniRedA, ciljniRedA, hitrostPrehoda);
    trenutniGreenA = lerp(trenutniGreenA, ciljniGreenA, hitrostPrehoda);
    trenutniBlueA = lerp(trenutniBlueA, ciljniBlueA, hitrostPrehoda);

    analogWrite(r1, int(trenutniRedT));
    analogWrite(g1, int(trenutniGreenT));
    analogWrite(b1, int(trenutniBlueT));

    analogWrite(r2, int(trenutniRedA));
    analogWrite(g2, int(trenutniGreenA));
    analogWrite(b2, int(trenutniBlueA));
  }

  if (zdaj - prejsnjiCasLCD >= intervalLCD) {
    prejsnjiCasLCD = zdaj;

    // Vrstica 0: T:24.3C H:56%
    lcd.setCursor(0, 0);
    char vrstica0[17];
    char tempStr[6];
    dtostrf(temp, 4, 1, tempStr);  // 4 mesta, 1 decimalka
    snprintf(vrstica0, sizeof(vrstica0), "T:%sC H:%2d%%", tempStr, (int)hum);
    lcd.print(vrstica0);

    // Vrstica 1: C: 400 T: 45
    lcd.setCursor(0, 1);
    char vrstica1[17];
    snprintf(vrstica1, sizeof(vrstica1), "C:%4d T:%4d", co2, tvoc);
    lcd.print(vrstica1);
  }

  Serial.println("-----------");
  Serial.print("Temperatura: ");
  Serial.print(temp);
  Serial.println(" °C");

  Serial.print("Vlaga: ");
  Serial.print(hum);
  Serial.println(" %");

  Serial.print("eCO2: ");
  Serial.print(co2);
  Serial.println(" ppm");

  Serial.print("TVOC: ");
  Serial.print(tvoc);
  Serial.println(" ppb");

  delay(10);
}

float lerp(float trenutna, float ciljna, float alpha) {
  return trenutna + alpha * (ciljna - trenutna);
}

void izracunajCiljneBarveTemp() {
  ciljniRedT = ciljniGreenT = ciljniBlueT = 0;

  if (temp < 20) {
    float ratio = constrain((20 - temp) / 10.0, 0.0, 1.0);
    ciljniBlueT = 255 * ratio;
  }
  else if (temp >= 20 && temp <= 22) {
    ciljniGreenT = 255;
  }
  else if (temp > 22 && temp < 24) {
    float ratio = (temp - 22) / 2.0;
    ciljniRedT = 255 * ratio;
    ciljniGreenT = 255;
  }
  else if (temp >= 24 && temp <= 27) {
    ciljniRedT = 255;
    ciljniGreenT = 255;
  }
  else if (temp > 27 && temp <= 35) {
    float ratio = (temp - 27) / 8.0;
    ciljniRedT = 255;
    ciljniGreenT = 255 * (1.0 - ratio);
  }
  else if (temp > 35) {
    ciljniRedT = 255;
  }
}

void izracunajCiljneBarveCO2() {
  ciljniRedA = ciljniGreenA = ciljniBlueA = 0;

  if (co2 <= 800) {
    float ratio = co2 / 800.0;
    ciljniRedA = 255 * ratio;
    ciljniGreenA = 255 - (155 * ratio);
  }
  else if (co2 > 800 && co2 <= 1200) {
    float ratio = (co2 - 800) / 400.0;
    ciljniRedA = 255;
    ciljniGreenA = 100 * (1 - ratio);
  }
  else {
    ciljniRedA = 255;
  }
}
