#CallKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCall.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCall.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCall.h	2016-05-25 04:41:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCall.h	2016-06-27 07:46:22.000000000 +0200
@@ -21,6 +21,8 @@
 
 - (instancetype)init NS_UNAVAILABLE;
 
+- (BOOL)isEqualToCall:(CXCall *)call;
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallAction.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallAction.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallAction.h	2016-05-25 04:41:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallAction.h	2016-06-27 07:46:22.000000000 +0200
@@ -9,8 +9,6 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-@class CXCallActionResponse;
-
 NS_CLASS_AVAILABLE(10_12, 10_0)
 @interface CXCallAction : CXAction
 
@@ -20,8 +18,6 @@
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
 - (instancetype)init NS_UNAVAILABLE;
 
-- (void)fulfillWithResponse:(nullable CXCallActionResponse *)response DEPRECATED_MSG_ATTRIBUTE("Use -[CXAction fulfill] instead");
-
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallUpdate.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallUpdate.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallUpdate.h	2016-05-25 04:41:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallUpdate.h	2016-06-27 07:46:22.000000000 +0200
@@ -9,13 +9,19 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class CXHandle;
+
 // Any property that is not set will be ignored
 
 NS_CLASS_AVAILABLE(10_12, 10_0)
 @interface CXCallUpdate : NSObject <NSCopying>
 
+/// Handle for the remote party (for an incoming call, the caller; for an outgoing call, the callee)
+@property (nonatomic, copy, nullable) CXHandle *remoteHandle;
+
 /// Identifier for the remote party (e.g. phone number, email address)
-@property (nonatomic, copy, nullable) NSString *callerIdentifier;
+/// NOTE: Will be removed in a future beta SDK version.
+@property (nonatomic, copy, nullable) NSString *callerIdentifier NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use CXCallUpdate.remoteHandle instead");
 
 /// Override the computed caller name to a provider-defined value.
 /// Normally the system will determine the appropriate caller name to display (e.g. using the user's contacts) based on the supplied caller identifier. Set this property to customize.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXError.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXError.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXError.h	2016-05-25 04:41:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXError.h	2016-06-27 07:46:22.000000000 +0200
@@ -33,8 +33,9 @@
     CXErrorCodeRequestTransactionErrorUnknownCallProvider = 2,
     CXErrorCodeRequestTransactionErrorEmptyTransaction = 3,
     CXErrorCodeRequestTransactionErrorUnknownCallUUID = 4,
-    CXErrorCodeRequestTransactionErrorInvalidAction = 5,
-    CXErrorCodeRequestTransactionErrorMaximumCallGroupsReached = 6,
+    CXErrorCodeRequestTransactionErrorCallUUIDAlreadyExists = 5,
+    CXErrorCodeRequestTransactionErrorInvalidAction = 6,
+    CXErrorCodeRequestTransactionErrorMaximumCallGroupsReached = 7,
 } NS_ENUM_AVAILABLE(10_12, 10_0);
 
 typedef NS_ENUM(NSInteger, CXErrorCodeCallDirectoryManagerError) {
@@ -42,9 +43,10 @@
     CXErrorCodeCallDirectoryManagerErrorNoExtensionFound = 1,
     CXErrorCodeCallDirectoryManagerErrorNoAttachmentFound = 2,
     CXErrorCodeCallDirectoryManagerErrorLoadingInterrupted = 3,
-    CXErrorCodeCallDirectoryManagerErrorParsingFailed = 4,
-    CXErrorCodeCallDirectoryManagerErrorMaximumEntriesExceeded = 5,
-    CXErrorCodeCallDirectoryManagerErrorExtensionDisabled = 6,
+    CXErrorCodeCallDirectoryManagerErrorEntriesOutOfOrder = 4,
+    CXErrorCodeCallDirectoryManagerErrorDuplicateEntries = 5,
+    CXErrorCodeCallDirectoryManagerErrorMaximumEntriesExceeded = 6,
+    CXErrorCodeCallDirectoryManagerErrorExtensionDisabled = 7,
 } NS_ENUM_AVAILABLE(10_12, 10_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXHandle.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXHandle.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXHandle.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXHandle.h	2016-06-27 07:46:22.000000000 +0200
@@ -0,0 +1,31 @@
+//
+//  CXHandle.h
+//  CallKit
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+typedef NS_ENUM(NSInteger, CXHandleType) {
+    CXHandleTypeGeneric = 1,
+    CXHandleTypePhoneNumber = 2,
+    CXHandleTypeEmailAddress = 3,
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CXHandle : NSObject <NSCopying, NSSecureCoding>
+
+@property (nonatomic, readonly) CXHandleType type;
+@property (nonatomic, readonly, copy) NSString *value;
+
+- (instancetype)initWithType:(CXHandleType)type value:(NSString *)value NS_DESIGNATED_INITIALIZER;
+- (instancetype)init NS_UNAVAILABLE;
+
+- (BOOL)isEqualToHandle:(CXHandle *)handle;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXPlayDTMFCallAction.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXPlayDTMFCallAction.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXPlayDTMFCallAction.h	2016-05-25 04:41:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXPlayDTMFCallAction.h	2016-06-27 07:46:22.000000000 +0200
@@ -18,6 +18,12 @@
 NS_CLASS_AVAILABLE(10_12, 10_0)
 @interface CXPlayDTMFCallAction : CXCallAction
 
+- (instancetype)initWithCallUUID:(NSUUID *)callUUID digits:(NSString *)digits type:(CXPlayDTMFCallActionType)type NS_DESIGNATED_INITIALIZER;
+- (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
+
+/// NOTE: Will be removed in a future beta SDK version.
+- (instancetype)initWithCallUUID:(NSUUID *)callUUID NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use CXPlayDTMFCallAction(call:digits:type:) instead");
+
 // The string representation of the digits that should be played as DTMF tones
 @property (nonatomic, copy) NSString *digits;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProvider.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProvider.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProvider.h	2016-05-25 04:42:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProvider.h	2016-06-27 07:46:22.000000000 +0200
@@ -32,11 +32,12 @@
 } NS_ENUM_AVAILABLE(10_12, 10_0);
 
 @protocol CXProviderDelegate <NSObject>
-@optional
 
 /// Called when the provider has been reset. Delegates must respond to this callback by cleaning up all internal call state (disconnecting communication channels, releasing network resources, etc.). This callback can be treated as a request to end all calls without the need to respond to any actions
 - (void)providerDidReset:(CXProvider *)provider;
 
+@optional
+
 /// Called when the provider has been fully created and is ready to send actions and receive updates
 - (void)providerDidBegin:(CXProvider *)provider;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProviderConfiguration.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProviderConfiguration.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProviderConfiguration.h	2016-05-25 04:41:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProviderConfiguration.h	2016-06-27 07:46:22.000000000 +0200
@@ -18,11 +18,15 @@
 /// Name of resource in app's bundle to play as ringtone for incoming call
 @property (nonatomic, strong, nullable) NSString *ringtoneSound;
 
+@property (nonatomic, strong, nullable) NSData *iconMaskImageData; // Image should be a square with side length of 40 points
 @property (nonatomic) NSUInteger maximumCallGroups; // Default 2
 @property (nonatomic) NSUInteger maximumCallsPerCallGroup; // Default 5
 
 @property (nonatomic) BOOL supportsVideo; // Default NO
 
+// Numbers are of type CXHandleType
+@property (nonatomic, copy) NSSet<NSNumber *> *supportedHandleTypes;
+
 - (instancetype)initWithLocalizedName:(NSString *)localizedName;
 - (instancetype)init NS_UNAVAILABLE;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetGroupCallAction.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetGroupCallAction.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetGroupCallAction.h	2016-05-25 04:41:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetGroupCallAction.h	2016-06-27 07:46:22.000000000 +0200
@@ -12,6 +12,12 @@
 NS_CLASS_AVAILABLE(10_12, 10_0)
 @interface CXSetGroupCallAction : CXCallAction
 
+- (instancetype)initWithCallUUID:(NSUUID *)callUUID callUUIDToGroupWith:(nullable NSUUID *)callUUIDToGroupWith NS_DESIGNATED_INITIALIZER;
+- (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
+
+/// NOTE: Will be removed in a future beta SDK version.
+- (instancetype)initWithCallUUID:(NSUUID *)callUUID NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use CXSetGroupCallAction(call:callUUIDToGroupWith:) instead");
+
 /// The UUID of another call to group with.
 ///
 /// - If the call for this action's UUID is already in a group, it should leave that group if necessary.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetHeldCallAction.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetHeldCallAction.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetHeldCallAction.h	2016-05-25 04:41:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetHeldCallAction.h	2016-06-27 07:46:22.000000000 +0200
@@ -12,6 +12,12 @@
 NS_CLASS_AVAILABLE(10_12, 10_0)
 @interface CXSetHeldCallAction : CXCallAction
 
+- (instancetype)initWithCallUUID:(NSUUID *)callUUID onHold:(BOOL)onHold NS_DESIGNATED_INITIALIZER;
+- (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
+
+/// NOTE: Will be removed in a future beta SDK version.
+- (instancetype)initWithCallUUID:(NSUUID *)callUUID NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use CXSetHeldCallAction(call:onHold:) instead");
+
 @property (nonatomic, getter=isOnHold) BOOL onHold;
 
 @end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetMutedCallAction.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetMutedCallAction.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetMutedCallAction.h	2016-05-25 04:41:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetMutedCallAction.h	2016-06-27 07:46:22.000000000 +0200
@@ -12,6 +12,12 @@
 NS_CLASS_AVAILABLE(10_12, 10_0)
 @interface CXSetMutedCallAction : CXCallAction
 
+- (instancetype)initWithCallUUID:(NSUUID *)callUUID muted:(BOOL)muted NS_DESIGNATED_INITIALIZER;
+- (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
+
+/// NOTE: Will be removed in a future beta SDK version.
+- (instancetype)initWithCallUUID:(NSUUID *)callUUID NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use CXSetMutedCallAction(call:muted:) instead");
+
 @property (nonatomic, getter=isMuted) BOOL muted;
 
 @end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXStartCallAction.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXStartCallAction.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXStartCallAction.h	2016-05-25 04:41:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXStartCallAction.h	2016-06-27 07:46:22.000000000 +0200
@@ -9,11 +9,22 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class CXHandle;
+
 NS_CLASS_AVAILABLE(10_12, 10_0)
 @interface CXStartCallAction : CXCallAction
 
-// TODO improve name?
-@property (nonatomic, copy) NSString *destination;
+- (instancetype)initWithCallUUID:(NSUUID *)callUUID handle:(CXHandle *)handle NS_DESIGNATED_INITIALIZER;
+- (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
+
+/// NOTE: Will be removed in a future beta SDK version.
+- (instancetype)initWithCallUUID:(NSUUID *)callUUID NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use CXStartCallAction(call:handle:) instead");
+
+/// Handle for the party to call
+@property (nonatomic, copy) CXHandle *handle;
+
+/// NOTE: Will be removed in a future beta SDK version.
+@property (nonatomic, copy) NSString *destination NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use CXStartCallAction.handle instead");
 
 @property (nonatomic, copy, nullable) NSString *contactIdentifier;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CallKit.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CallKit.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CallKit.h	2016-05-25 04:41:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CallKit.h	2016-06-27 07:46:22.000000000 +0200
@@ -12,6 +12,7 @@
 #import <CallKit/CXAuthorization.h>
 
 #import <CallKit/CXCallUpdate.h>
+#import <CallKit/CXHandle.h>
 #import <CallKit/CXError.h>
 
 #import <CallKit/CXAction.h>

```