#WatchKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h	2016-07-12 05:59:37.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKBackgroundTask.h	2016-07-26 04:01:46.000000000 +0200
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