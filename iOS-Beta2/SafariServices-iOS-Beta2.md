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

```