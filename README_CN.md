# RecyclerViewDecoration
一个通用的RecyclerView分割线，支持.9图片.

你可以直接导入这个库，因为它已经在JCenter.

### Attention Please
StickyHeadItemDecoration(smooth mode)依然有一个bug,我会尽快修复它。Emm，最近我比较忙。

#### gradle
```code
compile 'com.arjinmc.android:recyclerviewdecoration:2.3.3'
```
#### maven
```code
<dependency>
  <groupId>com.arjinmc.android</groupId>
  <artifactId>recyclerviewdecoration</artifactId>
  <version>2.3.3</version>
  <type>pom</type>
</dependency>
```

# 更新日志

<b>2017/12/20th</b>
* 更新算法，不包括StickyHeadItemDecoration。

<b>2017/10/25th</b>
* 加入固定头部样式，可以自动获取group作为header，你只需要告诉它你的分组的viewtype类型。

它可以自动匹配的group的内容作为固定的header。只支持这种布局LinearLayoutManager.VERTICAL。

<b>2017/9/8th</b>

* 优化绘制和适配LayoutManager。
* 删除两个属性mode和parent。
* 新增RecyclerViewSpaceItemDecoration用来创建空白的分割线。
* 更新示例代码。

现在可以完全自动适配LayoutManager的方向。

<b>2017/7/3rd</b>

* 优化网格模式的画线方式
* 删除旧的过时方法
* 新增网格模式两个属性gridHorizontalSpacing 和 gridVerticalSpacing，可以画纯色线和虚线。

<b>2017/5/27th</b>

* 加入适配v7包的LayoutManager的支持.  

如果你搞不清楚RecyclerViewItemDecoration的画线防线，使用 <b>builder.parent(recycelerView)</b> 替代builder.mode(orientaion), 它可以自动适配RecyclerView的实际方向。

<b>2017/5/23rd</b>

* 网格模式新增属性gridBottomVisible,gridTopVisible,gridLeftVisible,gridRightVisible。你可以控制网格模式的边框是否显示，默认是隐藏。
* 优化算法。

<b>2017/4/15th</b>

* 新增Builder模式创建RecyclerViewItemDecoration。
* 纵/横模式新增paddingStart 和 paddingEnd。
* 纵/横模式新增firstLineVisible 和 lastLineVisible 控制第一行和最后一行是否显示分割线。

# RecyclerViewItemDecoration.Builder
thickness的值最好是偶数，2的倍数。

## Horizonal Mode（横向模式）
``` java

rvData.setLayoutManager(new LinearLayoutManager(context
  , LinearLayoutManager.VERTICAL,false));
rvData.addItemDecoration(new RecyclerViewItemDecoration.Builder(context)
        .color(Color.RED)
        .color("#ff0000")
        .dashWidth(8)
        .dashGap(5)
        .thickness(6)
        .drawableID(R.drawable.diver)
        .drawableID(R.drawable.diver_color_no)
        .paddingStart(20)
        .paddingEnd(10)
        .firstLineVisible(true)
        .lastLineVisible(true)
        .create());

```
## Vertical Mode（纵向模式）
``` java

rvData.setLayoutManager(new LinearLayoutManager(context
  , LinearLayoutManager.HORIZONTAL,false));
rvData.addItemDecoration(new RecyclerViewItemDecoration.Builder(this)
       .color(Color.RED)
       .color("#ff0000")
       .dashWidth(8)
       .dashGap(5)
       .thickness(6)
       .drawableID(R.drawable.diver_vertical)
       .drawableID(R.drawable.diver_v)
       .paddingStart(20)
       .paddingEnd(10)
       .firstLineVisible(true)
       .lastLineVisible(true)
       .create());
```

## Grid Mode（网格模式）
``` java

rvData.setLayoutManager(new GridLayoutManager(this, 6));
rvData.addItemDecoration(new RecyclerViewItemDecoration.Builder(this)
       .color(Color.RED)
       .color("#ff0000")
       .dashWidth(8)
       .dashGap(5)
       .thickness(6)
       .drawableID(R.drawable.diver_color_no)
       .gridBottomVisible(true) //控制下面边框
       .gridTopVisible(true) //控制上面边框
       .gridLeftVisible(true) //控制左边边框
       .gridRightVisible(true) //控制右边边框
       .create());

```

当你使用gridHorizontalSpacing 或者 gridVerticalSpacing 或者两个都使用时,如果你需要显示边框时thickness是必须的属性。目前而言，这两个属性还不支持图片和.9图片。下面是一个例子。

```java
rvData.setLayoutManager(new GridLayoutManager(this, 6));
rvData.addItemDecoration(new RecyclerViewItemDecoration.Builder(this)
       .color("#ff0000")
       .dashWidth(8)
       .dashGap(5)
       .thickness(6)
       .gridBottomVisible(true) //控制下面边框
       .gridTopVisible(true) //控制上面边框
       .gridLeftVisible(true) //控制左边边框
       .gridRightVisible(true) //控制右边边框
       .gridHorizontalSpacing(20)
       .gridVerticalSpacing(10)
       .create());

```

## RecyclerViewSpaceItemDecoration

```java
rvData.setLayoutManager(new GridLayoutManager(this, 6));
rvData.addItemDecoration(new RecyclerViewSpaceItemDecoration.Builder(this)
      //如果纵横间距是一样的，使用margin(int size)
      //如果RecyclerView是线性布局，使用margin(int size)
//      .margin(10)
        .marginHorizontal(10)
        .marginVertical(20)
        .create());
```

## StickyHeadItemDecoration

```java
mCurrentItemDecoration = new RecyclerViewStickyHeadItemDecoration.Builder()
//                .groupViewType(0) //告诉它你的group的viewtype的值
                .isSmooth(true)  //是否需要平滑的移动固定的header，默认是否。
                .create();
mRecyclerView.addItemDecoration(mCurrentItemDecoration);
```

## 效果图
![image](https://github.com/arjinmc/RecyclerViewDecoration/blob/master/images/sample_sticky_head.gif)  
![image](https://github.com/arjinmc/RecyclerViewDecoration/blob/master/images/device-2015-12-02-111504.png)  
![image](https://github.com/arjinmc/RecyclerViewDecoration/blob/master/images/device-2015-11-30-155050.png)
![image](https://github.com/arjinmc/RecyclerViewDecoration/blob/master/images/device-2015-11-30-154937.png)
![image](https://github.com/arjinmc/RecyclerViewDecoration/blob/master/images/device-2015-11-30-155157.png)

