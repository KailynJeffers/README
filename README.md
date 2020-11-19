# README Group 8 Robot

Readme file for the code for a robot made for Elementary to Middle grade students to introduce them to the world of engineering.

* This is meant to explain the code used to run the robot project.
* It will also describe the steps to install the proper software needed to code for the robot.

## Installation: 

###### The software needed for this robot is Arduino IDE.

* The software for the Arduino IDE can be found on https://www.arduino.cc/en/software.
* The page offers several download options based on the operating system of the computer.
* Windows 7 or higher, and Mac OS X 10.10 or newer is preferred.

Download the software for the laptop's respective OS.\
Run the software.\
Select "New" to create a new sketch to paste and run the robot's code.\
"Verify" compiles the code for errors.\
"Upload" compiles and runs the code.


## Description of code:

#include <Servo.h>\
Servo myservo;
*************************
The first portion of the code declares the Servo.h library that helps the Arduino board control the servo motor.\
The next line declares the variable for the servo motor.

*************************
*************************

int Trig = A2;\
int Echo = A1;

int ENA = 11;\
int ENB = 5;\
int IN1 = 7;\
int IN2 = 9;\
int IN3 = 6;\
int IN4 = 3;\
#define carSpeed 155\
#define carSpeed2 155\
int rightDistance = 0, leftDistance = 0;
*************************
This portion of the code declares the Trig and Echo pins on the ultrasonic sensor, and it declares the motor pins on the L298N board.\

After the pins are declared, carSpeed and carSpeed2 are defined. carSpeed represents the speed the motors drive forward and backwards, and carSpeed2 represents the motors'turn speed.\

Lastly, rightDistance and leftDistance are declared and set to zero.
*************************
*************************
void setup() {\
  myservo.attach(10);\
  Serial.begin(9600);\
  pinMode(Echo, INPUT);\
  pinMode(Trig, OUTPUT);\
  pinMode(IN1, OUTPUT);\
  pinMode(IN2, OUTPUT);\
  pinMode(IN3, OUTPUT);\
  pinMode(IN4, OUTPUT);\
  pinMode(ENA, OUTPUT);\
  pinMode(ENB, OUTPUT);\
  stop();\
  digitalWrite(ENA, HIGH);\
  digitalWrite(ENB, HIGH);\
}
*************************
The setup() function sets the servo motor to pin 10 on the Arduino, initializes the serial monitor that displays the sensor's commands, and sets each pin to output except for Echo which is an input. Then, the ENA and ENB pins are set to high.
*************************
*************************
void loop() {

  servo.write(60);\
  delay(200);\
  rightDistance = distance_test();

  servo.write(120);\
  delay(200);\
  leftDistance = distance_test();

  if((rightDistance > 70)&&(leftDistance > 70)){\
    stop();\
  }\
  else if((rightDistance >= 20)&&(leftDistance >= 20)){\
    moveForward();\
  }\
  else if((rightDistance <= 10)&&(leftDistance <= 10)){\
    moveBack();\
    delay(100);\
  }\
  else if(rightDistance - 3 > leftDistance){\
    moveLeft();\
    delay(100);\
  }\
  else if(rightDistance + 3 < leftDistance){\
    moveRight();\
    delay(100);\
  }\
  else{\
    stop();\
  }

}

********************************
The loop() function uses the ultrasonic sensor to determine which movement function to run. It relies on the distance from the sensor to the object to determine which function is run.\
The loop() function uses if/else statements.
********************************
********************************
void moveForward(){\
  analogWrite(ENA, carSpeed);\
  analogWrite(ENB, carSpeed);\
  digitalWrite(IN1, HIGH);\
  digitalWrite(IN2, LOW);\
  digitalWrite(IN3, LOW);\
  digitalWrite(IN4, HIGH);\
  Serial.println("Forward");\
}
*******************************
The moveForward() function sets the IN1 and IN4 pins to high and the IN2 and IN3 pins to low. This causes the left and right wheels to both move forward.
*******************************
*******************************
void moveBack(){\
  analogWrite(ENA, carSpeed);\
  analogWrite(ENB, carSpeed);\
  digitalWrite(IN1, LOW);\
  digitalWrite(IN2, HIGH);\
  digitalWrite(IN3, HIGH);\
  digitalWrite(IN4, LOW);\
  Serial.println("Back");\
}
********************************
The moveBack() function sets the 1N2 and IN3 pins to high and the IN1 and IN4 pins to low. This causes the left and right wheels to both move backward.
********************************
********************************
void moveLeft(){\
  analogWrite(ENA, carSpeed2);\
  analogWrite(ENB, carSpeed2);\
  digitalWrite(IN1, LOW);\
  digitalWrite(IN2, HIGH);\
  digitalWrite(IN3, LOW);\
  digitalWrite(IN4, HIGH);\
  Serial.println("Left");\
}
********************************
The moveLeft() function sets the IN2 and IN4 pins to high and the IN1 and IN3 pins to low. This causes the left wheel to move backward and the right wheel to move forward. This makes the car turn left.
********************************
********************************
void moveRight(){\
  analogWrite(ENA, carSpeed2);\
  analogWrite(ENB, carSpeed2);\
  digitalWrite(IN1, HIGH);\
  digitalWrite(IN2, LOW);\
  digitalWrite(IN3, HIGH);\
  digitalWrite(IN4, LOW);\
  Serial.println("Right");\
}
********************************
The moveLeft() function sets the IN1 and IN3 pins to high and the IN2 and IN4 pins to low. This causes the left wheel to move forward and the right wheel to move backward. This makes the car turn right.
********************************
********************************
void stop(){\
  digitalWrite(ENA, LOW);\
  digitalWrite(ENB, LOW);\
  Serial.println("Stop!");\
}
********************************
The stop() function sets the ENA and ENB pins to low, causing the robot to stop.
********************************
********************************
int distance_test(){\
  digitalWrite(Trig, LOW);\
  delayMicroseconds(2);\
  digitalWrite(Trig, HIGH);\
  delayMicroseconds(20);\
  digitalWrite(Trig, LOW);\
  float Fdistance = pulseIn(Echo, HIGH);\
  Fdistance = Fdistance / 58;\
  return (int)Fdistance;\
}
*******************************
The distance_test() function uses the ultrasonic sensor to determine the location of an object in respect to the sensor.
