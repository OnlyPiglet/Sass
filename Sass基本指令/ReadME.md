![每日美图](https://upload-images.jianshu.io/upload_images/13419832-acf0b89f14a37be4.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#介绍
指令我们在[Sass函数](https://www.jianshu.com/p/282fd6e6e741)的介绍中有提到过，并且在那一章提前学习了@function指令。今天我们就来看一下Sass中常用的一些指令，在学习指令这一部分我会分为两篇学习，
只要因为指令包含了基于css指令扩展的指令与sass原生指令。本篇会讲解基于css指令扩展的指令。
#指令的形式
@指令标识符 指令内容;

#编码指令charset
不知道各位读者有没有发现我们前面的源码中在文件开始处会有@charset,这其实是一个CSS3指令，用于设置编译器解析文本所使用的编码，如果在源码中存在中文则需要否则编译出来的是乱码，如下
```scss
.mian{
  font-family:"宋体";
}
```
没有设置编码编译出的css
```css
.mian {
  font-family: "瀹嬩綋";
}
```
设置了编码后编译出来的
```css
@charset "UTF-8";
.mian {
  font-family: "宋体";
}
```
#import样式导入指令
css中import只能导入css，在sass中此指令被加强了，也可以导入sass文件。
@import 寻找 Sass 文件并将其导入，但在以下情况下，@import 仅作为普通的 CSS 语句，不会导入任何 Sass 文件。
* 文件拓展名是 .css；
* 文件名以 http:// 开头；
* 文件名是 url()；
* @import 包含 media queries；

* 如果只希望导入其他的sass文件但是不希望被编译成css，此文件可以在命名时以下划线_开头；
![截图](https://upload-images.jianshu.io/upload_images/13419832-5b734c9a014d257f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
我们可以看到_Compenet.sass并没有编译为css文件

* import指令只可以用在文件最外层，简而言之就是和@charset一样，不能用在嵌套的上下文内如；
```scss
//import错误用法
.mian{
  font-family:"宋体";
  @import "Compenet";

}
```
此处import在mian中使用，并不是最外层，会报如下错误信息：
```css
//error _Compenet.scss (Line 1: @charset may only be used at the root of a document.)
```
##媒体指令media
* 其在 CSS 规则中嵌套。如果 @media 嵌套在 CSS 规则内，编译时，@media 将被编译到文件的最外层，而media则包含嵌套的父选择器。
* media 的 queries 允许互相嵌套使用，编译时，Sass 自动添加 and
* media 可以使用 SassScript（比如变量，函数，以及运算符）代替条件的名称或者值
#总结
在最后，我依旧将本文的关键内容整理为思维导图供读者快速理解
![Sass指令1.png](https://upload-images.jianshu.io/upload_images/13419832-498c72578366ad63.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)