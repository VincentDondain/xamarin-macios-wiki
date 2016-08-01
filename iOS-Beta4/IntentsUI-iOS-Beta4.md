#IntentsUI.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/INUIHostedViewSiriProviding.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/INUIHostedViewSiriProviding.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/INUIHostedViewSiriProviding.h	2016-07-11 07:35:18.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/INUIHostedViewSiriProviding.h	2016-07-25 08:42:17.000000000 +0200
@@ -11,6 +11,6 @@
 
 @property (nonatomic, assign, readonly) BOOL displaysMap;
 @property (nonatomic, assign, readonly) BOOL displaysMessage;
-@property (nonatomic, assign, readonly) BOOL displaysPaymentTranscation;
+@property (nonatomic, assign, readonly) BOOL displaysPaymentTransaction;
 
 @end

```