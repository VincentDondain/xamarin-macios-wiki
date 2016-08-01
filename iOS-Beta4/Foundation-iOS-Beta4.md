#Foundation.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/Foundation.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/Foundation.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/Foundation.h	2016-07-13 05:25:23.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/Foundation.h	2016-07-25 07:03:55.000000000 +0200
@@ -180,3 +180,5 @@
 #import <Foundation/NSXPCConnection.h>
 
 #endif
+
+#import <Foundation/FoundationLegacySwiftCompatibility.h>
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/FoundationErrors.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/FoundationErrors.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/FoundationErrors.h	2016-07-10 07:46:56.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/FoundationErrors.h	2016-07-25 07:06:53.000000000 +0200
@@ -100,5 +100,16 @@
     NSBundleOnDemandResourceOutOfSpaceError NS_ENUM_AVAILABLE(NA, 9_0) = 4992, // There was not enough space available to download the requested On Demand Resources.
     NSBundleOnDemandResourceExceededMaximumSizeError NS_ENUM_AVAILABLE(NA, 9_0) = 4993, // The application exceeded the amount of On Demand Resources content in use at one time
     NSBundleOnDemandResourceInvalidTagError NS_ENUM_AVAILABLE(NA, 9_0) = 4994, // The application specified a tag which the system could not find in the application tag manifest
+    
+    NSCloudSharingNetworkFailureError API_AVAILABLE(macosx(10.12), ios(10.0)) API_UNAVAILABLE(watchos, tvos) = 5120,        // Sharing failed due to a network failure.
+    NSCloudSharingQuotaExceededError API_AVAILABLE(macosx(10.12), ios(10.0)) API_UNAVAILABLE(watchos, tvos) = 5121,         // The user doesn't have enough storage space available to share the requested items.
+    NSCloudSharingTooManyParticipantsError API_AVAILABLE(macosx(10.12), ios(10.0)) API_UNAVAILABLE(watchos, tvos) = 5122,   // Additional participants could not be added to the share, because the limit was reached.
+    NSCloudSharingConflictError API_AVAILABLE(macosx(10.12), ios(10.0)) API_UNAVAILABLE(watchos, tvos) = 5123,              // A conflict occurred while trying to save changes to the CKShare and/or root CKRecord. Respond to this error by first fetching the server's changes to the records, then either handle the conflict manually or present it, which will instruct the user to try the operation again.
+    NSCloudSharingNoPermissionError API_AVAILABLE(macosx(10.12), ios(10.0)) API_UNAVAILABLE(watchos, tvos) = 5124,         // The current user doesn't have permission to perform the requested actions.
+    NSCloudSharingOtherError API_AVAILABLE(macosx(10.12), ios(10.0)) API_UNAVAILABLE(watchos, tvos) = 5375,                 // These errors may require application-specific responses. For CloudKit sharing, use the NSUnderlyingErrorKey, which is a CKErrorDomain error, to discover the specific error and refer to the CloudKit documentation for the proper response to these errors.
+    
+    NSCloudSharingErrorMinimum API_AVAILABLE(macosx(10.12), ios(10.0)) API_UNAVAILABLE(watchos, tvos) = 5120,
+    NSCloudSharingErrorMaximum API_AVAILABLE(macosx(10.12), ios(10.0)) API_UNAVAILABLE(watchos, tvos) = 5375,
+
 };
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/FoundationLegacySwiftCompatibility.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/FoundationLegacySwiftCompatibility.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/FoundationLegacySwiftCompatibility.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/FoundationLegacySwiftCompatibility.h	2016-07-25 07:11:34.000000000 +0200
@@ -0,0 +1,397 @@
+#import <Foundation/NSObjCRuntime.h>
+
+#pragma mark Swift epochs before 8
+
+#if FOUNDATION_SWIFT_SDK_EPOCH_LESS_THAN(8)
+
+#import <Foundation/NSBundle.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSBundle (NSLegacySwiftCompatibility)
++ (NSBundle *)mainBundle;
++ (NSArray<NSBundle *> *)allBundles;
++ (NSArray<NSBundle *> *)allFrameworks;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSCalendar.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSCalendar (NSLegacySwiftCompatibility)
++ (NSCalendar *)currentCalendar;
++ (NSCalendar *)autoupdatingCurrentCalendar NS_AVAILABLE(10_5, 2_0);
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSCharacterSet.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSCharacterSet (NSLegacySwiftCompatibility)
++ (NSCharacterSet *)controlCharacterSet;
++ (NSCharacterSet *)whitespaceCharacterSet;
++ (NSCharacterSet *)whitespaceAndNewlineCharacterSet;
++ (NSCharacterSet *)decimalDigitCharacterSet;
++ (NSCharacterSet *)letterCharacterSet;
++ (NSCharacterSet *)lowercaseLetterCharacterSet;
++ (NSCharacterSet *)uppercaseLetterCharacterSet;
++ (NSCharacterSet *)nonBaseCharacterSet;
++ (NSCharacterSet *)alphanumericCharacterSet;
++ (NSCharacterSet *)decomposableCharacterSet;
++ (NSCharacterSet *)illegalCharacterSet;
++ (NSCharacterSet *)punctuationCharacterSet;
++ (NSCharacterSet *)capitalizedLetterCharacterSet;
++ (NSCharacterSet *)symbolCharacterSet;
++ (NSCharacterSet *)newlineCharacterSet NS_AVAILABLE(10_5, 2_0);
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSDate.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSDate (NSLegacySwiftCompatibility)
++ (NSTimeInterval)timeIntervalSinceReferenceDate;
++ (NSDate *)distantFuture;
++ (NSDate *)distantPast;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSDateFormatter.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSDateFormatter (NSLegacySwiftCompatibility)
++ (NSDateFormatterBehavior)defaultFormatterBehavior;
++ (void)setDefaultFormatterBehavior:(NSDateFormatterBehavior)behavior;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSDecimalNumber.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSDecimalNumber (NSLegacySwiftCompatibility)
++ (NSDecimalNumber *)zero;
++ (NSDecimalNumber *)one;
++ (NSDecimalNumber *)minimumDecimalNumber;
++ (NSDecimalNumber *)maximumDecimalNumber;
++ (NSDecimalNumber *)notANumber;
++ (id <NSDecimalNumberBehaviors>)defaultBehavior;
++ (void)setDefaultBehavior:(id <NSDecimalNumberBehaviors>)behavior;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSException.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSAssertionHandler (NSLegacySwiftCompatibility)
++ (NSAssertionHandler *)currentHandler;
+@end
+NS_ASSUME_NONNULL_END
+
+#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE)) || (TARGET_OS_EMBEDDED || TARGET_OS_IPHONE)
+#import <Foundation/NSFileCoordinator.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSFileCoordinator (NSLegacySwiftCompatibility)
++ (NSArray<id<NSFilePresenter>> *)filePresenters;
+@end
+NS_ASSUME_NONNULL_END
+#endif
+
+#import <Foundation/NSFileHandle.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSFileHandle (NSLegacySwiftCompatibility)
++ (NSFileHandle *)fileHandleWithStandardInput;
++ (NSFileHandle *)fileHandleWithStandardOutput;
++ (NSFileHandle *)fileHandleWithStandardError;
++ (NSFileHandle *)fileHandleWithNullDevice;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSFileManager.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSFileManager (NSLegacySwiftCompatibility)
++ (NSFileManager *)defaultManager;
+
+@property (nullable, readonly, copy) NSDictionary<NSString *, id> *fileAttributes;
+@property (nullable, readonly, copy) NSDictionary<NSString *, id> *directoryAttributes;
+
+- (BOOL)setAttributes:(NSDictionary<NSString *, id> *)attributes ofItemAtPath:(NSString *)path error:(NSError **)error NS_AVAILABLE(10_5, 2_0);
+- (nullable NSDictionary<NSString *, id> *)attributesOfItemAtPath:(NSString *)path error:(NSError **)error NS_AVAILABLE(10_5, 2_0);
+- (nullable NSDictionary<NSString *, id> *)attributesOfFileSystemForPath:(NSString *)path error:(NSError **)error NS_AVAILABLE(10_5, 2_0);
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSHTTPCookieStorage.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSHTTPCookieStorage (NSLegacySwiftCompatibility)
++ (NSHTTPCookieStorage *)sharedHTTPCookieStorage;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSKeyValueCoding.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSObject(NSKeyValueCodingLegacySwiftCompatibility)
++ (BOOL)accessInstanceVariablesDirectly;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSLocale.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSLocale (NSLegacySwiftCompatibility)
++ (NSLocale *)autoupdatingCurrentLocale NS_AVAILABLE(10_5, 2_0);
++ (NSLocale *)currentLocale;
++ (NSLocale *)systemLocale;
++ (NSArray<NSString *> *)availableLocaleIdentifiers;
++ (NSArray<NSString *> *)ISOLanguageCodes;
++ (NSArray<NSString *> *)ISOCountryCodes;
++ (NSArray<NSString *> *)ISOCurrencyCodes;
++ (NSArray<NSString *> *)commonISOCurrencyCodes NS_AVAILABLE(10_5, 2_0);
++ (NSArray<NSString *> *)preferredLanguages NS_AVAILABLE(10_5, 2_0);
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSNotification.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSNotificationCenter (NSLegacySwiftCompatibility)
++ (NSNotificationCenter *)defaultCenter;
+- (void)addObserver:(id)observer selector:(SEL)aSelector name:(nullable NSString *)aName object:(nullable id)anObject;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSNotificationQueue.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSNotificationQueue (NSLegacySwiftCompatibility)
++ (NSNotificationQueue *)defaultQueue;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSOperation.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSOperationQueue (NSLegacySwiftCompatibility)
++ (nullable NSOperationQueue *)currentQueue NS_AVAILABLE(10_6, 4_0);
++ (NSOperationQueue *)mainQueue;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSProcessInfo.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSProcessInfo (NSLegacySwiftCompatibility)
++ (NSProcessInfo *)processInfo;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSRunLoop.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSRunLoop (NSLegacySwiftCompatibility)
++ (NSRunLoop *)currentRunLoop;
++ (NSRunLoop *)mainRunLoop NS_AVAILABLE(10_5, 2_0);
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSStream.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSStream (NSLegacySwiftCompatibility)
+- (nullable id)propertyForKey:(NSString *)key;
+- (BOOL)setProperty:(nullable id)property forKey:(NSString *)key;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSString.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSString (NSLegacySwiftCompatibility)
++ (const NSStringEncoding *)availableStringEncodings;
++ (NSStringEncoding)defaultCStringEncoding;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSTextCheckingResult.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSTextCheckingResult (NSLegacySwiftCompatibility)
+@property (nullable, readonly, copy) NSArray<NSString *> *grammarDetails;
++ (NSTextCheckingResult *)grammarCheckingResultWithRange:(NSRange)range details:(NSArray<NSString *> *)details;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSThread.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSThread (NSLegacySwiftCompatibility)
++ (NSThread *)currentThread;
++ (NSArray<NSNumber *> *)callStackReturnAddresses;
++ (NSArray<NSString *> *)callStackSymbols;
++ (BOOL)isMainThread NS_AVAILABLE(10_5, 2_0);
++ (NSThread *)mainThread NS_AVAILABLE(10_5, 2_0);
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSTimeZone.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSTimeZone (NSLegacySwiftCompatibility)
++ (NSTimeZone *)systemTimeZone;
++ (NSTimeZone *)defaultTimeZone;
++ (void)setDefaultTimeZone:(NSTimeZone *)timeZone;
++ (NSTimeZone *)localTimeZone;
++ (NSArray<NSString *> *)knownTimeZoneNames;
++ (void)setAbbreviationDictionary:(NSDictionary<NSString *, NSString *> *)dictionary NS_AVAILABLE(10_6, 4_0);
++ (NSDictionary<NSString *, NSString *> *)abbreviationDictionary;
++ (NSString *)timeZoneDataVersion NS_AVAILABLE(10_6, 4_0);
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSURL.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSCharacterSet (NSLegacySwiftCompatibility)
++ (NSCharacterSet *)URLUserAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
++ (NSCharacterSet *)URLPasswordAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
++ (NSCharacterSet *)URLHostAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
++ (NSCharacterSet *)URLPathAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
++ (NSCharacterSet *)URLQueryAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
++ (NSCharacterSet *)URLFragmentAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSURLCache.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSURLCache (NSLegacySwiftCompatibility)
++ (NSURLCache *)sharedURLCache;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSURLCredentialStorage.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSURLCredentialStorage (NSLegacySwiftCompatibility)
++ (NSURLCredentialStorage *)sharedCredentialStorage;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSURLRequest.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSURLRequest (NSLegacySwiftCompatibility)
++ (BOOL)supportsSecureCoding;
+@end
+NS_ASSUME_NONNULL_END
+
+#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE)) || (TARGET_OS_EMBEDDED || TARGET_OS_IPHONE)
+#import <Foundation/NSURLSession.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSURLSession (NSLegacySwiftCompatibility)
++ (NSURLSession *)sharedSession;
+@end
+NS_ASSUME_NONNULL_END
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSURLSessionConfiguration (NSLegacySwiftCompatibility)
++ (NSURLSessionConfiguration *)defaultSessionConfiguration;
++ (NSURLSessionConfiguration *)ephemeralSessionConfiguration;
+@end
+NS_ASSUME_NONNULL_END
+#endif
+
+#import <Foundation/NSUserDefaults.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSUserDefaults (NSLegacySwiftCompatibility)
++ (NSUserDefaults *)standardUserDefaults;
+@end
+NS_ASSUME_NONNULL_END
+
+#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
+#import <Foundation/NSUserNotification.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSUserNotificationCenter (NSLegacySwiftCompatibility)
++ (NSUserNotificationCenter *)defaultUserNotificationCenter;
+@end
+NS_ASSUME_NONNULL_END
+#endif
+
+#endif // FOUNDATION_SWIFT_SDK_EPOCH_LESS_THAN(8)
+
+#pragma mark Swift epochs before 7
+
+#if FOUNDATION_SWIFT_SDK_EPOCH_LESS_THAN(7)
+
+#import <Foundation/NSError.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSError (NSLegacySwiftCompatibility)
++ (void)setUserInfoValueProviderForDomain:(NSErrorDomain)errorDomain provider:(id _Nullable (^ _Nullable)(NSError *err, NSErrorUserInfoKey userInfoKey))provider NS_AVAILABLE(10_11, 9_0);
++ (id _Nullable (^ _Nullable)(NSError *err, NSErrorUserInfoKey userInfoKey))userInfoValueProviderForDomain:(NSErrorDomain)errorDomain NS_AVAILABLE(10_11, 9_0);
+@end
+NS_ASSUME_NONNULL_END
+
+#endif // FOUNDATION_SWIFT_SDK_EPOCH_LESS_THAN(7)
+
+#pragma mark Swift epochs before 6
+
+#if FOUNDATION_SWIFT_SDK_EPOCH_LESS_THAN(6)
+
+#if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE)) || (TARGET_OS_EMBEDDED || TARGET_OS_IPHONE)
+#import <Foundation/NSExpression.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSExpression (NSLegacySwiftCompatibility)
+@property (readonly, retain) id constantValue;
+
+- (id)expressionValueWithObject:(nullable id)object context:(nullable NSMutableDictionary *)context;
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSPredicate.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSPredicate (NSLegacySwiftCompatibility)
++ (NSPredicate*)predicateWithBlock:(BOOL (^)(id evaluatedObject, NSDictionary<NSString *, id> * _Nullable bindings))block NS_AVAILABLE(10_6, 4_0);
+@end
+NS_ASSUME_NONNULL_END
+#endif
+
+#import <Foundation/NSURL.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSURL (NSLegacySwiftCompatibility)
+@property (readonly, copy) NSString *absoluteString;
+@property (nullable, readonly, copy) NSString *relativeString; // The relative portion of a URL.  If baseURL is nil, or if the receiver is itself absolute, this is the same as absoluteString
+@property (nullable, readonly, copy) NSURL *baseURL; // may be nil.
+@property (readonly, copy) NSURL *absoluteURL; // if the receiver is itself absolute, this will return self.
+
+/* Any URL is composed of these two basic pieces.  The full URL would be the concatenation of [myURL scheme], ':', [myURL resourceSpecifier]
+ */
+@property (readonly, copy) NSString *scheme;
+@property (readonly, copy) NSString *resourceSpecifier;
+
+- (NSURL *)URLByAppendingPathComponent:(NSString *)pathComponent NS_AVAILABLE(10_6, 4_0);
+- (NSURL *)URLByAppendingPathComponent:(NSString *)pathComponent isDirectory:(BOOL)isDirectory NS_AVAILABLE(10_7, 5_0);
+@property (nullable, readonly, copy) NSURL *URLByDeletingLastPathComponent NS_AVAILABLE(10_6, 4_0);
+- (NSURL *)URLByAppendingPathExtension:(NSString *)pathExtension NS_AVAILABLE(10_6, 4_0);
+@property (nullable, readonly, copy) NSURL *URLByDeletingPathExtension NS_AVAILABLE(10_6, 4_0);
+@end
+NS_ASSUME_NONNULL_END
+
+#import <Foundation/NSPathUtilities.h>
+
+NS_ASSUME_NONNULL_BEGIN
+@interface NSString (NSStringPathExtensionsLegacySwiftCompatibility)
+- (NSUInteger)completePathIntoString:(NSString * _Nonnull * _Nullable)outputName caseSensitive:(BOOL)flag matchesIntoArray:(NSArray<NSString *> * _Nonnull * _Nullable)outputArray filterTypes:(nullable NSArray<NSString *> *)filterTypes;
+@end
+NS_ASSUME_NONNULL_END
+
+#endif
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSBundle.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSBundle.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSBundle.h	2016-07-13 05:50:31.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSBundle.h	2016-07-25 07:12:53.000000000 +0200
@@ -29,7 +29,7 @@
 }
 
 /* Methods for creating or retrieving bundle instances. */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, strong) NSBundle *mainBundle;
 #endif
 
@@ -42,7 +42,7 @@
 + (NSBundle *)bundleForClass:(Class)aClass;
 + (nullable NSBundle *)bundleWithIdentifier:(NSString *)identifier;
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, copy) NSArray<NSBundle *> *allBundles;
 @property (class, readonly, copy) NSArray<NSBundle *> *allFrameworks;
 #endif
@@ -252,12 +252,4 @@
  */
 FOUNDATION_EXPORT double const NSBundleResourceRequestLoadingPriorityUrgent NS_AVAILABLE(NA, 9_0);
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSBundle (NSLegacySwiftCompatability)
-+ (NSBundle *)mainBundle;
-+ (NSArray<NSBundle *> *)allBundles;
-+ (NSArray<NSBundle *> *)allFrameworks;
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCalendar.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCalendar.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCalendar.h	2016-07-13 05:25:24.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCalendar.h	2016-07-25 07:03:32.000000000 +0200
@@ -98,7 +98,7 @@
 @interface NSCalendar : NSObject <NSCopying, NSSecureCoding>
 
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, copy) NSCalendar *currentCalendar;					// user's preferred calendar
 @property (class, readonly, strong) NSCalendar *autoupdatingCurrentCalendar NS_AVAILABLE(10_5, 2_0); // tracks changes to user's preferred calendar identifier
 #endif
@@ -469,14 +469,5 @@
 
 
 @end
-    
-    
-    
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSCalendar (NSLegacySwiftCompatability)
-+ (NSCalendar *)currentCalendar;
-+ (NSCalendar *)autoupdatingCurrentCalendar NS_AVAILABLE(10_5, 2_0);
-@end
-#endif
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCharacterSet.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCharacterSet.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCharacterSet.h	2016-07-10 07:46:56.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCharacterSet.h	2016-07-25 07:03:55.000000000 +0200
@@ -17,22 +17,22 @@
 
 @interface NSCharacterSet : NSObject <NSCopying, NSMutableCopying, NSSecureCoding>
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
-@property (nonatomic, readonly, class, copy) NSCharacterSet *controlCharacterSet;
-@property (nonatomic, readonly, class, copy) NSCharacterSet *whitespaceCharacterSet;
-@property (nonatomic, readonly, class, copy) NSCharacterSet *whitespaceAndNewlineCharacterSet;
-@property (nonatomic, readonly, class, copy) NSCharacterSet *decimalDigitCharacterSet;
-@property (nonatomic, readonly, class, copy) NSCharacterSet *letterCharacterSet;
-@property (nonatomic, readonly, class, copy) NSCharacterSet *lowercaseLetterCharacterSet;
-@property (nonatomic, readonly, class, copy) NSCharacterSet *uppercaseLetterCharacterSet;
-@property (nonatomic, readonly, class, copy) NSCharacterSet *nonBaseCharacterSet;
-@property (nonatomic, readonly, class, copy) NSCharacterSet *alphanumericCharacterSet;
-@property (nonatomic, readonly, class, copy) NSCharacterSet *decomposableCharacterSet;
-@property (nonatomic, readonly, class, copy) NSCharacterSet *illegalCharacterSet;
-@property (nonatomic, readonly, class, copy) NSCharacterSet *punctuationCharacterSet;
-@property (nonatomic, readonly, class, copy) NSCharacterSet *capitalizedLetterCharacterSet;
-@property (nonatomic, readonly, class, copy) NSCharacterSet *symbolCharacterSet;
-@property (nonatomic, readonly, class, copy) NSCharacterSet *newlineCharacterSet NS_AVAILABLE(10_5, 2_0);
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
+@property (readonly, class, copy) NSCharacterSet *controlCharacterSet;
+@property (readonly, class, copy) NSCharacterSet *whitespaceCharacterSet;
+@property (readonly, class, copy) NSCharacterSet *whitespaceAndNewlineCharacterSet;
+@property (readonly, class, copy) NSCharacterSet *decimalDigitCharacterSet;
+@property (readonly, class, copy) NSCharacterSet *letterCharacterSet;
+@property (readonly, class, copy) NSCharacterSet *lowercaseLetterCharacterSet;
+@property (readonly, class, copy) NSCharacterSet *uppercaseLetterCharacterSet;
+@property (readonly, class, copy) NSCharacterSet *nonBaseCharacterSet;
+@property (readonly, class, copy) NSCharacterSet *alphanumericCharacterSet;
+@property (readonly, class, copy) NSCharacterSet *decomposableCharacterSet;
+@property (readonly, class, copy) NSCharacterSet *illegalCharacterSet;
+@property (readonly, class, copy) NSCharacterSet *punctuationCharacterSet;
+@property (readonly, class, copy) NSCharacterSet *capitalizedLetterCharacterSet;
+@property (readonly, class, copy) NSCharacterSet *symbolCharacterSet;
+@property (readonly, class, copy) NSCharacterSet *newlineCharacterSet NS_AVAILABLE(10_5, 2_0);
 #endif
 
 + (NSCharacterSet *)characterSetWithRange:(NSRange)aRange;
@@ -86,24 +86,4 @@
 
 @end
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSCharacterSet (NSLegacySwiftCompatability)
-+ (NSCharacterSet *)controlCharacterSet;
-+ (NSCharacterSet *)whitespaceCharacterSet;
-+ (NSCharacterSet *)whitespaceAndNewlineCharacterSet;
-+ (NSCharacterSet *)decimalDigitCharacterSet;
-+ (NSCharacterSet *)letterCharacterSet;
-+ (NSCharacterSet *)lowercaseLetterCharacterSet;
-+ (NSCharacterSet *)uppercaseLetterCharacterSet;
-+ (NSCharacterSet *)nonBaseCharacterSet;
-+ (NSCharacterSet *)alphanumericCharacterSet;
-+ (NSCharacterSet *)decomposableCharacterSet;
-+ (NSCharacterSet *)illegalCharacterSet;
-+ (NSCharacterSet *)punctuationCharacterSet;
-+ (NSCharacterSet *)capitalizedLetterCharacterSet;
-+ (NSCharacterSet *)symbolCharacterSet;
-+ (NSCharacterSet *)newlineCharacterSet NS_AVAILABLE(10_5, 2_0);
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDate.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDate.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDate.h	2016-07-13 05:25:23.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDate.h	2016-07-25 07:03:55.000000000 +0200
@@ -42,7 +42,7 @@
 @property (readonly, copy) NSString *description;
 - (NSString *)descriptionWithLocale:(nullable id)locale;
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly) NSTimeInterval timeIntervalSinceReferenceDate;
 #endif
 
@@ -56,7 +56,7 @@
 + (instancetype)dateWithTimeIntervalSince1970:(NSTimeInterval)secs;
 + (instancetype)dateWithTimeInterval:(NSTimeInterval)secsToBeAdded sinceDate:(NSDate *)date;
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, copy) NSDate *distantFuture;
 @property (class, readonly, copy) NSDate *distantPast;
 #endif
@@ -67,12 +67,4 @@
 
 @end
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSDate (NSLegacySwiftCompatability)
-+ (NSTimeInterval)timeIntervalSinceReferenceDate;
-+ (NSDate *)distantFuture;
-+ (NSDate *)distantPast;
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateFormatter.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateFormatter.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateFormatter.h	2016-07-13 05:50:30.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateFormatter.h	2016-07-25 07:03:55.000000000 +0200
@@ -60,7 +60,7 @@
 	// no options defined, pass 0 for now
 
 // Attributes of an NSDateFormatter
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class) NSDateFormatterBehavior defaultFormatterBehavior;
 #endif
 
@@ -120,12 +120,4 @@
 @end
 #endif
 
-
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSDateFormatter (NSLegacySwiftCompatability)
-+ (NSDateFormatterBehavior)defaultFormatterBehavior;
-+ (void)setDefaultFormatterBehavior:(NSDateFormatterBehavior)behavior;
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDecimalNumber.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDecimalNumber.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDecimalNumber.h	2016-07-13 05:25:23.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDecimalNumber.h	2016-07-25 07:06:53.000000000 +0200
@@ -61,7 +61,7 @@
 + (NSDecimalNumber *)decimalNumberWithString:(nullable NSString *)numberValue;
 + (NSDecimalNumber *)decimalNumberWithString:(nullable NSString *)numberValue locale:(nullable id)locale;
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, copy) NSDecimalNumber *zero;
 @property (class, readonly, copy) NSDecimalNumber *one;
 @property (class, readonly, copy) NSDecimalNumber *minimumDecimalNumber;
@@ -94,7 +94,7 @@
 - (NSComparisonResult)compare:(NSNumber *)decimalNumber;
     // compare two NSDecimalNumbers
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, strong) id <NSDecimalNumberBehaviors> defaultBehavior;
 #endif
     // One behavior per thread - The default behavior is
@@ -153,17 +153,4 @@
 
 @end
 
-                            
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSDecimalNumber (NSLegacySwiftCompatability)
-+ (NSDecimalNumber *)zero;
-+ (NSDecimalNumber *)one;
-+ (NSDecimalNumber *)minimumDecimalNumber;
-+ (NSDecimalNumber *)maximumDecimalNumber;
-+ (NSDecimalNumber *)notANumber;
-+ (id <NSDecimalNumberBehaviors>)defaultBehavior;
-+ (void)setDefaultBehavior:(id <NSDecimalNumberBehaviors>)behavior;
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSError.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSError.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSError.h	2016-07-13 05:25:24.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSError.h	2016-07-25 07:03:55.000000000 +0200
@@ -6,7 +6,7 @@
 
 @class NSDictionary, NSArray<ObjectType>, NSString;
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 7)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(7)
 typedef NSString *NSErrorDomain;
 #else
 typedef NSString *NSErrorDomain NS_EXTENSIBLE_STRING_ENUM;
@@ -22,7 +22,7 @@
 FOUNDATION_EXPORT NSErrorDomain const NSOSStatusErrorDomain;
 FOUNDATION_EXPORT NSErrorDomain const NSMachErrorDomain;
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 7)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(7)
 // Key in userInfo. A recommended standard way to embed NSErrors from underlying calls. The value of this key should be an NSError.
 FOUNDATION_EXPORT NSString *const NSUnderlyingErrorKey;
 #else
@@ -31,7 +31,7 @@
 #endif
 
 // Keys in userInfo, for subsystems wishing to provide their error messages up-front. Note that NSError will also consult the userInfoValueProvider for the domain when these values are not present in the userInfo dictionary.
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 7)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(7)
 FOUNDATION_EXPORT NSString *const NSLocalizedDescriptionKey;             // NSString
 FOUNDATION_EXPORT NSString *const NSLocalizedFailureReasonErrorKey;      // NSString
 FOUNDATION_EXPORT NSString *const NSLocalizedRecoverySuggestionErrorKey; // NSString
@@ -115,12 +115,9 @@
  
 If an appropriate result for the requested key cannot be provided, return nil rather than choosing to manufacture a generic fallback response such as "Operation could not be completed, error 42." NSError will take care of the fallback cases.
 */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 7)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(7)
 + (void)setUserInfoValueProviderForDomain:(NSErrorDomain)errorDomain provider:(id _Nullable (^ _Nullable)(NSError *err, NSString *userInfoKey))provider NS_AVAILABLE(10_11, 9_0);
 + (id _Nullable (^ _Nullable)(NSError *err, NSString *userInfoKey))userInfoValueProviderForDomain:(NSErrorDomain)errorDomain NS_AVAILABLE(10_11, 9_0);
-#else
-+ (void)setUserInfoValueProviderForDomain:(NSErrorDomain)errorDomain provider:(id _Nullable (^ _Nullable)(NSError *err, NSErrorUserInfoKey userInfoKey))provider NS_AVAILABLE(10_11, 9_0);
-+ (id _Nullable (^ _Nullable)(NSError *err, NSErrorUserInfoKey userInfoKey))userInfoValueProviderForDomain:(NSErrorDomain)errorDomain NS_AVAILABLE(10_11, 9_0);
 #endif
 
 @end
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSException.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSException.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSException.h	2016-07-10 08:52:39.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSException.h	2016-07-25 07:14:39.000000000 +0200
@@ -293,7 +293,7 @@
     void *_reserved;
 }
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, strong) NSAssertionHandler *currentHandler;
 #endif
 
@@ -303,10 +303,4 @@
 
 @end
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSAssertionHandler (NSLegacySwiftCompatability)
-+ (NSAssertionHandler *)currentHandler;
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSExpression.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSExpression.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSExpression.h	2016-07-13 05:25:23.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSExpression.h	2016-07-25 07:11:34.000000000 +0200
@@ -108,10 +108,8 @@
 
 // accessors for individual parameters - raise if not applicable
 @property (readonly) NSExpressionType expressionType;
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 6)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(6)
 @property (nullable, readonly, retain) id constantValue;
-#else
-@property (readonly, retain) id constantValue;
 #endif
 @property (readonly, copy) NSString *keyPath;
 @property (readonly, copy) NSString *function;
@@ -131,10 +129,8 @@
 @property (readonly, copy) id (^expressionBlock)(id _Nullable, NSArray *, NSMutableDictionary * _Nullable) NS_AVAILABLE(10_6, 4_0);
 
 // evaluate the expression using the object and bindings- note that context is mutable here and can be used by expressions to store temporary state for one predicate evaluation
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 6)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(6)
 - (nullable id)expressionValueWithObject:(nullable id)object context:(nullable NSMutableDictionary *)context;
-#else
-- (id)expressionValueWithObject:(nullable id)object context:(nullable NSMutableDictionary *)context;
 #endif
 
 - (void)allowEvaluation NS_AVAILABLE(10_9, 7_0); // Force an expression which was securely decoded to allow evaluation
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileCoordinator.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileCoordinator.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileCoordinator.h	2016-07-13 05:50:32.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileCoordinator.h	2016-07-25 07:12:54.000000000 +0200
@@ -103,7 +103,7 @@
 */
 + (void)addFilePresenter:(id<NSFilePresenter>)filePresenter;
 + (void)removeFilePresenter:(id<NSFilePresenter>)filePresenter;
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, copy) NSArray<id<NSFilePresenter>> *filePresenters;
 #endif
 
@@ -229,10 +229,5 @@
 
 @end
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSFileCoordinator (NSLegacySwiftCompatability)
-+ (NSArray<id<NSFilePresenter>> *)filePresenters;
-@end
-#endif
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileHandle.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileHandle.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileHandle.h	2016-07-13 05:50:30.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileHandle.h	2016-07-25 07:03:55.000000000 +0200
@@ -37,7 +37,7 @@
 
 @interface NSFileHandle (NSFileHandleCreation)
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, strong) NSFileHandle *fileHandleWithStandardInput;
 @property (class, readonly, strong) NSFileHandle *fileHandleWithStandardOutput;
 @property (class, readonly, strong) NSFileHandle *fileHandleWithStandardError;
@@ -103,13 +103,4 @@
 
 @end
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSFileHandle (NSLegacySwiftCompatability)
-+ (NSFileHandle *)fileHandleWithStandardInput;
-+ (NSFileHandle *)fileHandleWithStandardOutput;
-+ (NSFileHandle *)fileHandleWithStandardError;
-+ (NSFileHandle *)fileHandleWithNullDevice;
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileManager.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileManager.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileManager.h	2016-07-13 05:25:23.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileManager.h	2016-07-25 07:06:53.000000000 +0200
@@ -76,7 +76,7 @@
 } NS_ENUM_AVAILABLE(10_11, NA);
 
 /* If unmountVolumeAtURL:options:completionHandler: fails, the process identifier of the dissenter can be found in the  NSError's userInfo dictionary with this key */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 7)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(7)
 FOUNDATION_EXPORT NSString *const NSFileManagerUnmountDissentingProcessIdentifierErrorKey NS_AVAILABLE(10_11, NA); // value is NSNumber containing the process identifier of the dissenter
 #else
 FOUNDATION_EXPORT NSErrorUserInfoKey const NSFileManagerUnmountDissentingProcessIdentifierErrorKey NS_AVAILABLE(10_11, NA);
@@ -90,13 +90,13 @@
 
 /* Returns the default singleton instance.
 */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, strong) NSFileManager *defaultManager;
 #endif
 
 /* -mountedVolumeURLsIncludingResourceValuesForKeys:options: returns an NSArray of NSURLs locating the mounted volumes available on the computer. The property keys that can be requested are available in <Foundation/NSURL.h>.
  */
-- (nullable NSArray<NSURL *> *)mountedVolumeURLsIncludingResourceValuesForKeys:(nullable NSArray<NSString *> *)propertyKeys options:(NSVolumeEnumerationOptions)options NS_AVAILABLE(10_6, 4_0);
+- (nullable NSArray<NSURL *> *)mountedVolumeURLsIncludingResourceValuesForKeys:(nullable NSArray<NSURLResourceKey> *)propertyKeys options:(NSVolumeEnumerationOptions)options NS_AVAILABLE(10_6, 4_0);
 
 /* This method starts the process of unmounting the volume specified by url. If the volume is encrypted, it is re-locked after being unmounted. The completionHandler will be executed when the operation is complete. If the operation was successful, the block’s errorOrNil argument will be nil; otherwise, errorOrNil will be an error object indicating why the unmount operation failed.
  */
@@ -108,7 +108,7 @@
  
     If you wish to only receive the URLs and no other attributes, then pass '0' for 'options' and an empty NSArray ('[NSArray array]') for 'keys'. If you wish to have the property caches of the vended URLs pre-populated with a default set of attributes, then pass '0' for 'options' and 'nil' for 'keys'.
  */
-- (nullable NSArray<NSURL *> *)contentsOfDirectoryAtURL:(NSURL *)url includingPropertiesForKeys:(nullable NSArray<NSString *> *)keys options:(NSDirectoryEnumerationOptions)mask error:(NSError **)error NS_AVAILABLE(10_6, 4_0);
+- (nullable NSArray<NSURL *> *)contentsOfDirectoryAtURL:(NSURL *)url includingPropertiesForKeys:(nullable NSArray<NSURLResourceKey> *)keys options:(NSDirectoryEnumerationOptions)mask error:(NSError **)error NS_AVAILABLE(10_6, 4_0);
 
 
 /* -URLsForDirectory:inDomains: is analogous to NSSearchPathForDirectoriesInDomains(), but returns an array of NSURL instances for use with URL-taking APIs. This API is suitable when you need to search for a file or files which may live in one of a variety of locations in the domains specified.
@@ -145,10 +145,8 @@
  
     This method replaces changeFileAttributes:atPath:.
  */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 - (BOOL)setAttributes:(NSDictionary<NSFileAttributeKey, id> *)attributes ofItemAtPath:(NSString *)path error:(NSError **)error NS_AVAILABLE(10_5, 2_0);
-#else
-- (BOOL)setAttributes:(NSDictionary<NSString *, id> *)attributes ofItemAtPath:(NSString *)path error:(NSError **)error NS_AVAILABLE(10_5, 2_0);
 #endif
 
 /* createDirectoryAtPath:withIntermediateDirectories:attributes:error: creates a directory at the specified path. If you pass 'NO' for createIntermediates, the directory must not exist at the time this call is made. Passing 'YES' for 'createIntermediates' will create any necessary intermediate directories. This method returns YES if all directories specified in 'path' were created and attributes were set. Directories are created with attributes specified by the dictionary passed to 'attributes'. If no dictionary is supplied, directories are created according to the umask of the process. This method returns NO if a failure occurs at any stage of the operation. If an error parameter was provided, a presentable NSError will be returned by reference.
@@ -173,20 +171,16 @@
  
     This method replaces fileAttributesAtPath:traverseLink:.
  */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 - (nullable NSDictionary<NSFileAttributeKey, id> *)attributesOfItemAtPath:(NSString *)path error:(NSError **)error NS_AVAILABLE(10_5, 2_0);
-#else
-- (nullable NSDictionary<NSString *, id> *)attributesOfItemAtPath:(NSString *)path error:(NSError **)error NS_AVAILABLE(10_5, 2_0);
 #endif
 
 /* attributesOfFileSystemForPath:error: returns an NSDictionary of key/value pairs containing the attributes of the filesystem containing the provided path. If this method returns 'nil', an NSError will be returned by reference in the 'error' parameter. This method does not traverse a terminal symlink.
  
     This method replaces fileSystemAttributesAtPath:.
  */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 - (nullable NSDictionary<NSFileAttributeKey, id> *)attributesOfFileSystemForPath:(NSString *)path error:(NSError **)error NS_AVAILABLE(10_5, 2_0);
-#else
-- (nullable NSDictionary<NSString *, id> *)attributesOfFileSystemForPath:(NSString *)path error:(NSError **)error NS_AVAILABLE(10_5, 2_0);
 #endif
 
 /* createSymbolicLinkAtPath:withDestination:error: returns YES if the symbolic link that point at 'destPath' was able to be created at the location specified by 'path'. If this method returns NO, the link was unable to be created and an NSError will be returned by reference in the 'error' parameter. This method does not traverse a terminal symlink.
@@ -272,7 +266,7 @@
 
     If you wish to only receive the URLs and no other attributes, then pass '0' for 'options' and an empty NSArray ('[NSArray array]') for 'keys'. If you wish to have the property caches of the vended URLs pre-populated with a default set of attributes, then pass '0' for 'options' and 'nil' for 'keys'.
  */
-- (nullable NSDirectoryEnumerator<NSURL *> *)enumeratorAtURL:(NSURL *)url includingPropertiesForKeys:(nullable NSArray<NSString *> *)keys options:(NSDirectoryEnumerationOptions)mask errorHandler:(nullable BOOL (^)(NSURL *url, NSError *error))handler NS_AVAILABLE(10_6, 4_0);
+- (nullable NSDirectoryEnumerator<NSURL *> *)enumeratorAtURL:(NSURL *)url includingPropertiesForKeys:(nullable NSArray<NSURLResourceKey> *)keys options:(NSDirectoryEnumerationOptions)mask errorHandler:(nullable BOOL (^)(NSURL *url, NSError *error))handler NS_AVAILABLE(10_6, 4_0);
 
 /* subpathsAtPath: returns an NSArray of all contents and subpaths recursively from the provided path. This may be very expensive to compute for deep filesystem hierarchies, and should probably be avoided.
  */
@@ -421,12 +415,9 @@
 
 /* For NSDirectoryEnumerators created with -enumeratorAtPath:, the -fileAttributes and -directoryAttributes methods return an NSDictionary containing the keys listed below. For NSDirectoryEnumerators created with -enumeratorAtURL:includingPropertiesForKeys:options:errorHandler:, these two methods return nil.
  */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (nullable, readonly, copy) NSDictionary<NSFileAttributeKey, id> *fileAttributes;
 @property (nullable, readonly, copy) NSDictionary<NSFileAttributeKey, id> *directoryAttributes;
-#else
-@property (nullable, readonly, copy) NSDictionary<NSString *, id> *fileAttributes;
-@property (nullable, readonly, copy) NSDictionary<NSString *, id> *directoryAttributes;
 #endif
 
 - (void)skipDescendents;
@@ -498,10 +489,4 @@
 - (nullable NSNumber *)fileGroupOwnerAccountID;
 @end
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSFileManager (NSLegacySwiftCompatability)
-+ (NSFileManager *)defaultManager;
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHTTPCookieStorage.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHTTPCookieStorage.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHTTPCookieStorage.h	2016-07-10 08:52:39.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHTTPCookieStorage.h	2016-07-25 07:03:56.000000000 +0200
@@ -56,7 +56,7 @@
     @discussion Starting in OS X 10.11, each app has its own sharedHTTPCookieStorage singleton, 
     which will not be shared with other applications.
 */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property(class, readonly, strong) NSHTTPCookieStorage *sharedHTTPCookieStorage;
 #endif
 
@@ -153,13 +153,6 @@
 - (void)getCookiesForTask:(NSURLSessionTask *)task completionHandler:(void (^) (NSArray<NSHTTPCookie *> * _Nullable cookies))completionHandler NS_AVAILABLE(10_10, 8_0);
 @end
 
-
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSHTTPCookieStorage (NSLegacySwiftCompatability)
-+ (NSHTTPCookieStorage *)sharedHTTPCookieStorage;
-@end
-#endif
-
 /*!
     @const NSHTTPCookieManagerAcceptPolicyChangedNotification
     @discussion Name of notification that should be posted to the
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSISO8601DateFormatter.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSISO8601DateFormatter.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSISO8601DateFormatter.h	2016-07-13 05:25:23.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSISO8601DateFormatter.h	2016-07-25 07:12:53.000000000 +0200
@@ -60,7 +60,7 @@
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
 
 - (NSString *)stringFromDate:(NSDate *)date;
-- (NSDate *)dateFromString:(NSString *)string;
+- (nullable NSDate *)dateFromString:(NSString *)string;
 
 + (NSString *)stringFromDate:(NSDate *)date timeZone:(NSTimeZone *)timeZone formatOptions:(NSISO8601DateFormatOptions)formatOptions;
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyValueCoding.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyValueCoding.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyValueCoding.h	2016-07-10 08:52:39.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyValueCoding.h	2016-07-25 07:03:55.000000000 +0200
@@ -41,10 +41,8 @@
 
 /* Return YES if -valueForKey:, -setValue:forKey:, -mutableArrayValueForKey:, -storedValueForKey:, -takeStoredValue:forKey:, and -takeValue:forKey: may directly manipulate instance variables when sent to instances of the receiving class, NO otherwise. The default implementation of this property returns YES.
 */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly) BOOL accessInstanceVariablesDirectly;
-#else
-+ (BOOL)accessInstanceVariablesDirectly;
 #endif
 
 /* Given a key that identifies an attribute or to-one relationship, return the attribute value or the related object. Given a key that identifies a to-many relationship, return an immutable array or an immutable set that contains all of the related objects.
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLocale.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLocale.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLocale.h	2016-07-10 07:46:56.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLocale.h	2016-07-25 07:12:53.000000000 +0200
@@ -34,59 +34,52 @@
 - (NSString *)localizedStringForLocaleIdentifier:(NSString *)localeIdentifier API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
 @property (readonly, copy) NSString *languageCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
-- (NSString *)localizedStringForLanguageCode:(NSString *)languageCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (nullable NSString *)localizedStringForLanguageCode:(NSString *)languageCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
-@property (readonly, copy) NSString *countryCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
-- (NSString *)localizedStringForCountryCode:(NSString *)countryCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+@property (nullable, readonly, copy) NSString *countryCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (nullable NSString *)localizedStringForCountryCode:(NSString *)countryCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
-@property (readonly, copy) NSString *scriptCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
-- (NSString *)localizedStringForScriptCode:(NSString *)scriptCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+@property (nullable, readonly, copy) NSString *scriptCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (nullable NSString *)localizedStringForScriptCode:(NSString *)scriptCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
-@property (readonly, copy) NSString *variantCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
-- (NSString *)localizedStringForVariantCode:(NSString *)variantCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+@property (nullable, readonly, copy) NSString *variantCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (nullable NSString *)localizedStringForVariantCode:(NSString *)variantCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
 @property (readonly, copy) NSCharacterSet *exemplarCharacterSet API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
-@property (readonly) NSCalendar *calendar API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
-- (NSString *)localizedStringForCalendar:(NSCalendar *)calendar API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+@property (readonly, copy) NSString *calendarIdentifier API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (nullable NSString *)localizedStringForCalendarIdentifier:(NSString *)calendarIdentifier API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
-@property (readonly, copy) NSString *collationIdentifier API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
-- (NSString *)localizedStringForCollationIdentifier:(NSString *)collationIdentifier API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+@property (nullable, readonly, copy) NSString *collationIdentifier API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (nullable NSString *)localizedStringForCollationIdentifier:(NSString *)collationIdentifier API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
 @property (readonly) BOOL usesMetricSystem API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
 @property (readonly, copy) NSString *decimalSeparator API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
-- (NSString *)localizedStringForDecimalSeparator:(NSString *)decimalSeparator API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
 @property (readonly, copy) NSString *groupingSeparator API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
-- (NSString *)localizedStringForGroupingSeparator:(NSString *)groupingSeparator API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
 @property (readonly, copy) NSString *currencySymbol API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
-- (NSString *)localizedStringForCurrencySymbol:(NSString *)currencySymbol API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
-@property (readonly, copy) NSString *currencyCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
-- (NSString *)localizedStringForCurrencyCode:(NSString *)currencyCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+@property (nullable, readonly, copy) NSString *currencyCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (nullable NSString *)localizedStringForCurrencyCode:(NSString *)currencyCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
 @property (readonly, copy) NSString *collatorIdentifier API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
-- (NSString *)localizedStringForCollatorIdentifier:(NSString *)collatorIdentifier API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (nullable NSString *)localizedStringForCollatorIdentifier:(NSString *)collatorIdentifier API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
 @property (readonly, copy) NSString *quotationBeginDelimiter API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
-- (NSString *)localizedStringForQuotationBeginDelimiter:(NSString *)quotationBeginDelimiter API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
 @property (readonly, copy) NSString *quotationEndDelimiter API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
-- (NSString *)localizedStringForQuotationEndDelimiter:(NSString *)quotationEndDelimiter API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
 @property (readonly, copy) NSString *alternateQuotationBeginDelimiter API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
-- (NSString *)localizedStringForAlternateQuotationBeginDelimiter:(NSString *)alternateQuotationBeginDelimiter API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
 @property (readonly, copy) NSString *alternateQuotationEndDelimiter API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
-- (NSString *)localizedStringForAlternateQuotationEndDelimiter:(NSString *)alternateQuotationEndDelimiter API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
 @end
 
 @interface NSLocale (NSLocaleCreation)
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, strong) NSLocale *autoupdatingCurrentLocale NS_AVAILABLE(10_5, 2_0); // generally you should use this property
 
 @property (class, readonly, copy) NSLocale *currentLocale;	// an object representing the user's current locale
@@ -101,7 +94,7 @@
 
 @interface NSLocale (NSLocaleGeneralInfo)
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, copy) NSArray<NSString *> *availableLocaleIdentifiers;
 @property (class, readonly, copy) NSArray<NSString *> *ISOLanguageCodes;
 @property (class, readonly, copy) NSArray<NSString *> *ISOCountryCodes;
@@ -177,18 +170,4 @@
 FOUNDATION_EXPORT NSString * const NSIndianCalendar NS_CALENDAR_DEPRECATED(10_6, 10_10, 4_0, 8_0, "Use NSCalendarIdentifierIndian instead");
 FOUNDATION_EXPORT NSString * const NSISO8601Calendar NS_CALENDAR_DEPRECATED(10_6, 10_10, 4_0, 8_0, "Use NSCalendarIdentifierISO8601 instead");
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSLocale (NSLegacySwiftCompatability)
-+ (NSLocale *)autoupdatingCurrentLocale NS_AVAILABLE(10_5, 2_0);
-+ (NSLocale *)currentLocale;
-+ (NSLocale *)systemLocale;
-+ (NSArray<NSString *> *)availableLocaleIdentifiers;
-+ (NSArray<NSString *> *)ISOLanguageCodes;
-+ (NSArray<NSString *> *)ISOCountryCodes;
-+ (NSArray<NSString *> *)ISOCurrencyCodes;
-+ (NSArray<NSString *> *)commonISOCurrencyCodes NS_AVAILABLE(10_5, 2_0);
-+ (NSArray<NSString *> *)preferredLanguages NS_AVAILABLE(10_5, 2_0);
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMeasurementFormatter.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMeasurementFormatter.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMeasurementFormatter.h	2016-07-13 05:25:24.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMeasurementFormatter.h	2016-07-25 07:03:56.000000000 +0200
@@ -13,8 +13,8 @@
 NS_ASSUME_NONNULL_BEGIN
 
 typedef NS_OPTIONS(NSUInteger, NSMeasurementFormatterUnitOptions) {
-    NSMeasurementFormatterUnitOptionsProvidedUnit = (1UL << 0),              // e.g  This ensures the formatter uses this unit even if it is not the preferred unit of the set locale.  All other unit options are ignored if this option is set.
-    NSMeasurementFormatterUnitOptionsNaturalScale = (1UL << 1),              // e.g. This would make the formatter show "12 kilometers" instead of "12000 meters"
+    NSMeasurementFormatterUnitOptionsProvidedUnit = (1UL << 0),              // e.g  This ensures the formatter uses this unit even if it is not the preferred unit of the set locale.
+    NSMeasurementFormatterUnitOptionsNaturalScale = (1UL << 1),              // e.g. This would make the formatter show "12 kilometers" instead of "12000 meters".  Note that setting NSMeasurementFormatterUnitOptionsNaturalScale results in scaling within the unit system of the preferred unit of the locale.  To scale within the unit system of the provided unit, set NSMeasurementFormatterUnitOptionsNaturalScale | NSMeasurementFormatterUnitOptionsProvidedUnit.
     NSMeasurementFormatterUnitOptionsTemperatureWithoutUnit = (1UL << 2),    // e.g. This would display "90°" rather than "90°F" or "90°C"
 } API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotification.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotification.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotification.h	2016-07-13 05:25:24.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotification.h	2016-07-25 07:03:55.000000000 +0200
@@ -41,7 +41,7 @@
     void *_pad[11];
 }
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, strong) NSNotificationCenter *defaultCenter;
 
 - (void)addObserver:(id)observer selector:(SEL)aSelector name:(nullable NSNotificationName)aName object:(nullable id)anObject;
@@ -60,11 +60,4 @@
 
 @end
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSNotificationCenter (NSLegacySwiftCompatability)
-+ (NSNotificationCenter *)defaultCenter;
-- (void)addObserver:(id)observer selector:(SEL)aSelector name:(nullable NSString *)aName object:(nullable id)anObject;
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotificationQueue.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotificationQueue.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotificationQueue.h	2016-07-13 05:25:24.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotificationQueue.h	2016-07-25 07:03:55.000000000 +0200
@@ -29,7 +29,7 @@
     id		_idleQueue;
     id		_idleObs;
 }
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, strong) NSNotificationQueue *defaultQueue;
 #endif
 
@@ -42,10 +42,4 @@
 
 @end
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSNotificationQueue (NSLegacySwiftCompatability)
-+ (NSNotificationQueue *)defaultQueue;
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObjCRuntime.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObjCRuntime.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObjCRuntime.h	2016-07-13 05:50:30.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObjCRuntime.h	2016-07-25 07:12:53.000000000 +0200
@@ -260,7 +260,7 @@
 #define NS_DEPRECATED_MAC(_macIntro, _macDep, ...) CF_DEPRECATED_MAC(_macIntro, _macDep, __VA_ARGS__)
 #define NS_DEPRECATED_IOS(_iosIntro, _iosDep, ...) CF_DEPRECATED_IOS(_iosIntro, _iosDep, __VA_ARGS__)
 
-#define NS_DEPRECATED_WITH_REPLACEMENT_MAC(_rep, _mac) API_DEPRECATED_WITH_REPLACEMENT(_rep, macosx(_mac))
+#define NS_DEPRECATED_WITH_REPLACEMENT_MAC(_rep, _macIntroduced, _macDeprecated) API_DEPRECATED_WITH_REPLACEMENT(_rep, macosx(_macIntroduced, _macDeprecated)) API_UNAVAILABLE(ios, watchos, tvos)
 
 #define NS_ENUM_AVAILABLE(_mac, _ios) CF_ENUM_AVAILABLE(_mac, _ios)
 #define NS_ENUM_AVAILABLE_MAC(_mac) CF_ENUM_AVAILABLE_MAC(_mac)
@@ -355,6 +355,9 @@
 #define NS_SWIFT_NOTHROW
 #endif
 
+#define FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(__epoch__) (!defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && (SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= __epoch__)))
+#define FOUNDATION_SWIFT_SDK_EPOCH_LESS_THAN(__epoch__) (! FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(__epoch__) )
+
 NS_ASSUME_NONNULL_BEGIN
 
 FOUNDATION_EXPORT double NSFoundationVersionNumber;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObject.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObject.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObject.h	2016-07-13 05:25:24.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObject.h	2016-07-25 07:03:56.000000000 +0200
@@ -40,7 +40,7 @@
 @required
 // This property must return YES on all classes that allow secure coding. Subclasses of classes that adopt NSSecureCoding and override initWithCoder: must also override this method and return YES.
 // The Secure Coding Guide should be consulted when writing methods that decode data.
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly) BOOL supportsSecureCoding;
 #else
 + (BOOL)supportsSecureCoding;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOperation.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOperation.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOperation.h	2016-07-13 05:25:24.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOperation.h	2016-07-25 07:06:53.000000000 +0200
@@ -136,19 +136,12 @@
 
 - (void)waitUntilAllOperationsAreFinished;
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, strong, nullable) NSOperationQueue *currentQueue NS_AVAILABLE(10_6, 4_0);
 @property (class, readonly, strong) NSOperationQueue *mainQueue NS_AVAILABLE(10_6, 4_0);
 #endif
 
 @end
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSOperationQueue (NSLegacySwiftCompatability)
-+ (nullable NSOperationQueue *)currentQueue NS_AVAILABLE(10_6, 4_0);
-+ (NSOperationQueue *)mainQueue;
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPathUtilities.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPathUtilities.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPathUtilities.h	2016-07-10 07:51:25.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPathUtilities.h	2016-07-25 07:14:39.000000000 +0200
@@ -31,10 +31,8 @@
 
 - (NSArray<NSString *> *)stringsByAppendingPaths:(NSArray<NSString *> *)paths;
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 6)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(6)
 - (NSUInteger)completePathIntoString:(NSString * _Nullable * _Nullable)outputName caseSensitive:(BOOL)flag matchesIntoArray:(NSArray<NSString *> * _Nullable * _Nullable)outputArray filterTypes:(nullable NSArray<NSString *> *)filterTypes;
-#else
-- (NSUInteger)completePathIntoString:(NSString * _Nonnull * _Nullable)outputName caseSensitive:(BOOL)flag matchesIntoArray:(NSArray<NSString *> * _Nonnull * _Nullable)outputArray filterTypes:(nullable NSArray<NSString *> *)filterTypes;
 #endif
 
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPredicate.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPredicate.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPredicate.h	2016-07-13 05:25:24.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPredicate.h	2016-07-25 07:03:56.000000000 +0200
@@ -33,10 +33,8 @@
 
 + (NSPredicate *)predicateWithValue:(BOOL)value;    // return predicates that always evaluate to true/false
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 6)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(6)
 + (NSPredicate*)predicateWithBlock:(BOOL (^)(id _Nullable evaluatedObject, NSDictionary<NSString *, id> * _Nullable bindings))block NS_AVAILABLE(10_6, 4_0);
-#else
-+ (NSPredicate*)predicateWithBlock:(BOOL (^)(id evaluatedObject, NSDictionary<NSString *, id> * _Nullable bindings))block NS_AVAILABLE(10_6, 4_0);
 #endif
 @property (readonly, copy) NSString *predicateFormat;    // returns the format string of the predicate
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProcessInfo.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProcessInfo.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProcessInfo.h	2016-07-13 05:50:31.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProcessInfo.h	2016-07-25 07:06:53.000000000 +0200
@@ -35,7 +35,7 @@
     NSInteger		automaticTerminationOptOutCounter;
 }
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, strong) NSProcessInfo *processInfo;
 #endif
 
@@ -233,10 +233,4 @@
  */
 FOUNDATION_EXTERN NSNotificationName const NSProcessInfoPowerStateDidChangeNotification NS_AVAILABLE(NA, 9_0);
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSProcessInfo (NSLegacySwiftCompatability)
-+ (NSProcessInfo *)processInfo;
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProgress.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProgress.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProgress.h	2016-07-10 07:46:56.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProgress.h	2016-07-25 07:03:56.000000000 +0200
@@ -10,7 +10,7 @@
 @class NSDictionary, NSMutableDictionary, NSMutableSet, NSURL, NSUUID, NSXPCConnection, NSLock;
 
 typedef NSString * NSProgressKind NS_EXTENSIBLE_STRING_ENUM;
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 typedef NSString * NSProgressUserInfoKey NS_EXTENSIBLE_STRING_ENUM;
 #else
 typedef NSString * NSProgressKey NS_EXTENSIBLE_STRING_ENUM;
@@ -151,7 +151,7 @@
 
 /* Set a value in the dictionary returned by invocations of -userInfo, with appropriate KVO notification for properties whose values can depend on values in the user info dictionary, like localizedDescription. If a nil value is passed then the dictionary entry is removed.
 */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 - (void)setUserInfoObject:(nullable id)objectOrNil forKey:(NSProgressUserInfoKey)key;
 #else
 - (void)setUserInfoObject:(nullable id)objectOrNil forKey:(NSString *)key;
@@ -181,7 +181,7 @@
 
 /* Arbitrary values associated with the receiver. Returns a KVO-compliant dictionary that changes as -setUserInfoObject:forKey: is sent to the receiver. The dictionary will send all of its KVO notifications on the thread which updates the property. The result will never be nil, but may be an empty dictionary. Some entries have meanings that are recognized by the NSProgress class itself. See the NSProgress...Key string constants listed below.
 */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (readonly, copy) NSDictionary<NSProgressUserInfoKey, id> *userInfo;
 #else
 @property (readonly, copy) NSDictionary *userInfo;
@@ -236,7 +236,7 @@
 
 /* How much time is probably left in the operation, as an NSNumber containing a number of seconds.
 */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressEstimatedTimeRemainingKey NS_AVAILABLE(10_9, 7_0);
 #else
 FOUNDATION_EXPORT NSProgressKey const NSProgressEstimatedTimeRemainingKey NS_AVAILABLE(10_9, 7_0);
@@ -244,7 +244,7 @@
 
 /* How fast data is being processed, as an NSNumber containing bytes per second.
 */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressThroughputKey NS_AVAILABLE(10_9, 7_0);
 #else
 FOUNDATION_EXPORT NSProgressKey const NSProgressThroughputKey NS_AVAILABLE(10_9, 7_0);
@@ -258,7 +258,7 @@
 
 /* A user info dictionary key, for an entry that is required when the value for the kind property is NSProgressKindFile. The value must be one of the strings listed in the next section. The default implementations of of -localizedDescription and -localizedItemDescription use this value to determine the text that they return.
 */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressFileOperationKindKey NS_AVAILABLE(10_9, 7_0);
 #else
 FOUNDATION_EXPORT NSProgressKey const NSProgressFileOperationKindKey NS_AVAILABLE(10_9, 7_0);
@@ -273,7 +273,7 @@
 
 /* A user info dictionary key. The value must be an NSURL identifying the item on which progress is being made. This is required for any NSProgress that is published using -publish to be reported to subscribers registered with +addSubscriberForFileURL:withPublishingHandler:.
 */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressFileURLKey NS_AVAILABLE(10_9, 7_0);
 #else
 FOUNDATION_EXPORT NSProgressKey const NSProgressFileURLKey NS_AVAILABLE(10_9, 7_0);
@@ -281,7 +281,7 @@
 
 /* User info dictionary keys. The values must be NSNumbers containing integers. These entries are optional but if they are both present then the default implementation of -localizedAdditionalDescription uses them to determine the text that it returns.
 */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressFileTotalCountKey NS_AVAILABLE(10_9, 7_0);
 FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressFileCompletedCountKey NS_AVAILABLE(10_9, 7_0);
 #else
@@ -291,7 +291,7 @@
 
 /* User info dictionary keys. The value for the first entry must be an NSImage, typically an icon. The value for the second entry must be an NSValue containing an NSRect, in screen coordinates, locating the image where it initially appears on the screen.
 */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressFileAnimationImageKey NS_AVAILABLE(10_9, NA);
 FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressFileAnimationImageOriginalRectKey NS_AVAILABLE(10_9, NA);
 #else
@@ -300,7 +300,7 @@
 #endif
 /* A user info dictionary key. The value must be an NSImage containing an icon. This entry is optional but, if it is present, the Finder will use it to show the icon of a file while progress is being made on that file. For example, the App Store uses this to specify an icon for an application being downloaded before the icon can be gotten from the application bundle itself.
 */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressFileIconKey NS_AVAILABLE(10_9, NA);
 #else
 FOUNDATION_EXPORT NSProgressKey const NSProgressFileIconKey NS_AVAILABLE(10_9, NA);
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSRunLoop.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSRunLoop.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSRunLoop.h	2016-07-13 05:25:24.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSRunLoop.h	2016-07-25 07:03:56.000000000 +0200
@@ -23,7 +23,7 @@
     void	*_reserved[6];
 }
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, strong) NSRunLoop *currentRunLoop;
 @property (class, readonly, strong) NSRunLoop *mainRunLoop NS_AVAILABLE(10_5, 2_0);
 #endif
@@ -82,12 +82,4 @@
 
 @end
 
-
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSRunLoop (NSLegacySwiftCompatability)
-+ (NSRunLoop *)currentRunLoop;
-+ (NSRunLoop *)mainRunLoop NS_AVAILABLE(10_5, 2_0);
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSStream.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSStream.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSStream.h	2016-07-10 07:51:25.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSStream.h	2016-07-25 07:14:39.000000000 +0200
@@ -41,7 +41,7 @@
 @property (nullable, assign) id <NSStreamDelegate> delegate;
     // By default, a stream is its own delegate, and subclassers of NSInputStream and NSOutputStream must maintain this contract. [someStream setDelegate:nil] must restore this behavior. As usual, delegates are not retained.
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 - (nullable id)propertyForKey:(NSStreamPropertyKey)key;
 - (BOOL)setProperty:(nullable id)property forKey:(NSStreamPropertyKey)key;
 #else
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSString.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSString.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSString.h	2016-07-13 05:50:31.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSString.h	2016-07-25 07:06:53.000000000 +0200
@@ -258,14 +258,14 @@
 - (NSUInteger)maximumLengthOfBytesUsingEncoding:(NSStringEncoding)enc;	// Result in O(1) time; the estimate may be way over what's needed. Returns 0 on error (overflow)
 - (NSUInteger)lengthOfBytesUsingEncoding:(NSStringEncoding)enc;		// Result in O(n) time; the result is exact. Returns 0 on error (cannot convert to specified encoding, or overflow)
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly) const NSStringEncoding *availableStringEncodings;
 #endif
 + (NSString *)localizedNameOfStringEncoding:(NSStringEncoding)encoding;
 
 /* User-dependent encoding whose value is derived from user's default language and potentially other factors. The use of this encoding might sometimes be needed when interpreting user documents with unknown encodings, in the absence of other hints.  This encoding should be used rarely, if at all. Note that some potential values here might result in unexpected encoding conversions of even fairly straightforward NSString content --- for instance, punctuation characters with a bidirectional encoding.
  */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly) NSStringEncoding defaultCStringEncoding;	// Should be rarely used
 #endif
 
@@ -526,11 +526,4 @@
 extern void *_NSConstantStringClassReference;
 #endif
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSString (NSLegacySwiftCompatability)
-+ (const NSStringEncoding *)availableStringEncodings;
-+ (NSStringEncoding)defaultCStringEncoding;
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTextCheckingResult.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTextCheckingResult.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTextCheckingResult.h	2016-07-13 05:50:32.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTextCheckingResult.h	2016-07-25 07:12:54.000000000 +0200
@@ -48,7 +48,7 @@
 
 /* Optional properties, used with certain types of results. */
 @property (nullable, readonly, copy) NSOrthography *orthography;
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (nullable, readonly, copy) NSArray<NSDictionary<NSString *, id> *> *grammarDetails;
 #endif
 @property (nullable, readonly, copy) NSDate *date;
@@ -91,7 +91,7 @@
 /* Methods for creating instances of the various types of results. */
 + (NSTextCheckingResult *)orthographyCheckingResultWithRange:(NSRange)range orthography:(NSOrthography *)orthography;
 + (NSTextCheckingResult *)spellCheckingResultWithRange:(NSRange)range;
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 + (NSTextCheckingResult *)grammarCheckingResultWithRange:(NSRange)range details:(NSArray<NSDictionary<NSString *, id> *> *)details;
 #endif
 + (NSTextCheckingResult *)dateCheckingResultWithRange:(NSRange)range date:(NSDate *)date;
@@ -109,12 +109,5 @@
 
 @end
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSTextCheckingResult (NSLegacySwiftCompatability)
-@property (nullable, readonly, copy) NSArray<NSString *> *grammarDetails;
-+ (NSTextCheckingResult *)grammarCheckingResultWithRange:(NSRange)range details:(NSArray<NSString *> *)details;
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSThread.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSThread.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSThread.h	2016-07-13 05:50:31.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSThread.h	2016-07-25 07:03:56.000000000 +0200
@@ -16,7 +16,7 @@
     uint8_t _bytes[44];
 }
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, strong) NSThread *currentThread;
 #endif
 
@@ -39,7 +39,7 @@
 
 @property NSQualityOfService qualityOfService NS_AVAILABLE(10_10, 8_0); // read-only after the thread is started
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, copy) NSArray<NSNumber *> *callStackReturnAddresses NS_AVAILABLE(10_5, 2_0);
 @property (class, readonly, copy) NSArray<NSString *> *callStackSymbols NS_AVAILABLE(10_6, 4_0);
 #endif
@@ -49,7 +49,7 @@
 @property NSUInteger stackSize NS_AVAILABLE(10_5, 2_0);
 
 @property (readonly) BOOL isMainThread NS_AVAILABLE(10_5, 2_0);
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly) BOOL isMainThread NS_AVAILABLE(10_5, 2_0); // reports whether current thread is main
 @property (class, readonly, strong) NSThread *mainThread NS_AVAILABLE(10_5, 2_0);
 #endif
@@ -87,15 +87,4 @@
 
 @end
 
-
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSThread (NSLegacySwiftCompatability)
-+ (NSThread *)currentThread;
-+ (NSArray<NSNumber *> *)callStackReturnAddresses;
-+ (NSArray<NSString *> *)callStackSymbols;
-+ (BOOL)isMainThread NS_AVAILABLE(10_5, 2_0);
-+ (NSThread *)mainThread NS_AVAILABLE(10_5, 2_0);
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTimeZone.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTimeZone.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTimeZone.h	2016-07-13 05:25:23.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTimeZone.h	2016-07-25 07:03:56.000000000 +0200
@@ -25,12 +25,12 @@
 
 @interface NSTimeZone (NSExtendedTimeZone)
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, copy) NSTimeZone *systemTimeZone;
 #endif
 + (void)resetSystemTimeZone;
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, copy) NSTimeZone *defaultTimeZone;
 
 @property (class, readonly, copy) NSTimeZone *localTimeZone;
@@ -89,17 +89,4 @@
 
 FOUNDATION_EXPORT NSNotificationName const NSSystemTimeZoneDidChangeNotification NS_AVAILABLE(10_5, 2_0);
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSTimeZone (NSLegacySwiftCompatability)
-+ (NSTimeZone *)systemTimeZone;
-+ (NSTimeZone *)defaultTimeZone;
-+ (void)setDefaultTimeZone:(NSTimeZone *)timeZone;
-+ (NSTimeZone *)localTimeZone;
-+ (NSArray<NSString *> *)knownTimeZoneNames;
-+ (void)setAbbreviationDictionary:(NSDictionary<NSString *, NSString *> *)dictionary NS_AVAILABLE(10_6, 4_0);
-+ (NSDictionary<NSString *, NSString *> *)abbreviationDictionary;
-+ (NSString *)timeZoneDataVersion NS_AVAILABLE(10_6, 4_0);
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURL.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURL.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURL.h	2016-07-10 08:52:39.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURL.h	2016-07-26 03:54:41.000000000 +0200
@@ -85,7 +85,7 @@
  */
 @property (readonly, copy) NSData *dataRepresentation NS_AVAILABLE(10_11, 9_0);
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 6)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(6)
 @property (nullable, readonly, copy) NSString *absoluteString;
 @property (readonly, copy) NSString *relativeString; // The relative portion of a URL.  If baseURL is nil, or if the receiver is itself absolute, this is the same as absoluteString
 @property (nullable, readonly, copy) NSURL *baseURL; // may be nil.
@@ -95,17 +95,7 @@
  */
 @property (nullable, readonly, copy) NSString *scheme;
 @property (nullable, readonly, copy) NSString *resourceSpecifier;
-#else
-@property (readonly, copy) NSString *absoluteString;
-@property (nullable, readonly, copy) NSString *relativeString; // The relative portion of a URL.  If baseURL is nil, or if the receiver is itself absolute, this is the same as absoluteString
-@property (nullable, readonly, copy) NSURL *baseURL; // may be nil.
-@property (readonly, copy) NSURL *absoluteURL; // if the receiver is itself absolute, this will return self.
-
-/* Any URL is composed of these two basic pieces.  The full URL would be the concatenation of [myURL scheme], ':', [myURL resourceSpecifier]
- */
-@property (readonly, copy) NSString *scheme;
-@property (readonly, copy) NSString *resourceSpecifier;
-#endif // SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 6
+#endif // FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(6)
 
 /* If the URL conforms to rfc 1808 (the most common form of URL), the following accessors will return the various components; otherwise they return nil.  The litmus test for conformance is as recommended in RFC 1808 - whether the first two characters of resourceSpecifier is @"//".  In all cases, they return the component's value after resolving the receiver against its base URL.
  */
@@ -515,7 +505,7 @@
 
 
 @interface NSCharacterSet (NSURLUtilities)
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 // Predefined character sets for the six URL components and subcomponents which allow percent encoding. These character sets are passed to -stringByAddingPercentEncodingWithAllowedCharacters:.
 
 // Returns a character set containing the characters allowed in an URL's user subcomponent.
@@ -562,19 +552,13 @@
 @property (nullable, readonly, copy) NSArray<NSString *> *pathComponents NS_AVAILABLE(10_6, 4_0);
 @property (nullable, readonly, copy) NSString *lastPathComponent NS_AVAILABLE(10_6, 4_0);
 @property (nullable, readonly, copy) NSString *pathExtension NS_AVAILABLE(10_6, 4_0);
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 6)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(6)
 - (nullable NSURL *)URLByAppendingPathComponent:(NSString *)pathComponent NS_AVAILABLE(10_6, 4_0);
 - (nullable NSURL *)URLByAppendingPathComponent:(NSString *)pathComponent isDirectory:(BOOL)isDirectory NS_AVAILABLE(10_7, 5_0);
 @property (nullable, readonly, copy) NSURL *URLByDeletingLastPathComponent NS_AVAILABLE(10_6, 4_0);
 - (nullable NSURL *)URLByAppendingPathExtension:(NSString *)pathExtension NS_AVAILABLE(10_6, 4_0);
 @property (nullable, readonly, copy) NSURL *URLByDeletingPathExtension NS_AVAILABLE(10_6, 4_0);
-#else
-- (NSURL *)URLByAppendingPathComponent:(NSString *)pathComponent NS_AVAILABLE(10_6, 4_0);
-- (NSURL *)URLByAppendingPathComponent:(NSString *)pathComponent isDirectory:(BOOL)isDirectory NS_AVAILABLE(10_7, 5_0);
-@property (nullable, readonly, copy) NSURL *URLByDeletingLastPathComponent NS_AVAILABLE(10_6, 4_0);
-- (NSURL *)URLByAppendingPathExtension:(NSString *)pathExtension NS_AVAILABLE(10_6, 4_0);
-@property (nullable, readonly, copy) NSURL *URLByDeletingPathExtension NS_AVAILABLE(10_6, 4_0);
-#endif // SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 6
+#endif // FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(6)
 
 /* The following methods work only on `file:` scheme URLs; for non-`file:` scheme URLs, these methods return the URL unchanged.
  */
@@ -626,15 +610,4 @@
 @end
 #endif
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSCharacterSet (NSLegacySwiftCompatability)
-+ (NSCharacterSet *)URLUserAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
-+ (NSCharacterSet *)URLPasswordAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
-+ (NSCharacterSet *)URLHostAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
-+ (NSCharacterSet *)URLPathAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
-+ (NSCharacterSet *)URLQueryAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
-+ (NSCharacterSet *)URLFragmentAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCache.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCache.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCache.h	2016-07-13 05:50:31.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCache.h	2016-07-26 03:54:41.000000000 +0200
@@ -149,7 +149,7 @@
     becoming unexpectedly unretrievable.
     @result the shared NSURLCache instance.
 */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, strong) NSURLCache *sharedURLCache;
 #endif
 
@@ -257,10 +257,4 @@
 - (void)removeCachedResponseForDataTask:(NSURLSessionDataTask *)dataTask NS_AVAILABLE(10_10, 8_0);
 @end
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSURLCache (NSLegacySwiftCompatability)
-+ (NSURLCache *)sharedURLCache;
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCredentialStorage.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCredentialStorage.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCredentialStorage.h	2016-07-13 05:25:24.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCredentialStorage.h	2016-07-25 07:12:53.000000000 +0200
@@ -34,7 +34,7 @@
     @abstract Get the shared singleton authentication storage
     @result the shared authentication storage
 */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, strong) NSURLCredentialStorage *sharedCredentialStorage;
 #endif
 
@@ -131,11 +131,4 @@
  */
 FOUNDATION_EXPORT NSString *const NSURLCredentialStorageRemoveSynchronizableCredentials NS_AVAILABLE(10_9, 7_0);
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSURLCredentialStorage (NSLegacySwiftCompatability)
-+ (NSURLCredentialStorage *)sharedCredentialStorage;
-@end
-#endif
-
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLRequest.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLRequest.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLRequest.h	2016-07-10 07:51:25.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLRequest.h	2016-07-26 03:54:41.000000000 +0200
@@ -197,10 +197,8 @@
     @abstract Indicates that NSURLRequest implements the NSSecureCoding protocol.
     @result A BOOL value set to YES.
 */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly) BOOL supportsSecureCoding;
-#else
-+ (BOOL)supportsSecureCoding;
 #endif
 /*!
     @method requestWithURL:cachePolicy:timeoutInterval:
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLSession.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLSession.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLSession.h	2016-07-13 05:50:30.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLSession.h	2016-07-25 07:03:55.000000000 +0200
@@ -125,7 +125,7 @@
  * The shared session uses the currently set global NSURLCache,
  * NSHTTPCookieStorage and NSURLCredentialStorage objects.
  */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, strong) NSURLSession *sharedSession;
 #endif
 
@@ -480,7 +480,7 @@
 NS_CLASS_AVAILABLE(NSURLSESSION_AVAILABLE, 7_0)
 @interface NSURLSessionConfiguration : NSObject <NSCopying>
 
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, strong) NSURLSessionConfiguration *defaultSessionConfiguration;
 @property (class, readonly, strong) NSURLSessionConfiguration *ephemeralSessionConfiguration;
 #endif
@@ -999,15 +999,4 @@
 
 @end
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSURLSession (NSLegacySwiftCompatability)
-+ (NSURLSession *)sharedSession;
-@end
-
-@interface NSURLSessionConfiguration (NSLegacySwiftCompatability)
-+ (NSURLSessionConfiguration *)defaultSessionConfiguration;
-+ (NSURLSessionConfiguration *)ephemeralSessionConfiguration;
-@end
-#endif
-
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserActivity.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserActivity.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserActivity.h	2016-07-13 05:50:30.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserActivity.h	2016-07-26 03:54:41.000000000 +0200
@@ -18,11 +18,11 @@
 
 /* Initializes and returns a newly created NSUserActivity with the given activityType. A user activity may be continued only in an application that (1) has the same developer Team ID as the activity's source application and (2) supports the activity's type. Supported activity types are specified in the application's Info.plist under the NSUserActivityTypes key. When receiving a user activity for continuation, the system locates the appropriate application to launch by finding applications with the target Team ID, then filtering on the incoming activity's type identifier.
 */
-- (instancetype)initWithActivityType:(NSString *)activityType;
+- (instancetype)initWithActivityType:(NSString *)activityType NS_DESIGNATED_INITIALIZER;
 
 /* Initializes and returns a newly created NSUserActivity with the first activityType from the NSUserActivityTypes key in the application’s Info.plist.
 */
-- (instancetype)init;
+- (instancetype)init API_DEPRECATED("Use initWithActivityType: with a specific activity type string", macosx(10.10, 10.12), ios(8.0, 10.0), watchos(2.0, 3.0), tvos(9.0, 10.0));
 
 /* The activityType the user activity was created with.
 */
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserDefaults.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserDefaults.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserDefaults.h	2016-07-10 07:51:25.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserDefaults.h	2016-07-25 07:12:53.000000000 +0200
@@ -57,7 +57,7 @@
 /*!
  +standardUserDefaults returns a global instance of NSUserDefaults configured to search the current application's search list.
  */
-#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+#if FOUNDATION_SWIFT_SDK_EPOCH_AT_LEAST(8)
 @property (class, readonly, strong) NSUserDefaults *standardUserDefaults;
 #endif
 
@@ -242,10 +242,4 @@
 FOUNDATION_EXPORT NSString * const NSNegativeCurrencyFormatString NS_DEPRECATED(10_0, 10_5, NA, NA);
 #endif
 
-#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
-@interface NSUserDefaults (NSLegacySwiftCompatability)
-+ (NSUserDefaults *)standardUserDefaults;
-@end
-#endif
-
 NS_ASSUME_NONNULL_END

```