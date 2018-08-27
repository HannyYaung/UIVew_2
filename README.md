# UIVew_2
Android UI 高级进行,布局部分

## 布局过程的含义

布局过程,就是程序在运行时利用布局文件的代码来计算出实际尺寸的过程

## 布局过程的工作内容

两个阶段: 测量阶段和布局阶段

**测量阶段:** 从上到下递归地调用每个View或者ViewGroup 的 measure()方法,测量他们的尺寸并结算他们的位置;
**布局阶段:** 从上到下递归地调用每个View或者ViewGroup 的 layout()方法,把测得的他们的尺寸和位置赋值给他们.

## View 或 ViewGroup 的布局过程

1.测量阶段,measure()方法被父View调用,在measure()中做一些准备和优化工作后,调用onMeasure()来进行实际的自我测量.onMesaure()做的事,View和ViewGroup不一样:

**1.View:** View在onMeasure() 中会算出自己的尺寸然后保存

**2.ViewGroup:** ViewGroup 在onMeasure()中会调用所有子View的measure()让他们进行自我测量,并根据子View计算出的期望尺寸来计算出他们的实际尺寸和位置,然后保存.同时,它会根据子View的尺寸和位置来计算出自己的尺寸然后保存;

2.布局阶段,layout() 方法被父View调用,在layout()中他会保存父View传进来的自己位置和尺寸,并调用onlayout()来进行实际的内部布局.onlayout()做的事,View和ViewGroup也不一样:

**1.View** 由于没有子View,所以View的onlayout什么也不用做

**2.ViewGroup:** ViewGroup 在onLyaout()中调用自己所以子View的layout()方法,把他们的尺寸和位置传给他们,让他们自我完成内部布局

## 布局过程自定义的方式

三类:

- 重写onMeasure() 来修改已有的View 的尺寸;

- 重写onMeasure() 来全新定制View的尺寸;

- 重写onMeasure() 和 onLayout() 来全新定制自定义ViewGroup 的内部布局.

## 第一类自定义的具体做法

也就是重写onMeasure()来修改已有的View的尺寸具体做法:

1.重写onMeasure()方法,并在里面调用super.onMeasure().触发原有的自我测量;

2.在super.onMeasure()的下面用getMeasureWidth()和getMeasureHeight(),来获取之前的测量结果,并使用自己的算法,根据测量结果计算出新的结果;

3.调用setMeasureDimension(),来保存新的结果.

