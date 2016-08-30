# JWLaunchAd
### 一行代码集成启动广告图，支持GIF。

[![Support](https://img.shields.io/badge/support-iOS%207%2B-brightgreen.svg)](https://github.com/JWXIAN/MVCProject)
[![AppVeyor](https://img.shields.io/appveyor/ci/gruntjs/grunt.svg?maxAge=2592000)](https://github.com/JWXIAN/MVCProject)
[![Bintray](https://img.shields.io/badge/version-1.2-brightgreen.svg)](https://github.com/JWXIAN/MVCProject)

--

### 效果图
--
![image](https://github.com/JWXIAN/JWLaunchAd/blob/master/JWLaunchAd/gif.gif)
![image](https://github.com/JWXIAN/JWLaunchAd/blob/master/JWLaunchAd/gif2.gif)

--
## 使用方法
 #### 1.设置项目启动页为LaunchImage
 *    设置方法:在Assets.xcassets中新建LaunchImage<br>
      在项目中设置`Launch Images Source`,并将`Launch Screen File`清空<br>
      ![image]()
 
 #### 2.在LaunchImage 添加相应启动图片<br>
 *    ![image]()
 
 #### 3.在AppDelegate中设置window.rootViewController之后调用下面方法
    *1.设置启动页广告图片的url
    NSString *imgUrlString =@"http://imgstore.cdn.sogou.com/app/a/100540002/714860.jpg";
    //支持Gif
    //NSString *imgUrlString = @"http://img1.imgtn.bdimg.com/it/u=473895314,616407725&fm=206&gp=0.jpg";
    
    *2.初始化启动页广告(初始化后,自动添加至视图,不用手动添加)
    [JWLaunchAd initImageWithAttribute:10.0 hideSkip:NO setLaunchAd:^(JWLaunchAd *launchAd) {
        __block JWLaunchAd *weakSelf = launchAd;
        [launchAd setWebImageWithURL:imgUrlString options:JWWebImageDefault result:^(UIImage *image, NSURL *url) {
            *3.异步加载图片完成回调(设置图片尺寸)
            weakSelf.adFrame = CGRectMake(0, 0, kScreen_Width, kScreen_Height-150);
        } adClickBlock:^{
            *4.点击广告回调
            NSString *url = @"https://www.baidu.com";
            [[UIApplication sharedApplication] openURL:[NSURL URLWithString:url]];
        }];
    }];
