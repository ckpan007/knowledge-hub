# 一秒钟把Github项目变成前端网站

GitHub Pages大家可能都知道，常用的做法，是建立一个gh-pages的分支，通过setting里的设置的GitHub Pages模块可以自动创建该项目的网站。

这里经常遇到的痛点是，master遇到变更，经常需要去sync到gh-pages，特别是纯web前端项目，这样的痛点是非常地痛。

Github官方可能嗅觉到了该痛点，出了个master当作网站是选项，太有用了。

![Image 1](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/git/image-1.jpg)


选择完master branch之后，master自动变成了网站。master所有的提交会自动更新到网站。

# 精准分享关键代码

比如你有一个文件里的某一行代码写得非常酷炫或者关键，想分享一下。

可以在url后面加上#L行号

比如，点击下面这个url：

https://github.com/AlloyTeam/AlloyTouch/blob/master/alloy_touch.js#L240
你便会跳到alloy_touch.js的第240行。

![Image 2](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/git/image-2.jpg)

那么问题来了？如果我是一段代码，即多行代码想分享呢？也很简单：url后面加上 #L开始行号-L结束行号

比如，AlloyTouch的运动缓动和逆向缓动函数如下面代码段所示：

https://github.com/AlloyTeam/AlloyTouch/blob/master/alloy_touch.js#L39-L45
其实也不用记忆你直接在网址后面操作，github自动会帮你生成url。比如你点击39行，url变成了

https://github.com/AlloyTeam/AlloyTouch/blob/master/alloy_touch.js#L39
再按住shift点击45行，url变成了

https://github.com/AlloyTeam/AlloyTouch/blob/master/alloy_touch.js#L39-L45
然后你这个url就可以复制分享出去了，点击这个url的人自动会跳到39行，并且39-45行高亮。

![Image 3](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/git/image-3.jpg)

# 通过提交的msg自动关闭issues

比如有人提交了个issues https://github.com/AlloyTeam/AlloyTouch/issues/6
然后你去主干上改代码，改完之后提交填msg的时候，填入：

fix  https://github.com/AlloyTeam/AlloyTouch/issues/6
这个issues会自动被关闭。当然不仅仅是fix这个关键字。下面这些关键字也可以：

close
closes
closed
fixes
fixed
resolve
resolves
resolved

# 通过HTML方式嵌入Github

如下面所示，user和repo改成你想要展示的便可以

 <iframe src="//ghbtns.com/github-btn.html?
user=alloyteam&repo=alloytouch&type=watch&count=true"
allowtransparency="true"
frameborder="0" scrolling="0"
width="110" height="20">
</iframe>
插入之后你便可以看到这样的展示：

![Image 4](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/git/image-4.jpg)

# gitattributes设置项目语言

![Image 5](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/git/image-5.jpg)

如上图所示，github会根据相关文件代码的数量来自动识别你这个项目是HTML项目还是Javascript项目。

这就带来了一个问题，比如AlloyTouch最开始被识别成HTML项目。

因为HTML例子比JS文件多。怎么办呢？gitattributes来帮助你搞定。在项目的根目录下添加如下.gitattributes文件便可

https://github.com/AlloyTeam/AlloyTouch/blob/master/.gitattributes
里面的：

*.html linguist-language=JavaScript
主要意思是把所有html文件后缀的代码识别成js文件。

# 查看自己项目的访问数据

在自己的项目下，点击Graphs，然后再点击Traffic如下所示：

![Image 6](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/git/image-6.jpg)

里面有Referring sites和Popular content的详细数据和排名。如：Referring sites

![Image 7](https://github.com/HuangMarco/knowledge-hub/blob/dev/zResources/git/image-7.jpg)

其中Referring sites代表大家都是从什么网站来到你的项目的，Popular content代表大家经常看你项目的哪些文件。

# trending排行榜

上面教大家设置语言了，下面可以看看怎么查看某类型语言的每日排行榜。比如js每日排行榜：

https://github.com/trending/javascript?since=daily
https://github.com/trending/html?since=daily
https://github.com/trending/css?since=daily

Github推荐：https://github.com/explore

# 其他

issue中输入冒号 : 添加表情
任意界面，shift + ？显示快捷键
issue中选中文字，R键快速引用
