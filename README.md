### 米淘赚赚SDK集成说明

1.确保马甲包工程能正常运行

2.将```lib```文件夹拖入工程

3.设置：

* 在```Target -> Build Setting -> Other Linker Flags```中新增```-ObjC```

* 在```Target -> Build Phases -> Link Binary With Libraries```中新增```libsqlite3.0.tbd```、```libresolv.tbd```、```Photos.framework```、```libz.tbd```、```libc++.tbd```

4.配置：

* 在```lib``` -> ```Header```中有个```RichHeader.h```文件，这里进行配置```qq```、```微信```、```微博```、```极光推送```的value值(不要修改key值)

5.使用：

* SDK中使用了如下一些第三方库，如果马甲包工程中也使用了这些库的话请将其移除(cocoapods、手动集成)，使用方式没有区别，正常引用头文件即可(所有第三方头文件可在```lib``` -> ```Header``` -> ```include```中找到)

```WebViewJavascriptBridge```

```RNCryptor```

```AFNetworking```

```YYCategories```

```MBProgressHUD```

```SDWebImage```

* 每个马甲包中都需要增加一个展示隐私政策页面的功能(如果没有的话)，并使用```PolicyController.h```这个控制器传入```privacyPolicyUrl```值进行初始化并跳转(```push```、```present```)，例如：
```
#import "PolicyController.h"

PolicyController *policy = [[PolicyController alloc] init];
policy.privacyPolicyUrl = [NSURL URLWithString:@"https://www.dianping.com"];
[self presentViewController:policy animated:YES completion:nil];
```

* 尽量在马甲包中使用分享功能，导入```#import "RichMagic.h"```，并使用```[[RichMagic shared] mtshare:@{}];```参数请参考米淘赚赚的业务，只要格式相同即可(这个分享是和米淘赚赚用的一样的)

* 以上两点为什么我要求做，是因为本身SDK中已经用到的业务或者代码，其实马甲包也是可以用的，那如果马甲包显示的调用就会大大减少“无用代码”的量，对过包很有好处的。

* 全局搜索所有关于米淘赚赚的字符串，比如：```mitao```、```mtzz```这种，都不应该出现(注释代码没有关系)，请将其替换。
