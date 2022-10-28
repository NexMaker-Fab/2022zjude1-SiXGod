# Processign初试
Processing是一种具有革命前瞻性的新兴计算机语言，它的概念是在电子艺术的环境下介绍程序语言，并将电子艺术的概念介绍给程序设计师。  
它是 Java 语言的延伸，并支持许多现有的 Java 语言架构，不过在语法上简易许多，并具有许多贴心及人性化的设计。

### 1 第一个交互demo的诞生
● 抱着复制粘贴的心态，去OpenProcessing偷创意代码，找到了一个蜘蛛爬爬的样例如下：    

![](https://raw.githubusercontent.com/Fy1307/IMGofSixGod/master/img/Pcs1.gif)

● 但是很遗憾源码是用不明语言编译的了，无法copy。只能自己动手。  
<div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/pcs2.png?raw=true" width = "1000" />
</div>
<br></br>

● 将源代码的意思理解后，重新写成processing的语法，如下：  
```java
int STEP = 40;//矩阵点的步长

int StepRound(int i) {//四舍五入至最近的步长
    return int(round(float(i) / STEP) * STEP);
}

void setup() {
    size(800, 800);//画布大小
    stroke(255);//白色描边
}

int dist(int x1, int y1,int x2, int y2) {//重载函数dist()
    return int(dist(float(x1),float(y1),float(x2),float(y2)));
}

void draw() {
    background(0);//刷新画布
    int x = mouseX,y = mouseY;//鼠标取点
    ellipse(x, y,STEP / 4 ,STEP / 4);//蜘蛛身体
    for (int i = StepRound(x) - STEP * 2; i <= StepRound(x) + STEP * 2; i += STEP) {//矩阵打点
        for (int j = StepRound(y) - STEP * 2; j <= StepRound(y) + STEP * 2; j += STEP) {
            int leg = dist(x, y, i, j);//计算连线距离
            ellipse(i, j,(STEP * 3 - leg) / STEP + 1,(STEP * 3 - leg) / STEP + 1);
            if (leg > STEP && leg < STEP * 2) //连线距离判断
                line(x, y, i, j);//蜘蛛脚
        }
    }
}
```


### 2 问题解决  
● dist()函数的传参只能是float类型，过于局限，我们重载一下函数，使其适用于int类型。函数如下：  
```java
int dist(int x1, int y1,int x2, int y2) {//重载函数dist()
return int(dist(float(x1),float(y1),float(x2),float(y2)));
}
```

● 每次循环draw()时要刷新一下画布，要不然画面就会往上叠。  
```java
background(0);//刷新画布
```
### 3 最终效果
<img src="https://raw.githubusercontent.com/Fy1307/IMGofSixGod/master/img/pscdemo.GIF"/>


### 参考
[Processing介绍](https://baike.baidu.com/item/Processing/378062?fr=aladdin)  
[代码参考来源](https://openprocessing.org)