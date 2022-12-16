# First Try of Processign
Processing is a revolutionary and forward-looking new computer language. Its concept is to introduce programming languages in the environment of electronic art, and introduce the concept of electronic art to programmers. 
It is an extension of the Java language and supports many of the existing Java language architectures, but it is much simpler in syntax and has many intimate and user-friendly designs.

### 1  The first interactive demo was born
- With the mindset of copy and paste, I went to OpenProcessing to steal the creative code and found a spider crawling sample such as the following:

![](https://raw.githubusercontent.com/Fy1307/IMGofSixGod/master/img/Pcs1.gif)

- Unfortunately, the source code is compiled in an unknown language and cannot be copied. I had to do it myself.
<div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/pcs2.png?raw=true" width = "1000" />
</div>
<br></br>

- After understanding the meaning of the source code, I rewrote the processing syntax as follows. 
  
### 2  Code
```jsx
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


### 3  Solutions for problems  
- Function dist() can only pass parameters of type float, which is too limited. Let's overload the function to work with int. The functions are as follows:
```java
    int dist(int x1, int y1,int x2, int y2) {//重载函数dist()
    return int(dist(float(x1),float(y1),float(x2),float(y2)));
    }
```

- Refresh the canvas every time you loop through draw(), or the screen will stack up.
```java
background(0);//刷新画布
```
### 4  Final results
<img src="https://raw.githubusercontent.com/Fy1307/IMGofSixGod/master/img/pscdemo.GIF"/>


### Reference
[Processing Introduction](https://baike.baidu.com/item/Processing/378062?fr=aladdin)  
[Code reference](https://openprocessing.org)