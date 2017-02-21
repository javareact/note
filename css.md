# css兼容性

1. 浏览器
2. 语法版本

# 优化

文件合并<br>
文件压缩<br>
cdn<br>
缓存

## css优先级

- 渲染规则<br>
  1.计算权重<br>
  2.就近规则<br>
  3.!important<br>
  ( 当!important第一次在CSS1中被介绍时是这样规定的，即一个由开发者声明的!important样式要比一个由用户声明的!important样式获得更大的权重。为了提高访问性，在CSS2 中它被颠倒了过来。 如果!important被用于一个简写的样式属性，那么这条简写的样式属性所代表的子属性都会被作用上!important。 关键字!important必须放在一行样式的末尾并且要放在该行分号前，否则就没有效果。 （不过分号前的空格不会影响它） 如果因为一些特殊原因，你不得不在一个代码块中声明两个同样的属性，那么请把!important加在第一个属性后面，因为这样做会让所有浏览器中第一个属性的权重更大，而IE6除外（这是一个只有IE6才有的hack，但是不会影响你的CSS） 在IE6和IE7中如果你使用不同的单词替代!important（像!hotdog），这条CSS样式依然会获得更大的权重，但是其他浏览器却会忽略它。 )

### css动画

- 2D 3D转换 transform属性
- 过度 transition prop time 效果（属性）+时间
- 动画 animation 名称+时间 属性 遵循@keyframes ```js // apply prefixed event handlers function PrefixedEvent(element, type, callback) { for (var p = 0; p < pfx.length; p++) { if (!pfx[p]) type = type.toLowerCase(); element.addEventListener(pfx[p]+type, callback, false); } };<br>
  // handle animation events<br>
  function AnimationListener(e) { LogEvent("Animation '"+e.animationName+"' type '"+e.type+"' at "+e.elapsedTime.toFixed(2)+" seconds"); if (e.type.toLowerCase().indexOf("animationend") >= 0) { LogEvent("Stopping animation..."); ToggleAnimation(); } } // animation listener events PrefixedEvent(anim, "AnimationStart", AnimationListener); PrefixedEvent(anim, "AnimationIteration", AnimationListener); PrefixedEvent(anim, "AnimationEnd", AnimationListener);

var $element = $('.eye').bind("webkitAnimationEnd oAnimationEnd msAnimationEnd animationend", function(event){ if (event.animationName === "three") { console.log('the event happened'); } }

````
### js动画

```js
// 访问css class列表
var el = document.querySelector(".myclass");
// selectors 是一个字符串，包含一个或是多个 CSS 选择器 ，多个则以逗号分隔。
//如果没有找到匹配元素，则返回 null，如果找到多个匹配元素，则返回第一个匹配到的元素。
// elementList = document.querySelectorAll(selectors);
el.classList.add('className');
el.classList.remove('className');
el.classList.item(index);

// animation
window.requestAnimationFrame = window.requestAnimationFrame || window.mozRequestAnimationFrame || window.webkitRequestAnimationFrame || window.msRequestAnimationFrame;

function Box () {

  var animationStartTime = 0;
  var animationDuration = 500;
  var target = document.querySelector('.box');

  this.startAnimation = function() {
    animationStartTime = Date.now();
    requestAnimationFrame(update);
  };

  function update() {
    var currentTime = Date.now();
    var positionInAnimation = (currentTime - animationStartTime) / animationDuration;

    var xPosition = positionInAnimation * 100;
    var yPosition = positionInAnimation * 100;

    target.style.transform = 'translate(' + xPosition + 'px, ' + yPosition + 'px)';

    if (positionInAnimation <= 1)
      requestAnimationFrame(update);
  }
}

var box = new Box();
box.startAnimation();
````

### css常用操作

- 盒子模型

  > border-radius box-shadow border-image<br>
  > 外边距叠加: 遵循最大原则

- 对齐

  > - margin 水平
  > - position 4个值<br>
  >   static<br>
  >   absolute 脱离文档流<br>
  >   relative<br>
  >   fixed
  > - float 左右<br>
  >   inline-block 脱离文档流<br>
  >   .clearfix { overflow: auto; zoom: 1; }

- 选择器 >

  - 多类选择器 css: .class.class{ } html: class = "class1 class2"
  - 相邻选择器 + 同一个父亲，该元素之后的所有同级元素都起效果
  - 同辈选择器 ~
  - 属性选择器 早在CSS2中就被引入了，其主要作用就是为带有指定属性的HTML元素设置样式。使用CSS3属性选择器，你可以只指定元素的某个属性，或者你还可以同时指定元素的某个属性和其对应的属性值。<br>
    在CSS2中引入了一些属性选择器，而CSS3在CSS2的基础上对属性选择器进行了扩展，新增了3个属性选择器，使得属性选择器有了通配符的概念，这三个属性选择器与CSS2的属性选择器共同构成了CSS功能强大的属性选择器。<br>
    CSS3的属性选择器主要包括以下几种：
  - E[attr^="value"]：指定了属性名，并且有属性值，属性值是以value开头的；
  - E[attr$="value"]：指定了属性名，并且有属性值，而且属性值是以value结束的；
  - E[attr*="value"]：指定了属性名，并且有属性值，而且属值中包含了value； 如下，我们设置a标签的href属性值的背景色：<br>
    .wrap a[href^="<http://"]{background:orange;color:blue;}><br>
    .wrap a[href^="mailto:"]{background:blue;color:orange;}<br>
    上面代码选择了a标签的href属性，并且选取属性值为"<http://"和"mailto:"开头的所有a标签，改变其颜色。>

    ```css
    .wrap {
    width: 300px;
    height: 30px;
    padding-top:10px;
    border: 3px solid #ccc;
    }
    .wrap a {
    float: left;
    height: 20px;
    width: 20px;
    border-radius: 10px;
    text-align: center;
    background: #92EF09;
    color: red;
    margin: 0 5px 0 5px;
    }
    ```

  - 这节内容是CSS3选择器最新部分，有人也称这种选择器为CSS3结构类，下面我们通过实际的应用来具体了解他们的使用和区别，首先列出他具有的选择方法：

    1. :first-child选择某个元素的第一个子元素；
    2. :last-child选择某个元素的最后一个子元素；
    3. :first-of-type选择一个上级元素下的第一个同类子元素；
    4. :last-of-type选择一个上级元素的最后一个同类子元素；
    5. :nth-child()选择某个元素的一个或多个特定的子元素；
    6. :nth-last-child()选择某个元素的一个或多个特定的子元素，从这个元素的最后一个子元素开始算；
    7. :nth-of-type()选择指定的元素；
    8. :nth-last-of-type()选择指定的元素，从元素的最后一个开始计算；
    9. :only-child选择的元素是它的父元素的唯一一个了元素；
    10. :only-of-type选择一个元素是它的上级元素的唯一一个相同类型的子元素；
    11. :empty选择的元素里面没有任何内容。 .wrap { width: 300px; height: 30px; padding-top:10px; border: 3px solid #ccc; } .wrap a { float: left; height: 20px; width: 20px; border-radius: 10px; text-align: center; background: #92EF09; color: red; margin: 0 5px 0 5px; }

选择某个元素的第一个子元素<:first-child> :first-child是用来选择某个元素的第一个子元素，比如我们这里的这个demo，你想让列表中的"1"具有与从不同的样式，按照之前的写法，我们需在要第一个li上加上一个相应的class名，比如说"first"，然后我们在给予对应的样式，如下：

.wrap li.first {background: green; border: 1px dashed blue;} 在CSS3最新选择器出现之后，我们就可以使用:first-child来实现，就不需要在增加一个额外的class名了，设置如下：

.wrap li:first-child {background: green; border: 1px dashed blue;} 两种方法最终效果是一样的，只是后者对我来说在操作上会更显得简单、方便、快捷。

请亲自把右侧的第一个背景变为红色，边框为1像素、蓝色、虚线。

.wrap { width: 480px; height: 40px; padding-top:10px; border: 3px solid #ccc; } .wrap ul{ list-style-type:none; margin-left:-25px; margin-top:2px; } .wrap li { border: 1px solid #ccc; padding: 2px; float: left; margin-right: 10px; } .wrap a{ float: left; height: 20px; width: 20px; border-radius: 10px; text-align: center; background: #92EF09; color: red; margin: 0 5px 0 5px; }

选择某个元素的最后一个子元素<:last-child> :last-child选择器与:first-child选择器的作用类似，不同的是它选择是的元素的最后一个子元素。

比如说，我们需要单独给列表最后一项一个不同的样式，我们就可以使用这个选择器，如下设置简单样式：

.wrap li:last-child {background: green; border: 2px dashed blue;} :last-child选择器与:first-child选择器使用方法是不是很类似，亲身感受一下效果吧！

.wrap { width: 480px; height: 40px; padding-top:10px; border: 3px solid #ccc; } .wrap ul{ list-style-type:none; margin-left:-25px; margin-top:2px; } .wrap li { border: 1px solid #ccc; padding: 2px; float: left; margin-right: 10px; } .wrap a{ float: left; height: 20px; width: 20px; border-radius: 10px; text-align: center; background: #92EF09; color: red; margin: 0 5px 0 5px; }

选择某元素下的第一个同类子元素<:first-of-type> ":first-of-type"选择器类似于":first-child"选择器，但不同的是:first-of-type"选择器还额外指定了元素的类型，主要用定位匹配属于其父元素的特定类型的首个子元素。

:first-of-type选择器，不限制是否为第一个子元素，只要为该类型元素的第一个就行， 类型是指什么呢，就是冒号前面匹配到的东西，比如 p:first-of-type，就是指所有p元素中的第一个。

如下我们为第一个p元素设置背景色：

.wrap > p:first-of-type { background: green; }

.wrap div{ margin:20px auto; }

选择某元素的最后一个同类子元素<:last-of-type> 和:first-of-type选择器相反，:last-of-type选择器选择的是父元素下的某个类型的最后一个子元素。

如下，为最后一个p元素设置背景色：

.wrap > p:last-of-type { background: green; } 请亲自把最后一个div标签对应的背景色改为蓝色！

选择某元素的一或多个特定的子元素<:nth-child()> :nth-child()可以选择元素的一个或多个特定的子元素，可以定义他的值(值可以是整数也可以是表达式)。

1. 简单数字序号写法 :nth-child(number)，直接匹配第number个元素。参数number必须为大于0的整数。

  如下，把第3个p的背景设为绿色：

  p:nth-child(3){background:green;}

2. 倍数写法 :nth-child(an)，匹配所有倍数为a的元素。其中参数an中的字母n不可缺省，它是倍数写法的标志，如3n、5n。

  如下，把第2、第4、第6、...、所有2的倍数的p的背景设为蓝色：

  p:nth-child(2n){background:blue;}

3. 倍数分组匹配 :nth-child(an+b)与:nth-child(an-b)，先对元素进行分组，每组有a个，b为组内成员的序号，其中字母n和加号+不可缺省，位置不可调换，这是该写法的标志，其中a,b均为正整数或0。

  如下，匹配第1、第4、第7、...、每3个为一组的第1个p元素

  p:nth-child(3n+1){background:orange;} 如下，匹配第3-1=2、第6-1=5、...、第3的倍数减1个p元素

  p:nth-child(3n-1){background:#33FF33;}

1. 奇偶匹配 :nth-child(odd)与:nth-child(even)分别匹配序号为奇数与偶数的元素。奇数(odd)与(2n+1)结果一样；偶数(even)与(2n+0)及(2n)结果一样。

  这里，我们为奇数和偶数p元素指定两种不同的背景色：

  p:nth-child(odd) { background:#ff0000; } p:nth-child(even) { background:#0000ff; }

  选择元素并倒序计算<:nth-last-child()> ":nth-last-child()"选择器和前面的":nth-child()"很相似，只是这里多了一个last，所以他起的作用就和前面的":nth-child"不一样了，它是从最后一个元素开始算，来选择特定元素。

  如下使用:nth-last-child()选择器来选择元素并添加样式：

  .wrap p:nth-last-child(4) {background: red;} 如上我们设置p元素的倒数第四个元素，我们也可以像":nth-child(2)"一样，使用表达式来选择特定元素。

选择指定的元素<:nth-of-type()> :nth-of-type类似于:nth-child，不同的是他只计算选择器中指定的那个元素，其实我们前面的实例都是指定了具体的元素，这个选择器主要对用来定位元素中包含了好多不同类型的元素是很有用处。

例如我们为奇数和偶数的p元素指定两种不同的背景色，如下：

p:nth-of-type(odd) { background:#FFFF33; } p:nth-of-type(even) { background:#99FF33; }

匹配特定类型的元素并倒数计算<:nth-last-of-type()> :nth-last-of-type(n)选择器匹配属于父元素的特定类型的第N个子元素的每个元素，从最后一个子元素开始计数(n可以是数字或公式)。

如下设置指定p元素背景色：

p:nth-last-of-type(3){ background: red; }

匹配其父元素中有唯一子元素的元素<:only-child> E:only-child，匹配那些是其父元素唯一子元素的E元素。简单来说就是匹配父元素中只有一个子元素的类型元素。

看下如下简单示例：

p:only-child { background:red; }

选择元素的特定类型并唯一的子元素<:only-of-type> :only-of-type是表示一个元素他有很多个子元素，而其中只有一个子元素是唯一的。

所以我们使用这种选择器就可以选中元素的唯一子元素。

如下设置右栏中是唯一元素的背景色：

div :only-of-type{ background-color: green; }

选择没有任何内容的元素<:empty> :empty是用来选择没有任何内容的元素，这里没有内容指的是一点内容都没有，哪怕是一个空格。

现在有四个段落，其中一个段落什么都没有内容为空，如果你想这个p隐藏掉，就可通过:empty选择器来实现，如下：

p:empty { display: none; } :empty选择器对于没有任何内容的元素判断是非常有用的。

本节介绍如何使用CSS3的样式进行圆角边框的绘制。圆角边框的绘制也是Web网站或Web应用程序中经常用来美化页面的效果的手法之一。

在CSS3之前，需要使用图像文件才能达到同样效果，如果只靠样式就能完成圆角边框的绘制，对界面设计者来说无疑是一件可喜的事情。

到目前为止，Safari浏览器、Firefox浏览器、Opera浏览器及Chrome浏览器都支持这种绘制圆角边框的样式。

box-shadow:inset 0 1px 1px rgba(0,0,0,0.075); border-radius:3px; border-color:#ccc; height:1.94em; line-height:1.94em; text-indent:0.8em; border:0; margin:0; -webkit-appearance:none; background-color:#fff; color:#333; outline:0; background-clip:border-box; -webkit-rtl-ordering: logical; -webkit-user-select: text; cursor: auto; text-rendering: auto; -webkit-writing-mode: horizontal-tb;

p:first-line { font-variant: small-caps; } a:link:after { content: " (" attr(href) ")"; }

.wrap { width: 300px; height: 30px; padding-top:10px; border: 3px solid #ccc; } .wrap a { float: left; height: 20px; width: 20px; border-radius: 10px; text-align: center; background: #92EF09; color: red; margin: 0 5px 0 5px; }

# Exemples

1. font:italic bold 50px verdana;