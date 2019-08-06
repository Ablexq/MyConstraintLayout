

[带你了解 Android 约束布局 ConstraintLayout](https://mp.weixin.qq.com/s/JijR16p-DjlsZz8wn5D-PQ)

[约束布局ConstraintLayout用法全解析](https://mp.weixin.qq.com/s/9GrZa4pGBIPDHmyveqhL1A)

[]()

# 优缺点：

ConstraintLayout具有以下优势：

较高的性能优势

布局嵌套层次越高，性能开销越大。而使用ConstraintLayout，经常就一层嵌套就搞定了，所以其性能要好很多。

完美的屏幕适配

ConstraintLayout的大小、距离都可以使用比例来设置，所以其适配性更好。

书写简单

可视化编辑

缺点：

缺点就是调整布局特别是删除一个控件时如果依赖关系比较多时就很麻烦。不过Google爸爸建议使用ConstraintLayout替代RelativeLayout，而且从性能上也比RelativeLayout要好

对于控件的Id定义是一件头疼的事情。还有删除一个控件 就需要动依赖这个控件的所有布局。代码量偏多

# 报错

This view is not constrained vertically: at runtime it will jump to the top unless you add a vertical constraint less... (Ctrl+F1) 
Inspection info:The layout editor allows you to place widgets anywhere on the canvas,
and it records the current position with designtime attributes (such as layout_editor_absoluteX). 
These attributes are not applied at runtime, so if you push your layout on a device, 
the widgets may appear in a different location than shown in the editor. 
To fix this, make sure a widget has both horizontal and vertical constraints by dragging from the edge connections.  
Issue id: MissingConstraints

必须上下或左右都要有约束

# 相对位置

要在ConstraintLayout中确定view的位置,必须至少添加一个水平和垂直的约束。
每一个约束表示到另一个view，父布局，或者不可见的参考线的连接或者对齐。如果水平或者垂直方向上没有约束，那么其位置就是0。

# 尺寸约束

view中使用warp_content或者固定值等等是没有问题的。
但是ConstraintLayout中不支持MATCH_PARENT这个值，如果需要实现跟MATCH_PARENT同样的效果，
可以使用0dp来代替，其表示MATCH_CONSTRAINT,即适应约束。其跟MATCH_PARENT还是有区别的

# 宽高比

在ConstraintLayout中，还可以将宽定义成高的一个比例或者高定义成宽的比率。
首先，需要将宽或者高设置为0dp（即MATCH_CONSTRAINT），即要适应约束条件。
然后通过layout_constraintDimensionRatio属性设置一个比率即可。
这个比率可以是一个浮点数，表示宽度和高度之间的比率；也可以是“宽度：高度”形式的比率。

# 百分比宽高

ConstraintLayout还能使用百分比来设置view的宽高。
要使用百分比，宽或高同样要设置为0dp（MATCH_CONSTRAINT）。
然后设置以下属性即可：
``` 
app:layout_constraintWidth_default="percent" //设置宽为百分比
app:layout_constraintWidth_percent="0.3" //0到1之间的值
或
app:layout_constraintHeight_default="percent" //设置高为百分比
app:layout_constraintHeight_percent="0.3" //0到1之间的值
```

# 位置偏向

如果想让view的位置偏向某一侧，可以使用以下的两个属性来设置：
``` 
layout_constraintHorizontal_bias  //水平偏向
layout_constraintVertical_bias  //竖直偏向
```
其值同样也是0到1之间。

bias即偏移量,他们的取值范围从0~1，0即挨着左边，1是挨着右边，所以要使处于1/3处，可以设置如下属性app:layout_constraintHorizontal_bias="0.33"





# layout_marginStart与layout_marginLeft的区别

有两种阅读方式，从左到右（left-to-right，即LTR）和从右到左（right-to-left，即RTL）。
简单来说，对于LTR，start、end等同于left、right；而对于RTL，则相反。
为了使用RTL布局，需要实现以下两点：

在AndroidManifest中声明支持RTL布局：在 <application>元素下添加android:supportsRtl="true"声明。
在App中用start、end来替代left、right：


如果用4.2及以上编译（ targetSdkVersion或者minSdkVersion大于等于17），则start、end来替代left、right，例如：android:paddingLeft 应改为android:paddingStart

如果用4.2以下编译（ targetSdkVersion或者minSdkVersion小于等于16），两者都必须使用，例如：需要同时使用android:paddingLeft 和android:paddingStart























