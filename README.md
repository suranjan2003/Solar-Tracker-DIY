# Solar-Tracker-DIY
# to run the code we need Arduino IDE and the real/virtual circuit set up

#include <Servo.h>  // Include the Servo library

Servo myservo;  // Create a Servo object to control a servo motor

#define LDR_1 A0  // Define LDR_1 as the analog pin A0
#define LDR_2 A1  // Define LDR_2 as the analog pin A1

int pos = 90;  // Initialize the servo position at 90 degrees (midpoint)
int Resistance = 20;  // Sensitivity threshold to determine when to move the servo

void setup() {
  myservo.attach(4);  // Attach the servo to digital pin 4
  pinMode(LDR_1, INPUT);  // Set LDR_1 as an input
  pinMode(LDR_2, INPUT);  // Set LDR_2 as an input

  myservo.write(pos);  // Set the initial position of the servo to 90 degrees
  delay(1000);  // Wait for 1 second to stabilize the system
}

void loop() {      
  int value_1 = analogRead(LDR_1);  // Read the analog value from LDR_1
  int value_2 = analogRead(LDR_2);  // Read the analog value from LDR_2
      
  if(abs(value_1 - value_2) > Resistance) {  // Check if the difference in light levels exceeds the threshold
    if(value_1 > value_2) {  // If LDR_1 detects more light than LDR_2
      pos = pos + 1;  // Increase the servo position (turn right)
    } else if(value_1 < value_2) {  // If LDR_2 detects more light than LDR_1
      pos = pos - 1;  // Decrease the servo position (turn left)
    }
  }
     
  if(pos > 180) {  // Ensure the servo position does not exceed 180 degrees
    pos = 180;
  } 
  if(pos < 0) {  // Ensure the servo position does not go below 0 degrees
    pos = 0;
  } 

  myservo.write(pos);  // Move the servo to the new position
  delay(50);  // Wait for 50 milliseconds before the next loop iteration
}

}
     
if(pos > 180) {pos = 180;} 
if(pos < 0) {pos = 0;} 
myservo.write(pos); 
delay(50);

}
