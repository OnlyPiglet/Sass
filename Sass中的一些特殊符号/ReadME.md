![每日美图.jpg](https://upload-images.jianshu.io/upload_images/13419832-57f41c0b7851cdc3.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#介绍
在我们看完前面的一些指令之后，sass中的内容我们已经基本看完了，在总结之前我们在看一下sass我们需要注意的一些特殊符号
* `=`           既可以是赋值运算也可以是`@mixin`的缩写
* `+`           既可以是加法运算也可以是`@include`的缩写
* `#{}`         可以占位格式化输出符号
* `!optional`   这个的用法有点特殊难以描述，还是直接看代码吧
```scss
a.important {@extend .notice;}
```
当我们写下这段代码时，因为没有notice的样式所以一定会报错，想要忽略的话可以这样
```scss
a.important {@extend .notice !optional;}
```
在官网中说
` It's also an error if the only selector containing .notice is h1.notice, since h1 conflicts with a and so no new selector would be generated.`
但是在我亲自试验后发现有没有`!optional`结果是一样的也许是版本问题吧。
#总结
1. `=`           既可以是赋值运算也可以是`@mixin`的缩写
2. `+`           既可以是加法运算也可以是`@include`的缩写
3. `#{}`         可以占位格式化输出符号
4. `!optional`   用于忽略@extend的引入错误