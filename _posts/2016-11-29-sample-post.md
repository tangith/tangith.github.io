---
layout: post
title: "一篇包含图片的文章"
description: "在文章中显示图片的例子和代码。"
tags: [sample post, images, test, 图片]
---

下面是一些一篇文章中包含图片的例子。如果你想用带各种类的`figure`标签响应式的并列显示两或三张图片。每个`figure`自动编号并且展示在标题。

## Figures (for images or video)

### One Up

<figure>
	<a href="http://farm9.staticflickr.com/8426/7758832526_cc8f681e48_b.jpg"><img src="http://farm9.staticflickr.com/8426/7758832526_cc8f681e48_c.jpg" alt=""></a>
	<figcaption><a href="http://www.flickr.com/photos/80901381@N04/7758832526/" title="Morning Fog Emerging From Trees by A Guy Taking Pictures, on Flickr">Morning Fog Emerging From Trees by A Guy Taking Pictures, on Flickr</a>.</figcaption>
</figure>

### Two Up

应用`.href`类并排显示两张图片，它们的标题是一样的。

```html
<figure class="half">
	<img src="/images/image-filename-1.jpg" alt="">
	<img src="/images/image-filename-2.jpg" alt="">
	<figcaption>Caption describing these two images.</figcaption>
</figure>
```

你会得到下面这样的效果：

<figure class="half">
	<a href="http://placehold.it/1200x600.jpg"><img src="http://placehold.it/600x300.jpg" alt=""></a>
	<a href="http://placehold.it/1200x600.jpg"><img src="http://placehold.it/600x300.jpg" alt=""></a>
	<img src="http://placehold.it/600x300.jpg" alt="">
	<img src="http://placehold.it/600x300.jpg" alt="">
	<figcaption>Two images.</figcaption>
</figure>

### Three Up

应用`.third`类并排显示三张图片，它们的标题是一样的。


```html
<figure class="third">
	<a href="http://placehold.it/1200x600.jpg"><img src="http://placehold.it/600x300.jpg" alt=""></a>
	<a href="http://placehold.it/1200x600.jpg"><img src="http://placehold.it/600x300.jpg" alt=""></a>
	<a href="http://placehold.it/1200x600.jpg"><img src="http://placehold.it/600x300.jpg" alt=""></a>
	<figcaption>Caption describing these three images.</figcaption>
</figure>
```

你会得到下面的效果：

<figure class="third">
	<a href="http://placehold.it/1200x600.jpg"><img src="http://placehold.it/600x300.jpg" alt=""></a>
	<a href="http://placehold.it/1200x600.jpg"><img src="http://placehold.it/600x300.jpg" alt=""></a>
	<a href="http://placehold.it/1200x600.jpg"><img src="http://placehold.it/600x300.jpg" alt=""></a>
	<a href="http://placehold.it/1200x600.jpg"><img src="http://placehold.it/600x300.jpg" alt=""></a>
	<a href="http://placehold.it/1200x600.jpg"><img src="http://placehold.it/600x300.jpg" alt=""></a>
	<a href="http://placehold.it/1200x600.jpg"><img src="http://placehold.it/600x300.jpg" alt=""></a>
	<figcaption>Three images.</figcaption>
</figure>

### Alternative way 供选择的方式

另外一种实现相同效果的方式是引入`gallery`瀑布流模板。用这种方式，你不需要写任何 HTML 标签，只需要复制一小块代码，调整参数（见下文），用任意数量的图片链接填充内容块。相对路径和绝路径可以混合使用。

下面是你可能会使用到的代码块：

```liquid
{% raw %}{% capture images %}
	/images/abstract-10.jpg
	/images/abstract-11.jpg
	http://upload.wikimedia.org/wikipedia/en/2/24/Lenna.png
{% endcapture %}
{% include gallery images=images caption="Test images" cols=3 %}{% endraw %}
```

参数：

- `caption`: 设置在 gallery 下方的标题（见上方`figcaption`HTML 标签）;
- `cols`: 设置瀑布流的列数。可用的值为: [1..3]。

下面是效果：

{% capture images %}
	/images/abstract-10.jpg
	/images/abstract-11.jpg
	http://upload.wikimedia.org/wikipedia/en/2/24/Lenna.png
{% endcapture %}
{% include gallery images=images caption="Test images" cols=3 %}
