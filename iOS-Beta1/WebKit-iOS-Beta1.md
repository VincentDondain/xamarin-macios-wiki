#WebKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKBackForwardListItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKBackForwardListItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKBackForwardListItem.h	2015-10-03 01:53:22.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKBackForwardListItem.h	2016-05-25 07:59:32.000000000 +0200
@@ -36,6 +36,8 @@
 NS_CLASS_AVAILABLE(10_10, 8_0)
 @interface WKBackForwardListItem : NSObject
 
+- (instancetype)init NS_UNAVAILABLE;
+
 /*! @abstract The URL of the webpage represented by this item.
  */
 @property (readonly, copy) NSURL *URL;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKElementInfo.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKElementInfo.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKElementInfo.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKElementInfo.h	2016-05-25 07:59:32.000000000 +0200
@@ -0,0 +1,41 @@
+/*
+ * Copyright (C) 2015 Apple Inc. All rights reserved.
+ *
+ * Redistribution and use in source and binary forms, with or without
+ * modification, are permitted provided that the following conditions
+ * are met:
+ * 1. Redistributions of source code must retain the above copyright
+ *    notice, this list of conditions and the following disclaimer.
+ * 2. Redistributions in binary form must reproduce the above copyright
+ *    notice, this list of conditions and the following disclaimer in the
+ *    documentation and/or other materials provided with the distribution.
+ *
+ * THIS SOFTWARE IS PROVIDED BY APPLE INC. AND ITS CONTRIBUTORS ``AS IS''
+ * AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
+ * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
+ * PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL APPLE INC. OR ITS CONTRIBUTORS
+ * BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
+ * CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
+ * SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
+ * INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
+ * CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
+ * ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF
+ * THE POSSIBILITY OF SUCH DAMAGE.
+ */
+
+#import <WebKit/WKFoundation.h>
+
+#if WK_API_ENABLED
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface WKElementInfo : NSObject <NSCopying>
+
+@property (nonatomic, readonly) NSURL *linkURL;
+
+@end
+
+NS_ASSUME_NONNULL_END
+
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigationDelegate.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigationDelegate.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigationDelegate.h	2015-10-03 01:53:22.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKNavigationDelegate.h	2016-06-02 06:55:04.000000000 +0200
@@ -137,7 +137,7 @@
  credential.
  @discussion If you do not implement this method, the web view will respond to the authentication challenge with the NSURLSessionAuthChallengeRejectProtectionSpace disposition.
  */
-- (void)webView:(WKWebView *)webView didReceiveAuthenticationChallenge:(NSURLAuthenticationChallenge *)challenge completionHandler:(void (^)(NSURLSessionAuthChallengeDisposition disposition, NSURLCredential *__nullable credential))completionHandler;
+- (void)webView:(WKWebView *)webView didReceiveAuthenticationChallenge:(NSURLAuthenticationChallenge *)challenge completionHandler:(void (^)(NSURLSessionAuthChallengeDisposition disposition, NSURLCredential *_Nullable credential))completionHandler;
 
 /*! @abstract Invoked when the web view's web content process is terminated.
  @param webView The web view whose underlying web content process was terminated.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKOpenPanelParameters.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKOpenPanelParameters.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKOpenPanelParameters.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKOpenPanelParameters.h	2016-05-25 07:59:32.000000000 +0200
@@ -0,0 +1,47 @@
+/*
+ * Copyright (C) 2016 Apple Inc. All rights reserved.
+ *
+ * Redistribution and use in source and binary forms, with or without
+ * modification, are permitted provided that the following conditions
+ * are met:
+ * 1. Redistributions of source code must retain the above copyright
+ *    notice, this list of conditions and the following disclaimer.
+ * 2. Redistributions in binary form must reproduce the above copyright
+ *    notice, this list of conditions and the following disclaimer in the
+ *    documentation and/or other materials provided with the distribution.
+ *
+ * THIS SOFTWARE IS PROVIDED BY APPLE INC. AND ITS CONTRIBUTORS ``AS IS''
+ * AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
+ * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
+ * PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL APPLE INC. OR ITS CONTRIBUTORS
+ * BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
+ * CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
+ * SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
+ * INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
+ * CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
+ * ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF
+ * THE POSSIBILITY OF SUCH DAMAGE.
+ */
+
+#import <WebKit/WKFoundation.h>
+
+#if WK_API_ENABLED
+
+#import <Foundation/Foundation.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/*! WKOpenPanelParameters contains parameters that a file upload control has specified.
+ */
+NS_CLASS_AVAILABLE(10_12, NA)
+@interface WKOpenPanelParameters : NSObject
+
+/*! @abstract Whether the file upload control supports multiple files.
+ */
+@property (nonatomic, readonly) BOOL allowsMultipleSelection;
+
+@end
+
+NS_ASSUME_NONNULL_END
+
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreferences.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreferences.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreferences.h	2015-10-03 01:53:22.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreferences.h	2016-05-25 07:59:32.000000000 +0200
@@ -35,7 +35,7 @@
  its web view configuration.
  */
 NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface WKPreferences : NSObject
+@interface WKPreferences : NSObject <NSCoding>
 
 /*! @abstract The minimum font size in points.
  @discussion The default value is 0.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewActionItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewActionItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewActionItem.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewActionItem.h	2016-05-25 07:59:32.000000000 +0200
@@ -0,0 +1,39 @@
+/*
+ * Copyright (C) 2016 Apple Inc. All rights reserved.
+ *
+ * Redistribution and use in source and binary forms, with or without
+ * modification, are permitted provided that the following conditions
+ * are met:
+ * 1. Redistributions of source code must retain the above copyright
+ *    notice, this list of conditions and the following disclaimer.
+ * 2. Redistributions in binary form must reproduce the above copyright
+ *    notice, this list of conditions and the following disclaimer in the
+ *    documentation and/or other materials provided with the distribution.
+ *
+ * THIS SOFTWARE IS PROVIDED BY APPLE INC. AND ITS CONTRIBUTORS ``AS IS''
+ * AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
+ * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
+ * PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL APPLE INC. OR ITS CONTRIBUTORS
+ * BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
+ * CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
+ * SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
+ * INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
+ * CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
+ * ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF
+ * THE POSSIBILITY OF SUCH DAMAGE.
+ */
+
+#import <WebKit/WKFoundation.h>
+
+#if WK_API_ENABLED && TARGET_OS_IPHONE
+
+#import <UIKit/UIViewController.h>
+
+NS_AVAILABLE(NA, 10_0)
+@protocol WKPreviewActionItem <UIPreviewActionItem>
+
+@property (nonatomic, copy, readonly) NSString *identifier;
+
+@end
+
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewActionItemIdentifiers.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewActionItemIdentifiers.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewActionItemIdentifiers.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewActionItemIdentifiers.h	2016-05-25 07:59:32.000000000 +0200
@@ -0,0 +1,38 @@
+/*
+ * Copyright (C) 2016 Apple Inc. All rights reserved.
+ *
+ * Redistribution and use in source and binary forms, with or without
+ * modification, are permitted provided that the following conditions
+ * are met:
+ * 1. Redistributions of source code must retain the above copyright
+ *    notice, this list of conditions and the following disclaimer.
+ * 2. Redistributions in binary form must reproduce the above copyright
+ *    notice, this list of conditions and the following disclaimer in the
+ *    documentation and/or other materials provided with the distribution.
+ *
+ * THIS SOFTWARE IS PROVIDED BY APPLE INC. AND ITS CONTRIBUTORS ``AS IS''
+ * AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
+ * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
+ * PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL APPLE INC. OR ITS CONTRIBUTORS
+ * BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
+ * CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
+ * SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
+ * INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
+ * CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
+ * ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF
+ * THE POSSIBILITY OF SUCH DAMAGE.
+ */
+
+
+#import <WebKit/WKFoundation.h>
+
+#if WK_API_ENABLED
+
+#import <Foundation/Foundation.h>
+
+WK_EXTERN NSString * const WKPreviewActionItemIdentifierOpen NS_AVAILABLE(NA, 10_0);
+WK_EXTERN NSString * const WKPreviewActionItemIdentifierAddToReadingList NS_AVAILABLE(NA, 10_0);
+WK_EXTERN NSString * const WKPreviewActionItemIdentifierCopy NS_AVAILABLE(NA, 10_0);
+WK_EXTERN NSString * const WKPreviewActionItemIdentifierShare NS_AVAILABLE(NA, 10_0);
+
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewElementInfo.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewElementInfo.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewElementInfo.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKPreviewElementInfo.h	2016-05-25 07:59:32.000000000 +0200
@@ -0,0 +1,41 @@
+/*
+ * Copyright (C) 2015 Apple Inc. All rights reserved.
+ *
+ * Redistribution and use in source and binary forms, with or without
+ * modification, are permitted provided that the following conditions
+ * are met:
+ * 1. Redistributions of source code must retain the above copyright
+ *    notice, this list of conditions and the following disclaimer.
+ * 2. Redistributions in binary form must reproduce the above copyright
+ *    notice, this list of conditions and the following disclaimer in the
+ *    documentation and/or other materials provided with the distribution.
+ *
+ * THIS SOFTWARE IS PROVIDED BY APPLE INC. AND ITS CONTRIBUTORS ``AS IS''
+ * AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO,
+ * THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
+ * PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL APPLE INC. OR ITS CONTRIBUTORS
+ * BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
+ * CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
+ * SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
+ * INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
+ * CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
+ * ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF
+ * THE POSSIBILITY OF SUCH DAMAGE.
+ */
+
+#import <WebKit/WKFoundation.h>
+
+#if WK_API_ENABLED && TARGET_OS_IPHONE
+
+#import <WebKit/WKElementInfo.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE(NA, 10_0)
+@interface WKPreviewElementInfo : WKElementInfo
+
+@end
+
+NS_ASSUME_NONNULL_END
+
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKProcessPool.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKProcessPool.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKProcessPool.h	2015-10-03 01:53:22.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKProcessPool.h	2016-05-25 07:59:32.000000000 +0200
@@ -36,7 +36,7 @@
  with the same process pool end up sharing web content processes.
  */
 NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface WKProcessPool : NSObject
+@interface WKProcessPool : NSObject <NSCoding>
 @end
 
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUIDelegate.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUIDelegate.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUIDelegate.h	2015-10-03 01:53:22.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUIDelegate.h	2016-05-25 07:23:53.000000000 +0200
@@ -28,11 +28,14 @@
 #if WK_API_ENABLED
 
 #import <Foundation/Foundation.h>
+#import <WebKit/WKPreviewActionItem.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
 @class WKFrameInfo;
 @class WKNavigationAction;
+@class WKOpenPanelParameters;
+@class WKPreviewElementInfo;
 @class WKWebViewConfiguration;
 @class WKWindowFeatures;
 
@@ -112,7 +115,58 @@
 
  If you do not implement this method, the web view will behave as if the user selected the Cancel button.
  */
-- (void)webView:(WKWebView *)webView runJavaScriptTextInputPanelWithPrompt:(NSString *)prompt defaultText:(nullable NSString *)defaultText initiatedByFrame:(WKFrameInfo *)frame completionHandler:(void (^)(NSString * __nullable result))completionHandler;
+- (void)webView:(WKWebView *)webView runJavaScriptTextInputPanelWithPrompt:(NSString *)prompt defaultText:(nullable NSString *)defaultText initiatedByFrame:(WKFrameInfo *)frame completionHandler:(void (^)(NSString * _Nullable result))completionHandler;
+
+#if TARGET_OS_IPHONE
+
+/*! @abstract Allows your app to determine whether or not the given element should show a preview.
+ @param webView The web view invoking the delegate method.
+ @param elementInfo The elementInfo for the element the user has started touching.
+ @discussion To disable previews entirely for the given element, return NO. Returning NO will prevent 
+ webView:previewingViewControllerForElement:defaultActions: and webView:commitPreviewingViewController:
+ from being invoked.
+ 
+ This method will only be invoked for elements that have default preview in WebKit, which is
+ limited to links. In the future, it could be invoked for additional elements.
+ */
+- (BOOL)webView:(WKWebView *)webView shouldPreviewElement:(WKPreviewElementInfo *)elementInfo NS_AVAILABLE(NA, 10_0);
+
+/*! @abstract Allows your app to provide a custom view controller to show when the given element is peeked.
+ @param webView The web view invoking the delegate method.
+ @param elementInfo The elementInfo for the element the user is peeking.
+ @param defaultActions An array of the actions that WebKit would use as previewActionItems for this element by 
+ default. These actions would be used if allowsLinkPreview is YES but these delegate methods have not been 
+ implemented, or if this delegate method returns nil.
+ @discussion Returning a view controller will result in that view controller being displayed as a peek preview.
+ To use the defaultActions, your app is responsible for returning whichever of those actions it wants in your 
+ view controller's implementation of -previewActionItems.
+ 
+ Returning nil will result in WebKit's default preview behavior. webView:commitPreviewingViewController: will only be invoked
+ if a non-nil view controller was returned.
+ */
+- (nullable UIViewController *)webView:(WKWebView *)webView previewingViewControllerForElement:(WKPreviewElementInfo *)elementInfo defaultActions:(NSArray<id <WKPreviewActionItem>> *)previewActions NS_AVAILABLE(NA, 10_0);
+
+/*! @abstract Allows your app to pop to the view controller it created.
+ @param webView The web view invoking the delegate method.
+ @param previewingViewController The view controller that is being popped.
+ */
+- (void)webView:(WKWebView *)webView commitPreviewingViewController:(UIViewController *)previewingViewController NS_AVAILABLE(NA, 10_0);
+
+#endif // TARGET_OS_IPHONE
+
+#if !TARGET_OS_IPHONE
+
+/*! @abstract Displays a file upload panel.
+ @param webView The web view invoking the delegate method.
+ @param parameters Parameters describing the file upload control.
+ @param frame Information about the frame whose file upload control initiated this call.
+ @param completionHandler The completion handler to call after open panel has been dismissed. Pass the selected URLs if the user chose OK, otherwise nil.
+
+ If you do not implement this method, the web view will behave as if the user selected the Cancel button.
+ */
+- (void)webView:(WKWebView *)webView runOpenPanelWithParameters:(WKOpenPanelParameters *)parameters initiatedByFrame:(WKFrameInfo *)frame completionHandler:(void (^)(NSArray<NSURL *> * _Nullable URLs))completionHandler NS_AVAILABLE(10_12, NA);
+
+#endif
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUserContentController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUserContentController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUserContentController.h	2015-10-03 01:53:22.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKUserContentController.h	2016-05-25 07:59:33.000000000 +0200
@@ -40,7 +40,7 @@
  web view configuration.
  */
 NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface WKUserContentController : NSObject
+@interface WKUserContentController : NSObject <NSCoding>
 
 /*! @abstract The user scripts associated with this user content
  controller.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebView.h	2015-10-03 01:53:22.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebView.h	2016-05-25 07:23:53.000000000 +0200
@@ -83,7 +83,7 @@
  */
 - (instancetype)initWithFrame:(CGRect)frame configuration:(WKWebViewConfiguration *)configuration NS_DESIGNATED_INITIALIZER;
 
-- (instancetype)initWithCoder:(NSCoder *)coder NS_UNAVAILABLE;
+- (nullable instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
 
 /*! @abstract Navigates to a requested URL.
  @param request The request specifying the URL to which to navigate.
@@ -219,7 +219,7 @@
  @param completionHandler A block to invoke when script evaluation completes or fails.
  @discussion The completionHandler is passed the result of the script evaluation or an error.
 */
-- (void)evaluateJavaScript:(NSString *)javaScriptString completionHandler:(void (^ __nullable)(__nullable id, NSError * __nullable error))completionHandler;
+- (void)evaluateJavaScript:(NSString *)javaScriptString completionHandler:(void (^ _Nullable)(_Nullable id, NSError * _Nullable error))completionHandler;
 
 /*! @abstract A Boolean value indicating whether horizontal swipe gestures
  will trigger back-forward list navigations.
@@ -233,7 +233,7 @@
 
 /*! @abstract A Boolean value indicating whether link preview is allowed for any
  links inside this WKWebView.
- @discussion The default value is NO on iOS and YES on Mac.
+ @discussion The default value is YES on Mac and iOS.
  */
 @property (nonatomic) BOOL allowsLinkPreview NS_AVAILABLE(10_11, 9_0);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h	2015-10-03 01:53:22.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebViewConfiguration.h	2016-06-02 06:55:04.000000000 +0200
@@ -37,6 +37,7 @@
 @class WKWebsiteDataStore;
 
 #if TARGET_OS_IPHONE
+
 /*! @enum WKSelectionGranularity
  @abstract The granularity with which a selection can be created and modified interactively.
  @constant WKSelectionGranularityDynamic    Selection granularity varies automatically based on the selection.
@@ -49,14 +50,71 @@
     WKSelectionGranularityDynamic,
     WKSelectionGranularityCharacter,
 } NS_ENUM_AVAILABLE_IOS(8_0);
+
+/*! @enum WKDataDetectorTypes
+ @abstract The type of data detected.
+ @constant WKDataDetectorTypeNone No detection is performed.
+ @constant WKDataDetectorTypePhoneNumber Phone numbers are detected and turned into links.
+ @constant WKDataDetectorTypeLink URLs in text are detected and turned into links.
+ @constant WKDataDetectorTypeAddress Addresses are detected and turned into links.
+ @constant WKDataDetectorTypeCalendarEvent Dates and times that are in the future are detected and turned into links.
+ @constant WKDataDetectorTypeAll All of the above data types are turned into links when detected. Choosing this value will
+ automatically include any new detection type that is added.
+ */
+typedef NS_OPTIONS(NSUInteger, WKDataDetectorTypes) {
+    WKDataDetectorTypeNone = 0,
+    WKDataDetectorTypePhoneNumber = 1 << 0,
+    WKDataDetectorTypeLink = 1 << 1,
+    WKDataDetectorTypeAddress = 1 << 2,
+    WKDataDetectorTypeCalendarEvent = 1 << 3,
+    WKDataDetectorTypeTrackingNumber = 1 << 4,
+    WKDataDetectorTypeFlightNumber = 1 << 5,
+    WKDataDetectorTypeLookupSuggestion = 1 << 6,
+    WKDataDetectorTypeAll = NSUIntegerMax,
+
+    WKDataDetectorTypeSpotlightSuggestion NS_ENUM_DEPRECATED(NA, NA, 10_0, 10_0, "Please use WKDataDetectorTypeLookupSuggestion") = WKDataDetectorTypeLookupSuggestion,
+} NS_ENUM_AVAILABLE(NA, 10_0);
+
+#else
+
+/*! @enum WKUserInterfaceDirectionPolicy
+ @abstract The policy used to determine the directionality of user interface elements inside a web view.
+ @constant WKUserInterfaceDirectionPolicyContent User interface directionality follows CSS / HTML / XHTML
+ specifications.
+ @constant WKUserInterfaceDirectionPolicySystem User interface directionality follows the view's
+ userInterfaceLayoutDirection property
+ @discussion When WKUserInterfaceDirectionPolicyContent is specified, the directionality of user interface
+ elements is affected by the "dir" attribute or the "direction" CSS property. When
+ WKUserInterfaceDirectionPolicySystem is specified, the directionaltiy of user interface elements is
+ affected by the direction of the view.
+*/
+typedef NS_ENUM(NSInteger, WKUserInterfaceDirectionPolicy) {
+    WKUserInterfaceDirectionPolicyContent,
+    WKUserInterfaceDirectionPolicySystem,
+} NS_ENUM_AVAILABLE(10_12, NA);
+
 #endif
 
+/*! @enum WKAudiovisualMediaTypes
+ @abstract The types of audiovisual media which will require a user gesture to begin playing.
+ @constant WKAudiovisualMediaTypeNone No audiovisual media will require a user gesture to begin playing.
+ @constant WKAudiovisualMediaTypeAudio Audiovisual media containing audio will require a user gesture to begin playing.
+ @constant WKAudiovisualMediaTypeVideo Audiovisual media containing video will require a user gesture to begin playing.
+ @constant WKAudiovisualMediaTypeAll All audiovisual media will require a user gesture to begin playing.
+*/
+typedef NS_OPTIONS(NSUInteger, WKAudiovisualMediaTypes) {
+    WKAudiovisualMediaTypeNone = 0,
+    WKAudiovisualMediaTypeAudio = 1 << 0,
+    WKAudiovisualMediaTypeVideo = 1 << 1,
+    WKAudiovisualMediaTypeAll = NSUIntegerMax
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
 /*! A WKWebViewConfiguration object is a collection of properties with
  which to initialize a web view.
  @helps Contains properties used to configure a @link WKWebView @/link.
  */
 NS_CLASS_AVAILABLE(10_10, 8_0)
-@interface WKWebViewConfiguration : NSObject <NSCopying>
+@interface WKWebViewConfiguration : NSObject <NSCoding, NSCopying>
 
 /*! @abstract The process pool from which to obtain the view's web content
  process.
@@ -93,6 +151,8 @@
  */
 @property (nonatomic) BOOL allowsAirPlayForMediaPlayback NS_AVAILABLE(10_11, 9_0);
 
+@property (nonatomic) WKAudiovisualMediaTypes mediaTypesRequiringUserActionForPlayback NS_AVAILABLE(10_12, 10_0);
+
 #if TARGET_OS_IPHONE
 /*! @abstract A Boolean value indicating whether HTML5 videos play inline
  (YES) or use the native full-screen controller (NO).
@@ -100,12 +160,6 @@
  */
 @property (nonatomic) BOOL allowsInlineMediaPlayback;
 
-/*! @abstract A Boolean value indicating whether HTML5 videos require the
- user to start playing them (YES) or can play automatically (NO).
- @discussion The default value is YES.
- */
-@property (nonatomic) BOOL requiresUserActionForMediaPlayback NS_AVAILABLE(NA, 9_0);
-
 /*! @abstract The level of granularity with which the user can interactively
  select content in the web view.
  @discussion Possible values are described in WKSelectionGranularity.
@@ -119,6 +173,23 @@
  */
 @property (nonatomic) BOOL allowsPictureInPictureMediaPlayback NS_AVAILABLE(NA, 9_0);
 
+/*! @abstract An enum value indicating the type of data detection desired.
+ @discussion The default value is WKDataDetectorTypeNone.
+ An example of how this property may affect the content loaded in the WKWebView is that content like
+ 'Visit apple.com on July 4th or call 1 800 555-5545' will be transformed to add links around 'apple.com', 'July 4th' and '1 800 555-5545'
+ if the dataDetectorTypes property is set to WKDataDetectorTypePhoneNumber | WKDataDetectorTypeLink | WKDataDetectorTypeCalendarEvent.
+
+ */
+@property (nonatomic) WKDataDetectorTypes dataDetectorTypes NS_AVAILABLE(NA, 10_0);
+
+#else
+
+/*! @abstract The directionality of user interface elements.
+ @discussion Possible values are described in WKUserInterfaceDirectionPolicy.
+ The default value is WKUserInterfaceDirectionPolicyContent.
+ */
+@property (nonatomic) WKUserInterfaceDirectionPolicy userInterfaceDirectionPolicy NS_AVAILABLE(10_12, NA);
+
 #endif
 
 @end
@@ -128,6 +199,7 @@
 #if TARGET_OS_IPHONE
 @property (nonatomic) BOOL mediaPlaybackRequiresUserAction NS_DEPRECATED(NA, NA, 8_0, 9_0, "Please use requiresUserActionForMediaPlayback");
 @property (nonatomic) BOOL mediaPlaybackAllowsAirPlay NS_DEPRECATED(NA, NA, 8_0, 9_0, "Please use allowsAirPlayForMediaPlayback");
+@property (nonatomic) BOOL requiresUserActionForMediaPlayback NS_DEPRECATED(NA, NA, 9_0, 10_0, "Please use mediaTypesRequiringUserActionForPlayback");
 #endif
 
 @end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebsiteDataStore.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebsiteDataStore.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebsiteDataStore.h	2015-10-03 01:53:22.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WKWebsiteDataStore.h	2016-05-25 07:59:33.000000000 +0200
@@ -36,7 +36,7 @@
  IndexedDB databases, and local storage.
  */
 NS_CLASS_AVAILABLE(10_11, 9_0)
-@interface WKWebsiteDataStore : NSObject
+@interface WKWebsiteDataStore : NSObject <NSCoding>
 
 /* @abstract Returns the default data store. */
 + (WKWebsiteDataStore *)defaultDataStore;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WebKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WebKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WebKit.h	2015-10-03 01:53:22.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/WebKit.framework/Headers/WebKit.h	2016-05-25 07:59:33.000000000 +0200
@@ -25,6 +25,7 @@
 
 #import <WebKit/WKBackForwardList.h>
 #import <WebKit/WKBackForwardListItem.h>
+#import <WebKit/WKElementInfo.h>
 #import <WebKit/WKError.h>
 #import <WebKit/WKFoundation.h>
 #import <WebKit/WKFrameInfo.h>
@@ -32,7 +33,11 @@
 #import <WebKit/WKNavigationAction.h>
 #import <WebKit/WKNavigationDelegate.h>
 #import <WebKit/WKNavigationResponse.h>
+#import <WebKit/WKOpenPanelParameters.h>
 #import <WebKit/WKPreferences.h>
+#import <WebKit/WKPreviewActionItem.h>
+#import <WebKit/WKPreviewActionItemIdentifiers.h>
+#import <WebKit/WKPreviewElementInfo.h>
 #import <WebKit/WKProcessPool.h>
 #import <WebKit/WKScriptMessage.h>
 #import <WebKit/WKScriptMessageHandler.h>

```