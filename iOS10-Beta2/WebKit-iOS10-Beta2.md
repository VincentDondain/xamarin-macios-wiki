#WebKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebView.h	2016-05-25 07:23:53.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebView.h	2016-06-27 08:27:30.000000000 +0200
@@ -164,12 +164,11 @@
  */
 @property (nonatomic, readonly) BOOL hasOnlySecureContent;
 
-/*! @abstract An array of SecCertificateRef objects forming the certificate
- chain for the currently committed navigation.
- @discussion The certificates are ordered from leaf (at index 0) to anchor.
- @link WKWebView @/link is key-value observing (KVO) compliant for this property.
+/*! @abstract A SecTrustRef for the currently committed navigation.
+ @discussion @link WKWebView @/link is key-value observing (KVO) compliant 
+ for this property.
  */
-@property (nonatomic, readonly, copy) NSArray *certificateChain NS_AVAILABLE(10_11, 9_0);
+@property (nonatomic, readonly, nullable) SecTrustRef serverTrust NS_AVAILABLE(10_12, 10_0);
 
 /*! @abstract A Boolean value indicating whether there is a back item in
  the back-forward list that can be navigated to.
@@ -305,6 +304,12 @@
 
 #endif
 
+@interface WKWebView (WKDeprecated)
+
+@property (nonatomic, readonly, copy) NSArray *certificateChain NS_DEPRECATED(10_11, 10_12, 9_0, 10_0, "Please use serverTrust");
+
+@end
+
 NS_ASSUME_NONNULL_END
 
 #endif
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h	2016-06-02 06:55:04.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h	2016-06-27 08:09:32.000000000 +0200
@@ -85,7 +85,7 @@
  userInterfaceLayoutDirection property
  @discussion When WKUserInterfaceDirectionPolicyContent is specified, the directionality of user interface
  elements is affected by the "dir" attribute or the "direction" CSS property. When
- WKUserInterfaceDirectionPolicySystem is specified, the directionaltiy of user interface elements is
+ WKUserInterfaceDirectionPolicySystem is specified, the directionality of user interface elements is
  affected by the direction of the view.
 */
 typedef NS_ENUM(NSInteger, WKUserInterfaceDirectionPolicy) {

```