<h1 align='center'><font color=red>css笔记</font></h1>

### 框模型
 * #### 边框 <font size=5 color=gree>border</font>
 ##### 基本属性
 <pre>
  border #四个边框的属性值例：border:3px solid blue;
  border-width #边框粗细 例：boder-width:10px;
  border-style #边框样式,可能的值如下所示
    inherit：从父元继承
    none:无边框
    solid：实线边框
    double:双实线边框
    hidden:隐藏边框
    dotted:点状边框
    dashed：虚线边框
    groove：3D凹槽边框 ridge:3D垄状边框 inset:3Dinset边框 outset:3Doutset边框
  border-color #边框颜色
  border-right #设置某侧边框
  border-right-width #设置某侧边框的属性
 </pre>

 ##### css3中的边框 <font size=2 color=gray>（IE9以上支持）</font>
 ```
  border-radius #圆角 例：border-radius:2px;
  box-shadow #边框阴影 例：box-shadow: 10px 10px 5px #888888;按照上左下右的方向依次设置阴影扩散区域，最后一个参数是颜色
  border-image  #边框图片 例：border-image:url(border.png) 30 30 round;
 ```
