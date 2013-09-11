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

