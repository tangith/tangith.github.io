---
layout: post
title: 简单布局
description: "几乎包含了你需要的所有的主题：标题、段落、引用、表、代码块等等。"
modified: 2016-11-29
tags: [简单布局]
image:
  feature: abstract-12.jpg
  credit: thisang
  creditlink: https://thisangblog.wordpress.com/
---

下面是所有你需要的主题风格。检查源代码去查看更多嵌入到段落里的元素。

# 一级标题

## 二级标题

### 三级标题

#### 四级标题

##### 五级标题

###### 六级标题

### 正文

Lorem ipsum dolor sit amet, test link adipiscing elit. **This is strong**. Nullam dignissim convallis est. Quisque aliquam.**加粗文字**

这是一段文字这是一段文字这是一段文字这是一段文字这是一段文字这是一段文字这是一段文字这是一段文字这是一段文字这是一段文字这是一段文字

![Smithsonian Image]({{ site.url }}/images/3953273590_704e3899d5_m.jpg)
{: .image-right}

*强调*. Donec faucibus. Nunc iaculis suscipit dui. 53 = 125. Water is H<sub>2</sub>O. Nam sit amet sem. Aliquam libero nisi, imperdiet at, tincidunt nec, gravida vehicula, nisl. The New York Times <cite>cite标签，用来放地址</cite>. <u>下划线</u>. Maecenas ornare tortor. Donec sed tellus eget sapien fringilla nonummy. Mauris a ante. Suspendisse quam sem, consequat at, commodo vitae, feugiat in, nunc. Morbi imperdiet augue quis tellus.

HTML and <abbr title="cascading stylesheets">CSS<abbr> are our tools. Mauris a ante. Suspendisse quam sem, consequat at, commodo vitae, feugiat in, nunc. Morbi imperdiet augue quis tellus. Praesent mattis, massa quis luctus fermentum, turpis mi volutpat justo, eu volutpat enim diam eget metus.

### 引用

> Lorem ipsum dolor sit amet, test link adipiscing elit. Nullam dignissim convallis est. Quisque aliquam.这是引用段落。

## 列表样式

### 有序列表

1. 项目一
   1. 子项目一
   2. 子项目二
   3. 子项目三
2. 项目二

### 无序列表

* 项目一
* 项目二
* 项目三

## 表格

| 表头一 | 表头二 | 表头三 |
|:--------|:-------:|--------:|
| 格1   | 格2   | 格3   |
| 格4   | 格5   | 格6   |
|----
| cell1   | cell2   | cell3   |
| cell4   | cell5   | cell6   |
|=====
| 表尾一   | 表尾二   | 表尾三
{: rules="groups"}

## 代码段

通过 Pygments 语法高亮显示

{% highlight css %}
#container {
  float: left;
  margin: 0 -240px 0 0;
  width: 100%;
}
{% endhighlight %}

{% highlight js %}
var thisang = {
	name:thisang,
	sex:male,
	age:22;
}
{% endhighlight %}

无 Pygments 高亮的代码示例

    <div id="awesome">
        <p>This is great isn't it?</p>
    </div>

## 按钮

应用 `.btn`类,让按钮有更多样式。


{% highlight html %}
<a href="#" class="btn btn-success">Success Button</a>
{% endhighlight %}

<div markdown="0"><a href="#" class="btn">Primary Button</a></div>
<div markdown="0"><a href="#" class="btn btn-success">Success Button</a></div>
<div markdown="0"><a href="#" class="btn btn-warning">Warning Button</a></div>
<div markdown="0"><a href="#" class="btn btn-danger">Danger Button</a></div>
<div markdown="0"><a href="#" class="btn btn-info">Info Button</a></div>
