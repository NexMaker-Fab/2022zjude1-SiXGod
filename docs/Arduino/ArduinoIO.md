# Arduino Application Input & Output

### 1 Display ambient temperature and humidity
- **List of components:**
    - LCD display monitor
    - potentiometer
    - temperature and humidity sensorDHT11
- **Schematic circuit diagram**
    
    <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/AAIO.png?raw=true" width = "1000" />
    </div>
    <br></br>
    
- **Practice process and steps:**
    - Install "LCD Display" and "DHT11" libraries from "Project" -- "Load Library" -- "Manage Library"
        
    <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/AAIO1.png?raw=true" width = "1000" />
    </div>
    <br></br>
        
    - Find the technical parameters, schematics, and pin descriptions of LCD and temperature and humidity sensor DHT11 in the Chinese Arduino community (Taiji Maker)
    - Build the circuit
        
    <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/AAIO2.png?raw=true" width = "1000" />
    </div>
    <br></br>
        
    - Debug code, run and test
- **Run result**
    <div align= 'left'>
    <img src="https://raw.githubusercontent.com/Fy1307/IMGofSixGod/master/img/temperature.GIF"/>
    </div>
    <br></br>
- **code:**
    
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

    

### 2 Near the object, the servo motor turns; Go away, don't turn

- **List of components:**
    - LCD display monitor
    - potentiometer
    - Ultrasonic distance sensor
    - Servo motorSG90
- **Schematic circuit diagram**
    
    <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/AAIO3.png?raw=true" width = "1000" />
    </div>
    <br></br>
    
- **Practice process and steps:**
    - Install "Servo motor SG90" and "LCD display" function library from "Project" -- "Load Library" -- "Management library"
    - Find the technical parameters, schematics and pin descriptions of LCD and servo motor SG90 in the Chinese Arduino community (Taiji Maker)
    - Build the circuit
        
    <div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/AAIO4.png?raw=true" width = "1000" />
    </div>
    <br></br>
        
    - Debug code, run and test
  
- **Run result**
    <div align= 'left'>
    <img src="https://raw.githubusercontent.com/Fy1307/IMGofSixGod/master/img/chaoshengbo.GIF"/>
    </div>
    <br></br>
  
- **code:**
    
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

### Reference

[Tai Chi Maker](http://www.taichi-maker.com/)
    
[LCD Display](http://www.taichi-maker.com/homepage/reference-index/arduino-library-index/liquidcrystal-library/#Arduino%E6%8E%A7%E5%88%B6LCD%E6%B6%B2%E6%99%B6%E5%B1%8F%E7%94%B5%E8%B7%AF)
    
[DHT11 temperature and humidity sensor](http://www.taichi-maker.com/homepage/reference-index/arduino-sensor-index/arduino-dht11-temperature-sensor/)