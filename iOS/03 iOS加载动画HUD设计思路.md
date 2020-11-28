#03 iOS加载动画HUD设计思路

## 需求分析
在项目中难免存在一些地方是需要等待的地方，比如网络请求的时候或者是一些耗时操作的地方，就需要做一些等待的动画或者是界面出来，做这一块的处理在iOS中最典型的有SVProgressHUD MBProgressHUD等等，这些第三方框架功能很强大可以满足大部分的功能需求，但是也有一些无能为力的地方，比如我在项目中遇到的一个需求
![](https://ww4.sinaimg.cn/large/006tNc79gy1fdhui4dwgoj30oq0zk7d4.jpg)
***

在中间的这个网络请求的时候加载动画是一个动态的，其实在其它一些App中这种动画都是很常见的，比如斗鱼
![](https://ww4.sinaimg.cn/large/006tNc79gy1fdhuwl5g3mj30ku112wi7.jpg)
***

而这些动画其实用SVP并不好做的，而且UI样式和SVP等跟设计的UI不同
***
## 解决方式
拿出一个类继承自UIView比如ARROWShowHudView，在类中写上几个类方法

`+ (void)ShowWaitingWithStates:(NSString *)State;
+ (void)ShowSuccessWithStates:(NSString *)SuccessState;
+ (void)ShowFailureWithStates:(NSString *)FailureState;
+ (void)ShowNormalStateWith:(NSString *)NormalState;
+ (void)ShowAttentionStateWith:(NSString *)AttentionState;
+ (void)DismissWaitingStates;
+ (void)DismissSuccessStates;
+ (void)DismissFailureWithStates;
+ (void)DismissNormalStateStates;
+ (void)DismissAttentionStates;`

***

* Show类实现方法如下

```
+ (void)ShowWaitingWithStates:(NSString *)State
{
    // 1.初始化hud蒙版视图
    ARROWShowHudView *ShowHudView = [[ARROWShowHudView alloc] initWithFrame:CGRectMake(0, 0, ARROWWidth, ARROWHeight)];
    ShowHudView.backgroundColor = [UIColor clearColor];
    // 2.初始化背景视图
    UIView *StateView = [[UIView alloc] init];
    StateView.backgroundColor = [UIColor colorWithHexString:@"#343434"];
    StateView.alpha = 0.9;
    StateView.layer.cornerRadius = 5;
    [ShowHudView addSubview:StateView];
    [StateView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.centerX.mas_equalTo(ShowHudView.mas_centerX).offset(0);
        make.centerY.mas_equalTo(ShowHudView.mas_centerY).offset(0);
        make.width.mas_equalTo(ArrowAutoWidth * 360);
        make.height.mas_equalTo(ArrowAutoHeight * 140);
    }];
    // 3.初始化动画视图
    UIImageView *AnimationView = [[UIImageView alloc] init];
    NSArray *ImagesGroup = @[[UIImage imageNamed:@"fresh4.png"],
                             [UIImage imageNamed:@"fresh3.png"],
                             [UIImage imageNamed:@"fresh2.png"],
                             [UIImage imageNamed:@"fresh1.png"],
                             ];
    AnimationView.animationImages = ImagesGroup;
    AnimationView.animationDuration = 0.8;
    [AnimationView startAnimating];
    [StateView addSubview:AnimationView];
    [AnimationView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.centerY.mas_equalTo(StateView.mas_centerY).offset(0);
        make.left.mas_equalTo(StateView.mas_left).offset(ArrowAutoWidth * 20);
        make.width.mas_equalTo(ArrowAutoWidth * 120);
        make.height.mas_equalTo(ArrowAutoHeight * 104);
    }];
    // 4.初始化文本提示label
    UILabel *AttentionLabel = [UILabel ArrowLabelWithText:State TextColor:@"#FFFFFF" TextFontSize:12 BoolFont:NO];
    [StateView addSubview:AttentionLabel];
    
    [AttentionLabel mas_makeConstraints:^(MASConstraintMaker *make) {
        make.centerY.mas_equalTo(StateView.mas_centerY).offset(0);
        make.left.mas_equalTo(AnimationView.mas_right).offset(ArrowAutoWidth * 20);
        make.right.mas_equalTo(StateView.mas_right).offset(-ArrowAutoWidth * 20);
    }];
    [UIApplication sharedApplication].keyWindow.userInteractionEnabled = NO; \\ 禁用手势点击
    [[UIApplication sharedApplication].keyWindow addSubview:ShowHudView];
}
```

* Dissmissl类实现方法

```
for (UIView *subview in [UIApplication sharedApplication].keyWindow.subviews)
    {
        if ([subview isKindOfClass:self]) {
            [subview removeFromSuperview];
        }
    }
    [UIApplication sharedApplication].keyWindow.userInteractionEnabled = YES;

```

* 思路分析

其实这样自定义的方式就是在window上面添加一个view然后再对这个view做自定义，需要禁用手势点击的时候，其实是禁用window的那个用户交互方式







