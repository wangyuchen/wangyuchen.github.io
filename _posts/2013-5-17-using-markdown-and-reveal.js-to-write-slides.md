---
layout: post
title: 用Markdown和reveal.js做幻灯片
---

遇到一个小报告要做幻灯片，受了上周R沙龙上看到的可视化报告的影响，就想既然要做，不如做的好看点吧。想起第一次看到的HTML5幻灯片确实很震撼，后来才知道那个模板叫*impress.js*,我以前用过一次google的那个[html5 slides](https://code.google.com/p/html5slides/)，也用过Rmd文件用*pandoc*转成幻灯片, 总觉得各种支持不太好，做起来累，效果也远没有达到令人满意的地步。


这次本来想做个*impress.js*的幻灯片的，但后来想想挺学术的报告，做的那么炫效果不一定好，就又查了查还有什么模板，看到了有人写的一篇[6 Best HTML5/CSS3 Presentation Frameworks](http://zoomzum.com/6-best-html5css3-presentation-frameworks/)，里面就有这个*reveal.js*，想了解这个模板最直接的就是看它的[demo](http://lab.hakim.se/reveal-js/)，我就不多废话了。


- - - 


我觉得这个模板提供的主题和效果都很中规中矩，和ppt与keynote有区别，但又不至于像*impress.js*一样太夸张。有人写了一篇博客总结各大模板写作的难易程度，结论是*impress.js*那个转啊转的效果需要自己设定每张slide的中心，然后在大的画纸上铺开。。想想就对于我们这种美术基础很差的人来说很难啊。


另一个吸引我的点就是他的翻页设计。主要使用的从左到右的翻页加上每一页中可以层叠上下翻页的子页面，有一种天然的目录的效果，提供给讲者对整体演讲框架的把握感。右翻页一次是一个新的小节，这个小节的子页面就都做成下翻页的，讲到底就知道这个小节讲完了，再往右新翻一页就行。ppt里经常会到下一节的标题页出来才开始总结说上一节讲完了，beamer中带着章节提示的模板又太难看。。。另外，iOS上的很多杂志软件似乎就是这种横轴滑动为主，每一节内容又是上下滑动来显示的设计。


- - -


*reveal.js*是一套完整的基于html5，css，javascript的幻灯片模板，可以[从github上下载](https://github.com/hakimel/reveal.js)，下载下来的内容就是之前提到过的那个demo，把index.html打开，每一个`<section>`标签里就是一页幻灯片，你可以尽情对照着html代码和显示效果来把他改成自己的内容。demo里基本上显示了所有的功能，值得一提的是他的theme提供的比demo里介绍的多，可以在theme目录下找到的css都可以用进去作为主题。


好了，最重要的部分。*reveal.js*支持外部markdown文件，在原来的index.html里添加
```
<section data-markdown="example.md" data-separator="^\n\n\n" data-vertical="^\n\n"></section>
```
就能导入用markdown写的幻灯片内容源文件example.md。这行代码里同时设定了三个空行为新的页面，两行为新的子页面，这也完全符合markdown的极简原则，写出来的文档非常清晰，同时markdown的所有语法也都在模板里做了很好的css支持，非常简单就能把幻灯片的主要内容做好。在需要动画效果的地方，在markdown里放入几行html代码就行了。


不过外部markdown源文件的做法，如果你仍然直接打开index.html来看会报错。这是因为外部文件的导入需要一个web服务器来架起这个网站。Mac上从10.8以后没有直接的设置可以开apache了，你可以装mamp或xampp等软件，或者照着如下做法把apache打开：

1. 打开终端
2. 输入如下命令，注意修改里面的USERNAME为你自己Mac上的用户名 (可能需要sudo)：`nano /etc/apache2/users/USERNAME.conf`
3. 添加下面gist里的内容，同样需要改USERNAME，Directory可以不改，或者改成你想要的文件夹地址
	{% gist 5593641 %}
4. 输入如下命令：`sudo apachectl start`
5. 在`~/Sites`或你改的文件夹里放入你的幻灯片，保证index.html在这个文件夹下。打开`localhost/~USERNAME`即可看到你的幻灯片了。

这样做幻灯片的方法简单好用，但是遗憾的是markdown太好写了，幻灯片的内容大部分都局限于quote,list和code，使得幻灯片的内容非常单调，我都根本不高兴多做点效果进去。。但这也带来了好处，就是你必须更加仔细思考每一页幻灯片的内容，然后概括你的观点，把每一个层次的内容用不同的页面展示，基本不会做出需要照着念的幻灯片来。


最后，用HTML5做的目的就是为了能放在自己网站上给人看，我这次做的关于meta—analysis的幻灯片在[http://wangyuchen.github.io/slides/meta-analysis/](http://wangyuchen.github.io/slides/meta-analysis/)。
