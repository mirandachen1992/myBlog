---
layout: post
title:  "《编写高质量代码》（一）HTML、CSS 部分"
date:   2015-08-29
categories: HTML CSS
---


##开始说几句
最近在看《编写高质量代码--Web前端开发修炼之道》(曹刘阳 著)，内容有点老了，但是中间有部分内容是我平时没有注意到或者没有深入理解的，所以用这两篇先总结一下个人觉得平时用的比较多又比较容易出错的部分。Smile ^_^~

---

###（一）CSS的命名

css的命名一般有两种方式驼峰式timeList和划线式time-list/time_List。书中作者认为比较好的方法是：驼峰命名法用于区别不同单词，划线用于表明从属关系。如：


    <ul class="timeList">
      <li class="timeList-firstItem"></li>
      <li class="timeList-secondItem"></li>
      <li class="timeLIst-LastItem"></li>
    </ul>

###（二）挂多个class还是新建class -- 多用组合，少用继承

加入我们想得到下图

![2015-8-29(1)]({{"/css/pics/2015-8-29(1).PNG"}})

**方案一**：分别视为三种不同的类，代码冗余

    <style>
      .numberList1{border:1px solid #ccc; padding: 10px; list-style-type: none;}
      .numberList1 li{height: 20px; line-height: 20px; font-size: 12px;}
      .numberList2{border:1px solid #ccc; padding: 10px; list-style-type: none;}
      .numberList2 li{height: 20px; line-height: 20px; font-size: 16px;}
      .numberList3{border:1px solid #ccc; padding: 10px; list-style-type: none;}
      .numberList3 li{height: 20px; line-height: 20px; font-size: 12px; color: red;}
    </style>
    <body>
      <ul class="numberList1">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
      <ul class="numberList2">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
      <ul class="numberList3">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
    </body>

**方案二**：与方案一的思路相同，只是想样式相同的部分提取出来

    <style>
      .numberList1,.numberList2,.numberList3{border:1px solid #ccc; padding: 10px; list-style-type: none;}
      .numberList1 li,.numberList2 li,.numberList3 li{height: 20px; line-height: 20px; font-size: 12px;}
      .numberList2 li{font-size: 16px;}
      .numberList3 li{font-size: 12px; color: red;}
    </style>
    <body>
      <ul class="numberList1">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
      <ul class="numberList2">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
      <ul class="numberList3">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
    </body>

**方案三**:提取出更多粒度更小的类，通过类的组合实现

    <style>
      .numberList{border:1px solid #ccc; padding: 10px; list-style-type: none;}
      .numberList li{height: 20px; line-height: 20px}
      .f16{font-size: 16px;}
      .f12{font-size: 12px;}
      .red{color: red;}
    </style>
    <body>
      <ul class="numberList f12">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
      <ul class="numberList f16">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
      <ul class="numberList f12 red">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
    </body>

总的来说，方案二和三都不错，方案二调用简单，方案三代码精简。但是如果我们有添加一个numberList4的话，情况会发生什么改变呢？

对于方案二：

    <style>
      .numberList{border:1px solid #ccc; padding: 10px; list-style-type: none;}
      .numberList li{height: 20px; line-height: 20px}
      .f16{font-size: 16px;}
      .f12{font-size: 12px;}
      .red{color: red;}
    </style>
    <body>
      <ul class="numberList ">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
      <ul class="numberList2">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
      <ul class="numberList3">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
      <ul class="numberList4">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
    </body>

对于方案三：

    <style>
      .numberList1,.numberList2,.numberList3,.numberList4{border:1px solid #ccc; padding: 10px; list-style-type: none;}
      .numberList1 li,.numberList2 li,.numberList3 li,.numberList4 li{height: 20px; line-height: 20px; font-size: 12px;}
      .numberList2 li,.numberList4 li{font-size: 16px;}
      .numberList3 li,.numberList4 li{font-size: 12px; color: red;}
    </style>
    <body>
      <ul class="numberList f12">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
      <ul class="numberList f16">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
      <ul class="numberList f12 red">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
      <ul class="numberList f16 red">
        <li>11111111</li>
        <li>11111111</li>
      </ul>
    </body>

可以看出方案三比方案二改起来方便不要太多，只需要在html中加上一个ul，并且加上适当的类名就可以了，而方案二还需要在css中改动几处，这样也容易出错。

>   在面向对象编程里，有类似的情况：继承和组合。**继承**的思路是将一个复杂且包含变化的类，拆分成几个复杂但是稳定的子类。**组合**的思路是讲一个复杂的类分成容易产生变化的部分和相对稳定的部分。
>使用继承的话，任何一点小的变化也需要重新定义一个类，很容易引起类的爆炸式增长，所以在面向对象编程里，有个很重要的原则就是“**多用组合，少用继承**”。

###（三）低权重原则——避免滥用子选择器

>css权重的规则：
  标签：1，    类：10，   id：100,
  如果权重相同，样式遵循就近原则。

为了保证样式容易被覆盖，提高可维护性，css选择符需保证权重尽可能低。所以，除非确定HTML结构非常稳定，一定不会再修改，否则尽量不要使用子选择器。

###（四）CSS sprite

>CSS sprite： 将多张背景图片合并到一张大图上，然后利用background-position属相来展示需要的部分。
>
>优点：大大减少网页的HTTP请求数，减小服务器压力。
>
>缺点：
>
>*  图片的位置精确程度要求非常高，在制作网页时，我们需要精确测量坐标，还需要考虑如何让图案尽可能密集地排列，影响开发速度。
>*  大图中每个小图的坐标值都不可轻易改动，因为每改动一个小图，都能影响到周边的其他图片，大大降低了可维护性。

关于 CSS sprite，需要注意几点:

1、它能合并的只能是用于背景的图片，对于`<img src=""/>`设置的图片，是不能够合并到大图的，会影响页面的可读性。

2、对于横向和纵向都平铺的图片，也不能使用。

###（五）CSS hack
1、IE条件注释法

下面这个例子是针对不同的IE版本分别导入样式
    
    <!-- 只在IE6情况下加载 -->
    <!-- [if IE 6]>
      <link rel="stylesheet" href="ie6.css">
    <![endif] -->
    <!-- 只在版本号大于7情况下加载 -->
    <!-- [if gt IE 7]>
      <link rel="stylesheet" href="ie7.css">
    <![endif] -->--------
    <!-- 只在版本号大于8情况下加载 -->
    <!-- [if gt IE 8]>
      <link rel="stylesheet" href="ie8.css">
    <![endif] -->

lte:小于等于

gte:大于等于

gt:大于

！:不等于

>事实上，虽然条件注释最常用于CSS的hack，但它能包含的内容还可以是`<scipt></script>`。从上面的例子可以看出，虽然它的向后兼容是最好的，但是它的缺点也是非常明显：将同意CSS选择符下的样式分散到三个文件中去控制，增加了开发和维护成本。

2、选择符前缀法

    <style>
      .test{width:80px;}           /*IE6，IE7，IE8*/
      *html .test{width: 60px;}    /*only for IE6*/
      *+html .test{width: 70px;}   /*only for IE7*/
    </style>

选择符前缀法的原理是在CSS选择符前加一些只有特定浏览器才能识别的前缀，从而让某样式只对特定浏览器生效。

>选择符前缀法相比于IE条件注释法来说，样式可以集中起来，可维护性强了很多。但是不能保证以后IE9，IE10不能识别*html和*+html，向后兼容性上存在一点风险。

3、样式属性前缀法

    <style>
      .test{width: 80px; *width: 70px; _width:60px;}
    </style>

样式属性前缀法是在样式的属性名前加前缀，这些前缀只有在特定浏览器下才生效。例如"_"只在IE6下生效，"*"只在IE6和IE7下生效。

>样式属性前缀法比选择符前缀法聚合度更高，代码更精简，可维护性很强，但是和选择符前缀法一样，它在向后兼容性上存在风险。

###（六）居中

####1、水平居中

1） 文本、图片等行内元素的水平居中
  
  父元素设置`text-align:center`。

2） 确定宽度的块级元素的水平居中

  设置`margin-left:auto; margin-right:auto`来实现。

3） 不确定宽度的块级元素的水平居中

* **方法一**：用table标签来帮助实现。

table本身并不是块级元素，如果不给它设置宽度的话，他的宽度由内部元素的宽度“撑起”，但即使不设置它的宽度，仅设置`margin-left:auto; margin-right:auto`就可以实现水平居中。**缺点**是增加了无语义标签，加深了标签的嵌套层数。

    <style>
      ul {list-style: none;margin: 0;padding: 0;}
      li{float: left;display: inline;margin-right: 5px;}
      table{margin: 0 auto;}
      a {width: 20px;height: 20px;text-align: center;background: red;float: left;} /*float:left相当于display:inline-block*/
    </style>
    <body>
      <table><tr><td><ul>
        <li>
          <a href="#">1</a>
        </li>
        <li>
          <a href="#">2</a>
        </li>
      </ul></td></tr></table>
    </body>

* **方法二**：改变块元素display为inline，然后再使用`text-align:center`

相比于方法一，它的好处是不用增加无语义的标签，简化嵌套，但是他也存在一些问题：将块级元素变成行内元素，就会少一些功能，比如说设置宽高，在某些特殊需求CSS设置中，可能带来一些限制。

    <style>
      ul {list-style: none;margin: 0;padding: 0;}
      .test {text-align: center;}
      .test li{display: inline;}
      a {padding: 2px 6px;text-align: center;background: red;}/* 行内元素嵌套的元素也必须是行内元素*/
    </style>
    <body>
      <ul class="test">
        <li>
          <a href="#">1</a>
        </li>
        <li>
          <a href="#">2</a>
        </li>
      </ul>
    </body>

* **方法三**：设置`position:relative`和left

通过给父元素设置float,然后父元素设置`position:relative`和`left:50%`，子元素设置`positin:relative`和`left:-50%`来实现水平居中。它可以保留块级元素仍以display:block的形式显示，而且不会添加无语义标签，但是它的缺点是`position:relative`带来一定的副作用。

    <style>
      ul {list-style: none;margin: 0;padding: 0;}
      .test {clear: both;float:left;position: relative;left: 50%;}
      .test li{float: left;display: inline;margin-right: 5px;position: relative;left: -50%;}
      a {float: left;width: 20px;height: 20px;text-align: center;background: red;}
    </style>
    <body>
      <ul class="test">
        <li>
          <a href="#">1</a>
        </li>
        <li>
          <a href="#">2</a>
        </li>
      </ul>
    </body>

####2、竖直居中

1）父元素高度不确定的文本、图片、块级元素的竖直居中

  给父元素设置相同的上下边距padding

2）父元素高度确定的单行文本的竖直居中

  给父元素设置line-height来实现，让line-height等于父元素的高度

3）父元素高度确定的多行文本、图片、块级元素的竖直居中

持续更新中……
