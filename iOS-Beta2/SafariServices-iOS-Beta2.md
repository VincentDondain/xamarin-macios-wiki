#SafariServices.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerManager.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerManager.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerManager.h	2016-05-25 05:53:32.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerManager.h	2016-06-26 10:37:48.000000000 +0200
@@ -8,18 +8,19 @@
 #import <SafariServices/SFFoundation.h>
 
 #import <Foundation/Foundation.h>
+#import <SafariServices/SFError.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
 @class SFContentBlockerState;
 
-SF_EXTERN NSString * const SFContentBlockerErrorDomain NS_AVAILABLE_IOS(9_0);
+SF_EXTERN NSString * const SFContentBlockerErrorDomain NS_DEPRECATED_IOS(9_0, 10_0, "Please use SFErrorDomain.");
 
 typedef NS_ENUM(NSInteger, SFContentBlockerErrorCode) {
-    SFContentBlockerNoExtensionFound = 1,
-    SFContentBlockerNoAttachmentFound = 2,
-    SFContentBlockerLoadingInterrupted = 3,
-} NS_ENUM_AVAILABLE_IOS(9_0);
+    SFContentBlockerNoExtensionFound NS_ENUM_DEPRECATED_IOS(9_0, 10_0, "Please use SFErrorNoExtensionFound.") = SFErrorNoExtensionFound,
+    SFContentBlockerNoAttachmentFound NS_ENUM_DEPRECATED_IOS(9_0, 10_0, "Please use SFErrorNoAttachmentFound.") = SFErrorNoAttachmentFound,
+    SFContentBlockerLoadingInterrupted NS_ENUM_DEPRECATED_IOS(9_0, 10_0, "Please use SFErrorLoadingInterrupted.") = SFErrorLoadingInterrupted,
+} NS_ENUM_DEPRECATED_IOS(9_0, 10_0, "Please use SFErrorCode.");
 
 NS_CLASS_AVAILABLE_IOS(9_0)
 @interface SFContentBlockerManager : NSObject
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerState.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerState.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerState.h	2016-05-25 05:53:32.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerState.h	2016-06-26 10:37:48.000000000 +0200
@@ -5,6 +5,8 @@
 //  Copyright © 2016 Apple Inc. All rights reserved.
 //
 
+#import <Foundation/Foundation.h>
+
 NS_CLASS_AVAILABLE_IOS(10_0)
 @interface SFContentBlockerState : NSObject
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFError.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFError.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFError.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFError.h	2016-06-26 10:37:48.000000000 +0200
@@ -0,0 +1,18 @@
+//
+//  SFError.h
+//  SafariServices
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <SafariServices/SFFoundation.h>
+
+#import <Foundation/Foundation.h>
+
+SF_EXTERN NSString * const SFErrorDomain NS_AVAILABLE_IOS(10_0);
+
+typedef NS_ENUM(NSInteger, SFErrorCode) {
+    SFErrorNoExtensionFound = 1,
+    SFErrorNoAttachmentFound = 2,
+    SFErrorLoadingInterrupted = 3,
+} NS_ENUM_AVAILABLE_IOS(10_0);
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewController.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewController.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewController.h	2016-05-25 05:53:32.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewController.h	2016-06-26 10:37:48.000000000 +0200
@@ -25,7 +25,7 @@
  initialized. */
 @property (nonatomic, readonly, copy) SFSafariViewControllerConfiguration *configuration NS_AVAILABLE_IOS(10_0);
 
-/*! @abstract The view controller's delegate */
+/*! @abstract The view controller's delegate. */
 @property (nonatomic, weak, nullable) id <SFSafariViewControllerDelegate> delegate;
 
 - (instancetype)init NS_UNAVAILABLE;
@@ -33,8 +33,8 @@
 - (instancetype)initWithNibName:(nullable NSString *)nibNameOrNil bundle:(nullable NSBundle *)nibBundleOrNil NS_UNAVAILABLE;
 
 /*! @abstract Returns a view controller that loads a URL.
- @param URL, the URL to navigate to.
- @param configuration the configuration for the new view controller
+ @param URL the initial URL to navigate to. Only supports initial URLs with http:// or https:// schemes.
+ @param configuration the configuration for the new view controller.
  @discussion This is a designated initializer. You can use
  @link -initWithURL: @/link to initialize an instance with the default configuration. The initializer
  copies the specified configuration, so mutating the configuration after invoking the initializer has
@@ -43,14 +43,14 @@
 - (instancetype)initWithURL:(NSURL *)URL configuration:(SFSafariViewControllerConfiguration *)configuration NS_DESIGNATED_INITIALIZER NS_AVAILABLE_IOS(10_0);
 
 /*! @abstract Returns a view controller that loads a URL.
-    @param URL, the URL to navigate to.
+    @param URL the initial URL to navigate to. Only supports initial URLs with http:// or https:// schemes.
     @param entersReaderIfAvailable indicates if the Safari Reader version of content should be shown automatically
-    when Safari Reader is available on a web page
+    when Safari Reader is available on a web page.
  */
 - (instancetype)initWithURL:(NSURL *)URL entersReaderIfAvailable:(BOOL)entersReaderIfAvailable NS_DEPRECATED_IOS(9_0, 10_0, "Please use initWithURL:configuration:");
 
 /*! @abstract Returns a view controller that loads a URL.
-    @param URL, the URL to navigate to.
+    @param URL the initial URL to navigate to. Only supports initial URLs with http:// or https:// schemes.
  */
 - (instancetype)initWithURL:(NSURL *)URL;
 
@@ -61,8 +61,8 @@
 @optional
 
 /*! @abstract Called when the view controller is about to show UIActivityViewController after the user taps the action button.
-    @param URL, the URL of the web page.
-    @param title, the title of the web page.
+    @param URL the URL of the web page.
+    @param title the title of the web page.
     @result Returns an array of UIActivity instances that will be appended to UIActivityViewController.
  */
 - (NSArray<UIActivity *> *)safariViewController:(SFSafariViewController *)controller activityItemsForURL:(NSURL *)URL title:(nullable NSString *)title;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SafariServices.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SafariServices.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SafariServices.h	2016-05-25 05:53:32.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SafariServices.h	2016-06-26 10:37:48.000000000 +0200
@@ -7,6 +7,7 @@
 
 #import <SafariServices/SFContentBlockerManager.h>
 #import <SafariServices/SFContentBlockerState.h>
+#import <SafariServices/SFError.h>
 #import <SafariServices/SFFoundation.h>
 #import <SafariServices/SFSafariViewController.h>
 #import <SafariServices/SFSafariViewControllerConfiguration.h>

```