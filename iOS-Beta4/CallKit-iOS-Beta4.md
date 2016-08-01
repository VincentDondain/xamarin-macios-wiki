#CallKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXAuthorization.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXAuthorization.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXAuthorization.h	2016-07-11 07:03:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXAuthorization.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,23 +0,0 @@
-//
-//  CXAuthorization.h
-//  CallKit
-//
-//  Copyright © 2016 Apple. All rights reserved.
-//
-
-#import <Foundation/Foundation.h>
-
-NS_ASSUME_NONNULL_BEGIN
-
-typedef NS_ENUM(NSInteger, CXAuthorizationStatus) {
-    /// The user has not yet made a choice regarding whether the application may contibute calls.
-    CXAuthorizationStatusNotDetermined = 0,
-    /// The application is not authorized to contribute calls due to settings restrictions.
-    CXAuthorizationStatusRestricted = 1,
-    /// The user explicitly denied access for the application to contribute calls.
-    CXAuthorizationStatusDenied = 2,
-    /// The application is authorized to contribute calls.
-    CXAuthorizationStatusAuthorized = 3,
-} API_DEPRECATED("Authorization is no longer required", ios(10.0, 10.0));
-
-NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectory.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectory.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectory.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectory.h	2016-07-26 06:26:52.000000000 +0200
@@ -0,0 +1,16 @@
+//
+//  CXCallDirectory.h
+//  CallKit
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+typedef int64_t CXCallDirectoryPhoneNumber;
+
+static const CXCallDirectoryPhoneNumber CXCallDirectoryPhoneNumberMax = (INT64_MAX - 1);
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectoryExtensionContext.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectoryExtensionContext.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectoryExtensionContext.h	2016-07-11 07:03:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectoryExtensionContext.h	2016-07-26 06:26:52.000000000 +0200
@@ -7,15 +7,26 @@
 
 #import <Foundation/Foundation.h>
 #import <CallKit/CXBase.h>
+#import <CallKit/CXCallDirectory.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class CXCallDirectoryExtensionContext;
+
+@protocol CXCallDirectoryExtensionContextDelegate <NSObject>
+
+- (void)requestFailedForExtensionContext:(CXCallDirectoryExtensionContext *)extensionContext withError:(NSError *)error;
+
+@end
+
 CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXCallDirectoryExtensionContext : NSExtensionContext
 
-- (void)addBlockingEntryWithNextSequentialPhoneNumber:(NSString *)phoneNumber;
+@property (nonatomic, weak, nullable) id<CXCallDirectoryExtensionContextDelegate> delegate;
+
+- (void)addBlockingEntryWithNextSequentialPhoneNumber:(CXCallDirectoryPhoneNumber)phoneNumber;
 
-- (void)addIdentificationEntryWithNextSequentialPhoneNumber:(NSString *)phoneNumber label:(NSString *)label;
+- (void)addIdentificationEntryWithNextSequentialPhoneNumber:(CXCallDirectoryPhoneNumber)phoneNumber label:(NSString *)label;
 
 - (void)completeRequestWithCompletionHandler:(nullable void (^)(BOOL expired))completion;
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProvider.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProvider.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProvider.h	2016-07-11 07:04:13.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProvider.h	2016-07-26 06:26:51.000000000 +0200
@@ -7,7 +7,6 @@
 
 #import <Foundation/Foundation.h>
 #import <CallKit/CXBase.h>
-#import <CallKit/CXAuthorization.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -70,9 +69,6 @@
 CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXProvider : NSObject
 
-/// Returns the current authorization status of the calling application
-@property (readonly, class) CXAuthorizationStatus authorizationStatus API_DEPRECATED("Authorization is no longer required", ios(10.0, 10.0));
-
 /// Initialize a new provider instance with the supplied configuration
 - (instancetype)initWithConfiguration:(CXProviderConfiguration *)configuration NS_DESIGNATED_INITIALIZER;
 - (instancetype)init NS_UNAVAILABLE;
@@ -81,11 +77,6 @@
 /// A nil queue implies that delegate callbacks should happen on the main queue. The delegate is stored weakly
 - (void)setDelegate:(nullable id<CXProviderDelegate>)delegate queue:(nullable dispatch_queue_t)queue;
 
-/// Request permission to contribute calls.
-///
-/// This method must be called prior to using the provider. If the current authorization is anything other than `CXAuthorizationStatusNotDetermined`, this method does nothing. Otherwise, the result is delivered to the delegate's `provider:didChangeAuthorizationStatus:` method
-- (void)requestAuthorization API_DEPRECATED("Authorization is no longer required", ios(10.0, 10.0));
-
 /// Report a new incoming call to the system.
 ///
 /// If completion is invoked with a non-nil `error`, the incoming call has been disallowed by the system and will not be displayed, so the provider should not proceed with the call.
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProviderConfiguration.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProviderConfiguration.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProviderConfiguration.h	2016-07-11 07:03:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProviderConfiguration.h	2016-07-26 06:26:52.000000000 +0200
@@ -19,7 +19,8 @@
 /// Name of resource in app's bundle to play as ringtone for incoming call
 @property (nonatomic, strong, nullable) NSString *ringtoneSound;
 
-@property (nonatomic, strong, nullable) NSData *iconMaskImageData; // Image should be a square with side length of 40 points
+@property (nonatomic, copy, nullable) NSData *iconTemplateImageData; // Image should be a square with side length of 40 points
+@property (nonatomic, strong, nullable) NSData *iconMaskImageData API_DEPRECATED_WITH_REPLACEMENT("iconTemplateImageData", ios(10.0, 10.0)); // Note: will be removed in a future beta SDK
 @property (nonatomic) NSUInteger maximumCallGroups; // Default 2
 @property (nonatomic) NSUInteger maximumCallsPerCallGroup; // Default 5
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXStartCallAction.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXStartCallAction.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXStartCallAction.h	2016-07-11 07:03:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXStartCallAction.h	2016-07-26 06:26:52.000000000 +0200
@@ -16,12 +16,15 @@
 
 - (instancetype)initWithCallUUID:(NSUUID *)callUUID handle:(CXHandle *)handle NS_DESIGNATED_INITIALIZER;
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithCallUUID:(NSUUID *)callUUID NS_UNAVAILABLE;
 
 /// Handle for the party to call
 @property (nonatomic, copy) CXHandle *handle;
 
 @property (nonatomic, copy, nullable) NSString *contactIdentifier;
 
+@property (nonatomic, getter=isVideo) BOOL video;
+
 /// Normally, providers can just call -[CXAction fulfill] to indicate action fulfillment. Use this method to note a specific date that the call started if it is different from [NSDate date]. A call is considered started when its invitation has been sent to the remote callee.
 - (void)fulfillWithDateStarted:(NSDate *)dateStarted;
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXTransaction.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXTransaction.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXTransaction.h	2016-07-11 07:03:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXTransaction.h	2016-07-26 06:26:52.000000000 +0200
@@ -24,6 +24,9 @@
 /// The list of actions contained by the receiver
 @property (nonatomic, readonly, copy) NSArray<__kindof CXAction *> *actions;
 
+- (instancetype)initWithActions:(NSArray<CXAction *> *)actions NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithAction:(CXAction *)action;
+
 /// Add the provided action to the receiver's list of actions
 - (void)addAction:(CXAction *)action;
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CallKit.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CallKit.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CallKit.h	2016-07-11 07:03:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CallKit.h	2016-07-26 06:26:52.000000000 +0200
@@ -9,8 +9,6 @@
 
 #import <CallKit/CXBase.h>
 
-#import <CallKit/CXAuthorization.h>
-
 #import <CallKit/CXCallUpdate.h>
 #import <CallKit/CXHandle.h>
 #import <CallKit/CXError.h>
@@ -34,6 +32,7 @@
 #import <CallKit/CXCallObserver.h>
 #import <CallKit/CXCallController.h>
 
+#import <CallKit/CXCallDirectory.h>
 #import <CallKit/CXCallDirectoryManager.h>
 #import <CallKit/CXCallDirectoryProvider.h>
 #import <CallKit/CXCallDirectoryExtensionContext.h>

```