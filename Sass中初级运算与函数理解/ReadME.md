![每日美图.png](https://upload-images.jianshu.io/upload_images/13419832-8d249c09238fbb83.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
# 介绍
今天是大年三十，祝福大家新年快乐，阖家欢乐😉，感谢读者的支持，作者一定会坚持持续为大家带来高质量的文章。任何语言中都会存在数据的运算，运算又分为数值运算和逻辑运算。我们今天就来看一下这一方面。
#简单四则运算
学习运算有一个小技巧，运算涉及到两个要素，变量和运算符，而这两者又都有类型之分。变量类型可以有[Sass变量理解](https://www.jianshu.com/p/dac3b4a67a9d)提到的的几种基本类型，有数字、字符串、颜色、空值
运算又有加减乘除、==、！=、not、or、and，这两个元素在一起又会怎么样呢？一起来看看吧。
##加/减/乘/除
###数字
对于数字类型来说
* 参与*加减乘除*运算的数字只有一种单位则，没有单位的数字会自动转换为此种单位
* 参与*加减乘除*运算的数字存在两种或以上的不同的单位相加减会出问题如下

```scss
.calculator{

  $a : 1px;
  $b : 2;
  $c : 3rem;
  max-height: $a + $c;
  }
```
```scss
//Error: Incompatible units: 'rem' and 'px';
```
* 对于以下三种情况 / 将被视为除法运算符号：
    1. 如果值，或值的一部分，是变量或者函数的返回值
    2. 如果值被圆括号包裹
    3. 如果值是算数表达式的一部分
    4. 如果需要使用变量，同时又要确保 / 不做除法运算而是完整地编译到 CSS 文件中，只需要用 #{} 插值语句将变量包裹。
###字符

* 字符与字符*只有相加，没有相减*，如果字符串之间相减如下
 ```scss
.calculator {
  data-name: "a"-"d";
}
``` 
* 字符与字符之间是不存在*乘除*操作的
```scss
//Error: Undefined operatio
```
* 字符串与数字相加减时数字会转换为字符串,没有乘除操作
* 有引号字符串（位于 + 左侧）连接无引号字符串，运算结果是有引号的，相反，无引号字符串（位于 + 左侧）连接有引号字符串，运算结果则没有引号。
###颜色
* 16进制，短形式如#123，转换为#112233 继续进行正常的16进制加减乘除
```scss
.body{
 $color1 : #123;
 $color2 : #ff1234;
 background-color:$color1 +color2;
 }
```
```scss
.body{
background-color: #ff3467;
}
```
* 16进制与颜色类型和没有单位的数字是可以加减乘除，其他的基本类型都会报错。

###布尔型
除了* 运算会报错外之外其他都会当成字符串"false"与"true"处理。

###空值
基本所有其他类型和null进行操作都报错，连null与null操作也是如此，各位读者也可以自己试试看的。
```scss
//Error: Invalid null operation: \"null plus null

```
#逻辑判断
##==和!=
判断两个变量是否相等
针对颜色类型rgb，16进制与 color-name形式是没有关系的，只要是同一种颜色就是可以的。

##and or not
用于逻辑运算
null空值被当做false处理。

#圆括号
圆括号与数学中的一样可以改变运算顺序。
#总结
在文章最后，作者总结了这边文章中的要点，并整理为一张思维导读方便各位读者迅速理解文章，文章中代码可以点击该[链接](https://github.com/OnlyPiglet/Sass/tree/master/Sass%E4%B8%AD%E5%88%9D%E7%BA%A7%E8%BF%90%E7%AE%97%E4%B8%8E%E5%87%BD%E6%95%B0%E7%90%86%E8%A7%A30)查看。
![Saas基本变量类型运算.png](https://upload-images.jianshu.io/upload_images/13419832-05ef29c124965343.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
