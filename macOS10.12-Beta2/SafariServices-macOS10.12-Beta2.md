#SafariServices.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerManager.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerManager.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerManager.h	2016-06-02 06:00:00.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFContentBlockerManager.h	2016-06-27 01:42:30.000000000 +0200
@@ -10,19 +10,12 @@
 #if __OBJC2__
 
 #import <Foundation/Foundation.h>
+#import <SafariServices/SFError.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
 @class SFContentBlockerState;
 
-SF_EXTERN NSString * const SFContentBlockerErrorDomain SF_AVAILABLE_MAC_SAFARI(10_0);
-
-typedef NS_ENUM(NSInteger, SFContentBlockerErrorCode) {
-    SFContentBlockerNoExtensionFound = 1,
-    SFContentBlockerNoAttachmentFound = 2,
-    SFContentBlockerLoadingInterrupted = 3,
-} SF_ENUM_AVAILABLE_MAC_SAFARI(10_0);
-
 SF_CLASS_AVAILABLE_MAC_SAFARI(10_0)
 @interface SFContentBlockerManager : NSObject
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFError.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFError.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFError.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFError.h	2016-06-27 01:42:30.000000000 +0200
@@ -0,0 +1,22 @@
+//
+//  SFError.h
+//  SafariServices
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <SafariServices/SFFoundation.h>
+
+#if __OBJC2__
+
+#import <Foundation/Foundation.h>
+
+SF_EXTERN NSString * const SFErrorDomain SF_AVAILABLE_MAC_SAFARI(10_0);
+
+typedef NS_ENUM(NSInteger, SFErrorCode) {
+    SFErrorNoExtensionFound = 1,
+    SFErrorNoAttachmentFound = 2,
+    SFErrorLoadingInterrupted = 3,
+} SF_ENUM_AVAILABLE_MAC_SAFARI(10_0);
+
+#endif // __OBJC2__
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariExtensionHandling.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariExtensionHandling.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariExtensionHandling.h	2016-06-02 06:00:00.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariExtensionHandling.h	2016-06-27 01:42:30.000000000 +0200
@@ -20,7 +20,7 @@
 
 @optional
 /// This is called when a content script from an extension dispatches a message to the app extension.
-- (void)messageReceivedWithName:(NSString *)messageName fromPage:(SFSafariPage *)page userInfo:(nullable NSDictionary *)userInfo;
+- (void)messageReceivedWithName:(NSString *)messageName fromPage:(SFSafariPage *)page userInfo:(nullable NSDictionary<NSString *, id> *)userInfo;
 
 /// This is called when the extension's toolbar item is clicked.
 - (void)toolbarItemClickedInWindow:(SFSafariWindow *)window;
@@ -29,7 +29,7 @@
 - (void)validateToolbarItemInWindow:(SFSafariWindow *)window validationHandler:(void (^)(BOOL enabled, NSString *badgeText))validationHandler;
 
 /// This is called when one of the extension's context menu items is selected.
-- (void)contextMenuItemSelectedWithCommand:(NSString *)command inPage:(SFSafariPage *)page userInfo:(nullable NSDictionary *)userInfo;
+- (void)contextMenuItemSelectedWithCommand:(NSString *)command inPage:(SFSafariPage *)page userInfo:(nullable NSDictionary<NSString *, id> *)userInfo;
 
 /// This is called when the extension's popover is about to be opened.
 - (void)popoverWillShowInWindow:(SFSafariWindow *)window;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariExtensionManager.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariExtensionManager.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariExtensionManager.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariExtensionManager.h	2016-06-27 01:42:30.000000000 +0200
@@ -0,0 +1,25 @@
+//
+//  SFSafariExtensionManager.h
+//  Safari
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <SafariServices/SFFoundation.h>
+
+#if __OBJC2__
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class SFSafariExtensionState;
+
+SF_CLASS_AVAILABLE_MAC_SAFARI(10_0)
+@interface SFSafariExtensionManager : NSObject
+
++ (void)getStateOfSafariExtensionWithIdentifier:(NSString *)identifier completionHandler:(void (^)(SFSafariExtensionState * _Nullable state, NSError * _Nullable error))completionHandler;
+
+@end
+
+NS_ASSUME_NONNULL_END
+
+#endif // __OBJC2__
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariExtensionState.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariExtensionState.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariExtensionState.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariExtensionState.h	2016-06-27 01:42:30.000000000 +0200
@@ -0,0 +1,21 @@
+//
+//  SFSafariExtensionState.h
+//  Safari
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <SafariServices/SFFoundation.h>
+
+#if __OBJC2__
+
+#import <Foundation/Foundation.h>
+
+SF_CLASS_AVAILABLE_MAC_SAFARI(10_0)
+@interface SFSafariExtensionState : NSObject
+
+@property (nonatomic, readonly, getter=isEnabled) BOOL enabled;
+
+@end
+
+#endif // __OBJC2__
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariPage.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariPage.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariPage.h	2016-06-02 06:00:00.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSafariPage.h	2016-06-27 01:42:30.000000000 +0200
@@ -22,7 +22,7 @@
 - (instancetype)init NS_UNAVAILABLE;
 
 /// Dispatches a message to the content script injected in this page.
-- (void)dispatchMessageToScriptWithName:(NSString *)messageName userInfo:(nullable NSDictionary *)userInfo;
+- (void)dispatchMessageToScriptWithName:(NSString *)messageName userInfo:(nullable NSDictionary<NSString *, id> *)userInfo;
 
 /// Reloads the page.
 - (void)reload;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSwiftOverlaySupport.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSwiftOverlaySupport.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSwiftOverlaySupport.h	2016-06-02 06:00:00.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SFSwiftOverlaySupport.h	2016-06-27 01:42:30.000000000 +0200
@@ -14,7 +14,7 @@
 extern "C" {
 #endif
 
-extern void* _SFSafariServicesAvailable __attribute__((visibility("default"))) __attribute__((weak_import));
+extern void* _SFSafariServicesAvailable __attribute__((visibility("default"))) __attribute__((weak_import)) __attribute__((availability(swift, unavailable)));
 
 #ifdef __cplusplus
 }
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SafariServices.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SafariServices.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SafariServices.h	2016-06-02 06:00:00.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SafariServices.framework/Headers/SafariServices.h	2016-06-27 01:42:30.000000000 +0200
@@ -7,10 +7,13 @@
 
 #import <SafariServices/SFContentBlockerManager.h>
 #import <SafariServices/SFContentBlockerState.h>
+#import <SafariServices/SFError.h>
 #import <SafariServices/SFFoundation.h>
 #import <SafariServices/SFSafariApplication.h>
 #import <SafariServices/SFSafariExtensionHandler.h>
 #import <SafariServices/SFSafariExtensionHandling.h>
+#import <SafariServices/SFSafariExtensionManager.h>
+#import <SafariServices/SFSafariExtensionState.h>
 #import <SafariServices/SFSafariExtensionViewController.h>
 #import <SafariServices/SFSafariPage.h>
 #import <SafariServices/SFSafariPageProperties.h>

```