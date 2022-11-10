# Arduino& Processing

任务：用arduino的摇杆控制processing的“蜘蛛”行走。

### 1  学会使用摇杆
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/Frame_10.jpg?raw=true" width = "1000" div align= 'center' /><br><br/>

```arduino
#define pinX  A0  //声明端口
#define pinY  A1
int value1 = 0;
int value2 = 0;
int x;

void setup()
{
  pinMode(pinX, INPUT); //设置A0 A1两个端口为输入
  pinMode(pinY, INPUT);
  Serial.begin(9600);  //设置波特率 两端波特率一致方可通信
}

void loop()
{
  value1 = analogRead(pinX); 
  value2 = analogRead(pinY);
  Serial.print(value1);  //读取x轴上传的值
  Serial.print(",");
  Serial.println(value2); //读取y轴上传的值
  delay(100);
}
```

依靠上述代码，可以在串口监视器中读到这样的数据。  

<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/data_arduino.png?raw=true" width = "1000" div align= 'center' /><br><br/>

操纵摇杆从一端打到另一端，可以令x或y轴输出范围在0~1023的值。当摇杆处于中立位，会输出500+的中间值，如上图。  


### 2  让processing读取arduino传来的数据

关键代码如下，有这些代码就可以实现双方的通信：  

```java
import processing.serial.*;
Serial myPort;         // 建立一个端口
int input;              // 声明一个变量，赋给它从arduino接收到的数据

void setup() {
    port = new Serial(this,"COM3",9600); //建立一个通道和速率，必须和Arduino一致
}

void draw() {
   int input = port.read();  //将串口收到数据给input
}
```

```arduino

void setup()
{
  Serial.begin(9600);  //设置波特率，两端波特率一致方可通信
}

void loop()
{
	Serial.write();  //将arduino内的数据上传给processing 
  delay(100);
}
```

### 3  让蜘蛛跟随摇杆移动

起初，我的想法是将x轴的数据赋给processing中的变量x，将y轴的数据赋给processing中的变量y，再使用一个map映射函数，将x，y的值（原本应该是0~1023）限定为画布的长宽值，然后用变量x, y控制蜘蛛的位置。

<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/Arduino3.png?raw=true" width = "1000" div align= 'center' /><br><br/>

但是这种方法的问题在于，arduino会连续输出x, y的值，processing是分辨不出来的，如上图。（当然肯定是有办法解决的，只是我基础薄弱T T，没有好的办法）因此最后使用的方法是：首先在arduino中读取摇杆的值，设定8种状态（对应8种移动方式），再由processing读取状态，慢慢地更改x, y的值。

最后代码如下：

```arduino
import processing.serial.*;
Serial port;
int v =1;
int STEP = 40; //矩阵点的步长
int x0 = 0, y0= 0;
float vx = 0, vy = 0; //鼠标取点
int StepRound(int i) { //四舍五入至最近的步长
    return int(round(float(i) / STEP) * STEP);
}

void setup() {
    size(800, 800);//画布大小
    stroke(255);//白色描边
    port = new Serial(this,"COM3",9600);
}

int dist(int x1, int y1,int x2, int y2) {//重载函数dist()
    return int(dist(float(x1),float(y1),float(x2),float(y2)));
}

void draw() {
    background(0); //刷新画布
    int input = port.read(); //读取arduino的状态
    if(input == 1){  //蜘蛛向右下移动
      vx+=v;  //增加x方向的速度
      vy+=v;  //增加y方向的速度
    }
    if(input == 2){ //蜘蛛向右上移动，以下同理
      vx+=v;
      vy-=v;}    
    if(input == 3){
      vx-=v;
      vy+=v;}
    if(input == 4){
      vx-=v;
      vy-=v;}
     if(input == 5) //蜘蛛向右移动
      vx+=v;
    if(input == 6) //蜘蛛向左移动，以下同理
      vx-=v;
    if(input == 7) 
      vy-=v;
    if(input == 8) 
      vy+=v;
    if(input == -1){  //实验过程中发现如果摇杆处于中立位，默认输出-1，此时给蜘蛛添加一个阻力，令其减速
		vx*=0.95; 
    vy*=0.95;}
    
    x0+=round(vx); //改变蜘蛛的坐标，round函数起四舍五入的作用，这样可以让摇杆在中立位停住
    y0+=round(vy);
      
    if(x0<20) x0=20;  //限制蜘蛛的活动范围，不让它移出画布
    if(x0>780) x0=780;
    if(y0<20) y0=20;
    if(y0>780) y0=780;
    ellipse(x0, y0,STEP / 4 ,STEP / 4);//蜘蛛身体
    for (int i = StepRound(x0) - STEP * 2; i <= StepRound(x0) + STEP * 2; i += STEP) {//矩阵打点
        for (int j = StepRound(y0) - STEP * 2; j <= StepRound(y0) + STEP * 2; j += STEP) {
            int leg = dist(x0, y0, i, j);//计算连线距离
            ellipse(i, j,(STEP * 3 - leg) / STEP + 1,(STEP * 3 - leg) / STEP + 1);
            if (leg > STEP && leg < STEP * 2) //连线距离判断
                line(x0, y0, i, j);//蜘蛛脚
        }
    }
    //delay(10);//*****
}
```

```arduino
#define pinX  A0  //声明端口
#define pinY  A1
#define left 480
#define right 560
int value1 = 0;
int value2 = 0;

void setup()
{
  pinMode(pinX, INPUT); //设置A0 A1两个端口为输入
  pinMode(pinY, INPUT);
  Serial.begin(9600);  //设置波特率 两端波特率一致方可通信
}

void loop()
{
  value1 = analogRead(pinX); 
  value2 = analogRead(pinY);
  if(value1 > right && value2 > right)
  Serial.write(1);
  else if(value1 > right && value2 <left)
  Serial.write(2);
  else if(value1 < left && value2 >right)
  Serial.write(3);
  else if(value1 < left && value2 <left)
  Serial.write(4);
  else if(value1 >= right && value2 >=left && value2 <=right)
  Serial.write(5);
  else if(value1 < left && value2 >left && value2 <right)
  Serial.write(6);
  else if(value2 < left && value1 >left && value1 <right)
  Serial.write(7);
  else if(value2 > right && value1 >left && value1 <right)
  Serial.write(8);
  delay(50);
}

```

### 3  效果实现
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/Arduino_Result.GIF?raw=true" width = "1000" div align= 'center' /><br><br/>