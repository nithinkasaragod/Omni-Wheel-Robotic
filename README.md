/*
  HC05 - Bluetooth AT-Command mode
  Download "Android Control robot car" applicationin your Mobile Phone from PlayStore
*/
#include "SoftwareSerial.h"
#include <AFMotor.h>

AF_DCMotor motor1(1, MOTOR12_64KHZ); // create motor #1, 64KHz pwm
AF_DCMotor motor2(2, MOTOR12_64KHZ); // create motor #2, 64KHz pwm
AF_DCMotor motor3(3, MOTOR12_64KHZ); // create motor #3, 64KHz pwm

SoftwareSerial MyBlue(2, 3); // RX | TX

int state;

void setup()
{
  Serial.begin(9600);
  MyBlue.begin(9600);  //Baud Rate for AT-command Mode.
  motor1.setSpeed(250);
  motor2.setSpeed(250);
  motor3.setSpeed(250);
  motor1.run(RELEASE);
  motor2.run(RELEASE);
  motor3.run(RELEASE);
}
void loop()
{
  if (MyBlue.available() > 0)
  {
    state = MyBlue.read();
    Serial.println(state);
  }
  if (state == 'S')
  {
    motor1.run(RELEASE);
    motor2.run(RELEASE);
    motor3.run(RELEASE);
  }
  if (state == 'F')
  {
    motor1.run(FORWARD);
    motor2.run(BACKWARD);
    motor3.run(RELEASE);
  }
  if (state == 'B')
  {
    motor1.run(BACKWARD);
    motor2.run(FORWARD);
    motor3.run(RELEASE);
  }
  if (state == 'L')
  {
    motor1.run(BACKWARD);
    motor2.run(BACKWARD);
    motor3.run(BACKWARD);
  }
  if (state == 'R')
  {
    motor1.run(FORWARD);
    motor2.run(FORWARD);
    motor3.run(FORWARD);
  }
   if (state == 'S')
  {
    motor1.run(RELEASE);
    motor2.run(RELEASE);
    motor3.run(RELEASE);
  }
}
