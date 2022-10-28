# 网页美化

### 1  封面
● 首先在index.html中，把coverpage的属性设置为true  

● 新建一个文件 _coverpage.md  <br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/cover.png?raw=true" width = "1000" div align= 'center' /><br><br/>

● 封面效果如图  <br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/cover1.png?raw=true" width = "1000" div align= 'center' /><br><br/>

### 2  网页小图标
● 在index.html的head部分加入以下代码  <br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/IconCode.png?raw=true" width = "1000" div align= 'center' /><br><br/>

● 图标效果如图  <br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/Icon.png?raw=true" width = "1000" div align= 'center' /><br><br/>

### 3  侧边栏折叠
● 首先确认你的侧边栏已经启用  

● 在index.html中插入以下代码
```html
<script>
  window.$docsify = {
    loadSidebar: true,
    alias: {
      '/.*/_sidebar.md': '/_sidebar.md',
    },
    subMaxLevel: 3,
    ...
    sidebarDisplayLevel: 1, // set sidebar display level
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>

<!-- plugins -->
<script src="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/docsify-sidebar-collapse.min.js"></script>
```

● 在index.html的head里选择你喜欢的风格添加链接  
箭头风格：  
```html
  <!-- Sidebar: arrows  -->
  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/sidebar.min.css" />
```  
文件夹风格：  
```html
  <!-- Sidebar: folder   -->
  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/sidebar-folder.min.css" />
```  
● 最终效果  
<div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/folder.png?raw=true" width = "400" />
</div>

### 4  全文搜索框
● 在index.html中script的window.$docsify中加入以下代码：  
``` html
search: {//添加搜索功能，中文和英文文档同时搜索
        paths: 'auto',
        placeholder: {
        '/':'🔍 搜索',
        },},
```  
或者用默认参数也可以：  
``` html
search: 'auto'
```  

● 再引用Docsify搜索插件的代码：
``` html
<script src="//cdn.bootcss.com/docsify/4.5.9/plugins/search.min.js"></script>
```

● 部分网上教程会比上一步多一行如下代码，这是官方文档中的一个bug，这会导致出现两个搜索框，请规避错误  
```html 
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

● 最终得到效果如下  
<div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/search.png?raw=true" width = "400" />
</div>
<br></br>

### 参考
[封面美化方式](https://www.jianshu.com/p/38b6f67c6837)  
[侧边栏折叠](https://github.com/iPeng6/docsify-sidebar-collapse)  
[全文检索方法](http://docsify.tb1043.com/#/?id=全文检索)  
[出现两个搜索框解决办法](https://www.jianshu.com/p/28529ea2303d)
