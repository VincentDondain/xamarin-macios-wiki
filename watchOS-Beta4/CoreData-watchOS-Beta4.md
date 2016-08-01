#CoreData.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreDataDefines.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreDataDefines.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreDataDefines.h	2016-07-10 07:49:23.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/CoreData.framework/Headers/CoreDataDefines.h	2016-07-25 07:16:38.000000000 +0200
@@ -89,6 +89,8 @@
 #define NSCoreDataVersionNumber10_10      526.0
 #define NSCoreDataVersionNumber10_10_2    526.1
 #define NSCoreDataVersionNumber10_10_3    526.2
+#define NSCoreDataVersionNumber10_11      640.0
+#define NSCoreDataVersionNumber10_11_3    641.3
 
 #define NSCoreDataVersionNumber_iPhoneOS_3_0		241.0
 #define NSCoreDataVersionNumber_iPhoneOS_3_1		248.0
@@ -105,5 +107,8 @@
 #define NSCoreDataVersionNumber_iPhoneOS_7_1		479.3
 #define NSCoreDataVersionNumber_iPhoneOS_8_0		519.0
 #define NSCoreDataVersionNumber_iPhoneOS_8_3		519.15
+#define NSCoreDataVersionNumber_iPhoneOS_9_0		640.0
+#define NSCoreDataVersionNumber_iPhoneOS_9_2		641.4
+#define NSCoreDataVersionNumber_iPhoneOS_9_3		641.6
 
 #endif // _COREDATADEFINES_H

```