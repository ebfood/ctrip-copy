# ctrip移动端首页

通过flex布局为主, 模仿携程首页, 还是学习各大网页的代码来提升自己, 标准自己的代码更快些, 携程的首页使用flex布局, 因此来模仿.

# 搜索栏

## 右半边

思路: 

![image-20210311144214192](https://ebcode.oss-cn-shanghai.aliyuncs.com/img/image-20210311144214192.png)

二倍精灵图,所以用ps缩放一半

![image-20210311151040935](https://ebcode.oss-cn-shanghai.aliyuncs.com/img/image-20210311151040935.png)

![image-20210311151130063](https://ebcode.oss-cn-shanghai.aliyuncs.com/img/image-20210311151130063.png)

窗口 -> 信息 就可以看到当前鼠标坐标

![image-20210311151223940](https://ebcode.oss-cn-shanghai.aliyuncs.com/img/image-20210311151223940.png)

然后写代码

对于小盒子,只需要也是flex, 主轴纵向, 然后全部居中

```css
.search-user{
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  width: 44px;
  height: 44px;
}
```



## 搜索栏

思路: 

左边的放大镜还是精灵图

![image-20210311160325962](https://ebcode.oss-cn-shanghai.aliyuncs.com/img/image-20210311160325962.png)

但是添加了放大镜, 是个block, 把文字挤下去了, 所以, 直接给他个绝对定位让他脱标

```css
.search-bar span::before {
  content: "";
  position: absolute;
  left: 8px;
  top: 6px;
  /* 会获得宽高属性 */
  width: 35px;
  height: 28px;

  background: url(../images/home-common-sprite2x@v7.15.png) no-repeat 0 0;
  background-size: 21px auto;
}
```

![image-20210311161102526](https://ebcode.oss-cn-shanghai.aliyuncs.com/img/image-20210311161102526.png)整体搞定

实现fixed布局就好了

```css
.search-box {
  display: flex;
  align-items: center;
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 44px;
  padding-left: 12px;
  /* background-color: tomato; */
}
```



# 背景图

看原网页的背景图是个圆角, 来实现一下

```css
.focus {
  position: absolute;
  width: 100%;
  height: 180px;
  background: url(../images/banner.jpg) no-repeat center -35px;
  background-size: 100% auto;
  border-bottom-left-radius: 50% 15%;
  border-bottom-right-radius: 50% 15%;
}
```

![image-20210311165828827](https://ebcode.oss-cn-shanghai.aliyuncs.com/img/image-20210311165828827.png)

# local nav

思路: 

+ 要实现压在上图上吗的效果, 给个负数的margin
+ 通过flex布局横向排列, 每个小a在通过flex布局, 设置主轴纵向, 就可以实现
+ 关于背景图的切换, 首先用一个属性选择器选择含有icon-local的设置统一样式, 然后单个选中修改背景图偏移量
  ![image-20210311212306322](https://ebcode.oss-cn-shanghai.aliyuncs.com/img/image-20210311212306322.png)

```css

.local-nav li {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  flex: 1;
}

.local-nav li [class^=icon-local] {
  width: 40px;
  height: 40px;
  background: url(../images/home-fivemain-sprite2x@v7.15.png) no-repeat 0 0;
  background-size: 40px auto;
}

.local-nav li .icon-local-index2 {
  background-position: 0px -40px;
}
```

# nav

思路:

+ ![image-20210311221349733](https://ebcode.oss-cn-shanghai.aliyuncs.com/img/image-20210311221349733.png)
  竖着来一个flex, 三行, 横着来几个flex, flex参数用百分比, 左边那个最大的31%, 小号的23%, 最大号的46%, 分别给个类名就好了
+ 每一行有个色彩渐变,
+ 文字也用flex, nth选择每行第一个特殊处理白边 文字
+ 给小格子添加左边边框
+ 下面的小背景图是用span的背景弄的, 给span一个flex 1 撑满父亲, 然后给背景图
+ 除了那个金色的, 小背景都是直接a上做的, 金色那个是颜色问题, 不坐在span上会覆盖颜色, 这里直接size原版大小, 然后bottom right拼一个, bottom left拼一个 拼成一整个, 挺好玩的![image-20210311234242372](https://ebcode.oss-cn-shanghai.aliyuncs.com/img/image-20210311234242372.png)

```css
/* 具体导航模块 */
.nav {
  overflow: hidden;
  display: flex;
  flex-direction: column;
  height: 200px;
  margin: 0 12px 10px 12px;
  border-radius: 10px;
}

.nav [class^=sub] {
  flex: 1;
  display: flex;
}

.nav .sub1 {
  background: -webkit-linear-gradient(left, #fa5a56, #fb8650)
}

.nav .sub2 {
  border-top: 1px solid #fff;
  border-bottom: 1px solid #fff;
  background: -webkit-linear-gradient(left, #4c8fed, #54bced)
}

.nav .sub3 {
  background: -webkit-linear-gradient(left, #37c2aa, #6bd558)
}

.nav div[class^=sub] {
  display: flex;
}

.nav div[class^=sub] a[class$=middle] {
  flex: 31%;
}

.nav div[class^=sub] a[class$=small] {
  flex: 23%;
}

.nav div[class^=sub] a[class$=big] {
  flex: 46%;
}

/* 给所有a添加一个左边白线 */
.nav a {
  display: flex;
  align-items: center;
  justify-content: center;
  border-left: 1px solid #fff;
  font-size: 14px;
  font-weight: 700;
  color: #fff;
}

.nav span {
  flex: 1;
  text-align: center;
  padding: 22px 0;
}

/* 每行第一个a要特殊处理 */
.nav div[class^=sub] a:first-child{
  border-left: none;
  padding-left: 10px;
  padding-right: 60px;
}

.nav-big {
  background-color: #ffc24b;
}
/* 给特惠单独的背景色 */
#nav-sale {
  flex: 1;
  color: #a05415;
  background: url(../images/grid-nav-items-hot.png) no-repeat 0 0;
  background-size: 100% 100%;
}

.nav .sub1 .nav-middle {
  background: url(../images/grid-nav-items-hotel@v7.15.png) no-repeat bottom right;
  background-size: 73px auto;
}

.nav .sub1 .nav-small {
  background: url(../images/grid-nav-items-minsu@v7.15.png) no-repeat bottom left;
  background-size: 37px auto;
}
```



# double-nav

两行的导航, 唯一注意的就是flex需要给20%, 才能做到五个一行, 剩下的和local-nav一样



# 最终效果

![](https://ebcode.oss-cn-shanghai.aliyuncs.com/img/image-20210312002620722.png)