### 视口viewport：

> 就是浏览器显示页面内部的屏幕区域，视口可以分为三种，布局视口  视觉视口和理想视口

#### 布局视口 layout viewport：

- 一般移动设备的浏览器都默认设置了一个布局视口，用于解决早起的PC端页面在手机上显示的问题
- IOS,Android基本都将这个视口分辨率设置为980px ，所以PC上的网页大多都能在手机上呈现，只不过元素看上去很小，一般默认可以通过手动缩放网页

#### 视觉视口 visual viewport：

- 它是用户正在看到的网站区域  注意：是网站区域
- 我们可以通过缩放去操作视觉视口，但不会影响布局视口，布局视口仍保持原来的宽度

#### 理想视口：ideal viewport

- 为了使网站在移动端有最理想的浏览和阅读宽度而设定
- 对设备来讲，是最理想的视口尺寸
- 需要手动添加meta视口标签通知浏览器操作
- meta视口标签的主要目的：布局视口的宽度应该与理想视口的宽度一致，简单理解就是设备有多宽，我们布局的视口就有多宽

#### meta视口标签：

```html
 <meta name="viewport" content="width=device-width, user-scalable=no,initial-scale=1.0,maximum=1.0,minimum-scale=1.0">
```

| 属性          | 解释说明                                             |
| ------------- | ---------------------------------------------------- |
| width         | 宽度设置的是viewport宽度，可以设置device-width特殊值 |
| initial-scale | 初始缩放比，大于0的数字                              |
| user-scalable | 用户是否可以缩放，yes或者no(1或0)                    |
| maximum-scale | 最大缩放比，大于0的数字                              |
| minimum-scale | 最小缩放比，大于0的数字                              |

标准的viewport设置

- 视口宽度和设备保持一致
- 视口的默认缩放比例1.0
- 不允许用户自行缩放
- 最大允许缩放比例1.0
- 最小允许缩放比例1.0

```html
 <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes"/>
```

### 物理像素

- 物理像素点指的是屏幕显示的最小颗粒，是物理真实存在的，这是厂商在出厂时就设置好的，比如苹果6/7/8是750*1334
- 我们开发的时候1px不是一定等于一个物理像素的
- PC端页面，1个px等于一个1个物理像素，但是移动端就不尽相同
- 一个px的能显示的物理像素点的个数，称为物理像素比或屏幕像素比

### 二倍图

#### 物理像素和物理像素比

- PC端和早期的手机屏幕/普通手机屏幕：1css像素=1物理像素
- Retina(视网膜屏幕) 是一种显示技术，可以将把更多的物理像素压缩至一块屏幕里
- 从而达到更高的分辨率，并提高屏幕显示的细腻程度

#### 多倍图

- 对于一张50px*50px的图片，在手机Retina屏中打开，按照刚才的物理像素比会放大数倍，这样会造成图片模糊
- 在标准的viewport设置中，使用倍图来提高图片质量，解决在高清设备中模糊问题
- 通常使用二倍图，因为iPhone6/7/8的影响，但是现在还存在3倍图4倍图的情况，这个看实际开发公司需求
- 背景图片注意缩放问题

#### 背景缩放 background-size

background-size属性规定背景图像尺寸

```html
background-size:背景图片宽度 背景图片高度
```

- 如果只写一个，那么另一个就会等比例缩放
- 也可以写百分比
- 单位：百分比|长度|cover|contain
- cover把背景图片扩展至足够大，以使背景图像完全覆盖背景区域（可能有背景图片显示不全）
- contain把图像扩展至最大尺寸，以使其宽度和高度完全适应内容区域（高度和宽度等比例拉伸，当宽度或者高度铺满div盒子就不在进行拉伸了，可能有部分空白区域）

#### 二倍精灵图的做法

- 在firework里面把精灵图等比例缩放为原来的一半
- 之后根据大小测量坐标
- 注意代码里面background-size也要写：精灵图原来宽度的一半

### 多背图切图 cutterman 插件

### 移动端开发选择

#### 移动端主流方案

- 单独制作移动端页面（主流）
  - 流式布局（百分比布局）
  - flex弹性布局（强烈推荐）
  - less+rem+媒体查询布局
  - 混合布局
- 响应式页面兼容移动端（其次）
  - 媒体查询
  - bootstarp

#### 移动端浏览器

> 移动端浏览器基本以webkit内核为主，因此我们就考虑webkit兼容性问题
>
> 我们可以放心使用H5标签和css3样式
>
> 同时我们浏览器的私有前缀我们只需要考虑添加webkit即可

#### css初始化 [normalize.css](https://necolas.github.io/normalize.css/) 

#### css3盒子模型 box-sizing

- 传统的模式宽度计算content-box：盒子的宽度=css中设置的width+border+padding
- Css3盒子模型border-box：盒子的宽度=css中设置的宽度 里面包含了border和padding
- 也就是说，我们的css3中的盒子模型，padding和border不会撑大盒子
- 移动端可以全部css3盒子模型
- pc端如果完全需要兼容，我们就用传统模式，如果不考虑兼容性，我们就选择css3盒子模型

特殊样式

```js
//点击高亮我们需要清除  设置为transparent完全透明
-webkit-tap-highlight-color:transparent;

//在移动端浏览器默认的外观在IOS上加上这个属性才能给按钮和输入框自定义样式
-webkit-appearance:none;

//禁用长按页面时弹出菜单
img,a{
    -webkit-touch-callout:none;
}
```

### 流式布局

- 就是百分比布局，也称非固定像素布局
- 通过盒子的宽度设置成百分比来根据屏幕的宽度进行伸缩，不受固定像素的限制，内容向俩侧填充
- 流式布局的方式是移动web开发使用的比较常见的布局方式

常用初始化样式

```js
body {
  width: 100%;
  min-width: 320px;
  max-width: 640px;
  margin: 0 auto;
  background-color: #fff;
  font-size: 14px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  line-height: 1.5;
  color: #666;
}
```

### 图片格式

dpg图片压缩技术

> 京东自主研发推出dpg图片压缩技术，经测试该技术，可直接节省用户近50%的浏览量，
>
> 极大的提升了用户网页打开速度
>
> 能过兼容jpeg，实现全平台，全部浏览器的兼容支持
>
> 经过内部和外部上万张图片的人跟浏览器器测试后发现，压缩后的图片和webp的清晰度对比没有差距

webp图片格式

> 谷歌开发的一种旨在加快图片加载速度的图片格式
>
> 图片的压缩体积大约只有jpeg的2/3
>
> 并能节省大量的服务器宽带资源和数据空间

### flex布局（弹性布局）

- display:flex

  flex（）后面的值也可以写百分比

- 操作方便，布局极为简单，移动端应用范围很广
- PC端浏览器支持情况较差
- IE  11或者更低的版本，不支持或仅部分支持

建议：

- 如果是PC端页面布局，我们还是使用传统布局
- 如果是移动端或者不考虑兼容性问题的PC端页面布局，我们还是使用flex弹性布局

布局原理：

- 用来为盒状模型提供最大的灵活性
- **任何一个容器都可以指定为flex布局**
- 当我们为父盒子设为flex布局以后，子元素的float,clear和vertical-align属性将失效
- 伸缩布局=弹性布局=伸缩盒布局=弹性布局=flex布局

align-content 设置侧轴上的子元素的排列方式（多行）

align-items设置侧轴的排列方式

justify-content设置主轴方向的排列方式

| flex-start    | 头部开始排列                   |
| ------------- | ------------------------------ |
| flex-end      | 尾部开始排列                   |
| center        | 中间显示                       |
| space-around  | 平分剩余空间                   |
| space-between | 先分布在俩头，再平分剩余空间   |
| strech        | 设置子项元素高度平分父元素高度 |

flex-flow是 flex-direction和flex-wrap的复合属性

flex-direction:column|默认row

flex-wrap:wrap|no-wrap

align-self控制子项自己再侧轴上的排列方式（脱离群体）

> 允许单个项目有与其它项目不一样的对齐方式，可覆盖align-items属性
>
> 默认值为auto 表示继承父元素的align-items属性，如果没有父元素，则等同于stretch

order 属性定义项目的排列顺序

> 数值越小，排列越靠前，默认为0
>
> 注意 ：和 z-index不一样

背景色渐变

```css
background:linear-gradient(起始方向，颜色1，颜色2，....)
background:-webkit-linear-grandient(left,red,blue)
background:-webkit-linear-grandient(left top,red,blue)
```

> 背景渐变必须添加浏览器私有前缀
>
> 起始方向可以是：方位名词 或者度数 如果省略默认就是top

### rem布局

- 页面布局文字能否随屏幕大小变化而变化
- 流式布局和flex布局主要针对于宽度布局，那高度如何设置
- 怎样让屏幕发生变化的时候元素高度等比例缩放
- 而rem布局能很好的解决上述问题

#### rem单位

- rem(root em)是一个相对单位，类似于em,em是父元素字体的大小
- 不同的是     rem的基准是相对于html元素的字体大小 而 em是相对于父元素的字体大小来说的
- 但是各个父级元素大小不同，这样就不好设置
- rem的优点是可以通过修改html里面的文字大小来改变页面元素的大小   可以控制整体
- 比如，根元素html设置font-size=12px,非根元素设置width:2rem,则换成px表示就是24px

#### 媒体查询

> 媒体查询是css3的新语法

- 使用@media查询，可以针对不同的媒体类型定义不同的样式
- **@media可以针对不同屏幕尺寸设置不同的样式**
- 当你重置浏览器大小的过程中，页面也会根据浏览器的宽度和高度重新渲染页面
- 目前针对很多苹果手机Android手机，平板等设备都用的多媒体查询

**语法规范**

```js
@media mediatype and|not|only(media feature) {
    css-Code
}
```

- 用@media开头注意@符号
- mediatype媒体查询类型
- 关键字 and not only
- media feature 媒体特性必须要有小括号包含

**mediatype查询类型**

> 将不同的终端设备划分成不同的类型，称为媒体类型

| all   | 用于所有设备                     |
| ----- | -------------------------------- |
| print | 用于打印机和打印预览             |
| scree | 用于电脑屏幕，平板电脑，智能手机 |

关键字

> 关键字将媒体类型或多个媒体特性连接到一起作为媒体查询的条件

- and:可以将多个媒体特性连接到一起，相当于"且"的意思
- not:排除某个媒体类型，相当于“非"的意思，可以省略
- only:指定某个特性的媒体类型，可以省略

**媒体特性**

> 每种媒体类型都具备各自不同的特性，根据不同的媒体类型的媒体特性设置不同的展示风格
>
> 注意他们要加小括号包含

| width     | 定义输出设备中页面可见区域的宽度   |
| --------- | ---------------------------------- |
| min-width | 定义输出设备中页面最小可见区域宽度 |
| max-width | 定义输出设备中页面最大可见区域     |

媒体查询案例：

```js
/* 媒体查询一般按照从大到小  或者从小到大的顺序来 */
  /* 小于540px 页面的背景色变为蓝色 */
  @media screen and (max-width:539px) {
    body {
      background-color: blue;
    }
  }

  /* 540~970我们的颜色改为绿色 */
  /* @media screen and (min-width:540px) and (max-width:969px) {
    body {
      background-color: green;
    }
  } */

  @media screen and (min-width:540px) {
    body {
      background-color: green;
    }
  }

  /* 大于等于970 我们的页面的颜色改为 红色 */
  @media screen and (min-width:970px) {
    body {
      background-color: skyblue;
    }
  }
```

#### 媒体查询+rem实现元素动态大小变化

```js
@media scree and (min-width:320px){
    html{
        font-size:50px
    }
}

@media scree and (min-width:640px)
{
    html{
        font-size:100px
    }
}

.top {
    height:1rem;
    font-size:.5rem;
    color:#fff;
    text-align:1rem;
}
```

#### 引入资源

> 当样式比较繁多的时候，我们可以针对不同的媒体使用不同的stylesheets（样式表）
>
> 原理：就是直接在 link 中判断设备尺寸，然后引入不同的css文件

语法规范：

```html
<link ref="stylesheet" media="mediatype and|not|only (media feature)" href="mystylesheet.css"></link>
```

#### less基础

> 维护css的弊端

> css是一门程序式语言，没有变量、函数、scope(作用域)等概念
>
> - css需要书写大量看似没有逻辑的代码，css冗余度是比较高的
> - 不方便维护及扩展，不利于复用
> - css没有很好地计算能力‘
> - 对非前端开发工程师来讲，往往会因为缺少编写经验而很难写出组织良好且易于维护的css代码项目

less介绍

> 是一门css扩展语言，也成为预处理器
>
> 作为css的一种形式扩展，它并没有减少css功能，而是在现有的css语法上，为css加入程序式语言的特性
>
> 它在css的语法基础上，引入了变量，Mixin（混入）,运算以及函数等功能，大大简化了css编写，并且减低了css的维护成本，就像它的名称所说的那样
>
> less可以让我们用更少的代码做更多的事
>
> 常见的css预处理器
>
> Sass Less Stylus

less变量

> 变量是指没有固定的值，可以改变的，因为我们CSS中的一些颜色和数值等经常使用

```less
@变量名：值
```

变量命名规范

- 必须要有@为前缀
- 不能包含特殊字符
- 不能以数字开头
- 大小写敏感

less编译

> 本质上，less包含一套自定义的语法和一个解析器，用户根据这些语法定义自己的样式规则，这些规则最终会通过解析器，编译生成对应的css问件
>
> 所以，我们需要把我们的less问件，编译生成css文件，这样我们的html页面才能使用

vscode less插件

>  easyless

less[嵌套](https://less.bootcss.com/#%E5%B5%8C%E5%A5%97%EF%BC%88nesting%EF%BC%89)

> 如果遇到（交集|伪类|伪元素选择器）
>
> - 内层选择器的前面没有 &符号，则它被解析为父选择器的后代
> - 如果有&符号，它就被解析为父元素自身或父元素的伪类

rem适配方案原理

> 让一些不能等比自适应的元素，达到设备尺寸发生改变的时候，等比例适配当前设备
>
> 使用媒体查询根据不同设备按比例设置html的字体大小
>
> 然后页面元素使用rem做尺寸单位，当html字体大小变化
>
> 元素尺寸也会发生变化，从而达到等比缩放适配

rem实际开发适配方案

- 按照设计稿与设备的比例，动态计算并设置html根标签的font-size大小:媒体查询
- css中，设计稿元素的宽、高，相对位置等取值，按照同等比例换算为rem为单位的值

技术使用（市场主流）

技术方案1

> - less
> - 媒体查询
> - rem

设计稿常见尺寸

| 设备        | 常见宽度                                                     |
| ----------- | ------------------------------------------------------------ |
| iphone 4  5 | 640px                                                        |
| iphone679   | 750px                                                        |
| Android     | 常见320px、360px、384px、414px、500px、720px （大部分4.7~5寸的安卓设备为720px） |

> 一般情况下，以一套或两套效果图适应大部分的屏幕，放弃极端屏或对其优雅降级、牺牲一些效果，现在基本以750为准

技术方案2

> flexible.js
>
> rem

动态设置html标签font-size大小

- 假设设计稿是750px
- 假设我们把整个屏幕划分为15等分（这里的划分标准不一  可以是20份也可以是10等份）
- 每一份作为html字体大小。这里就是50px
- 那么在320px设备时，字体大小为320/15就是21.33px
- 用我们页面元素的大小除以不同的html字体大小会发现他们比例还是相同的
- 比如我么以750为标准设计稿
- 一个100*100像素的页面元素澡750屏幕下，就是100/50转换为rem是2rem  *  2rem比例是1比1
- 320屏幕下，html字体大小为21.33则 2rem=42.66px 此时宽度和高都是42.66 但是宽和高的比例还是1比1
- 320屏幕下，html字体大小为21.33 则2rem=42.66px 此时宽和高都是42.66 但是宽和高的比例还是1比1
- 但是已经能实现不同屏幕下 页面元素盒子等比例缩放

> 总结：大小变了，但比例没变

元素大小取值方法：

- 最后的公式：页面元素的rem=页面元素值（px）/ (屏幕宽度/划分的份数)
- 屏幕宽度/划分的份数 就是html font-size的大小
- 或者：页面元素的rem值=页面元素值（px）/ html font-size 字体大小

简洁高效的rem适配方案flexible.js

> 手机淘宝团队出的简洁高效移动端适配库
>
> 我们再也不需要写不同的媒体查询，因为里面的js做了处理
>
> 它的原理是把当前设备划分为10等份，但是不同 设备下，比例还是一致的
>
> 我们要做的就是确定好我们当前设备的html文字大小就可以了
>
> 比如当前设计稿是750px 那么我们只要把html文字大小设置为750px/10就可以
>
> 里面的元素rem值：页面元素的px值 / 75
>
> 剩余的,让flexible.js来算

总结：

> 俩种方案现在都存在
>
> 方案2更简单

苏宁易购首页案例：

设置公共common.less文件

- 新建common.less 设置好最常见的屏幕尺寸，利用媒体查询设置不同的html字体大小，因为除了首页其它页面也需要
- 我们关心的尺寸有320px、360px、375px、384px、400px、414px、424px、480px、540px、720px、750px
- 划分的份数我们定为15等份
- 因为我们PC端也可以打开苏宁易购首页，我们默认html字体大小为50px ,注意这句话写到最上面

import导入样式

@import "common"

> @import 导入的意思 可以把一个样式文件导入到另一个样式文件里面
>
> link 是把一个样式文件引入到html中

```js
body {
  min-width: 320px;
  width: 15rem;
  margin: 0 auto;
  line-height: 1.5;
  font-family: Arial, Helvetica;
  background-color: #f2f2f2;
}
```



方案2：

flexible.js

```js
(function flexible (window, document) {
  var docEl = document.documentElement
  var dpr = window.devicePixelRatio || 1

  // adjust body font size
  function setBodyFontSize () {
    if (document.body) {
      document.body.style.fontSize = (12 * dpr) + 'px'
    }
    else {
      document.addEventListener('DOMContentLoaded', setBodyFontSize)
    }
  }
  setBodyFontSize();

  // set 1rem = viewWidth / 10
  function setRemUnit () {
    var rem = docEl.clientWidth / 10
    docEl.style.fontSize = rem + 'px'
  }

  setRemUnit()

  // reset rem unit on page resize
  window.addEventListener('resize', setRemUnit)
  window.addEventListener('pageshow', function (e) {
    if (e.persisted) {
      setRemUnit()
    }
  })

  // detect 0.5px supports
  if (dpr >= 2) {
    var fakeBody = document.createElement('body')
    var testElement = document.createElement('div')
    testElement.style.border = '.5px solid transparent'
    fakeBody.appendChild(testElement)
    docEl.appendChild(fakeBody)
    if (testElement.offsetHeight === 1) {
      docEl.classList.add('hairlines')
    }
    docEl.removeChild(fakeBody)
  }
}(window, document))

```

设置视口标签以及引入初始化样式还有js文件

```html
 <meta name="viewport"
    content="width=device-width, initial-scale=1.0 ,user-scalable=no,maximum-scale=1.0,minimum-scale=1.0">
  <title>Document</title>
  <link rel="stylesheet" href="./css/normalize.css">
  <link rel="stylesheet" href="./css/index.css">
  <script src="./js/flexible.js"></script>
```

#### Vscode px 装换rem插件 cssrem

> 注意：这个插件默认的html文字大小cssroot 16px
>
> 需要根据设计稿手动修改默认html文字大小
>
> 找到setting.json 修改 root font size

![image-20210805154650069](D:\笔记\HTML5 CSS5基础知识\移动端开发.assets\image-20210805154650069.png)

### 移动web响应式布局   [Bootstrap](https://v3.bootcss.com/)

响应式开发原理

> 就是使用媒体查询（@media scree and （））针对不同的设备进行布局和样式设置
>
> ```html
>  <style>
>         .container {
>             height: 150px;
>             background-color: pink;
>             margin: 0 auto;
>         }
>         /* 1. 超小屏幕下  小于 768  布局容器的宽度为 100% */
>         
>         @media screen and (max-width: 767px) {
>             .container {
>                 width: 100%;
>             }
>         }
>         /* 2. 小屏幕下  大于等于768  布局容器改为 750px */
>         
>         @media screen and (min-width: 768px) {
>             .container {
>                 width: 750px;
>             }
>         }
>         /* 3. 中等屏幕下 大于等于 992px   布局容器修改为 970px */
>         
>         @media screen and (min-width: 992px) {
>             .container {
>                 width: 970px;
>             }
>         }
>         /* 4. 大屏幕下 大于等于1200 布局容器修改为 1170 */
>         
>         @media screen and (min-width: 1200px) {
>             .container {
>                 width: 1170px;
>             }
>         }
>     </style>
> </head>
> 
> <body>
>     <!-- 响应式开发里面，首先需要一个布局容器 -->
>     <div class="container"></div>
> </body>
> ```

| 设备划分                 | 尺寸区间        | 常见响应式尺寸划分 |
| ------------------------ | --------------- | ------------------ |
| 超小屏幕（手机）         | <768px          | 设置宽度为100%     |
| 小设备（平板）           | >=992px~<992px  | 设置宽度为750px    |
| 中等屏幕（桌面显示器）   | >=992px~<1200px | 宽度设置为970px    |
| 宽屏设备（大桌面显示器） | >=1200px        | 宽度设置为1170px   |

响应式布局容器

> 响应式需要一个父级作为布局容器，来配合子级元素来实现变化效果
>
> 原理就是在不同的屏幕下，通过媒体查询来改变这个布局容器的大小，再改变里面子元素的排列方式和大小，从而实现不同屏幕下，看到不同页面布局和样式变化

### Bootstrap前端开发框架

> Bootstrap来自Twitter（tuite），是目前最受欢迎的前端框架。
>
> 基于HTML、CSS和JAVASCRIPT
>
> 简洁灵活，使得Web开发更高效
>
> 使用框架固然好，但是后期维护就不太友好啦，还是要注重原理实现

优点：

- 标准化的html+css编码规范
- 提供了一套简洁、直观、强悍的组件
- 有自己的生态圈，不断的更新迭代
- 让开发更简单，提高了开发效率

版本：

- 2.x.x：停止维护，兼容性好，代码不够简洁，功能不够完善
- 3.x.x：目前使用最多，稳定，但是放弃了IE6~IE7支持，但是界面效果不好，偏向于开发响应式布局、移动设备优先的WEB项目
- 4.x.x：最新版，目前还不是很流行

使用：

> 控制权在框架本身，使用者按照框架规定的某种规范进行开发

- 创建文件夹结构
- 创建html骨架结构
- 引入相关样式文件
- 书写内容

布局容器

> bootstrap需要为页面内容和栅格系统包裹一个.container容器，bootstarp预先定义好了这个类，叫.container
>
> 它提供了两个做此用处的类

[栅格系统](https://v3.bootcss.com/css/#grid)

> 栅格系统英文为"gridsystem",也有人翻译为"网格系统，它是指将页面布局划分为等宽的列，然后通过列数的定义来模块化布局"
>
> bootstrap提供了一套响应式、移动设备优先的流式栅格系统，随着屏幕或视口尺寸的增加，系统会自动分为最多12列
>
> bootstrap里面的container宽度是固定的，但是不同屏幕下，container的宽度不同，我们再把container划分为12等份

| 超小屏幕 手机 (<768px) | 小屏幕 平板 (≥768px)       | 中等屏幕 桌面显示器 (≥992px)                        | 大屏幕 大桌面显示器 (≥1200px) |            |
| :--------------------- | :------------------------- | :-------------------------------------------------- | :---------------------------- | ---------- |
| 栅格系统行为           | 总是水平排列               | 开始是堆叠在一起的，当大于这些阈值时将变为水平排列C |                               |            |
| `.container` 最大宽度  | None （自动）              | 750px                                               | 970px                         | 1170px     |
| **类前缀**             | `.col-xs-`                 | `.col-sm-`                                          | `.col-md-`                    | `.col-lg-` |
| 列（column）数         | 12                         |                                                     |                               |            |
| 最大列（column）宽     | 自动                       | ~62px                                               | ~81px                         | ~97px      |
| 槽（gutter）宽         | 30px （每列左右均有 15px） |                                                     |                               |            |
| 可嵌套                 | 是                         |                                                     |                               |            |
| 偏移（Offsets）        | 是                         |                                                     |                               |            |
| 列排序                 | 是                         |                                                     |                               |            |

- 按照不同屏幕划分为1~12等份
- 行（row）可以去除父容器左右15px的边距
- xs-extra small：超小；sm-small:小；md-medium:中等；lg-large:大
- 可以同时为一列指定多个设备类名，以便划分不同的份数  例如：class="col-md-4  col-sm-6"

列嵌套

> 为了使用内置的栅格系统将内容再次嵌套，可以通过添加一个新的 `.row` 元素和一系列 `.col-sm-*` 元素到已经存在的 `.col-sm-*` 元素内。被嵌套的行（row）所包含的列（column）的个数不能超过12（其实，没有要求你必须占满12列）。

响应式工具

> 为了加快对移动设备友好的页面开发工作，利用媒体查询功能，并使用这些工具类可以方便针对不同设备，展示或隐藏页面内容

| 类名       | 超小屏 | 小屏 | 中屏 | 大屏 |
| ---------- | ------ | ---- | ---- | ---- |
| .hidden-xs | 隐藏   | 可见 | 可见 | 可见 |
| .hidden-sm | 可见   | 隐藏 | 可见 | 可见 |
| .hidden-md | 可见   | 可见 | 隐藏 | 可见 |
| .hidden-lg | 可见   | 可见 | 可见 | 隐藏 |

> 与之相反的，是visible-xs visible-sm visible-lg是显示某个页面内容



阿里百秀首页案例：

需求分析

> 屏幕划分分析
>
> - 屏幕缩放发现，中屏幕和大屏幕时一致的，因此我们列 定义为col-md-就可以了，md是大于等于970以上的
> - 小屏幕的布局发生变化，因此我们需要为小屏幕根据需求改变布局
> - 超小屏幕又发生变化，因此我们需要为超小屏幕根据需求改变布局
> - 策略：我们先布局md以上的pc端布局，最后根据实际需求修改小屏幕和超小屏幕的特殊布局样式


