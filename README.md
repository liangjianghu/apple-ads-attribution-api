# apple-ads-attribution-api

苹果广告归因 API 示例，Apple Ads Attribution examples 

## 1234567890 问题

苹果提供了归因模拟数据的方式，供开发者在开发调试时，方便解析处理归因数据。但不少 app 在开发完成、开始广告投放后，依然收集到了大量模拟数据。

```json
{
    "adGroupId": 1234567890,
    "attribution": true,
    "campaignId": 1234567890,
    "conversionType": "Download",
    "countryOrRegion": "US",
    "creativeSetId": 1234567890,
    "keywordId": 12323222,
    "orgId": 1234567890
}
```

量江湖已经通过调研与测试验证，找到了此类数据产生的原因。如开发者有此疑问，可以联系量江湖。 

## 将框架添加到您的项目工程

* AdServices.framework 这个框架是用于 ASA 归因的，不受 ATT 约束，就是无论用户是否允许跟踪，都可以归因，仅支持 14.3 及更高版本系统，需XCode 12.3及更高版本支持。
* iAd.framework 这个框架是用于 ASA 归因的，受 ATT 以及 LAT 约束，如果用户允许跟踪，就可以归因。支持当前所有iOS版本，但未来可能废弃。
* AppTrackingTransparency.framework 在iOS 14 及更高版本用于征求用户跟踪许可的框架，就是弹窗询问用户是否同意跟踪；在 iOS 14.5 上苹果将强制要求开发者实施，也是获取 IDFA 的前提。
* AdSupport.framework 这个框架用于获取 IDFA，以及在低于 iOS 14 的版本中获取 LAT 信息。

以上framework，在添加到项目中后，均设置为 optional

## 注意事项

* XCode 版本必需 12.3 及以上
* 请在项目工程中务必添加AdServices Framework
* AdServices获取的token不可作为唯一设备标识
* 获取token需要设备联网，并且要做超时及容错处理
* 获取token的步骤，可以借助日志系统收集相关信息，用于排查问题和代码优化
* AdServices的restful api请求，失败后每隔5秒重试，最多3次
* token有效期为24小时
* 如在14.0-14.4设备中实施了ATT，iAd的归因时机建议在ATT弹窗之前
