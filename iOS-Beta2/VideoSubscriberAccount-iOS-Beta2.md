#VideoSubscriberAccount.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountManager.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountManager.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountManager.h	2016-05-28 06:25:59.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountManager.h	2016-06-28 06:19:03.000000000 +0200
@@ -21,13 +21,14 @@
 @protocol VSAccountManagerDelegate;
 
 /// Represents the current state of the application's access to the user's subscription information.
-typedef NS_ENUM(NSUInteger, VSAccountAccessStatus)
+typedef NS_ENUM(NSInteger, VSAccountAccessStatus)
 {
-    VSAccountAccessStatusNotDetermined, // The user has not yet made a choice about whether to allow this access to the app.
-    VSAccountAccessStatusRestricted, // Restrictions, e.g. parental controls, prohibit the user from allowing access to the app.
-    VSAccountAccessStatusDenied, // The user has explicitly decided to not allow the app to access subscription information.
-    VSAccountAccessStatusGranted, // The user has currently decided to allow the app to access subscription information.
-};
+    VSAccountAccessStatusNotDetermined = 0, // The user has not yet made a choice about whether to allow this access to the app.
+    VSAccountAccessStatusRestricted = 1, // Restrictions, e.g. parental controls, prohibit the user from allowing access to the app.
+    VSAccountAccessStatusDenied = 2, // The user has explicitly decided to not allow the app to access subscription information.
+    VSAccountAccessStatusGranted = 3, // The user has currently decided to allow the app to access subscription information.
+}
+NS_ENUM_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE;
 
 /// Options that may be provided when checking access status.
 typedef NSString * VSCheckAccessOption NS_STRING_ENUM
@@ -37,7 +38,7 @@
 VS_EXTERN VSCheckAccessOption const VSCheckAccessOptionPrompt
 NS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE;
 
-/// A VSAAccountManager instance coordinates access to a subscriber's account.
+/// A VSAccountManager instance coordinates access to a subscriber's account.
 NS_CLASS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE
 @interface VSAccountManager : NSObject
 
@@ -63,6 +64,8 @@
 @end
 
 
+/// A VSAccountManager instance coordinates access to a subscriber's account.
+VS_EXPORT NS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE
 @protocol VSAccountManagerDelegate <NSObject>
 
 @required
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountMetadata.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountMetadata.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountMetadata.h	2016-05-28 06:28:11.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountMetadata.h	2016-06-29 07:00:15.000000000 +0200
@@ -22,6 +26,10 @@
 /// The value might be nil if the user is not currently authenticated.
 @property (nonatomic, readonly, copy, nullable) NSDate *authenticationExpirationDate;
 
+/// An opaque blob of data that can be used to cryptographically verify that the
+/// SAML AttributeQuery response actually came from the account provider.
+@property (nonatomic, readonly, copy, nullable) NSData *verificationData;
+
 /// The SAML AttributeQuery response received from the account provider.
 /// The value might be nil if your account metadata request did not specify any SAML attributes or if the user does not have a valid authentication.
 @property (nonatomic, readonly, copy, nullable) NSString *SAMLAttributeQueryResponse;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountMetadataRequest.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountMetadataRequest.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountMetadataRequest.h	2016-05-28 06:28:11.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountMetadataRequest.h	2016-06-29 07:00:15.000000000 +0200
@@ -5,11 +5,15 @@
 //  Copyright © 2016 Apple Inc. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
+#import <Availability.h>
 #import <VideoSubscriberAccount/VideoSubscriberAccountDefines.h>
+#import <Foundation/NSObject.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class NSArray<ObjectType>;
+@class NSString;
+
 /// Specifies which information the app wants to obtain about the subscriber's account.
 /// You should only request the information you need to fulfill your contractual obligations.
 NS_CLASS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE
@@ -30,9 +34,17 @@
 /// Whether to request the expiration date of the subscriber's current authentication.
 @property (nonatomic, assign) BOOL includeAuthenticationExpirationDate;
 
+/// A brief, user-presentable name for the video that the app will play if it receives a successful response.
+/// For example, "What's New in Swift" or "Office Space"
+/// Do not provide a value if the request will not be used to play a specific video.
+@property (nonatomic, copy, nullable) NSString *localizedVideoTitle;
+
 /// Whether the user might expect to be prompted to authenticate in order to complete this request.
 @property (nonatomic, assign, getter=isInterruptionAllowed) BOOL interruptionAllowed;
 
+/// Controls whether the request will ignore any cached credentials.
+@property (nonatomic, assign) BOOL forceAuthentication;
+
 /// Attributes to add to a SAML attributeQuery request and sent to the account provider.
 @property (nonatomic, copy) NSArray<NSString *> *attributeNames;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VideoSubscriberAccountErrors.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VideoSubscriberAccountErrors.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VideoSubscriberAccountErrors.h	2016-05-28 06:28:11.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VideoSubscriberAccountErrors.h	2016-06-29 07:00:15.000000000 +0200
@@ -5,24 +5,40 @@
 //  Copyright © 2016 Apple Inc. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
+#import <Availability.h>
+#import <Foundation/NSObjCRuntime.h>
+#import <Foundation/NSError.h>
 #import <VideoSubscriberAccount/VideoSubscriberAccountDefines.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class NSString;
+
 /// The domain of all errors returned by VideoSubscriberAccount framework.
-VS_EXTERN NSString * const VSErrorDomain;
+VS_EXTERN NSErrorDomain const VSErrorDomain
+NS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE;
 
 /// A key that can be used to obtain the subscription provider's SAML response string from an error user info dictionary.
-VS_EXTERN NSString * const VSErrorInfoKeySAMLResponse;
+VS_EXTERN NSString * const VSErrorInfoKeySAMLResponse
+NS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE;
+
+/// A key that can be used to obtain the subscription provider's SAML status code string from an error user info dictionary.
+VS_EXTERN NSString * const VSErrorInfoKeySAMLResponseStatus
+NS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE;
+
+/// A key that can be used to obtain the identifier string of the user's unsupported subscription provider from an error user info dictionary.
+VS_EXTERN NSString * const VSErrorInfoKeyUnsupportedProviderIdentifier
+NS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE;
 
 typedef NS_ENUM(NSInteger, VSErrorCode)
 {
-    VSErrorCodeAccessNotGranted, // The user has not granted the app access to their subscription information.
-    VSErrorCodeUnsupportedProvider, // The system does not currently support the user's subscription provider.
-    VSErrorCodeUserCancelled, // The request was cancelled by the user.
-    VSErrorCodeServiceTemporarilyUnavailable, // The request failed, but a subsequent attempt might succeed.
-    VSErrorCodeProviderRejected,// The user's subscription provider did not allow the request to proceed, e.g. because the subscription tier doesn't include the resource, or interactive reauthentication is required, but the request does not allow interruption.
-};
+    VSErrorCodeAccessNotGranted = 0, // The user has not granted the app access to their subscription information.
+    VSErrorCodeUnsupportedProvider = 1, // The system does not currently support the user's subscription provider.
+    VSErrorCodeUserCancelled = 2, // The request was cancelled by the user.
+    VSErrorCodeServiceTemporarilyUnavailable = 3, // The request failed, but a subsequent attempt might succeed.
+    VSErrorCodeProviderRejected = 4,// The user's subscription provider did not allow the request to proceed, e.g. because the subscription tier doesn't include the resource, or interactive reauthentication is required, but the request does not allow interruption.
+    VSErrorCodeInvalidVerificationToken = 5,// The request's verification token was rejected by the user's subscription provider.
+}
+NS_ENUM_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE;
 
 NS_ASSUME_NONNULL_END

```