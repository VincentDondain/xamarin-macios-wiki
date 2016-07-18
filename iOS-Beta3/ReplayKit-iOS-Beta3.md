#ReplayKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcast.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcast.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcast.h	2016-06-27 06:49:16.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ReplayKit.framework/Headers/RPBroadcast.h	2016-07-10 12:58:44.000000000 +0200
@@ -93,6 +93,7 @@
  @param error Required error in the RPRecordingErrorCode domain.
  */
 @protocol RPBroadcastControllerDelegate <NSObject>
+@optional
 - (void)broadcastController:(RPBroadcastController *)broadcastController didFinishWithError:(NSError * __nullable)error;
 - (void)broadcastController:(RPBroadcastController *)broadcastController didUpdateServiceInfo:(NSDictionary <NSString *, NSObject <NSCoding> *> *)serviceInfo;
 @end
```