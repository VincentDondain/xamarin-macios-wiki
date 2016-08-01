#WebKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h	2016-07-11 08:37:12.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h	2016-07-25 08:15:52.000000000 +0200
@@ -182,6 +182,12 @@
  */
 @property (nonatomic) WKDataDetectorTypes dataDetectorTypes API_AVAILABLE(ios(10.0));
 
+/*! @abstract A Boolean value indicating whether the WKWebView should always allow scaling of the web page, regardless of author intent.
+ @discussion This will override the user-scalable property.
+ The default value is NO.
+ */
+@property (nonatomic) BOOL ignoresViewportScaleLimits API_AVAILABLE(ios(10.0));
+
 #else
 
 /*! @abstract The directionality of user interface elements.

```