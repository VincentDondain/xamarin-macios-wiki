#WebKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKBackForwardList.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKBackForwardList.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKBackForwardList.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKBackForwardList.h	2016-07-14 08:04:22.000000000 +0200
@@ -34,7 +34,7 @@
  */
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_10, 8_0)
+WK_EXTERN API_AVAILABLE(macosx(10.10), ios(8.0))
 @interface WKBackForwardList : NSObject
 
 /*! @abstract The current item.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKBackForwardListItem.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKBackForwardListItem.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKBackForwardListItem.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKBackForwardListItem.h	2016-07-14 08:04:22.000000000 +0200
@@ -33,7 +33,7 @@
  */
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_10, 8_0)
+WK_EXTERN API_AVAILABLE(macosx(10.10), ios(8.0))
 @interface WKBackForwardListItem : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKElementInfo.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKElementInfo.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKElementInfo.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKElementInfo.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,41 +0,0 @@
-/*
- * Copyright (C) 2015 Apple Inc. All rights reserved.
- *
- * Redistribution and use in source and binary forms, with or without
- * modification, are permitted provided that the following conditions
- * are met:
- * 1. Redistributions of source code must retain the above copyright
- *    notice, this list of conditions and the following disclaimer.
- * 2. Redistributions in binary form must reproduce the above copyright
- *    notice, this list of conditions and the following disclaimer in the
- *    documentation and/or other materials provided with the distribution.
- *
- * THIS SOFTWARE IS PROVIDED BY APPLE INC. AND ITS CONTRIBUTORS ``AS IS''
- * AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
- * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
- * PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL APPLE INC. OR ITS CONTRIBUTORS
- * BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
- * CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
- * SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
- * INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
- * CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
- * ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF
- * THE POSSIBILITY OF SUCH DAMAGE.
- */
-
-#import <WebKit/WKFoundation.h>
-
-#if WK_API_ENABLED
-
-NS_ASSUME_NONNULL_BEGIN
-
-NS_CLASS_AVAILABLE(10_12, 10_0)
-@interface WKElementInfo : NSObject <NSCopying>
-
-@property (nonatomic, readonly) NSURL *linkURL;
-
-@end
-
-NS_ASSUME_NONNULL_END
-
-#endif
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKError.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKError.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKError.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKError.h	2016-07-14 08:04:22.000000000 +0200
@@ -32,7 +32,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 /*! @constant WKErrorDomain Indicates a WebKit error. */
-WK_EXTERN NSString * const WKErrorDomain NS_AVAILABLE(10_10, 8_0);
+WK_EXTERN NSString * const WKErrorDomain API_AVAILABLE(macosx(10.10), ios(8.0));
 
 /*! @enum WKErrorCode
  @abstract Constants used by NSError to indicate errors in the WebKit domain.
@@ -47,8 +47,8 @@
     WKErrorWebContentProcessTerminated,
     WKErrorWebViewInvalidated,
     WKErrorJavaScriptExceptionOccurred,
-    WKErrorJavaScriptResultTypeIsUnsupported NS_ENUM_AVAILABLE(10_11, 9_0),
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+    WKErrorJavaScriptResultTypeIsUnsupported API_AVAILABLE(macosx(10.11), ios(9.0)),
+} API_AVAILABLE(macosx(10.10), ios(8.0));
 
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKFrameInfo.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKFrameInfo.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKFrameInfo.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKFrameInfo.h	2016-07-14 08:04:22.000000000 +0200
@@ -37,7 +37,7 @@
  */
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_10, 8_0)
+WK_EXTERN API_AVAILABLE(macosx(10.10), ios(8.0))
 @interface WKFrameInfo : NSObject <NSCopying>
 
 /*! @abstract A Boolean value indicating whether the frame is the main frame
@@ -51,7 +51,7 @@
 
 /*! @abstract The frame's current security origin.
  */
-@property (nonatomic, readonly) WKSecurityOrigin *securityOrigin NS_AVAILABLE(10_11, 9_0);
+@property (nonatomic, readonly) WKSecurityOrigin *securityOrigin API_AVAILABLE(macosx(10.11), ios(9.0));
 
 @end
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigation.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigation.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigation.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigation.h	2016-07-14 08:04:22.000000000 +0200
@@ -34,7 +34,7 @@
  also passed to the navigation delegate methods, to uniquely identify a webpage
  load from start to finish.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+WK_EXTERN API_AVAILABLE(macosx(10.10), ios(8.0))
 @interface WKNavigation : NSObject
 
 @end
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigationAction.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigationAction.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigationAction.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigationAction.h	2016-07-14 08:04:22.000000000 +0200
@@ -53,12 +53,12 @@
     WKNavigationTypeReload,
     WKNavigationTypeFormResubmitted,
     WKNavigationTypeOther = -1,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10), ios(8.0));
 
 /*! 
 A WKNavigationAction object contains information about an action that may cause a navigation, used for making policy decisions.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+WK_EXTERN API_AVAILABLE(macosx(10.10), ios(8.0))
 @interface WKNavigationAction : NSObject
 
 /*! @abstract The frame requesting the navigation.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigationDelegate.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigationDelegate.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigationDelegate.h	2016-06-27 02:42:39.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigationDelegate.h	2016-07-11 08:37:11.000000000 +0200
@@ -45,7 +45,7 @@
 typedef NS_ENUM(NSInteger, WKNavigationActionPolicy) {
     WKNavigationActionPolicyCancel,
     WKNavigationActionPolicyAllow,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10), ios(8.0));
 
 /*! @enum WKNavigationResponsePolicy
  @abstract The policy to pass back to the decision handler from the webView:decidePolicyForNavigationResponse:decisionHandler: method.
@@ -55,7 +55,7 @@
 typedef NS_ENUM(NSInteger, WKNavigationResponsePolicy) {
     WKNavigationResponsePolicyCancel,
     WKNavigationResponsePolicyAllow,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10), ios(8.0));
 
 /*! A class conforming to the WKNavigationDelegate protocol can provide
  methods for tracking progress for main frame navigations and for deciding
@@ -137,12 +137,12 @@
  credential.
  @discussion If you do not implement this method, the web view will respond to the authentication challenge with the NSURLSessionAuthChallengeRejectProtectionSpace disposition.
  */
-- (void)webView:(WKWebView *)webView didReceiveAuthenticationChallenge:(NSURLAuthenticationChallenge *)challenge completionHandler:(void (^)(NSURLSessionAuthChallengeDisposition disposition, NSURLCredential *_Nullable credential))completionHandler;
+- (void)webView:(WKWebView *)webView didReceiveAuthenticationChallenge:(NSURLAuthenticationChallenge *)challenge completionHandler:(void (^)(NSURLSessionAuthChallengeDisposition disposition, NSURLCredential * _Nullable credential))completionHandler;
 
 /*! @abstract Invoked when the web view's web content process is terminated.
  @param webView The web view whose underlying web content process was terminated.
  */
-- (void)webViewWebContentProcessDidTerminate:(WKWebView *)webView NS_AVAILABLE(10_11, 9_0);
+- (void)webViewWebContentProcessDidTerminate:(WKWebView *)webView API_AVAILABLE(macosx(10.11), ios(9.0));
 
 @end
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigationResponse.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigationResponse.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigationResponse.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigationResponse.h	2016-07-14 08:04:22.000000000 +0200
@@ -35,7 +35,7 @@
 
 /*! Contains information about a navigation response, used for making policy decisions.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+WK_EXTERN API_AVAILABLE(macosx(10.10), ios(8.0))
 @interface WKNavigationResponse : NSObject
 
 /*! @abstract A Boolean value indicating whether the frame being navigated is the main frame.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKOpenPanelParameters.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKOpenPanelParameters.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKOpenPanelParameters.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKOpenPanelParameters.h	2016-07-14 08:04:22.000000000 +0200
@@ -25,7 +25,7 @@
 
 #import <WebKit/WKFoundation.h>
 
-#if WK_API_ENABLED
+#if WK_API_ENABLED && !TARGET_OS_IPHONE
 
 #import <Foundation/Foundation.h>
 
@@ -33,7 +33,7 @@
 
 /*! WKOpenPanelParameters contains parameters that a file upload control has specified.
  */
-NS_CLASS_AVAILABLE(10_12, NA)
+WK_EXTERN API_AVAILABLE(macosx(10.12))
 @interface WKOpenPanelParameters : NSObject
 
 /*! @abstract Whether the file upload control supports multiple files.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreferences.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreferences.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreferences.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreferences.h	2016-07-14 08:04:22.000000000 +0200
@@ -34,7 +34,7 @@
  view. The preferences object associated with a web view is specified by
  its web view configuration.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+WK_EXTERN API_AVAILABLE(macosx(10.10), ios(8.0))
 @interface WKPreferences : NSObject <NSCoding>
 
 /*! @abstract The minimum font size in points.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewActionItem.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewActionItem.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewActionItem.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewActionItem.h	2016-07-14 08:04:22.000000000 +0200
@@ -29,7 +29,7 @@
 
 #import <UIKit/UIViewController.h>
 
-NS_AVAILABLE(NA, 10_0)
+API_AVAILABLE(ios(10.0))
 @protocol WKPreviewActionItem <UIPreviewActionItem>
 
 @property (nonatomic, copy, readonly) NSString *identifier;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewActionItemIdentifiers.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewActionItemIdentifiers.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewActionItemIdentifiers.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewActionItemIdentifiers.h	2016-07-14 08:04:23.000000000 +0200
@@ -26,13 +26,13 @@
 
 #import <WebKit/WKFoundation.h>
 
-#if WK_API_ENABLED
+#if WK_API_ENABLED && TARGET_OS_IPHONE
 
 #import <Foundation/Foundation.h>
 
-WK_EXTERN NSString * const WKPreviewActionItemIdentifierOpen NS_AVAILABLE(NA, 10_0);
-WK_EXTERN NSString * const WKPreviewActionItemIdentifierAddToReadingList NS_AVAILABLE(NA, 10_0);
-WK_EXTERN NSString * const WKPreviewActionItemIdentifierCopy NS_AVAILABLE(NA, 10_0);
-WK_EXTERN NSString * const WKPreviewActionItemIdentifierShare NS_AVAILABLE(NA, 10_0);
+WK_EXTERN NSString * const WKPreviewActionItemIdentifierOpen API_AVAILABLE(ios(10.0));
+WK_EXTERN NSString * const WKPreviewActionItemIdentifierAddToReadingList API_AVAILABLE(ios(10.0));
+WK_EXTERN NSString * const WKPreviewActionItemIdentifierCopy API_AVAILABLE(ios(10.0));
+WK_EXTERN NSString * const WKPreviewActionItemIdentifierShare API_AVAILABLE(ios(10.0));
 
 #endif
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewElementInfo.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewElementInfo.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewElementInfo.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewElementInfo.h	2016-07-14 08:04:23.000000000 +0200
@@ -27,12 +27,12 @@
 
 #if WK_API_ENABLED && TARGET_OS_IPHONE
 
-#import <WebKit/WKElementInfo.h>
-
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(NA, 10_0)
-@interface WKPreviewElementInfo : WKElementInfo
+WK_EXTERN API_AVAILABLE(ios(10.0))
+@interface WKPreviewElementInfo : NSObject <NSCopying>
+
+@property (nonatomic, readonly, nullable) NSURL *linkURL;
 
 @end
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKProcessPool.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKProcessPool.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKProcessPool.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKProcessPool.h	2016-07-14 08:04:23.000000000 +0200
@@ -35,7 +35,7 @@
  implementation-defined process limit is reached; after that, web views
  with the same process pool end up sharing web content processes.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+WK_EXTERN API_AVAILABLE(macosx(10.10), ios(8.0))
 @interface WKProcessPool : NSObject <NSCoding>
 @end
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKScriptMessage.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKScriptMessage.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKScriptMessage.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKScriptMessage.h	2016-07-14 08:04:23.000000000 +0200
@@ -37,7 +37,7 @@
 /*! A WKScriptMessage object contains information about a message sent from
  a webpage.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+WK_EXTERN API_AVAILABLE(macosx(10.10), ios(8.0))
 @interface WKScriptMessage : NSObject
 
 /*! @abstract The body of the message.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKSecurityOrigin.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKSecurityOrigin.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKSecurityOrigin.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKSecurityOrigin.h	2016-07-14 08:04:23.000000000 +0200
@@ -36,7 +36,7 @@
  */
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_11, 9_0)
+WK_EXTERN API_AVAILABLE(macosx(10.11), ios(9.0))
 @interface WKSecurityOrigin : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUIDelegate.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUIDelegate.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUIDelegate.h	2016-06-27 08:09:32.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUIDelegate.h	2016-07-14 07:50:23.000000000 +0200
@@ -65,7 +65,7 @@
   @discussion Your app should remove the web view from the view hierarchy and update
   the UI as needed, such as by closing the containing browser tab or window.
   */
-- (void)webViewDidClose:(WKWebView *)webView NS_AVAILABLE(10_11, 9_0);
+- (void)webViewDidClose:(WKWebView *)webView API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*! @abstract Displays a JavaScript alert panel.
  @param webView The web view invoking the delegate method.
@@ -129,7 +129,7 @@
  This method will only be invoked for elements that have default preview in WebKit, which is
  limited to links. In the future, it could be invoked for additional elements.
  */
-- (BOOL)webView:(WKWebView *)webView shouldPreviewElement:(WKPreviewElementInfo *)elementInfo NS_AVAILABLE(NA, 10_0);
+- (BOOL)webView:(WKWebView *)webView shouldPreviewElement:(WKPreviewElementInfo *)elementInfo API_AVAILABLE(ios(10.0));
 
 /*! @abstract Allows your app to provide a custom view controller to show when the given element is peeked.
  @param webView The web view invoking the delegate method.
@@ -144,13 +144,13 @@
  Returning nil will result in WebKit's default preview behavior. webView:commitPreviewingViewController: will only be invoked
  if a non-nil view controller was returned.
  */
-- (nullable UIViewController *)webView:(WKWebView *)webView previewingViewControllerForElement:(WKPreviewElementInfo *)elementInfo defaultActions:(NSArray<id <WKPreviewActionItem>> *)previewActions NS_AVAILABLE(NA, 10_0);
+- (nullable UIViewController *)webView:(WKWebView *)webView previewingViewControllerForElement:(WKPreviewElementInfo *)elementInfo defaultActions:(NSArray<id <WKPreviewActionItem>> *)previewActions API_AVAILABLE(ios(10.0));
 
 /*! @abstract Allows your app to pop to the view controller it created.
  @param webView The web view invoking the delegate method.
  @param previewingViewController The view controller that is being popped.
  */
-- (void)webView:(WKWebView *)webView commitPreviewingViewController:(UIViewController *)previewingViewController NS_AVAILABLE(NA, 10_0);
+- (void)webView:(WKWebView *)webView commitPreviewingViewController:(UIViewController *)previewingViewController API_AVAILABLE(ios(10.0));
 
 #endif // TARGET_OS_IPHONE
 
@@ -164,7 +164,7 @@
 
  If you do not implement this method, the web view will behave as if the user selected the Cancel button.
  */
-- (void)webView:(WKWebView *)webView runOpenPanelWithParameters:(WKOpenPanelParameters *)parameters initiatedByFrame:(WKFrameInfo *)frame completionHandler:(void (^)(NSArray<NSURL *> * _Nullable URLs))completionHandler NS_AVAILABLE(10_12, NA);
+- (void)webView:(WKWebView *)webView runOpenPanelWithParameters:(WKOpenPanelParameters *)parameters initiatedByFrame:(WKFrameInfo *)frame completionHandler:(void (^)(NSArray<NSURL *> * _Nullable URLs))completionHandler API_AVAILABLE(macosx(10.12));
 
 #endif
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUserContentController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUserContentController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUserContentController.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUserContentController.h	2016-07-14 08:04:23.000000000 +0200
@@ -39,7 +39,7 @@
  The user content controller associated with a web view is specified by its
  web view configuration.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+WK_EXTERN API_AVAILABLE(macosx(10.10), ios(8.0))
 @interface WKUserContentController : NSObject <NSCoding>
 
 /*! @abstract The user scripts associated with this user content
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUserScript.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUserScript.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUserScript.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUserScript.h	2016-07-14 08:04:23.000000000 +0200
@@ -39,11 +39,11 @@
 typedef NS_ENUM(NSInteger, WKUserScriptInjectionTime) {
     WKUserScriptInjectionTimeAtDocumentStart,
     WKUserScriptInjectionTimeAtDocumentEnd
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10), ios(8.0));
 
 /*! A @link WKUserScript @/link object represents a script that can be injected into webpages.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+WK_EXTERN API_AVAILABLE(macosx(10.10), ios(8.0))
 @interface WKUserScript : NSObject <NSCopying>
 
 /* @abstract The script source code. */
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebView.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebView.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebView.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebView.h	2016-07-11 08:37:12.000000000 +0200
@@ -49,10 +49,10 @@
  Used to configure @link WKWebView @/link instances.
  */
 #if TARGET_OS_IPHONE
-NS_CLASS_AVAILABLE(10_10, 8_0)
+WK_EXTERN API_AVAILABLE(macosx(10.10), ios(8.0))
 @interface WKWebView : UIView
 #else
-NS_CLASS_AVAILABLE(10_10, 8_0)
+WK_EXTERN API_AVAILABLE(macosx(10.10), ios(8.0))
 @interface WKWebView : NSView
 #endif
 
@@ -98,7 +98,7 @@
  If readAccessURL references a directory, files inside that file may be loaded by WebKit.
  @result A new navigation for the given file URL.
  */
-- (nullable WKNavigation *)loadFileURL:(NSURL *)URL allowingReadAccessToURL:(NSURL *)readAccessURL NS_AVAILABLE(10_11, 9_0);
+- (nullable WKNavigation *)loadFileURL:(NSURL *)URL allowingReadAccessToURL:(NSURL *)readAccessURL API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*! @abstract Sets the webpage contents and base URL.
  @param string The string to use as the contents of the webpage.
@@ -114,7 +114,7 @@
  @param baseURL A URL that is used to resolve relative URLs within the document.
  @result A new navigation.
  */
-- (nullable WKNavigation *)loadData:(NSData *)data MIMEType:(NSString *)MIMEType characterEncodingName:(NSString *)characterEncodingName baseURL:(NSURL *)baseURL NS_AVAILABLE(10_11, 9_0);
+- (nullable WKNavigation *)loadData:(NSData *)data MIMEType:(NSString *)MIMEType characterEncodingName:(NSString *)characterEncodingName baseURL:(NSURL *)baseURL API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*! @abstract Navigates to an item from the back-forward list and sets it
  as the current item.
@@ -168,7 +168,7 @@
  @discussion @link WKWebView @/link is key-value observing (KVO) compliant 
  for this property.
  */
-@property (nonatomic, readonly, nullable) SecTrustRef serverTrust NS_AVAILABLE(10_12, 10_0);
+@property (nonatomic, readonly, nullable) SecTrustRef serverTrust API_AVAILABLE(macosx(10.12), ios(10.0));
 
 /*! @abstract A Boolean value indicating whether there is a back item in
  the back-forward list that can be navigated to.
@@ -228,13 +228,13 @@
 
 /*! @abstract The custom user agent string or nil if no custom user agent string has been set.
 */
-@property (nullable, nonatomic, copy) NSString *customUserAgent NS_AVAILABLE(10_11, 9_0);
+@property (nullable, nonatomic, copy) NSString *customUserAgent API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*! @abstract A Boolean value indicating whether link preview is allowed for any
  links inside this WKWebView.
  @discussion The default value is YES on Mac and iOS.
  */
-@property (nonatomic) BOOL allowsLinkPreview NS_AVAILABLE(10_11, 9_0);
+@property (nonatomic) BOOL allowsLinkPreview API_AVAILABLE(macosx(10.11), ios(9.0));
 
 #if TARGET_OS_IPHONE
 /*! @abstract The scroll view associated with the web view.
@@ -306,7 +306,7 @@
 
 @interface WKWebView (WKDeprecated)
 
-@property (nonatomic, readonly, copy) NSArray *certificateChain NS_DEPRECATED(10_11, 10_12, 9_0, 10_0, "Please use serverTrust");
+@property (nonatomic, readonly, copy) NSArray *certificateChain API_DEPRECATED_WITH_REPLACEMENT("serverTrust", macosx(10.11, 10.12), ios(9.0, 10.0));
 
 @end
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h	2016-06-27 08:09:32.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h	2016-07-11 08:37:12.000000000 +0200
@@ -49,7 +49,7 @@
 typedef NS_ENUM(NSInteger, WKSelectionGranularity) {
     WKSelectionGranularityDynamic,
     WKSelectionGranularityCharacter,
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} API_AVAILABLE(ios(8.0));
 
 /*! @enum WKDataDetectorTypes
  @abstract The type of data detected.
@@ -72,8 +72,8 @@
     WKDataDetectorTypeLookupSuggestion = 1 << 6,
     WKDataDetectorTypeAll = NSUIntegerMax,
 
-    WKDataDetectorTypeSpotlightSuggestion NS_ENUM_DEPRECATED(NA, NA, 10_0, 10_0, "Please use WKDataDetectorTypeLookupSuggestion") = WKDataDetectorTypeLookupSuggestion,
-} NS_ENUM_AVAILABLE(NA, 10_0);
+    WKDataDetectorTypeSpotlightSuggestion API_DEPRECATED_WITH_REPLACEMENT("WKDataDetectorTypeLookupSuggestion", ios(10.0, 10.0)) = WKDataDetectorTypeLookupSuggestion,
+} API_AVAILABLE(ios(10.0));
 
 #else
 
@@ -91,7 +91,7 @@
 typedef NS_ENUM(NSInteger, WKUserInterfaceDirectionPolicy) {
     WKUserInterfaceDirectionPolicyContent,
     WKUserInterfaceDirectionPolicySystem,
-} NS_ENUM_AVAILABLE(10_12, NA);
+} API_AVAILABLE(macosx(10.12));
 
 #endif
 
@@ -107,13 +107,13 @@
     WKAudiovisualMediaTypeAudio = 1 << 0,
     WKAudiovisualMediaTypeVideo = 1 << 1,
     WKAudiovisualMediaTypeAll = NSUIntegerMax
-} NS_ENUM_AVAILABLE(10_12, 10_0);
+} API_AVAILABLE(macosx(10.12), ios(10.0));
 
 /*! A WKWebViewConfiguration object is a collection of properties with
  which to initialize a web view.
  @helps Contains properties used to configure a @link WKWebView @/link.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+WK_EXTERN API_AVAILABLE(macosx(10.10), ios(8.0))
 @interface WKWebViewConfiguration : NSObject <NSCoding, NSCopying>
 
 /*! @abstract The process pool from which to obtain the view's web content
@@ -134,7 +134,7 @@
 
 /*! @abstract The website data store to be used by the web view.
  */
-@property (nonatomic, strong) WKWebsiteDataStore *websiteDataStore NS_AVAILABLE(10_11, 9_0);
+@property (nonatomic, strong) WKWebsiteDataStore *websiteDataStore API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*! @abstract A Boolean value indicating whether the web view suppresses
  content rendering until it is fully loaded into memory.
@@ -144,14 +144,14 @@
 
 /*! @abstract The name of the application as used in the user agent string.
 */
-@property (nullable, nonatomic, copy) NSString *applicationNameForUserAgent NS_AVAILABLE(10_11, 9_0);
+@property (nullable, nonatomic, copy) NSString *applicationNameForUserAgent API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*! @abstract A Boolean value indicating whether AirPlay is allowed.
  @discussion The default value is YES.
  */
-@property (nonatomic) BOOL allowsAirPlayForMediaPlayback NS_AVAILABLE(10_11, 9_0);
+@property (nonatomic) BOOL allowsAirPlayForMediaPlayback API_AVAILABLE(macosx(10.11), ios(9.0));
 
-@property (nonatomic) WKAudiovisualMediaTypes mediaTypesRequiringUserActionForPlayback NS_AVAILABLE(10_12, 10_0);
+@property (nonatomic) WKAudiovisualMediaTypes mediaTypesRequiringUserActionForPlayback API_AVAILABLE(macosx(10.12), ios(10.0));
 
 #if TARGET_OS_IPHONE
 /*! @abstract A Boolean value indicating whether HTML5 videos play inline
@@ -171,7 +171,7 @@
  picture-in-picture.
  @discussion The default value is YES.
  */
-@property (nonatomic) BOOL allowsPictureInPictureMediaPlayback NS_AVAILABLE(NA, 9_0);
+@property (nonatomic) BOOL allowsPictureInPictureMediaPlayback API_AVAILABLE(ios(9_0));
 
 /*! @abstract An enum value indicating the type of data detection desired.
  @discussion The default value is WKDataDetectorTypeNone.
@@ -180,7 +180,7 @@
  if the dataDetectorTypes property is set to WKDataDetectorTypePhoneNumber | WKDataDetectorTypeLink | WKDataDetectorTypeCalendarEvent.
 
  */
-@property (nonatomic) WKDataDetectorTypes dataDetectorTypes NS_AVAILABLE(NA, 10_0);
+@property (nonatomic) WKDataDetectorTypes dataDetectorTypes API_AVAILABLE(ios(10.0));
 
 #else
 
@@ -188,7 +188,7 @@
  @discussion Possible values are described in WKUserInterfaceDirectionPolicy.
  The default value is WKUserInterfaceDirectionPolicyContent.
  */
-@property (nonatomic) WKUserInterfaceDirectionPolicy userInterfaceDirectionPolicy NS_AVAILABLE(10_12, NA);
+@property (nonatomic) WKUserInterfaceDirectionPolicy userInterfaceDirectionPolicy API_AVAILABLE(macosx(10.12));
 
 #endif
 
@@ -197,9 +197,9 @@
 @interface WKWebViewConfiguration (WKDeprecated)
 
 #if TARGET_OS_IPHONE
-@property (nonatomic) BOOL mediaPlaybackRequiresUserAction NS_DEPRECATED(NA, NA, 8_0, 9_0, "Please use requiresUserActionForMediaPlayback");
-@property (nonatomic) BOOL mediaPlaybackAllowsAirPlay NS_DEPRECATED(NA, NA, 8_0, 9_0, "Please use allowsAirPlayForMediaPlayback");
-@property (nonatomic) BOOL requiresUserActionForMediaPlayback NS_DEPRECATED(NA, NA, 9_0, 10_0, "Please use mediaTypesRequiringUserActionForPlayback");
+@property (nonatomic) BOOL mediaPlaybackRequiresUserAction API_DEPRECATED_WITH_REPLACEMENT("requiresUserActionForMediaPlayback", ios(8.0, 9.0));
+@property (nonatomic) BOOL mediaPlaybackAllowsAirPlay API_DEPRECATED_WITH_REPLACEMENT("allowsAirPlayForMediaPlayback", ios(8.0, 9.0));
+@property (nonatomic) BOOL requiresUserActionForMediaPlayback API_DEPRECATED_WITH_REPLACEMENT("mediaTypesRequiringUserActionForPlayback", ios(9.0, 10.0));
 #endif
 
 @end
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebsiteDataRecord.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebsiteDataRecord.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebsiteDataRecord.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebsiteDataRecord.h	2016-07-14 08:04:23.000000000 +0200
@@ -32,31 +32,31 @@
 NS_ASSUME_NONNULL_BEGIN
 
 /*! @constant WKWebsiteDataTypeDiskCache On-disk caches. */
-WK_EXTERN NSString * const WKWebsiteDataTypeDiskCache NS_AVAILABLE(10_11, 9_0);
+WK_EXTERN NSString * const WKWebsiteDataTypeDiskCache API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*! @constant WKWebsiteDataTypeMemoryCache In-memory caches. */
-WK_EXTERN NSString * const WKWebsiteDataTypeMemoryCache NS_AVAILABLE(10_11, 9_0);
+WK_EXTERN NSString * const WKWebsiteDataTypeMemoryCache API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*! @constant WKWebsiteDataTypeOfflineWebApplicationCache HTML offline web application caches. */
-WK_EXTERN NSString * const WKWebsiteDataTypeOfflineWebApplicationCache NS_AVAILABLE(10_11, 9_0);
+WK_EXTERN NSString * const WKWebsiteDataTypeOfflineWebApplicationCache API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*! @constant WKWebsiteDataTypeCookies Cookies. */
-WK_EXTERN NSString * const WKWebsiteDataTypeCookies NS_AVAILABLE(10_11, 9_0);
+WK_EXTERN NSString * const WKWebsiteDataTypeCookies API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*! @constant WKWebsiteDataTypeSessionStorage HTML session storage. */
-WK_EXTERN NSString * const WKWebsiteDataTypeSessionStorage NS_AVAILABLE(10_11, 9_0);
+WK_EXTERN NSString * const WKWebsiteDataTypeSessionStorage API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*! @constant WKWebsiteDataTypeLocalStorage HTML local storage. */
-WK_EXTERN NSString * const WKWebsiteDataTypeLocalStorage NS_AVAILABLE(10_11, 9_0);
+WK_EXTERN NSString * const WKWebsiteDataTypeLocalStorage API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*! @constant WKWebsiteDataTypeWebSQLDatabases WebSQL databases. */
-WK_EXTERN NSString * const WKWebsiteDataTypeWebSQLDatabases NS_AVAILABLE(10_11, 9_0);
+WK_EXTERN NSString * const WKWebsiteDataTypeWebSQLDatabases API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*! @constant WKWebsiteDataTypeIndexedDBDatabases IndexedDB databases. */
-WK_EXTERN NSString * const WKWebsiteDataTypeIndexedDBDatabases NS_AVAILABLE(10_11, 9_0);
+WK_EXTERN NSString * const WKWebsiteDataTypeIndexedDBDatabases API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*! A WKWebsiteDataRecord represents website data, grouped by domain name using the public suffix list. */
-NS_CLASS_AVAILABLE(10_11, 9_0)
+WK_EXTERN API_AVAILABLE(macosx(10.11), ios(9.0))
 @interface WKWebsiteDataRecord : NSObject
 
 /*! @abstract The display name for the data record. This is usually the domain name. */
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebsiteDataStore.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebsiteDataStore.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebsiteDataStore.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebsiteDataStore.h	2016-07-14 08:04:23.000000000 +0200
@@ -35,7 +35,7 @@
  make use of. This includes cookies, disk and memory caches, and persistent data such as WebSQL,
  IndexedDB databases, and local storage.
  */
-NS_CLASS_AVAILABLE(10_11, 9_0)
+WK_EXTERN API_AVAILABLE(macosx(10.11), ios(9.0))
 @interface WKWebsiteDataStore : NSObject <NSCoding>
 
 /* @abstract Returns the default data store. */
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWindowFeatures.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWindowFeatures.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWindowFeatures.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWindowFeatures.h	2016-07-14 08:04:23.000000000 +0200
@@ -33,7 +33,7 @@
  */
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_10, 8_0)
+WK_EXTERN API_AVAILABLE(macosx(10.10), ios(8.0))
 @interface WKWindowFeatures : NSObject
 
 /*! @abstract BOOL. Whether the menu bar should be visible. nil if menu bar visibility was not specified.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WebKit.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WebKit.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WebKit.h	2016-06-27 08:27:30.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WebKit.h	2016-07-14 08:04:23.000000000 +0200
@@ -25,7 +25,6 @@
 
 #import <WebKit/WKBackForwardList.h>
 #import <WebKit/WKBackForwardListItem.h>
-#import <WebKit/WKElementInfo.h>
 #import <WebKit/WKError.h>
 #import <WebKit/WKFoundation.h>
 #import <WebKit/WKFrameInfo.h>

```