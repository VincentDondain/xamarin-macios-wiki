#WatchKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceDevice.h /Applications/Xcode8-GM.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceDevice.h
--- /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceDevice.h	2016-08-06 23:37:47.000000000 -0500
+++ /Applications/Xcode8-GM.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceDevice.h	2016-08-06 23:29:41.000000000 -0500
@@ -47,6 +47,12 @@
     WKInterfaceDeviceCrownOrientationRight,
 } WK_AVAILABLE_WATCHOS_ONLY(3.0);
 
+#if TARGET_OS_WATCH
+typedef NS_ENUM(NSInteger, WKWaterResistanceRating) {
+    WKWaterResistanceRatingIPX7 NS_SWIFT_NAME(ipx7),
+    WKWaterResistanceRatingWR50 NS_SWIFT_NAME(wr50),
+} WK_AVAILABLE_WATCHOS_ONLY(3.0);
+#endif
 @interface WKInterfaceDevice : NSObject
 
 + (WKInterfaceDevice *)currentDevice;
@@ -73,6 +79,9 @@
 @property(nonatomic, readonly, copy) NSString *localizedModel WK_AVAILABLE_WATCHOS_IOS(2.0,9.0); // localized version of model
 @property(nonatomic, readonly, copy) NSString *systemName     WK_AVAILABLE_WATCHOS_IOS(2.0,9.0); // e.g. @"watchOS"
 
+#if TARGET_OS_WATCH
+@property (nonatomic,readonly) WKWaterResistanceRating waterResistanceRating WK_AVAILABLE_WATCHOS_ONLY(3.0);
+#endif
 - (void)playHaptic:(WKHapticType)type WK_AVAILABLE_WATCHOS_ONLY(2.0);
 
 @end

```