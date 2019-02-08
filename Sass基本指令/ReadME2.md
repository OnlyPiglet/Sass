![每日美图](https://upload-images.jianshu.io/upload_images/13419832-d58af452870b14b7.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#介绍
有一天一定可以陪着爸妈一起去图中的美景，在这里说一句，谢谢爸妈对我的养育之恩，一次次的原谅包容我的错误，我一定不会让你们失望的，为了美好的未来奋斗，因为这是我值得的Yeah。
还是回到正题吧，上篇[Sass基本指令](https://www.jianshu.com/p/e29a32d851af)我们看了一些sass基于css指令扩展的指令，本文我们只要来看sass独有的一些指令以及用法，我会尽量以最精简的文字描述。
##函数指令function
用于声明函数的指令，详情可以查看[Sass函数](https://www.jianshu.com/p/98f33bf997d8)一篇中的内容，这里就不在赘述了，希望各位读者见谅。
##流程控制指令
在任何计算机语言中都会有流程控制，sass中也是借由指令实现这一功能，sass中的流程指令有
@if、@else、@else if、@while、@for、@each
这里的用法@for与@each需要看一下
for的用法
@for $var from <start> through <end>
@for $var from <start> to <end>
两者的区别就是through是包含end的，而to是不包含end的
@each遍历指令可以是
@each $i in list{}
@each $i,$j in map{}

##开发记录指令
@debug @warn @error
可以使用--quiet命令行选项或:quiet Sass选项关闭警告。 

##样式复用指令@extend
首先我们需要了解一些概念术语
```scss
.cal{
 //...
}
a:hover {
  text-decoration: underline;
}
#fake-links .link {
  @extend a;
}
```
这段代码中a:hover .cal称为选择器,#fake-links .link称为选择器列
@extend 的作用是将重复使用的样式 (.error) 延伸 (extend) 给需要包含这个样式的特殊样式，延伸是什么什么概念呢，具体看一下下面的代码
```scss
.error {
  border: 1px #f00;
  background-color: #fdd;
}
.error.intrusion {
  background-image: url("/image/hacked.png");
}
.seriousError {
  @extend .error;
  border-width: 3px;
}
```
```css
.error, .seriousError {
  border: 1px #f00;
  background-color: #fdd;
}

.error .intrusion, .seriousError .intrusion {
  background-image: url("/image/hacked.png");
}

.seriousError {
  border-width: 3px;
}
```
我们可以发现@extend的延伸其实就是在使用error的地方也使用seriousError。
@extend
* 同一个选择器可以延伸给多个选择器，它所包含的属性将继承给所有被延伸的选择器：
* 当一个选择器延伸给第二个后，可以继续将第二个选择器延伸给第三个；
* 暂时不可以将选择器列 (Selector Sequences)，比如 .foo .bar 或 .foo + .bar，延伸给其他元素
#@mixin @include
同样的针对mixin指令再来看一段代码
```scss
@mixin large-text {
  font: {
    family: Arial;
  }
  color: #ff0000;
}
.page-title {
  @include large-text;
  margin-top: 10px;
}
```
```css
.page-title {
  font-family: Arial;
  color: #ff0000;
  margin-top: 10px; }
```
我们发现使用了include就是讲mixin的样式直接引用进来：
@mixin还可以这样使用
```scss
$color: white;
@mixin colors($color: blue) {
  background-color: $color;
  @content;
  border-color: $color;
}
.colors {
  @include colors { color : $color; }
}
```
```css
.colors {
  background-color: blue;
  color: white;
  border-color: blue;
}
```
这里的@content类似于占位指令的作用
上面描述了@extend与@mixin的主要区别：
* @mixin是支持参数的，@extend是不支持参数的；
* 为便于书写，@mixin 可以用 = 表示，而 @include 可以用 + 表示
#嵌套范围指令@at-root
还记得我们在[Sass基于CSS的嵌套扩展](https://www.jianshu.com/p/c1f437677258)一文中用到了&符号来已用外层选择器，这里的@at-root指令也有一样的含义，但是功能更为强大
看一下关于@at-root的规则
* 默认@at-root只会跳出选择器嵌套，而不能跳出@media或@support。

* 如果要跳出这两种，则需使用@at-root (without: media)，@at-root (without: support)。

* 这个语法的关键词有四个：all（表示所有），rule（表示常规css），media（表示media），support（表示support，因为@support目前还无法广泛使用，所以在此不表）。

#总结
最后依然在文章最后将本文的内容整理为思维导图的形式以便让读者迅速理解：
![Sass基本指令2.png](https://upload-images.jianshu.io/upload_images/13419832-9a5a51516c3b4ce6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)