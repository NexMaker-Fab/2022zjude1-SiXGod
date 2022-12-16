# ESP32

### 1 Introduction

- The ESP32 SoC chip supports the following features.
  - 2.4 GHz Wi-Fi
  - Bluetooth
  - High-performance Xtensa® 32-bit LX6 dual-core processor
  - Ultra-low power co-processor
  - Multiple Peripherals

ESP32 is made by 40 nm process, with the best power performance, RF performance, stability, versatility and reliability, suitable for various application scenarios and different power requirements.

Loxin provides users with complete software and hardware resources for the development of ESP32 hardware devices. Among them, Loxin's software development environment, ESP-IDF, is designed to assist users to quickly develop Internet of Things (IoT) applications, which can meet users' requirements for Wi-Fi, Bluetooth, low power consumption, etc.

- PINOUT Picture
  <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/PINOUTPICTURE.png?raw=true" width = "1000" />
  </div>
  <br></br>   

### 2 Application

- Function Introduction

Through the nodeMCU module on the esp32, the application Blinker is connected to the cell phone via Wi-Fi. The DHT11 temperature and humidity sensor, vibration module, and SG90 servo are connected to the esp32 in turn, and the corresponding buttons and data reading boxes are set on the Blinker application to realize the temperature and humidity reading function and the control function of vibration and servo.

- Blinker app Introduction

Blinker is a professional and easy-to-use IoT solution that provides server, application, and device side sdk support. The server side developed based on high-performance asynchronous framework can carry a large number of device connections, allowing device owners to easily manage their devices; the simple and convenient application with multi-device support sdk allows developers to achieve device access in 3 minutes. There are three editions of the Blinker service, the community edition is open source and free, so that everyone can experience the features and advantages of the Spotlight solution; the cloud service edition provides more value-added services and functions, and effectively reduces the project implementation costs for customers, allowing them to upgrade their IoT faster; the commercial edition can be deployed independently, which can meet more diverse needs of customers.

- Connect Wire Picture and Physical Picture

  <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/电路.png?raw=true" width = "1000" />
  </div>
  <br></br>  
  <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/实物图.png?raw=true" width = "1000" />
  </div>
  <br></br>

- Blinker app Set
  <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/app1.png?raw=true" width = "1000" />
  </div>
  <br></br>
  <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/app2.png?raw=true" width = "1000" />
  </div>
  <br></br>
    <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/app3.png?raw=true" width = "1000" />
  </div>
  <br></br>
    <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/app4.png?raw=true" width = "1000" />
  </div>
  <br></br>

- Implementation code

```cpp
#define BLINKER_WIFI
 
#include <Blinker.h>
#include <DHT.h>
#include <Servo.h>

char auth[] = "ba56818a6d1f";       //app中获取到的Secret Key
char ssid[] = "hsc";                //WiFi热点名称
char pswd[] = "88888888";           //WiFi密码
 
Servo myservo;  //创建一个舵机控制对象
int pos = 0;    // 

BlinkerNumber HUMI("humi");     //湿度
BlinkerNumber TEMP("temp");     //温度
BlinkerButton Button1("btn1");  //震动
BlinkerButton Button2("btn2");  //舵机

#define DHTPIN 2  
#define DHTTYPE DHT11   // DHT 11

 
DHT dht(DHTPIN, DHTTYPE);
 
float humi_read = 0, temp_read = 0;
 
void th()
{
    //反馈温度数据
    HUMI.print(humi_read);
    HUMI.icon("fas fa-thermometer-2");
    HUMI.color("#fddb10");

    //反馈湿度数据
    TEMP.print(temp_read);
    TEMP.icon("fas fa-heart");
    HUMI.color("#fddb01");
}

void Button1_callback(const String & state){
    if (state == "press") {    
      digitalWrite(4,HIGH);    
      delay(30);
  }
    else{
      digitalWrite(4,LOW);
      delay(30);
    }    
} 

void Button2_callback(const String & state){
    if (state == "press") {               
      myservo.write(0);
      for(pos = 0; pos <= 180; pos ++)    
        {                                    
        myservo.write(pos);               
        delay(10);                        
      } 
      for(pos = 180; pos >= 0; pos --)      
        {                                
        myservo.write(pos);                
        delay(10);                         
      }
  }    
} 

void setup()
{
    Serial.begin(9600);
    BLINKER_DEBUG.stream(Serial);
    BLINKER_DEBUG.debugAll();
    pinMode(13, OUTPUT);
    digitalWrite(13, HIGH);
 
    Blinker.begin(auth, ssid, pswd);
    Blinker.attachHeartbeat(th);
    dht.begin();

    myservo.attach(16);
}
 
void loop()
{
    Blinker.run();
 
    float h = dht.readHumidity();
    float t = dht.readTemperature();
 
    if (isnan(h) || isnan(t))
    {
        BLINKER_LOG("Failed to read from DHT sensor!");
    }
    else
    {
        BLINKER_LOG("Humidity: ", h, " %");
        BLINKER_LOG("Temperature: ", t, " *C");
        humi_read = h;
        temp_read = t;
    }

    pinMode(4,OUTPUT);
    Button1.attach(Button1_callback); 
    Button2.attach(Button2_callback);
    Blinker.delay(2000);
}
```

- Achieving results

