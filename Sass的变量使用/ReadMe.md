![每日美图](https://upload-images.jianshu.io/upload_images/13419832-4fee036b9b7c5157.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
# 介绍
在[Sass变量理解](https://www.jianshu.com/p/dac3b4a67a9d)中我们学习了变量的相关知识。在本章我们将会针对Sass变量的理解看一些实例
#实例
##作用范围的不同
###全局变量
```scss
@charset "UTF-8";


$basecolor : #FF0000;


.globalclass{

   $fontsize : 1.2rem !global;
  
}

.main{

  background-color: $basecolor;
  font-size: $fontsize;
  
}

```
编译后为

```scss
@charset "UTF-8";
.main {
  background-color: #FF0000;
  font-size: 1.2rem;
}

/*# sourceMappingURL=VariableScope.css.map */
```
我们可以看到不论是在嵌套外申明的内容，或者在嵌套内申明的变量加上!global 作用域都是全局的。
###局部变量

```scss

.section-one{

   $backcolor : blue;

    background-color: $backcolor;

}

.section-two{

  $backcolor : red;

  background-color: $backcolor;

}
```
编译后的内容
```scss
.section-one {
  background-color: blue;
}

.section-two {
  background-color: red;
}
```
我们发现在section-one与section-two中声明的同名变量$backcolor是互不干扰的,如果去掉section-two中的声明直接使用的话会报如下错误
```scss
"Error: Undefined variable: \"$backcolor\".\A 
```
各位读者也可以尝试一下

#不同类型变量的需要注意的地方
##字符串
代码太多了这里就不展示了，不过有一点值得注意的
```scss
$font-family-one:"宋体";

.four{

  font:{
    family: #{$font-family-one};
  }

}
```
编译后
```scss
.four {
  font-family: 宋体;
}
```
发现引号没有了，这里我们使用了#{}占位符，有过编程经验的朋友应该很熟悉这中表达，占位符，顾名思义在一段代码中占据一定的地方，但内容是不确定，但是不管什么样的内容使用的占位符，有会有一些规则作用于改内容上，
当规则不同时则是不同类型的占位符，目前我们只需要关注 #{}占位符，我们可以总结出该占位符的规则之一就是字符串的引号会被去掉。
##数字
数字其实没什么好说的
```scss
$font-size:1.2rem;

.number{

  font-size: $font-size;
}
```
编译后
```scss
.number {
  font-size: 1.2rem;
}
```


##数组
一般数组用于padding 或者 margin 四边的设置*tips:四边的顺序是12点钟方向顺时钟就是上/右/下/左*
这里就不过多演示就看一种呀
```scss
$padding : 0 0 0 0;
```
编译后
```scss
.padding {
  padding: 0 0 0 0;
}
```
##Map
```scss
$settings:(mask:1000,base:2000);

.mask{
  z-index: map_get($settings,mask);
}
```
编译后
```scss
.mask {
  z-index: 1000;
}
```
key为字符串即使为其他类型也会转换为字符串的

##布尔值
用于逻辑判断，基本不会出现在编译后的css文件中
```scss
//布尔型
$open:true;
$close:false;
```

##空值
当某个样式**仅**使用了null值那么就不会被编译
```scss
//空值
$ifdisable:null;
```
编译后什么都没有

##颜色
颜色需要注意的是当16进制表达的颜色在**压缩格式**输出时又可能会产生变化
```scss
/*!颜色*/

$color:#FF0000;

.main{
  background-color: $color;
}
```
编译后会变为
```scss
/*!颜色*/.main{background-color:red}
/*# sourceMappingURL=Color.css.map */
```
正因为这种变化如果在使用颜色变量时一定要注意防止因为压缩格式编译后引发的变量出错。
本章中所有的源码可以点击[链接](https://github.com/OnlyPiglet/Sass)下载