# 网页构建流程

本组采用 GitHub+Docsify 的方式构建了我们的网页。Docsify是一个简易的文档网站生成器，GitHub则提供了免费且适合团队合作的网页文件管理服务。

### 1  工具准备和环境配置
● 首先你要有自己的[GitHub](https://github.com)账号  

● 下载[Git（Mac用户不需要）](https://blog.csdn.net/weixin_47638941/article/details/120632890)、[GitHub Desktop](https://desktop.github.com)、[VScode](https://baijiahao.baidu.com/s?id=1737611420111454761&wfr=spider&for=pc)和[Picgo](https://blog.csdn.net/weixin_42837669/article/details/126279327)  

● 下载[nodejs](https://www.runoob.com/nodejs/nodejs-install-setup.html)以配置环境  


### 2  网页设置
#### 2.1 建立团队仓库  
建立一个属于团队的仓库，这一步由老师完成。  

#### 2.2 网页部署 
在GitHub上部署属于团队的网页，在这一步我们获得了一个空白网页和它的链接。
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild2-1.png?raw=true" width = "1000" div align= 'center' /><br><br/>

<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild2-2.png?raw=true" width = "1000" div align= 'center' /><br><br/>

<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild2-3.png?raw=true" width = "1000" div align= 'center' /><br><br/>


### 3  本地设置
#### 3.1 克隆网页文件到本地
每次修改网页文件内容之前都需要先将最新版的网页文件克隆到本地，GitHub Desktop提供了这一功能，让操作变得非常简单。
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild3-1.png?raw=true" width = "1000" div align= 'center' /><br><br/>

<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild3-2.png?raw=true" width = "1000" div align= 'center' /><br><br/>

#### 3.2 使用Docsify编辑网页
● 在安装Docsify之前请确定已经安装了nodejs。  
安装配置教程：[Window版](https://www.cnblogs.com/wanpi/p/16119433.html)  ; 
[IOS版](https://blog.csdn.net/qq_45220508/article/details/122972391)

● 使用命令行语句在终端安装Docsify
> npm i docsify-cli -g

● 初始化环境
首先定位到网页文件的本地位置,在该位置初始化环境.
> cd +本地位置  

> docsify init ./docs

● 运行和预览
> docsify serve docs  

然后就可以在 http://localhost:3000 预览你的网页啦！

● 设置index.html和侧边栏
index.html的代码内容如下：

```html
<!DOCTYPE html>
<html>
<head>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <meta charset="UTF-8">
  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/themes/vue.css" />
  <title>SIXGOD</title>
  <link rel="icon" type="image/png" href="https://github.com/Fy1307/IMGofSixGod/
  blob/master/img/Favicon.png?raw=true" >
  <!-- Theme: Simple Dark 
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/docsify-themeable@0/dist/css/theme-simple-dark.css">
  -->
</head>
<body>
  <div id="app"></div>
  <script>
    window.$docsify = {
        loadSidebar: true,
        coverpage: true,
        onlyCover: true,
  }
  </script>
  <script src="//cdn.jsdelivr.net/npm/docsify@4"></script>
</body>
</html>
```

然后在docs文件夹里新建一个空文件".nojekyll"，它的作用是防止docsify忽略"_"开头的的文件。此后新建"_sidebar.md"，在里面输入侧边栏的内容。

##### 3.3 上传到GitHub
用GitHub Desktop上传变更并在GitHub上查看网页结果。
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild3-4.png?raw=true" width = "1000" div align= 'center' /><br><br/>

<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild3-5.png?raw=true" width = "1000" div align= 'center' /><br><br/>

#### 3.4 网页图片资源管理
为了减小网页文件所占空间，我们采用GitHub+PicGo的方式将文件上传至我们的图片仓库，并在网页文件中直接引用图片地址。
● 建立一个图片仓库，并生成一个给PicGo的密钥

● 配置PicGo
密钥可由GitHub生成，具体参见[密钥生成](https://www.nexmaker.com/doc/1projectmanage/imageuploadservice.html)
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/PicGoConfig.png?raw=true" width = "1000" div align= 'center' /><br><br/>

● 调用图片网址
在图片仓库获得需要引用的图片地址就可以在md文档中插入图片了。
```html
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild3-1.png?raw=true" width = "1000" div align= 'center' /><br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild3-2.png?raw=true" width = "1000" div align= 'center' /><br><br/>
```

### 4  问题解决
#### 4.1 Docsify在Macbook(M1)的下载和运行问题
● 安装权限问题
如果在安装时出现问题，请尝试在安装语句之前加上"sudo "。

● 终端配置问题
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/zsh.png?raw=true" width = "1000" div align= 'center' /><br><br/>
部分macbook的配置文件可能比较与众不同，本人的Macbook就不幸中彩了。  
遇到"zsh: command not found"这样的错误提示，可参考这个教程尝试解决：[解决教程](https://www.jianshu.com/p/64c175476acc)

#### 4.2 网页文件结构变化后上传github的问题
GitHub Desktop中的commit键是灰色，是因为你还没有给出本次修改的描述。上传后需要等待片刻才能在GitHub上看到网页的改变。
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/upload.png?raw=true" width = "1000" div align= 'center' /><br><br/>

### 参考
[总体流程学习](https://www.nexmaker.com)  
[Markdown语法](https://www.runoob.com/markdown/md-link.html)  
[Docsify官方文档](https://docsify.js.org/#/)