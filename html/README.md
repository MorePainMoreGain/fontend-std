# HTML
尽量遵循 HTML 标准和语义，但是不要以牺牲实用性为代价。任何时候都要尽量使用最少的标签并保持最小的复杂度。


## 语法{#sync}
* 用两个空格来代替制表符（tab） -- 这是唯一能保证在所有环境下获得一致展现的方法。
* 嵌套元素应当缩进一次（即两个空格）。
* 对于属性的定义，确保全部使用双引号，绝不要使用单引号。
* 不要在自闭合（self-closing）元素的尾部添加斜线 -- HTML5 规范中明确说明这是可选的。
* 不要省略可选的结束标签（closing tag）（例如，</li> 或 </body>）。
* 标签没有的属性就不要乱加，例如在`<a>`加上`value`属性

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Page title</title>
  </head>
  <body>
    <img src="images/company-logo.png" alt="Company">
    <h1 class="hello-world">Hello, world!</h1>
  </body>
</html>
```
## 通用{#doctype}
* 为每个 HTML 页面的第一行添加标准模式（standard mode）的声明，这样能够确保在每个浏览器中拥有一致的展现。
* 强烈建议为 html 根元素指定 lang 属性，从而为文档设置正确的语言，有助于语音合成工具确定其所应该采用的发音，以及翻译工具确定其翻译时所应遵守的规则等等。
* 在`<head>`标签里面必须添加`<meta charset="UTF-8">`,定义页面的编码格式
* 在`<head>`标签里面必须添加`<meta http-equiv="X-UA-Compatible" content="IE=edge">`,可以避免IE使用兼容模式


```html
<!DOCTYPE html>
<html lang="ZH">
  <head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  </head>
</html>
```
更多关于 lang 属性的知识可以从 [此规范](http://www.w3.org/html/wg/drafts/html/master/semantics.html#the-html-element) 中了解。

这里列出了[语言代码表](https://www.sitepoint.com/iso-2-letter-language-codes/)。


## 属性顺序{#order}
HTML 属性应当按照以下给出的顺序依次排列，确保代码的易读性。

* `class`
* `id`,
* `name`
* `data-*`
* `src`, `for`, `type`, `href`, `value`
* `title`, `alt`
* `role`, `aria-*`

class 用于标识高度可复用组件，因此应该排在首位。id 用于标识具体组件，应当谨慎使用（例如，页面内的书签），因此排在第二位。
以上的顺序，上一层应该排在下一层的前面，同一层内排序不分先后

## 布尔（boolean）型属性{#boolean}
布尔型属性可以在声明时不赋值。XHTML 规范要求为其赋值，但是 HTML5 规范不需要。
更多信息请参考 [WhatWG section on boolean attributes](http://www.whatwg.org/specs/web-apps/current-work/multipage/common-microsyntaxes.html#boolean-attributes)：
> 元素的布尔型属性如果有值，就是 true，如果没有值，就是 false。
如果一定要为其赋值的话，请参考 WhatWG 规范：
> 如果属性存在，其值必须是空字符串或 [...] 属性的规范名称，并且不要在首尾添加空白符。
**简单来说，就是不用赋值。**

```html
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
  <option value="1" selected>1</option>
</select>
```

## 减少标签的数量
编写 HTML 代码时，尽量避免多余的父元素。很多时候，这需要迭代和重构来实现。请看下面的案例：

```html
<!-- Not so great -->
<span class="avatar">
  <img src="...">
</span>

<!-- Better -->
<img class="avatar" src="...">

```
## 行内样式
* 养成在样式文件`.css`写样式的习惯
* 如果一个样式要重复使用多次，请在style样式文件`.css`中添加样式
* 避免在标签里面写很多的样式，如果需要请在style样式文件`.css`中添加样式
* 只有特例的时候，才可以写行内样式，如css样式已经定义好`.news`的宽度为500，但当前模块只需要450，这种特殊化的情况才可以使用行内样式

**反面教材：**

![错误的CSS方法](style.png)

* 图中的1，2，3标注的地方分别可以用`.red`,`.grey`,`.blue` 在css样式中声明
* 图4要视具体情况，命名一个语义化的`class`，图中的原意是用css写的一个关闭按钮，所以我们可以用`.close`声明


