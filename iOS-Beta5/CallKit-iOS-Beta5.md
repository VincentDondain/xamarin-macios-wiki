#CallKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCall.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCall.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCall.h	2016-07-26 06:26:52.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXCall.h	2016-08-03 04:41:54.000000000 +0200
@@ -22,7 +22,7 @@
 
 - (instancetype)init NS_UNAVAILABLE;
 
-- (BOOL)isEqualToCall:(CXCall *)call;
+- (BOOL)isEqualToCall:(CXCall *)call NS_SWIFT_UNAVAILABLE("Use == operator instead");
 
 @end
 
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXHandle.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXHandle.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXHandle.h	2016-07-26 06:26:52.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXHandle.h	2016-08-03 04:41:54.000000000 +0200
@@ -25,7 +25,7 @@
 - (instancetype)initWithType:(CXHandleType)type value:(NSString *)value NS_DESIGNATED_INITIALIZER;
 - (instancetype)init NS_UNAVAILABLE;
 
-- (BOOL)isEqualToHandle:(CXHandle *)handle;
+- (BOOL)isEqualToHandle:(CXHandle *)handle NS_SWIFT_UNAVAILABLE("Use == operator instead");
 
 @end
 
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProvider.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProvider.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProvider.h	2016-07-26 06:26:51.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProvider.h	2016-08-03 04:13:50.000000000 +0200
@@ -28,6 +28,8 @@
     CXCallEndedReasonFailed = 1, // An error occurred while trying to service the call
     CXCallEndedReasonRemoteEnded = 2, // The remote party explicitly ended the call
     CXCallEndedReasonUnanswered = 3, // The call never started connecting and was never explicitly ended (e.g. outgoing/incoming call timeout)
+    CXCallEndedReasonAnsweredElsewhere = 4, // The call was answered on another device
+    CXCallEndedReasonDeclinedElsewhere = 5, // The call was declined on another device
 } API_AVAILABLE(ios(10.0));
 
 @protocol CXProviderDelegate <NSObject>
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProviderConfiguration.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProviderConfiguration.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProviderConfiguration.h	2016-07-26 06:26:52.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CallKit.framework/Headers/CXProviderConfiguration.h	2016-08-03 04:41:54.000000000 +0200
@@ -20,7 +20,6 @@
 @property (nonatomic, strong, nullable) NSString *ringtoneSound;
 
 @property (nonatomic, copy, nullable) NSData *iconTemplateImageData; // Image should be a square with side length of 40 points
-@property (nonatomic, strong, nullable) NSData *iconMaskImageData API_DEPRECATED_WITH_REPLACEMENT("iconTemplateImageData", ios(10.0, 10.0)); // Note: will be removed in a future beta SDK
 @property (nonatomic) NSUInteger maximumCallGroups; // Default 2
 @property (nonatomic) NSUInteger maximumCallsPerCallGroup; // Default 5
 

```