# KeyTechnology and potential technical issues

### 1 CapacitiveSensor

- Capacitive sensors that can detect touch or proximity.
The capacitiveSensor library turns two or more Arduino pins into a capacitive sensor, which can sense the electrical capacitance of the human body. All the sensor setup requires is a medium to high value resistor and a piece of wire and a small (to large) piece of aluminum foil on the end. At its most sensitive, the sensor will start to sense a hand or body inches away from the sensor.

- How it works

<div align= 'center'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/原理.png?raw=true" width = "500" />
</div><br></br>

The capacitiveSensor method toggles a microcontroller send pin to a new state and then waits for the receive pin to change to the same state as the send pin. A variable is incremented inside a while loop to time the receive pin's state change. The method then reports the variable's value, which is in arbitrary units.

- Library Methods
The library contains three main methods and some utility methods:

> CapacitiveSensor CapacitiveSensor(byte sendPin, byte receivePin)

CapacitiveSensor creates an instance of the library (please note the capital letters, this is not the same method as below)

> long capacitiveSensorRaw(byte samples)

capacitiveSensorRaw requires one parameter, samples, and returns a long integer containing the absolute capacitance, in arbitrary units. The samples parameter can be used to increase the returned resolution, at the expense of slower performance. The returned value is not averaged over the number of samples, and the total value is reported.

capacitiveSensorRaw will return -2 if the capacitance value exceeds the value of CS_Timeout_Millis (in milliseconds). The default value for CS_Timeout_Millis 2000 milliseconds (2 seconds).

> long capacitiveSensor(byte samples)

capacitiveSensor requires one parameter, samples, and returns a long containing the added (sensed) capacitance, in arbitrary units. capacitiveSensor keeps track of the lowest baseline (unsensed) capacitance, and subtracts that from the sensed capacitance, so it should report a low value in the unsensed condition.

The baseline is value is re-calibrated at intervals determined by CS_Autocal_Millis. The default value is 200000 milliseconds (20 seconds). This re-calibration may be turned off by setting CS_Autocal_Millis to a high value with the set_CS_AutocaL_Millis() method.


> void set_CS_Timeout_Millis(unsigned long timeout_millis);

The set_CS_Timeout_Millis method may be used to set the CS_Timeout_Millis value, which determines how long the method will take to timeout, if the receive (sense) pin fails to toggle in the same direction as the send pin. A timeout is necessary because a while loop will lock-up a sketch unless a timeout is provided. CS_Timeout_Millis' default value is 2000 milliseconds (2 seconds).

> void reset_CS_AutoCal()

reset_CS_AutoCal may be used to force an immediate calibration of capacitiveSensor function.

> void set_CS_AutocaL_Millis(unsigned long autoCal_millis)

The method set_CS_AutocaL_Millis(unsigned long autoCal_millis) may be used to set the timeout interval of the capacitiveSensor function. Re-calibration may be turned off by using set_CS_AutocaL_Millis to set CS_AutocaL_Millis to "0xFFFFFFFF".

- Demo Sketch

```cpp
#include <CapacitiveSensor.h>

CapacitiveSensor   cs_4_2 = CapacitiveSensor(4,2);        // 10 megohm resistor between pins 4 & 2, pin 2 is sensor pin, add wire, foil
CapacitiveSensor   cs_4_5 = CapacitiveSensor(4,5);        // 10 megohm resistor between pins 4 & 6, pin 6 is sensor pin, add wire, foil
CapacitiveSensor   cs_4_8 = CapacitiveSensor(4,8);        // 10 megohm resistor between pins 4 & 8, pin 8 is sensor pin, add wire, foil

void setup()                    
{

   cs_4_2.set_CS_AutocaL_Millis(0xFFFFFFFF);     // turn off autocalibrate on channel 1 - just as an example
   Serial.begin(9600);

}

void loop()                    
{
    long start = millis();
    long total1 =  cs_4_2.capacitiveSensor(30);
    long total2 =  cs_4_5.capacitiveSensor(30);
    long total3 =  cs_4_8.capacitiveSensor(30);

    Serial.print(millis() - start);        // check on performance in milliseconds
    Serial.print("\t");                    // tab character for debug window spacing

    Serial.print(total1);                  // print sensor output 1
    Serial.print("\t");
    Serial.print(total2);                  // print sensor output 2
    Serial.print("\t");
    Serial.println(total3);                // print sensor output 3

    delay(10);                             // arbitrary delay to limit data to serial port 
}
```

### 2 DFPlayer Mini SCM

- Introduction
DFPlayer Mini is an MP3 module that can be connected directly to a speaker. The module can be used as a module of Arduino UNO with the power supply battery, speaker, and buttons separately.

- Exterior Pictures
<div align= 'center'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/dfplayer.png?raw=true" width = "500" />
</div><br></br>

- IO Pin
<div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/io.png?raw=true" width = "800" />
</div><br></br>

- Connect wire
<div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/连线.png?raw=true" width = "800" />
</div><br></br>

- Demo sketch

```cpp
#include "Arduino.h"
#include "SoftwareSerial.h"
#include "DFRobotDFPlayerMini.h"

SoftwareSerial mySoftwareSerial(10, 11); // RX, TX
DFRobotDFPlayerMini myDFPlayer;
void printDetail(uint8_t type, int value);

void setup()
{
  mySoftwareSerial.begin(9600);
  Serial.begin(115200);
  
  Serial.println();
  Serial.println(F("DFRobot DFPlayer Mini Demo"));
  Serial.println(F("Initializing DFPlayer ... (May take 3~5 seconds)"));
  
  if (!myDFPlayer.begin(mySoftwareSerial)) {  //Use softwareSerial to communicate with mp3.
    Serial.println(F("Unable to begin:"));
    Serial.println(F("1.Please recheck the connection!"));
    Serial.println(F("2.Please insert the SD card!"));
    while(true){
      delay(0); // Code to compatible with ESP8266 watch dog.
    }
  }
  Serial.println(F("DFPlayer Mini online."));
  
  myDFPlayer.volume(10);  //Set volume value. From 0 to 30
  myDFPlayer.play(1);  //Play the first mp3
}

void loop()
{
  static unsigned long timer = millis();
  
  if (millis() - timer > 15000) {
    timer = millis();
    myDFPlayer.next();  //Play next mp3 every 3 second.
    Serial.println(F("Playing Next one"));
  }
  
  if (myDFPlayer.available()) {
    printDetail(myDFPlayer.readType(), myDFPlayer.read()); //Print the detail message from DFPlayer to handle different errors and states.
  }
}

void printDetail(uint8_t type, int value){
  switch (type) {
    case TimeOut:
      Serial.println(F("Time Out!"));
      break;
    case WrongStack:
      Serial.println(F("Stack Wrong!"));
      break;
    case DFPlayerCardInserted:
      Serial.println(F("Card Inserted!"));
      break;
    case DFPlayerCardRemoved:
      Serial.println(F("Card Removed!"));
      break;
    case DFPlayerCardOnline:
      Serial.println(F("Card Online!"));
      break;
    case DFPlayerUSBInserted:
      Serial.println("USB Inserted!");
      break;
    case DFPlayerUSBRemoved:
      Serial.println("USB Removed!");
      break;
    case DFPlayerPlayFinished:
      Serial.print(F("Number:"));
      Serial.print(value);
      Serial.println(F(" Play Finished!"));
      break;
    case DFPlayerError:
      Serial.print(F("DFPlayerError:"));
      switch (value) {
        case Busy:
          Serial.println(F("Card not found"));
          break;
        case Sleeping:
          Serial.println(F("Sleeping"));
          break;
        case SerialWrongStack:
          Serial.println(F("Get Wrong Stack"));
          break;
        case CheckSumNotMatch:
          Serial.println(F("Check Sum Not Match"));
          break;
        case FileIndexOut:
          Serial.println(F("File Index Out of Bound"));
          break;
        case FileMismatch:
          Serial.println(F("Cannot Find File"));
          break;
        case Advertise:
          Serial.println(F("In Advertise"));
          break;
        default:
          break;
      }
      break;
    default:
      break;
    }
}
```

### 3 Ultrasonic Distance Sensor

- Ultrasonic transmitter to a certain direction to launch ultrasound, in the launch of the same time to start timing, ultrasound propagation in the air, on the way to encounter obstacles immediately return to the ultrasonic receiver received the reflected wave immediately stop timing. Sound waves in the air propagation speed of 340m / s, according to the timer recorded time t, you can calculate the launch point from the distance of the obstacle s, that is: s = 340m / s × t / 2 . This is the so-called time difference distance measurement method.

- Exterior Pictures
<div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/exteriorpicture.png?raw=true" width = "800" />
</div><br></br>


- Connect wire
<div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/connectwire.png?raw=true" width = "800" />
</div><br></br>

- Demo sketch

```cpp
#define PIN_TRIG 12
#define PIN_ECHO 11

float cm;
float temp;

void setup(){
  Serial.begin(9600);
  pinMode(PIN_TRIG, OUTPUT);
  pinMode(PIN_ECHO, INPUT);
}

void loop(){
  digitalWrite(PIN_TRIG, LOW);
  delayMicroseconds(2);
  digitalWrite(PIN_TRIG, HIGH);
  delayMicroseconds(10);
  digitalWrite(PIN_TRIG, LOW);

  temp = float(pulseIn(PIN_ECHO, HIGH));
  cm = (temp*17)/1000;

  Serial.print("Echo = ");
  Serial.print(temp);
  Serial.print(", Distance = ");
  Serial.print(cm);
  Serial.print("cm");
  delay(300);
}
```

### 4 Potential technical issues
- When replacing plants, how to achieve the transfer of the circuit？
- When playing sound, how to achieve the superimposition of sound？
- When connecting the plant to measure the capacitance, the capacitance measurement may fail or be unstable due to external factors？
- How to map the capacitance change to the interaction of the plant？