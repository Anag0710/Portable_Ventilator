#include <Wire.h>
#include "MAX30100_PulseOximeter.h"
#include <ESP8266WiFi.h>
#include "Adafruit_GFX.h"
#include "OakOLED.h"

#define REPORTING_PERIOD_MS 1000
#define NUM_READINGS 10

OakOLED oled;

PulseOximeter pox;
float BPMReadings[NUM_READINGS];
float SpO2Readings[NUM_READINGS];
int readIndex = 0;
uint32_t tsLastReport = 0;

const unsigned char bitmap [] PROGMEM = {
    0x00, 0x00, 0x00, 0x00, 0x01, 0x80, 0x18, 0x00, 0x0f, 0xe0, 0x7f, 0x00, 0x3f, 0xf9, 0xff, 0xc0,
    0x7f, 0xf9, 0xff, 0xc0, 0x7f, 0xff, 0xff, 0xe0, 0x7f, 0xff, 0xff, 0xe0, 0xff, 0xff, 0xff, 0xf0,
    0xff, 0xf7, 0xff, 0xf0, 0xff, 0xe7, 0xff, 0xf0, 0xff, 0xe7, 0xff, 0xf0, 0x7f, 0xdb, 0xff, 0xe0,
    0x7f, 0x9b, 0xff, 0xe0, 0x00, 0x3b, 0xc0, 0x00, 0x3f, 0xf9, 0x9f, 0xc0, 0x3f, 0xfd, 0xbf, 0xc0,
    0x1f, 0xfd, 0xbf, 0x80, 0x0f, 0xfd, 0x7f, 0x00, 0x07, 0xfe, 0x7e, 0x00, 0x03, 0xfe, 0xfc, 0x00,
    0x01, 0xff, 0xf8, 0x00, 0x00, 0xff, 0xf0, 0x00, 0x00, 0x7f, 0xe0, 0x00, 0x00, 0x3f, 0xc0, 0x00,
    0x00, 0x0f, 0x00, 0x00, 0x00, 0x06, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00
};

void onBeatDetected() {
    Serial.println("Beat Detected!");
    oled.drawBitmap(60, 20, bitmap, 28, 28, 1);
    oled.display();
}

void setup() {
    Serial.begin(115200);
    oled.begin();
    oled.clearDisplay();
    oled.setTextSize(1);
    oled.setTextColor(1);
    oled.setCursor(0, 0);

    oled.println("Initializing pulse oximeter..");
    oled.display();
    
    pinMode(16, OUTPUT);

    Serial.print("Initializing Pulse Oximeter..");

    if (!pox.begin()) {
        Serial.println("FAILED");
        oled.clearDisplay();
        oled.setTextSize(1);
        oled.setTextColor(1);
        oled.setCursor(0, 0);
        oled.println("FAILED");
        oled.display();
        for(;;);
    } else {
        oled.clearDisplay();
        oled.setTextSize(1);
        oled.setTextColor(1);
        oled.setCursor(0, 0);
        oled.println("SUCCESS");
        oled.display();
        Serial.println("SUCCESS");
        pox.setOnBeatDetectedCallback(onBeatDetected);

        // Adjust the IR LED current for reduced range
        pox.setIRLedCurrent(MAX30100_LED_CURR_7_6MA); // Set to a low current value
    }

    // Initialize the arrays
    for (int i = 0; i < NUM_READINGS; i++) {
        BPMReadings[i] = 0;
        SpO2Readings[i] = 0;
    }
}

void loop() {
    pox.update();

    // Add the new reading to the arrays
    BPMReadings[readIndex] = pox.getHeartRate();
    SpO2Readings[readIndex] = pox.getSpO2();
    readIndex = (readIndex + 1) % NUM_READINGS;

    // Calculate the average
    float avgBPM = 0;
    float avgSpO2 = 0;
    for (int i = 0; i < NUM_READINGS; i++) {
        avgBPM += BPMReadings[i];
        avgSpO2 += SpO2Readings[i];
    }
    avgBPM /= NUM_READINGS;
    avgSpO2 /= NUM_READINGS;

    if (millis() - tsLastReport > REPORTING_PERIOD_MS) {
        Serial.print("Heart rate:");
        Serial.print(avgBPM);
        Serial.print(" SpO2:");
        Serial.print(avgSpO2);
        Serial.println(" %");

        oled.clearDisplay();
        oled.setTextSize(1);
        oled.setTextColor(1);
        oled.setCursor(0, 0);
        oled.println("Heart BPM");
        oled.setCursor(0, 16);
        oled.println(avgBPM);
        oled.setCursor(0, 30);
        oled.println("SpO2");
        oled.setCursor(0, 45);
        oled.println(avgSpO2);
        oled.display();

        tsLastReport = millis();
    }
}
