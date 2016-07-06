#PushKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PushKit.framework/Headers/PKDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PushKit.framework/Headers/PKDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PushKit.framework/Headers/PKDefines.h	2015-10-02 23:34:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PushKit.framework/Headers/PKDefines.h	2016-05-20 07:38:40.000000000 +0200
@@ -5,8 +5,12 @@
 //  Copyright (c) 2014 Apple. All rights reserved.
 //
 
+#import <Foundation/Foundation.h>
+
 #ifdef __cplusplus
 #define PK_EXPORT           extern "C" __attribute__((visibility("default")))
 #else
 #define PK_EXPORT           extern __attribute__((visibility("default")))
 #endif
+
+typedef NSString *PKPushType NS_STRING_ENUM;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PushKit.framework/Headers/PKPushCredentials.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PushKit.framework/Headers/PKPushCredentials.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PushKit.framework/Headers/PKPushCredentials.h	2015-10-02 23:34:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PushKit.framework/Headers/PKPushCredentials.h	2016-05-20 07:38:40.000000000 +0200
@@ -6,11 +6,16 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <PushKit/PKDefines.h>
+
+NS_ASSUME_NONNULL_BEGIN
 
 NS_CLASS_AVAILABLE_IOS(8_0)
 @interface PKPushCredentials : NSObject
 
-@property (readonly,copy) NSString *type;
+@property (readonly,copy) PKPushType type;
 @property (readonly,copy) NSData *token;
 
 @end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PushKit.framework/Headers/PKPushPayload.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PushKit.framework/Headers/PKPushPayload.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PushKit.framework/Headers/PKPushPayload.h	2015-10-02 23:34:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PushKit.framework/Headers/PKPushPayload.h	2016-05-20 07:38:40.000000000 +0200
@@ -6,11 +6,16 @@
 //
 
 #import <Foundation/Foundation.h>
+#import <PushKit/PKDefines.h>
+
+NS_ASSUME_NONNULL_BEGIN
 
 NS_CLASS_AVAILABLE_IOS(8_0)
 @interface PKPushPayload : NSObject
 
-@property (readonly,copy) NSString *type;
+@property (readonly,copy) PKPushType type;
 @property (readonly,copy) NSDictionary *dictionaryPayload;
 
 @end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PushKit.framework/Headers/PKPushRegistry.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PushKit.framework/Headers/PKPushRegistry.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PushKit.framework/Headers/PKPushRegistry.h	2015-10-02 23:34:17.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/PushKit.framework/Headers/PKPushRegistry.h	2016-05-20 07:38:40.000000000 +0200
@@ -8,11 +8,13 @@
 #import <Foundation/Foundation.h>
 #import <PushKit/PKDefines.h>
 
+NS_ASSUME_NONNULL_BEGIN
+
 /* PKPushType constants can be used to register for a PKPushType-specific push token or to identify received push
    notifications.
  */
-PK_EXPORT NSString * const PKPushTypeVoIP NS_AVAILABLE_IOS(8_0);
-PK_EXPORT NSString * const PKPushTypeComplication NS_AVAILABLE_IOS(9_0);
+PK_EXPORT PKPushType const PKPushTypeVoIP NS_AVAILABLE_IOS(8_0);
+PK_EXPORT PKPushType const PKPushTypeComplication NS_AVAILABLE_IOS(9_0);
 
 @protocol PKPushRegistryDelegate;
 @class PKPushCredentials, PKPushPayload;
@@ -20,7 +22,7 @@
 /*!
  @class         PKPushRegistry
  @abstract      An instance of this class can be used to register for 3rd party notifications. The supported push
-                notification types are listed above as NSString constants.
+                notification types are listed above as PKPushType constants.
  */
 NS_CLASS_AVAILABLE_IOS(8_0)
 @interface PKPushRegistry : NSObject
@@ -29,14 +31,14 @@
  @property      delegate
  @abstract      Setting a delegate is required to receive device push tokens and incoming pushes.
  */
-@property (readwrite,weak) id<PKPushRegistryDelegate> delegate;
+@property (readwrite,weak,nullable) id<PKPushRegistryDelegate> delegate;
 
 /*!
  @property      desiredPushTypes
  @abstract      An app requests registration for various types of pushes by setting this NSSet to the desired
-                PKPushType NSString constants. Push tokens and notifications will be delivered via delegate callback.
+                PKPushType constants. Push tokens and notifications will be delivered via delegate callback.
  */
-@property (readwrite,copy) NSSet *desiredPushTypes;
+@property (readwrite,copy,nullable) NSSet<PKPushType> *desiredPushTypes;
 
 /*!
  @method        pushTokenForType:
@@ -44,11 +46,11 @@
  @discussion    A push token returned here has previously been given to the delegate via handlePushTokenUpdate:forType:
                 callback.
  @param         type
-                This is a PKPushType NSString constant that is already in desiredPushTypes.
+                This is a PKPushType constant that is already in desiredPushTypes.
  @result        Returns the push token that can be used to send pushes to the device for the specified PKPushType.
                 Returns nil if no push token is available for this PKPushType at the time of invocation.
  */
-- (NSData *)pushTokenForType:(NSString *)type;
+- (nullable NSData *)pushTokenForType:(PKPushType)type;
 
 /*!
  @method        initWithQueue:
@@ -58,7 +60,13 @@
  @result        A PKPushRegistry instance that can be used to register for push tokens and notifications for supported
                 push types.
  */
-- (instancetype)initWithQueue:(dispatch_queue_t)queue;
+- (instancetype)initWithQueue:(nullable dispatch_queue_t)queue NS_DESIGNATED_INITIALIZER;
+
+/*!
+ @method        init
+ @abstract      Unavailable, use -initWithQueue: instead.
+ */
+- (instancetype)init NS_UNAVAILABLE;
 
 @end
 
@@ -76,9 +84,9 @@
  @param         credentials
                 The push credentials that can be used to send pushes to the device for the specified PKPushType.
  @param         type
-                This is a PKPushType NSString constant which is present in [registry desiredPushTypes].
+                This is a PKPushType constant which is present in [registry desiredPushTypes].
  */
-- (void)pushRegistry:(PKPushRegistry *)registry didUpdatePushCredentials:(PKPushCredentials *)credentials forType:(NSString *)type;
+- (void)pushRegistry:(PKPushRegistry *)registry didUpdatePushCredentials:(PKPushCredentials *)credentials forType:(PKPushType)type;
 
 /*!
  @method        pushRegistry:didReceiveIncomingPushWithPayload:forType:
@@ -88,9 +96,9 @@
  @param         payload
                 The push payload sent by a developer via APNS server API.
  @param         type
-                This is a PKPushType NSString constant which is present in [registry desiredPushTypes].
+                This is a PKPushType constant which is present in [registry desiredPushTypes].
  */
-- (void)pushRegistry:(PKPushRegistry *)registry didReceiveIncomingPushWithPayload:(PKPushPayload *)payload forType:(NSString *)type;
+- (void)pushRegistry:(PKPushRegistry *)registry didReceiveIncomingPushWithPayload:(PKPushPayload *)payload forType:(PKPushType)type;
 
 
 @optional
@@ -103,8 +111,10 @@
  @param         registry
                 The PKPushRegistry instance responsible for the delegate callback.
  @param         type
-                This is a PKPushType NSString constant which is present in [registry desiredPushTypes].
+                This is a PKPushType constant which is present in [registry desiredPushTypes].
  */
-- (void)pushRegistry:(PKPushRegistry *)registry didInvalidatePushTokenForType:(NSString *)type;
+- (void)pushRegistry:(PKPushRegistry *)registry didInvalidatePushTokenForType:(PKPushType)type;
 
 @end
+
+NS_ASSUME_NONNULL_END

```