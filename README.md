# mansory 布局中，都会遇到动态改变某个视图的显示隐藏
![](http://p1.bqimg.com/567571/b4f57f8e4a16f83c.png)


此时redView，yellowView，greenView 纵向间隔都是30个点，此时若控制yellowView隐藏，那么greenView顶部距离redView的底部距离就变成60，这明显会造成界面布局的错乱



![](http://p1.bqimg.com/567571/fe8ffb8caa93c500.png)

我的思路就是给yellowView，greenView加一个背景yelloewBackView，greenBackView，距离这个背景View的顶部距离为30个点，之后再影藏时直接影藏yelloewBackView，这样的话greenBackView的顶部就会顶到redView的底部了，而greenView距离greenBackView的顶部又是30个点，那看上去就是距离redView的底部30个点了，完美展示

![](http://p1.bpimg.com/567571/e8ce10172964363a.png)


下图是思路详解，ps不是很擅长，凑合看
![](http://p1.bpimg.com/567571/a254ec039916b0b4.png)






下图具体项目中实现

![](http://i1.piimg.com/567571/bfad4d4e49cb73df.png)
