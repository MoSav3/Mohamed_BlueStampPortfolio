Gesture controlled robot
Imagine commanding a robot with just a wave of your hand—no buttons, no remotes, just pure intuitive control. This robot turns your gestures into an extraordinary interactive experience.


| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Mohamed S | The Urban Assembly for Law and Justice | Mechancial Engineering | Incoming Senior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**


  
# Final Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/v_w25taoswc" frameborder="0" allowfullscreen></iframe>

For my third and final milestone, I connected the accelerometer to the Arduino micro allowing for the controller to detect gestures. My biggest challenge was the coding aspect due to my lack of experience; my greatest triumph was honestly finishing the main project a couple of days before demo night despite having a couple of challenges. The key topics I learned were the importance of learning how to communicate with an audience as well as learning more about different types of engineering. I hope that I learn what it takes to create something truly innovative in the future. 


# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/tHdXrODQ0GA" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

For my second milestone, I got both Bluetooth to connect. I had to ensure a stable connection and follow the correct wiring layouts for the Micro and Uno Bluetooth. What has been surprising is building this car showed me how powerful coding is. Before this program, I always viewed coding as something that's only associated with software, however, now I know that coding makes machines move. This process was smooth and there weren't any obstacles I faced. My next step is to get the accelerometer to work which would be the final step for building the gesture-controlled robot

# First Milestone

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
| Car Chassis | Used for building a car robot | $21 | <a href="https://www.amazon.com/perseids-Chassis-Encoder-Wheels-Battery/dp/B07DNXBFQN/ref=sr_1_8?crid=26VIPBXQSRZVY&dib=eyJ2IjoiMSJ9.7sBydE6izOdKBo7i4BbNazTCnIXk6jbvhXxhVXfTpGNPHl-7i8IWAkzF1yTQH8GwPWm9nDQ1Kjw09y-DlcSWpKQ1APYegZUhsIlQ4rBqvFjlLvER1kxvQg8yoC3IN6v94FzZNnlw6uSxpzKY-y5FcC2Jreu6V7Eb5QoP4EZN8Ix0BERFJYKVTyQWni7YHv70g1oX8U1HicDvqGPeG-PrgSnKLv9tiDrA4hbxMyjvrQBWUe3VtChjFyxtZYsZ1DMIjziERvkg23YIDlKkKa1oGC7koX4mWBk8zJGMg8ijnYU.o1nap2RMrn2q4GBkrjbbkn4TA1kjWqtZEIdzoOxPP7g&dib_tag=se&keywords=car%2Bchassis&qid=1719623332&sprefix=car%2Bchas%2Caps%2C131&sr=8-8&th=1">Link</a> |
| Breadboard | For building electronic circuits | $9 | <a href="https://www.amazon.com/Breadboards-Solderless-Breadboard-Distribution-Connecting/dp/B07DL13RZH/ref=sr_1_5?crid=2EDD94AMO7VBD&dib=eyJ2IjoiMSJ9.LQIZ685myU7rU29tXH-XxQjRwKgAf980dm6TNDrxtuFH3FpuD6KaRLjoXPQIpR1358QUEy5hXlg5wDWPmb69BKxOSGXpOSg3W8GenR__BQrTya-8g3zXMvb8dYtR8lPP1cZOl1snSWOJJUbuCLPKOMSQ-v5tza3blhSH8Ja-Ato3phGY65WAffDv-FF7Bg5Au5yGdLKdWVBI0nnJx-A9Us4tPE0FBzgDHd_JT2GLRRo.cwU787mWVaYnx2NvRJfRWAQaiI5JTYXZ1xmQE7LdN-s&dib_tag=se&keywords=rexqualis+breadboard&qid=1719623398&sprefix=rexqualis%2Caps%2C97&sr=8-5">Link</a> |
| Arduino Uno | Controls the motor driver and collects sensor data | $17 | <a href="https://www.amazon.com/ELEGOO-Board-ATmega328P-ATMEGA16U2-Compliant/dp/B01EWOE0UU/ref=sr_1_1_sspa?crid=1NUTBU8A5CZSL&dib=eyJ2IjoiMSJ9.mMwW9AQ5cM5IcBhuz3WQYbuZBocbivwOzYdf5nIppRX1DLx4YepwiC0DGd58SxJlYtaJNim490vrxGgWKcnxzCKC_zyYC6AfPz804_hfWeJr7ooyVmZa_bDWgbCV7QZ10kFg6W8u4r621fwc2wSWNL4Izrfj8IJGDxikhfynZM82MsuzKEv3ibCs8LvonTAqMTSMjsIeS9JRridvaTA2hgvMndrbjbwpuGRpTIHNYBg.qnvY9ap37Uy3a1voTKf7alWelectronics">Link</a> |
| L9110S Motor Driver | For controlling motors | $9 | <a href="https://www.amazon.com/Treedix-2-5-12V-Stepper-H-Bridge-Stepping/dp/B089M5VHJT/ref=sr_1_17?crid=2U4RHQ4DTWFEG&dib=eyJ2IjoiMSJ9.bzhBjwP5JaVoGGo7c4Jo2a4NMg8bHXPnf45PV79JFatL5HHJNDcgFvq8AGspDF_h4KZVp0UnwPF3N0aBkOenIV1KduGtu2weFZ8s8gRlMAI8d468VgGshB7wFa72vIrHMkuAbLqVWcvSrNLIIUpV8EzGgWDE1OwqlVH4-JLZ0u3jfNx3wn3DHdQHKg00fBIe1426mFZqOCkbPEIJ26KLXlhRs_ZAG1TzjdcsA3F_B523DYB46MKM977hQhZtgWYO25w6nJw1b93XPhW-QzLwpAeqIsLul0roJRqhGQuq3cQ.PxtJmYH4rimN1s8kUbJfmHj8_GyOfSaU9bg_XXUgwE0&dib_tag=se&keywords=l9110s&qid=1719623762&s=electronics&sprefix=l9110s%2Celectronics%2C63&sr=1-17">Link</a> |
| Two HC-05 Bluetooth Modules | For wireless communication | $20 | <a href="https://www.amazon.com/DSD-TECH-HC-05-Pass-through-Communication/dp/B01G9KSAF6?psc=1&pd_rd_w=fkqrF&content-id=amzn1.sym.3c1bdb31-a20d-42d0-a8cf-ddadf63cd1a8&pf_rd_p=3c1bdb31-a20d-42d0-a8cf-ddadf63cd1a8&pf_rd_r=TDRDTRATHZSAQXYAWMYZ&pd_rd_wg=G4guZ&pd_rd_r=8bfedcef-937c-4a60-9c4e-cf42fbd79f64&ref_=sspa_dk_detail_img_1">Link</a> |
| MPU6050 Accelerometer | For measuring acceleration and orientation | $10 | <a href="https://www.amazon.com/Pre-Soldered-Accelerometer-Raspberry-Compatible-Arduino/dp/B0BMY15TC4/ref=sr_1_4?crid=27HK9MBNU2N2Q&dib=eyJ2IjoiMSJ9.nQ-HfKOFyZoszrV3cxLK6stPzn4eOISYIBYbmDYSRsXHRFLJIqIGbMOfDezTc3MrItEYIew2Uptr8QCIbZTJZBs4dKEBoT4YlTz80GUeV3X6XmWdwztFGyPSYx6ueoxx9zSH0i3Vlf5ejQVCSNjIf-VHspGZlpfVL20Iq1VkyxckHrSc0IdETvhQCe7zJYPmO6CwI2pe2UZYIQgEnFnZcCSkXqy3sUn9GYWEpjqKmSo.hrjCE6qelVSLo80TYyr3R24pIivuugTLbREchbMeZfo&dib_tag=se&keywords=mpu6050+accelerometer&qid=1719624079&sprefix=mpu6050+ac%2Caps%2C113&sr=8-4">Link</a> |
| Arduino Micro | Interprets gestures for robot control. | $22 | <a href="https://www.amazon.com/Arduino-Micro-Headers-A000053-Controller/dp/B00AFY2S56/ref=sr_1_3?crid=32PS86PQ286YJ&dib=eyJ2IjoiMSJ9.2fcKbc9rMUlyNF9BcEXPXm2hOtngsejs3Dhkj5zwQhNLW3xtQWRAKaaFQ-Oh6YcJvdK721z9zcE8zzkJnU-n2qHzoMMtVj7Bt6sDh7ZWdP-sEQNCNjjuNauzrtSxPou1VjW-nI_z
p9rRvqp7VGmkt1RdZyE0NWgRHiBHkdcgHaKQ8vYEo43LrlxyN72qR_h15Gd5bbsq6X4t_4Px1_T3bT0MI431JFL7rovjEHdJLiM.2JOBjncBzT7Rf11hOm99pbF4uaKnJydvkeL4gOQ3B9A&dib_tag=se&keywords=arduino+micro&qid=1719624113&sprefix=arduino+micro+%2Caps%2C106&sr=8-3">Link</a> |
| Small Screwdriver Set | For assembling the chassis | $7 | <a href="https://www.amazon.com/Small-Screwdriver-Set-Mini-Magnetic/dp/B08RYXKJW9/ref=sr_1_1?crid=36J7PXI9EKSR2&dib=eyJ2IjoiMSJ9.jssna5mXZtMkI4LOhCdOZgYkl3g4_UElXWT05P7CVEXGjHj071QN20LucGBJIEps.KdhjO980u6tgO2rMAT7PKWvFM0pvEu-xT6j7gFeK73E&dib_tag=se&keywords=tkiszyzr+32+in+1&qid=1719624212&s=electronics&sprefix=tkiszyzr+32+in+1%2Celectronics%2C77&sr=1-1">Link</a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
