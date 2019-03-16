### 米淘赚赚SDK集成说明

1.集成之前告诉我该包的bundle id、微信、QQ、微博、极光key值，并确保马甲包工程能正常运行。

2.将```lib```文件夹拖入工程。

3.配置：

* 3.1：在```Target -> Build Setting -> Other Linker Flags```中新增```-ObjC```。

* 3.2在```Target -> Build Phases -> Link Binary With Libraries```中新增```libsqlite3.0.tbd```、```libresolv.tbd```、```Photos.framework```、```libz.tbd```、```libc++.tbd```。

* 3.3：配置工程scheme，值和项目bundle id相同，再加上QQ、微信、微博至少四个scheme值。

* 3.4：配置工程info.plist文件各种白名单。

* 3.5：打开工程推送开关，壳子中不需要显示处理推送相关逻辑。

4.使用：

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
但是不要在应用启动时使用该控制器初始化任何页面，不要在应用启动时使用！

* 尽量在马甲包中使用分享功能，导入```#import "RichMagic.h"```，并使用```[[RichMagic shared] mtshare:@{}];```参数请参考米淘赚赚的业务，只要格式相同即可(这个分享是和米淘赚赚用的一样的)。

* 全局搜索所有关于米淘赚赚的字符串，比如：```mitao```、```mtzz```这种，都不应该出现(注释代码没有关系)，请将其替换。
