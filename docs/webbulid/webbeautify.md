# Web Page Beautification

### 1  The cover
● Start by setting the coverpage property to true in index.html

● Create a new file: _coverpage.md  

● The cover is shown below.  <br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/cover1.png?raw=true" width = "1000" div align= 'center' /><br><br/>

### 2  Web page icon
● Add the following code to the head section of index.html <br><br/>

```html
  <link rel="icon" type="image/png" href="https://github.com/Fy1307/IMGofSixGod/
  blob/master/img/Favicon.png?raw=true" >
```

● The icon is shown below.  <br><br/>
<img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/Icon.png?raw=true" width = "1000" div align= 'center' /><br><br/>

### 3  Sidebar fold function
● First make sure your sidebar is enabled  

● Insert the following code into index.html
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

● Add the link in the style you like in index.html head 
Arrow style：  
```html
  <!-- Sidebar: arrows  -->
  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/sidebar.min.css" />
```  
Folder Style：  
```html
  <!-- Sidebar: folder   -->
  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify-sidebar-collapse/dist/sidebar-folder.min.css" />
```  
●  Final result
<div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/folder.png?raw=true" width = "400" />
</div>

### 4  Full text search box
● Add the following code to the script window.$docsify in index.html: 
``` html
search: {//Add a search function to search Chinese and English documents simultaneously
        paths: 'auto',
        placeholder: {
        '/':'🔍 Search',
        },},
```  
Or you can use the default parameters: 
``` html
search: 'auto'
```  

● Code that references the Docsify search plug-in:
``` html
<script src="//cdn.bootcss.com/docsify/4.5.9/plugins/search.min.js"></script>
```

● Some online tutorials will add the following line of code than the previous step. This is a bug in the official documentation, which will cause two search boxes to appear. Please avoid the error.
```html 
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

● The final results are as follows 
<div align= 'left'>
    <img src="https://github.com/Fy1307/IMGofSixGod/blob/master/img/search_.png?raw=true" width = "400" />
</div>
<br></br>

### Reference
[Cover beautification](https://www.jianshu.com/p/38b6f67c6837)  
[Sidebar folding function](https://github.com/iPeng6/docsify-sidebar-collapse)  
[Full-text search methods](http://docsify.tb1043.com/#/?id=全文检索)  
[Solution for two search boxes](https://www.jianshu.com/p/28529ea2303d)
