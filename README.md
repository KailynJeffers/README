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
int Echo = A1;\

int ENA = 11;\
int ENB = 5;\
int IN1 = 7;\
int IN2 = 9;\
int IN3 = 6;\
int IN4 = 3;\
#define carSpeed 155\
#define carSpeed2 155\
int rightDistance = 0, leftDistance = 0;\
*************************
