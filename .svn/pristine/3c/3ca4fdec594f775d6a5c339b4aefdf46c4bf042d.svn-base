#include <gfxfont.h>
#include <Adafruit_GFX.h>
#include <Adafruit_BMP085.h>
#include <Adafruit_Sensor.h>
#include <Adafruit_SSD1306.h>

#include <DHT.h>
#include <SPI.h>
#include <Wire.h>

#define DHTPIN 4
DHT dht(DHTPIN, 11);
Adafruit_SSD1306 display(4);

void setup() { 
  Serial.begin(9600);
  dht.begin();
}

void loop() {
  double temperature, humidity, dew_point;
  temperature = dht.readTemperature();
  humidity = dht.readHumidity();
  dew_point = temperature - (80 - humidity) / 5;

  Serial.print("Humidity: ");
  Serial.print(humidity);
  Serial.print(", temperature: ");
  Serial.print(temperature);
  Serial.print(", heat index: ");
  Serial.println(dht.computeHeatIndex(dht.readTemperature(), dht.readHumidity(), false));

  //display start
  display.begin(SSD1306_SWITCHCAPVCC, 0x3C);

  display.setTextSize(2);
  display.setTextColor(WHITE);
  display.setCursor(0,0);
  display.clearDisplay();
  
  display.print("Temp:  ");
  display.println(temperature, 0);

  display.setTextSize(1);
  display.print("%humidity:    ");
  display.println(humidity, 0);

  //display.print("Dew:          ");
  //display.println(dew_point, 0);

  display.print("#index:  ");
  if (dew_point > 11) display.print("oo");
  if (dew_point > 13) display.print("oo");
  if (dew_point > 19) display.print("oo");
  if (dew_point > 25) display.print("oo");
  
  display.display();
  delay(5000);
}