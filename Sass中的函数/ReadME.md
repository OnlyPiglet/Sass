![每日美图.jpg](https://upload-images.jianshu.io/upload_images/13419832-b700fb7a4842e956.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#介绍
在查看[Sass中文网](https://www.sass.hk/docs/)发现对函数对函数的内容一笔带过，只提供了英文版内置函数的api，我们还是要看一下一些常用函数。
在[Sass变量基本运算](https://www.jianshu.com/p/98f33bf997d8)一文中我们看了“数字”、“字符串”、“颜色”、“布尔型”、“空值”类型的运算，
在本章中我们将会看有关函数的内容，也有对Map和List数据类型的操作。[指令](https://baike.baidu.com/item/%E6%8C%87%E4%BB%A4/3225201),指令就是告诉计算机从事某一特殊运算的代码。
#函数
##自定义函数
要实现函数的声明和返回内容我们需要使用function和return两个指令，类似于其他语言中的关键字。
@function 函数名(形参) {
  @return;
}

使用时时直接使用 函数名即可
```scss
@function getWidth($w) {

  @return $w * 2;
}


.main{

  max-width: #{getWidth(20)}px;

}
```
编译后
```css
.main {
  max-width: 40px;
}
```
##内置函数
内置函数是指语言本身针对一些数据类型和结构的常用操作进行封装，方便使用。
[Sass函数api链接](http://sass-lang.com/documentation/Sass/Script/Functions.html)
这里只会针对列表与Map的常见操作进行整理，其他更加详细的内容需要读者自己进行查阅了，官方API已经整理的很好啦
这些是对列表和Map都可以使用的函数
```scss
length($list) // 返回列表或者Map的长度.

nth($list, $n) // 返回列表或者Map中的一个元素，$n在是元素对应的index从1开始.

set-nth($list, $n, $value) // 替换列表或者Map中的元素.

join($list1, $list2, [$separator, $bracketed]) // 将两个列表或者Maps合并.

append($list1, $val, [$separator]) // 讲一个元素添加至列表或者Map中

zip($lists…) //将多个列表或者Map合并成新的列表或者Map里面每一个元素是原来单个列表

index($list, $value) // 返回列表或Map中元素的index

list-separator($list) // 返回list的分割符号有comma 逗号 space 空格

is-bracketed($list) // 返回一个列表或者map是否被（）包裹
```

```scss
$arr : 1 2 3 4;
$map : ("a":1,"b":2);

```

这里面的list元素为1、2、3、4，map中的元素为 "a" 1 、 "b" 2。没有错在map中元素就是 key value。kee与value都可以为null,list里也是可以存在null，不过null是不会编译到css中的

接下来针对map还有一些常见内置函数
```scss
map-get($map, $key) //根据key返回value

map-merge($map1, $map2) //将两个map合并为一个map

map-remove($map, $keys…) //根据key移除value

map-keys($map) //返回map中所有的key

map-values($map) //返回map中所有的values

map-has-key($map, $key)//判断map中是否存在key

type-of($value) //返回一个数值的数据类型
```

#总结
1. 指令就是告诉计算机从事某一特殊运算的代码。
2. 自定义函数需要使用到@function内置指令
3. [Sass函数api链接](http://sass-lang.com/documentation/Sass/Script/Functions.html)

