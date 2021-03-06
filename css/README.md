# CSS
> 我们力求让所有人维护css的时候，都不用打开`F12`控制台，调试代码的出处，不用`Ctrl+F`查找代码的位置；我们要通过我们的双眼发现问题的所在，提高维护效率。这必然要对我们的css编码提出要求。

## 通用{#common}

+ 用两个空格来代替制表符（tab） -- 这是唯一能保证在所有环境下获得一致展现的方法。
+ 三级之内禁止用标签名作为css选择器
+ 块元素标签名尽量不要直接用作选择器,但行内元素可以

## 语法一 选择器{#sync1}

+ 如果是选择器分组，每个选择器应该独立一行以`,`结尾；
+ 使用单行规则声明，每个选择器的声明应该尽量在一行，这么做是为了更易于维护；
+ 如果一行没办法放下所有的声明，那么第二行的第一个声明应该与第一行的第一个声明对齐。
+ 为了代码的易读性，在每个声明块的左花括号`{`前添加一个空格。
+ 对于多行声明的选择器,其结束的右花括号`}`应该独立一行，单行声明则不需要

```css
/* Bad CSS */
.selector, .selector-secondary, .selector[type=text] {
    padding:15px;
    margin:0px 0px 15px;
    background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0px 1px 2px #CCC,inset 0 1px 5px rgba(0, 0, 0, 0.2);
    }

/* Good CSS */
.selector,
.selector-secondary {padding: 15px;margin-bottom: 15px;background-color: rgba(0,0,0,.5);
                     box-shadow: 0 1px 2px #ccc, inset 0 1px 5px rgba(0,0,0,0.2);
}
```

## 语法二 属性声明{#sync2}

+ 每条声明语句的 `:` 后应该插入一个空格。

+ 十六进制值应该全部小写，例如，#fff。在扫描文档时，小写字符易于分辨，因为他们的形式更易于区分。
+ 尽量使用简写形式的十六进制值，例如，用 #fff 代替 #ffffff。

+ 对于属性值或颜色参数，省略小于 1 的小数前面的 0 （+ 如，.5 代替 0.5；-.5px 代替 -0.5px）。
+ 避免为 0 值指定单位，例如，用 margin: 0; 代替 margin: 0px;

+ 为选择器中的属性添加双引号，例如，input [type="text"]。只有在某些情况下是可选的，但是，为了代码的一致性，建议都加上双引号。
+ 对于以逗号分隔的属性值，每个逗号后面都应该插入一个空格（例如，box-shadow）。
+ 不要在 rgb()、rgba()、hsl()、hsla() 或 rect()+ 值的内部的逗号后面插入空格。这样利于从多个属性值（既加逗号也加空格）中区分多个颜色值（只加逗号，不加空格）。
+ 所有声明语句都应当以分号结尾。最后一条声明语句后面的分号是可选的，但是，如果省略这个分号，你的代码可能更易报错。


```css
.selector[type="text"] {padding: 15px;margin-bottom: 0 15px;background: rgba(0,0,0,.5) no-repeat;
                        box-shadow: 0 1px 2px #bbb, inset 0 1px 5px rgba(0,0,0,0.2);
```
## 声明顺序{#order}
**相关的属性声明应当归为一组，并按照下面的顺序排列：**

     Positioning
     Box model
     Typographic
     Visual

由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box model）相关的样式，因此排在首位。盒模型排在第二位，因为它决定了组件的尺寸和位置。

其他属性只是影响组件的内部（inside）或者是不影响前两组属性，因此排在后面。

完整的属性列表及其排列顺序请参考 [Recess](http://twitter.github.io/recess/)。

```css
.declaration-order {
  /* Positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* Box-model */
  display: block;
  float: right;
  width: 100px;
  height: 100px;

  /* Typography */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;

  /* Visual */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  /* Misc */
  opacity: 1;
}
```
注：上面的语法只是方便属性的归类用，实际应该采用单行的语法规则，具体参考上文提到的[语法](#sync1)一节
## 带前缀的属性{#prefix}
当使用特定厂商的带有前缀的属性时，每个属性必须独立成行，通过缩进的方式，让每个属性的值在垂直方向对齐，这样便于多行编辑。不带前缀的属性必须写在最后。

```css
/* Bad CSS */
.selector {
    -ms-box-shadow:0px 1px 2px #CCC,inset 0 1px 5px rgba(0, 0, 0, 0.2);
  -webkit-box-shadow:0px 1px 2px #CCC,inset 0 1px 5px rgba(0, 0, 0, 0.2);
   box-shadow:0px 1px 2px #CCC,inset 0 1px 5px rgba(0, 0, 0, 0.2);
  -moz-box-shadow:0px 1px 2px #CCC,inset 0 1px 5px rgba(0, 0, 0, 0.2);
  -o-box-shadow:0px 1px 2px #CCC,inset 0 1px 5px rgba(0, 0, 0, 0.2);  
 
    }
    /* Good CSS */
.selector{
  -webkit-box-shadow: 0px 1px 2px #CCC, inset 0 1px 5px rgba(0,0,0,0.2);
     -moz-box-shadow: 0px 1px 2px #CCC, inset 0 1px 5px rgba(0,0,0,0.2);  
      -ms-box-shadow: 0px 1px 2px #CCC, inset 0 1px 5px rgba(0,0,0,0.2);
       -o-box-shadow: 0px 1px 2px #CCC, inset 0 1px 5px rgba(0,0,0,0.2);
          box-shadow: 0px 1px 2px #CCC, inset 0 1px 5px rgba(0,0,0,0.2);
   
}
```
## 简写形式的属性声明{#short}
应当尽量限制使用简写形式的属性声明,除非在需要显式地设置所有值的情况下。常见的滥用简写属性声明的情况如下：
* `padding`
* `margin`
* `font`
* `background`
* `border`
* `border-radius`
大部分情况下，我们不需要为简写形式的属性声明指定所有值。例如，HTML 的 heading 元素只需要设置上、下边距（margin）的值，因此，在必要的时候，只需覆盖这两个值就可以。过度使用简写形式的属性声明会导致代码混乱，并且会对属性值带来不必要的覆盖从而引起意外的副作用。

在 MDN（Mozilla Developer Network）上一篇非常好的关于 [shorthand properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties) 的文章，对于不太熟悉简写属性声明及其行为的用户很有用。

## class命名{#class}

* class 名称中只能出现小写字符和破折号（dashe）（不是下划线，也不是驼峰命名法）。破折号应当用于相关 class 的命名（类似于命名空间）（例如，.btn 和 .btn-danger）。
* 避免过度任意的简写。.btn 代表 button，但是 .s 不能表达任何意思。
* class 名称应当尽可能短，并且意义明确。
* 使用有意义的名称。使用有组织的或目的明确的名称，不要使用表现形式（presentational）的名称。
* 当有通用意义的class时，基于最近的父 class 或基本（base） class 作为新 class 的前缀，例如新闻的header`.header`应该是`.news-header`。
* 使用 data-act 来标识行为（与样式相对），并且不要将它包含到 CSS 文件中

```css

/* Bad example */
.t { ... }
.red { ... }
.header { ... }

/* Good example */
.tweet { ... }
.important { ... }
.tweet-header { ... }
```

## 选择器{#selector}
* 对于通用元素使用 class ，这样利于渲染性能的优化。
* 对于经常出现的组件，避免使用属性选择器（例如，[class^="..."]）。浏览器的性能会受到这些因素的影响。
* 选择器要尽可能短，并且尽量限制组成选择器的元素个数，一般是3个左右，建议不要超过 5 。
* 尽量不要使用标签作为选择器,三级之内禁止用标签名作为css选择器

```css

/* Bad example */
.page-container  .stream-item .tweet .tweet-header .username { ... }
.txt span {...}


/* Good example */
.page-container .tweet-header .username { ... }
.txt .name {...}
```

## 代码组织{#organization}
* 以组件为单位组织代码段。
* 按组件注释使用`/*=======================组件名称=========================*/`注释。
* 组件注释应该距离上一个组件代码留两行空行，然后紧接模块代码不留空行。
* 组织组件代码时，必须要有命名空间，统一第一个class名称
* 组件样式与页面样式要分离
* 组件内部允许有子组件子模块的注释`/* 子模块 */`，此注释距离上一模块留一行空行，然后紧接模块代码。
* 组件内的css就算不区分子模块，也建议合理空行，增加代码的可读性

```css
/* Bad example */
.subTit{font-size: 22px;color: #333;}
.subTit span.tip button{vertical-align:middle;width:36px;}
.inputText{font-size: 14px;text-indent: 10px;}
.article .subTit {color: #999;}
/* good example */

/*==============================块状form表单=============================*/
.form-block .subTit {font-size: 22px;color: #333;}
.form-block .subTit span.tip button{vertical-align:middle;width:36px;}
.form-block .inputText {font-size: 14px;text-indent: 10px;}


/*==============================环球首页=============================*/
.article .form-block .subTit {font-size: color: #999;}//页面样式与上面组件样式分离

/* 新闻模块 */
.article .news {padding: 0 15px;}


/*==============================环球详情页=============================*/
...
/* 新闻模块 */
.article-detail .news {padding: 0 15px;}

```

## 注释{#note}
代码是由人编写并维护的。请确保你的代码能够自描述、注释良好并且易于他人理解。好的代码注释能够传达上下文关系和代码目的。不要简单地重申组件或 class 名称。

对于较长的注释，务必书写完整的句子；对于一般性注解，可以书写简洁的短语。

```css

/* Bad example */

.header {……}
/*页脚*/
.footer {……}

/* Good example */

.header {……}


/*==================页脚====================*/

.footer {……}
```

## scss{#scss}
* 与css代码一样尽量单行排列，单行放置不完第二行要左对齐选择符`{`后的第一个属性
* 嵌套的选择器要缩进2个字符，要有明显的层级关系

```scss
.home-index {position: relative;...
             font-size: 14px;
  .head {padding: 10px;}
}
```
## 图片{#img}
* 在css中引用的图片一般使用相对路径
* 对于css中使用的图片一般小于20k的，要使用图片精灵
* ps切图导出要用web格式，严禁直接导出png。根据具体情况，选择合适的图片格式，尽量使得图片的大小尽可能小，而又不失真。最大100k左右

## 范本{#example}
这个是css规范的一个例子，可以用作平常写css的参考

```css

/*=====================branner 样式 ========================*/
.banner {padding: 30px 0;background: #fff;position: relative;}
.banner .list {width: 1200px;height: 300px;overflow: hidden;}
.banner .list .item {float: left;display: inline;}
.banner .points {width: 100%;text-align: center;position: absolute;bottom: 35px;}
.banner .points span {width: 12px;height: 12px;display: inline-block;border-radius: 12px;background: #fff;opacity: 0.6;margin: 0 5px;cursor: pointer;}
.banner .points span:hover {opacity: 1;}

/*swiper banner 样式*/
.swiper-banner {width: 1200px;height: 300px;padding: 30px 0;border-radius: 5px;}
.swiper-banner .swiper-slide {background-position: center;}
.swiper-banner .swiper-pagination-bullet {width: 12px;height: 12px;background: #fff;}
.swiper-banner .swiper-pagination-bullet-active {background-color: #2c81ff;}


/*=====================微信支付弹窗样式========================*/
.wx-pay {width: 740px;height: 438px;}
.wx-pay .left,
.wx-pay .right {float: left;width: 50%;}
.wx-pay .left .head {padding: 15px 0 25px;text-align: center;font-size: 18px;}
.wx-pay .left .head strong {color: #3a94f6;}
.wx-pay .left .code-wrap {width: 250px;margin: 0 auto; border: 1px solid #f5f5f5;text-align: center;}
.wx-pay .left .code-wrap .code {width: 100%;height: 250px;}
.wx-pay .left .code-wrap .tip {background: #f5f5f5;color: #3a94f6;font-size: 12px;}
.wx-pay .left .code-wrap .tip:before {content:"";display: inline-block;width: 15px;height: 15px;margin-right: 8px;background: url(/static/home/style/images/right_sidebar.png) no-repeat;background-position: 0 -23px;background-size: 35px;vertical-align: text-top;}

.wx-pay .right {position: relative;}


/*=====================支付成功样式========================*/
.success-main {padding: 55px 0 170px;margin-bottom: 30px;text-align: center;background: #fff;}
.success-main .wrap{display: inline-block;}
.success-main .pay-sprite {float: left;}
.success-main .sprite-ok { background-position: 0 -37px; height: 60px; width: 60px; }
.success-main .sprite-ok2 { background-position: 0 -102px; height: 80px; width: 80px; }
.success-main .cont {display: inline-block;margin-left: 30px;margin-top: 16px;text-align: left;}
.success-main .cont h3 {margin-bottom: 5px;}

```


