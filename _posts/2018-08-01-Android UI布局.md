
---
layout:     post
title:      Android 布局参数
subtitle:   常见布局参数  
date:       2018-08-01
author:     mingshu
catalog: true
tags:
    - Android UI
---
# 组件位置
在 RelativeLayout 布局中，每个组件都可以通过ID来制定其相对于其他组件或者父组建的位置：
1. 组建间的相对位置

android:layout_above 将组件放在指定ID组件的上方 
android:layout_below 将组件放在指定ID组件的下方 
android:layout_toRightOf 将组件放在指定ID组件的左方 
android:layout_toRightOf 将组件放在指定ID组件的右方

2. 组件之间的对齐方式
android:layout_alignBaseline 将该组件放在指定ID组件进行中心线对齐 
android:layout_alignLeft 将该组件放在指定ID组件进行左边缘对齐 
android:layout_alignRight 将该组件放在指定ID组件进行右边缘对齐 
android:layout_alignTop 将该组件放在指定ID组件进行顶部对齐 
android:layout_alignButton 将该组件放在指定ID组件进行底部对齐

3. 当前组件与父布局的对齐方式： 
android:layout_alignParentTop 该组件与父组件进行顶部对齐 
android:layout_alignParentBottom 该组件与父组件进行底部对齐 
android:layout_alignParentLeft 该组件与父组件进行左边缘对齐 
android:layout_alignParentRight 该组件与父组件进行右边缘对齐

4. 组建放置的位置
android:layout_centerInParent 将该组件放置于水平方向中央及垂直中央的位置 
android:layout_centerHorizontal 将该组件放置于水平方向中央的位置 
android:layout_centerVertical 将该组件放置于垂直方向中央的位置

5. android:padding和android:layout_margin的区别
其实概念很简单，padding是站在父view的角度描述问题，它规定它里面的内容必须与这个父view边界的距离。margin则是站在自己的角度描述问题
规定自己和其他（上下左右）的view之间的距离，如果同一级只有一个view，那么它的效果基本上就和padding一样了。
android:gravity　属性是对该view 内容的限定．比如一个button 上面的text.  你可以设置该text 在view的靠左，靠右等位置．．
android:layout_gravity是用来设置该view相对与起父view 的位置．比如一个button 在linearlayout里，你想把该button放在靠左　　靠右等位置就可以通过该属性设置．

