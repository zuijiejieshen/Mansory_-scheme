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




###实现代码如下

```
- (void)createdTitleView{

    [self.contentView addSubview:self.typeLabel];
    [self.contentView addSubview:self.peopleView];
    [self.contentView addSubview:self.lineView];
    [self.contentView addSubview:self.infoLabel];

    [self.typeLabel mas_makeConstraints:^(MASConstraintMaker *make) {
        make.top.equalTo(self.contentView).offset(2);
        make.left.equalTo(self.contentView).offset(25);
    }];    
    [self.peopleView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.left.right.equalTo(self.contentView);
        make.top.equalTo(self.typeLabel.mas_bottom);
        self.cPeopleView = make.height.equalTo(@0).priority(UILayoutPriorityRequired);
        [self.cPeopleView deactivate];
    }];
    [self.lineView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.left.right.equalTo(self.contentView);
        make.top.equalTo(self.peopleView.mas_bottom);
        self.cLineView = make.height.equalTo(@0).priority(UILayoutPriorityRequired);
        [self.cLineView deactivate];
    }];
    [self.infoLabel mas_makeConstraints:^(MASConstraintMaker *make) {
        make.left.equalTo(self.contentView).offset(10);
        make.right.equalTo(self.contentView).offset(-10);
        make.top.equalTo(self.lineView.mas_bottom).offset(10);
    }];

}
```




```
- (UIView *)peopleView{
    if (_peopleView == nil) {
        _peopleView = [[UIView alloc] init];
        _peopleView.backgroundColor = [UIColor redColor];
        
        [_peopleView addSubview:self.peopleLabel];
        [_peopleView addSubview:self.peopleButton];
        [self.peopleLabel mas_makeConstraints:^(MASConstraintMaker *make) {
            make.left.equalTo(_peopleView).offset(12);
            make.right.equalTo(_peopleView).offset(-32);
            make.top.equalTo(_peopleView).offset(7);
            make.bottom.equalTo(_peopleView);
        }];
        
        [self.peopleButton mas_makeConstraints:^(MASConstraintMaker *make) {
            make.right.equalTo(_peopleView).offset(-12);
            make.width.height.equalTo(@15);
            make.top.equalTo(_peopleView).offset(7);
        }];
        
    }
    return _peopleView;
}

- (UIView *)peopleView{
    if (_peopleView == nil) {
        _peopleView = [[UIView alloc] init];
        _peopleView.backgroundColor = [UIColor redColor];
        
        [_peopleView addSubview:self.peopleLabel];
        [_peopleView addSubview:self.peopleButton];
        [self.peopleLabel mas_makeConstraints:^(MASConstraintMaker *make) {
            make.left.equalTo(_peopleView).offset(12);
            make.right.equalTo(_peopleView).offset(-32);
            make.top.equalTo(_peopleView).offset(7);
            make.bottom.equalTo(_peopleView);
        }];
        
        [self.peopleButton mas_makeConstraints:^(MASConstraintMaker *make) {
            make.right.equalTo(_peopleView).offset(-12);
            make.width.height.equalTo(@15);
            make.top.equalTo(_peopleView).offset(7);
        }];
        
    }
    return _peopleView;
}

- (UILabel *)peopleLabel{
    if (_peopleLabel == nil) {
        _peopleLabel = [UIFactory labelWithString:@"" size:14 color:@"96c72c" align:0];
    }
    return _peopleLabel;
}

- (UIButton *)peopleButton{
    if (_peopleButton == nil) {
        _peopleButton = [UIButton buttonWithType:UIButtonTypeCustom];
        [_peopleButton setImage:[UIImage imageNamed:@"mission_people_down"] forState:UIControlStateNormal];
        [_peopleButton addTarget:self action:@selector(peopleShowOrHiddenClicked:) forControlEvents:UIControlEventTouchUpInside];
    }
    return _peopleButton;
}

- (UIView *)lineView{
    if (_lineView == nil) {
        _lineView = [[UIView alloc] init];
        _lineView.backgroundColor = [UIColor yellowColor];
        
        [_lineView addSubview:self.lineBtn1];
        [_lineView addSubview:self.lineBtn2];

        [self.lineBtn1 mas_makeConstraints:^(MASConstraintMaker *make) {
            make.left.equalTo(_lineView).offset(12);
            make.top.equalTo(_lineView).offset(7);
            make.height.equalTo(@18);
            make.bottom.equalTo(_lineView);
        }];
        
        [self.lineBtn2 mas_makeConstraints:^(MASConstraintMaker *make) {
            make.left.equalTo(self.lineBtn1.mas_right).offset(10);
            make.top.equalTo(_lineView).offset(7);
            make.height.equalTo(@18);
        }];
    }
    return _lineView;
}


- (UIButton *)lineBtn1{
    if (_lineBtn1 == nil) {
        _lineBtn1 = [UIButton buttonWithType:UIButtonTypeCustom];
        [_lineBtn1 setBackgroundImage:[UIImage imageNamed:@"rw_lvsekuang"] forState:UIControlStateNormal];
        [_lineBtn1 setTitleColor:[UIColor hx_colorWithHexRGBAString:@"96c72c"] forState:UIControlStateNormal];
        _lineBtn1.titleLabel.font = [UIFont systemFontOfSize:12];
    }
    return _lineBtn1;
}

```

