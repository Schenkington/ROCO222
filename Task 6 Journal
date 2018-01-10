## Task 6 - servo project 1

1. Control an RC servo


'''cpp

#include <Servo.h> 
 
Servo myservo;
int pos = 0;
 
void setup() 
{ 
  myservo.attach(9); 
} 
 
 
void loop() 
{ 
  for(pos = 0; pos < 180; pos += 1)
  {
    myservo.write(pos);
    delay(13.9); 
  } 
  for(pos = 180; pos>=1; pos-=1)
  {
    myservo.write(pos);
    delay(13.9);
  } 
} 
'''
