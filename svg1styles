# 进击的 SVG 样式——代码写慢点我晕

 
  
   
   

## 为什么出现了 SVG？

从胶片时代过渡到电子时代，通过模拟像素点，人们把像素记录到了硬盘之中，通过像素的还原，在屏幕中呈现给大家。在这个过程中，产生了很多格式的位图，从 BMP 格式到 gif、jepg、png、webp 等等，其呈现效果和压缩率上不断地优化，成为了现阶段网络媒体的重要部分。

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/RBkmBX.jpg)

然而，通过每个像素点的模拟，呈现图像的方式，更适合显示具象的事物，随着抽象的图形在现实中的应用越来越多，于是矢量图形开始站上了历史的舞台，受限于载体还是以传统印刷的点状、栅格化方式呈现，往往在生产端是矢量，落地处却只能还是以位图的方式呈现，毕竟一张纸一个展板，是没有一个 CPU/GPU 去 渲染出你的矢量图形。而如今网页、移动端开始成为了人们接收信息最主要的窗口，位图格式的媒体已经难以再有更大的突破，效率和适用性上开始不再适用于某些场景，人们开始思考矢量图形在移动网络时代的应用，也发现了其巨大的潜力。就像你画个矢量的 logo，每条曲线背后只是一条公式而已，而你还要切成几万个像素点的 PNG 格式数据，最终呈现在网页上，关键是有时候一些场景现实上还不清晰，这样的呈现效率，你还觉得理所应当？

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/pYAEl6.png)

好，人们开始意识到矢量效率很高，体积小响应快还可以编辑与控制，于是前端开始有了实现的方式，用 canvas 画板来渲染矢量图形，许多简单的图形可以直接通过数学的方式去展示出来，不需要依赖位图，并且还可以低成本实现很多动画，只是，还没有很好的方案可以跟设计端直接打通。视觉呈现上，往往有更复杂的样式，更多的图形，以及复杂的动画，若通过 canvas 来实现，设计落地的成本和局限性比较大。canvas 更适合比较简单的图形方式，也可以用来控制位图和简单的交互。

> `Canvas`是由`HTML`代码配合高度和宽度属性而定义出的可绘制区域。`JavaScript`代码可以访问该区域，类似于其他通用的二维`API`，通过一套完整的绘图函数来动态生成图形。

如果有一种媒介，可以承载矢量素材，自由可控，设计端直接编辑输出，在网页和移动端落地，并且可以控制样式和动画，那它会是怎样的？我觉得就是 SVG ，人们开始需要它，然后它肯定就会出现，就像每一个好软件，使用的时候需要一个功能，你总能再某个角落找到它。

## 什么是 SVG？

> SVG 是一种基于 XML 语法的图像格式，全称是可缩放矢量图（Scalable Vector Graphics）。其他图像格式都是基于像素处理的，SVG 则是属于对图像的形状描述，所以它本质上是文本文件，体积较小，且不管放大多少倍都不会失真。

这里需要简单说明一下啥是 XML:

`可扩展标记语言，标准通用标记语言的子集，简称XML。是一种用于标记电子文件使其具有结构性的标记语言。` 

从这个解释上看有点云里雾里，其实就是把元素定义好，结构化，放在一个文档里面，然后外部可以直接访问具体的数据，或者进行动态地修改。举个比方：有一个叫 【三年二班】的 XML文件，文件里记录了30名学生的数据，姓名，年纪，成绩，职位和性格，加载这个文件后，你可以把班长、学习委员，或者前十名、男女比例等数据，按照你想要的信息，展示出来，除此之外，你（JavaScript）还可以跟里面的班主任打电话，跟她说，过了这个学期，座位按照成绩高地重新排序，或者把班长换成另一位同学。

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/SEJfmo.png)

>XML 被设计用来传输和存储数据, HTML 被设计用来显示数据。

而 SVG 就是这样一个 XML 文档，专门用来存储每个形状的数据和样式，多个形状可以分组形成结构，并且每个单位有自己的名字 ID，可以修改和调用。跟位图相比，一个一万像素点的位图，里面有一万个平等的单位，记录位置和 RGB/CMYK 数据，排序也是固定的，你只能整体控制所有像素，或者用算法限定某种规则去控制，比如把红色变成绿色。却无法自定义拆分每个结构，无法动态修改，与矢量相比，灵活性不足，且文件极大。

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/Y8Harv.png)

最常用的矢量媒体是字体，大家通过把矢量的字母和符号封装在一个字体文件里，我们打字呈现的每一个字，其实就是一串序号，网页通过序号调用了该矢量图形，渲染出来呈现在屏幕上。

## 使用 SVG ，时机成熟了吗？

很多时候我们觉得技术发展更新迭代的很快，似乎下一秒，我们手头功夫就会过时。然而把时间跨度拉长，很多曾经新颖流弊的概念，所谓革命性的技术，往往没有那么快可以落地，毕竟原先的生产流程难以快速更替，新技术往往有很多局限性和技术难度或者成本，解决和推进的过程是很慢的。2010年就在看 HTML 和 SVG 的案例和文章了，2012 年 VR 也火的不行，包括后面的 AI ，都是感觉下一秒就要新时代了，然而现在看来，普及的速度还是很慢的，所以新东西出现的时候，有一个重要的问题是：**是时候了吗？**

从以下几点，我来说说为什么时候到了。

### 浏览器、移动端兼容性

这是现在 SVG 在各个浏览器版本中是否支持的比例，97% 是支持全部样式的，1.76% 支持部分样式，剩下 1.24% 不支持，这一小部分其实用的是很古老的终端手机，一般这类手机基本用来通讯，只有很基本的网页功能，与大部分产品的互联网用户是不符的，因此可以低优先级处理。即使要处理也有相应的方案：把 SVG 渲染成位图展示。安卓4.4以下不支持 SVG，而现有的市场设备占比，4.4版本以下只有3%，并且有兼容解决方案，IOS 也基本没问题。

由此，SVG 在是可以作为普遍适用的媒介。

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/image-20191206171122561.png)

[上图原网站](https://caniuse.com/#feat=svg)

### 响应式布局

移动端为主、多端兼顾，并且如今移动端分辨率和长宽比均比较多样，响应式适配几乎是必须，而要在其中可以通用素材，高质量显示，自动排版，SVG 能体现出非常大的优势。

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/d8Dvfk.png)

### 手机硬件提升

SVG 的渲染不基于尺寸大小，因复杂度和复杂效果而定，过于复杂的 SVG 整体还是需要一定的硬件性能进行支撑。而现在的手机市场日新月异，CPU、GPU 以及内存都到了相当高的水准，足以支撑大型游戏的水平，因此，对于 SVG 渲染，硬件性能上已经十分成熟。

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/QCwJ3v.jpg)

### 手机分辨率提高

现今手机屏幕的分辨率越来越高，高清屏、2K 分辨率的手机越来越多，而大多数网页还在用 720px  的宽度进行素材的输出，如果使用位图作为全屏或者宽度百分百的展示，显示效果和质量都不高，去过用更高清的素材，加载速度，流量成本会比较高，这种情况下 SVG 的更好的解决方式。

> 根据百度流量研究院的统计数据显示，截止 2019 年 4 月， Android 设备的屏幕分辨率主要集中在 1080 * 1920。iOS 设备主要集中在 1242*2208 和 750 * 1334。

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/image-20191206213810308.png)

*图片来源于腾讯移动分析: 2K屏发展趋势

### 动画需求开始增加

手机性能提高，网络环境变好，扁平化风格盛行，体验强度和视觉表达的要求日渐提高，并且无论 web 还是移动端，都有比较成熟的动画方案，于是整个互联网环境，动画需求开始增加，很多交互细节上，或者运营视觉、插画，都开始动画化，而其中，SVG 是动画方案中必不可少的一部分，这部分下一篇主讲。

### 更多样的交互方式

SVG 支持JS 和 CSS 的控制，可以在图片或者动画上，做更细致更多样的交互，甚至实现一些拟物化的交互。

<img src="https://cdn.jsdelivr.net/gh/Himsann/writing@master/rongqiu.gif" style="margin-left:0;" />

### 设计系统开始盛行

在建立设计系统的过程中，样式、组件、元素，一砖一瓦建成大厦，打通设计端到落地全过程，便于维护和更改，快速试错，落地效率十分高效。其中 SVG 的元素，通过 CSS 和组件封装，十分便于搭建一个灵活高效的设计系统。

>Style Guide 逐渐发展衍变为 Design System，基于一套架构严谨、规则统一的框架体系，产品表现层面的设计可以逐渐实现模块化运作，从而大大提高设计效率。而 Atomic Design（原子设计）是构建 Design System 的核心指导理论。

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/uisdc-yz-20181113-21.jpg)



## SVG 与其它图片媒介对比

| 格式      | 大小优势 | 加载效率 | 动画     | 交互控制 | 实现成本       | 补充 |
| :-------- | -------- | -------- | -------- | -------- | -------------- | -------- |
| Jpg       | ☆☆☆      | ☆☆☆☆☆    | 不支持   | ☆     | ☆☆☆☆☆          | 有渐进式加载、无透明度、 |
| Png/Apng | ☆☆       | ☆☆☆☆☆    | ☆☆ | ☆        | ☆☆☆☆☆          | 当前最广泛应用的 格式属性，最稳定 |
| Webp/Webm | ☆☆☆☆     | ☆☆☆☆     | ☆☆☆ | ☆        | ☆☆☆ | 后起之秀，整体压缩压缩率，加载效率等综合素质高，就是兼容性还没跟上 |
| **SVG**   | **☆☆☆☆☆** | **☆☆☆**  | **☆☆☆☆** | **☆☆☆☆** | **☆☆☆☆**       | **矢量格式，数据可控，显示效果好** |
| Gif       | ☆☆       | ☆☆☆☆     | ☆☆☆☆     | ☆☆       | ☆☆☆☆☆          | 有广泛的素材基础，多用于尺寸较小的表情。 |



## 复杂样式插画视觉
### SVG 形式可以更多样

在 SVG 视觉的使用中，我们经常看到简洁、扁平化、描边风的插画视觉，对于有渐变也只是少范围，简单的样式。当然这种方式，文件非常小、便于前端维护与控制；颜色、元素、角色的管理、组合十分高效，容易形成品牌的统一性，由小至大建立一套完善的视觉系统。这种方案十分利于现阶段 Web、H5 移动端的维护与实现，只是大家都以此为途径，形成的视觉同质化比较严重，长期以往大家对于 SVG 矢量视觉形成了一个刻板印象，似乎 SVG 类型只能或者只适合做这类型的视觉，或者认为它就是潮流，而在之前矢量插画领域，有更多复杂的插画风格、更多样化更复杂更多纹理、笔触、氛围感观、对于创作者而言也更为自由。

一个好的媒介，不应该限制住创意的发散，于是这次我们想探讨一下：

'**更复杂样式的 SVG 插画，如何落地**'

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/image_processing20190819-19619-1oagit0.png)

抱着这样的想法，我在实际应用中，尝试了两例 `复杂样式` 视觉的运营活动，并实现了落地


|      | 思路 | 感想 |
| :--- | ---- | ---- |
| 1  | 管它什么样式，模糊、叠加模式，干了再说 | 舒服，反正实现不了还可以输出位图 |
| 2    | 拆分导出，并调整样式出错 | 妈呀，多样式要调整，颜色也要，还不能批量处理，真麻烦 |
| 3    | 压缩优化 | 整体大小真的小了很多 |
| 4    | 检查视觉 | 啧啧，这锐度和颜色和打开速度，真香，回不去了 |

逃不过“真香定律”，优化了流程后，坚定了以后尽量用 SVG 作为媒介去做运营活动，以下以其中一个视觉案例来讲讲细节，主要用的设计软件是 Sketch ：

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/image-20191209112523365.png)

`【猜歌答题】：产品端主要产出 Status 短视频（类似于朋友圈小视频），此类视频的特点是，时间短、主题简单、背景音乐强，类似抖音神曲，于是从音乐入手，让用户看十来秒的短视频，猜歌名闯关，排名前列可获得相应奖励，在此过程中实现拉新的目的`

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/Artboard.jpg)

我们可以看到，主视觉里为了模拟光感，使用了大量的样式与遮罩，包括最模糊柔光，其中也使用了 sketch 图层自带的模糊效果。如下图，奖品主题形状，用了径向渐变、描边、还有丧心病狂的四个带透明的内阴影，并且以它作为背景，叠加了一些反射光图层，反射光使用了图层模糊效果。

<img src="https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/1teoob.png" style="zoom: 40%;margin-left:0px" />

导出后发现，样式如下：

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/Artboard Copy.jpg)

整体样式居然基本可以呈现，出现的灰色色块是标题的遮罩，径向渐变和多层内阴影叠加均可以支持，不过细节还原度还不够。这时候我们再导出一个按钮样式试试效果：

<img src="https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/Artboard Copy 2.jpg"  />

由上图我们可以看到，细节上主要有以下几个问题：

* 遮罩出错：怀疑是 Sketch 的透明遮罩不兼容

* 整体对比度降低，明度增高：怀疑是颜色色值格式不同或叠加模式问题

* 渐变的颜色位置不正确（按钮）：需要测试求解。

这时候，根据行文节奏，我们点开右键查看源码，看看 SVG 里的代码：

<img src="https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/懵逼.png" style="zoom:100%; margin-left:0vw" />

Emm...作为一个成熟稳重思维清晰的设计师，这样的步骤显得太急于求成，我们应该再往前退两步，从基本元素的样式开始，看看从设计软件到 SVG 文件是怎么实现并且有啥玄机。

`温馨提示：以下部分包含少量前端知识，不感兴趣可以直接跳过此 part；不过个人建议对其熟悉一遍，会有利于理解与制作 SVG 动画以及 SVG 设计系统`

寻根究底，我们从以下几个点看看 SVG 文件中图形与样式是怎样的一个方式，包括其兼容性和兼容方式，了解其原理后，我们再解决上诉案例中的问题：

| 形状                                      | 描边                         | 纯色填充          | 渐变                                      | 阴影                               | 遮罩                         | 叠加模式                                |
| ----------------------------------------- | ---------------------------- | ----------------- | ----------------------------------------- | ---------------------------------- | ---------------------------- | --------------------------------------- |
| - 矩形<br/>- 圆形<br/>- 线条<br/>- 不规则 | - 纯色<br/>- 渐变<br/>- 多重 | - 色值<br/>- 多重 | - 线性<br/>- 色点位<br/>- 多点<br/>- 径向 | - 内阴影<br/>- 外阴影<br/>- 多阴影 | - 普通<br/>- 透明<br/>- 渐隐 | - 滤色<br/>- 正叠<br/>- 叠加<br/>- 颜色 |

### 样式测试

以下按照将按照上述表格，详细讲解 SVG 图形与样式的构成，并从视觉落地角度适当发散一些观点，对于设计师而言，无需详细去了解每个属性参数及代码写法，只需要大概知道它是什么，能做什么即可，期间可以对照自己的工作内容与方式，延展一下对自己有帮助的点，毕竟技术只是表达的工具，落地还有专业的前端小哥。

#### 基本形状

我们先在 sketch 中画一个简单的矩形并且导出 SVG，矩形属性如下：

<img src="https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/A35vhI.png" style="zoom:50%;margin-left:0px" />

导出 SVG 后看一下属性，发现代码比较冗杂，默认嵌套两个 group 组，以及一些声明：

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/v0PUeT.png)

真正的有效信息是：

```xml
 <g id="Artboard" transform="translate(-36.000000, -38.000000)" fill="#D8D8D8">

​      <rect id="矩形" x="36" y="38" width="53" height="53"></rect>

​    </g>
```

该信息定义了画板 artboard 作为一个组，获取画板属性，填充颜色。画板内一个矩形，包含了位置和长宽属性。如果只需要这部分的信息，那么其它信息应该可以过滤或者优化，把它定义为一个图片，那么应该会有图片压缩的方案。按照这个思路我们找到了一个开源、通用的压缩方案：[SVGO](https://github.com/svg/svgo)，并使用其网页版进行压缩操作，该网页最好的点是，属性可调，并且可以预览：[SVGOMG](https://jakearchibald.github.io/svgomg/)

压缩后代码如下：

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 53 53">   
	<path fill="#D8D8D8" fill-rule="evenodd" d="M0 0h53v53H0z"/> 
</svg>
```

瞬间清爽！把矩形信息去掉了，将形状转化为 path 路径，对于设计师来说可以理解为在 illustrator 进行转曲，路径的属性为 d="M0 0h53v53H0z"，这串看起来是乱码的语言，其实是一个划线的过程，从起点到终点，画了一个矩形框,简单图解为：

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/rukVTB.png)

由此看来，path 的绘图方式是十分高效的，其中在曲线的绘制上也是类似的划线方式，跟在矢量软件中作图一个原理，分为：

![image-20191210122359703](/Users/fangchuanqian/Library/Mobile Documents/com~apple~CloudDocs/文章写作/SVG 教程/image-20191210122359703.png)

这一部分细究起来，跟设计师矢量绘图的思路基本一致，其中点与点之间的连接还有很多细节，对于设计师来说，简单了解原理即可，此外如果要做路径动画，最低成本实现的方式，就是 SVG 画曲线，目标跟着曲线“绘图”的数据移动，并加以控制，这时候更具体的曲线绘图知识就可以用到：[SVG path 详解](https://cloud.tencent.com/developer/section/1423869)。路径动画的具体参数不用手动写，在矢量软件中画好，复制其曲线参数给到前端即可，可见可得，是未来的趋势。

好，接下来看看其它形状

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/AKqeN6.png)

```xml
<rect   id="矩形"  fill="#1E7BF1" x="0" y="11" width="65" height="26"></rect>                <circle  id="圆"   fill="#1E7BF1" cx="123.5" cy="24.5" r="24.5"></circle>                
<ellipse id="椭圆" fill="#1E7BF1" cx="221.5" cy="24" rx="38.5" ry="13"></ellipse>                <line    id="线"   x1="294.5" y1="24.5" x2="364.5" y2="24.5" stroke="#1E7BF1" stroke-width="3" stroke-linecap="round"></line>
```

忽略具体参数，我们可以看到 SVG 基本形状为：rect（矩形）、circle（圆形）、 ellipse（椭圆）、line（线）、path（路径），此外还有一个多边形 polygon，可以用 path 代替。

压缩后如下：


```xml
 <path fill="#1E7BF1" d="M0 11h65v26H0z"/>    
 <circle cx="123.5" cy="24.5" r="24.5" fill="#1E7BF1"/>    
 <ellipse cx="221.5" cy="24" fill="#1E7BF1" rx="38.5" ry="13"/>    
 <path stroke="#1E7BF1" stroke-linecap="round" stroke-width="3" d="M294.5 24.5h70"/>
```

由于 path 画线的方式比较难还原和控制圆形及椭圆，这类型的还是保持原有属性，其它的类别可以统一用 path 形状进行简化处理。对于复合图形，合并、相减、相交等，会统一进行转曲，并记录为 path，对于 SVG 的压缩这里有一个点需要顾虑，我们在设计软件中给每个图层命名，未压缩前是可以保存为 ID 信息的（ id="矩形"），如果需要精细到每个元素进行样式控制，还是需要保留 ID ，可以在 SVG 外部用 JS 或者 CSS 进行样式与动画控制，如果只是视觉展示，ID 信息作用不大，可以将其“优化”。

SVG 在设计软件中导出，信息比较冗杂，基本需要多一次压缩操作，因此以下样式测试，我们直接展示压缩后的样式，减少数学与代码的出现。

#### 纯色填充与描边

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/hsmWj7.png)

单色填充--双色填充--单色描边--双色描边，按照这个方式看看 SVG 中填充与描边的实现方式，得到的结果如下：

```xml
 <defs>
    <path id="a" d="M101 .11h59v59h-59z"/>        
   //定义矩形为 a
  </defs>

    <path fill="#2757DD" d="M0 .11h59v59H0z"/>    
		//第一个：蓝色单色
    
    <use fill="#2757DD" xlink:href="#a"/>
    <use fill="#E72525" fill-opacity=".5" xlink:href="#a"/>
		//第二个：use 引用上面定义的矩形，然后两个 fill 填充
    
    <path stroke="#2757DD" stroke-width="2" d="M202 .11h59v59h-59z"/> 
		//第三个：单色描边
    
    <g stroke-width="2"> 
      <path stroke="#2757DD" stroke-linejoin="square" d="M304 1.11h57v57h-57z"/>
      <path stroke="#F93030" d="M302-.89h61v61h-61z"/>
   //第四个：双层描边，用一个组概括起来

```

> SVG的<defs>元素用于预定义一个元素使其能够在SVG图像中重复使用，在<defs>元素中定义的图形不会直接显示在SVG图像上。要显示它们需要使用<use>元素来引入它们。

看得出多色填充时候，会先把图形预先定义为一个符号或者 symbol ，再叠加样式，从而实现 Sketch 中无限叠加样式的功能，并且复用图形的方式更加高效简洁。

#### 渐变

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/ko6sY5.png)

我们从最基本形式的渐变，到复杂、带有透明度的渐变进行测试，看到输出的 SVG 文件中，会预先定义好样式，再将样式赋予图形，这样的好处是，如果有使用了同样样式的图形，不需要重复写样式，类似于样式预设，更为高效。

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 424 59">
  <defs> //定义了五种样式
    <linearGradient id="a" x1="50%" x2="50%" y1="0%" y2="100%">
      <stop offset="0%" stop-color="#50F0DC"/>
      <stop offset="100%" stop-color="#2757DD"/>  </linearGradient>
   	 //第一个：垂直渐变，x 与 y  的单位用了百分比%参数，这样无论赋予什么尺寸的形状，都能保持合理的渐变位置。
    
    <linearGradient id="b" x1="111%" x2="22.6%" y1="0%" y2="100%">
      <stop offset="0%" stop-color="#50F0DC"/>
      <stop offset="100%" stop-color="#2757DD"/>  </linearGradient>
    	//第二个：倾斜渐变，其中x1=111%,是因为我的渐变点拉到了图形之外，所以会超过100%
    
    <linearGradient id="c" x1="111%" x2="22.6%" y1="0%" y2="100%">
      <stop offset="0%" stop-color="#50F0DC"/>
      <stop offset="57.9%" stop-color="#ECB0FF"/>
      <stop offset="100%" stop-color="#2757DD"/>  </linearGradient>
    	//第三个：三点多色渐变，offset 参数就是每个点在渐变轴上的位置。
    
    <linearGradient id="e" x1="74.8%" x2="50%" y1="23.2%" y2="100%">
      <stop offset="0%" stop-color="#50F0DC" stop-opacity="0"/>
      <stop offset="100%" stop-color="#2757DD"/>  </linearGradient>
    	//第五个：透明渐变
    
    <radialGradient id="d" cx="50%" cy="50%" r="63.5%" fx="50%" fy="50%">
      <stop offset="0%" stop-color="#50F0DC"/>
      <stop offset="100%" stop-color="#2757DD"/>  </radialGradient>
    	//第四个：径向渐变，有专门的定义radialGradient
  </defs>
  
  <g fill="none" fill-rule="evenodd">  //此处将定义好的样式 abcde  分别赋予图形
    <path fill="url(#a)" d="M0 0h59v59H0z"/>
    <path fill="url(#b)" d="M91 0h59v59H91z"/>
    <path fill="url(#c)" d="M182 0h59v59h-59z"/>
    <path fill="url(#d)" d="M274 0h59v59h-59z"/>
    <path fill="url(#e)" d="M365 0h59v59h-59z"/>
  </g>
</svg>
```

我们发现，SVG 优化后的代码，重复性的元素会预先定义，重复赋用，十分高效，如果后续设计师再建立相关的矢量图形或样式，建议参考这样的思路，从元素、组件进行建立与维护。

此处我们发现一个问题，渐变的点位出错，整体渐变向中间挤压，形状的长宽比约高，失真越大，呈二次线性变化：即方形或圆形、长宽相同，则点位完全正确；形状约长条状，渐变点位越向中间挤压。

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/MDwdud.png)

研究了一下发现，在 SVG 的坐标系单位中 gradientUnits，默认是基于物体方形边框，以百分比为参数的 objectBoundingBox，因为是基于方形边框，所以长宽比越大，比较短的那一个边的渐变点位，约失真。

>**gradientUnits**，它定义了定义渐变色使用的坐标单位。这个属性有2个可用值：**userSpaceOnUse**和**objectBoundingBox**。
>
>**objectBoundingBox**是默认值，它使用的坐标都是相对于对象包围盒的(方形包围盒，不是方形包围盒的情况比较复杂，略过)，取值范围是0到1。
>
>**userSpaceOnUse**表示使用的是绝对坐标，使用这个设置的时候，你必须要保证渐变色和填充的对象要保持在一个位置。

接着在 Adobe Illustrator 、Figma 中分别导出相应的渐变属性，发现完美适应，并没有失真。查看了一下渐变属性，发现这两家用的坐标系单位均为 userSpaceOnUse ，以像素为单位的绝对单位。

对比这两种方案： 

Sketch 中百分比单位属性，若作为预定义属性，复用于任何尺寸的大小，均能实现符合期望的渐变。

Figma 中像素单位的渐变点，若是复用于其它大小的形状，渐变只会固定于原先大小的位置，不能很好地适配。

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/ksXIYi.png)

由此可见，如果设计软件直出，Figma 、AI 的方式更好，如果用于定义好属性或视觉规范，Sketch 的点位方式更好，并且 Sketch 的这种失真，通过简单的导出算法优化，是可以完全避免的，希望后续有相关更新修复。

#### 阴影

先看看最常见的投影，是如何实现的：

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/ad0obh.png)

```xml
<svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 112 111">
  <defs>
    <filter id="a" width="172.5%" height="172.5%" x="-36.2%" y="-23.8%" filterUnits="objectBoundingBox">
      <feOffset dy="10" in="SourceAlpha" result="shadowOffsetOuter1"/>
      <feGaussianBlur in="shadowOffsetOuter1" result="shadowBlurOuter1" stdDeviation="8"/>
      <feColorMatrix in="shadowBlurOuter1" values="0 0 0 0 0.288433136 0 0 0 0 0.568417171 0 0 0 0 0.966230752 0 0 0 0.5 0"/>
    </filter>
    <rect id="b" width="80" height="80" x="50" y="5" rx="20"/>
  </defs>
  
  <g fill="none" fill-rule="evenodd" transform="translate(-34)">
    <use fill="#000" filter="url(#a)" xlink:href="#b"/>
    <use fill="#2757DD" xlink:href="#b"/>
  </g>
</svg>
```

啧啧，这一串代码，这里用了比较麻烦的实现方式，三个滤镜来实现：

1.feOffset 偏移滤镜：模拟阴影的偏移

2.feGaussianBlur 模糊滤镜：阴影的模糊程度，此处数值是 Sketch 里的一半，因为算的是边界往内 8px，往外 8px，而 Sketch 里统用了16.

3.feColorMatrix 颜色偏移滤镜：用于产生阴影的颜色，这里的数值是一个 4*5 矩阵向量，对于 R、G、B、A 颜色进行偏移操作，看起来是一连串的数字，anyway ，Sketch 中已经帮我们算好了，我们不需要深入了解具体算法。

SVG 中其实有 feDropShadow  滤镜，用于制作投影，只是它并不是原生的滤镜，只是更简便的写法，使用这个滤镜其实就是调用上面三个滤镜，为了代码的简洁和美观性，其实也可以用。

接下来我们看看内阴影的实现方式，不规则内阴影在前端 CSS 样式中一直是个难题（inner box-shadow  只适用于圆角方形），我们看看 SVG 有没有什么骚操作：

```xml
<svg  viewBox="0 0 80 80">
  <defs>
    <filter id="b" width="116.2%" height="116.2%" x="-8.1%" y="-8.1%" filterUnits="objectBoundingBox">
      <feGaussianBlur in="SourceAlpha" result="shadowBlurInner1" stdDeviation="4"/>
      <feOffset dy="5" in="shadowBlurInner1" result="shadowOffsetInner1"/>
      <feComposite in="shadowOffsetInner1" in2="SourceAlpha" k2="-1" k3="1" operator="arithmetic" result="shadowInnerInner1"/>
      <feColorMatrix in="shadowInnerInner1" values="0 0 0 0 0.067486527 0 0 0 0 0.066094982 0 0 0 0 0.546676857 0 0 0 1 0"/>
    </filter>
    
    <rect id="a" width="80" height="80" x="50" y="25" rx="20"/>
  </defs>
  
  <g fill="none" fill-rule="evenodd" transform="translate(-50 -25)">
    <use fill="#2757DD" xlink:href="#a"/>
    <use fill="#000" filter="url(#b)" xlink:href="#a"/>
  </g>
</svg>
```

这里用了四个滤镜来实现，还是比较复杂：

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/wuYWqD.png)

滤镜分别为：feGaussianBlur 模糊、feOffset 偏移、feComposite 叠加处理、feColorMatrix 颜色，此处发现一个问题，导出后阴影的颜色并不准确，明度偏高，饱和度下降，这就是上述案例中整体颜色变粉的原因了，此问题后续再处理；阴影样式已经这么复杂，如果日常作图中，用了多重阴影，会怎样实现，Let's see see:

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/jgMpoH.png)

导出后：

Emm......此处省略一页代码

并没有什么更好的方式去处理，总共叠加了十多个滤镜，进行了多样式的实现，不过整个文件大小压缩后只是 2k ，并没有变的很大，唯一需要担忧的是加载性能这一块，毕竟在以往的理解中，模糊的算法会比较耗性能。

在视觉呈现上我们发现两个问题：

1.并不支持阴影的图层叠加模式：

​	问题不大，不用叠加模式的阴影也可以达到效果；但 Figma 中支持阴影叠加模式。

2.阴影颜色失真，明度偏高，饱和度偏低：

​	原先以为是 feColorMatrix 颜色滤镜，Sketch 导出的参数错了。于是将阴影颜色从 HSB 模式改为 RGB ，并按照算法计算出滤镜的数值，与其对照竟然发现，参数并无错误！于是测试 Figma 输出阴影，发现其颜色显示完全正确，经过两者的样式代码对照，终于发现了问题：颜色模式

​	Figma 中，滤镜设置了颜色模式`color-interpolation-filters="sRGB"`, sRGB 平滑 RGB 模式，我们常用的一种颜色模式，而 Sketch 的滤镜，并无此设置，查了一下，若无设置，颜色模式为 LinearRGB ，线性 RGB 模式，这两者又有什么区别？

> 人类对于灰度的视觉感应，并不是线性的，而是一条曲线。
>
> <img src="https://cdn.jsdelivr.net/gh/Himsann/writing@master/5sRPjr.jpg" style="margin-left:0px;" />
>
> 举个例子，下图是一个从白色到黑色的渐变，于是很自然的，我们会认为中间的位置就是50度灰，也就是俗称的中灰：
>
> <img src="https://cdn.jsdelivr.net/gh/Himsann/writing@master/VIp7dD.jpg" style="margin-left:0;" />
>
> 然而这仅仅是我们的视觉感受是中灰，如果我们把这个灰色放到自然世界里，其物理亮度值大约在白色块的21%左右，**其实已经是相当黑了**。
>
> [颜色模式详解原文](https://www.zhangxinxu.com/wordpress/2017/12/linear-rgb-srgb-js-convert/)

于是为了平衡视觉上的灰度与数学上的灰度，一般使用 sRGB 模式去呈现不同的颜色，Sketch 中也是这种颜色模式，只是在导出阴影的时候，并没有把这个模式定义好，开发小哥的锅，导致用线性 RGB 使得视觉上整体灰度变高了不少，希望后续 Sketch 能把这个问题修复。

#### 遮罩 Mask

前端技术的发展中，遮罩的使用和特殊遮罩的使用，一直有层出不穷的骚操作，甚至在最初圆角属性没出现的时候，用圆角位图+遮罩的方式模拟出圆角。而在 SVG 中，遮罩变成了一个很低成本的实现方式，并且很多时候 HTML 中直接用 SVG 标签加形状实现各种各样的遮罩和图形组合，包括动画。此处我们看看，SVG 的遮罩，其能与不能。

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/ED2K6i.png)

 SVG 代码中，主要用一句话就可以概括：

```xml
<circle cx="67" cy="65" r="35" fill="#E6293F" mask="url(#b)"/>
```

圆形中带有一个 mask 属性，mask 为 url(#b) ,这个 #b  是在头部已经先定义好的蓝色矩形。三个样式中，普通遮罩，透明遮罩都正常显示，唯有Alpha 通道遮罩在 Sketch 里是不支持的。通过查阅，我们发现 SVG 的 mask 中是可以定义 mask-mode 属性为 alpha 的，而 Sketch 中并没有将其属性导出，几个字符的事，开发小哥真是够懒，测试后发现 Figma 的开发小哥勤奋优秀，三种遮罩均完美支持。

如果 sketch 中非要实现这种效果，用 SVG 滤镜功能也可以做到，像上面的内阴影里面就使用了相关的方式，只是这种方式不适合设计师操作，直接 pass。

#### 图层叠加模式

许多视觉样式，都是通过不同的图层叠加做出的效果，设计师在前期学习中，图层叠加模式是绕不开的一关，熟悉使用之后直呼真香，可是往往在前端实现中很少会用到，一方面是兼容性不够好，另一方面是性能方面的担忧；而今两方面我觉得都可以兼顾了，设计师在一些落地方案，可以探索性地去使用，说不定以后会成为另一种视觉落地的康庄大道。

好，我们看看 SVG 中，叠加模式的实现：

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/BhdtAb.png)

```xml
 <g>
    <rect width="65" height="65" y="8" fill="#2757DD" rx="20"/>
    <circle cx="48" cy="26" r="26" fill="#E6293F" style="mix-blend-mode:screen"/>
</g>
```

Perfect!  所有的叠加方式均可以正确展示，并且没有用到 fliter  滤镜，在样式中已经有mix-blen-mode 混合模式进行控制，上面四个分别用了：Screen、multiply、overlay、color，一一对应，其中 color 模式，可以用于设计系统，用一个颜色图层的叠加来控制颜色，google 的 Material Design 下载的 library，就是将颜色全局样式赋予图层叠加到其它元素，进行整体控制，由此可见叠加模式大有可为，大家可以多多尝试。

#### SVG 中的 位图

在使用的过程中，我发现元素中如果含有位图，也可以输出为 SVG 格式，刚开始以为是由 HTML 的 img 标签加载，只是用这种方式需要先把图片存储于本地或者服务器上，通过地址请求进行加载；直到看到文件增大了不少，才发现是“植入”了位图：

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/Artboard.jpg)

```xml
<svg  viewBox="0 0 120 120">
  <rect width="120" height="120" fill="#2757DD" rx="30"/>
  <image width="51" height="54" x="34" y="33" xlink:href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADMA...(此处省略上千个字符)" />
</svg>
```

位图还是用 image  标签加载，后面挂了几十行的字符“乱码”，后面了解到是将图片进行 Base 64 编码转换。

> Base64是网络上最常见的用于传输8Bit字节码的编码方式之一，Base64就是一种基于64个可打印字符来表示二进制数据的方法。

谷歌和百度的解释，对设计师来说简直不是“人话”，可以简单理解为，Base 是一种编码方式，把 3 个 8bit 字节的变成用 4 个 6bit 字节， 反正 3x8=6x4=24 ( 什么鬼)。可以用来编码多种类型的信息，其中包括图片。用其编码图片的好处是，直接可以记录图片信息，不用把图片存放在服务端，因此加载的时候不用进行网络请求，咻的一下就出来了，并且通过这种方式还可以将小图片与文本混合在一起展示。不好的地方是， base64 会大量增加代码量，代码多了，浏览器撑不住， 也不便于维护；图片整体大小会增大，大约为图片原本大小的4/3，增加整体加载的流量。因此我们建议，如果是非常小的位图，可以用这种方式内置，减少加载时间，增加效率。

（配图：服务器请求，对比直接编码转换）

此外还有一种用法，就是作为平铺图案。而矢量图形也可以作为平铺元素，对比矢量图形填充，位图的优势是什么？在此，脑海里冒出了两个词：“材质”与“风格”，在艺术创作到互联网落地的过程，往往是从传统美术通过不同的方式模拟为电子数据，包括现在大部分的设计软件和操作方式，也与之交融，而材质和风格模拟往往是其中的难点，在学些 SVG 样式的过程中，fliter  滤镜和上面的 base 64位图填充的方式似乎可以模拟多种风格，不禁脑洞大开，其中最先想到的是，噪波纹理填充插画，在这两年非常流行，既有纸质纹理又有抽象矢量几何，而这种风格的视觉一般是用位图的方式承载与实现。

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/PIx0x8.png)

此处我们以图中的碗为例子，植入一个 base64 噪点位图平铺作为纹理，再叠加渐变，可以在 sketch 中用形状填充图案制作，最后效果如下，基本可以还原：

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/JmELa1.png)

其中为了突出效果，噪点被加重显示，不过在导出的过程中，阴影样式的色彩依旧无法还原，这边用了复制原图层加模糊的方式制作了阴影。以 base64 图片作为平铺素材，不用向服务器请求图片，并且一整个插画，可以以一个平铺素材重复赋用，极大程度地节省资源并作出效果，值得尝试与扩展。

`在实践过程中，发现 sketch 输出，重复素材并没有整合优化重复赋用，此处需要前端手动修改，或者后面看看其它工具能不能更友好地导出。`

其它材质测试，均以小尺寸纹理填充平铺：

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/v8tSBc.png)

此外还有更好的方式，用滤镜中 feTurbulence 湍流滤镜，type 选择 fractalNoise 噪波模式，可以填充随机的、基于 Perlin噪声算法的噪波，无需填充位图，是最为低成本的实现方式，只不过暂时这块还无法由设计软件直接生成，没想到接入到设计流程的方法，当然，设计师们可以叫感兴趣的前端小哥去实现，其中可能有坑，建议在时间比较宽裕的项目中尝试。

>`feTurbulence`滤镜可以通过应用Perlin噪声算法创建一个噪声文本（1981年，Ken Perlin在他研究TRON的工作期间发明的）。这可以生成一个填充了噪点的矩形，就像你在深夜时看旧电视机（有线电视发明之前）看到的画面。
>
>`著作权归作者所有。商业转载请联系作者获得授权,非商业转载请注明出处。
>原文:https://www.w3cplus.com/svg/why-the-svg-filter-is-awesome.html`

## 工作流程：从设计到落地

### 猜歌案例 SVG 修复

绕了一圈，大家对 SVG 也有了一定的理解，我们回到挂了许久的案例之中，看看问题怎么解决：

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/uPic/Artboard Copy.jpg)

问题与解法如下：

* 遮罩出错：怀疑是 Sketch 的透明遮罩不兼容

  * 原因： SVG 的 mask 中是可以定义 mask-mode 属性为 alpha 的，而 Sketch 中并没有将其属性导出。
  * 解法：将遮罩改为普通遮罩，并将图层填充的颜色透明度设为0：
  * ![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/IDdrZu.png)
  * 设置完看看效果，bingo！
  * ![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/wunpDh.png)

* 整体对比度降低，明度增高：怀疑是颜色色值格式不同或叠加模式问题

  * 原因：Sketch 在导出阴影的时候，颜色模式没有设置为 sRGB，而按照默认值 linearRGB ，会跟人眼视觉产生灰度偏差
  * 解法：十分难解，只能将原本样式中的颜色灰度加深，或者迁移到 Figma 中导出，推荐后者，前者调样式的时间太久，不符合所见所得操作方式。还有一种暴力解法，用“叠加模式”整体叠加一个灰度为20%左右的颜色，使整体明度下降，这种方式会影响到图层填充和描边的样式，只适合用于应急，太粗太暴，不适合斯文人。

* 渐变的颜色位置不正确

  * 原因：Sketch 导出渐变 SVG 的坐标系单位是基于物体方形边框，以百分比为参数的 objectBoundingBox，所以长宽比越大，失真越大。
  * 解法：在长宽比非常大，约为长条形的形状，需要叠加一层正方形图层，并在正方形图层中调整渐变位置。或者迁移到 Figma 中进行导出。

  ![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/89DtyU.png)

最终在 Figma 的帮助下，完美地将样式完全还原，给 Sketch 跪，当其页面落地时候，在手机看效果，特别是高清的平面，成像效果真的非常细腻，细节丰富锐度高，十分舒适。

### 工作流程

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/ybluuC.png)

#### 视觉设计

- 软件端，通过对比，Figma 对 SVG 的支持最好，最为原生，可以无所顾忌地输出，并且它有提供 API 接口，若是要用 SVG 的方式搭建一个设计系统，会非常的有效。
- AI 用于素材处理或复杂插画，也非常高效，记得导出前先转曲。
- 如果用 Sketch ，需要注意以下三点：
  - 1.不要用透明遮罩
  - 2.长宽比过高的图形，渐变要经过处理（见上文）
  - 3.阴影不支持叠加模式，颜色偏低，尽量用复制图层+模糊的方式制作阴影。
- 位图元素，如果非常小，导出会生成 Base64  格式，如果比较大，需要单独处理，以位图元素导出。

#### 页面结构拆分

- 按照背景、中景、前景方式拆分元素，背景可以用渐变加图案填充的方式营造氛围感，相比于位图背景，SVG 制作大面积背景往往成本很低，几 kb 大小就完事儿了。

![](https://cdn.jsdelivr.net/gh/Himsann/writing@master/1cMzVG.png)

- 自适应，SVG 很适合自适应，因为不会失真，不需要用多套图，可以与前端小哥沟通好自适应方式，并且可以直接在 SVG 文件中修改。
- 按钮、视频框、和其它样式整理并导出，若有大面积位图，需要单独处理。
- 一些自定义形状样式，可以跟前端沟通，用 SVG 遮罩的方式：比如心形头像、文字纹理等。
- 整体页面一些样式，可以整体叠加一个 SVG 滤镜，比如水流效果、融球效果等，需要跟前端小哥可以沟通。

#### SVG 输出

- 压缩：有个开源的压缩库 SVGO ，现在基本都用它进行压缩，可以搜索其 Sketch 插件或 Figma 插件，输出的时候自动压缩，不用一张一张去网页端处理，十分方便。
- 如果有动画控制，交互控制，压缩时候不要去除 ID 信息，不然没办法精准控制图层。

#### 前端落地与检查

- 颜色与适配，页面加载速度，可以使用一些网页性能检测网页工具，自动检查其打开速度，流量占用。

## 小结

网上也有更细的，关于 SVG 属性的手册和文章，为什么还要长篇大论细究 SVG 的属性？

技术作为工具，前端和移动端开发在学习的过程中，看到的“我能做什么”，跟设计师看到的是完全两个角度，既然 SVG 可以作为更成熟，更有前景的媒介，我希望设计师从自己的角度，去看到其中的各种可能性，看到了，才会去尝试，并且实现更优更好的表达。

希望大家抱着玩的心态，多多尝试。

下一篇讲 SVG 动画 - 动次打次！



