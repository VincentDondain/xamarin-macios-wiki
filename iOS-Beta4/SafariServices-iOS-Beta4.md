#SafariServices.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewController.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewController.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewController.h	2016-07-10 13:33:50.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewController.h	2016-07-25 09:38:55.000000000 +0200
@@ -10,7 +10,6 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-@class SFSafariViewControllerConfiguration;
 @protocol SFSafariViewControllerDelegate;
 
 /*!
@@ -21,39 +20,37 @@
 NS_CLASS_AVAILABLE_IOS(9_0)
 @interface SFSafariViewController : UIViewController
 
-/*! @abstract A copy of the configuration with which the view controller was
- initialized. */
-@property (nonatomic, readonly, copy) SFSafariViewControllerConfiguration *configuration NS_AVAILABLE_IOS(10_0);
-
-/*! @abstract The view controller's delegate. */
-@property (nonatomic, weak, nullable) id <SFSafariViewControllerDelegate> delegate;
-
 - (instancetype)init NS_UNAVAILABLE;
 - (instancetype)initWithCoder:(NSCoder *)aDecoder NS_UNAVAILABLE;
 - (instancetype)initWithNibName:(nullable NSString *)nibNameOrNil bundle:(nullable NSBundle *)nibBundleOrNil NS_UNAVAILABLE;
 
 /*! @abstract Returns a view controller that loads a URL.
- @param URL the initial URL to navigate to. Only supports initial URLs with http:// or https:// schemes.
- @param configuration the configuration for the new view controller.
- @discussion This is a designated initializer. You can use
- @link -initWithURL: @/link to initialize an instance with the default configuration. The initializer
- copies the specified configuration, so mutating the configuration after invoking the initializer has
- no effect on the view controller.
- */
-- (instancetype)initWithURL:(NSURL *)URL configuration:(SFSafariViewControllerConfiguration *)configuration NS_DESIGNATED_INITIALIZER NS_AVAILABLE_IOS(10_0);
-
-/*! @abstract Returns a view controller that loads a URL.
     @param URL the initial URL to navigate to. Only supports initial URLs with http:// or https:// schemes.
     @param entersReaderIfAvailable indicates if the Safari Reader version of content should be shown automatically
     when Safari Reader is available on a web page.
  */
-- (instancetype)initWithURL:(NSURL *)URL entersReaderIfAvailable:(BOOL)entersReaderIfAvailable NS_DEPRECATED_IOS(9_0, 10_0, "Please use initWithURL:configuration:");
+- (instancetype)initWithURL:(NSURL *)URL entersReaderIfAvailable:(BOOL)entersReaderIfAvailable NS_DESIGNATED_INITIALIZER;
 
 /*! @abstract Returns a view controller that loads a URL.
     @param URL the initial URL to navigate to. Only supports initial URLs with http:// or https:// schemes.
  */
 - (instancetype)initWithURL:(NSURL *)URL;
 
+/*! @abstract The view controller's delegate. */
+@property (nonatomic, weak, nullable) id <SFSafariViewControllerDelegate> delegate;
+
+/*! @abstract The preferred color to tint the background of the navigation bar and toolbar. If SFSafariViewController is in Private
+    Browsing mode or is displaying an anti-phishing warning page, this color will be ignored. Changes made after the view controller
+    has been presented will not be reflected.
+ */
+@property (nonatomic) UIColor *preferredBarTintColor NS_AVAILABLE_IOS(10_0);
+
+/*! @abstract The preferred color to tint the control buttons on the navigation bar and toolbar. If SFSafariViewController is in Private
+    Browsing mode or is displaying an anti-phishing warning page, this color will be ignored. Changes made after the view controller
+    has been presented will not be reflected.
+ */
+@property (nonatomic) UIColor *preferredControlTintColor NS_AVAILABLE_IOS(10_0);
+
 @end
 
 NS_AVAILABLE_IOS(9_0)
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewControllerConfiguration.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewControllerConfiguration.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewControllerConfiguration.h	2016-07-10 13:33:50.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewControllerConfiguration.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,28 +0,0 @@
-//
-//  SFSafariViewControllerConfiguration.h
-//  SafariServices
-//
-//  Copyright © 2016 Apple Inc. All rights reserved.
-//
-
-#import <SafariServices/SFFoundation.h>
-#import <UIKit/UIKit.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-NS_CLASS_AVAILABLE_IOS(10_0)
-@interface SFSafariViewControllerConfiguration : NSObject
-
-/*! @abstract Indicates if SFSafariViewController should automatically show the Reader version of web pages. This will only
-    happen when Safari Reader is available on a web page.
- */
-@property (nonatomic) BOOL entersReaderIfAvailable;
-
-/*! @abstract The preferred color to tint the background of the navigation bar and tool bar. If SFSafariViewController is in Private Browsing
-    mode or is displaying an anti-phishing warning page, this color will be ignored.
- */
-@property (nonatomic) UIColor *preferredBarTintColor;
-
-@end
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SafariServices.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SafariServices.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SafariServices.h	2016-07-10 13:33:50.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SafariServices.h	2016-07-25 09:38:55.000000000 +0200
@@ -10,5 +10,4 @@
 #import <SafariServices/SFError.h>
 #import <SafariServices/SFFoundation.h>
 #import <SafariServices/SFSafariViewController.h>
-#import <SafariServices/SFSafariViewControllerConfiguration.h>
 #import <SafariServices/SSReadingList.h>

```