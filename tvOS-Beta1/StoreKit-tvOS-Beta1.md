#StoreKit.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKCloudServiceController.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKCloudServiceController.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKCloudServiceController.h	2016-08-02 05:15:17.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKCloudServiceController.h	2016-10-23 10:46:59.000000000 +0200
@@ -2,7 +2,7 @@
 //  SKCloudServiceController.h
 //  StoreKit
 //
-//  Copyright © 2015 Apple Inc. All rights reserved.
+//  Copyright © 2015-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
@@ -20,6 +20,7 @@
 typedef NS_OPTIONS(NSUInteger, SKCloudServiceCapability) {
     SKCloudServiceCapabilityNone                           = 0,
     SKCloudServiceCapabilityMusicCatalogPlayback           = 1 << 0,
+    SKCloudServiceCapabilityMusicCatalogSubscriptionEligible    NS_ENUM_AVAILABLE_IOS(10_1)  = 1 << 1,
     SKCloudServiceCapabilityAddToCloudMusicLibrary         = 1 << 8,
 } NS_AVAILABLE_IOS(9_3);
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKCloudServiceSetupViewController.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKCloudServiceSetupViewController.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKCloudServiceSetupViewController.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/StoreKit.framework/Headers/SKCloudServiceSetupViewController.h	2016-10-23 10:46:59.000000000 +0200
@@ -0,0 +1,51 @@
+//
+//  SKCloudServiceSetupViewController.h
+//  StoreKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <StoreKit/StoreKitDefines.h>
+#import <UIKit/UIKit.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+typedef NSString * SKCloudServiceSetupOptionsKey NS_STRING_ENUM;
+typedef NSString * SKCloudServiceSetupAction NS_STRING_ENUM;
+
+@protocol SKCloudServiceSetupViewControllerDelegate;
+
+/// View controller to allow user to setup iTunes Store account for cloud service, such as Apple Music subscription.
+SK_EXTERN_CLASS_AVAILABLE(10_1) __TVOS_PROHIBITED @interface SKCloudServiceSetupViewController : UIViewController
+
+/// Optional delegate.
+@property (nonatomic, nullable, weak) id <SKCloudServiceSetupViewControllerDelegate> delegate;
+
+/// Load cloud service setup view with the given options.
+/// Block is invoked on the main thread when the load finishes.
+- (void)loadWithOptions:(NSDictionary<SKCloudServiceSetupOptionsKey, id> *)options completionHandler:(nullable void (^)(BOOL result, NSError * _Nullable error))completionHandler;
+
+@end
+
+
+@protocol SKCloudServiceSetupViewControllerDelegate <NSObject>
+
+@optional
+
+/// Sent when the view controller was dismissed.
+- (void)cloudServiceSetupViewControllerDidDismiss:(SKCloudServiceSetupViewController *)cloudServiceSetupViewController __TVOS_PROHIBITED NS_AVAILABLE_IOS(10_1);
+
+@end
+
+
+/// Action for setup entry point (of type SKCloudServiceSetupAction).
+SK_EXTERN SKCloudServiceSetupOptionsKey const SKCloudServiceSetupOptionsActionKey NS_SWIFT_NAME(action) NS_AVAILABLE_IOS(10_1);
+
+/// Identifier of the iTunes Store item the user is trying to access which requires cloud service setup (NSNumber).
+SK_EXTERN SKCloudServiceSetupOptionsKey const SKCloudServiceSetupOptionsITunesItemIdentifierKey NS_SWIFT_NAME(iTunesItemIdentifier) NS_AVAILABLE_IOS(10_1);
+
+// Supported actions for setup entry point.
+
+SK_EXTERN SKCloudServiceSetupAction const SKCloudServiceSetupActionSubscribe NS_AVAILABLE_IOS(10_1);
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/StoreKit.framework/Headers/StoreKit.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/StoreKit.framework/Headers/StoreKit.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/StoreKit.framework/Headers/StoreKit.h	2016-08-02 05:15:17.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/StoreKit.framework/Headers/StoreKit.h	2016-10-23 10:46:59.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <StoreKit/SKCloudServiceController.h>
+#import <StoreKit/SKCloudServiceSetupViewController.h>
 #import <StoreKit/SKDownload.h>
 #import <StoreKit/SKError.h>
 #import <StoreKit/SKPayment.h>

```