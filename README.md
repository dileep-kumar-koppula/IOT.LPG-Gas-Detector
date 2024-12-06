# LPG Gas Detector with Buzzer and LCD Display

This project uses a **LPG Gas Sensor** to detect the presence of LPG gas. If gas is detected, a **buzzer** sounds an alert and the **LCD display** shows a message indicating a gas leakage.

## Code

```cpp
#include <LiquidCrystal.h>

// LCD and sensor pin definitions
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
#define lpg_sensor 7
#define buzzer 13

void setup() 
{
  // Set pin modes
  pinMode(lpg_sensor, INPUT);
  pinMode(buzzer, OUTPUT);

  // Initialize LCD
  lcd.begin(16, 2);
  lcd.print("LPG Gas Detector");
  lcd.setCursor(0, 1);
  lcd.print("Techno Review 85");
  delay(2000); // Display the intro message for 2 seconds
}

void loop() 
{
  // Read LPG sensor status
  if(digitalRead(lpg_sensor))
  {
    // No gas detected, turn off the buzzer
    digitalWrite(buzzer, LOW);
    
    // Display "No LPG Gas Leakage" on the LCD
    lcd.clear();
    lcd.print("   NO LPG GAS   ");
    lcd.setCursor(0, 1);
    lcd.print("    LEAKAGE     ");
    delay(400); // Wait for 400 milliseconds
    digitalWrite(buzzer, LOW); // Ensure the buzzer is off
    delay(500); // Wait for 500 milliseconds before the next check
  }
  else 
  {
    // LPG gas detected, turn on the buzzer and display alert
    digitalWrite(buzzer, HIGH);
    
    // Display "LPG Gas Leakage Alert" on the LCD
    lcd.clear();
    lcd.print(" LPG Gas Leakage ");
    lcd.setCursor(0, 1);
    lcd.print("     Alert     ");
    delay(1000); // Wait for 1 second before the next check
  }
}
