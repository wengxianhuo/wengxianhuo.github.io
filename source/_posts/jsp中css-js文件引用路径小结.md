---
title: 'jsp中css,js文件引用路径小结'
date: 2016-07-29 16:02:39
tags: js，css引用路径
---
　　今天下午花了不少时间找这方面的资料，自己总结一下。先讲自己已经理清头绪的：相对路径是指，相对当前的jsp页面来说的，也就是说假想当前目录就为此时的jsp页面，要走怎样的路径才可以到达目标js或者css。如果jsp文件与目标js或css在同一级目录，如图：

![同一目录](https://raw.githubusercontent.com/wengxianhuo/pictures/master/same_dir.png)

	大家都知道，assets是存放js，css资源的文件即assets/js和assets/css，为了图片比较简洁，我就不展开assets目录了。

　　此时我们的相对路径应该这么写：assets/js/js文件 或者 assets/css/css文件。原因就是上面说的，对于相对路径，我们假想从当前jsp开始寻找目标资源，在同一级目录，是可以直接反问的，没什么弯路。

但是，还有另一种情况，即：

![同一目录](https://raw.githubusercontent.com/wengxianhuo/pictures/master/other_dir.png)


　　在这种情况下我们当然是没办法像上面一样直接就寻得资源，如图可知道当前jsp在低一级的目录，这时候我们要先找到跑到assets目录才行啊，所以出现了..这样的格式，使用..可以让我们回到上一级目录，即assets的所在目录，都找到assets目录了，自然也可以直接寻得资源，写法是：../assets/js/js文件或../assets/css/css文件
	..有一个特别之处，他会自动往上一级寻找，如果上一级没找到，会寻找上上一级，直到根目录都没有找到assets目录就直接not found了

　　现在我们推荐使用绝对路径就是/project/资源路径的形式，用这种方式出现的错误会比较少吧，感觉上。。。当然了，这里也有特别需要注意的一点就是，你在tomcat中的server配置中的context的path属性设置为什么，那对应的project就是什么。比如`<Context path="/amazeUI" docBase="AmazeUI" reloadable="false" />`那我设置的绝对路径就应该是/amazeUI/assert/js/js文件。

　　如有不正之处，请多多包涵，多多指教。

