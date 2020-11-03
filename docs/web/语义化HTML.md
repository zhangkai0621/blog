#### 语义化HTML

### 一，前言
HTML5 新增了很多功能性标签如 video、audio 等多媒体标签，canvas、svg 图像标签，新的表单类型和属性，以及非常多的语义标签。

然而在的日常开发中除了用一些如 `footer`、`header` 等 h5 语义化标签外，其他的基本都是 `div + span` 一梭子全部搞定。快速还原设计稿，并不会感觉有什么不妥。因为在 HTML 语义上面花费太多时间并不会有一个很明显的收益，还可能会被领导误认为在摸鱼。所以语义化的 HTML 在紧张的开发迭代中就这么被忽略了。

### 二，语义化 HTML 的意义
- 语义类标签对开发者更为友好，使用语义类标签增强了**可读性**，即便是在没有 CSS 的时候，开发者也能够清晰地看出网页的结构，也更为便于团队的开发和维护。
- 语义类标签也十分适宜机器阅读。它的文字表现力丰富，更适合**搜索引擎检索**（SEO），也可以让搜索引擎爬虫更好地获取到更多有效信息，有效提升网页的搜索量，并且语义类还可以**支持读屏软件**，根据文章可以自动生成目录等等。


### 三，标签

#### ruby
> 在东亚使用，显示的是东亚字符的发音。
与 `<ruby>` 以及 `<rt>` 标签一同使用

```html
<ruby>
    好<rt> hao </rt>
</ruby>
```
![](https://i.loli.net/2020/10/26/9Xxv2Rz87EFPn3H.png)

#### em
> em 标签告诉浏览器把其中的文本表示为强调的内容。<br>
对于所有浏览器来说，这意味着要把这段文字用斜体来显示。

em 是英文 emphasize 的缩写，意思为强调。

```html
我今天吃了一个<em>苹果</em>
```

我今天吃了一个<em>苹果</em><br>
我<em>今天</em> 吃了一个苹果

> 如果仅仅是为了斜体显示则使用 i 标签

#### strong
> strong 标签和 em 标签一样，用于强调文本，但它强调的程度更强一些。

#### aside
> aside 元素表示一个和其余页面内容几乎无关的部分<br>
被认为是独立于该内容的一部分并且可以被单独的拆分出来而不会使整体受影响。其通常表现为侧边栏或者标注框（call-out boxes）。

- 在 article 元素之外使用作为页面或站点全局的附属信息部分。最典型的是侧边栏，其中的内容可以使友情链接，博客中的其它文章列表、广告单元等。

#### section
> section 元素表示一个包含在HTML文档中的独立部分，它没有更具体的语义元素来表示，一般来说会有包含一个标题。

- section 的嵌套会使得其中的 h1-h6 下降一级

```html
<section>
    <h3>PRC</h3>
    <p>The People's Republic of China was born in 1949...</p>
</section>
```

<section>
  <h3>PRC</h3>
  <p>The People's Republic of China was born in 1949...</p>
</section>



#### article
> article 标签规定独立的自包含内容。<br>一篇文章应有其自身的意义，应该有可能独立于站点的其余部分对其进行分发。

`article` 元素的潜在来源：
- 论坛帖子
- 报纸文章
- 博客条目
- 用户评论

```html
<article>
    <h1>Internet Explorer 9</h1>
    <p>Windows Internet Explorer 9（简称 IE9）于 2011 年 3 月 14 日发布.....</p>
</article>
```

#### header
> 如其名，通常出现在前部，表示导航或者介绍性的内容。

#### footer
> 通常出现在尾部，包含一些作者信息、相关链接、版权信息等。

#### blockquote
> blockquote 之间的所有文本都会从常规文本中分离出来，经常会在左、右两边进行缩进（增加外边距），而且有时会使用斜体。也就是说，块引用拥有它们自己的空间。

```html
<blockquote>
Here is a long quotation here is a long quotation here is a long quotation 
here is a long quotation here is a long quotation here is a long quotation 
</blockquote>
```

<blockquote>
Here is a long quotation here is a long quotation here is a long quotation 
here is a long quotation here is a long quotation here is a long quotation 
</blockquote>


#### time
> time 标签用来表示24小时制时间或者公历日期，若表示日期则也可包含时间和时区。

```html
<p>
    我们在每天早上 <time>9:00</time> 开始营业。
</p>
<p>
    我在 <time datetime="2010-02-14">情人节</time> 有个约会。
</p>
```
<p>
    我们在每天早上 <time>9:00</time> 开始营业。
</p>
<p>
    我在 <time datetime="2010-02-14">情人节</time> 有个约会。
</p>

#### figure
> 用于表示与主文章相关的图片，代码、表格等流内容。


#### pre
> pre 元素表示预定义格式文本。在该元素中的文本通常按照原文件中的编排，以等宽字体的形式展现出来，文本中的空白符（比如空格和换行符）都会显示出来。(紧跟在 pre 开始标签后的换行符也会被省略)

```html
<pre>
    html
  js     css      
</pre>
```
<pre>
    html
  js     css      
</pre>


#### code
> code 元素呈现一段计算机代码。

```html
<code>
    const a = 123
</code>
```

<code>
    const a = 123
</code>

#### var
> var 元素表示数学表达式或编程上下文中的变量。

```html
<code>
<p> 一个简单的方程：<var>x</var> = <var>y</var> + 2 </p>
</code>
```
![](https://i.loli.net/2020/10/26/YytZ5Esd8ARnHVQ.png)


### 四，参考文章
- [掘金-语义化 HTML](https://juejin.im/post/6844903993525665800)<br>
- [HTML语义：div 和 span 是不够用了吗](https://time.geekbang.org/column/article/78158)