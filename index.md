# Phone Controlled Robotic Arm
Replace this text with a brief description (2-3 sentences) of your project. This description should draw the reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Atlas M | Head-Royce School (HRS) | Mechanical Engineering | Incoming Freshman


![Headstone Image](unnamed.jpg)

  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**



For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

**My second Milestone was successfully attaching the wheels to my arm along with getting the app working on the phone. I also completed wiring, and coding the robot so I can now controll the wheels and the arm through the PS2 controller. I can now connect with the HC-06 through the android phone and send inputs through the phone, which will move the arm accordingly. I also attached the current arm onto a previous rover that I worked on which had wheels. One surprising thing about the project, was how well the base for the arm fit in with the base for the rover. Some of the challenges I faced include that the main arm only had one corresponding screw hole to screw into the rover, meaning that it would move around. I overcame this challenge by taking 2 shoelaces and tying them around the front to create stability. Another challenge that I faced was that the arm was too high to grab things down below, I fixed this by swapping the standoffs between the arduino, and the arm. This rose another challenge though, as the arduino got in the way, as the arm was rotating. I also solved this by using a pocket knife to carve into the frame of the arm and allow it to rotate through the arduino itself. Another challenge I faced was that the right wheel was not working properly. I easily fixed this, by adjusting my code, and choosing different ports in the sensor sheild, since ports 0 and 1 were not working. Before my final Milestone, I plan on making the controller remote. Since the controller is attached to the arduino board with wiring. I plan on doing this by using a PS2 wireless adapter onto the arduino.**

<iframe allowfullscreen width='852' height='480' scrolling='no' frameborder='0' style='border: none;' src='https://www.wevideo.com/embed/#3130678975' allowfullscreen></iframe>



# First Milestone

**My first milestone was getting my arm built and functioning along with the PS2 controller attached to it. After I got all 4 servos working, I went on to finish the arm itself. A servo works similarly to a motor, but it can only move a certain degree. Meaning that servos work perfectly for things like steering a RC car, or a robotic arm. The arm moves by taking the X and Y inputs of each joystick from the PS2 controler. The signals are then sent to the arduino to move the servos corespondingly. One major challenge that I faced was getting the angle right for the each servo on the arm. Since each servo is set at 90 degrees by default, I need to put on the parts at the right angle for the arm to have full range of motion. For example, if the servo is set at 60 degrees, the actual arm part that goes on the servo needs to be at the same degree as the servo. Otherwise, the joint in the arm will not function properly. The next step for me is to get the app working on the phone, and to add wheels, and a battery pack to the arm.**

<iframe allowfullscreen width='852' height='480' scrolling='no' frameborder='0' style='border: none;' src='https://www.wevideo.com/embed/#3128006909' allowfullscreen></iframe>

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code

**Starter code to get the arm moving with the PS2 controller input**

```c++
#include <Servo.h>
Servo myservo1;  // create servo object to control a servo
Servo myservo2;
Servo myservo3;
Servo myservo4;
int pos1=90, pos2=90, pos3=90, pos4=90; 

void setup()
{
  myservo1.attach(3);    // set the control pin of servo 1 to 3 digital I/0
  myservo2.attach(5);    // set the control pin of servo 1 to 3 digital I/0
  myservo3.attach(6);    // set the control pin of servo 1 to 3 digital I/0
  myservo4.attach(9);    // set the control pin of servo 1 to 3 digital I/0
  
  myservo1.write(pos1);
  myservo2.write(pos2);
  myservo3.write(pos3);
  myservo4.write(pos4);
  delay(1500);
}

void loop() 
{

  // close the claw 
  for(pos4;pos4>45;pos4--)
  {
    myservo4.write(pos4);
  }
  delay(1000);
  
 // open the claw
 for(pos4;pos4<120;pos4++)
 {
   myservo4.write(pos4);
 }
  delay(1000);

// turn right
  for(pos1;pos1>30;pos1--)
  {
    myservo1.write(pos1);
    delay(5);      // delay 5ms（used to adjust the servo speed）
  }
  delay(1000);

   // turn to left 
  for(pos1;pos1<150;pos1++)
  {
    myservo1.write(pos1);
    delay(5);
  }
  delay(1000);

  //  stretch out the arm
  for(pos2;pos2<130;pos2++)
  {
    myservo2.write(pos2);
    delay(5);
  }
  delay(1000);\

  // retracte the arm
  for(pos2;pos2>80;pos2--)
  {
    myservo2.write(pos2);
    delay(5);
  }
  delay(1000);

  // raise the arm 
  for(pos3;pos3<100;pos3++)
  {
    myservo3.write(pos3);
    delay(5);
  }
  delay(1500);

 // Lower the arm 
  for(pos3;pos3>40;pos3--)
  {
    myservo3.write(pos3);
    delay(5);
  }
  delay(1000);

}
```

**Modified code for non-remote controlled arm with the wheels**

```c++
#include <Servo.h> // add the servo libraries
Servo myservo1; // create servo object to control a servo
Servo myservo2;
Servo myservo3;
Servo myservo4;
int pos1=90, pos2=90, pos3=90, pos4=90; // define the variable of 4 servo angle,and assign the initial value (that is the boot posture
//angle value)
const int right_X = A2; // define the right X pin to A2
const int right_Y = A5; // define the right Y pin to A5
const int right_key = 7; // define the right key pin to 7（that is the value of Z）
const int left_X = A3; // define the left X pin to A3
const int left_Y = A4; // define the left X pin to A4
const int left_key = 8; //define the left key pin to 8（that is the value of Z）
const int in1 = 12; // define the in1 pin from the motor driver
const int in2 = 13; // define the in2 pin from the motor driver
const int in3 = 10; // define the in3 pin from the motor driver
const int in4 = 11; // define the in4 pin from the motor driver
const int enA = 2;
const int enB = 4;
int x1,y1,z1; // define the variable, used to save the joystick value it read.
int x2,y2,z2;


void setup()
{
// boot posture
myservo1.write(pos1);
delay(1000);
myservo2.write(pos2);
myservo3.write(pos3);
myservo4.write(pos4);
delay(1500);
pinMode(right_key, INPUT_PULLUP); // set the right/left key to INPUT_PULLUP
pinMode(left_key, INPUT_PULLUP);
pinMode(in1, OUTPUT); // set all Input keys in the motor driver to OUTPUT
pinMode(in2, OUTPUT);
pinMode(in3, OUTPUT);
pinMode(in4, OUTPUT);
pinMode(enA, OUTPUT);
pinMode(enB, OUTPUT);
Serial.begin(9600); // set the baud rate to 9600
}
void loop()
{
myservo1.attach(3); // set the control pin of servo 1 to D3  dizuo-servo1-3
myservo2.attach(5); // set the control pin of servo 2 to D5  arm-servo2-5
myservo3.attach(6); //set the control pin of servo 3 to D6   lower arm-servo-6
myservo4.attach(9); // set the control pin of servo 4 to D9  claw-servo-9
x2 = analogRead(right_X); //read the right X value
y2 = analogRead(right_Y); // read the right Y value
z2 = digitalRead(right_key); //// read the right Z value
x1 = analogRead(left_X); //read the left X value
y1 = analogRead(left_Y); //read the left Y value
z1 = digitalRead(left_key); // read the left Z value
//delay(5); // lower the speed overall

// claw
claw();

// rotate
turn();

// upper arm
upper_arm();

//lower arm
lower_arm();

//right wheel forward
if (z2==0) // if right joystick pushed down
{
right_wheel();
}
else
{
stop_right();
}

//left wheel forward
if (z1==0) // if left joystick pushed down
{
left_wheel();
}
else
{
stop_left();
}

}



//***************************************************
//claw
void claw()
{
//claw
if(x1<50) // if push the left joystick to the right
{
pos4=pos4+3; 
myservo4.write(pos4); //servo 4 operates the motion, the claw gradually opens. 
delay(5);

if(pos4>120) //limit the largest angle when open the claw 
{
pos4=120;
}
}

if(x1>1000) ////if push the right joystick to the left 
{
pos4=pos4-3; 
myservo4.write(pos4); // servo 4 operates the action, claw is gradually closed.
delay(5);
if(pos4<45) // 
{
pos4=45; //limit the largest angle when close the claw
}

}
}



//******************************************************/
// turn
void turn()
{
if(x2<50) //if push the right joystick to the let 
{
pos1=pos1+3; 
myservo1.write(pos1); // arm turns left
delay(5);
if(pos1>180) //limit the angle when turn right 
{
pos1=180;
}

}

if(x2>1000) // if push the right joystick to the right
{
pos1=pos1-3; 
myservo1.write(pos1); //servo 1 operates the motion, the arm turns right. 
delay(5);
if(pos1<1) // limit the angle when turn left
{
pos1=1;
}
}
}




//**********************************************************/
// lower arm
void lower_arm()
{
if(y2>1000) // if push the right joystick downward
{
pos2=pos2-2;
myservo2.write(pos2); // lower arm will draw back
delay(5);
if(pos2<25) // limit the retracted angle
{
pos2=25;
}
}

if(y2<50) // if push the right joystick upward
{
pos2=pos2+2;
myservo2.write(pos2); // lower arm will stretch out
delay(5);
if(pos2>180) // limit the stretched angle
{
pos2=180;
}
}
}





//*************************************************************/

//upper arm
void upper_arm()
{
if(y1<50) // if push the left joystick downward
{
pos3=pos3-2;
myservo3.write(pos3); // upper arm will go down
delay(5);
if(pos3<1) //  limit the angle when go down 
{
pos3=1;
}
}
if(y1>1000) // if push the left joystick upward
{
pos3=pos3+2;
myservo3.write(pos3); // the upper arm will lift
delay(5);

if(pos3>135) //limit the lifting angle 
{
pos3=135;
}
}
}

//right wheel forward
void right_wheel()
{
digitalWrite(in1, HIGH);
digitalWrite(in2, LOW);
analogWrite(enA, 200);
}

//left wheel forward
void left_wheel()
{
digitalWrite(in3, HIGH);
digitalWrite(in4, LOW);
analogWrite(enB, 200);
}

//stop the right wheel from turning
void stop_right()
{
digitalWrite(in1, LOW);
digitalWrite(in2, LOW);
}

//stop the left wheel from turning
void stop_left()
{
digitalWrite(in3, LOW);
digitalWrite(in4, LOW);
}
```



# Bill of Materials

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| LAFVIN phone controlled robot arm kit | Used for building the arm itself | $35.99 | <a href="[https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/](https://www.amazon.com/LAFVIN-Acrylic-Mechanical-Compatible-Tutorial/dp/B07ZYZVNY4)"> Link </a> |
| SunFounder 3 in 1 Starter Kit for Arduino Uno | Used to build the rover part of the arm | $69.99 | <a href="[https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/](https://www.sunfounder.com/products/sunfounder-3-in-1-iot-smart-car-learning-ultimate-starter-kit)"> Link </a> |

# Scematics 

![Headstone Image](scematic_old.png)
