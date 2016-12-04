# HTML5笔记

## 语义化标签

### 常用语义化标签
- header     头部区域
- nav        导航区域
- section    区块
- article    文字区域
- aside      侧边栏区域
- footer     页脚
- time       事件标签，时间不明确时可以使用datetime属性指明具体时间
- figure     流媒体区域，用于包括图片、视频、音频等多媒体
- figcaption 流媒体区域的标题
- mark       用荧光笔的效果来强调
- progress   精度条标签，属性有min最小值，max最大值，value当前值
- meter      计量标签，属性有min最小值，max最大值，value当前值，low低值，high高值

### 兼容性处理
兼容性处理主要是针对IE浏览器而言。
- 使用IE提供的hack处理，在文档加载之前添加一下代码：
~~~
<!--[if lte IE 8]>
<script>
    document.createElement('header');
    document.createElement('nav');
    document.createElement('section');
    document.createElement('aside');
    document.createElement('article');
    document.createElement('footer');
</script>
<![endif]-->
~~~
- 通常开发中都会使用第三方开发库来处理，比如：
~~~
<!--[if lte IE 8]>
<script src="../lib/html5shiv/html5shiv.js"></script>
<script src="../lib/respond/respond.min.js"></script>
<![endif]-->
~~~

## 表单

### 新增表单元素类型：
新增表单元素类型主要针对于input输入框的type属性的值，部分表单类型只针对移动设备起作用，使用时注意兼容性。
- email  邮件类型
- color  拾色器
- url    网址
- number 数字类型
- range  在某个取值范围内，属性min取值的最小值，max取值的最大值，value当前值
- search 搜索框
- tel    电话号码，目前大部分都不支持
- date   日期类型，若要兼容性好可以使用第三方库文件
- time   时间类型
- datetime 时间日期类型
- week   选择周
- month  选择月
- datetime-local 本地的时间日期

### 新增表单元素
- datalist 数据列表标签，默认是隐藏在页面中，为其他元素所用，在目标元素上使用list属性，并且属性的值必须是datalist的id值
~~~
<input type="text" list='cities'>
<datalist id='cities'>
    <option value="">北京</option>
    <option value="">上海</option>
    <option value="">广州</option>
</datalist>
~~~
- output 用于呈现计算的结果
- optgroup 对下拉列表项进行分组
~~~
<select name="" id="">
    <optgroup label="一线城市">
        <option value="">北京</option>
        <option value="">上海</option>
    </optgroup>
        <option value="">武汉</option>
</select>
~~~

### 新增表单属性
- autofocus   自动获取焦点
- required    必填项
- autocomplete 自动完成，其值为on时表示开启，默认为off时表示关闭，可以给单个表单元素设置也可以给整个表单域设置
- placeholder 占位符
- pattern     正则表达式匹配
- mutiple     多个项，可作用于下拉菜单，邮箱，文件上传
- form        将表单域外的元素添加到表单域内

### 新的表单事件
- invalid     表单元素验证不通过时触发
- input       当文本域或者文本框中输入内容时触发，一输入就会触发该事件
input与change的区别;
- input只要输入内容就会发生变化，change表示当元素发生改变时，失去焦点时触发
- input的事件源只能是文本框或者文本域，change的事件源就更为广泛
- input的兼容性没有change好，IE9及以上才支持input事件

## 多媒体
- video 视频，常见属性，width宽度，height高度，controls显示控制面板，poster="对应封面的资源地址"显示封面，loop循环播放，preload预加载，autoplay自动播放，由于版权限制所有没有一种格式是所有浏览器都支持的，所以通常要做到兼容需要由sourse标签来完成：
~~~
<video controls loop preload autoplay>
    <source src="test.mp4"></source>
    <source src="test.webm"></source>
    你的浏览器不支持
</video>
~~~
视频的控制中还有一些属性：
- paused 是否暂停
- currentTime 视频播放的当前位置（秒数）
- duration 视频的长度（秒数）
- playbackRate 视频播放速度或者速率，1表示正常速度
- muted 是否静音
- volume 视频音量 0-1范围内
- play() 播放视频
- pause() 暂停

案例：<a href="视频控制.html">视频控制</a>

- audio 音频，属性和用法和video差不多，只是少了一个poster属性其他的一模一样
~~~
<audio controls loop preload autoplay muted>
    <source src="test.mp3"></source>
    <source src="test.ogg"></source>
    你的浏览器不支持
</audio>
~~~

## DOM

### 获取元素
- document.getElementsByClassName('类名') 通过类名获取元素，获得的元素为匹配结果的所有元素即数组
- document.querySelector('CSS选择器')   通过css选择器来获取元素，获得元素为匹配结果的第一个元素
- document.querySelectorAll('CSS选择器')   通过css选择器来获取元素，获得元素为匹配结果的所有元素

### 类名操作
- el.classList.add('类名') 添加某各类
- el.classList.remove('类名') 删除某个类
- el.classList.toggle('类名') 切换某个类
- el.classList.contains('类名') 判断是否存在某个类

案例：<a href="类名操作.html">类名操作</a>

### 自定义属性
HTML5中允许自定义属性，但属性必须以data-开头，访问时时通过dataset.属性名访问，注意如果data后面有多个以-连接的话获取时要用驼峰式命名法
~~~
<img src="test.png" data-big-img="btest.png" alt="">
<script>
    var img = document.querySelector('img');
    img.onclick = function(){
        this.src = img.dataset.bigImg;
    }
</script>
~~~

## 新增API

### 拖拽
- draggable  使元素具备可拖拽可将其值设为true，作用于被拖拽元素上
#### 拖拽事件
作用于拖拽元素身上的事件：
- dragstart  拖拽开始触发
- drag   被拖拽中
- dragend 拖拽结束即松开鼠标时
作用于目标元素身上的事件：
- dragenter 进入目标元素范围内
- dragleave 拖出目标元素范围内
- dragover  在目标元素上拖拽时，默认是禁止将拖拽元素放置到其他元素上，如想允许必须阻止默认事件
- drop  在目标元素上松开鼠标时
#### 拖拽中数据传递
拖拽中的数据传递是通过事件对象中dataTransfer.setData()和dataTransfer.getData()来进行的

案例：<a href="h5新标签.html">拖拽</a>

### 地理定位
地理定位中主要通过Geolocation api来实现
- navigator.geolocation.getCurrentPositon(successCallback,errorCallback,options)  获取地理位置
- navigator.geolocation.watchPosition() 重复获取地理位置
获取地理位置的三个参数分别是获取成功后的回调函数，出错时的回调函数，设置选项
options中通常有三个值：enableHighAccuracy是否高精度访问通常为false，timeout过期时长单位为毫秒，maximumAge重复获取地理信息的时间间隔只对watchPosition有效
ps：大陆可能chrome浏览器不能使用定位

案例：<a href="在百度地图显示当前位置.html">定位</a>

### webstorage 

#### localstorage
本地存储永久有效，除非手动删除，可以在多个窗口之间进行数据共享
存储数据的两种方式;
- window.localStorage.键名
- window.localStorage.setItem(键名,键值)
获取存储数据的两种方式：
- window.localStorage.键名
- window.localStorage.getItem(键名)
这里第一种方式是利用对象来操作的，第二种是h5提供的方法

#### sessionstroage
会话存储：方法和用法同上，关闭窗口即失效，只能统一窗口共享数据

案例：<a href="web存储.html">存储</a>


### 网络状态
- navigator.onLine 判断网络状态
html5中提供两个事件来判断网络上线或者掉线，两个事件的事件源都是window
- offline 网络掉线触发
- online  网络上线触发

### 应用程序缓存
通常都是在新建一个以.appcache为后缀名的缓存清单，清单内容如下：
~~~
CACHE MANIFEST

# 需要缓存的文件
CACHE:
images/5_129368073560000000_0475.jpg
images/5_129626322580000000_7066.jpg
css.css

# 需要联网访问的资源
NETWORK:
js.js

# 文件出错时将出错文件替换为后面资源
FALLBACK:
images/  images/logo.png
~~~
然后在html文件中添加上要缓存的文件地址，如下：
~~~
<!DOCTYPE html>
<html lang="en" manifest="demo.appcache">
    <head>
        <meta charset="utf-8">
        <title>web应用缓存</title>
        <link rel="stylesheet" href="css.css">
        <script src="js.js"></script>
    </head>
    <body>
    	有一种老师叫做别人的老师！<br><br>
    	<img src="images/5_129368073560000000_0475.jpg" alt="">
    	<img src="images/5_129626322580000000_7066.jpg" alt="">
    	<img src="1.jpg" alt="">
    </body>
</html>
~~~