# Preliminary experimental procedure

### 1 Capacitance changes are monitored and mapped to white noise

- **List of components:**
    - DFPlayer mini SCM
    - SD card & Card reader
    - Speaker

- **Circuit diagram:**
    
    <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/cnct.jpg?raw=true" width = "1000" />
    </div>
    
- **Operational process and steps:**
    - Configure the DFRobotDFPlayerMini library and CapacitiveSensor library
    - Try playing music from your SD card
    - Import the white noise into the SD card
    - Build circuits and use codes to monitor capacitance changes and map them to different white noises
    <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/musicmodule2.png?raw=true" width = "1000" />
    </div>

- **Code:**
```c++
#include <CapacitiveSensor.h>
#include "Arduino.h"
#include "DFRobotDFPlayerMini.h"
#include "SoftwareSerial.h"
CapacitiveSensor Sensor1 = CapacitiveSensor(2,3);  //森林-蕨类，电阻23.5k欧（并联俩47），触摸时峰值为50-60左右
CapacitiveSensor Sensor2 = CapacitiveSensor(4,6);  //沙漠-仙人掌，电阻47k欧，触摸时峰值为100-180左右
CapacitiveSensor Sensor3 = CapacitiveSensor(8,10);  //湖泊-睡莲，电阻94k欧（串联俩47），触摸时峰值为200-280左右
/*SD卡1 引脚*/
SoftwareSerial mySoftwareSerial(11, 12); // RX, TX
DFRobotDFPlayerMini DFPlayer1;
long val1;  //森林-蕨类
long val2;  //沙漠-仙人掌
long val3;  //湖泊-睡莲
void setup() {
  mySoftwareSerial.begin(9600);
  Serial.begin(9600);

  Serial.println();
  Serial.println(F("DFRobot DFPlayer Mini Demo"));
  Serial.println(F("Initializing DFPlayer ... (May take 3~5 seconds)"));
  
  if (!DFPlayer1.begin(mySoftwareSerial)) {  //Use softwareSerial to communicate with mp3.
    Serial.println(F("Unable to begin:"));
    Serial.println(F("1.Please recheck the connection!"));
    Serial.println(F("2.Please insert the SD card!"));
    while(true);
  }
  Serial.println(F("DFPlayer Mini online."));

  //设置音量为20
  DFPlayer1.volume(20);
}
void loop() {

  val1 = Sensor1.capacitiveSensor(30);  //森林-蕨类
  val2 = Sensor2.capacitiveSensor(30);  //沙漠-仙人掌
  val3 = Sensor3.capacitiveSensor(30);  //湖泊-睡莲

  Serial.print(val1);  //森林-蕨类
  Serial.print(" ");
  Serial.print("\t");

  Serial.print(val2);  //沙漠-仙人掌
  Serial.print(" ");
  Serial.print("\t");

  Serial.print(val3);  //湖泊-睡莲
  Serial.print(" ");
  Serial.print("\t");
  Serial.println();
  delay(200);
  
  
  if (val1 >= 50){
    //森林模块
    Serial.println("forest");
    delay(200);
    DFPlayer1.playFolder(1, 1);
    delay(10000);
    DFPlayer1.playFolder(1, 2);
    delay(11000);
    DFPlayer1.playFolder(1, 3);
    delay(300000);
  }
  else if (val2 >= 100){
    //湖泊模块
    Serial.println("lake");
    DFPlayer1.playFolder(2, 1);
    delay(10000);
    DFPlayer1.playFolder(2, 2);
    delay(11000);
    DFPlayer1.playFolder(2, 3);
    delay(300000);
  }
  else if (val3 >= 200){
    //沙漠模块
    Serial.println("desert");
    DFPlayer1.playFolder(3, 1);
    delay(10000);
    DFPlayer1.playFolder(3, 2);
    delay(11000);
    DFPlayer1.playFolder(3, 3);
    delay(300000);
  }
  
  delay(10);
}
```