html5--app
==========

轻量级的html5响应式框架和移动app框架实例

###  lungo.js 
一个使用 HTML5/CSS3 和 JavaScript 技术的移动 Web 开发框架。
http://lungo.tapquo.com/


结构
---------
主页面引用
``` html 
<link rel="stylesheet" href="components/lungo.brownie/lungo.css">
<link rel="stylesheet" href="components/lungo.icon/lungo.icon.css">
<link rel="stylesheet" href="components/lungo.brownie/lungo.theme.css">
<script src="components/quojs/quo.js"></script>
<script src="components/lungo/lungo.js"></script>
``` 
section 单个页面的ui容器
``` html
<section id="main">
	<article id="main-article">   
		Your content
	</article>
</section>
```

### 使用js加载
``` javascript
//Load resource on app init
Lungo.init({
	name: 'example',
	resources: ['section_to_load.html']
});
```

### 使用link加载
``` html
<section id="loader" data-transition="">
	<article id="art1" class="active">
		<a href="#main" data-router="section" data-async="section_to_load.html">
			Go to section
		</a>
	</article>
</section>
```

### 使用 data-view-section 跳转页面
``` html
<section id="mian" data-transition="">
	<article id="art1" class="active">
		<a href="#" data-view-setion="load" data-router="section" data-async="section_to_load.html">
			Go to load
		</a>
	</article>
</section>

<section id="load" data-transition="">
	<article id="loader">
		Your loader
	</article>
</section>
```

### 返回按钮 
使用data-view-*属性跳转页面不记录在浏览器后退栈中,浏览器默认后退无用
在header中使用 data-back
``` html
<header data-back="home"></header>
```
在`<a>`或者`<button>`中使用  data-view-section="back" 或者  href="#back"
``` html
<button data-view-section="back" data-label="Return to previous section"></button>
<a href="#back"  data-view-section="back"> Back to section </a> 
```


主要元素
---------
### Section & Article
一个Section表示可表示一个完整的ui，其中可包括`<article>`、`<header>`、`<footer>`等元素。
如果需要制定当前活动页，可使用`class="active"`
``` html
<section id="main_section">
    <header data-title="example"></header>
    <article id="main-article" class="active">
        {{CONTENT}}
    </article>
</section>
````

### Header
``` html
<section id="main_section">
    <header data-title="example"></header>
    <article id="main-article" class="active">
        {{CONTENT}}
    </article>
</section>
```
header中可以添加导航按钮, 使用`class="on-right"`或者`class="on-left"`可以指定按钮位置
``` html  
<header data-title="Your header" class="extended">
    <nav class="on-right">
       <a href="#" data-icon="menu" class="active"></a>
       <a href="#" data-icon="share"></a>
       <a href="#" data-icon="user"></a>
       <button data-view-aside="features" data-icon="forward"></button>
   </nav>
</header>
```

### Footer
``` html
<section id="main_section">
    <article id="main" class="active">
        {{CONTENT}}
    </article>
    <footer>
        <nav>
            <a href="#" data-icon="menu" class="active"></a>
            <a href="#" data-icon="share"></a>
            <a href="#" data-icon="user"></a>
            <a href="#" data-icon="users"></a>
        </nav>
    </footer>
</section>
```

### Aside
侧边栏的UI模板  
``` html
<aside id="features">
    <header data-title="Options"></header>
    <article class="active">
        {{CONTENT}}
    </article>
</aside>
```
UI模板生成以后需要将aside链接到主页面中  
用`data-aside="features"`指定启用aside的id，使用`data-view-aside`指定点击按钮显示或隐藏的aside  
``` html
<section id="main_section" data-aside="features">
    <header data-title="Aside">
        <nav>
            <button data-view-aside="features" data-icon="menu"></button>
        </nav>
    </header>
    <article id="main-article" class="active indented">
        {{CONTENT}}
    </article>
</section>
```


导航
----------

### Data-View 
使用 `data-view-*`进行页面跳转，需要指定被跳转页面为`<section>`、`<article>`还是`<aside>`  
``` html
<section id="main">
    <article id="article_1" class="active">
        <button class="button" data-view-article="article_2" data-icon="forward">To article_2</button>
    </article>
    <article id="article_2">
        <button class="button" data-view-article="article_1" data-icon="home" data-label="To article_1"></button>
    </article>
</section>
```
### Groupbar
页面中的分类导航使用`data-control="groupbar"`，如果作为header导航的推展，需要在`<header>`中添加`class="extended"`  
``` html
<section id="main">
    <header data-title="groupbar" class="extended"></header>
    <nav data-control="groupbar">
        <a href="#" data-view-article="article_1" class="active">Art-1</a>
        <a href="#" data-view-article="article_2">Art-2</a>
    </nav>
    <article id="article_1" class="active">{{CONTENT}}</article>
    <article id="article_2">{{OTHER_CONTENT}}</article>
</section>
```

### Menu
弹出下拉菜单，使用`data-control="menu"`来指定nav的样式为menu，使用`data-view-menu="id"`来指定按钮弹出下拉菜单  
```html
<section id="menu" data-transition="slide">
    <header data-title="data-control=menu">
        <nav>
            <a href="#" data-view-menu="options" data-icon="menu"></a>
        </nav>
    </header>  
    <nav id="options" data-control="menu">
        <a href="#" data-view-article="home-menu" data-icon="menu">Home</a>
        <a href="#" data-view-article="explore-menu" data-icon="globe">Explore</a>
        <a href="#" data-view-article="activity-menu" data-icon="comments">Activity</a>
        <a href="#" data-view-article="profile-menu" data-icon="user">Profile</a>
    </nav>
</section>
```

数据绑定
--------
### Data-title
指定title ` data-title="Default title"`
```html
<header data-title="Title of section">
</header>
```
### Data-label
指定内容  `data-label="Default label"`
```html
<button class="button" data-view-article="article_1" data-icon="home" data-label="To article_1"></button>
```

JavaScript API
==============


Core
----
#### log()
调试打印信息,其中 (1)Log, (2)Warn, (>2)Error  
*Example*
``` javascipt
Lungo.Core.log(1, "Launched event");
Lungo.Core.log(2, "Warning!!");
Lungo.Core.log(3, "Error!!!!");
```

#### execute()
顺序执行指定回调方法

*Example*
``` javascript
var myFunc = function(){
    //Do something
};
var myFunc2 = function(){
    //Do something
};
Lungo.Core.execute(myFunc, myFunc2);
```

#### isMobile()
**Returns** 检测是否为移动设备
*Example*
``` javascript
Lungo.Core.isMobile();
//Result:false
```
#### environment()
**Returns**  当前环境
*Example*
``` javascript
Lungo.Core.environment();
//Result: "Object {browser: "WebKit/537.36", os: null, isMobile: false, screen: Object}"
```

Cache
-----
lungo 提供类似于session的缓存机制,
#### set()
使用key/value形式存储缓存

**Parameters**
```
string:     Key for the new value.
string:     [OPTIONAL] Subkey in LungoJS Cache System.
object:     Value asigned to the key.
```

*Example*
``` javascript
var framework = {name: "Lungo", twitter: "lungojs"};
Lungo.Cache.set("lungoFramework", framework);
```
#### get()
Returns the cached value of a given key.

**Parameters**
```
string:      Key in LungoJS Cache System.
string:     [OPTIONAL] Subkey in LungoJS Cache System.
```
This method **return** an object containing the value.

*Example*
``` javascript
var cachedFramework = Lungo.Cache.get("lungoFramework");
//Result: {name: "Lungo", twitter: "lungojs"}
```


#### remove()
Removes the instance of a given key in LungoJs Cache System.

**Parameters**
```
string:     Key in LungoJS Cache System.
string:     [OPTIONAL] Subkey in LungoJS Cache System.
```

*Example*
``` javascript
Lungo.Cache.remove("lungoFramework");
```


#### exists()
Checks if the given key is stored in the cache.

**Parameters**
```
string Key in LungoJS Cache System.
```
This method **return** a boolean value which is true if the key is found

*Example*
``` javascript
Lungo.Cache.exists("lungoFramework");
```
