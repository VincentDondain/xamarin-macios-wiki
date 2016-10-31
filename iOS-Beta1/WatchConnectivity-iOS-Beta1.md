#WatchConnectivity.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchConnectivity.framework/Headers/WCSessionFile.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchConnectivity.framework/Headers/WCSessionFile.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchConnectivity.framework/Headers/WCSessionFile.h	2016-09-24 04:09:35.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchConnectivity.framework/Headers/WCSessionFile.h	2016-10-22 04:16:19.000000000 +0200
@@ -13,7 +13,7 @@
  */
 NS_CLASS_AVAILABLE_IOS(9.0)
 @interface WCSessionFile : NSObject
-@property (nonatomic, readonly) NSURL *fileURL;
+@property (nonatomic, readonly, nullable) NSURL *fileURL;
 @property (nonatomic, copy, readonly, nullable) NSDictionary<NSString *, id> *metadata;
 @end
 

```