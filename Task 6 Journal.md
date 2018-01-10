## Task 6 - servo project 1

1. Control an RC servo
Step 1 requires a servo to be connected to an arduino, with a program that generates a movement with a frequency of 0.2 Hz. The program I used was as follows:

```cpp
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
```
The code steps from 0-180 then 180-0 with the number increasing/decreasing every 13.9 ms. I used 13.9 ms as this will make the servo follow a sine wave of around 0.2 Hz. This was calculated using the following maths: 

Number of steps = 360 
Period = 1/0.2 = 5
5/360 = 0.013888...

2. Control the servo with a potentiometer
Step 2 requires the servo to be controlled using a potentiometer. The code I used for this was as follows:

```cpp
#include <Servo.h> 
 
Servo myservo;

int val;

void setup() 
{ 
  Serial.begin(9600);
  myservo.attach(9); 
} 

void loop() 
{ 
 val = analogRead(A0);
 //Serial.println(val);
 //delay(1000);
 val = (val/5.683);
 myservo.write(val);
} 
```
To scale the value of the potentiometer to a value a servo could use, I divided the collected potentiometer by 5.683. 5.683 was calculated by dividing 1023 (the maximum value of the potentiometer) by 180 (the maximum value of the servo), resulting in 5.68333.... There is also some commented code that was used to read the value of the potentiometer. When the code was active, it was used to collect the following values from the potentiometer: 

![Task 6 step 2](https://github.com/Schenkington/Images/blob/master/task%206%20step%202.png)
