## css实现水平垂直居中的几种方式
![目标样子](https://img-blog.csdnimg.cn/20190123140158975.png)



总结了一下css实现水平垂直居中比较常用的几种方法

**居中元素宽高固定时的方法**
1. absolute + top:50% left:50% + margin负值
2. absolute + top:0 left:0 right:0 botton:0 + margin:auto
3. absolute + top:calc left:calc

**居中元素宽高未知时的方法**

4. absolute + transform
5. line-height
6. flex布局（移动端布局最常用）
7. css-table

------
##### 第一种：absolute + top:50% left:50% + margin负值

```
<div class="main">
    <div class="box size box1">box1</div>
</div>
```

```
/* 公共样式--start */
*{
    box-sizing:border-box;
}
body{
    padding:50px;
}
.main{	/* main是父元素的类名 */
    width:400px;
    height:400px;
    border:1px solid red;
}
.box{	/* box是子元素的类名 */
    background:green;
    color:#fff;
    font-size:16px;
    padding:10px;
}
.size{	/* size用来表示指定宽度 */
    width:100px;
    height:100px;
}
/* 公共样式--end */

/* 第一种对齐样式：absolute + top50% left50% + margin负值 */
.main{
    position:relative;
}
.box1{
    position:absolute;
    top:50%;
    left:50%;
    margin-top:-50px;
    margin-left:-50px;
}
```
绝对定位的百分比(top50% left50%)是相对于父元素的宽高，通过这个特性可以让子元素居中显示，但是对于绝对定位是基于子元素的左上角，期望的效果是基于子元素的中心居中显示。
为了修正这个问题，可以借助外边距的负值，负的外边距可以让元素向相反的方向定位，通过指定子元素的外边距为子元素宽度(或高度)一半的负值，就可以让子元素居中了。

🆚 很常用，容易理解兼容性也很好。缺点是需要已知子元素的宽高。

##### 第二种：absolute + top:0 left:0 right:0 botton:0 + margin:auto

```
<div class="main">
    <div class="box size box2">box2</div>
</div>
```

```
/* 此处还需引用上面的公共样式代码 */

/* 第二种：absolute + top:0 left:0 right:0 botton:0 + margin:auto */
.main{
    position:relative;
}
.box2{
    position:absolute;
    top:0;
    left:0;
    right:0;
    bottom:0;
    margin:auto;
}
```
通过绝对定位子元素，并且在各个定位方向的距离上都设为0，此时再将margin设为auto，就可以让子元素居中显示了。

🆚 比较常用，兼容性较好。缺点是需要已知子元素的宽高。

##### 第三种：absolute + top:calc left:calc

```
<div class="main">
    <div class="box size box3">box3</div>
</div>
```

```
/* 此处还需引用上面的公共样式代码 */

/* 第三种：absolute + top:calc left:calc */
.main{
    position:relative;
}
.box3{
    position:absolute;
    top:calc(50% - 50px);
    left:calc(50% - 50px);
}
```
css3出现了计算属性calc，这样我们就可以用第一种方法的思维加上calc来实现水平垂直居中的实现。

🆚 不怎么常用，兼容性需要依赖[calc的兼容性](https://www.css88.com/book/css/values/functional/calc%28%29.htm)。缺点是需要已知子元素的宽高。

##### 第四种：absolute + transform
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190123151158668.png)
```
<div class="main">
    <div class="box box4">box4</div>
</div>
```

```
/* 此处还需引用上面的公共样式代码 */

/* 第四种：absolute + transform */
.main{
    position:relative;
}
.box4{
    position:absolute;
    top:50%;
    left:50%;
    transform: translate(-50%, -50%);
}
```
原理同第一种方法，不过使用了css3新增的transform可以不必已知子元素的宽高。transform的translate属性也可以设置百分比，它是相对于自身的宽高，所以可以在不知道子元素宽高的情况下设置translate(-50%,-50%)，就可以让子元素向相反方向移动自身宽高的一半，继而实现水平垂直居中。

🆚 很常用，兼容性需依赖[transform(2D)的兼容性](http://www.runoob.com/cssref/css3-pr-transform.html)。

##### 第五种：line-height
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190123151747344.png)
```
<div class="main">
    <div class="box box5">box5</div>
</div>
```

```
/* 此处还需引用上面的公共样式代码 */

/* 第五种：line-height */
.main{
     text-align: center;
     line-height: 400px;
     font-size:0;
 }
 .box5{
     font-size:16px;
     line-height: initial;
     display: inline-block;
     vertical-align: middle;
 }
```
利用行内元素居中的属性实现水平垂直居中，关键点父元素设置text-align:center并且父元素高度固定并设置line-height:400px，子元素设置为内联元素并且vertical-align:middle，line-height:initial。

🆚 不常用，实际使用中限制比较多。

##### 第六种：flex
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190123152750297.png)

```
<div class="main">
    <div class="box box6">box6 box6 box6</div>
</div>
```

```
/* 此处还需引用上面的公共样式代码 */

/* 第六种：flex */
.main{
     display: flex;
     justify-content: center;
     align-items: center;
 }
 .box6{
     
 }
```
flex作为现代的布局方案，颠覆了过去的经验，只需要几行代码就可以优雅的做到水平垂直居中。点这里查看[flex详解](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)

🆚 很常用，目前移动端已经完全可以使用flex了，PC端需要看自己业务的兼容情况。

##### 第七种：css-table
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190123153926799.png)

```
<div class="main">
    <div class="box box7">box7 box7</div>
</div>
```

```
/* 此处还需引用上面的公共样式代码 */

/* 第七种：css-table */
.main{
    display: table-cell;
    text-align: center;
    vertical-align: middle;
}
.box7{
    display: inline-block;
}
```
css新增的table属性，可以让我们把普通元素，变为table元素的现实效果，通过这个特性也可以实现水平垂直居中，这个属性和table标签一样的居中原理。

🆚 不太常用，没有冗余代码，兼容也还不错。


> 参考博文
> https://yanhaijing.com/css/2018/01/17/horizontal-vertical-center/

