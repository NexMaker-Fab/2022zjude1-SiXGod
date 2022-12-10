# Web Page Construction Process

We built our web page using GitHub+Docsify. Docsify is a simple document site generator, and GitHub provides a free and team-friendly web file management service.

### 1  Tool preparation and environment configuration
- First, you need to have your own[GitHub](https://github.com)account  


- Download [Git（The user of Mac doesn't have to）](https://blog.csdn.net/weixin_47638941/article/details/120632890)、[GitHub Desktop](https://desktop.github.com)、[VScode](https://baijiahao.baidu.com/s?id=1737611420111454761&wfr=spider&for=pc) and [Picgo](https://blog.csdn.net/weixin_42837669/article/details/126279327)  
  
- Download [nodejs](https://www.runoob.com/nodejs/nodejs-install-setup.html) to configure the environment  


### 2  Web page Setup
#### 2.1 Building a team warehouse  
Set up a warehouse that belongs to the team, this step is completed by the teacher. 

#### 2.2 Web page deployment 
Deploy the team's web page on GitHub, where we get a blank web page and a link to it.
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild2-1.png?raw=true" width = "1000" div align= 'center' /><br><br/>

<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild2-2.png?raw=true" width = "1000" div align= 'center' /><br><br/>

<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild2-3.png?raw=true" width = "1000" div align= 'center' /><br><br/>


### 3 Local settings
#### 3.1 Clone the web page file locally
Every time you modify the content of the web file, you need to clone the latest version of the web file to the local. GitHub Desktop provides this function, so that the operation becomes very simple.
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild3-1.png?raw=true" width = "1000" div align= 'center' /><br><br/>

<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild3-2.png?raw=true" width = "1000" div align= 'center' /><br><br/>

#### 3.2 Edit web pages using Docsify
- Make sure you have nodejs installed before installing Docsify.  
Installation and Configuration tutorial: [Windows](https://www.cnblogs.com/wanpi/p/16119433.html)  ; 
[IOS](https://blog.csdn.net/qq_45220508/article/details/122972391)

- Install Docsify in the terminal using command-line statements
> npm i docsify-cli -g

- Initialization
First navigate to the local location of the web page file and initialize the environment at that location.
> cd + Local location  

> docsify init ./docs

- Run and preview
> docsify serve docs  

Then you can preview your page at http://localhost:3000 

- Set index.html and sidebar
The code for index.html is as follows:

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

Then create an empty file ".nojekyll" in your docs folder. This will prevent docsify from ignoring files starting with "_". Then create "_sidebar.md" and enter the contents of the sidebar inside. The sidebar code is as follows:

```html
<div align= 'center'>
  <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/logo.jpg?raw=true" width = "200"/>
</div>

* Team Information
  * [Team Introduction](teamintro/member.md)
  
* Assignment
  * Project Management
    * [Web Page Construction](webbulid/webbuild.md)
    * [Web Page Beautification](webbulid/webbeautify.md)
  * CAD Design
    * [Fusion360](CAD/fusion360.md)
    * [Introduction to Other CAD Softwares](CAD/OtherCAD.md)
  * Arduino Basic
    * [First Try of Processing](Processing/FirstProcessign.md)
    * [Arduino & Processing](Arduino/Arduino.md)

* Final Project
  * [Design Theme](Final/topic.md)
  * [User Research](Final/UserResearch.md)
  * [Innovation Points](Final/InnovationPoints.md)
  * [Market Research](Final/MarketResearch.md)
  * [Design Scheme](Final/designScheme.md)
  * [Experimentation](Final/how_to_make.md)
  * [Key Technology](Final/KeyTechnology.md)
  * [Demo](Final/Demo.md)



```

##### 3.3 Upload to GitHub
Upload changes using GitHub Desktop and view the web results on GitHub.
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild3-4.png?raw=true" width = "1000" div align= 'center' /><br><br/>

<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild3-5.png?raw=true" width = "1000" div align= 'center' /><br><br/>

#### 3.4 Web image resource management
In order to reduce the space occupied by web files, we use GitHub+PicGo to upload files to our image warehouse, and refer to the image address directly in the web file.
- Create an image repository and generate a key for PicGo.

- Config PicGo
The key can be generated by GitHub, see details[key generation](https://www.nexmaker.com/doc/1projectmanage/imageuploadservice.html)
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/PicGoConfig.png?raw=true" width = "1000" div align= 'center' /><br><br/>

- Call the image URL
To insert the image in the md document, get the image address that you need to reference in the image repository.
```html
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild3-1.png?raw=true" width = "1000" div align= 'center' /><br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/webuild3-2.png?raw=true" width = "1000" div align= 'center' /><br><br/>
```

### 4  Problem solving
#### 4.1 Docsify download and run issues on Macbook(M1)
- Installation permission issues
If you have problems installing, try adding "sudo "before the installation statement.

- Terminal Configuration issues
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/zsh.png?raw=true" width = "1000" div align= 'center' /><br><br/>
Some MacBooks may have different profiles.
If you encounter an error such as "zsh: command not found", you can use this tutorial to try to solve it: [solution](https://www.jianshu.com/p/64c175476acc)

#### 4.2 The problem of uploading Github after changing the structure of the webpage file
The commit key in GitHub Desktop is gray because you haven't given a description of the change. You need to wait a while after uploads to see the changes on GitHub.
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/upload.png?raw=true" width = "1000" div align= 'center' /><br><br/>

### Reference
[Overall process learning](https://www.nexmaker.com)  
[Markdown syntax](https://www.runoob.com/markdown/md-link.html)  
[Docsify official document](https://docsify.js.org/#/)