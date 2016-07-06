#CoreTelephony.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreTelephony.framework/Headers/CTCall.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreTelephony.framework/Headers/CTCall.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreTelephony.framework/Headers/CTCall.h	2015-10-03 00:23:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreTelephony.framework/Headers/CTCall.h	2016-05-27 07:14:55.000000000 +0200
@@ -11,10 +11,10 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-CORETELEPHONY_EXTERN NSString * const CTCallStateDialing  __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_0);
-CORETELEPHONY_EXTERN NSString * const CTCallStateIncoming  __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_0);
-CORETELEPHONY_EXTERN NSString * const CTCallStateConnected  __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_0);
-CORETELEPHONY_EXTERN NSString * const CTCallStateDisconnected  __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_0);
+CORETELEPHONY_EXTERN NSString * const CTCallStateDialing  __OSX_AVAILABLE_BUT_DEPRECATED_MSG(__MAC_NA, __MAC_NA, __IPHONE_4_0, __IPHONE_10_0, "Replaced by <CallKit/CXCall.h> properties");
+CORETELEPHONY_EXTERN NSString * const CTCallStateIncoming  __OSX_AVAILABLE_BUT_DEPRECATED_MSG(__MAC_NA, __MAC_NA, __IPHONE_4_0, __IPHONE_10_0, "Replaced by <CallKit/CXCall.h> properties");
+CORETELEPHONY_EXTERN NSString * const CTCallStateConnected  __OSX_AVAILABLE_BUT_DEPRECATED_MSG(__MAC_NA, __MAC_NA, __IPHONE_4_0, __IPHONE_10_0, "Replaced by <CallKit/CXCall.h> properties");
+CORETELEPHONY_EXTERN NSString * const CTCallStateDisconnected  __OSX_AVAILABLE_BUT_DEPRECATED_MSG(__MAC_NA, __MAC_NA, __IPHONE_4_0, __IPHONE_10_0, "Replaced by <CallKit/CXCall.h> properties");
 
 CORETELEPHONY_CLASS_AVAILABLE(4_0)
 @interface CTCall : NSObject
@@ -33,7 +33,7 @@
  *     to CTCallStateConnected when the call is established with all parties 
  *     involved and will move to CTCallStateDisconnected when this call is terminated.
  */
-@property(nonatomic, readonly, copy) NSString *callState  __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_0);
+@property(nonatomic, readonly, copy) NSString *callState  __OSX_AVAILABLE_BUT_DEPRECATED_MSG(__MAC_NA, __MAC_NA, __IPHONE_4_0, __IPHONE_10_0, "Replaced by <CallKit/CXCall.h> properties");
 
 /*
  * callID
@@ -42,7 +42,7 @@
  *     A unique identifier for this call to be used by clients to differentiate
  *     multiple active calls.
  */
-@property(nonatomic, readonly, copy) NSString *callID  __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_0);
+@property(nonatomic, readonly, copy) NSString *callID  __OSX_AVAILABLE_BUT_DEPRECATED_MSG(__MAC_NA, __MAC_NA, __IPHONE_4_0, __IPHONE_10_0, "Replaced by <CallKit/CXCall.h> properties");
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreTelephony.framework/Headers/CTCallCenter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreTelephony.framework/Headers/CTCallCenter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreTelephony.framework/Headers/CTCallCenter.h	2015-10-03 00:23:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreTelephony.framework/Headers/CTCallCenter.h	2016-05-27 07:14:55.000000000 +0200
@@ -15,13 +15,6 @@
 
 CORETELEPHONY_CLASS_AVAILABLE(4_0)
 @interface CTCallCenter : NSObject
-{
-@private
-    void *_server;
-
-    NSSet *_currentCalls;
-    void (^_callEventHandler)(CTCall *);
-}
 
 /*
  * currentCalls
@@ -29,9 +22,9 @@
  * Discussion:
  *   An array containing CTCall objects for all calls that are currently
  *   in progress. If no calls are active, this will be nil.
- *   
+ *
  */
-@property(readonly, retain, nullable) NSSet<CTCall*> *currentCalls __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_0);
+@property(readonly, retain, nullable) NSSet<CTCall*> *currentCalls __OSX_AVAILABLE_BUT_DEPRECATED_MSG(__MAC_NA, __MAC_NA, __IPHONE_4_0, __IPHONE_10_0, "Replaced by <CallKit/CXCallObserver.h>");
 
 /*
  * callEventHandler
@@ -41,7 +34,7 @@
  *   queue when a new call event occurs. Set this property to a block
  *   that is defined in your application to handle call events.
  */
-@property(nonatomic, copy, nullable) void (^callEventHandler)(CTCall*) __OSX_AVAILABLE_STARTING(__MAC_NA,__IPHONE_4_0);
+@property(nonatomic, copy, nullable) void (^callEventHandler)(CTCall*) __OSX_AVAILABLE_BUT_DEPRECATED_MSG(__MAC_NA, __MAC_NA, __IPHONE_4_0, __IPHONE_10_0, "Replaced by <CallKit/CXCallObserver.h>");
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreTelephony.framework/Headers/CTTelephonyNetworkInfo.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreTelephony.framework/Headers/CTTelephonyNetworkInfo.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreTelephony.framework/Headers/CTTelephonyNetworkInfo.h	2015-10-03 00:23:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreTelephony.framework/Headers/CTTelephonyNetworkInfo.h	2016-05-27 07:14:55.000000000 +0200
@@ -2,7 +2,7 @@
  *  CTTelephonyNetworkInfo.h
  *  CoreTelephony
  *
- *  Copyright 2009 Apple, Inc. All rights reserved.
+ *  Copyright 2009 Apple Inc. All rights reserved.
  *
  */
 

```