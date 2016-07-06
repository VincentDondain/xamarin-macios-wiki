#SafariServices.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerManager.h	2015-10-05 03:14:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerManager.h	2016-05-25 05:53:32.000000000 +0200
@@ -11,6 +11,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class SFContentBlockerState;
+
 SF_EXTERN NSString * const SFContentBlockerErrorDomain NS_AVAILABLE_IOS(9_0);
 
 typedef NS_ENUM(NSInteger, SFContentBlockerErrorCode) {
@@ -22,7 +24,8 @@
 NS_CLASS_AVAILABLE_IOS(9_0)
 @interface SFContentBlockerManager : NSObject
 
-+ (void)reloadContentBlockerWithIdentifier:(NSString *)identifier completionHandler:(void (^__nullable)(NSError *__nullable error))completionHandler;
++ (void)reloadContentBlockerWithIdentifier:(NSString *)identifier completionHandler:(void (^_Nullable)(NSError *_Nullable error))completionHandler;
++ (void)getStateOfContentBlockerWithIdentifier:(NSString *)identifier completionHandler:(void (^)(SFContentBlockerState *_Nullable state, NSError *_Nullable error))completionHandler NS_AVAILABLE_IOS(10_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerState.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerState.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerState.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerState.h	2016-05-25 05:53:32.000000000 +0200
@@ -0,0 +1,13 @@
+//
+//  SFContentBlockerState.h
+//  SafariServices
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+NS_CLASS_AVAILABLE_IOS(10_0)
+@interface SFContentBlockerState : NSObject
+
+@property (nonatomic, readonly, getter=isEnabled) BOOL enabled;
+
+@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewController.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewController.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewController.h	2015-10-05 03:14:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewController.h	2016-05-25 05:53:32.000000000 +0200
@@ -10,6 +10,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class SFSafariViewControllerConfiguration;
 @protocol SFSafariViewControllerDelegate;
 
 /*!
@@ -20,19 +21,33 @@
 NS_CLASS_AVAILABLE_IOS(9_0)
 @interface SFSafariViewController : UIViewController
 
+/*! @abstract A copy of the configuration with which the view controller was
+ initialized. */
+@property (nonatomic, readonly, copy) SFSafariViewControllerConfiguration *configuration NS_AVAILABLE_IOS(10_0);
+
 /*! @abstract The view controller's delegate */
-@property (nonatomic, weak, nullable) id<SFSafariViewControllerDelegate> delegate;
+@property (nonatomic, weak, nullable) id <SFSafariViewControllerDelegate> delegate;
 
 - (instancetype)init NS_UNAVAILABLE;
 - (instancetype)initWithCoder:(NSCoder *)aDecoder NS_UNAVAILABLE;
 - (instancetype)initWithNibName:(nullable NSString *)nibNameOrNil bundle:(nullable NSBundle *)nibBundleOrNil NS_UNAVAILABLE;
 
 /*! @abstract Returns a view controller that loads a URL.
+ @param URL, the URL to navigate to.
+ @param configuration the configuration for the new view controller
+ @discussion This is a designated initializer. You can use
+ @link -initWithURL: @/link to initialize an instance with the default configuration. The initializer
+ copies the specified configuration, so mutating the configuration after invoking the initializer has
+ no effect on the view controller.
+ */
+- (instancetype)initWithURL:(NSURL *)URL configuration:(SFSafariViewControllerConfiguration *)configuration NS_DESIGNATED_INITIALIZER NS_AVAILABLE_IOS(10_0);
+
+/*! @abstract Returns a view controller that loads a URL.
     @param URL, the URL to navigate to.
     @param entersReaderIfAvailable indicates if the Safari Reader version of content should be shown automatically
     when Safari Reader is available on a web page
  */
-- (instancetype)initWithURL:(NSURL *)URL entersReaderIfAvailable:(BOOL)entersReaderIfAvailable NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithURL:(NSURL *)URL entersReaderIfAvailable:(BOOL)entersReaderIfAvailable NS_DEPRECATED_IOS(9_0, 10_0, "Please use initWithURL:configuration:");
 
 /*! @abstract Returns a view controller that loads a URL.
     @param URL, the URL to navigate to.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewControllerConfiguration.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewControllerConfiguration.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewControllerConfiguration.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariViewControllerConfiguration.h	2016-05-25 05:53:32.000000000 +0200
@@ -0,0 +1,28 @@
+//
+//  SFSafariViewControllerConfiguration.h
+//  SafariServices
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <SafariServices/SFFoundation.h>
+#import <UIKit/UIKit.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE_IOS(10_0)
+@interface SFSafariViewControllerConfiguration : NSObject
+
+/*! @abstract Indicates if SFSafariViewController should automatically show the Reader version of web pages. This will only
+    happen when Safari Reader is available on a web page.
+ */
+@property (nonatomic) BOOL entersReaderIfAvailable;
+
+/*! @abstract The preferred color to tint the background of the navigation bar and tool bar. If SFSafariViewController is in Private Browsing
+    mode or is displaying an anti-phishing warning page, this color will be ignored.
+ */
+@property (nonatomic) UIColor *preferredBarTintColor;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SafariServices.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SafariServices.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SafariServices.h	2015-10-05 03:14:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SafariServices.h	2016-05-25 05:53:32.000000000 +0200
@@ -6,6 +6,8 @@
 //
 
 #import <SafariServices/SFContentBlockerManager.h>
+#import <SafariServices/SFContentBlockerState.h>
 #import <SafariServices/SFFoundation.h>
 #import <SafariServices/SFSafariViewController.h>
+#import <SafariServices/SFSafariViewControllerConfiguration.h>
 #import <SafariServices/SSReadingList.h>

```