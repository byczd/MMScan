

## MMScan


[![Building](https://img.shields.io/wercker/ci/wercker/docs.svg?style=flat)](https://cocoapods.org/pods/MMScan) 
[![Building](https://img.shields.io/badge/language-Objective--C-orange.svg?style=flat)](https://cocoapods.org/pods/MMScan)
[![CocoaPods compatible](https://img.shields.io/badge/pod-v1.3.1-blue.svg?style=flat)](https://cocoapods.org/pods/MMScan) 
[![Platform](https://img.shields.io/badge/platform-ios-lightgrey.svg?style=flat)](https://github.com/MinMao-Hub/MMScan)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg?style=flat)](http://opensource.org/licenses/MIT)

### Introduction

`MMScan`是一个简单的二维码以及条码扫描工具，使用`Objective-C`语言开发,有一套自定义的扫描动画以及界面，还包括生成二维码以及条码【一行代码搞定】

`MMScan ` is an simple QRCode and barcode scanning tool,Contains a separate set of interfaces and a single call, as well as the generation of QRCode code and bar code, a line of code can run.

### Rquirements

* iOS 8.0+
* Xcode 9
* Xcode 8 

### Installation


#### Install with  Cocoapods

记得更新你的pod-master,命令`pod repo update master`

* `pod 'MMScan', '~> 0.0'`
* `#import <MMScan/MMScanViewController.h> `  in you code


#### Copy code into project

[克隆代码](https://github.com/MinMao-Hub/MMScan.git)，然后将MMScanner文件夹下面的所有文件【包含资源】加入到你的项目中即可。	

Just clone and add the folder `MMScanner` to your project.

### Example



<div style="padding: 20px">
	<img src="gifs/static_img.png" width="35%" style="margin-top: 20"/>
</div>
<div style="margin-top: 10px">
	<img src="gifs/mmscan.gif" width="35%" style="margin-left:20px" />
</div>

* 2018.6.10 新增

<div style="margin-top: 10px">
	<img src="gifs/history.png" width="35%" style="margin-left:20px" />
</div>



### Usage

下面仅介绍简单的使用，具体使用见[MMScanDemo](https://github.com/MinMao-Hub/MMScan.git)

引入头文件`#import "MMScanViewController.h"`,如果是使用`cocoapods`，则需要引入`#import <MMScan/MMScanViewController.h>`

***PS:注意事项***
因为会调用到相册和相机权限，所以一定要记得在`info.plist`文件中添加必要的权限代码

```
<key>NSCameraUsageDescription</key>
<string>App需要您的同意,才能访问相机</string>
<key>NSPhotoLibraryUsageDescription</key>
<string>App需要您的同意,才能访问相册</string>
<key>NSPhotoLibraryAddUsageDescription</key>
<string>App需要您的同意,才能添加图片到相册</string>
```

#### 扫描二维码&条码

```Objective-C
MMScanViewController *scanVc = [[MMScanViewController alloc] initWithQrType:MMScanTypeAll onFinish:^(NSString *result, NSError *error) {
    if (error) {
        NSLog(@"error: %@",error);
    } else {
        NSLog(@"扫描结果：%@",result);
    }
}];
[self.navigationController pushViewController:scanVc animated:YES];

```
##### 注释
1. `QrType`
	
	有三种值：【MMScanTypeAll、MMScanTypeQrCode、MMScanTypeBarCode】
	* `MMScanTypeAll`  界面下方有个菜单，支持切换二维码和条码的扫描
	* `MMScanTypeQrCode` 单纯的二维码扫描
	* `MMScanTypeBarCode` 单纯的条码扫描
2. 回调结果
	
	回调回来的是扫描结果，如果是多张二维码，也只返回一条数据【数组中的第一条】

#### 生成二维码以及条码

```
//生成二维码
UIImage *image = [MMScanViewController createQRImageWithString:_linkTfd.text QRSize:CGSizeMake(250, 250) QRColor:[UIColor blackColor] bkColor:[UIColor colorWithRed:0.318 green:0.690 blue:0.839 alpha:1.00]];

//如果不需要设置背景色以及前景色，则使用下面代码  默认白色底黑色码
UIImage *image = [ScanViewController createQRImageWithString:_linkTfd.text QRSize:CGSizeMake(250, 250)];

//生成条形码
UIImage *image = [MMScanViewController createBarCodeImageWithString:_linkTfd.text QRSize:CGSizeMake(250, 150) QRColor:[UIColor blackColor] bkColor:[UIColor colorWithRed:0.318 green:0.690 blue:0.839 alpha:1.00]];

//如果不需要设置背景色以及前景色，则使用下面代码  默认白色底黑色码
UIImage *image = [ScanViewController createBarCodeImageWithString:_linkTfd.text barSize:CGSizeMake(250, 150)];


```

#### 保留历史记录以及查看历史记录

```
//设置历史数据回调
[scanVc setHistoryCallBack:^(NSArray *result) {
    NSLog(@"%@",result);
}];
```

设置该回调，即显示历史记录按钮【在导航条右边-> 可自定义该item】,点击历史按钮便会回调历史数据。

##### 清除历史数据

```
/**
 清空所有历史记录
 */
- (void)clearAllRecords;


/**
 清空某一条记录

 @param index 需要删除的index
 */
- (void)clearRecordIndex: (NSUInteger)index;
```



### 更多

更多自定义以及修改原有属性，[请看源码](https://github.com/MinMao-Hub/MMScan/tree/master/MMScanner)

### Contribution

You are welcome to fork and submit pull requests.

### License

MMScan is open-sourced software licensed under the MIT license.

### Update Log

> *v0.0.7* [2018.6.11]

> *v0.0.6* [2018.6.10]

* 新增历史记录查看功能
* 新增导航条小按钮自定义功能

<hr/>

> *v0.0.5* [2017.12.21]

* 闪光灯小按钮问题处理【扫一扫底部工具栏切换时，闪光灯会关闭，需要重置小按钮的选中状态】

<hr/>

> *v0.0.4* [2017.12.21]

1. 添加闪光灯小按钮 [#Issues-1](https://github.com/MinMao-Hub/MMScan/issues/1)

2. 底部toolBar适配iPhone X【只在模拟器测试过】


<hr/>


