#GameKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h	2016-07-11 07:47:47.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameKit.framework/Headers/GKGameSession.h	2016-07-23 02:15:44.000000000 +0200
@@ -60,7 +60,7 @@
 // Get the URL needed to share this session.
 - (void)getShareURLWithCompletionHandler:(void(^)(NSURL * __nullable url, NSError * __nullable error))completionHandler;
 
-// Load associated persistent data. The session's lastModifiedDate and lastModifiedPlayer will be updated upon completion.
+// Load associated persistent data.
 - (void)loadDataWithCompletionHandler:(void(^)(NSData * __nullable data, NSError * __nullable error))completionHandler;
 
 // Save new/updated persistent data. Data size is limited to 512K. The session's lastModifiedDate and lastModifiedPlayer will be updated upon completion.

```