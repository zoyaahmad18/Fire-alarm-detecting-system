#include <LiquidCrystal.h>
LiquidCrystal lcd(7, 6, 5, 4, 3, 2);

int redLed = 10;
int greenLed = 12;
int buzzer = 8;
int smokepin = A0;

int sensorThres = 150;

void setup() {
  pinMode(redLed, OUTPUT);
  pinMode(buzzer, OUTPUT);
  pinMode(smokepin, INPUT);
  Serial.begin(9600);
  lcd.begin(16,2);
}

void loop() {
  int analogSensor = analogRead(smokepin);

  lcd.print("Smoke Level:");
  lcd.print(analogSensor-50);
  // Checks if it has reached the threshold value
  if (analogSensor-50 > sensorThres)
  {
    digitalWrite(redLed, HIGH);
    lcd.setCursor(0, 2);
    lcd.print("Alert!");
    digitalWrite(12, LOW);
    digitalWrite(buzzer, HIGH);
  }
  else
  {
    digitalWrite(redLed, LOW);
    digitalWrite(12, HIGH);
    lcd.setCursor(0, 2);
    lcd.print("Safe");
    digitalWrite(buzzer, LOW);
    
  }
  delay(500);
  lcd.clear();
}
