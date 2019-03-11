### 米淘赚赚SDK集成说明

1.确保马甲包工程能正常运行

2.将```lib```文件夹拖入工程

3.设置：

* 在```Target -> Build Setting -> Other Linker Flags```中新增```-ObjC```

* 在```Target -> Build Phases -> Link Binary With Libraries```中新增```libsqlite3.0.tbd```、```libresolv.tbd```、```Photos.framework```、```libz.tbd```、```libc++.tbd```

4.配置：

* 在```lib``` -> ```Header```中有个```MTZZHeader.h```文件，这里进行配置```qq```、```微信```、```微博```、```极光推送```的key值

5.使用：

* SDK中使用了如下一些第三方库，如果马甲包工程中也使用了这些库的话请将其移除(cocoapods、手动集成)，头文件引用方式不变可正常使用
```WebViewJavascriptBridge```
```RNCryptor```
```AFNetworking```
```YYCategories```
```MBProgressHUD```
```SDWebImage```

* 每个马甲包中都需要增加一个展示隐私政策页面的功能(如果没有的话)，并使用```MTZZController.h```这个控制器传入```privacyPolicyUrl```值进行初始化并跳转(```push```、```present```)，例如：
```
#import "MTZZController.h"

MTZZController *policy = [[MTZZController alloc] init];
    policy.privacyPolicyUrl = [NSURL URLWithString:@"https://www.dianping.com"];
    [self presentViewController:policy animated:YES completion:nil];
```

