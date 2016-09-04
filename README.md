DCAdMobNativeAds
============================

AdMobのネイティブ広告を表示する「DCAdMobNativeAds」クラスです。

下記に使用方法を記載しますので、実装の際のお役に立てば幸いです。

##使用方法

###A. ネイティブ広告を指定したビューに配置

```objective-c
CGFloat const nativeAdsWidth  = [[UIScreen mainScreen] bounds].size.width;
CGFloat const nativeAdsHeight = 80.0;

UIView *nativeAdsView = [[UIView alloc] initWithFrame:CGRectMake(0.0, 0.0, nativeAdsWidth, nativeAdsHeight)];
[[DCAdMobNativeAds sharedManager] showNativeAd:self targetView:nativeAdsView
                                         frame:CGRectMake(0.0, 0.0, nativeAdsWidth, nativeAdsHeight)];
[self.view addSubView:nativeAdsView];
```

###B. ネイティブ広告を指定したビューに取得

```objective-c
CGFloat const nativeAdsWidth  = [[UIScreen mainScreen] bounds].size.width;
CGFloat const nativeAdsHeight = 80.0;

UIView *nativeAdsView = [[UIView alloc] initWithFrame:CGRectMake(0.0, 0.0, nativeAdsWidth, nativeAdsHeight)];
nativeAdsView = [[DCAdMobNativeAds sharedManager] nativeAd:self
                                         frame:CGRectMake(0.0, 0.0, nativeAdsWidth, nativeAdsHeight)];
[self.view addSubView:nativeAdsView];
```

##ネイティブ広告の寸法について

AdMobネイティブ広告の縦幅は、160px（80dp）以上である必要があります。それ未満のサイズを指定するとエラー取得時のデリゲートメソッドが呼ばれ、広告は表示されません。

横幅の最小値については未検証ですが、ネイティブ広告のユニット作成時にプレビューサイズを指定する際、280dp 以上である必要がありますので、恐らく 280dp が最小値だと思います。

iPhoneは 4-inch/ 4.7-inch/ 5.5-inch で横幅が異なりますので、今回のサンプルでは横幅一杯に指定する方法を取っています。

ネイティブ広告初期化の際、下記のように縦幅 80dp 以上のサイズを指定することで正常に表示されました。

```objective-c
CGSize const nativeAdsSize = CGSizeMake([[UIScreen mainScreen] bounds].size.width, 80.0);
self.nativeExpressAdView = [[GADNativeExpressAdView alloc] initWithAdSize:GADAdSizeFromCGSize(nativeAdsSize)
                                                                       origin:CGPointMake(0.0, 0.0)];
```
