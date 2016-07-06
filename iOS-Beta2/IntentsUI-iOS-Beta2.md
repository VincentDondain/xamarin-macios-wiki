#IntentsUI.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/INUIHostedViewSiriProviding.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/INUIHostedViewSiriProviding.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/INUIHostedViewSiriProviding.h	2016-05-25 07:37:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/INUIHostedViewSiriProviding.h	2016-06-26 09:17:38.000000000 +0200
@@ -11,5 +11,6 @@
 
 @property (nonatomic, assign, readonly) BOOL displaysMap;
 @property (nonatomic, assign, readonly) BOOL displaysMessage;
+@property (nonatomic, assign, readonly) BOOL displaysPaymentTranscation;
 
 @end

```