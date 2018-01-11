# Roco222 Lab Book
## 25/09/17
### Practical 1: Software engineering for roboticists
1. Write your first markdown document

Here are the the basic syntax rules of markdown:
* Hash is used to denote a heading, with additional hashes being used for further sub-headings
```markdown
# Heading
``` 
* Bold is represented using either double asterisk or underscore either side of what you want bold
```markdown
**Bold**
```
* Italics is represented using either an asterisk or an underscore either side of what you want to have in italic
```markdown
_Italics_
```
* Paragraphs are separated by a blank line
```markdown

Paragraph
```
* Two spaces at the end of a line leaves a line break
```markdown
Line break  
```
* Three dashes create a horizontal rule
```markdown
--- 
```
* Asterisks are used to create a bullet list
```markdown
* Bullet point
```
* Numbers and a period creates a numbered list
```markdown
1. Numbered list
```
* Putting text in square brackets creates a link, with the url of the link in brackets afterwords
```markdown
[http://example.com](http://example.com)
```

2. Command-Line 101

* ls - list directory contents
* cd /tmp - changes directory to a tempory directory
* cd $HOME - changes directory to the home directory, the $ represents the user account 
* mkdir - used to make directories
* echo "Hello" > hello.md - outputs the text "Hello" and saves it to a .md file
* cat hello.md - outputs the text in the .md file
* cp hello.md hello-again.md - copies the contents of hello.md into a new file
* mv hello-again.md hello-hello.md - renames file
* rm hello.md - removes the file 
* rm -rf - force deletes everything (doesn't work in practice)
* cat /proc/cpuinfo - displays the specs of the cpu

4. Your first git repository

ls -al - displays all data on the files and folders in the selected directory, it shows things such as the number of bits and the creation date and time of each file and folder.

6. Version tracking

So far i've learnt that git uses repositories to store data. These repositories allow tracking of the various versions of added data through the use of commit messages. Repositories can be stored locally or online.

## 02/10/17
### Practical 2: Build a DC motor

1. Build a commutator

The commutator is used to power the motor coils. We had no issues with construction at this time.

2. Add a support shaft

The inserted nails support the motor and allow it to rotate. We had no issues with construction at this time. 

3. Wind the armature coil

The coil cuts the magnetic field which causes motion when a current is flowing. We had a small amount trouble whilst winding (tangling etc.), but nothing too major. We ended up with 120 turns in our coil.

4. Build the shaft support and magnet brackets
5. Build the baseplate

These components are use to hold the commutator and coil whilst it spins. We had some issues when attaching the supports to the baseplate, but we managed to solve this problem by using extra washers.

## 09/10/17

1. Finish the motor
2. Test the motor

Initially we had some issues as we hadn't correctly turned on the power supply, once this was corrected the motor turned successfully. From our tests we found a few issues with the design that we should be able to fix with future iterations. These issues are as follows:
* Crumpled commutator - Through the building process the commutator became damaged, this caused some issues whilst the motor was in motion.
* Single wire brushes - We used stripped single core wire as the motor brushes, and used our hands to support them. These two factors caused a very unreliable connection.
* Loose motor supports - The paper clip motor supports allowed for quite a lot a shifting when the motor was turning.

3. A better DC motor

We began the design for our next DC motor at the end of the session, we will use what we learnt from our previous attempt to ensure a more reliable system. 

## 16/10/17

This is the DC motor we built: 

![Better motor](https://github.com/Schenkington/Images/blob/master/Better%20motor.JPG)

Motor specs:
* Number of coils: 2
* Turns per coil: 60
* Coil resistance (per coil): ~2 ohms

The motor is made from 2 coils which each are soldered to 2 quartered copper compression olives on each end, which act as the motors commutator. The core of the armature is made from a number of washers glued together, with cork halves on either end. The motor brushes are made from half spheres of solder that sit atop a spring system that allows the brushes to adjust to the shape of the commutator while still keeping in contact. 

This motor does not work. It has been tested and we know that power runs through the coils whilst its in motion. Due to this, we narrowed down the problem to 2 factors: 
1. The magnetic field may be too weak (2 of the neodymium magnets broke so the motor only has 2 in it)
2. There is too much friction in the system for it to turn using its own power

## 23/10/17
### Practical 3: Incremental Encoder
1. Circuit diagram
2. Build the IR LED light source
3. Build the light detector

The circuit we built looks like this:
![Encoder](https://github.com/Schenkington/Images/blob/master/Encoder.JPG)

This ciruit was built by soldering the components into a piece of stripboard, based on the circuit diagram found in step 1. Jumper cables were used for the +5V, GND and Sense Voltage connections. Two 500 ohm resistors in series were used instead of a 1k, as I didn't have a 1k resistor. 
The circuit was tested by first looking at the IR LED using a the camera on a mobile phone, the dim purple light output by the led showed us that it turned on when the circuit was powered. The phototransistor was tested by connecting the sense voltage cable to an analogue port in the arduino. The output was viewed on the serial console, which changed when the IR LED was covered. 

4. Place an encoder disc on the motor
Our motor with disc: 
![Encoder disk](https://github.com/Schenkington/Images/blob/master/Encoder%20disc.JPG)

The disc was attached to the motor using a small screw, which will keep it more secure compared to suggested method of using blue tack. 
When held in front of the encoders IR LED and allowed to spin, the disc successfully blocks all the light except when the gap spins to the appropriate position.

## 30/10/17

5. Calculate the angular velocity of your motor (using arduino)

This step requires you to edit a previous piece of code in order to count the pulses of light that occur in a second.

```cpp
const byte ledPin = 13;
const byte interruptPin = 2;
volatile byte state = LOW;
int count = 0;

void setup() {
  Serial.begin(9600);
  pinMode(ledPin, OUTPUT);
  pinMode(interruptPin, INPUT);
  attachInterrupt(digitalPinToInterrupt(interruptPin), countfunc, RISING);
}

void loop() {
  delay(1000)
  pulsecount();
}

void countfunc() {
  count += 1;
}

void pulsecount(){
  Serial.println("Pulse count:");
  Serial.println(count); 
  count = 0; 
  delay(1000);
}
```

In the new code the interrupt instead adds 1 to a variable every time its activated. Every second the program outputs this count to the serial console and then resets the count variable. 
Using this program I estimate the motor I used to have a angular velocity of ~20 rads/s

## 06/11/17
### Practical 4: Controlling the motor
1. Install the motor shield
2. Control a small hobby DC motor

The arduino motor shield was installed onto the arduino motor shield by carefully all the pins of the shield into the ports of the arduino. The following code was used to run a motor using channel A:

```cpp
/*************************************************************
Motor Shield 1-Channel DC Motor
by Randy Sarafan
For more information see:
https://www.instructables.com/id/Arduino-Motor-Shield-Tutorial/
*************************************************************/
void setup() {
  //Setup Channel A
  pinMode(12, OUTPUT); //Initiates Motor Channel A pin
  pinMode(9, OUTPUT); //Initiates Brake Channel A pin
}
void loop(){
  //forward @ full speed
  digitalWrite(12, HIGH); //Establishes forward direction of Channel A
  digitalWrite(9, LOW);
  //Disengage the Brake for Channel A
  analogWrite(3, 255);
  //Spins the motor on Channel A at full speed
  delay(3000);
  digitalWrite(9, HIGH); //Engage the Brake for Channel A
  delay(1000);
  //backward @ half speed
  digitalWrite(12, LOW); //Establishes backward direction of Channel A
  digitalWrite(9, LOW);
  //Disengage the Brake for Channel A
  analogWrite(3, 123);
  //Spins the motor on Channel A at half speed
  delay(3000);
  digitalWrite(9, HIGH); //Eengage the Brake for Channel A
  delay(1000);
}
```
To change a motors direction when using channel A, you change the value of pin 12, with HIGH being forward, and LOW being backward. To change the speed of the motor on channel A, you write an analogue value of 0-255 to pin 3, with 255 being the maximum speed and 0 being the minimum (off).

3. Get your DC motor to rotate 
4. Close the loop

This is the program I wrote to adjust the speed of the motor based on the values collected from the encoder 

```cpp 
const byte ledPin = 13;
const byte interruptPin = 2;
volatile byte state = LOW;
int count = 0;
int val = 255;
int RPM = 150;
int pulses;

void setup() {
  pinMode(12, OUTPUT);
  pinMode(9, OUTPUT);
  pinMode(ledPin, OUTPUT);
  pinMode(interruptPin, INPUT);
  attachInterrupt(digitalPinToInterrupt(interruptPin), countfunc, RISING);
}

void loop() {
  digitalWrite(12, HIGH);
  digitalWrite(9, LOW);
  analogWrite(3, val);
  delay(1000);
  pulsecount();
}

void countfunc() {
  count += 1;
}

void pulsecount(){
  pulses = RPM/60;
  if (pulses > count){
    val += 1;
  }
  else if (pulses < count){
    val -= 1;
  }
  else if (val >= 255){
    val = 255;
  }
  count = 0; 
}
```

The program works by comparing the number of counted pulses to the set number of desired pulses. If the number of pulses is greater, the value that denotes speed is reduced by one, if lesser it is increased by one. An example RPM of 150 is used in this program.

## 13/11/17
### Practical 5: Stepper motors

1. Wiring
2. Initial direction
3. Programming of modes

* Full-step mode

```cpp
boolean Adir = HIGH;
boolean Bdir = HIGH;

void setup() {
  pinMode(12, OUTPUT); 
  pinMode(13, OUTPUT);
}

void loop(){
  digitalWrite(12, HIGH);
  Aspeed();
  digitalWrite(13, HIGH);
  Bspeed();
  digitalWrite(12, LOW);
  Aspeed();
  digitalWrite(13, LOW);
  Bspeed();
}

void Aspeed(){
  analogWrite(3, 255);
  delay(1);
  analogWrite(3, 0);
}

void Bspeed(){
  analogWrite(11, 255);
  delay(1);
  analogWrite(11, 0);
}
```

* Half-step mode 

```cpp
boolean Adir = HIGH;
boolean Bdir = HIGH;

void setup() {
  pinMode(12, OUTPUT); 
  pinMode(13, OUTPUT);
}

void loop(){
  digitalWrite(12, HIGH);
  digitalWrite(13, HIGH);
  activate();
  digitalWrite(12, LOW);
  digitalWrite(13, LOW);
  activate();
}


void activate(){
  analogWrite(3, 255);
  analogWrite(11, 255);
  delay(1);
  analogWrite(11, 0);
  analogWrite(3, 0);
}
```

## 20/11/17
### Task 6 - servo project 1

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

3. A robot arm mock-up

This step requires a test robot arm to be constructed using cardboard and 2 servo motors. The arm I created looks like this:

![Mock arm](https://github.com/Schenkington/Images/blob/master/Mock%20arm.JPG)

We were meant to use this arm to estimate the torque of the servo motor, but I had some issues keeping the mass stable on mine, so I used a lolly stick with cm marks:

![Torque Measure](https://github.com/Schenkington/Images/blob/master/Torque%20measure.JPG)

Using this method the motor would stall when a 65g weight was ~4cm away from the point of turn, this would mean the motor has the following torque:

65g = 0.065 kgf
T = 4*0.065 
T = 0.26 kgfcm

This is much less than the 1.6 kgfcm that is stated to be the stall torque by the servos datasheet.

This step also required that the mock arm to have 2 servos, each controlled by a potentiometer. The code I wrote for this is as follows:

```cpp
#include <Servo.h> 
 
Servo servo1;
Servo servo2;

int pot1;
int pot2;

void setup() 
{ 
  servo1.attach(9);
  servo2.attach(10); 
} 

void loop() 
{ 
 pot1 = analogRead(A0);
 pot2 = analogRead(A1);
 pot1 = (pot1/5.683);
 pot2 = (pot2/5.683);
 servo1.write(pot1);
 servo2.write(pot2);
} 
```
## 27/11/17-11/12/17
### Task 7 - servo project 2

The following arm was designed using CAD:

![CAD arm](https://github.com/Schenkington/Images/blob/master/CAD%20arm.png)

Using an add-on to solidworks the assembly was converted into a urdf file. I attempted to incorporate this into rviz, but was unable to solve a number of errors:

![Failure](https://github.com/Schenkington/Images/blob/master/failure.png)
