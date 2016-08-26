# PPGetAddressBook
* PPGetAddressBook对AddressBook框架(iOS9之前)和Contacts框架(iOS9之后)做了对应的封装处理;

* 支持获取按联系人姓名首字拼音A~Z排序(*重点:已经对姓名的第二个字做了处理,排序更准确!*);
* 支持获取原始顺序的联系人,未分组,可自行处理.
* 已对号码中的"+86","-","()",空号和联系人姓名空白做了处理,不会出现因为数据源NULL导致程序crash的问题.

[简书地址](http://www.jianshu.com/p/b51a6125bcff) ; [codeData 地址](http://www.codedata.cn/cdetail/Objective-C/Demo/1471619974294285)

![image](https://github.com/jkpang/PPGetAddressBook/blob/master/AddressBook.mov.gif)
##Installation 安装
###1.手动安装:
`下载DEMO后,将子文件夹PPGetAddressBook拖入到项目中, 导入头文件PPGetAddressBook.h开始使用`
###2.CocoaPods安装:
first
`pod 'PPGetAddressBook' `

then
`pod install或pod install --no-repo-update`
##Usage 使用方法

###一、首先必须要请求用户是否授权APP访问通讯录的权限(建议在APPDeletegate.m中的didFinishLaunchingWithOptions方法中调用)

```objc
     //请求用户获取通讯录权限
    [PPGetAddressBook requestAddressBookAuthorization];
```
###二、获取通讯录
###1.获取按联系人姓名首字拼音A~Z排序(已经对姓名的第二个字做了处理),一句话搞定!

```objc
//获取按联系人姓名首字拼音A~Z排序(已经对姓名的第二个字做了处理)
    [PPGetAddressBook getOrderAddressBook:^(NSDictionary<NSString *,NSArray *> *addressBookDict, NSArray *peopleNameKey) {
        //addressBookDict:装着所有联系人的字典
        //peopleNameKey:联系人分组按拼音分组的Key值;
        //刷新 tableView       
        [self.tableView reloadData];
    } authorizationFailure:^{
        NSLog(@"请在iPhone的“设置-隐私-通讯录”选项中，允许PPAddressBook访问您的通讯录");
    }];

   
```
###2.获取原始顺序的联系人模型,未分组,一句话搞定!

```objc
//获取没有经过排序的联系人模型
    [PPGetAddressBook getOriginalAddressBook:^(NSArray<PPPersonModel *> *addressBookArray) {
       //addressBookArray:原始顺序的联系人数组
       
       //刷新 tableView       
        [self.tableView reloadData];
    } authorizationFailure:^{
       NSLog(@"请在iPhone的“设置-隐私-通讯录”选项中，允许PPAddressBook访问您的通讯录");
    }];
    
```

此封装里面还有些不太完美的地方,如果你有更好的实现方法,希望不吝赐教!
##CocoaPods更新日志
* 2016.08.26(tag:0.2.0)--将联系人排序的耗时操作放在子线程,大大优化程序的载入速度与体验
* 2016.08.23(tag:0.1.2)--小细节优化
* 2016.08.21(tag:0.1.1)--初始化

##联系方式:
* Weibo : @CoderPang
* Email : jkpang@outlook.com
* QQ : 2406552315

##许可证
PPGetAddressBook 使用 MIT 许可证，详情见 LICENSE 文件。




