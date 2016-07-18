#CallKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXAction.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXAction.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXAction.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXAction.h	2016-07-11 07:03:59.000000000 +0200
@@ -6,10 +6,11 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <CallKit/CXBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXAction : NSObject <NSCopying, NSSecureCoding>
 
 /// Unique ID
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXAnswerCallAction.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXAnswerCallAction.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXAnswerCallAction.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXAnswerCallAction.h	2016-07-11 07:03:59.000000000 +0200
@@ -9,7 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXAnswerCallAction : CXCallAction
 
 /// Normally, providers can just call -[CXAction fulfill] to indicate action fulfillment. Use this method to note a specific date that the call connected. A call is considered connected when both caller and callee can start communicating.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXAuthorization.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXAuthorization.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXAuthorization.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXAuthorization.h	2016-07-11 07:03:59.000000000 +0200
@@ -5,6 +5,8 @@
 //  Copyright © 2016 Apple. All rights reserved.
 //
 
+#import <Foundation/Foundation.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 typedef NS_ENUM(NSInteger, CXAuthorizationStatus) {
@@ -16,6 +18,6 @@
     CXAuthorizationStatusDenied = 2,
     /// The application is authorized to contribute calls.
     CXAuthorizationStatusAuthorized = 3,
-} NS_ENUM_AVAILABLE(10_12, 10_0);
+} API_DEPRECATED("Authorization is no longer required", ios(10.0, 10.0));
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXBase.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXBase.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXBase.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXBase.h	2016-07-11 07:03:59.000000000 +0200
@@ -15,6 +15,8 @@
 #define CX_EXTERN extern __attribute__((visibility("default")))
 #endif
 
+#define CX_CLASS_AVAILABLE(...) CX_EXTERN API_AVAILABLE(__VA_ARGS__)
+
 #define CXBundleIdentifier "com.apple.CallKit"
 #define CXBundleIdentifierLowercase "com.apple.callkit"
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCall.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCall.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCall.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCall.h	2016-07-11 07:03:59.000000000 +0200
@@ -6,10 +6,11 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <CallKit/CXBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXCall : NSObject
 
 @property (nonatomic, readonly, copy) NSUUID *UUID;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallAction.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallAction.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallAction.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallAction.h	2016-07-11 07:03:59.000000000 +0200
@@ -9,7 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXCallAction : CXAction
 
 @property (nonatomic, readonly, copy) NSUUID *callUUID;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallController.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallController.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallController.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallController.h	2016-07-11 07:03:59.000000000 +0200
@@ -6,13 +6,14 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <CallKit/CXBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
 @class CXCallObserver;
 @class CXTransaction;
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXCallController : NSObject
 
 /// Initialize call controller with a private, serial queue.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectoryExtensionContext.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectoryExtensionContext.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectoryExtensionContext.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectoryExtensionContext.h	2016-07-11 07:03:59.000000000 +0200
@@ -6,10 +6,11 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <CallKit/CXBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXCallDirectoryExtensionContext : NSExtensionContext
 
 - (void)addBlockingEntryWithNextSequentialPhoneNumber:(NSString *)phoneNumber;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectoryManager.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectoryManager.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectoryManager.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectoryManager.h	2016-07-11 07:03:59.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <CallKit/CXBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -13,9 +14,9 @@
     CXCallDirectoryEnabledStatusUnknown = 0,
     CXCallDirectoryEnabledStatusDisabled = 1,
     CXCallDirectoryEnabledStatusEnabled = 2,
-} NS_ENUM_AVAILABLE(10_12, 10_0);
+} API_AVAILABLE(ios(10.0));
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXCallDirectoryManager : NSObject
 
 @property (readonly, class) CXCallDirectoryManager *sharedInstance;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectoryProvider.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectoryProvider.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectoryProvider.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallDirectoryProvider.h	2016-07-11 07:03:59.000000000 +0200
@@ -6,12 +6,13 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <CallKit/CXBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
 @class CXCallDirectoryExtensionContext;
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXCallDirectoryProvider : NSObject <NSExtensionRequestHandling>
 
 - (void)beginRequestWithExtensionContext:(CXCallDirectoryExtensionContext *)context;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallObserver.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallObserver.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallObserver.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallObserver.h	2016-07-11 07:03:59.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <CallKit/CXBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -18,7 +19,7 @@
 
 @end
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXCallObserver : NSObject
 
 /// Retrieve the current call list, blocking on initial state retrieval if necessary
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallUpdate.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallUpdate.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallUpdate.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCallUpdate.h	2016-07-11 07:03:59.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <CallKit/CXBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -13,16 +14,12 @@
 
 // Any property that is not set will be ignored
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXCallUpdate : NSObject <NSCopying>
 
 /// Handle for the remote party (for an incoming call, the caller; for an outgoing call, the callee)
 @property (nonatomic, copy, nullable) CXHandle *remoteHandle;
 
-/// Identifier for the remote party (e.g. phone number, email address)
-/// NOTE: Will be removed in a future beta SDK version.
-@property (nonatomic, copy, nullable) NSString *callerIdentifier NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use CXCallUpdate.remoteHandle instead");
-
 /// Override the computed caller name to a provider-defined value.
 /// Normally the system will determine the appropriate caller name to display (e.g. using the user's contacts) based on the supplied caller identifier. Set this property to customize.
 @property (nonatomic, copy, nullable) NSString *localizedCallerName;
@@ -39,6 +36,9 @@
 /// The call can send DTMF tones via hard pause digits or in-call keypad entries
 @property (nonatomic) BOOL supportsDTMF;
 
+/// The call includes video in addition to audio.
+@property (nonatomic) BOOL hasVideo;
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXEndCallAction.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXEndCallAction.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXEndCallAction.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXEndCallAction.h	2016-07-11 07:03:59.000000000 +0200
@@ -9,7 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXEndCallAction : CXCallAction
 
 /// Normally, providers can just call -[CXAction fulfill] to indicate action fulfillment. Use this method to note a specific date that the call ended.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXError.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXError.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXError.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXError.h	2016-07-11 07:03:59.000000000 +0200
@@ -10,43 +10,42 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-CX_EXTERN NSString *const CXErrorDomain NS_AVAILABLE(10_12, 10_0);
-CX_EXTERN NSString *const CXErrorDomainIncomingCall NS_AVAILABLE(10_12, 10_0);
-CX_EXTERN NSString *const CXErrorDomainRequestTransaction NS_AVAILABLE(10_12, 10_0);
-CX_EXTERN NSString *const CXErrorDomainCallDirectoryManager NS_AVAILABLE(10_12, 10_0);
+CX_EXTERN NSString *const CXErrorDomain API_AVAILABLE(ios(10.0));
+CX_EXTERN NSString *const CXErrorDomainIncomingCall API_AVAILABLE(ios(10.0));
+CX_EXTERN NSString *const CXErrorDomainRequestTransaction API_AVAILABLE(ios(10.0));
+CX_EXTERN NSString *const CXErrorDomainCallDirectoryManager API_AVAILABLE(ios(10.0));
 
 typedef NS_ENUM(NSInteger, CXErrorCode) {
     CXErrorCodeUnknownError = 0,
-} NS_ENUM_AVAILABLE(10_12, 10_0);
+} API_AVAILABLE(ios(10.0));
 
 typedef NS_ENUM(NSInteger, CXErrorCodeIncomingCallError) {
     CXErrorCodeIncomingCallErrorUnknown = 0,
-    CXErrorCodeIncomingCallErrorNotAuthorized = 1,
+    CXErrorCodeIncomingCallErrorUnentitled = 1,
     CXErrorCodeIncomingCallErrorCallUUIDAlreadyExists = 2,
     CXErrorCodeIncomingCallErrorFilteredByDoNotDisturb = 3,
     CXErrorCodeIncomingCallErrorFilteredByBlockList = 4,
-} NS_ENUM_AVAILABLE(10_12, 10_0);
+} API_AVAILABLE(ios(10.0));
 
 typedef NS_ENUM(NSInteger, CXErrorCodeRequestTransactionError) {
     CXErrorCodeRequestTransactionErrorUnknown = 0,
-    CXErrorCodeRequestTransactionErrorNotAuthorized = 1,
+    CXErrorCodeRequestTransactionErrorUnentitled = 1,
     CXErrorCodeRequestTransactionErrorUnknownCallProvider = 2,
     CXErrorCodeRequestTransactionErrorEmptyTransaction = 3,
     CXErrorCodeRequestTransactionErrorUnknownCallUUID = 4,
     CXErrorCodeRequestTransactionErrorCallUUIDAlreadyExists = 5,
     CXErrorCodeRequestTransactionErrorInvalidAction = 6,
     CXErrorCodeRequestTransactionErrorMaximumCallGroupsReached = 7,
-} NS_ENUM_AVAILABLE(10_12, 10_0);
+} API_AVAILABLE(ios(10.0));
 
 typedef NS_ENUM(NSInteger, CXErrorCodeCallDirectoryManagerError) {
     CXErrorCodeCallDirectoryManagerErrorUnknown = 0,
     CXErrorCodeCallDirectoryManagerErrorNoExtensionFound = 1,
-    CXErrorCodeCallDirectoryManagerErrorNoAttachmentFound = 2,
-    CXErrorCodeCallDirectoryManagerErrorLoadingInterrupted = 3,
-    CXErrorCodeCallDirectoryManagerErrorEntriesOutOfOrder = 4,
-    CXErrorCodeCallDirectoryManagerErrorDuplicateEntries = 5,
-    CXErrorCodeCallDirectoryManagerErrorMaximumEntriesExceeded = 6,
-    CXErrorCodeCallDirectoryManagerErrorExtensionDisabled = 7,
-} NS_ENUM_AVAILABLE(10_12, 10_0);
+    CXErrorCodeCallDirectoryManagerErrorLoadingInterrupted = 2,
+    CXErrorCodeCallDirectoryManagerErrorEntriesOutOfOrder = 3,
+    CXErrorCodeCallDirectoryManagerErrorDuplicateEntries = 4,
+    CXErrorCodeCallDirectoryManagerErrorMaximumEntriesExceeded = 5,
+    CXErrorCodeCallDirectoryManagerErrorExtensionDisabled = 6,
+} API_AVAILABLE(ios(10.0));
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXHandle.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXHandle.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXHandle.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXHandle.h	2016-07-11 07:03:59.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <CallKit/CXBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -13,9 +14,9 @@
     CXHandleTypeGeneric = 1,
     CXHandleTypePhoneNumber = 2,
     CXHandleTypeEmailAddress = 3,
-} NS_ENUM_AVAILABLE(10_12, 10_0);
+} API_AVAILABLE(ios(10.0));
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXHandle : NSObject <NSCopying, NSSecureCoding>
 
 @property (nonatomic, readonly) CXHandleType type;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXPlayDTMFCallAction.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXPlayDTMFCallAction.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXPlayDTMFCallAction.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXPlayDTMFCallAction.h	2016-07-11 07:03:59.000000000 +0200
@@ -11,18 +11,16 @@
     CXPlayDTMFCallActionTypeSingleTone = 1, // The user tapped a digit on the in-call keypad
     CXPlayDTMFCallActionTypeSoftPause = 2, // The user included digits after a soft pause in their dial string
     CXPlayDTMFCallActionTypeHardPause = 3, // The user included digits after a hard pause in their dial string
-} NS_ENUM_AVAILABLE(10_12, 10_0);
+} API_AVAILABLE(ios(10.0));
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXPlayDTMFCallAction : CXCallAction
 
 - (instancetype)initWithCallUUID:(NSUUID *)callUUID digits:(NSString *)digits type:(CXPlayDTMFCallActionType)type NS_DESIGNATED_INITIALIZER;
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
-
-/// NOTE: Will be removed in a future beta SDK version.
-- (instancetype)initWithCallUUID:(NSUUID *)callUUID NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use CXPlayDTMFCallAction(call:digits:type:) instead");
+- (instancetype)initWithCallUUID:(NSUUID *)callUUID NS_UNAVAILABLE;
 
 // The string representation of the digits that should be played as DTMF tones
 @property (nonatomic, copy) NSString *digits;
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProvider.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProvider.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProvider.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProvider.h	2016-07-11 07:04:13.000000000 +0200
@@ -6,7 +6,7 @@
 //
 
 #import <Foundation/Foundation.h>
-
+#import <CallKit/CXBase.h>
 #import <CallKit/CXAuthorization.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -29,7 +29,7 @@
     CXCallEndedReasonFailed = 1, // An error occurred while trying to service the call
     CXCallEndedReasonRemoteEnded = 2, // The remote party explicitly ended the call
     CXCallEndedReasonUnanswered = 3, // The call never started connecting and was never explicitly ended (e.g. outgoing/incoming call timeout)
-} NS_ENUM_AVAILABLE(10_12, 10_0);
+} API_AVAILABLE(ios(10.0));
 
 @protocol CXProviderDelegate <NSObject>
 
@@ -65,16 +65,13 @@
 - (void)provider:(CXProvider *)provider didActivateAudioSession:(AVAudioSession *)audioSession;
 - (void)provider:(CXProvider *)provider didDeactivateAudioSession:(AVAudioSession *)audioSession;
 
-/// Called when the provider's authorization status changes
-- (void)provider:(CXProvider *)provider didChangeAuthorizationStatus:(CXAuthorizationStatus)authorizationStatus;
-
 @end
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXProvider : NSObject
 
 /// Returns the current authorization status of the calling application
-@property (readonly, class) CXAuthorizationStatus authorizationStatus;
+@property (readonly, class) CXAuthorizationStatus authorizationStatus API_DEPRECATED("Authorization is no longer required", ios(10.0, 10.0));
 
 /// Initialize a new provider instance with the supplied configuration
 - (instancetype)initWithConfiguration:(CXProviderConfiguration *)configuration NS_DESIGNATED_INITIALIZER;
@@ -87,7 +84,7 @@
 /// Request permission to contribute calls.
 ///
 /// This method must be called prior to using the provider. If the current authorization is anything other than `CXAuthorizationStatusNotDetermined`, this method does nothing. Otherwise, the result is delivered to the delegate's `provider:didChangeAuthorizationStatus:` method
-- (void)requestAuthorization;
+- (void)requestAuthorization API_DEPRECATED("Authorization is no longer required", ios(10.0, 10.0));
 
 /// Report a new incoming call to the system.
 ///
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProviderConfiguration.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProviderConfiguration.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProviderConfiguration.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProviderConfiguration.h	2016-07-11 07:03:59.000000000 +0200
@@ -6,10 +6,11 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <CallKit/CXBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXProviderConfiguration : NSObject <NSCopying>
 
 /// Localized name of the provider
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetGroupCallAction.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetGroupCallAction.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetGroupCallAction.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetGroupCallAction.h	2016-07-11 07:03:59.000000000 +0200
@@ -9,14 +9,12 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXSetGroupCallAction : CXCallAction
 
 - (instancetype)initWithCallUUID:(NSUUID *)callUUID callUUIDToGroupWith:(nullable NSUUID *)callUUIDToGroupWith NS_DESIGNATED_INITIALIZER;
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
-
-/// NOTE: Will be removed in a future beta SDK version.
-- (instancetype)initWithCallUUID:(NSUUID *)callUUID NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use CXSetGroupCallAction(call:callUUIDToGroupWith:) instead");
+- (instancetype)initWithCallUUID:(NSUUID *)callUUID NS_UNAVAILABLE;
 
 /// The UUID of another call to group with.
 ///
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetHeldCallAction.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetHeldCallAction.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetHeldCallAction.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetHeldCallAction.h	2016-07-11 07:03:59.000000000 +0200
@@ -9,14 +9,12 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXSetHeldCallAction : CXCallAction
 
 - (instancetype)initWithCallUUID:(NSUUID *)callUUID onHold:(BOOL)onHold NS_DESIGNATED_INITIALIZER;
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
-
-/// NOTE: Will be removed in a future beta SDK version.
-- (instancetype)initWithCallUUID:(NSUUID *)callUUID NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use CXSetHeldCallAction(call:onHold:) instead");
+- (instancetype)initWithCallUUID:(NSUUID *)callUUID NS_UNAVAILABLE;
 
 @property (nonatomic, getter=isOnHold) BOOL onHold;
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetMutedCallAction.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetMutedCallAction.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetMutedCallAction.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXSetMutedCallAction.h	2016-07-11 07:03:59.000000000 +0200
@@ -9,14 +9,12 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXSetMutedCallAction : CXCallAction
 
 - (instancetype)initWithCallUUID:(NSUUID *)callUUID muted:(BOOL)muted NS_DESIGNATED_INITIALIZER;
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
-
-/// NOTE: Will be removed in a future beta SDK version.
-- (instancetype)initWithCallUUID:(NSUUID *)callUUID NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use CXSetMutedCallAction(call:muted:) instead");
+- (instancetype)initWithCallUUID:(NSUUID *)callUUID NS_UNAVAILABLE;
 
 @property (nonatomic, getter=isMuted) BOOL muted;
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXStartCallAction.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXStartCallAction.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXStartCallAction.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXStartCallAction.h	2016-07-11 07:03:59.000000000 +0200
@@ -11,21 +11,15 @@
 
 @class CXHandle;
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXStartCallAction : CXCallAction
 
 - (instancetype)initWithCallUUID:(NSUUID *)callUUID handle:(CXHandle *)handle NS_DESIGNATED_INITIALIZER;
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
 
-/// NOTE: Will be removed in a future beta SDK version.
-- (instancetype)initWithCallUUID:(NSUUID *)callUUID NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use CXStartCallAction(call:handle:) instead");
-
 /// Handle for the party to call
 @property (nonatomic, copy) CXHandle *handle;
 
-/// NOTE: Will be removed in a future beta SDK version.
-@property (nonatomic, copy) NSString *destination NS_DEPRECATED(10_12, 10_12, 10_0, 10_0, "Use CXStartCallAction.handle instead");
-
 @property (nonatomic, copy, nullable) NSString *contactIdentifier;
 
 /// Normally, providers can just call -[CXAction fulfill] to indicate action fulfillment. Use this method to note a specific date that the call started if it is different from [NSDate date]. A call is considered started when its invitation has been sent to the remote callee.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXTransaction.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXTransaction.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXTransaction.h	2016-06-27 07:46:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXTransaction.h	2016-07-11 07:03:59.000000000 +0200
@@ -6,12 +6,13 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <CallKit/CXBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
 @class CXAction;
 
-NS_CLASS_AVAILABLE(10_12, 10_0)
+CX_CLASS_AVAILABLE(ios(10.0))
 @interface CXTransaction : NSObject <NSCopying, NSSecureCoding>
 
 /// Unique ID

```