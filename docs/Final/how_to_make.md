# 植物🌳Arduino Application

### 1 显示环境温湿度

- **元件清单：**
    - LCD显示屏
    - 电位器
    - 温湿度传感器DHT11
- **连线示意图：**
    
    <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/tempre1.png?raw=true" width = "1000" />
    </div>
    
- **实操过程与步骤：**
    - 从“项目”——“加载库”——“管理库”——安装“LCD Display”和“DHT11”的函数库
        
    <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/tempre2.png?raw=true" width = "1000" />
    </div>
        
    - 查找中文Arduino社区（太极创客）中，关于LCD和温湿度传感器DHT11的技术参数、原理图、引脚说明
    - 搭建电路
        
    <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/tempre3.png?raw=true" width = "1000" />
    </div>

    - 调试代码，运行，测试
- **程序代码：**
    
    ```cpp
    #include <EduIntro.h> 
    #include <LiquidCrystal.h>
    LiquidCrystal lcd(12,11,5,4,3,2);  //定义脚位
    DHT11 dht11(D7);
    float h;
    float t;
    
    void setup()
    {
    Serial.begin(9600);
    lcd.begin(16,2); //设置LCD显示的数目。16 X 2：16格2行。
    }
    
    void loop()
    {
    dht11.update();
    h=dht11.readHumidity();
    t=dht11.readCelsius();
    lcd.print("Humidity:");
    lcd.print(h);
    Serial.println("Humidity:");
    Serial.print(h,DEC);
    Serial.println("");
    lcd.setCursor(0,1);  //将闪烁的光标设置到column 0, line 1 (注释：从0开始数起，line 0是显示第一行，line 1是第二行。)
    lcd.print("Temperature:");
    lcd.print(t);
    Serial.println("Temperature:");
    Serial.print(t,DEC);
    Serial.println("");
    Serial.println("");
    delay(5000);
    lcd.clear();
    
    }
    ```
    
- **参考**
    
    （1）太极创客：[http://www.taichi-maker.com/](http://www.taichi-maker.com/)
    
    （2）LCD Display液晶屏：[http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/#Arduino控制LCD液晶屏电路](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/#Arduino%E6%8E%A7%E5%88%B6LCD%E6%B6%B2%E6%99%B6%E5%B1%8F%E7%94%B5%E8%B7%AF)
    
    （3）DHT11温湿度传感器：[http://www.taichi-maker.com/homepage/reference-index/arduino-sensor-index/arduino-dht11-temperature-sensor/](http://www.taichi-maker.com/homepage/reference-index/arduino-sensor-index/arduino-dht11-temperature-sensor/)
    

### 2 靠近物体，伺服马达转动；远离，不转动

- **元件清单：**
    - LCD显示屏
    - 电位器
    - 超声波距离传感器
    - 伺服马达SG90
- **连线示意图：**
    
    <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/motor1.png?raw=true" width = "1000" />
    </div>
    
- **实操过程与步骤：**
    - 从“项目”——“加载库”——“管理库”——安装“伺服马达SG90”和“LCD显示屏”的函数库
    - 查找中文Arduino社区（太极创客）中，关于LCD和伺服马达SG90的技术参数、原理图、引脚说明
    - 搭建电路
        
    <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/motor2.png?raw=true" width = "1000" />
    </div>
        
    - 调试代码，运行，测试
- **程序代码：**
    
    ```cpp
    #include <LiquidCrystal.h>
    #include <Servo.h> //想使用伺服马达，一定要先加这行，就是导入函数库的意思
    Servo myservo;  // 先确定马达对象的名字即代号
    
    #define TrigPin A0
    
    #define EchoPin A1
    
    //脉冲宽度(PULSE WIDTH)代表距离(超声发射的时间，来回)
    //脉宽不会超过38ms，表示超时
    //距离=速度x时间
    //声速~= 340米/秒= 0.340毫米/秒
    
    int count = 0;
    int angle=0;
    
    long duration;
    
    LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
    
    void setup() {
    myservo.attach(9);  // 宣告此马达的讯号控制脚位为9号脚位
    Serial.begin(115200);
    pinMode(TrigPin, OUTPUT);
    pinMode(EchoPin, INPUT);
    digitalWrite(TrigPin, LOW);
    delay(1);
    lcd.begin(16, 2);
    }
    
    void loop() {
    Serial.println(count++);
    Serial.println(getDistance());
    Serial.println("");
    Serial.println("");
    lcd.begin(16, 2);
    lcd.print("Distance:");
    lcd.setCursor(0, 1);
    lcd.print(getDistance());
    delay(1000);
    lcd.clear();
    
    if (getDistance() < 100){   //当距离近，小于100mm时
      digitalWrite(13,HIGH);
      angle=180;
      myservo.write(angle);
      delay(1000);
      angle=0;
      myservo.write(angle);
    
    }else{
      digitalWrite(13,LOW);
    }
    
    Serial.println(angle);
    }
    
    long getDistance() {
    // trig
    digitalWrite(TrigPin, LOW);
    delayMicroseconds(2);
    digitalWrite(TrigPin, HIGH);
    delayMicroseconds(10);
    digitalWrite(TrigPin, LOW);
    // echo
    duration = pulseIn(EchoPin, HIGH);     // unit: us
    return duration * 0.34029 / 2;         // unit: mm
    }
    ```

### 3 监测电容变化并映射到音乐

- **元件清单：**
    - DFPlayer mini单片机
    - SD卡和读卡器
    - 小音箱

- **连线示意图：**
    
    <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/musicmodule1.png?raw=true" width = "1000" />
    </div>
    
- **实操过程与步骤：**
    - 配置DFRobotDFPlayerMini库和CapacitiveSensor库
    - 尝试播放SD卡中的音乐
    - 采样音乐并导入SD卡
    - 搭建电路，用代码监测电容变化并映射到音高
    <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/musicmodule2.png?raw=true" width = "1000" />
    </div>

- **程序代码：**
    ```java
    #include "Arduino.h"
    #include "SoftwareSerial.h"
    #include "DFRobotDFPlayerMini.h"
    #include <CapacitiveSensor.h> 

    CapacitiveSensor ini = CapacitiveSensor(2,6);
    long touch;

    SoftwareSerial mySoftwareSerial(10, 11); // RX, TX
    DFRobotDFPlayerMini myDFPlayer;
    void printDetail(uint8_t type, int value);

    void setup()
    {
    mySoftwareSerial.begin(9600);
    Serial.begin(9600);

    Serial.println();
    Serial.println(F("DFRobot DFPlayer Mini Demo"));
    Serial.println(F("Initializing DFPlayer ... (May take 3~5 seconds)"));
  
    if (!myDFPlayer.begin(mySoftwareSerial)) {  //Use softwareSerial to communicate with mp3.
        Serial.println(F("Unable to begin:"));
        Serial.println(F("1.Please recheck the connection!"));
        Serial.println(F("2.Please insert the SD card!"));
        while(true);
    }
    Serial.println(F("DFPlayer Mini online."));
  
    pinMode(8,OUTPUT);
  
    myDFPlayer.volume(20);  //Set volume value. From 0 to 30
    myDFPlayer.playFolder(1,1);  //开机问候语
    }

    void loop()
    {
    touch = ini.capacitiveSensor(30);
    delay(10);
    Serial.println(touch);
    if(touch > 0){
        digitalWrite(8,HIGH);
        delay(200);
        touchNum++;
    }
    else{
        digitalWrite(8,LOW);
        delay(200);
    }
    delay(10);

    musicModule();
    }

    void musicModule(){
    if (touch != -2) {
      if (touch > 0 && touch <=9 ) {
        //Serial.println("0-9");
        myDFPlayer.playFolder(4, 1 + touch/2);
        delay(3000);
      }
      else if (touch >= 10 && touch <=99) {
        Serial.println("10-100");
        myDFPlayer.playFolder(4, 6 + touch/20);
        delay(3000);
      }      
      else if (touch >= 100 && touch <= 999) {
        Serial.println("100-999");
        myDFPlayer.playFolder(4, 11 + touch/200);
        delay(3000);
      }
      else if (touch >= 1000 && touch <= 9999) {
        Serial.println("1000-9999");
        myDFPlayer.playFolder(4, 16 + touch/2000);
        delay(3000);
      }
      else if (touch >= 10000 && touch <= 99999) {
        Serial.println("10000-99999");
        myDFPlayer.playFolder(4, 21 + touch/20000);
        delay(3000);
      }
    }
    }
    ```