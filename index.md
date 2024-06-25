Gesture controlled robot
Imagine commanding a robot with just a wave of your hand—no buttons, no remotes, just pure intuitive control. This robot turns your gestures into an extraordinary interactive experience.

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Mohamed S | The Urban Assembly for Law and Justice | Mechancial Engineering | Incoming Senior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For my third and final milestone, I connected the accelerometer to the Arduino micro allowing for the controller to detect gestures. My biggest challenge was the coding aspect due to my lack of experience; my greatest triumph was honestly finishing the main project a couple of days before demo night despite having a couple of challenges. The key topics I learned were the importance of learning how to communicate with an audience as well as learning more about different types of engineering. I hope that I learn what it takes to create something truly innovative in the future. 


# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/tHdXrODQ0GA" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

For my second milestone, I got both Bluetooth to connect. I had to ensure a stable connection and follow the correct wiring layouts for the Micro and Uno Bluetooth. What has been surprising is building this car showed me how powerful coding is. Before this program, I always viewed coding as something that's only associated with software, however, now I know that coding makes machines move. This process was smooth and there weren't any obstacles I faced. My next step is to get the accelerometer to work which would be the final step for building the gesture-controlled robot

# First Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to YouTube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/HGaoFZ29CbI?si=uWr7Lsl0iQ7C_Clm" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>



  For my first milestone, I'm working on getting the motors working. This project is a robotic car controlled by hand gestures. This project involves integrating DC motors, an H-Bridge for motor direction control, an Arduino Uno R3 for signal processing, and a Bluetooth module for wireless communication with a controller. So far, I've successfully set up the Arduino and H-Bridge, and I've made progress in programming basic motor functions. However, my main challenge was coding because I had no prior experience. Moving forward, my plan is to focus on getting the Bluetooth module operational to establish communication between the controller and the robot. 


# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```cpp
#include <SoftwareSerial.h>

#define tx 8
#define rx 9

SoftwareSerial configBt(rx, tx);
long tm, t, d; // variables to record time in seconds

const int Aclockwise = 12;
const int AcounterClock = 13;
const int Bclockwise = 6;
const int BcounterClock = 7;

const int Cclockwise = 4;
const int CcounterClock = 5;
const int Dclockwise = 2;
const int DcounterClock = 3;

void setup() {
  Serial.begin(38400);
  configBt.begin(38400);
  pinMode(tx, OUTPUT);
  pinMode(rx, INPUT);

  pinMode(Aclockwise, OUTPUT);
  pinMode(AcounterClock, OUTPUT);
  pinMode(Bclockwise, OUTPUT);
  pinMode(BcounterClock, OUTPUT);
  pinMode(Cclockwise, OUTPUT);
  pinMode(CcounterClock, OUTPUT);
  pinMode(Dclockwise, OUTPUT);
  pinMode(DcounterClock, OUTPUT);
}

char c; // declare c as a global variable

void loop()
{
  //checks for Bluetooth data
  if (configBt.available()){
    //if available stores to command character
    c = (char)configBt.read();
    //prints to serial
    Serial.println(c);
  }

  //acts based on character
  switch(c){
    //forward case
    case 'F':
      moveForward();
      break;
     
    //left case
    case 'L':
      turnLeft();
      break;
     
    //right case
    case 'R':
      turnRight();
      break;
     
    //back case
    case 'B':
      moveBackward();
      break;
     
    //default is to stop robot
    case 'S':
      freeze();
      break;
  }
}

void moveForward() {
  // Move forward by setting motors appropriately
  digitalWrite(Aclockwise, HIGH);
  digitalWrite(AcounterClock, LOW);
  digitalWrite(Bclockwise, HIGH);
  digitalWrite(BcounterClock, LOW);
  digitalWrite(Cclockwise, LOW);
  digitalWrite(CcounterClock, HIGH);
  digitalWrite(Dclockwise, LOW);
  digitalWrite(DcounterClock, HIGH);
}

void moveBackward() {
  // Move backward by reversing motor directions
  digitalWrite(Aclockwise, LOW);
  digitalWrite(AcounterClock, HIGH);
  digitalWrite(Bclockwise, LOW);
  digitalWrite(BcounterClock, HIGH);
  digitalWrite(Cclockwise, HIGH);
  digitalWrite(CcounterClock, LOW);
  digitalWrite(Dclockwise, HIGH);
  digitalWrite(DcounterClock, LOW);
}

void turnLeft() {
  // Turn left by adjusting motor directions
  digitalWrite(Aclockwise, LOW);
  digitalWrite(AcounterClock, HIGH);
  digitalWrite(Bclockwise, LOW);
  digitalWrite(BcounterClock, HIGH);
  digitalWrite(Cclockwise, LOW);
  digitalWrite(CcounterClock, HIGH);
  digitalWrite(Dclockwise, LOW);
  digitalWrite(DcounterClock, HIGH);
}

void turnRight() {
  // Turn right by adjusting motor directions
  digitalWrite(Aclockwise, HIGH);
  digitalWrite(AcounterClock, LOW);
  digitalWrite(Bclockwise, HIGH);
  digitalWrite(BcounterClock, LOW);
  digitalWrite(Cclockwise, HIGH);
  digitalWrite(CcounterClock, LOW);
  digitalWrite(Dclockwise, HIGH);
  digitalWrite(DcounterClock, LOW);
}

void freeze() {
  // Stationary
  digitalWrite(Aclockwise, LOW);
  digitalWrite(AcounterClock, LOW);
  digitalWrite(Bclockwise, LOW);
  digitalWrite(BcounterClock, LOW);
  digitalWrite(Cclockwise, LOW);
  digitalWrite(CcounterClock, LOW);
  digitalWrite(Dclockwise, LOW);
  digitalWrite(DcounterClock, LOW);
}

#include <Wire.h>

#define MPU6050_ADDRESS 0x68

int16_t accelerometerX, accelerometerY, accelerometerZ;

void setup()
{
  Wire.begin();
  Serial1.begin(38400);

  // Initialize MPU6050
  Wire.beginTransmission(MPU6050_ADDRESS);
  Wire.write(0x6B);  // PWR_MGMT_1 register
  Wire.write(0);     // set to zero (wakes up the MPU6050)
  Wire.endTransmission(true);

  delay(100); // Delay to allow MPU6050 to stabilize
}

void loop()
{
  readAccelerometerData();
  determineGesture();
  delay(500);
}

void readAccelerometerData()
{
  Wire.beginTransmission(MPU6050_ADDRESS);
  Wire.write(0x3B);  // starting with register 0x3B (ACCEL_XOUT_H)
  Wire.endTransmission(false);
  Wire.requestFrom(MPU6050_ADDRESS, 6, true);  // request a total of 6 registers

  // read accelerometer data
  accelerometerX = Wire.read() << 8 | Wire.read();
  accelerometerY = Wire.read() << 8 | Wire.read();
  accelerometerZ = Wire.read() << 8 | Wire.read();
}

void determineGesture()
{
  if (accelerometerY >= 6500) {
    Serial1.write('F');
    Serial.println('F');
  }
  else if (accelerometerY <= -4000) {
    Serial1.write('B');
    Serial.println('B');
  }
  else if (accelerometerX <= -3250) {
    Serial1.write('L');
    Serial.println('L');
  }
  else if (accelerometerX >= 3250) {
    Serial1.write('R');
    Serial.println('R');
  }
  else {
    Serial1.write('S');
    Serial.println('S');
  }
}
```
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
