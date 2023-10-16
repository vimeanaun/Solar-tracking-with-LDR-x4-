# Solar-tracking-with-LDR-x4-
https://youtu.be/Qa-48_J2lQI

// blue line
#include <Servo.h>

int LT =0;
int LB =0;
int RT =0;
int RB =0;

Servo servo1;
Servo servo2;
int position1 =90;
int position2 =90;

void setup(){
Serial.begin(9600);
servo1.attach(9);
servo2.attach(10);
}

void loop(){

servo1.write(position1); //turning left and right 
servo2.write(position2); // turning up and down
delay(1000);

int sumLT = 0;
int sumLB = 0;
int sumRT = 0;
int sumRB = 0;

for ( int i=0; i<=200; i++)
{
  sumLT += analogRead(A0);
  sumLB += analogRead(A1);
  sumRT += analogRead(A2);
  sumRB += analogRead(A3);
}
LT = sumLT/200;
LB = sumLB/200;
//Serial.println ("lb"+String('LB'));
RT = sumRT/200;
RB = sumRB/200;
int result2 = (LT+LB)-(RT+RB); // left and right.
int result1 = (LT+RT)-(RB+LB); // up and down.
delay(100);

if (abs(result1) > 5)
{
  if (result1 > 0)
  {
    if (position1 >180)
    {
    position1 -=3;
    servo1.write(position1 -=3);
    }
    else 
    {
    position1 -=3;
    servo1.write(position1 -=3);
    }
  }
  else if (result1 <0)
  {
    {
      if (position1 <0)
    {
    position1 +=3;
    servo1.write(position1 +=3);
    }
    else{
    position1 +=3;
    servo1.write(position1 +=3); 
    }
  }
  delay(1000);
  }
}
 if (abs(result2) > 5)
{
  if (result2 > 0)
  {
    if (position2 <0)
    {
    position2 +=3;
    servo2.write(position2 +=3);
    }
    else {
    position2 +=3;
    servo2.write(position2 +=3);
    }
  }
  else if ( result2 <0 )
    {
      if (position2 >180)
    position2 -=3;
    servo2.write(position2 -=3);
    }
    else {
    position2 -=3;
    servo2.write(position2 -=3);
    }
  delay(1000);
}
Serial.print("result1:"+String(result1));
Serial.println("position1:"+String(position1));
Serial.print("result2:"+String(result2));
Serial.println("position2:"+String(position2));
}
