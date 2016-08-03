#Foundation.framework

``` diff
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
d```