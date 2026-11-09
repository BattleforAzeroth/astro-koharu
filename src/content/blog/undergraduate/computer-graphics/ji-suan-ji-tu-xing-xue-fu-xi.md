---
title: 计算机图形学复习
link: ji-suan-ji-tu-xing-xue-fu-xi
date: 2022-10-30 13:59:54
categories:
  - - 本科作业
    - 计算机图形学
cover: https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.cover.png
tags:
  - 计算机图形学
math: true
quiz: true
---

:::info
以下为个人计算机图形学考前复习笔记
课程：计算机图形学
教材：计算机图形学基础（第 3 版） 陆枫 何云峰 编著
:::
:::warning
整理知识点来自教材中对应的章节
:::
# 计算机图形系统及图形硬件（第二章）
## 图形显示设备（2.3）
### 阴极射线管
1. 阴极射线管 CRT
![阴极射线管的组成](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.1.png#pic_center "CRT的构造"){height="200px"}
CRT 由电子枪、偏转系统及荧光屏（荫罩、荧光粉层、玻璃外壳）三个基本部分组成
- 电子枪：由灯丝、阴极、控制栅组成。彩色 CRT 中有[红]{.red}[绿]{.green}[蓝]{.blue}三支电子枪（有的是单枪三束）
++荧光粉++具有++余辉特性++{.dot}：电子束停止轰击荧光屏后，荧光粉的亮度并不是立即消失，而是按++指数++{.dot}规律衰减，图像逐渐变暗，[为了得到亮度稳定的图像，电子枪需要不断地根据帧缓存的内容轰击荧光屏]{.pink}，反复重绘同一幅图像，即不断刷新屏幕
- 控制栅：加上负电压后，能够控制通过其中小孔的带负电的电子束的强弱。通过调节负电压高低来控制电子数量，即控制荧光屏上相应点的亮度
- 最大偏转角：电子束要到达屏幕的边缘时，偏转角度就会增大。到达屏幕最边缘的偏转角度被称为最大偏转角
- 持续发光时间：电子束离开某点后，该点的亮度值衰减到初始值 1/10 所需的时间
- 刷新频率：每秒钟重绘屏幕的次数
某种 CRT 产生稳定图像所需要的++最小刷新频率++{.dot}=1 秒/荧光物质的持续发光时间
:::info
例如：一种荧光物质持续光时间 40 毫秒，刷新频率为 1000/40=25 帧/秒
:::
- 像素：构成屏幕（图像）的最小元素
- 分辨率：CRT 在水平或竖直方向单位长度上能识别的最大像素个数，单位通常为 dpi

2. 彩色阴极射线管
将能够发出[红]{.red}[绿]{.green}[蓝]{.blue}三种颜色的荧光粉涂在荧光屏上。荧光粉受到不同强度的电子束激发使发出的色光产生混合形成彩色图形
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.2.png#pic_center "荫罩及彩色显像管上荧光小点的排列"){height="150px"}

### CRT 图像显示器
1. 随机扫描的图形显示器
在随机扫描图形显示器中，电子束的定位和偏转具有随机性，即电子束的扫描轨迹随显示内容而变化，只在需要的地方扫描，而不必全屏扫描

2. 直视存储管图形显示器
这种显示器的电子束不是直接打在荧光屏上，而是先用写入电子枪将图像信息以正电荷“写”在一个每英寸有 250 条细丝的存储栅上。读电子枪发出的电子流再把存储栅上的图像“重写”在屏幕上。紧靠着存储栅后面的是收集栅，主要作用是使读出的电子流均匀，并以垂直方向射向屏幕。读电子枪发出的电子流以低速流经收集栅，并被吸引到存储栅上存有图像信息的正电荷上去，而存储栅上的非正电荷部分则被排斥。被吸引过去的电子直接通过存储栅并轰击荧光粉形成图像

3. 光栅扫描图形显示器

光栅显示器为了在能整个屏幕上显示出图形，电子束需要从屏幕的左上角开始，沿着水平方向从左至右匀速地扫描，一直扫描到屏幕的右下角，显示出一帧图像
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.3.png#pic_center)
- 帧缓冲器：显存内用于存储一帧图像的一片连续内存空间。光栅扫描显示器使用帧缓冲存储屏幕上每个像素的颜色信息，帧缓冲使用++位面++{.dot}与屏幕像素一一对应。
- 1 位面：如果屏幕上每个像素的颜色只用一位表示，其值非 0 即 1，屏幕只能显示黑白二色图像，称为黑白显示器，此时帧缓冲器只有一个位面
- 8 位面：如果每个像素的颜色可以用一个字节表示，帧缓冲器需要用八个位面，可表示 256 种灰度，称为灰度显示器

1. 灰度等级为 16 级，分辨率为 1024*1024 的显示器，至少需要的帧缓存容量为 [A]{.gap} 。 {.quiz .fill}
    - 512KB {.correct}
    - 1MB
    - 2MB
    - 3MB
{.options}
    > 16 种灰度需 4 位面
    > 4 bit × 1024 × 1024 = 512 KB

- 24 位面：如果每个像素用 RGB 三原色混合表示，其中每种原色分别用一个字节表示，各对应一把电子枪，每种颜色可有 256 种亮度，三种颜色的组合是$2^{24}$颜色，共有 24 个位面

### 平板显示器
低电压、轻小型、数字化显示器件，适用于小型设备上的显示装置
有五种：液晶显示器（LCD 显示器）、等离子体显示板、薄片光电显示器、发光二极管显示器、激光显示器

## 图形显示子系统（2.4）
### 光栅扫描图形显示子系统的结构
- 帧缓冲存储器：用来存储像素颜色（灰度）值的存储器
- 双缓存：一个缓存用来刷新的同时，另一个写入数据信息，尔后这两个缓存可互换角色。这种方式称为双缓存，它可以使得显示的动画流畅而没有滑动感

![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.4.png#pic_center "简单的光栅图形显示子系统")
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.5.png#pic_center "常用的光栅图形显示子系统")
{.gallery data-height="100"}


### 绘制流水线
图形子系统的图形绘制功能常常采用++流水线++{.dot}结构绘制，或者称为++管线绘制++{.dot}。
绘制流水线包括三个阶段：应用程序阶段、几何阶段、光栅阶段
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.6.png#pic_center "绘制流水线的结构")

# 图形的表示与数据结构（第 4 章）
## 坐标系（4.1.3）
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.7.png#pic_center "坐标系的分类"){height="200px"}

1. 建模坐标系：又称为造型坐标系，用来定义基本形体或图素。对千定义的每个形体或图素都可以有各自的坐标原点和长度单位。这里定义的形体和图素经调用可放在用户坐标系的指定位置。因此，造型坐标系又可看作局部坐标系，而用户坐标系可看作整体坐标系（全局坐标系）
2. 用户坐标系：也称为世界坐标系，用千定义用户的整图结构或最高层图形结构，各种子图、图素经调用后，都放在用户坐标系的适当位置。用户可根据应用的情况选择相应的坐标系，如直角坐标系、仿射坐标系、圆柱坐标系、球坐标系和极坐标系等
3. 观察坐标系：可在用户坐标系的任何位置、任何方向定义。它主要有两个用途：一是指定裁剪空间，确定形体的哪部分要显示输出；二是通过定义观察（投影）平面，把三维形体的用户坐标变换成规格化的设备坐标
4. 规格化的设备坐标系：用来定义视图区，其取值范围一般约为$(0.0, 0.0, 0.0)$到$(1.0, 1.0, 1.0)$，通过坐标转换，可提高应用程序的可移植性
5. 设备坐标系：图形输入、输出设备的坐标系，如图形显示器有其特殊的坐标系。通常是定义像素，或位图的坐标系

## 多边形表面模型（4.2.1）
### 数据结构
1. 几何信息：顶点表、边表和多边形表
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.8.png#pic_center "顶点表、边表和多边形表"){height="350px"}
2. 拓扑信息：翼边结构表示
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.9.png#pic_center "顶点表、边表和多边形表"){height="200px"}
3. 属性信息：用属性表来存储多边形面的属性，指明物体透明度及表面反射度的参数和纹理特征等等
### 多边形网络
三维形体的边界通常用++多边形网格++{.dot}的拼接来模拟

## 层次建模（4.4）
- 段：具有逻辑意义的有限个图素（或体素）及其附加属性的集合称为段，或者称为图段（二维空间中）、结构和对象
- 段是可以嵌套的，即用一些简单的段和图素可以形成更复杂的段
- 段与基本图形元素的区别在于，基本图形元素是用++数据++{.dot}来描述的，而段是用++规则++{.dot}来描述的
- 段的三个特性：可见性、醒目性和可选择性（可由交互式输入设备来选择）
- 图段进行层次建模的好处：
- [x] 存储简单：一个段虽然在图中各处出现，但他的几何和拓扑信息只要保存一次。
- [x] 编辑简单：删除、移动及缩放操作都可以以段为单位。
- 层次模型：系统的层次模型可以通过将一个图段嵌套到另一个图段中形成图段树来创建
- 图层：通过把功能相同的部分归类，并将它们绘制在同一层上，有助于图形的理解和管理。一般图层不再嵌套

# 基本图形生成算法（第 5 章）
## 直线的扫描转换（5.1）
### 数值微分法（DDA）
$$
\begin{dcases}
x_{i+1}=x_i+ \varepsilon \cdot \Delta x \\
y_{i+1}=y_i+ \varepsilon \cdot \Delta y 
\end{dcases}
$$
$$
\varepsilon = 1/ \max (\left| \Delta x \right|, \left| \Delta y \right|)
$$
最大位移方向上+1，计算后舍入取整`(int)(x+0.5)`
### 中点 Bresenham 算法
原理：每次在最大位移方向上走一步，而另一个方向是走步还是不走步取决于误差项的判别
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.10.png#pic_center){height="300px"}

$$F(x)=y-kx-b$$

$$\begin{equation}
\begin{split}
d_i&=F(x_i+1,y_i+0.5) \\
&=y_i+0.5-k(x_i+1)-b
\end{split}
\end{equation}$$

误差项的递推($d<0$，走一步)：

$$\begin{equation}
\begin{split}
d_{i+1}&=F(x_i+2,y_i+1.5) \\
&=y_i+1.5-k(x_i+2)-b \\
&=d_i+1-k
\end{split}
\end{equation}$$

误差项的递推($d \geq 0$，不走)：

$$\begin{equation}
\begin{split}
d_{i+1}&=F(x_i+2,y_i+0.5) \\
&=y_i+0.5-k(x_i+2)-b \\
&=d_i-k
\end{split}
\end{equation}$$

初始值$d$的计算：

$$\begin{equation}
\begin{split}
d_0&=F(x_0+1,y_0+0.5) \\
&=y_0+0.5-k(x_0+1)-b \\
&=0.5-k
\end{split}
\end{equation}$$

### 改进的Bresenham算法
误差项的计算：
1. $d_0=0$
2. 每走一步：$d=d+k$
3. 一旦y方向上走了一步（$d>0.5$），$d=d-1$

:::success no-icon
改进1：$e=d-0.5$
1. $e_0=-0.5$
2. 每走一步：$e=e+k$
3. 一旦y方向上走了一步（$e>0$），$e=e-1$
:::
:::success no-icon
改进2：用$E=2e \Delta x$来替换$e$，进行化整
1. $E_0=-0.5 \cdot 2 \Delta x =- \Delta x$
2. 每走一步：$E=(e+k) \cdot 2 \delta x = E + 2 \Delta y$
3. 一旦y方向上走了一步（$E>0$），$E=(e-1) \cdot 2 \Delta x =E-2 \Delta x$
:::

## 圆的扫描转换（5.2）

![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.11.png#pic_center){height="300px"}

$$F(x)=x^2+y^2-R^2$$

$$\begin{equation}
\begin{split}
d_i&=F(x_i+1,y_i-0.5) \\
&=(x_i+1)^2+(y_i-0.5)^2-R^2
\end{split}
\end{equation}$$

误差项的递推($d \leq 0$，不走)：

$$\begin{equation}
\begin{split}
d_{i+1}&=F(x_i+2,y_i-0.5) \\
&=(x_i+2)^2+(y_i-0.5)^2-R^2 \\
&=d_i+2x_i+3
\end{split}
\end{equation}$$

误差项的递推($d > 0$，走一步)：

$$\begin{equation}
\begin{split}
d_{i+1}&=F(x_i+2,y_i-1.5) \\
&=(x_i+2)^2+(y_i-1.5)^2-R^2 \\
&=d_i+2(x_i-y_i)+5
\end{split}
\end{equation}$$

初始值$d$的计算：

$$\begin{equation}
\begin{split}
d_0&=F(x_0+1,y_0-0.5) \\
&=(x_0+1)^2+(y_0-0.5)^2-R^2 \\
&=1+(R-0.5)^2-R^2 \\
&=1.25-R
\end{split}
\end{equation}$$

:::success no-icon
改进1：$e=d-0.25$
1. $e_0=1-R$
2. 因$d$为整数，判别条件不变
:::

## 椭圆的扫描转换（5.3）

$$F(x)=b^2x^2+a^2y^2-a^2b^2$$

以弧上斜率为－1的点作为分界将第一象限椭圆弧分为上下两部分(两部分的最大位移方向不同)
上半部分，$x$为最大位移方向，满足$b^2(x+1)<a^2(y-0.5)$：

![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.12.png#pic_center){height="250px"}

$$\begin{equation}
\begin{split}
d_1&=F(x_i+1,y_i-0.5) \\
&=b^2(x_i+1)^2+a^2(y_i-0.5)^2-a^2b^2
\end{split}
\end{equation}$$

误差项的递推($d_1 \leq 0$，不走)：

$$\begin{equation}
\begin{split}
d_1&=F(x_i+2,y_i-0.5) \\
&=b^2(x_i+2)^2+a^2(y_i-0.5)^2-a^2b^2 \\
&=d_1+b^2(2x_i+3)
\end{split}
\end{equation}$$

误差项的递推($d_1 > 0$，走一步)：

$$\begin{equation}
\begin{split}
d_1&=F(x_i+2,y_i-1.5) \\
&=b^2(x_i+2)^2+a^2(y_i-1.5)^2-a^2b^2 \\
&=d_1+b^2(2x_i+3)+a^2(-2y_i+2)
\end{split}
\end{equation}$$

初始值$d$的计算：

$$\begin{equation}
\begin{split}
d_{10}&=F(x_0+1,y_0-0.5) \\
&=b^2(x_0+1)^2+a^2(y_0-0.5)^2-a^2b^2 \\
&=b^2+a^2(b-0.5)^2-a^2b^2 \\
&=b^2+a^2(-b+0.25)
\end{split}
\end{equation}$$

下半部分：

![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.13.png#pic_center){height="250px"}

$$\begin{equation}
\begin{split}
d_2&=F(x_i+0.5,y_i-1) \\
&=b^2(x_i+0.5)^2+a^2(y_i-1)^2-a^2b^2
\end{split}
\end{equation}$$

误差项的递推($d_1 \leq 0$，走一步)：

$$\begin{equation}
\begin{split}
d_2&=F(x_i+1.5,y_i-2) \\
&=b^2(x_i+1.5)^2+a^2(y_i-2)^2-a^2b^2 \\
&=d_2+b^2(2x_i+2)+a^2(-2y_i+3)
\end{split}
\end{equation}$$

误差项的递推($d_1 > 0$，不走)：

$$\begin{equation}
\begin{split}
d_2&=F(x_i+0.5,y_i-2) \\
&=b^2(x_i+0.5)^2+a^2(y_i-2)^2-a^2b^2 \\
&=d_2+a^2(-2y_i+3)
\end{split}
\end{equation}$$

用上半部分计算的最后点$(x,y)$来计算下半部分中误差项的初值：

$$\begin{equation}
\begin{split}
d_{20}&=F(x+0.5,y-1) \\
&=b^2(x+0.5)^2+a^2(y-1)^2-a^2b^2
\end{split}
\end{equation}$$

注意判断条件：$b^2(x+1)<a^2(y-0.5)$，满足条件为上半部分，否则转到下半部分

## 多边形的扫描转换和区域填充（5.4）

- 多边形的扫描转换（多边形填充）：给定多边形顶点，填充多边形多边形内的所有点
- 区域填充（种子填充）：给定区域内的一点（种子），填充围定该点的边界内的所有点

### X-扫描线算法取整规则：
检查顶点两条边的另外两个端点的Y值，两个Y值中大于交点Y值的个数是0，1，2，来决定取0，1，2个交点
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.14.png#pic_center){height="280px"}

### 改进的有效边表算法（Y连贯性算法）
- 有效边：指与当前扫描线相交的多边形的边，也称为活性边
- 有效边表（AET）：把有效边按与扫描线交点x坐标递增的顺序存放在一个链表中，此链表称为有效边表
有效边表的每个结点存放对应边的信息（含边较低端点x坐标、最大y坐标、边斜率倒数）：

| :---: | :---: | :---: | :---: |
|  $x$  | $y_m$ | $1/k$ | $next$ |

![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.15.png#pic_center){height="240px"}
只有交点计为1个时需要缩减，习题中采用(b)缩减$y_{max}$的边
算法步骤见[习题](https://battleforazeroth.github.io/%E6%9C%AC%E7%A7%91%E4%BD%9C%E4%B8%9A/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%BD%A2%E5%AD%A6/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%BD%A2%E5%AD%A6%E4%B9%A0%E9%A2%98%E6%95%B4%E7%90%86/#%E4%B9%A0%E9%A2%98511)

## 反走样（5.7）
- 走样：用离散量表示连续量引起的失真
- 走样现象：
1. 光栅图形产生的阶梯形
2. 图形中包含相对微小的物体时，这些物体在静态图形中容易被丢弃或忽略，在动画序列中时隐时现，产生闪烁

- 产生原因：数学意义上的图形是由无线多个连续的、面积为零的点构成；但在光栅显示器上，用有限多个离散的，具有一定面积的像素来近似地表示他们
- 反走样：用于减少或消除走样的技术
- 过取样：在高于显示分辨率的较高分辨率下用点取样方法计算，然后对几个像素的属性进行平均得到较低分辨率下的像素属性
- 简单过取样：在x，y方向把分辨率都提高一倍，使每个像素对应4个子象素，然后扫描转换求得各子象素的颜色亮度，再对4个像素的颜色亮度进行平均，得到较低分辨率下的像素颜色亮度

![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.16.png#pic_center "简单过取样"){height="240px"}

- 重叠过取样：为了得到更好的效果，在对一个像素点进行着色处理时，不仅仅只对其本身的子像素进行采样，同时对其周围的多个像素的子像素进行采样，来计算该点的颜色属性

![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.17.png#pic_center "重叠过取样"){height="200px"}

- 基于加权模板的过取样：前面在确定像素的亮度时，仅仅是对所有子像素的亮度进行简单的平均。更常见的做法是给接近像素中心的子像素赋予较大的权值，即对所有子像素的亮度进行加权平均

![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.18.png#pic_center "常用的加权模板"){height="150px"}

- 在区域取样中，使用覆盖像素的连续加权函数（滤波函数）来确定像素的亮度
- 加权区域采样特点：
1. 接近理想直线的像素将被分配更多的灰度值
2. 相邻两个像素的滤波器相交，有利于缩小直线条上相邻像素的灰度差

## 在OpenGL中绘制图形（5.8）
- 点的绘制

```cpp
glBegin(GL_POINTS)；
//float类型，3表示3维坐标，glVertex2i则表示2维坐标int类型
glVertex3f(0.0f, 0.0f, 0.0f);
glVertex3f(10.0f, 0.0f, 0.0f);
glEnd()；
```

- 点的属性（大小）

```cpp
void glPointSize(GLfloat size);  //颜色：glColor3f
```

- 直线的绘制模式

![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.19.png#pic_center){height="200px"}

- 直线的属性

```cpp
//线宽
void glLineWidth(GLfloat width);
//线型
glEnable(GL_LINE_STIPPLE);
glLineStipple(GLint factor，GLushort pattern);
```
- 三角形面的绘制：GL_TRIANGLES

```cpp
glBegin(GL_TRIANGLES);
g1Vertex2f(0.0,0.0);
g1Vertex2f(15.0,15.0);
g1Vertex2f(30.0,0.0);
glEnd();
```

- 四边形面的绘制：GL_QUADS
- 多边形面的绘制：GL_POLYGON（必须平面，必须是凸多边形）

# 二维变换及二维观察（第6章）
## 几何变换
### 平移变换

![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.20.png#pic_center)

$$
\left(\begin{matrix}x'&y'&1\\\end{matrix}\right)=\left(\begin{matrix}x&y&1\\\end{matrix}\right)\left(\begin{matrix}1&0&0\\0&1&0\\T_x&T_y&1\\\end{matrix}\right)=\left(\begin{matrix}x+T_x&y+T_y&1\\\end{matrix}\right)
$$

### 比例变换

$$
\left(\begin{matrix}x'&y'&1\\\end{matrix}\right)=\left(\begin{matrix}x&y&1\\\end{matrix}\right)\left(\begin{matrix}S_x&0&0\\0&S_y&0\\0&0&1\\\end{matrix}\right)=\left(\begin{matrix}S_x\cdot x&S_y\cdot y&1\\\end{matrix}\right)
$$
整体比例变换：$\left[\begin{matrix}1&0&0\\0&1&0\\0&0&s\\\end{matrix}\right]$
注意是整体++缩小++{.dot}s倍

### 旋转变换

![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.21.png#pic_center)

$$
\left(\begin{matrix}x'&y'&1\\\end{matrix}\right)=\left(\begin{matrix}x&y&1\\\end{matrix}\right)\left(\begin{matrix}cos{\theta}&sin{\theta}&0\\-sin{\theta}&cos{\theta}&0\\0&0&1\\\end{matrix}\right)=\left(\begin{matrix}xcos{\theta}-ysin{\theta}&xsin{\theta}+ycos{\theta}&1\\\end{matrix}\right)
$$

### 对称变换

$$
\left(\begin{matrix}x*&y*&1\\\end{matrix}\right)=\left(\begin{matrix}x&y&1\\\end{matrix}\right)\left(\begin{matrix}a&d&0\\b&e&0\\0&0&1\\\end{matrix}\right)=\left(\begin{matrix}ax+by&dx+ey&1\\\end{matrix}\right)
$$

![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.22.png#pic_center)

### 错切变换

![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.23.png#pic_center)

$$
\left(\begin{matrix}x'&y'&1\\\end{matrix}\right)=\left(\begin{matrix}x&y&1\\\end{matrix}\right)\left(\begin{matrix}1&b&0\\c&1&0\\0&0&1\\\end{matrix}\right)=\left(\begin{matrix}x+cy&bx+y&1\\\end{matrix}\right)
$$

### 相对任意参考点的复合变换
相对某个参考点$(x_F,y_F)$作二维几何变换，其变换过程为：（分解成基本的几何变换）
1. 平移$(-x_F,-y_F)$
2. 针对原点进行二维几何变换
3. 反平移$(+x_F,+y_F)$

### 二维观察
- 窗口：在用户坐标系中需要进行观察和处理的一个坐标区域
- 视区：窗口映射到显示设备上的坐标区域
- 观察坐标系：依据窗口的方向和形状在用户坐标平面中定义的直角坐标系
- 引入观察坐标系的目的：简化窗口到视区的变换
- 规格化设备坐标：将二维的设备坐标系规格化到$(0.0，0.0)$到$(1.0，1.0)$的坐标范围内形成的坐标系
- 引入规格化坐标系的目的：使观察变换独立于设备
二维观察流程：
![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.24.png#pic_center)

### Cohen-Sutherland算法（编码裁剪算法）

![](https://cdn.jsdelivr.net/gh/BattleforAzeroth/ImageHosting/posts/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%83%8F%E5%AD%A6%E5%A4%8D%E4%B9%A0.25.png#pic_center){height=300}

编码：对于任一端点$(x,y)$，根据其坐标所在的区域，赋予一个4位的二进制码$D_3D_2D_1D_0$
编码规则如下：（简记为[上]{.black}[下]{.green}[右]{.blue}[左]{.red}）
若$x<wxl$，则$D_0=1$，否则$D_0=0$
若$x>wxr$，则$D_1=1$，否则$D_1=0$
若$y<wyb$，则$D_2=1$，否则$D_2=0$
若$y>wyt$，则$D_3=1$，否则$D_3=0$

裁剪：
裁剪一条线段时，先求出端点p1和p2的编码code1和code2，然后：
1. 若$code1|code2=0$：简取。（全可见）
2. 若$code1 \& code2 \neq 0$： 简弃。（全不见）
3. 否则，求直线段与窗口边界的交点，弃外段。再对另一段重复进行上述处理
复习[习题](https://battleforazeroth.github.io/%E6%9C%AC%E7%A7%91%E4%BD%9C%E4%B8%9A/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%BD%A2%E5%AD%A6/%E8%AE%A1%E7%AE%97%E6%9C%BA%E5%9B%BE%E5%BD%A2%E5%AD%A6%E4%B9%A0%E9%A2%98%E6%95%B4%E7%90%86/#%E4%B9%A0%E9%A2%98611)

- 中点分割算法的思想：当对直线段不能简取也不能简弃时，则简单地把线段等分为二段，对两段重复前述测试处理，直到在给定误差范围内（如分割后的直线段长度小于1个像素时）每条线段完全在窗口内或完全在窗口外为止

[Sutherland-Hodgman多边形裁剪](/post/ji-suan-ji-tu-xing-xue-xi-ti-zheng-li/#习题615)、[Weiler-Atherton多边形裁剪](/post/ji-suan-ji-tu-xing-xue-xi-ti-zheng-li/#习题616)参考对应习题
