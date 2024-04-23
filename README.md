#include <SoftwareSerial.h>

#define SENSOR_PIN A0
#define PUMP_PIN 13

SoftwareSerial bluetooth(2, 3); // RX, TX

void setup() {
  pinMode(SENSOR_PIN, INPUT);
  pinMode(PUMP_PIN, OUTPUT);
  
  Serial.begin(9600);
  bluetooth.begin(9600);
}

void loop() {
  int waterLevel = analogRead(SENSOR_PIN);
  
  if (waterLevel < 500) { // Cambia este umbral según tu sensor y necesidades
    digitalWrite(PUMP_PIN, HIGH); // Enciende la bomba de agua
  } else {
    digitalWrite(PUMP_PIN, LOW); // Apaga la bomba de agua
  }
  
  // Envía el nivel de agua por Bluetooth
  bluetooth.print("Nivel de agua: ");
  bluetooth.println(waterLevel);
  
  delay(1000); // Espera un segundo antes de la próxima lectura
}
