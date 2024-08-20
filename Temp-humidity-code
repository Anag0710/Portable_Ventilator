#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>
#include <DHT.h>
#include <ESP8266WiFi.h>

#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64
#define DHTPIN D7
#define DHTTYPE DHT11

Adafruit_SSD1306 oled(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, -1);
DHT dht(DHTPIN, DHTTYPE);

void setup() {
    Serial.begin(9600);

    if(!oled.begin(SSD1306_SWITCHCAPVCC, 0x3C)) { 
        Serial.println(F("SSD1306 allocation failed"));
        for(;;); // Don't proceed, loop forever
    }
    
    oled.clearDisplay();
    oled.setTextSize(1);
    oled.setTextColor(WHITE);
    oled.setCursor(0, 10);
    oled.println("TEAM");
    oled.println(" ");
    oled.println("THE SAVIOURS");
    oled.display();

    dht.begin();
}

void loop() {
    float humidity = dht.readHumidity();
    float temperature_C = dht.readTemperature();

    if (isnan(humidity) || isnan(temperature_C)) {
        Serial.println(F("Failed to read from DHT sensor!"));
        return;
    }

    // Display on OLED
    oledDisplayCenter("Temp: " + String(temperature_C, 1) + "C");
    delay(3000);
    oledDisplayCenter("Humidity: " + String(humidity, 1) + "%");

    delay(2000); // Wait 2 seconds between readings
}

void oledDisplayCenter(String text) {
    int16_t x1, y1;
    uint16_t width, height;
    oled.getTextBounds(text, 0, 0, &x1, &y1, &width, &height);
    oled.clearDisplay();
    oled.setCursor((SCREEN_WIDTH - width) / 2, (SCREEN_HEIGHT - height) / 2);
    oled.println(text);
    oled.display();
}
