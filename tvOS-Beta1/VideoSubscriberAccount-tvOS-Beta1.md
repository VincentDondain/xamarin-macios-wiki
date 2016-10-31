#VideoSubscriberAccount.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountManager.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountManager.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountManager.h	2016-08-11 06:54:34.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountManager.h	2016-10-24 05:33:43.000000000 +0200
@@ -5,7 +5,7 @@
 //  Copyright © 2016 Apple Inc. All rights reserved.
 //
 
-#import <Availability.h>
+#import <os/availability.h>
 #import <Foundation/NSObject.h>
 #import <VideoSubscriberAccount/VideoSubscriberAccountDefines.h>
 
@@ -28,18 +28,18 @@
     VSAccountAccessStatusDenied = 2, // The user has explicitly decided to not allow the app to access subscription information.
     VSAccountAccessStatusGranted = 3, // The user has currently decided to allow the app to access subscription information.
 }
-NS_ENUM_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE;
+API_AVAILABLE(ios(10.0), tvos(10.0));
 
 /// Options that may be provided when checking access status.
 typedef NSString * VSCheckAccessOption NS_STRING_ENUM
-NS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE;
+API_AVAILABLE(ios(10.0), tvos(10.0));
 
 /// A boolean indicating whether the user may be prompted to grant access.
 VS_EXTERN VSCheckAccessOption const VSCheckAccessOptionPrompt
-NS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE;
+API_AVAILABLE(ios(10.0), tvos(10.0));
 
 /// A VSAccountManager instance coordinates access to a subscriber's account.
-NS_CLASS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE
+VS_EXPORT API_AVAILABLE(ios(10.0), tvos(10.0))
 @interface VSAccountManager : NSObject
 
 /// An object that can help the account manager by presenting and dismissing view controllers when needed.
@@ -65,7 +65,7 @@
 
 
 /// A VSAccountManager instance coordinates access to a subscriber's account.
-VS_EXPORT NS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE
+API_AVAILABLE(ios(10.0), tvos(10.0))
 @protocol VSAccountManagerDelegate <NSObject>
 
 @required
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountManagerResult.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountManagerResult.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountManagerResult.h	2016-08-11 06:54:34.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountManagerResult.h	2016-10-24 06:54:30.000000000 +0200
@@ -5,14 +5,14 @@
 //  Copyright © 2016 Apple Inc. All rights reserved.
 //
 
-#import <Availability.h>
+#import <os/availability.h>
 #import <Foundation/NSObject.h>
 #import <VideoSubscriberAccount/VideoSubscriberAccountDefines.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
 /// Represents an in-flight request to an account manger.
-NS_CLASS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE
+VS_EXPORT API_AVAILABLE(ios(10.0), tvos(10.0))
 @interface VSAccountManagerResult : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountMetadata.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountMetadata.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountMetadata.h	2016-08-11 06:54:34.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountMetadata.h	2016-10-24 06:54:30.000000000 +0200
@@ -5,7 +5,7 @@
 //  Copyright © 2016 Apple Inc. All rights reserved.
 //
 
-#import <Availability.h>
+#import <os/availability.h>
 #import <Foundation/NSObject.h>
 #import <VideoSubscriberAccount/VideoSubscriberAccountDefines.h>
 
@@ -13,9 +13,10 @@
 
 @class NSDate;
 @class NSString;
+@class VSAccountProviderResponse;
 
 /// A collection of information about a subscriber's account.
-NS_CLASS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE
+VS_EXPORT API_AVAILABLE(ios(10.0), tvos(10.0))
 @interface VSAccountMetadata : NSObject
 
 /// A value that uniquely identifies the account provider.
@@ -34,6 +35,12 @@
 /// The value might be nil if your account metadata request did not specify any SAML attributes or if the user does not have a valid authentication.
 @property (nonatomic, readonly, copy, nullable) NSString *SAMLAttributeQueryResponse;
 
+/// The response received from the account provider.
+/// The value might be nil if your account metadata request did not specify any
+/// attributes, or if the user does not have a valid authentication.
+@property (nonatomic, readonly, strong, nullable) VSAccountProviderResponse *accountProviderResponse
+API_AVAILABLE(ios(10.2), tvos(10.1));
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountMetadataRequest.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountMetadataRequest.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountMetadataRequest.h	2016-08-11 06:54:34.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountMetadataRequest.h	2016-10-24 06:54:30.000000000 +0200
@@ -5,8 +5,9 @@
 //  Copyright © 2016 Apple Inc. All rights reserved.
 //
 
-#import <Availability.h>
+#import <os/availability.h>
 #import <VideoSubscriberAccount/VideoSubscriberAccountDefines.h>
+#import <VideoSubscriberAccount/VSAccountProviderResponse.h>
 #import <Foundation/NSObject.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -16,7 +17,7 @@
 
 /// Specifies which information the app wants to obtain about the subscriber's account.
 /// You should only request the information you need to fulfill your contractual obligations.
-NS_CLASS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE
+VS_EXPORT API_AVAILABLE(ios(10.0), tvos(10.0))
 @interface VSAccountMetadataRequest : NSObject
 
 /// Identifies who is making the request.
@@ -48,6 +49,12 @@
 /// Attributes to add to a SAML attributeQuery request and sent to the account provider.
 @property (nonatomic, copy) NSArray<NSString *> *attributeNames;
 
+/// The collection of authentication schemes that the app supports for this request.
+/// This list may be used to determine compatibility of the app with providers.
+/// Defaults to SAML.
+@property (nonatomic, copy) NSArray<VSAccountProviderAuthenticationScheme> *supportedAuthenticationSchemes
+API_AVAILABLE(ios(10.2), tvos(10.1));
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountProviderResponse.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountProviderResponse.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountProviderResponse.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VSAccountProviderResponse.h	2016-10-24 06:54:30.000000000 +0200
@@ -0,0 +1,38 @@
+//
+//  VSAccountProviderResponse.h
+//  VideoSubscriberAccount
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/NSObject.h>
+#import <VideoSubscriberAccount/VideoSubscriberAccountDefines.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/// An opaque protocol name, to be coordinated with specific account providers.
+typedef NSString *VSAccountProviderAuthenticationScheme NS_EXTENSIBLE_STRING_ENUM;
+
+/// The authentication scheme for responses that use the SAML protocol.
+VS_EXTERN VSAccountProviderAuthenticationScheme const VSAccountProviderAuthenticationSchemeSAML
+NS_SWIFT_NAME(saml)
+API_AVAILABLE(ios(10.2), tvos(10.1));
+
+/// A value object that encapsulates the response given by an account provider.
+VS_EXPORT API_AVAILABLE(ios(10.2), tvos(10.1))
+@interface VSAccountProviderResponse : NSObject
+
+/// Identifies the protocol used in constructing this response.
+@property (nonatomic, readonly, copy) VSAccountProviderAuthenticationScheme authenticationScheme;
+
+/// The status code for this response.
+/// May be nil if there is no meaningful value for this type of response.
+@property (nonatomic, readonly, copy, nullable) NSString *status;
+
+/// The raw response from the provider.
+/// May be nil if the response contained security-sensitive information.
+@property (nonatomic, readonly, copy, nullable) NSString *body;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VideoSubscriberAccount.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VideoSubscriberAccount.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VideoSubscriberAccount.h	2016-08-11 06:54:34.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VideoSubscriberAccount.h	2016-10-24 06:54:30.000000000 +0200
@@ -11,3 +11,4 @@
 #import <VideoSubscriberAccount/VSAccountManagerResult.h>
 #import <VideoSubscriberAccount/VSAccountMetadata.h>
 #import <VideoSubscriberAccount/VSAccountMetadataRequest.h>
+#import <VideoSubscriberAccount/VSAccountProviderResponse.h>
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VideoSubscriberAccountDefines.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VideoSubscriberAccountDefines.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VideoSubscriberAccountDefines.h	2016-08-11 06:54:34.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VideoSubscriberAccountDefines.h	2016-10-24 06:54:30.000000000 +0200
@@ -5,7 +5,7 @@
 //  Copyright © 2016 Apple Inc. All rights reserved.
 //
 
-#import <Availability.h>
+#import <os/availability.h>
 #import <Foundation/NSObjCRuntime.h>
 
 #define VS_EXPORT __attribute__((visibility ("default")))
@@ -15,4 +15,3 @@
 #else
 #define VS_EXTERN extern VS_EXPORT
 #endif
-
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VideoSubscriberAccountErrors.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VideoSubscriberAccountErrors.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VideoSubscriberAccountErrors.h	2016-08-11 06:54:34.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/VideoSubscriberAccount.framework/Headers/VideoSubscriberAccountErrors.h	2016-10-24 06:54:30.000000000 +0200
@@ -5,7 +5,7 @@
 //  Copyright © 2016 Apple Inc. All rights reserved.
 //
 
-#import <Availability.h>
+#import <os/availability.h>
 #import <Foundation/NSObjCRuntime.h>
 #import <Foundation/NSError.h>
 #import <VideoSubscriberAccount/VideoSubscriberAccountDefines.h>
@@ -16,19 +16,23 @@
 
 /// The domain of all errors returned by VideoSubscriberAccount framework.
 VS_EXTERN NSErrorDomain const VSErrorDomain
-NS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE;
+API_AVAILABLE(ios(10.0), tvos(10.0));
 
 /// A key that can be used to obtain the subscription provider's SAML response string from an error user info dictionary.
 VS_EXTERN NSString * const VSErrorInfoKeySAMLResponse
-NS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE;
+API_AVAILABLE(ios(10.0), tvos(10.0));
 
 /// A key that can be used to obtain the subscription provider's SAML status code string from an error user info dictionary.
 VS_EXTERN NSString * const VSErrorInfoKeySAMLResponseStatus
-NS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE;
+API_AVAILABLE(ios(10.0), tvos(10.0));
+
+/// A key that can be used to obtain the account provider's response object from an error user info dictionary.
+VS_EXTERN NSString * const VSErrorInfoKeyAccountProviderResponse
+API_AVAILABLE(ios(10.2), tvos(10.1));
 
 /// A key that can be used to obtain the identifier string of the user's unsupported subscription provider from an error user info dictionary.
 VS_EXTERN NSString * const VSErrorInfoKeyUnsupportedProviderIdentifier
-NS_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE;
+API_AVAILABLE(ios(10.3), tvos(10.3));
 
 typedef NS_ENUM(NSInteger, VSErrorCode)
 {
@@ -39,6 +43,6 @@
     VSErrorCodeProviderRejected = 4,// The user's subscription provider did not allow the request to proceed, e.g. because the subscription tier doesn't include the resource, or interactive reauthentication is required, but the request does not allow interruption.
     VSErrorCodeInvalidVerificationToken = 5,// The request's verification token was rejected by the user's subscription provider.
 }
-NS_ENUM_AVAILABLE_IOS(10_0) __TVOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE;
+API_AVAILABLE(ios(10.0), tvos(10.0));
 
 NS_ASSUME_NONNULL_END

```