# Smart-Chair
#include <LiquidCrystal.h> //Please replace the single quote characters ('') with the parenthesis character (<>)


LiquidCrystal lcd(1, 2, 4, 5, 6, 7); // Creates an LCD object. Parameters: (rs, enable, d4, d5, d6, d7)

const int trigPin = 3;
const int echoPin = 8;
long duration;
int distanceCm, distanceInch;
unsigned long newtime;
unsigned long Time;
extern volatile unsigned long timer0_millis;


void setup() {
  
lcd.begin(16,2); // Initializes the interface to the LCD screen, and specifies the dimensions (width and height) of the display
pinMode(trigPin, OUTPUT);
pinMode(echoPin, INPUT);

}

void loop() {
  
digitalWrite(trigPin, LOW);
delayMicroseconds(2);
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);

duration = pulseIn(echoPin, HIGH);
distanceCm= duration*0.034/2;
distanceInch = duration*0.0133/2;

 Time = millis();
  newtime = Time/1000;

lcd.setCursor(0,0); // Sets the location at which subsequent text written to the LCD will be displayed
lcd.print("Distance: "); // Prints string "Distance" on the LCD
lcd.print(distanceCm); // Prints the distance value from the sensor
lcd.print("  cm");
delay(10);

if (distanceCm>=10 && distanceCm<=15)
  {
    Serial.println ("samay is");
    Serial.println(newtime);
    lcd.setCursor (0,1);
    lcd.print ("Count: ");
    lcd.print (newtime);
    delay (1000);
    
    }

    else {
      noInterrupts ();
      timer0_millis = 0;
      interrupts ();
      lcd.setCursor(6,1);
      lcd.print("     ");
      
      }



}
