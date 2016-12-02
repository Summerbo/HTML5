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

### 多媒体

## webstorage 
存储数据的两种方式;
- window.localStorage.键名
- window.localStorage.setItem(键名,键值)
获取存储数据的两种方式：
- window.localStorage.键名
- window.localStorage.getItem(键名)
这里第一种方式是利用对象来操作的，第二种是h5提供的方法