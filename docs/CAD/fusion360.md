# CAD设计

Fusion 360 是一款基于远程服务的三维建模、CAD、CAM、CAE 和 PCB 软件平台，主要用于产品设计和制造。本组所有人都是第一次接触这个软件，最初都觉得有些不习惯，但是慢慢地就感觉到了这个新生建模软件的优越性。

### 1  第一个3D模型的诞生
#### 1.1 详细建模过程
● 新建零部件，分别重命名，汽缸示意图共分为6个——摇杆、活塞、偏心轴、偏心轴座、汽缸、销。<br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/FU1.png?raw=true" width = "1000" div align= 'center' /><br><br/>

● 在对应的零部件中，创建草图。<br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/FU2.png?raw=true" width = "1000" div align= 'center' /><br><br/>

● 选择对应的草图，在“修改”栏中选择“推拉”，从草图生成实体。<br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/FU3.png?raw=true" width = "1000" div align= 'center' /><br><br/>

<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/FU4.png?raw=true" width = "1000" div align= 'center' /><br><br/>

● 选择对应“实体”，右键“从实体创建零部件”，为后续的“装配”环节做准备。待六个模型部分全部转化为零部件后，提前思考并确定各部分的装配关系与参考轴走向，例如：沿x/y/z轴形成滑块、旋转、刚性关系等。<br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/FU5.png?raw=true" width = "1000" div align= 'center' /><br><br/>

● 在“装配”栏中选择“联接原点”，分别确定各部件的装配基准点，并进行厚度偏移。<br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/FU6.png?raw=true" width = "1000" div align= 'center' /><br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/FU7.png?raw=true" width = "1000" div align= 'center' /><br><br/>

● 设定完所有的“联接原点”后，选择装配中的“联接”，将各六个部分两两配合，例如：活塞和汽缸以各自顶部的联接点为基准，沿着Z轴形成滑动关系。<br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/FU8.png?raw=true" width = "1000" div align= 'center' /><br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/FU9.png?raw=true" width = "1000" div align= 'center' /><br><br/>

● 完成所有部件的“装配联接”后，须确定部件的“刚性组”，在本案例中选择“汽缸”和“偏心轴座”为刚性组。<br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/FU10.png?raw=true" width = "1000" div align= 'center' /><br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/FU11.png?raw=true" width = "1000" div align= 'center' /><br><br/>

● 点击“偏心轴”与“偏心轴座”的旋转联接标记，即可调整不同的转动角度，带动整个汽缸进行活塞运动。<br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/FU12.png?raw=true" width = "1000" div align= 'center' /><br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/FU13.png?raw=true" width = "1000" div align= 'center' /><br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/FU14.png?raw=true" width = "1000" div align= 'center' /><br><br/>



#### 1.2 建模过程动画
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/PisonProcess2.GIF?raw=true" width = "1000" div align= 'center' /><br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/PisonProcess1.GIF?raw=true" width = "1000" div align= 'center' /><br><br/>

#### 1.3 工程图
● 在此展示偏心轴座的工程图：<br><br/>
<iframe src="https://myhub.autodesk360.com/ue28cacf9/shares/public/SH35dfcQT936092f0e4306430011aadf5b5b?mode=embed" width="800" height="600" allowfullscreen="true" webkitallowfullscreen="true" mozallowfullscreen="true"  frameborder="0"></iframe><br><br/>

#### 1.4 最终效果
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/Piston.GIF?raw=true" width = "1000" div align= 'center' /><br><br/>

<iframe src="https://myhub.autodesk360.com/ue28cacf9/shares/public/SH35dfcQT936092f0e4347a820aaecd0cf0f?mode=embed" width="800" height="600" allowfullscreen="true" webkitallowfullscreen="true" mozallowfullscreen="true"  frameborder="0"></iframe><br><br/>


### 2  其他CAD软件介绍
ProE是美国参数技术公司的重要产品，在三维造型软件领域中占有着重要地位，是现今主流的模具和产品设计三维CAD/CAM软件之一。
ProE第一个提出了参数化设计的概念，并且采用了单一数据库来解决特征的相关性问题。另外，它采用模块化方式，用户可以根据自身的需要进行选择，而不必安装所有模块。Pro/E的基于特征方式，能够将设计至生产全过程集成到一起，实现并行工程设计。<br><br/>

<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/ProE.jpg?raw=true" width = "1000" div align= 'center' /><br><br/>

### 3  参考
[Fusion360活塞建模教程](https://www.youtube.com/watch?v=62XqdYv7pWs)  
[ProE介绍](https://baike.baidu.com/reference/49241726c08j20UHV0JtDD2doRGdAkLi_wFFRSTJR8ap1lom0i0AnlPhgYQVKk2NVeZ10_UHWo3DL_2xmjkbe2dTbZCuW2aGAk)
