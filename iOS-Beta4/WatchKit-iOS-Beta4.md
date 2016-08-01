#WatchKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h	2016-07-10 10:18:02.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h	2016-07-26 06:58:37.000000000 +0200
@@ -22,7 +22,6 @@
 
 WK_AVAILABLE_WATCHOS_ONLY(3.0)
 @interface WKApplicationRefreshBackgroundTask : WKRefreshBackgroundTask
-- (void)setTaskCompleted;   // developer should call this when this task has been completed
 @end
 
 WK_AVAILABLE_WATCHOS_ONLY(3.0)
@@ -45,12 +44,10 @@
 WK_AVAILABLE_WATCHOS_ONLY(3.0)
 @interface WKURLSessionRefreshBackgroundTask : WKRefreshBackgroundTask
 @property (readonly, copy) NSString *sessionIdentifier;
-- (void)setTaskCompleted;   // developer should call this when this task has been completed
 @end
 
 WK_AVAILABLE_WATCHOS_ONLY(3.0)
 @interface WKWatchConnectivityRefreshBackgroundTask : WKRefreshBackgroundTask
-- (void)setTaskCompleted;   // developer should call this when this task has been completed
 @end
 
 @interface WKExtension (WKBackgroundTasks)

```