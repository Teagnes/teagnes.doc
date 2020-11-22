# 使用docsify 搭建在线文档



使用docsify来搭建在线文档，优势在于无需编译，可以集成github

- **安装docsify**
- **新建dmeo项目**
- **修改默认页面**
- **自定义侧边栏**
- **第一篇文档**
- **搜索**
- **nginx部署**



>  [官方文档](https://docsify.js.org/#/)

>  [中文文档](https://docsify.js.org/#/zh-cn/)



###  安装docsify

- 安装node和npm

- 安装docsify

```shell
npm i docsify-cli -g
```



### 新建demo项目

- 新建

如下命令新建项目

```
docsify init docsDemo
```

执行完成后会生成**.nojekyll** ，**index.html**, **README.md**  文件

- 启动

使用如下命令启动，即可在本地浏览器中查看默认的页面

```
docsify serve docsDemo
```



### 修改默认页面

默认会将生成文件中的 **README.md** 作为默认页面，修改一下启动的内容如下，在浏览器上查看效果



### 添加封面

修改`index.html`增加如下配置

```
  <script>
    window.$docsify = {
    ...
      coverpage: true
  	...

    }
```



在项目根目录下新建`_coverpage.md` 文件,添加如下内容

```
![logo](https://docsify.js.org/_media/icon.svg)

 

> Teagens 的在线文档.


[GitHub](https://github.com/Teagnes/teagnes.doc.git)
[Get Started](README.md)
```







### 自定义侧边栏

修改`index.html` 增加 `loadSidebar: true`

```
  <script>
    window.$docsify = {
      loadSidebar: true
    }
  </script>
```

在项目根目录下新建`_sidebar.md` 文件，

```
* [首页](README.md)
* 一级标题
  * 二级标题
    * 三级标题
```

在根目录下新家文件夹`zh-cn`，所有的文档都会保存在这里，根目录下不保存文档，根目录下保存侧边栏文件等

### 添加第一篇文档

最后套娃一下，用这篇文档作为第一篇文档，文档名`docsifyDemo.md` ，路径`./zh-cn/docsifyDemo.md`

修改`_sidebar.md`文件

```
* [首页](README.md)
* [使用docsify 搭建在线文档](zh-cn/docsifyDemo.md)
  * 二级标题
    * 三级标题
```



### 搜索

在`index.html` 文件中 增加如下配置

```html
search: {
        paths: 'auto',
        placeholder: '搜索',
        noData: '找不到结果',
        depth: 3,
      },

<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>
```





```
<body>
  
  <div id="app"></div>
  <script>
    window.$docsify = {
      loadSidebar: true,
      name: '',
      repo: '',
      search: {
        paths: 'auto',
        placeholder: '搜索',
        noData: '找不到结果',
        depth: 3,
      },

    }
  </script>
  <!-- Docsify v4 -->
  <script src="//cdn.jsdelivr.net/npm/docsify@4"></script>
  <script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>

</body>
```





### nginx部署

nginx部署比较简单，指定项目的根目录即可

` root   E:\\teagnes.doc;`

```
    server {
        listen       8088;
        server_name  localhost;
        #root web/; 
		#root html/; 
        #index index.html;

        location / {
            root   E:\\teagnes.doc;
            index  index.html index.htm;
        }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }

    }
```











