---
title: 小修改希望提高Blog访问速度
layout: post
guid: urn:uuid:710cb152-b1b1-4457-bf8c-585a0546862f
tags: #blog
  - 
---
这两天也是机缘巧合，先后做了两件事，应该比较明显的提高了小站的访问速度。当然此博客依旧采用jekyll托管在Github上，所做的优化也都是表面功夫。

##引入Instantclick.js##

[Instantclick](http://instantclick.io/)通过预加载的方式，会"~~显著提高~~"（其实是感觉上的）页面的载入速度，只需要引入一个js文件即可，只有25KB哦！

在页面底部插入如下代码：

	...
	<script src="instantclick.min.js" data-no-instant></script>
	<script data-no-instant>InstantClick.init();</script>
	</body>
	</html>
	
还可以有一些细节选择和性能上的调整，参见官方文档。赶紧到处戳戳链接体验一下吧。

##引入七牛CDN进行图片加速##

今日碰巧在V2EX上看到，Google了一下，也很简单。七牛为通过手机验证的用户提供了10G免费存储空间和10G的免费流量，对我来说足够使用了。

有两种方式可以实现图片访问加速。其一为将七牛做为图床。其二为图片依旧放在Github，同时引入七牛的CDN。我采用后者，更方便文件整体备份和将来有可能的搬家活动。我的所有图片都在 `/media/img/` 下。

+ 七牛中建一个**公开访问**的空间。镜像源对应本站图片路径，设为 `http://b.mutinux.com/media/img/`。

+ 修改 Jekyll 下 _config.yml 文件。加入如下一行：

		IMG_PATH: http://yourqiniuname.qiniudn.com
		
+ 之后写个post里如需要插入图片，以 `![Alt text]({{site.IMG_PATH}}/picture.jpg)` 语法完成即可。
