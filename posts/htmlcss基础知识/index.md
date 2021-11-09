# html&css基础知识

# meta标签作用

1. 设置网页字符集
2. 设置keywords
3. 设置网页描述信息
4. 网页重定向
5. 设置移动端的视口大小

```html
<!DOCTYPE html>//代表网页版本是HTML5
<html>
<head>
    <meta charset="UTF-8">//charser：设置网页的字符集
    <meta name="viewport" content="width=device-width, initial-scale=1.0">//name：（keywords（网页关键字，给搜索引擎看的），description（站点的主要内容，搜索到之后网页上显示的对网站的描述））指定的数据名称，content：指定的数据的内容
    <meta http-equiv="refresh" content="3;url=http://www.baidu.com">//3秒后跳转
    <title>Document</title>//title标签的内容作为搜索结果的超链接文字内容
</head>
</html>
```

# link和@import的区别

**1.从属关系区别**
`@import`是 CSS 提供的语法规则，只有导入样式表的作用；`link`是HTML提供的标签，不仅可以加载 CSS 文件，还可以定义 RSS、rel 连接属性等。

**2.加载顺序区别**
加载页面时，`link`标签引入的 CSS 被同时加载；`@import`引入的 CSS 将在页面加载完毕后被加载。

**3.兼容性区别**
`@import`是 CSS2.1 才有的语法，故只可在 IE5+ 才能识别；`link`标签作为 HTML 元素，不存在兼容性问题。

**4.DOM可控性区别**
可以通过 JS 操作 DOM ，插入`link`标签来改变样式；由于 DOM 方法是基于文档的，无法使用`@import`的方式插入样式。

**5.权重区别(该项有争议，下文将详解)**
`link`引入的样式权重大于`@import`引入的样式。

# 实体语法

&实体字符；

# 语义化标签

==注意==：

1. 一个网页h1只用一个
2. p中不能放任何块元素

# 结构化语义标签

1. header

   网页头部

2. main

   网页主体，一个网页中只有一个main

3. footer

   网页底部

4. nav

   导航

5. aside

   侧边栏

# 列表

## 无序

ul>li

## 有序

ol>li

## 定义

dl>dt&dd

# 表单

用于提交数据

1. form

   action：用于填写提交数据的url

   提交按钮：input type：submit

2. input //type包含：email,url,date,time,number,tel,search,color,submit,hidden,file(multipe属性：多选)，reset（重置表单值），color

   其他属性：required,placeholder,autofocus(自动聚焦),autocomplete(off/on显示之前输入过的值)

3. 文本框：text

    - name属性相当于提交给服务器时你填写的数据的标识
    - autocomplete：off/on 关注自动补全
    - readonly：只读，会提交
    - disable：禁用，不会提交
    - autofocus：自动获取焦点

4. 单选按钮：radio

    - name相同
    - 必须填写value属性，作为最终的值传递给服务器
    - check：默认选中

5. 多选按钮：checkbox

    - name相同
    - 必须填写value属性，作为最终的值传递给服务器
    - check：默认选中

6. 下拉列表：select>option

    - 必须填写value属性，作为最终的值传递给服务器
    - option中 selected：默认选中

7. textarea

8. button

9. label //for："id"，优化用户体验

10. 其他常用属性

    1. readOnly：只读
    2. disabled：失效
    3. required：必填
    4. value：默认值
    5. maxLength：规定输入字符最大数量
    6. autocomplete：自动补全
    7. autofocus：自动获得焦点

# 表格

```html
<table>
	<thead>
		<tr>//行
			<th></th>//表头
		</tr>
	</thead>
	<tbody>
		<tr>
			<td></td>
		</tr>
	</tbody>
    <tfoot>
        <tr>
            <td></td>
        </tr>
    </tfoot>
</table>
```

合并表格：

1. colspan="x" //合并x列
2. rowspan=“y” //合并y行
3. 先找第几行，第几列开始合并
4. 合并
5. 删除多余行列

表格的样式

```css
table{
	border: 1px solid black; //这里设置的是外围边框
    border-spacing: 0px  //指定边框间的距离(是0时，是两个边框重叠宽度为2)
    border-collapse:collapse; //指定边框的合并（此时边框为1px，不会重叠）
}
td{
	border: 1px solid black //这里设置的是内部边框
}
//表格隔行变色
tr{
    background-color:#xxxxx
}
table tr:nth-child(even){
    background-color:#xxxxx
}
```

==注意==：

1. 表格中没有使用tbody而是直接使用tr，那么浏览器会自动创建一个tbody，并且将tr全部放入tbody中，tr不是table的子元素，所以无法使用table>tr选择tr，要用tbody>tr

2. 默认情况下，元素在td中是垂直居中的。可以通过vertical-align来修改，水平居中用text-align：center

3. 块元素在块元素中的垂直居中方法：

    1. display：table-cell   //将父元素设置为单元格
    2. vertical-align：middle

   水平居中：

    1. 给父元素text-align：center  或者  给子元素margin: 0 auto

# 超链接

1. a中可以放任何元素，除了本身

2. target属性：

   _self 默认值，在当前页面打开超链接

   _blank 在一个新的页面打开超链接

3. 跳转到页面指定位置：href=”#id“

4. 在使用时一般将a标签转为块级元素

# 图片标签

1. alt属性：

   图片无法加载时显示，供搜索引擎寻找

2. title属性：

   鼠标移入显示额外信息

3. 宽高只修改一个，另一个会等比缩放

# 内联框架

iframe

1. 在当前页面中引入其他页面
2. src：要引入的网址
3. frameborder：内联框架边框

# 音视频播放

audio&&video

1. controls属性：

   用户控制播放

2. autoplay属性：

   自动播放

3. loop属性：

   循环播放

==注意==：

1. 默认情况下不允许用户自己控制播放停止
2. 可以用iframe将其他网站的视频放到网页中播放
3. js中用audio.play()开启播放

# 选择器

## 常用选择器

1. 标签选择器
2. id选择器
3. 类选择器

## 复合选择器

1. 交集选择器

   div.xxx//同时满足div和类

2. 并集选择器

   div,p,.xxx

## 关系选择器

1. 子元素选择器

   仅仅是下一层的标签

   ul li>a

2. 后代选择器

   后代中所有的标签

   ul li a

3. 兄弟选择器

   ul li + div //紧接在li后面的div

   ul li ~ div //li后面的所有div

## 属性选择器

1. 标签中含有属性

   input[value]

2. 标签中含有属性且值确定

   input[type="password"]

3. 标签中含有属性且值以xxx开头

   input[class^="icon"]

## 伪类选择器

1. father li:first-child
2. father li:last-child
3. father li:nth-child(3)
4. father li:nth-child(n)//n从0开始，每次+1（-n+4）

==注意==：

先从father的下一层中找第几个，再判断是不是li，如果不是则样式无效

1. father li:nth-of-type(n)

==注意==：

先从father的下一层中判断是不是li，再从是li的里面选择第n个

## 否定伪类选择器

:not()  //除了

```css
.nav-wrapper .nav li:not(:first-of-type):not(:nth-child(9)):not(:nth-child(10)):hover ~ .goods-info
```

## 伪元素

1. ::before //元素的开始
2. ::after //元素的最后
3. ::first-letter //选择第一个字母
4. ::first-letter //选择第一行
5. ::section //选中的内容

==注意==：

::before和::after必须结合content属性来用

## 超链接的伪类

1. a {}或者 a:link{} //未访问
2. a:visited //已访问
3. a:hover //鼠标经过
4. a:active //按下未松开
5. input:foucs //获得焦点得表单元素

## 选择器权重

| 选择器       | 权重                 |
| ------------ | -------------------- |
| 继承/*       | 0，0，0，0           |
| 标签         | 0，0，0，1           |
| 类/伪类/属性 | 0，0，1，0           |
| id           | 0，1，0，0           |
| 行内样式表   | 1，0，0，0           |
| ！imprtant   | 无穷大（在属性后加） |

# 继承

1. 后代会继承祖先的样式
2. 背景布局相关的不会被继承
3. height不会被继承，只能用100%，且必须父亲有高度
4. 视距perspective不会被继承

# 像素和百分比

1. 像素可以看成小点，不同屏幕的像素大小不同，像素越小，屏幕越清晰。所以同样的200px在不同设备下的显示效果就不一样
2. 可以将宽高设置为相对于父元素的百分比

# em和rem

1. 1em=1font-size，是相对于元素字体来算的，默认16px
2. rem是相对于根元素（html）的字体大小来计算的

# 盒子模型

## 块元素

1. 独占一行
2. 默认宽度是父元素的全部，默认高度是内容高度

## 行内元素

1. 不会独占一行，只占自身的大小，一行容纳不下会换到第二行
2. 宽高都由内容决定

## 块元素

1. content：width和height设置的是内容区的大小，设置盒子模型为border-box则是盒子包括padding，border的大小
2. padding
3. border：border-width（上右下左，上 左右 下，上下 左右）,border-style,border-color
4. margin：如果是负值，元素会向相反的方向移动

## 行内元素

1. 不支持设置width和height
2. 可以设置padding，但是垂直方向不会影响布局，只会覆盖
3. 可以设置border，垂直方向不会影响布局
4. 可以设置margin，垂直方向不会影响布局，水平方向不会合并，取和
5. 父元素text-align:center:水平居中

## 行内块元素

1. 可以设置width和height
2. 不会独占一行
3. text-align:center:水平居中
4. vertical-align:middle

==注意==：

1. 行内块之间会有缝隙，是写标签时换行引起的
2. display用来设置标签显示的类型，display：none//元素不显示且不占位置，visibility：hidden//元素不显示但是占位置

## 水平方向布局

子元素的水平content+padding+border+margin之和必须等于父元素的content宽度

- 如果等式不成立，浏览器会自动调整margin-right的值以使得等式成立
- 如果1个值为auto，则自动调整auto的值以使等式成立
- 3个auto，只调整width
- 左右margin为2个auto，则左右外边距对分，所以==子元素在父元素中的水平居中==：width：xxxpx；margin：0 auto

## 垂直方向布局

1. 如果父元素不设置高度，父元素的高度被内容撑开
2. 如果父元素设置了高度，子元素的高度超过了父元素的高度，则会溢出（父元素：overflow:hidden/scroll/auto）

## 垂直外边距的重叠

相邻的垂直方向外边距会发生重叠现象

1. 兄弟元素

   去两者外边距之间的较大值

   特殊情况：如果外边距一正一负取两者的和，如果都是负值，则取绝对值较大的

2. 父子元素

   父子元素间相邻外边距，子元素的会传递给父元素（上外边距）

    - 给父元素加上边框
    - .clearfix::before,.clear::after{content:'';display:table;clear:both}
        1. ::before{content:'';display:table)是为了解决垂直外边距合并的问题
        2. .clear::after(clear:both)是为了解决高度塌陷问题

# 浏览器默认样式

1. *{margin:0,padding:0,list-style:none}

# 盒子的大小

box-sizing

1. content-box:默认值，宽度和高度用来设置内容区大小
2. border-box：宽高设置整个盒子的大小

# 盒子阴影

box-shadow

1. 水平偏移量
2. 垂直偏移量
3. 阴影模糊半径
4. 阴影颜色

# 圆角

border-radius：50%

# 浮动

1. 脱离标准流，所以元素下方还在文档流的元素会自动上移
2. 水平布局等式失效
3. 不会从父元素中移出
4. 浮动元素不会覆盖其他浮动的元素
5. 如果浮动元素上边是一个没有浮动的块元素，则浮动元素无法上移

==特点==：

1. 浮动不会盖住文字（包括行内块，如input），文字会环绕在浮动元素周围

2. 块元素：

    1. 不再独占一行
    2. 宽度不再是全屏，而是宽高随内容撑开

3. 行内元素：

   特点和脱离文档流的块元素一样

# 高度塌陷和BFC

在浮动布局中，父元素没有设置高度，子元素浮动，会导致父元素高度丢失，导致下面的元素上移

解决：

1. 父元素定高度

2. BFC：Block Format Content(块级格式化环境)

    - BFC是css中一个隐藏的属性，为一个元素开启BFC后该元素会变成一个独立的布局区域

    - 元素开启BFC后的特点：

        1. 不会被上面浮动的元素所覆盖
        2. 不会有父子元素间的垂直外边距合并问题
        3. 可以解决高度塌陷问题

    - 开启方法：

      父元素：overflow：hidden

3. clear：见下面

4. 一般用clearfix类，见上面，就是用的clear属性

# clear

作用：清除浮动元素对当前元素产生的影响，后面的元素会上移

1. left：清除左浮动元素对当前元素的影响
2. right：清除右浮动元素对当前元素的影响
3. both：left和right中最大影响的那侧

原理：浏览器会为元素添加margin-top值，以使其位置不受浮动元素影响

解决高度塌陷：

1. 在父元素的最后用::after为元素设置一个没有脱离文档流的盒子，位置在浮动元素的下方
2. 如何到下方，则给伪元素用clear：both，此时父元素需要包住该盒子，则就会有高度了

# 定位

## 相对定位

position：relative

1. 参照于元素在文档流中的位置进行定位的
2. 会提升元素的层级
3. 不会使元素脱离文档流
4. 不会改变元素类型（块，行内）

## 绝对定位

position：absolute

1. 元素脱离文档流,相当于块级盒子脱离文档流，行内元素变成脱离文档流的块元素
2. 会提升元素层级
3. 相对于具有定位的祖先元素进行定位
4. 否则，以html根元素为准

==注意==：

1. 水平居中不能用：margin：0 atuo，需要先设置left和right，此时等式多了两个值。或者先left：50%，再往左自身的一半margin-left：-xxxpx

## 固定定位

position：fixed

1. 是一种特殊的绝对定位，不同的是永远以浏览器的视口进行定位
2. 不占原位置
3. 固定在版心右侧：left：50%，margin-left:版心宽度一半

## 粘性定位

position:sticky

1. 以浏览器伪基准，在元素到达某个位置时将其固定
2. 占有原位置
3. 必须添加left，top其一

==注意==：

1. 添加绝对定位和粘性定位变成行内块元素
2. 浮动定位都不会外边距合并

## 定位堆叠顺序

z-index :   //数值越大越往上

==注意==：

1. 祖先元素的层级再高也不会覆盖后代元素

# 绝对定位元素的水平布局

1. 开启绝对定位后，水平方向多了left和right两个值
2. 当发生过度约束（也就是不满足9个值相加的等式）
    1. 如果9个值中没有auto，则自动调整right值
    2. 有auto，自动调整auto值
3. 可以设置auto值的属性：margin width left right
4. 因为left和right默认值为auto，所以如果不知道left和right，则等式不满足时会自动调整这两个值，如果left和right已经确定，且width为auto则会调整width，如果leftright和width都确定则会调整margin

==注意==：

1. 绝对定位的元素想要水平居中：

    - left：0；right：0
    - 然后设置margin-left和margin-right：auto，此时等式不成立会自动调整auto的值，前提时left和right已经设置了值，否则不会调整margin，无法居中

   ==区别==：

   文档流中居中：margin：0 auto

   绝对定位居中：left：0；right：0；：margin：0 auto

# 绝对定位元素的垂直布局

与文档流中的不同，垂直方向的等式（9个值）也必须满足

所以垂直居中：top：0；buttom：0；margin-top：auto；margin-buttom：auto

# 等式不成立默认调整顺序

前提都为auto

绝对定位：

1. 水平：right->left->width->margin
2. 垂直：buttom->top->width->margin

文档流：

1. 水平：width->margin
2. 垂直：无等式要求

# 字体

1. color
2. font-size
3. font-family
4. @font-face：可以将服务器中的字体直接提供给用户使用
    - font-family：//自己给字体起名
    - src:url() format()；//服务器上字体的路径 字体格式

字体简写：

font：weight style 字体大小/行高 字体族

==注意==：

1. 行高如果不写，会使用默认值

# 图标字体

1. 用font-face的形式对字体进行引入

# 行高

1. 行高指的是文字占有的实际高度
2. 可以通过line-height来设置行高
3. 行高可以直接指定大小，可直接给行高设置整数，如果是整数，则行高是字体大小的倍数（默认1.333）

- 字体框：

  ​	字体存在的格子，设置font-size实际上就是设置字体框的高度

  ​	==行高会在字体框的上下平均分配==

- 字体居中：

  line-height=height

# 文本的水平对齐

text-align：left right center justify（两端对齐）

# 文本的垂直对齐

vertical-align：设置元素垂直对齐

1. baseline：默认值 基线对齐
2. top：顶部对齐
3. bottom：底部对齐
4. middle：居中对齐  注意：是将子元素的中线和字母x的中线对齐

注意：图片的默认对齐方式是基线对齐，会导致下面有空隙，将img的vertical-align设置为top。

# 其他文本样式

1. text-decoration:underline color

    - none
    - underline 下划线
    - line-through 删除线
    - overline 上划线

2. 省略文字

   .xxx{

   ​	white-space：nowrap；//不换行

   ​	overflow：hidden；

   ​	text-overflow：ellipsis；//溢出的内容变成省略号

   }

    1. white-space：设置网页如何处理空白
        - normal
        - nowrap 不换行
        - pre 保留空白（保留多个空白和换行）

# 背景

1. background-color

2. background-image

    - url

3. background-repeat

    - repeat
    - repeat-x
    - repeat-y
    - no-repeat

4. background-position

   九宫格

    - top
    - left
    - right
    - center

   注意：

    1. 注意要写==两个值==（水平和垂直），如果不写就是默认center
    2. 或者使用水平和垂直偏移量

5. background-clip

    1. border-box  //默认值，背景会出现在边框的下边
    2. padding-box  //背景不会出现在边框下边，只出现在内容区和内边距
    3. content-box //背景只出现在内容区

6. background-origin

    1. padding-box  //默认值，图片从内边距左上角开始计算
    2. content-box //图片从内容区左上角开始计算
    3. border-box //图片从边框左上角开始计算

7. background-size

   设置背景图片的大小

    1. 宽度
    2. 高度    //注意：如果只写一个，第二个值等比例缩放
    3. 或者
        1. cover //图片比例不变，将图片铺满盒子（图片可能显示不全）
        2. contain  //图片比例不变，将图片完整显示在盒子中（盒子可能放不满）

8. background-attachment

   背景图片是否跟随元素移动

    1. scroll  //默认值  背景图片会跟随元素移动
    2. fixed  //不会跟随元素移动

==注意==：

1. 背景简写：color url() position no-repeat
2. size必须写在background-position的后边，并且使用/隔开
3. origin必须在clip前面

# 精灵图

通过调整background-positon来改变显示的图片，一次性将多个图片加载进页面，降低请求的次数，加快访问速度

# 渐变

渐变是图片，需要通过background-image来设置

## 线性渐变

颜色沿着一条直线发生变化，线性渐变的开头可以指定渐变的方向

```css
linear-gradient(red,yellow)  //从上往下
linear-gradient(to right,red,yellow)  //从左往右  
// to top left
45deg  //表示旋转的度数
1turn  //表示旋转的圈数

linear-gradient(red,yellow，#ccc,orange)

linear-gradient(red 50px,yellow)  //表示从上到下50px的地方是red最浓的地方
// 表示的是颜色的起始位置，默认红色从0开始，黄色从底部开始，那么渐变的范围就是盒子的高

repeating-linear-gradient(red 50px,yellow 100px)  //渐变的范围是50px
```

## 径向渐变

放射性的效果

- 可以指定径向渐变的==大小==

1. circle  //正圆

2. ellipse  //椭圆

3. closet-side  //只渐变到最近的一条边

   farthest-side  //渐变到最远的一条边

   closet-corner  //最近的一个角

   farthest-side  //最远的一个角

- 可以指定圆心的==位置==

  at center center

```css
background-image: radial-gradient(100px 100px, red, yellow);
background-image: radial-gradient(circle, red, yellow);
background-image: radial-gradient(100px 100px at 0 0, red, yellow);
background-image: radial-gradient(cloest-side at 100px 100px, red, yellow);
```

语法总结：

radial-gradient(大小 at 位置，颜色 位置，颜色 位置，颜色 位置)

# 三角形

1. 宽高为0
2. 三角指向哪里那个边为none
3. 其他边不能为none，否则会影响目标三角形，所以将其他边颜色设置为==transparent==

```css
.app::after{
    border: 10px solid transparent;
    border-top: none;
    border-bottom-color:#ffffff;
}
```

# 局部滚动

overflow:hidden

overflow-y:scroll

# 过渡效果

transition：用于为样式设置过度效果

1. transtion：all 2s  //表示变换所有样式

2. 指定变换样式

   ```css
   高度由0变大，高度为0时设置overflow：hidden
   transition：height 3s//给需要变化样式的元素
   ```

3. transition-property：width，height

4. transtition-duration：0.3s，2s

5. transition-timing-function：

    - ease  //默认值，先加速，后减速
    - linear  //匀速运动
    - ease-in  //加速运动
    - ease-out  //减速运动
    - ease-in-out  //先加速，后减速
    - steps(2，end/start)  //分步执行

6. transition-delay:2s  //过渡效果的延迟执行

7. cubic-bezier() ：贝塞尔曲线来指定

==注意==：

1. 过渡时必须是从一个有效值向另一个有效过渡
2. 在使用translation时，需要变化的值必须有一个初始值，比如要变left，则需要变化的元素必须有一个left属性：left：0。

# 动画

1. 动画和过渡类似，都是可以实现一些动态的效果，不同的是动画是自动触发。
2. 设置动画效果，必须要先设置==关键帧==。关键帧设置了动画执行的每一个步骤。

|                           |                          |                                                              |
| ------------------------- | ------------------------ | ------------------------------------------------------------ |
| @keyframes 名字           | 关键帧                   |                                                              |
| animation-name            | 使用的关键帧名字         |                                                              |
| animation-duration        | 动画的执行时间           |                                                              |
| animation-delay           | 动画的延迟执行           |                                                              |
| animation-timing-function | 动画的执行函数（贝塞尔） |                                                              |
| animation-iteration-count | 动画的执行次数           | inifinite：无限执行                                          |
| animation-direction       | 动画运行的方向           | normal：默认从from到to    reverse：与normal相反    alternate：去从from到to，回来从to到from，即来回执行    alternate-reverse：与alternate相反 |
| animation-play-state      | 动画的执行状态           | running：默认动画执行    paused：动画暂停                    |
| animation-fill-mode       | 动画的填充模式           | none：默认动画执行完毕，元素回到原来的位置    forwards：停在动画结束的位置    backwards：动画开启了delay，在等待时就进入from的状态 |

# 关键帧

```css
        @keyframes ball {
            from{
                margin-top: 0;
            }
            20%,60%,to{
                margin-top: 400px;
                animation-timing-function: ease-out;
            }
            40%{
                margin-top: 100px;
            }
            80%{
                margin-top: 200px;
            }
        }
```

# 变形

1. transform：用来设置元素的变形效果，多个变形效果之间空格隔开
2. 默认是2D变形，如果要显示3D效果，则transform-style：3d，设置在父盒子上

## 平移

1. 变形就是指通过css来改变元素的形状或位置
2. 变形==不会影响页面的布局==

|                    |               |                                                              |
| ------------------ | ------------- | ------------------------------------------------------------ |
| translateX(xxxpx)  | 沿x轴方向平移 | 在平移元素时填百分比，是相对于自身去计算的                   |
| translateY(xxxpx)  | 沿y轴方向平移 |                                                              |
| translateZ (xxxpx) | 沿z轴方向平移 | 首先设置视距（人眼距离网页的距离）：html{ perspective：800px},然后值越大，元素越大，否则没有效果。 |

==注意==：

1. 开启绝对定位的元素，在没有设置宽高时，无法用top：0；bottom：0；left：0；right：0；margin：auto；来进行垂直和水平居中。因为根据等式原则，此时宽高和margin同时为auto，会调整宽高。
2. 利用left：50%；//向右移动包含块宽度的一半，transform：translateX(-50%)；//向左移动自身宽度的一半，此时自身的宽度是被内容撑开的。
3. 配合transition过渡食用更佳
4. 一个元素只有一个transform，否则会覆盖

## 平行四边形

```
transform: skewX(-10deg)
```

## 旋转

1. 可以使元素沿着x，y，z旋转指定角度
2. 可以先旋转后z轴平移，先z轴平移后旋转

|                         |      |                                                              |
| ----------------------- | ---- | ------------------------------------------------------------ |
| rotateZ（xxxdeg/xturn） |      | 中心轴旋转                                                   |
| rotateX（xxxdeg/xturn） |      | 要设置视距，才有近大远小的效果，html {     perspective: 800px; } |
| rotateY（xxxdeg/xturn） |      | 要设置视距，才有近大远小的效果                               |

## 缩放

对元素进行缩放

|          |              |                              |
| -------- | ------------ | ---------------------------- |
| scaleX() | 水平方向缩放 | 放大x倍                      |
| scaleY() | 垂直方向缩放 |                              |
| scaleZ() | z轴方向拉长  | 必须要设置trnsform-style：3d |
| scale()  | 水平和垂直   |                              |

## 变形的原点

trasform-origin

|           |                    |
| --------- | ------------------ |
| center    | 默认值             |
| xxpx xxpx | 自定义变形的起始点 |
|           |                    |

# 计算函数

cale()

可以进行计算，ie9以上支持

# Less

css的预处理语言，浏览器无法直接执行less代码，要执行必须将less转换为css，然后再由浏览器执行

1. 可以嵌套

2. 可以声名变量：直接使用和当类名使用

   ```less
   @a:10px;
   @b:20px;
   @c:box6;
   .box1{
   	width:@a;
   	.box2{
   		width:@b;
   	}
       .@{c}{  //类名
           width:@b;  //直接
       }
   }
   ```

3. 父元素和扩展

    1. &：表示外层的父元素

    2. :extend（）：对当前选择器扩展指定选择器的样式

       ```less
       .p2:extend(.p1){
           color:red;
       }//扩展
       ```

4. 混合函数

   ```less
   .p3{
   	.p1();
   }//将p1的样式混合到p3中
   ```

   使用类选择器时可以在选择器后边添加一个括号，实际上就创建了一个mixins

   ```less
   .p4(){
   	width:100px;
   	height:100px;
   	bgc:red;
   }//这组样式不会显示
   
   .p5{
   	.p4;
   }//这时会显示样式，因为p4只能给别人用
   ```

   使用混合函数可以添加括号定义变量

   ```less
   .test(@w){
   	width:@w;
   	height:100px;
   }
   div{
       //调用混合函数，按顺序传递参数
       .test(200px);
   }
   ```

# 弹性盒

css中的又一种布局手段，它主要用来完成页面的布局，flex可以使元素具有弹性，让元素可以跟随页面大小的改变而改变

## 弹性容器

1. 要使用弹性盒，必须将一个元素设置为弹性容器：display：flex（块级弹性容器）/inline-flex（行内的弹性容器）

|                 |                                  |                                                              |
| --------------- | -------------------------------- | ------------------------------------------------------------ |
| flex-direction  | 弹性元素排列方向                 | row：默认值，由左向右   row-reverse：从右向左    column：纵向（此时纵向为主轴）    column-reverse：从下向上 |
| flex-wrap       | 弹性元素是否在弹性容器中自动换行 | nowrap：默认值，元素不会自动换行    wrap：元素沿着侧轴方向自动换行    wrap-reverse：元素沿着侧轴反方向换行 |
| flex-flow       | direction和wrap的简写属性        | flex-flow：row wrap；                                        |
| justify-content | 主轴上的元素如何排列             | flex-start：元素沿着主轴起边排列    flex-end：元素沿着主轴终边排列    center：元素居中排列，空白都在两侧    space-around：空白分布到元素两侧，所以元素中间的距离是两边的两倍    space-evenly：空白分布到元素单侧，两边和中间的距离相等    space-between：空白均匀分布到元素间，两侧贴边框，没有空白 |
| align-items     | 辅轴上的元素如何排列             | stretch：默认值，将元素的长度设置为相同的值，指的是一行里元素的高度，并不每一行的高度    flex-start：元素不会拉伸，以辅轴起边对齐    flex-end：元素不会拉伸，以辅轴的终边对齐    center：居中对齐   baseline：沿着文字的基线对齐 |
| align-content   | 辅轴上的空间分布                 | center，flex-start：元素都靠上对齐，flex-end，space-around，space-between |

## 弹性元素

1. 弹性容器的子元素是弹性元素
2. 一个元素可以同时是弹性容器和弹性元素

|             |                                                              |                                                              |
| ----------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| flex-grow   | 指定弹性元素的生长系数，当父元素有多余的空间时，子元素如何伸展，父元素的剩余空间会按照比例分配 | 0：默认值                                                    |
| flex-shrink | 指定弹性元素的收缩系数，当父元素的空间无法容纳子元素时，如何对子元素进行收缩，值越大缩的越多 | 0：默认值                                                    |
| flex-basis  | 元素在主轴上的基础长度，会覆盖width。如果主轴是  横向的  则  该值指定的就是元素的宽度，如果主轴是纵向的  则  该值指定的就是元素的高度 | auto：默认值，参考元素自身的高度或宽度，即width和height      |
| flex        | flex：增长  缩减  基础值                                     | initial：默认值，相当于 flex：0 1 auto    auto：相当于 1 1 auto    none：相当于flex：0 0 auto |
| order       | 决定弹性元素的排列顺序                                       | order越小越靠前                                              |
| align-self  | 用来覆盖当前弹性元素上的align-items，和items的可选值一样     |                                                              |

## 主轴

弹性元素的排列方向

## 侧轴

与主轴垂直方向的称为侧轴

# 像素

1. 屏幕是由一个一个发光的小点构成的，这一个个小点就是像素
2. 分辨率：1920*1080就是说屏幕中小点的数量

## 物理像素

1. 上述所说的小点就是物理像素

## css像素

1. 编写网页时，我们所用的像素
2. 浏览器在显示网页时，需要将css像素转为物理像素然后再呈现
3. 一个css像素最终由几个物理像素显示，由浏览器决定。默认情况下在pc端一个css像素=一个物理像素

## 视口

1. 屏幕用来显示网页的区域

2. 可以通过查看视口的大小（看html的盒模型），来观察css像素和物理像素的比值

3. 默认情况下视口宽度1920px（css像素）

   ​					屏幕宽度 1920px（物理像素）

   所以1：1

4. 放大两倍

   视口宽度：960px

   ​                   1920px（物理像素）

   此时，css像素和物理像素的比为1：2

5. 我们可以通过改变视口的大小，来改变css像素和物理像素的比值

## 手机像素

1. 在不同的屏幕，单位像素的大小是不同的，像素越小屏幕会越清晰

2. 大部分情况下，手机的像素点要远远小于计算机的像素点

3. 问题：一个宽度为900px的网页在iphone中如何显示

   默认情况下移动端的网页都会将视口设置为980px，以确保pc端网页可以在移动端正常访问，但是如果网页宽度超过980，移动端浏览器会自动对网页缩放

4. 大部分pc端网站都可以在移动端中正常浏览，但往往不会有一个好的体验

## 完美视口

1. 移动端默认的视口大小是980px（css像素），默认情况下移动端的像素比就是  980/移动端宽度，（980/750）本身移动端像素就小，1个css像素只有0.几的物理像素，就更小了

2. 如果直接在网页中编写移动端代码，在980视口下，像素比会导致网页中的内容非常小

3. 编写移动端页面，必须要确保有一个合理的像素比

   1css像素  对应  2个物理像素,可以通过meta标签来设置视口大小

   ```html
   <meta name="viewport" content="width=device-width，initial-scale=1.0"></meta>//把视口设置为完美视口（一个css像素对应几个物理像素，调整到每个设备推荐的最佳值）
   ```

   视口/物理像素，调整一个css像素包含多少物理像素

4. 每一款移动设备设计时，都会有一个最佳的像素比，一般只需将像素比（视口/屏幕宽度（物理像素））设为该值即可得到一个最佳效果，称为完美视口（达到1：2或者1：3的像素比）

# VW

1. 在移动端开发时不能使用px来进行布局
2. vw表示的是视口的宽度，100vw表示一个视口的宽度
3. vw永远相对于视口宽度进行计算

## vw适配

1. 1 rem = 1 html 字体大小，设计图750px

   ```css
   html{
   	font-size:100vw;
   }
   .box1{
   	width:.5rem;
   }
   ```

2. ```css
   html{
   	font-size:0.13333333333333vw;//字体大小为1px
   }
   .box1{
   	width:750rem;//宽度对应设计图的1px
   }
   ```

   但是网页中字体不能小于12px，所以扩大40倍

   ```css
   html{
   	font-size:5.3333333333333vw;//字体大小为40px
   }
   .box1{
   	width:1.2rem;//1rem=40px（设计图中的像素）
   }
   ```

# 媒体查询

1. 响应式布局的关键，可以为不同的设备，或设备的不同状态来分别设置样式

2. 语法

   ```css
   @media print，screen{
   	body{}
   }
   ```

   | 查询规则 |              |
      | -------- | ------------ |
   | all      | 所有设备     |
   | print    | 打印机       |
   | screen   | 带屏幕的设备 |
   | speech   | 屏幕阅读器   |

3. 可以在查询规则前加only表示仅仅，兼容老版本浏览器

4. min-width：视口的最小宽度

   max-width：视口的最大宽度

   ，：或

   and：与

   not：非

```css
@mdia（min-width：500px00）{//当视口的宽度>500px时生效
	body{
	bgc:red;	
  }
}
```

​	5.断点

![](https://raw.githubusercontent.com/yzuxqz/pic-bed/master/notes-img/%E6%96%AD%E7%82%B9.png)

# 项目中的知识点

1. 一般给body设置min-width来确保网页的最小宽度
2. 一般logo盒子需要设置title，h1标签中需要写官网名字，text-indent：-999px；
3. 宽度100%参考的是包含块的宽度，如果包含块没有设置宽度会自动继承它的包含块的宽度。但是如果包含块开启了绝对定位，那么此时包含块脱离了文档流，宽度不再继承它的包含块，宽度由自身的内容撑开。此时它里面的元素再设置width:100%就不行了，必须先把包含块的宽度确定下来|||||或者给它的祖先开启相对定位，这样绝对定位的又会继承开启了相对定位的祖先元素的宽度
4. input里面存在默认的padding和2px的边框，会影响高度。一般把padding：0，border：none。给父元素设置边框。
5. button默认是border-box,也有默认的border和padding
6. input的轮廓线是focus，不是hover。轮廓线是outline不是border
7. opacity设置元素透明度
8. text-align-last：justify；最后一行文本两端对齐
9. 一般存储在网站的根目录下，名字一般叫做favicon.ico //<link rel="icon" href="./favicon.ico">
10. inline-block不会受前面的浮动元素的影响，会像文字环绕在浮动元素周围
11. 视距perspective无法继承，要么设置在html标签上，在需要3d效果的父元素上设置transform-style：3d，，要么直接将perspective设置在父元素上






