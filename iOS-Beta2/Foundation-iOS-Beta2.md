#Foundation.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSBundle.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSBundle.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSBundle.h	2016-05-20 06:25:32.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSBundle.h	2016-06-27 06:06:56.000000000 +0200
@@ -29,7 +29,10 @@
 }
 
 /* Methods for creating or retrieving bundle instances. */
-+ (NSBundle *)mainBundle;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, strong) NSBundle *mainBundle;
+#endif
+
 + (nullable instancetype)bundleWithPath:(NSString *)path;
 - (nullable instancetype)initWithPath:(NSString *)path NS_DESIGNATED_INITIALIZER;
 
@@ -39,8 +42,10 @@
 + (NSBundle *)bundleForClass:(Class)aClass;
 + (nullable NSBundle *)bundleWithIdentifier:(NSString *)identifier;
 
-+ (NSArray<NSBundle *> *)allBundles;
-+ (NSArray<NSBundle *> *)allFrameworks;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, copy) NSArray<NSBundle *> *allBundles;
+@property (class, readonly, copy) NSArray<NSBundle *> *allFrameworks;
+#endif
 
 /* Methods for loading and unloading bundles. */
 - (BOOL)load;
@@ -128,9 +133,9 @@
 @end
 
 #define NSLocalizedString(key, comment) \
-	    [[NSBundle mainBundle] localizedStringForKey:(key) value:@"" table:nil]
+	    [NSBundle.mainBundle localizedStringForKey:(key) value:@"" table:nil]
 #define NSLocalizedStringFromTable(key, tbl, comment) \
-	    [[NSBundle mainBundle] localizedStringForKey:(key) value:@"" table:(tbl)]
+	    [NSBundle.mainBundle localizedStringForKey:(key) value:@"" table:(tbl)]
 #define NSLocalizedStringFromTableInBundle(key, tbl, bundle, comment) \
 	    [bundle localizedStringForKey:(key) value:@"" table:(tbl)]
 #define NSLocalizedStringWithDefaultValue(key, tbl, bundle, val, comment) \
@@ -247,4 +252,12 @@
  */
 FOUNDATION_EXPORT double const NSBundleResourceRequestLoadingPriorityUrgent NS_AVAILABLE(NA, 9_0);
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSBundle (NSLegacySwiftCompatability)
++ (NSBundle *)mainBundle;
++ (NSArray<NSBundle *> *)allBundles;
++ (NSArray<NSBundle *> *)allFrameworks;
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCalendar.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCalendar.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCalendar.h	2016-05-20 07:35:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCalendar.h	2016-06-27 06:02:14.000000000 +0200
@@ -98,8 +98,10 @@
 @interface NSCalendar : NSObject <NSCopying, NSSecureCoding>
 
 
-+ (NSCalendar *)currentCalendar;					// user's preferred calendar
-+ (NSCalendar *)autoupdatingCurrentCalendar NS_AVAILABLE(10_5, 2_0); // tracks changes to user's preferred calendar identifier
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, copy) NSCalendar *currentCalendar;					// user's preferred calendar
+@property (class, readonly, strong) NSCalendar *autoupdatingCurrentCalendar NS_AVAILABLE(10_5, 2_0); // tracks changes to user's preferred calendar identifier
+#endif
 
 /*
 	This method returns a new autoreleased calendar object of the given type, specified by a calendar identifier constant.
@@ -467,5 +469,14 @@
 
 
 @end
+    
+    
+    
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSCalendar (NSLegacySwiftCompatability)
++ (NSCalendar *)currentCalendar;
++ (NSCalendar *)autoupdatingCurrentCalendar NS_AVAILABLE(10_5, 2_0);
+@end
+#endif
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCharacterSet.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCharacterSet.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCharacterSet.h	2016-05-20 07:35:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCharacterSet.h	2016-06-27 06:06:10.000000000 +0200
@@ -1,5 +1,5 @@
 /*	NSCharacterSet.h
-	Copyright (c) 1994-2015, Apple Inc. All rights reserved.
+	Copyright (c) 1994-2016, Apple Inc. All rights reserved.
 */
 
 #import <CoreFoundation/CFCharacterSet.h>
@@ -17,21 +17,23 @@
 
 @interface NSCharacterSet : NSObject <NSCopying, NSMutableCopying, NSSecureCoding>
 
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
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (nonatomic, readonly, class, copy) NSCharacterSet *controlCharacterSet;
+@property (nonatomic, readonly, class, copy) NSCharacterSet *whitespaceCharacterSet;
+@property (nonatomic, readonly, class, copy) NSCharacterSet *whitespaceAndNewlineCharacterSet;
+@property (nonatomic, readonly, class, copy) NSCharacterSet *decimalDigitCharacterSet;
+@property (nonatomic, readonly, class, copy) NSCharacterSet *letterCharacterSet;
+@property (nonatomic, readonly, class, copy) NSCharacterSet *lowercaseLetterCharacterSet;
+@property (nonatomic, readonly, class, copy) NSCharacterSet *uppercaseLetterCharacterSet;
+@property (nonatomic, readonly, class, copy) NSCharacterSet *nonBaseCharacterSet;
+@property (nonatomic, readonly, class, copy) NSCharacterSet *alphanumericCharacterSet;
+@property (nonatomic, readonly, class, copy) NSCharacterSet *decomposableCharacterSet;
+@property (nonatomic, readonly, class, copy) NSCharacterSet *illegalCharacterSet;
+@property (nonatomic, readonly, class, copy) NSCharacterSet *punctuationCharacterSet;
+@property (nonatomic, readonly, class, copy) NSCharacterSet *capitalizedLetterCharacterSet;
+@property (nonatomic, readonly, class, copy) NSCharacterSet *symbolCharacterSet;
+@property (nonatomic, readonly, class, copy) NSCharacterSet *newlineCharacterSet NS_AVAILABLE(10_5, 2_0);
+#endif
 
 + (NSCharacterSet *)characterSetWithRange:(NSRange)aRange;
 + (NSCharacterSet *)characterSetWithCharactersInString:(NSString *)aString;
@@ -84,4 +86,24 @@
 
 @end
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSCharacterSet (NSLegacySwiftCompatability)
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
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDate.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDate.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDate.h	2016-05-20 07:35:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDate.h	2016-06-27 07:21:40.000000000 +0200
@@ -42,7 +42,9 @@
 @property (readonly, copy) NSString *description;
 - (NSString *)descriptionWithLocale:(nullable id)locale;
 
-+ (NSTimeInterval)timeIntervalSinceReferenceDate;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly) NSTimeInterval timeIntervalSinceReferenceDate;
+#endif
 
 @end
 
@@ -54,8 +56,10 @@
 + (instancetype)dateWithTimeIntervalSince1970:(NSTimeInterval)secs;
 + (instancetype)dateWithTimeInterval:(NSTimeInterval)secsToBeAdded sinceDate:(NSDate *)date;
 
-+ (NSDate *)distantFuture;
-+ (NSDate *)distantPast;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, copy) NSDate *distantFuture;
+@property (class, readonly, copy) NSDate *distantPast;
+#endif
 
 - (instancetype)initWithTimeIntervalSinceNow:(NSTimeInterval)secs;
 - (instancetype)initWithTimeIntervalSince1970:(NSTimeInterval)secs;
@@ -63,4 +67,12 @@
 
 @end
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSDate (NSLegacySwiftCompatability)
++ (NSTimeInterval)timeIntervalSinceReferenceDate;
++ (NSDate *)distantFuture;
++ (NSDate *)distantPast;
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateFormatter.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateFormatter.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateFormatter.h	2016-05-20 06:25:32.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateFormatter.h	2016-06-27 06:02:14.000000000 +0200
@@ -60,9 +60,9 @@
 	// no options defined, pass 0 for now
 
 // Attributes of an NSDateFormatter
-
-+ (NSDateFormatterBehavior)defaultFormatterBehavior;
-+ (void)setDefaultFormatterBehavior:(NSDateFormatterBehavior)behavior;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class) NSDateFormatterBehavior defaultFormatterBehavior;
+#endif
 
 /*
  A convenient way to generate an appropriate localized date format, and set it, in a single operation.
@@ -120,4 +120,12 @@
 @end
 #endif
 
+
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSDateFormatter (NSLegacySwiftCompatability)
++ (NSDateFormatterBehavior)defaultFormatterBehavior;
++ (void)setDefaultFormatterBehavior:(NSDateFormatterBehavior)behavior;
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDecimalNumber.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDecimalNumber.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDecimalNumber.h	2016-05-20 07:35:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDecimalNumber.h	2016-06-27 07:19:44.000000000 +0200
@@ -61,11 +61,13 @@
 + (NSDecimalNumber *)decimalNumberWithString:(nullable NSString *)numberValue;
 + (NSDecimalNumber *)decimalNumberWithString:(nullable NSString *)numberValue locale:(nullable id)locale;
 
-+ (NSDecimalNumber *)zero;
-+ (NSDecimalNumber *)one;
-+ (NSDecimalNumber *)minimumDecimalNumber;
-+ (NSDecimalNumber *)maximumDecimalNumber;
-+ (NSDecimalNumber *)notANumber;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, copy) NSDecimalNumber *zero;
+@property (class, readonly, copy) NSDecimalNumber *one;
+@property (class, readonly, copy) NSDecimalNumber *minimumDecimalNumber;
+@property (class, readonly, copy) NSDecimalNumber *maximumDecimalNumber;
+@property (class, readonly, copy) NSDecimalNumber *notANumber;
+#endif
 
 - (NSDecimalNumber *)decimalNumberByAdding:(NSDecimalNumber *)decimalNumber;
 - (NSDecimalNumber *)decimalNumberByAdding:(NSDecimalNumber *)decimalNumber withBehavior:(nullable id <NSDecimalNumberBehaviors>)behavior;
@@ -92,9 +94,9 @@
 - (NSComparisonResult)compare:(NSNumber *)decimalNumber;
     // compare two NSDecimalNumbers
 
-+ (void)setDefaultBehavior:(id <NSDecimalNumberBehaviors>)behavior;
-
-+ (id <NSDecimalNumberBehaviors>)defaultBehavior;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, strong) id <NSDecimalNumberBehaviors> defaultBehavior;
+#endif
     // One behavior per thread - The default behavior is
     //   rounding mode: NSRoundPlain
     //   scale: No defined scale (full precision)
@@ -151,4 +153,17 @@
 
 @end
 
+                            
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSDecimalNumber (NSLegacySwiftCompatability)
++ (NSDecimalNumber *)zero;
++ (NSDecimalNumber *)one;
++ (NSDecimalNumber *)minimumDecimalNumber;
++ (NSDecimalNumber *)maximumDecimalNumber;
++ (NSDecimalNumber *)notANumber;
++ (id <NSDecimalNumberBehaviors>)defaultBehavior;
++ (void)setDefaultBehavior:(id <NSDecimalNumberBehaviors>)behavior;
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSException.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSException.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSException.h	2016-05-20 06:13:47.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSException.h	2016-06-27 06:06:10.000000000 +0200
@@ -293,7 +293,9 @@
     void *_reserved;
 }
 
-+ (NSAssertionHandler *)currentHandler;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, strong) NSAssertionHandler *currentHandler;
+#endif
 
 - (void)handleFailureInMethod:(SEL)selector object:(id)object file:(NSString *)fileName lineNumber:(NSInteger)line description:(nullable NSString *)format,... NS_FORMAT_FUNCTION(5,6);
 
@@ -301,4 +303,10 @@
 
 @end
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSAssertionHandler (NSLegacySwiftCompatability)
++ (NSAssertionHandler *)currentHandler;
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileCoordinator.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileCoordinator.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileCoordinator.h	2016-05-20 06:13:48.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileCoordinator.h	2016-06-26 17:36:07.000000000 +0200
@@ -103,7 +103,9 @@
 */
 + (void)addFilePresenter:(id<NSFilePresenter>)filePresenter;
 + (void)removeFilePresenter:(id<NSFilePresenter>)filePresenter;
-+ (NSArray<id<NSFilePresenter>> *)filePresenters;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, copy) NSArray<id<NSFilePresenter>> *filePresenters;
+#endif
 
 /* The designated initializer. If an NSFilePresenter is provided then the receiver is considered to have been created by that NSFilePresenter, or on its behalf.
 
@@ -227,5 +229,10 @@
 
 @end
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSFileCoordinator (NSLegacySwiftCompatability)
++ (NSArray<id<NSFilePresenter>> *)filePresenters;
+@end
+#endif
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileHandle.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileHandle.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileHandle.h	2016-05-20 07:35:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileHandle.h	2016-06-27 07:19:45.000000000 +0200
@@ -37,10 +37,12 @@
 
 @interface NSFileHandle (NSFileHandleCreation)
 
-+ (NSFileHandle *)fileHandleWithStandardInput;
-+ (NSFileHandle *)fileHandleWithStandardOutput;
-+ (NSFileHandle *)fileHandleWithStandardError;
-+ (NSFileHandle *)fileHandleWithNullDevice;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, strong) NSFileHandle *fileHandleWithStandardInput;
+@property (class, readonly, strong) NSFileHandle *fileHandleWithStandardOutput;
+@property (class, readonly, strong) NSFileHandle *fileHandleWithStandardError;
+@property (class, readonly, strong) NSFileHandle *fileHandleWithNullDevice;
+#endif
 
 + (nullable instancetype)fileHandleForReadingAtPath:(NSString *)path;
 + (nullable instancetype)fileHandleForWritingAtPath:(NSString *)path;
@@ -101,4 +103,13 @@
 
 @end
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSFileHandle (NSLegacySwiftCompatability)
++ (NSFileHandle *)fileHandleWithStandardInput;
++ (NSFileHandle *)fileHandleWithStandardOutput;
++ (NSFileHandle *)fileHandleWithStandardError;
++ (NSFileHandle *)fileHandleWithNullDevice;
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileManager.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileManager.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileManager.h	2016-05-20 07:39:55.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileManager.h	2016-06-27 07:21:40.000000000 +0200
@@ -90,7 +90,9 @@
 
 /* Returns the default singleton instance.
 */
-+ (NSFileManager *)defaultManager;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, strong) NSFileManager *defaultManager;
+#endif
 
 /* -mountedVolumeURLsIncludingResourceValuesForKeys:options: returns an NSArray of NSURLs locating the mounted volumes available on the computer. The property keys that can be requested are available in <Foundation/NSURL.h>.
  */
@@ -143,7 +145,11 @@
  
     This method replaces changeFileAttributes:atPath:.
  */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+- (BOOL)setAttributes:(NSDictionary<NSFileAttributeKey, id> *)attributes ofItemAtPath:(NSString *)path error:(NSError **)error NS_AVAILABLE(10_5, 2_0);
+#else
 - (BOOL)setAttributes:(NSDictionary<NSString *, id> *)attributes ofItemAtPath:(NSString *)path error:(NSError **)error NS_AVAILABLE(10_5, 2_0);
+#endif
 
 /* createDirectoryAtPath:withIntermediateDirectories:attributes:error: creates a directory at the specified path. If you pass 'NO' for createIntermediates, the directory must not exist at the time this call is made. Passing 'YES' for 'createIntermediates' will create any necessary intermediate directories. This method returns YES if all directories specified in 'path' were created and attributes were set. Directories are created with attributes specified by the dictionary passed to 'attributes'. If no dictionary is supplied, directories are created according to the umask of the process. This method returns NO if a failure occurs at any stage of the operation. If an error parameter was provided, a presentable NSError will be returned by reference.
  
@@ -167,13 +173,21 @@
  
     This method replaces fileAttributesAtPath:traverseLink:.
  */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+- (nullable NSDictionary<NSFileAttributeKey, id> *)attributesOfItemAtPath:(NSString *)path error:(NSError **)error NS_AVAILABLE(10_5, 2_0);
+#else
 - (nullable NSDictionary<NSString *, id> *)attributesOfItemAtPath:(NSString *)path error:(NSError **)error NS_AVAILABLE(10_5, 2_0);
+#endif
 
 /* attributesOfFileSystemForPath:error: returns an NSDictionary of key/value pairs containing the attributes of the filesystem containing the provided path. If this method returns 'nil', an NSError will be returned by reference in the 'error' parameter. This method does not traverse a terminal symlink.
  
     This method replaces fileSystemAttributesAtPath:.
  */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+- (nullable NSDictionary<NSFileAttributeKey, id> *)attributesOfFileSystemForPath:(NSString *)path error:(NSError **)error NS_AVAILABLE(10_5, 2_0);
+#else
 - (nullable NSDictionary<NSString *, id> *)attributesOfFileSystemForPath:(NSString *)path error:(NSError **)error NS_AVAILABLE(10_5, 2_0);
+#endif
 
 /* createSymbolicLinkAtPath:withDestination:error: returns YES if the symbolic link that point at 'destPath' was able to be created at the location specified by 'path'. If this method returns NO, the link was unable to be created and an NSError will be returned by reference in the 'error' parameter. This method does not traverse a terminal symlink.
  
@@ -407,8 +421,13 @@
 
 /* For NSDirectoryEnumerators created with -enumeratorAtPath:, the -fileAttributes and -directoryAttributes methods return an NSDictionary containing the keys listed below. For NSDirectoryEnumerators created with -enumeratorAtURL:includingPropertiesForKeys:options:errorHandler:, these two methods return nil.
  */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (nullable, readonly, copy) NSDictionary<NSFileAttributeKey, id> *fileAttributes;
+@property (nullable, readonly, copy) NSDictionary<NSFileAttributeKey, id> *directoryAttributes;
+#else
 @property (nullable, readonly, copy) NSDictionary<NSString *, id> *fileAttributes;
 @property (nullable, readonly, copy) NSDictionary<NSString *, id> *directoryAttributes;
+#endif
 
 - (void)skipDescendents;
 
@@ -479,4 +498,10 @@
 - (nullable NSNumber *)fileGroupOwnerAccountID;
 @end
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSFileManager (NSLegacySwiftCompatability)
++ (NSFileManager *)defaultManager;
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHTTPCookieStorage.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHTTPCookieStorage.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHTTPCookieStorage.h	2016-05-20 07:35:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHTTPCookieStorage.h	2016-06-27 06:06:10.000000000 +0200
@@ -50,13 +50,15 @@
 }
 
 /*!
-    @method sharedHTTPCookieStorage
+    @property sharedHTTPCookieStorage
     @abstract Get the shared cookie storage in the default location.
     @result The shared cookie storage
     @discussion Starting in OS X 10.11, each app has its own sharedHTTPCookieStorage singleton, 
     which will not be shared with other applications.
 */
-+ (NSHTTPCookieStorage *)sharedHTTPCookieStorage;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property(class, readonly, strong) NSHTTPCookieStorage *sharedHTTPCookieStorage;
+#endif
 
 /*!
     @method sharedCookieStorageForGroupContainerIdentifier:
@@ -151,6 +153,13 @@
 - (void)getCookiesForTask:(NSURLSessionTask *)task completionHandler:(void (^) (NSArray<NSHTTPCookie *> * _Nullable cookies))completionHandler NS_AVAILABLE(10_10, 8_0);
 @end
 
+
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSHTTPCookieStorage (NSLegacySwiftCompatability)
++ (NSHTTPCookieStorage *)sharedHTTPCookieStorage;
+@end
+#endif
+
 /*!
     @const NSHTTPCookieManagerAcceptPolicyChangedNotification
     @discussion Name of notification that should be posted to the
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyValueCoding.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyValueCoding.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyValueCoding.h	2016-05-20 07:39:55.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyValueCoding.h	2016-06-27 07:19:45.000000000 +0200
@@ -39,9 +39,13 @@
 
 @interface NSObject(NSKeyValueCoding)
 
-/* Return YES if -valueForKey:, -setValue:forKey:, -mutableArrayValueForKey:, -storedValueForKey:, -takeStoredValue:forKey:, and -takeValue:forKey: may directly manipulate instance variables when sent to instances of the receiving class, NO otherwise. The default implementation of this method returns YES.
+/* Return YES if -valueForKey:, -setValue:forKey:, -mutableArrayValueForKey:, -storedValueForKey:, -takeStoredValue:forKey:, and -takeValue:forKey: may directly manipulate instance variables when sent to instances of the receiving class, NO otherwise. The default implementation of this property returns YES.
 */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly) BOOL accessInstanceVariablesDirectly;
+#else
 + (BOOL)accessInstanceVariablesDirectly;
+#endif
 
 /* Given a key that identifies an attribute or to-one relationship, return the attribute value or the related object. Given a key that identifies a to-many relationship, return an immutable array or an immutable set that contains all of the related objects.
     
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLocale.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLocale.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLocale.h	2016-05-20 07:35:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLocale.h	2016-06-27 07:21:40.000000000 +0200
@@ -86,10 +86,12 @@
 
 @interface NSLocale (NSLocaleCreation)
 
-+ (NSLocale *)autoupdatingCurrentLocale NS_AVAILABLE(10_5, 2_0); // generally you should use this method
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, strong) NSLocale *autoupdatingCurrentLocale NS_AVAILABLE(10_5, 2_0); // generally you should use this property
 
-+ (NSLocale *)currentLocale;	// an object representing the user's current locale
-+ (NSLocale *)systemLocale;	// the default generic root locale with little localization
+@property (class, readonly, copy) NSLocale *currentLocale;	// an object representing the user's current locale
+@property (class, readonly, copy) NSLocale *systemLocale;	// the default generic root locale with little localization
+#endif
 
 + (instancetype)localeWithLocaleIdentifier:(NSString *)ident NS_AVAILABLE(10_6, 4_0);
 
@@ -99,13 +101,15 @@
 
 @interface NSLocale (NSLocaleGeneralInfo)
 
-+ (NSArray<NSString *> *)availableLocaleIdentifiers;
-+ (NSArray<NSString *> *)ISOLanguageCodes;
-+ (NSArray<NSString *> *)ISOCountryCodes;
-+ (NSArray<NSString *> *)ISOCurrencyCodes;
-+ (NSArray<NSString *> *)commonISOCurrencyCodes NS_AVAILABLE(10_5, 2_0);
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, copy) NSArray<NSString *> *availableLocaleIdentifiers;
+@property (class, readonly, copy) NSArray<NSString *> *ISOLanguageCodes;
+@property (class, readonly, copy) NSArray<NSString *> *ISOCountryCodes;
+@property (class, readonly, copy) NSArray<NSString *> *ISOCurrencyCodes;
+@property (class, readonly, copy) NSArray<NSString *> *commonISOCurrencyCodes NS_AVAILABLE(10_5, 2_0);
 
-+ (NSArray<NSString *> *)preferredLanguages NS_AVAILABLE(10_5, 2_0); // note that this list does not indicate what language the app is actually running in; the [NSBundle mainBundle] object determines that at launch and knows that information
+@property (class, readonly, copy) NSArray<NSString *> *preferredLanguages NS_AVAILABLE(10_5, 2_0); // note that this list does not indicate what language the app is actually running in; the NSBundle.mainBundle object determines that at launch and knows that information
+#endif
 
 + (NSDictionary<NSString *, NSString *> *)componentsFromLocaleIdentifier:(NSString *)string;
 + (NSString *)localeIdentifierFromComponents:(NSDictionary<NSString *, NSString *> *)dict;
@@ -173,4 +177,18 @@
 FOUNDATION_EXPORT NSString * const NSIndianCalendar NS_CALENDAR_DEPRECATED(10_6, 10_10, 4_0, 8_0, "Use NSCalendarIdentifierIndian instead");
 FOUNDATION_EXPORT NSString * const NSISO8601Calendar NS_CALENDAR_DEPRECATED(10_6, 10_10, 4_0, 8_0, "Use NSCalendarIdentifierISO8601 instead");
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSLocale (NSLegacySwiftCompatability)
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
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMeasurementFormatter.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMeasurementFormatter.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMeasurementFormatter.h	2016-05-20 07:35:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMeasurementFormatter.h	2016-06-27 07:21:40.000000000 +0200
@@ -1,6 +1,6 @@
 /*
  NSMeasurementFormatter.h
- Copyright © 2015, Apple Inc.
+ Copyright (c) 2015-2016, Apple Inc.
  All rights reserved.
  */
 
@@ -13,8 +13,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 typedef NS_OPTIONS(NSUInteger, NSMeasurementFormatterUnitOptions) {
-    NSMeasurementFormatterUnitOptionsPreferredUnitOfLocale API_DEPRECATED("No longer necessary - this is now the default behavior of the formatter.", macosx(10.12, 10.12), ios(10.0, 10.0), watchos(3.0, 3.0), tvos(10.0, 10.0)) = 0,
-    NSMeasurementFormatterUnitOptionsProvidedUnit = (1UL << 0),              // e.g  This ensures the formatter uses this unit even if it is not the preferred unit of the set locale.
+    NSMeasurementFormatterUnitOptionsProvidedUnit = (1UL << 0),              // e.g  This ensures the formatter uses this unit even if it is not the preferred unit of the set locale.  All other unit options are ignored if this option is set.
     NSMeasurementFormatterUnitOptionsNaturalScale = (1UL << 1),              // e.g. This would make the formatter show "12 kilometers" instead of "12000 meters"
     NSMeasurementFormatterUnitOptionsTemperatureWithoutUnit = (1UL << 2),    // e.g. This would display "90°" rather than "90°F" or "90°C"
 } API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
@@ -23,10 +22,6 @@
 @interface NSMeasurementFormatter : NSFormatter <NSSecureCoding> {
 @private
     void *_formatter;
-    NSMeasurementFormatterUnitOptions _unitOptions;
-    NSFormattingUnitStyle _unitStyle;
-    NSLocale *_locale;
-    NSNumberFormatter *_numberFormatter;
 }
 
 /*
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotification.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotification.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotification.h	2016-05-20 07:35:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotification.h	2016-06-27 07:21:40.000000000 +0200
@@ -41,9 +41,11 @@
     void *_pad[11];
 }
 
-+ (NSNotificationCenter *)defaultCenter;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, strong) NSNotificationCenter *defaultCenter;
 
-- (void)addObserver:(id)observer selector:(SEL)aSelector name:(nullable NSString *)aName object:(nullable id)anObject;
+- (void)addObserver:(id)observer selector:(SEL)aSelector name:(nullable NSNotificationName)aName object:(nullable id)anObject;
+#endif
 
 - (void)postNotification:(NSNotification *)notification;
 - (void)postNotificationName:(NSNotificationName)aName object:(nullable id)anObject;
@@ -58,4 +60,11 @@
 
 @end
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSNotificationCenter (NSLegacySwiftCompatability)
++ (NSNotificationCenter *)defaultCenter;
+- (void)addObserver:(id)observer selector:(SEL)aSelector name:(nullable NSString *)aName object:(nullable id)anObject;
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotificationQueue.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotificationQueue.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotificationQueue.h	2016-05-20 07:35:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotificationQueue.h	2016-06-27 07:21:40.000000000 +0200
@@ -29,8 +29,9 @@
     id		_idleQueue;
     id		_idleObs;
 }
-
-+ (NSNotificationQueue *)defaultQueue;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, strong) NSNotificationQueue *defaultQueue;
+#endif
 
 - (instancetype)initWithNotificationCenter:(NSNotificationCenter *)notificationCenter NS_DESIGNATED_INITIALIZER;
 
@@ -41,4 +42,10 @@
 
 @end
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSNotificationQueue (NSLegacySwiftCompatability)
++ (NSNotificationQueue *)defaultQueue;
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObject.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObject.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObject.h	2016-05-20 06:25:32.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObject.h	2016-06-27 06:02:14.000000000 +0200
@@ -38,9 +38,13 @@
 
 @protocol NSSecureCoding <NSCoding>
 @required
-// This method must be return YES on all classes that allow secure coding. Subclasses of classes that adopt NSSecureCoding and override initWithCoder: must also override this method and return YES.
+// This property must return YES on all classes that allow secure coding. Subclasses of classes that adopt NSSecureCoding and override initWithCoder: must also override this method and return YES.
 // The Secure Coding Guide should be consulted when writing methods that decode data.
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly) BOOL supportsSecureCoding;
+#else
 + (BOOL)supportsSecureCoding;
+#endif
 @end
 
 /***********	Base class		***********/
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOperation.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOperation.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOperation.h	2016-05-20 06:25:32.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOperation.h	2016-06-27 07:19:45.000000000 +0200
@@ -1,5 +1,5 @@
 /*	NSOperation.h
-	Copyright (c) 2006-2015, Apple Inc. All rights reserved.
+	Copyright (c) 2006-2016, Apple Inc. All rights reserved.
 */
 
 #import <Foundation/NSObject.h>
@@ -136,10 +136,19 @@
 
 - (void)waitUntilAllOperationsAreFinished;
 
-+ (nullable NSOperationQueue *)currentQueue NS_AVAILABLE(10_6, 4_0);
-+ (NSOperationQueue *)mainQueue NS_AVAILABLE(10_6, 4_0);
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, strong, nullable) NSOperationQueue *currentQueue NS_AVAILABLE(10_6, 4_0);
+@property (class, readonly, strong) NSOperationQueue *mainQueue NS_AVAILABLE(10_6, 4_0);
+#endif
+
+@end
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSOperationQueue (NSLegacySwiftCompatability)
++ (nullable NSOperationQueue *)currentQueue NS_AVAILABLE(10_6, 4_0);
++ (NSOperationQueue *)mainQueue;
 @end
+#endif
 
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPointerFunctions.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPointerFunctions.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPointerFunctions.h	2016-05-20 07:24:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPointerFunctions.h	2016-06-27 06:02:14.000000000 +0200
@@ -69,7 +69,6 @@
 @property (nullable) void (*relinquishFunction)(const void *item, NSUInteger (* _Nullable size)(const void *item));
 @property (nullable) void * _Nonnull (*acquireFunction)(const void *src, NSUInteger (* _Nullable size)(const void *item), BOOL shouldCopy);
 
-
 // GC used to require that read and write barrier functions be used when pointers are from GC memory
 @property BOOL usesStrongWriteBarrier // pointers should (not) be assigned using the GC strong write barrier
     API_DEPRECATED("Garbage collection no longer supported", macosx(10.5, 10.12), ios(2.0, 10.0), watchos(2.0, 3.0), tvos(9.0, 10.0));
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProcessInfo.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProcessInfo.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProcessInfo.h	2016-05-20 07:24:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProcessInfo.h	2016-06-27 06:06:10.000000000 +0200
@@ -35,7 +35,9 @@
     NSInteger		automaticTerminationOptOutCounter;
 }
 
-+ (NSProcessInfo *)processInfo;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, strong) NSProcessInfo *processInfo;
+#endif
 
 @property (readonly, copy) NSDictionary<NSString *, NSString *> *environment;
 @property (readonly, copy) NSArray<NSString *> *arguments;
@@ -103,15 +105,15 @@
  
  This API can also be used to control auto termination or sudden termination. 
  
-    id activity = [[NSProcessInfo processInfo] beginActivityWithOptions:NSActivityAutomaticTerminationDisabled reason:@"Good Reason"];
+    id activity = [NSProcessInfo.processInfo beginActivityWithOptions:NSActivityAutomaticTerminationDisabled reason:@"Good Reason"];
     // work
-    [[NSProcessInfo processInfo] endActivity:activity];
+    [NSProcessInfo.processInfo endActivity:activity];
  
  is equivalent to:
  
-    [[NSProcessInfo processInfo] disableAutomaticTermination:@"Good Reason"];
+    [NSProcessInfo.processInfo disableAutomaticTermination:@"Good Reason"];
     // work
-    [[NSProcessInfo processInfo] enableAutomaticTermination:@"Good Reason"]
+    [NSProcessInfo.processInfo enableAutomaticTermination:@"Good Reason"]
  
  Since this API returns an object, it may be easier to pair begins and ends. If the object is deallocated before the -endActivity: call, the activity will be automatically ended.
  
@@ -227,8 +229,14 @@
  
  When this notification is posted your application should attempt to reduce power usage by reducing potentially costly computation and other power using activities like network activity or keeping the screen on if the low power mode setting is enabled.
  
- This notification is posted on the global dispatch queue. Register for it using the default notification center. The object associated with the notification is +[NSProcessInfo processInfo].
+ This notification is posted on the global dispatch queue. Register for it using the default notification center. The object associated with the notification is NSProcessInfo.processInfo.
  */
 FOUNDATION_EXTERN NSNotificationName const NSProcessInfoPowerStateDidChangeNotification NS_AVAILABLE(NA, 9_0);
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSProcessInfo (NSLegacySwiftCompatability)
++ (NSProcessInfo *)processInfo;
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProgress.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProgress.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProgress.h	2016-05-20 06:12:55.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProgress.h	2016-06-27 06:02:14.000000000 +0200
@@ -1,14 +1,20 @@
 /*
 	NSProgress.h
-	Copyright (c) 2011-2015, Apple Inc.
+	Copyright (c) 2011-2016, Apple Inc.
 	All rights reserved.
 */
 
 #import <Foundation/NSObject.h>
+#import <Foundation/NSDictionary.h>
 
 @class NSDictionary, NSMutableDictionary, NSMutableSet, NSURL, NSUUID, NSXPCConnection, NSLock;
 
 typedef NSString * NSProgressKind NS_EXTENSIBLE_STRING_ENUM;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+typedef NSString * NSProgressUserInfoKey NS_EXTENSIBLE_STRING_ENUM;
+#else
+typedef NSString * NSProgressKey NS_EXTENSIBLE_STRING_ENUM;
+#endif
 typedef NSString * NSProgressFileOperationKind NS_EXTENSIBLE_STRING_ENUM;
 
 NS_ASSUME_NONNULL_BEGIN
@@ -145,7 +151,11 @@
 
 /* Set a value in the dictionary returned by invocations of -userInfo, with appropriate KVO notification for properties whose values can depend on values in the user info dictionary, like localizedDescription. If a nil value is passed then the dictionary entry is removed.
 */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+- (void)setUserInfoObject:(nullable id)objectOrNil forKey:(NSProgressUserInfoKey)key;
+#else
 - (void)setUserInfoObject:(nullable id)objectOrNil forKey:(NSString *)key;
+#endif
 
 #pragma mark *** Observing and Controlling Progress ***
 
@@ -171,7 +181,11 @@
 
 /* Arbitrary values associated with the receiver. Returns a KVO-compliant dictionary that changes as -setUserInfoObject:forKey: is sent to the receiver. The dictionary will send all of its KVO notifications on the thread which updates the property. The result will never be nil, but may be an empty dictionary. Some entries have meanings that are recognized by the NSProgress class itself. See the NSProgress...Key string constants listed below.
 */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (readonly, copy) NSDictionary<NSProgressUserInfoKey, id> *userInfo;
+#else
 @property (readonly, copy) NSDictionary *userInfo;
+#endif
 
 /* Either a string identifying what kind of progress is being made, like NSProgressKindFile, or nil. If the value of the localizedDescription property has not been set to a non-nil value then the default implementation of -localizedDescription uses the progress kind to determine how to use the values of other properties, as well as values in the user info dictionary, to create a string that is presentable to the user. This is most useful when -localizedDescription is actually being invoked in another process, whose localization language may be different, as a result of using the publish and subscribe mechanism described here.
 */
@@ -218,17 +232,23 @@
 @property (readonly) NSProgress *progress;
 @end
 
-typedef NSString * NSProgressKey NS_EXTENSIBLE_STRING_ENUM;
-
 #pragma mark *** Details of General Progress ***
 
 /* How much time is probably left in the operation, as an NSNumber containing a number of seconds.
 */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressEstimatedTimeRemainingKey NS_AVAILABLE(10_9, 7_0);
+#else
 FOUNDATION_EXPORT NSProgressKey const NSProgressEstimatedTimeRemainingKey NS_AVAILABLE(10_9, 7_0);
+#endif
 
 /* How fast data is being processed, as an NSNumber containing bytes per second.
 */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressThroughputKey NS_AVAILABLE(10_9, 7_0);
+#else
 FOUNDATION_EXPORT NSProgressKey const NSProgressThroughputKey NS_AVAILABLE(10_9, 7_0);
+#endif
 
 #pragma mark *** Details of File Progress ***
 
@@ -238,7 +258,11 @@
 
 /* A user info dictionary key, for an entry that is required when the value for the kind property is NSProgressKindFile. The value must be one of the strings listed in the next section. The default implementations of of -localizedDescription and -localizedItemDescription use this value to determine the text that they return.
 */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressFileOperationKindKey NS_AVAILABLE(10_9, 7_0);
+#else
 FOUNDATION_EXPORT NSProgressKey const NSProgressFileOperationKindKey NS_AVAILABLE(10_9, 7_0);
+#endif
 
 /* Possible values for NSProgressFileOperationKindKey entries.
 */
@@ -249,20 +273,37 @@
 
 /* A user info dictionary key. The value must be an NSURL identifying the item on which progress is being made. This is required for any NSProgress that is published using -publish to be reported to subscribers registered with +addSubscriberForFileURL:withPublishingHandler:.
 */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressFileURLKey NS_AVAILABLE(10_9, 7_0);
+#else
 FOUNDATION_EXPORT NSProgressKey const NSProgressFileURLKey NS_AVAILABLE(10_9, 7_0);
+#endif
 
 /* User info dictionary keys. The values must be NSNumbers containing integers. These entries are optional but if they are both present then the default implementation of -localizedAdditionalDescription uses them to determine the text that it returns.
 */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressFileTotalCountKey NS_AVAILABLE(10_9, 7_0);
+FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressFileCompletedCountKey NS_AVAILABLE(10_9, 7_0);
+#else
 FOUNDATION_EXPORT NSProgressKey const NSProgressFileTotalCountKey NS_AVAILABLE(10_9, 7_0);
 FOUNDATION_EXPORT NSProgressKey const NSProgressFileCompletedCountKey NS_AVAILABLE(10_9, 7_0);
+#endif
 
 /* User info dictionary keys. The value for the first entry must be an NSImage, typically an icon. The value for the second entry must be an NSValue containing an NSRect, in screen coordinates, locating the image where it initially appears on the screen.
 */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressFileAnimationImageKey NS_AVAILABLE(10_9, NA);
+FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressFileAnimationImageOriginalRectKey NS_AVAILABLE(10_9, NA);
+#else
 FOUNDATION_EXPORT NSProgressKey const NSProgressFileAnimationImageKey NS_AVAILABLE(10_9, NA);
 FOUNDATION_EXPORT NSProgressKey const NSProgressFileAnimationImageOriginalRectKey NS_AVAILABLE(10_9, NA);
-
+#endif
 /* A user info dictionary key. The value must be an NSImage containing an icon. This entry is optional but, if it is present, the Finder will use it to show the icon of a file while progress is being made on that file. For example, the App Store uses this to specify an icon for an application being downloaded before the icon can be gotten from the application bundle itself.
 */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+FOUNDATION_EXPORT NSProgressUserInfoKey const NSProgressFileIconKey NS_AVAILABLE(10_9, NA);
+#else
 FOUNDATION_EXPORT NSProgressKey const NSProgressFileIconKey NS_AVAILABLE(10_9, NA);
+#endif
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSRunLoop.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSRunLoop.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSRunLoop.h	2016-05-20 07:35:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSRunLoop.h	2016-06-27 07:21:40.000000000 +0200
@@ -23,8 +23,10 @@
     void	*_reserved[6];
 }
 
-+ (NSRunLoop *)currentRunLoop;
-+ (NSRunLoop *)mainRunLoop NS_AVAILABLE(10_5, 2_0);
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, strong) NSRunLoop *currentRunLoop;
+@property (class, readonly, strong) NSRunLoop *mainRunLoop NS_AVAILABLE(10_5, 2_0);
+#endif
 
 @property (nullable, readonly, copy) NSRunLoopMode currentMode;
 
@@ -50,6 +52,15 @@
 - (void)configureAsServer NS_DEPRECATED(10_0, 10_5, 2_0, 2_0);
 #endif
 
+/// Schedules the execution of a block on the target run loop in given modes.
+/// - parameter: modes   An array of input modes for which the block may be executed.
+/// - parameter: block   The block to execute
+- (void)performInModes:(NSArray<NSRunLoopMode> *)modes block:(void (^)(void))block API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+/// Schedules the execution of a block on the target run loop.
+/// - parameter: block   The block to execute
+- (void)performBlock:(void (^)(void))block API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
 @end
 
 /**************** 	Delayed perform	 ******************/
@@ -71,4 +82,12 @@
 
 @end
 
+
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSRunLoop (NSLegacySwiftCompatability)
++ (NSRunLoop *)currentRunLoop;
++ (NSRunLoop *)mainRunLoop NS_AVAILABLE(10_5, 2_0);
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSStream.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSStream.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSStream.h	2016-05-20 06:24:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSStream.h	2016-06-27 06:06:10.000000000 +0200
@@ -41,8 +41,13 @@
 @property (nullable, assign) id <NSStreamDelegate> delegate;
     // By default, a stream is its own delegate, and subclassers of NSInputStream and NSOutputStream must maintain this contract. [someStream setDelegate:nil] must restore this behavior. As usual, delegates are not retained.
 
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+- (nullable id)propertyForKey:(NSStreamPropertyKey)key;
+- (BOOL)setProperty:(nullable id)property forKey:(NSStreamPropertyKey)key;
+#else
 - (nullable id)propertyForKey:(NSString *)key;
 - (BOOL)setProperty:(nullable id)property forKey:(NSString *)key;
+#endif
 
 - (void)scheduleInRunLoop:(NSRunLoop *)aRunLoop forMode:(NSRunLoopMode)mode;
 - (void)removeFromRunLoop:(NSRunLoop *)aRunLoop forMode:(NSRunLoopMode)mode;
@@ -181,5 +186,6 @@
 FOUNDATION_EXPORT NSStreamNetworkServiceTypeValue const NSStreamNetworkServiceTypeVideo	    NS_AVAILABLE(10_7, 5_0);
 FOUNDATION_EXPORT NSStreamNetworkServiceTypeValue const NSStreamNetworkServiceTypeBackground	    NS_AVAILABLE(10_7, 5_0);
 FOUNDATION_EXPORT NSStreamNetworkServiceTypeValue const NSStreamNetworkServiceTypeVoice	    NS_AVAILABLE(10_7, 5_0);
+FOUNDATION_EXPORT NSStreamNetworkServiceTypeValue const NSStreamNetworkServiceTypeCallSignaling    API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSString.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSString.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSString.h	2016-05-20 06:24:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSString.h	2016-06-27 06:06:56.000000000 +0200
@@ -254,12 +254,16 @@
 - (NSUInteger)maximumLengthOfBytesUsingEncoding:(NSStringEncoding)enc;	// Result in O(1) time; the estimate may be way over what's needed. Returns 0 on error (overflow)
 - (NSUInteger)lengthOfBytesUsingEncoding:(NSStringEncoding)enc;		// Result in O(n) time; the result is exact. Returns 0 on error (cannot convert to specified encoding, or overflow)
 
-+ (const NSStringEncoding *)availableStringEncodings;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly) const NSStringEncoding *availableStringEncodings;
+#endif
 + (NSString *)localizedNameOfStringEncoding:(NSStringEncoding)encoding;
 
 /* User-dependent encoding whose value is derived from user's default language and potentially other factors. The use of this encoding might sometimes be needed when interpreting user documents with unknown encodings, in the absence of other hints.  This encoding should be used rarely, if at all. Note that some potential values here might result in unexpected encoding conversions of even fairly straightforward NSString content --- for instance, punctuation characters with a bidirectional encoding.
  */
-+ (NSStringEncoding)defaultCStringEncoding;	// Should be rarely used
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly) NSStringEncoding defaultCStringEncoding;	// Should be rarely used
+#endif
 
 
 #pragma mark *** Other ***
@@ -460,7 +464,7 @@
 
 @interface NSString (NSStringDeprecated)
 
-/* The following methods are deprecated and will be removed from this header file in the near future. These methods use [NSString defaultCStringEncoding] as the encoding to convert to, which means the results depend on the user's language and potentially other settings. This might be appropriate in some cases, but often these methods are misused, resulting in issues when running in languages other then English. UTF8String in general is a much better choice when converting arbitrary NSStrings into 8-bit representations. Additional potential replacement methods are being introduced in NSString as appropriate.
+/* The following methods are deprecated and will be removed from this header file in the near future. These methods use NSString.defaultCStringEncoding as the encoding to convert to, which means the results depend on the user's language and potentially other settings. This might be appropriate in some cases, but often these methods are misused, resulting in issues when running in languages other then English. UTF8String in general is a much better choice when converting arbitrary NSStrings into 8-bit representations. Additional potential replacement methods are being introduced in NSString as appropriate.
 */
 - (nullable const char *)cString NS_RETURNS_INNER_POINTER NS_DEPRECATED(10_0, 10_4, 2_0, 2_0);
 - (nullable const char *)lossyCString NS_RETURNS_INNER_POINTER NS_DEPRECATED(10_0, 10_4, 2_0, 2_0);
@@ -518,5 +522,11 @@
 extern void *_NSConstantStringClassReference;
 #endif
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSString (NSLegacySwiftCompatability)
++ (const NSStringEncoding *)availableStringEncodings;
++ (NSStringEncoding)defaultCStringEncoding;
+@end
+#endif
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTextCheckingResult.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTextCheckingResult.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTextCheckingResult.h	2016-05-20 06:13:48.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTextCheckingResult.h	2016-06-27 06:06:56.000000000 +0200
@@ -48,7 +48,9 @@
 
 /* Optional properties, used with certain types of results. */
 @property (nullable, readonly, copy) NSOrthography *orthography;
-@property (nullable, readonly, copy) NSArray<NSString *> *grammarDetails;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (nullable, readonly, copy) NSArray<NSDictionary<NSString *, id> *> *grammarDetails;
+#endif
 @property (nullable, readonly, copy) NSDate *date;
 @property (nullable, readonly, copy) NSTimeZone *timeZone;
 @property (readonly) NSTimeInterval duration;
@@ -89,7 +91,9 @@
 /* Methods for creating instances of the various types of results. */
 + (NSTextCheckingResult *)orthographyCheckingResultWithRange:(NSRange)range orthography:(NSOrthography *)orthography;
 + (NSTextCheckingResult *)spellCheckingResultWithRange:(NSRange)range;
-+ (NSTextCheckingResult *)grammarCheckingResultWithRange:(NSRange)range details:(NSArray<NSString *> *)details;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
++ (NSTextCheckingResult *)grammarCheckingResultWithRange:(NSRange)range details:(NSArray<NSDictionary<NSString *, id> *> *)details;
+#endif
 + (NSTextCheckingResult *)dateCheckingResultWithRange:(NSRange)range date:(NSDate *)date;
 + (NSTextCheckingResult *)dateCheckingResultWithRange:(NSRange)range date:(NSDate *)date timeZone:(NSTimeZone *)timeZone duration:(NSTimeInterval)duration;
 + (NSTextCheckingResult *)addressCheckingResultWithRange:(NSRange)range components:(NSDictionary<NSString *, NSString *> *)components;
@@ -105,5 +109,12 @@
 
 @end
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSTextCheckingResult (NSLegacySwiftCompatability)
+@property (nullable, readonly, copy) NSArray<NSString *> *grammarDetails;
++ (NSTextCheckingResult *)grammarCheckingResultWithRange:(NSRange)range details:(NSArray<NSString *> *)details;
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSThread.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSThread.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSThread.h	2016-05-20 07:35:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSThread.h	2016-06-26 17:36:07.000000000 +0200
@@ -16,8 +16,11 @@
     uint8_t _bytes[44];
 }
 
-+ (NSThread *)currentThread;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, strong) NSThread *currentThread;
+#endif
 
++ (void)detachNewThreadWithBlock:(void (^)(void))block API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 + (void)detachNewThreadSelector:(SEL)selector toTarget:(id)target withObject:(nullable id)argument;
 
 + (BOOL)isMultiThreaded;
@@ -36,19 +39,24 @@
 
 @property NSQualityOfService qualityOfService NS_AVAILABLE(10_10, 8_0); // read-only after the thread is started
 
-+ (NSArray<NSNumber *> *)callStackReturnAddresses NS_AVAILABLE(10_5, 2_0);
-+ (NSArray<NSString *> *)callStackSymbols NS_AVAILABLE(10_6, 4_0);
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, copy) NSArray<NSNumber *> *callStackReturnAddresses NS_AVAILABLE(10_5, 2_0);
+@property (class, readonly, copy) NSArray<NSString *> *callStackSymbols NS_AVAILABLE(10_6, 4_0);
+#endif
 
 @property (nullable, copy) NSString *name NS_AVAILABLE(10_5, 2_0);
 
 @property NSUInteger stackSize NS_AVAILABLE(10_5, 2_0);
 
 @property (readonly) BOOL isMainThread NS_AVAILABLE(10_5, 2_0);
-+ (BOOL)isMainThread NS_AVAILABLE(10_5, 2_0); // reports whether current thread is main
-+ (NSThread *)mainThread NS_AVAILABLE(10_5, 2_0);
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly) BOOL isMainThread NS_AVAILABLE(10_5, 2_0); // reports whether current thread is main
+@property (class, readonly, strong) NSThread *mainThread NS_AVAILABLE(10_5, 2_0);
+#endif
 
 - (instancetype)init NS_AVAILABLE(10_5, 2_0) NS_DESIGNATED_INITIALIZER;
 - (instancetype)initWithTarget:(id)target selector:(SEL)selector object:(nullable id)argument NS_AVAILABLE(10_5, 2_0);
+- (instancetype)initWithBlock:(void (^)(void))block API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
 @property (readonly, getter=isExecuting) BOOL executing NS_AVAILABLE(10_5, 2_0);
 @property (readonly, getter=isFinished) BOOL finished NS_AVAILABLE(10_5, 2_0);
@@ -79,4 +87,15 @@
 
 @end
 
+
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSThread (NSLegacySwiftCompatability)
++ (NSThread *)currentThread;
++ (NSArray<NSNumber *> *)callStackReturnAddresses;
++ (NSArray<NSString *> *)callStackSymbols;
++ (BOOL)isMainThread NS_AVAILABLE(10_5, 2_0);
++ (NSThread *)mainThread NS_AVAILABLE(10_5, 2_0);
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTimeZone.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTimeZone.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTimeZone.h	2016-05-20 07:35:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTimeZone.h	2016-06-26 17:36:07.000000000 +0200
@@ -25,20 +25,24 @@
 
 @interface NSTimeZone (NSExtendedTimeZone)
 
-+ (NSTimeZone *)systemTimeZone;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, copy) NSTimeZone *systemTimeZone;
+#endif
 + (void)resetSystemTimeZone;
 
-+ (NSTimeZone *)defaultTimeZone;
-+ (void)setDefaultTimeZone:(NSTimeZone *)aTimeZone;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, copy) NSTimeZone *defaultTimeZone;
 
-+ (NSTimeZone *)localTimeZone;
+@property (class, readonly, copy) NSTimeZone *localTimeZone;
 
-+ (NSArray<NSString *> *)knownTimeZoneNames;
+@property (class, readonly, copy) NSArray<NSString *> *knownTimeZoneNames;
+
+@property (class, copy) NSDictionary<NSString *, NSString *> *abbreviationDictionary NS_AVAILABLE(10_6, 4_0);
 
 + (NSDictionary<NSString *, NSString *> *)abbreviationDictionary;
-+ (void)setAbbreviationDictionary:(NSDictionary<NSString *, NSString *> *)dict NS_AVAILABLE(10_6, 4_0);
 
-+ (NSString *)timeZoneDataVersion NS_AVAILABLE(10_6, 4_0);
+@property (class, readonly, copy) NSString *timeZoneDataVersion NS_AVAILABLE(10_6, 4_0);
+#endif
 
 @property (readonly) NSInteger secondsFromGMT;
 @property (nullable, readonly, copy) NSString *abbreviation;
@@ -85,4 +89,17 @@
 
 FOUNDATION_EXPORT NSNotificationName const NSSystemTimeZoneDidChangeNotification NS_AVAILABLE(10_5, 2_0);
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSTimeZone (NSLegacySwiftCompatability)
++ (NSTimeZone *)systemTimeZone;
++ (NSTimeZone *)defaultTimeZone;
++ (void)setDefaultTimeZone:(NSTimeZone *)timeZone;
++ (NSTimeZone *)localTimeZone;
++ (NSArray<NSString *> *)knownTimeZoneNames;
++ (void)setAbbreviationDictionary:(NSDictionary<NSString *, NSString *> *)dictionary NS_AVAILABLE(10_6, 4_0);
++ (NSDictionary<NSString *, NSString *> *)abbreviationDictionary;
++ (NSString *)timeZoneDataVersion NS_AVAILABLE(10_6, 4_0);
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTimer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTimer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTimer.h	2016-05-20 07:35:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTimer.h	2016-06-27 06:02:14.000000000 +0200
@@ -1,5 +1,5 @@
 /*	NSTimer.h
-	Copyright (c) 1994-2015, Apple Inc. All rights reserved.
+	Copyright (c) 1994-2016, Apple Inc. All rights reserved.
 */
 
 #import <Foundation/NSObject.h>
@@ -15,6 +15,26 @@
 + (NSTimer *)timerWithTimeInterval:(NSTimeInterval)ti target:(id)aTarget selector:(SEL)aSelector userInfo:(nullable id)userInfo repeats:(BOOL)yesOrNo;
 + (NSTimer *)scheduledTimerWithTimeInterval:(NSTimeInterval)ti target:(id)aTarget selector:(SEL)aSelector userInfo:(nullable id)userInfo repeats:(BOOL)yesOrNo;
 
+
+/// Creates and returns a new NSTimer object initialized with the specified block object.
+/// - parameter:  timeInterval  The number of seconds between firings of the timer. If seconds is less than or equal to 0.0, this method chooses the nonnegative value of 0.1 milliseconds instead
+/// - parameter:  repeats  If YES, the timer will repeatedly reschedule itself until invalidated. If NO, the timer will be invalidated after it fires.
+/// - parameter:  block  The execution body of the timer; the timer itself is passed as the parameter to this block when executed to aid in avoiding cyclical references
++ (NSTimer *)timerWithTimeInterval:(NSTimeInterval)interval repeats:(BOOL)repeats block:(void (^)(NSTimer *timer))block API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+/// Creates and returns a new NSTimer object initialized with the specified block object and schedules it on the current run loop in the default mode.
+/// - parameter:  ti    The number of seconds between firings of the timer. If seconds is less than or equal to 0.0, this method chooses the nonnegative value of 0.1 milliseconds instead
+/// - parameter:  repeats  If YES, the timer will repeatedly reschedule itself until invalidated. If NO, the timer will be invalidated after it fires.
+/// - parameter:  block  The execution body of the timer; the timer itself is passed as the parameter to this block when executed to aid in avoiding cyclical references
++ (NSTimer *)scheduledTimerWithTimeInterval:(NSTimeInterval)interval repeats:(BOOL)repeats block:(void (^)(NSTimer *timer))block API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+/// Initializes a new NSTimer object using the block as the main body of execution for the timer.
+/// - parameter:  fireDate   The time at which the timer should first fire.
+/// - parameter:  interval  The number of seconds between firings of the timer. If seconds is less than or equal to 0.0, this method chooses the nonnegative value of 0.1 milliseconds instead
+/// - parameter:  repeats  If YES, the timer will repeatedly reschedule itself until invalidated. If NO, the timer will be invalidated after it fires.
+/// - parameter:  block  The execution body of the timer; the timer itself is passed as the parameter to this block when executed to aid in avoiding cyclical references
+- (instancetype)initWithFireDate:(NSDate *)date interval:(NSTimeInterval)interval repeats:(BOOL)repeats block:(void (^)(NSTimer *timer))block API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
 - (instancetype)initWithFireDate:(NSDate *)date interval:(NSTimeInterval)ti target:(id)t selector:(SEL)s userInfo:(nullable id)ui repeats:(BOOL)rep NS_DESIGNATED_INITIALIZER;
 
 - (void)fire;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURL.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURL.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURL.h	2016-05-20 06:24:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURL.h	2016-06-26 17:36:07.000000000 +0200
@@ -1,5 +1,5 @@
 /*	NSURL.h
-	Copyright (c) 1997-2015, Apple Inc. All rights reserved.
+	Copyright (c) 1997-2016, Apple Inc. All rights reserved.
 */
 
 #import <Foundation/NSObject.h>
@@ -515,27 +515,27 @@
 
 
 @interface NSCharacterSet (NSURLUtilities)
-
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
 // Predefined character sets for the six URL components and subcomponents which allow percent encoding. These character sets are passed to -stringByAddingPercentEncodingWithAllowedCharacters:.
 
 // Returns a character set containing the characters allowed in an URL's user subcomponent.
-+ (NSCharacterSet *)URLUserAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
+@property (class, readonly, copy) NSCharacterSet *URLUserAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
 
 // Returns a character set containing the characters allowed in an URL's password subcomponent.
-+ (NSCharacterSet *)URLPasswordAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
+@property (class, readonly, copy) NSCharacterSet *URLPasswordAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
 
 // Returns a character set containing the characters allowed in an URL's host subcomponent.
-+ (NSCharacterSet *)URLHostAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
+@property (class, readonly, copy) NSCharacterSet *URLHostAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
 
 // Returns a character set containing the characters allowed in an URL's path component. ';' is a legal path character, but it is recommended that it be percent-encoded for best compatibility with NSURL (-stringByAddingPercentEncodingWithAllowedCharacters: will percent-encode any ';' characters if you pass the URLPathAllowedCharacterSet).
-+ (NSCharacterSet *)URLPathAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
+@property (class, readonly, copy) NSCharacterSet *URLPathAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
 
 // Returns a character set containing the characters allowed in an URL's query component.
-+ (NSCharacterSet *)URLQueryAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
+@property (class, readonly, copy) NSCharacterSet *URLQueryAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
 
 // Returns a character set containing the characters allowed in an URL's fragment component.
-+ (NSCharacterSet *)URLFragmentAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
-
+@property (class, readonly, copy) NSCharacterSet *URLFragmentAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
+#endif
 @end
 
 
@@ -626,4 +626,15 @@
 @end
 #endif
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSCharacterSet (NSLegacySwiftCompatability)
++ (NSCharacterSet *)URLUserAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
++ (NSCharacterSet *)URLPasswordAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
++ (NSCharacterSet *)URLHostAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
++ (NSCharacterSet *)URLPathAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
++ (NSCharacterSet *)URLQueryAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
++ (NSCharacterSet *)URLFragmentAllowedCharacterSet NS_AVAILABLE(10_9, 7_0);
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCache.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCache.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCache.h	2016-05-20 07:24:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCache.h	2016-06-27 07:21:40.000000000 +0200
@@ -125,8 +125,11 @@
 }
 
 /*! 
-    @method sharedURLCache
-    @abstract Returns the shared NSURLCache instance.
+    @property sharedURLCache
+    @abstract Returns the shared NSURLCache instance or
+    sets the NSURLCache instance shared by all clients of
+    the current process. This will be the new object returned when
+    calls to the <tt>sharedURLCache</tt> method are made.
     @discussion Unless set explicitly through a call to
     <tt>+setSharedURLCache:</tt>, this method returns an NSURLCache
     instance created with the following default values:
@@ -139,23 +142,16 @@
     constraints should find the default shared cache instance
     acceptable. If this default shared cache instance is not
     acceptable, <tt>+setSharedURLCache:</tt> can be called to set a
-    different NSURLCache instance to be returned from this method.
+    different NSURLCache instance to be returned from this method. 
+    Callers should take care to ensure that the setter is called
+    at a time when no other caller has a reference to the previously-set 
+    shared URL cache. This is to prevent storing cache data from 
+    becoming unexpectedly unretrievable.
     @result the shared NSURLCache instance.
 */
-+ (NSURLCache *)sharedURLCache;
-
-/*! 
-    @method setSharedURLCache:
-    @abstract Sets the NSURLCache instance shared by all clients of
-    the current process. This will be the new object returned when
-    calls to the <tt>sharedURLCache</tt> method are made.
-    @discussion Callers should take care to ensure that this method is called
-    at a time when no other caller has a reference to the previously-set shared
-    URL cache. This is to prevent storing cache data from becoming 
-    unexpectedly unretrievable.
-    @param cache the new shared NSURLCache instance.
-*/
-+ (void)setSharedURLCache:(NSURLCache *)cache;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, strong) NSURLCache *sharedURLCache;
+#endif
 
 /*! 
     @method initWithMemoryCapacity:diskCapacity:diskPath:
@@ -261,4 +257,10 @@
 - (void)removeCachedResponseForDataTask:(NSURLSessionDataTask *)dataTask NS_AVAILABLE(10_10, 8_0);
 @end
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSURLCache (NSLegacySwiftCompatability)
++ (NSURLCache *)sharedURLCache;
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCredentialStorage.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCredentialStorage.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCredentialStorage.h	2016-05-20 06:24:14.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCredentialStorage.h	2016-06-27 07:21:40.000000000 +0200
@@ -30,11 +30,13 @@
 }
 
 /*!
-    @method sharedCredentialStorage
+    @property sharedCredentialStorage
     @abstract Get the shared singleton authentication storage
     @result the shared authentication storage
 */
-+ (NSURLCredentialStorage *)sharedCredentialStorage;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, strong) NSURLCredentialStorage *sharedCredentialStorage;
+#endif
 
 /*!
     @method credentialsForProtectionSpace:
@@ -129,5 +131,11 @@
  */
 FOUNDATION_EXPORT NSString *const NSURLCredentialStorageRemoveSynchronizableCredentials NS_AVAILABLE(10_9, 7_0);
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSURLCredentialStorage (NSLegacySwiftCompatability)
++ (NSURLCredentialStorage *)sharedCredentialStorage;
+@end
+#endif
+
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLRequest.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLRequest.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLRequest.h	2016-05-04 00:21:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLRequest.h	2016-06-26 17:36:07.000000000 +0200
@@ -130,6 +130,7 @@
 
  @constant NSURLNetworkServiceTypeVoice Specifies that the request is for voice data.
 
+ @constant NSURLNetworkServiceTypeCallSignaling Specifies that the request is for call signaling.
 */
 typedef NS_ENUM(NSUInteger, NSURLRequestNetworkServiceType)
 {
@@ -137,7 +138,8 @@
     NSURLNetworkServiceTypeVoIP = 1,	// Voice over IP control traffic
     NSURLNetworkServiceTypeVideo = 2,	// Video traffic
     NSURLNetworkServiceTypeBackground = 3, // Background traffic
-    NSURLNetworkServiceTypeVoice = 4	   // Voice data
+    NSURLNetworkServiceTypeVoice = 4,	   // Voice data
+    NSURLNetworkServiceTypeCallSignaling API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = 11, // Call Signaling
 };
 
 
@@ -190,13 +192,16 @@
 */
 + (instancetype)requestWithURL:(NSURL *)URL;
 
-/*
-    @method supportsSecureCoding
+/*!
+    @property supportsSecureCoding
     @abstract Indicates that NSURLRequest implements the NSSecureCoding protocol.
     @result A BOOL value set to YES.
 */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly) BOOL supportsSecureCoding;
+#else
 + (BOOL)supportsSecureCoding;
-
+#endif
 /*!
     @method requestWithURL:cachePolicy:timeoutInterval:
     @abstract Allocates and initializes a NSURLRequest with the given
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLSession.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLSession.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLSession.h	2016-05-20 07:39:55.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLSession.h	2016-06-26 17:36:07.000000000 +0200
@@ -125,7 +125,9 @@
  * The shared session uses the currently set global NSURLCache,
  * NSHTTPCookieStorage and NSURLCredentialStorage objects.
  */
-+ (NSURLSession *)sharedSession;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, strong) NSURLSession *sharedSession;
+#endif
 
 /*
  * Customization of NSURLSession occurs during creation of a new session.
@@ -478,8 +480,11 @@
 NS_CLASS_AVAILABLE(NSURLSESSION_AVAILABLE, 7_0)
 @interface NSURLSessionConfiguration : NSObject <NSCopying>
 
-+ (NSURLSessionConfiguration *)defaultSessionConfiguration;
-+ (NSURLSessionConfiguration *)ephemeralSessionConfiguration;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, strong) NSURLSessionConfiguration *defaultSessionConfiguration;
+@property (class, readonly, strong) NSURLSessionConfiguration *ephemeralSessionConfiguration;
+#endif
+
 + (NSURLSessionConfiguration *)backgroundSessionConfigurationWithIdentifier:(NSString *)identifier NS_AVAILABLE(10_10, 8_0);
 
 /* identifier for the background session configuration */
@@ -994,4 +999,15 @@
 
 @end
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSURLSession (NSLegacySwiftCompatability)
++ (NSURLSession *)sharedSession;
+@end
+
+@interface NSURLSessionConfiguration (NSLegacySwiftCompatability)
++ (NSURLSessionConfiguration *)defaultSessionConfiguration;
++ (NSURLSessionConfiguration *)ephemeralSessionConfiguration;
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUnit.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUnit.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUnit.h	2016-05-20 06:12:55.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUnit.h	2016-06-27 06:00:18.000000000 +0200
@@ -148,8 +148,6 @@
 @property (class, readonly, copy) NSUnitAngle *gradians;
 @property (class, readonly, copy) NSUnitAngle *revolutions;
 
-@property (class, readonly, copy) NSUnitAngle *degree API_DEPRECATED("No longer supported - use degrees instead", macosx(10.12, 10.12), ios(10.0, 10.0), watchos(3.0, 3.0), tvos(10.0, 10.0));
-
 @end
 
 API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
@@ -198,7 +196,7 @@
 @end
 
 API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
-@interface NSUnitDuration : NSDimension <NSSecureCoding>
+@interface NSUnitDuration : NSDimension <NSSecureCoding>  // Note: This class is not meant to be used for date calculation.  Use NSDate/NSCalendar/NSDateComponents for calendrical date and time operations.
 /*
  Base unit - seconds
  */
@@ -338,9 +336,6 @@
 @property (class, readonly, copy) NSUnitLength *astronomicalUnits;
 @property (class, readonly, copy) NSUnitLength *parsecs;
 
-@property (class, readonly, copy) NSUnitLength *meter API_DEPRECATED("No longer supported - use meters instead", macosx(10.12, 10.12), ios(10.0, 10.0), watchos(3.0, 3.0), tvos(10.0, 10.0));
-@property (class, readonly, copy) NSUnitLength *foot API_DEPRECATED("No longer supported - use feet instead", macosx(10.12, 10.12), ios(10.0, 10.0), watchos(3.0, 3.0), tvos(10.0, 10.0));
-
 @end
 
 API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserDefaults.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserDefaults.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserDefaults.h	2016-05-20 06:13:48.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserDefaults.h	2016-06-27 06:06:56.000000000 +0200
@@ -57,7 +57,9 @@
 /*!
  +standardUserDefaults returns a global instance of NSUserDefaults configured to search the current application's search list.
  */
-+ (NSUserDefaults *)standardUserDefaults;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 8)
+@property (class, readonly, strong) NSUserDefaults *standardUserDefaults;
+#endif
 
 /// +resetStandardUserDefaults releases the standardUserDefaults and sets it to nil. A new standardUserDefaults will be created the next time it's accessed. The only visible effect this has is that all KVO observers of the previous standardUserDefaults will no longer be observing it.
 + (void)resetStandardUserDefaults;
@@ -240,4 +242,10 @@
 FOUNDATION_EXPORT NSString * const NSNegativeCurrencyFormatString NS_DEPRECATED(10_0, 10_5, NA, NA);
 #endif
 
+#if defined(SWIFT_CLASS_EXTRA) && (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH < 8)
+@interface NSUserDefaults (NSLegacySwiftCompatability)
++ (NSUserDefaults *)standardUserDefaults;
+@end
+#endif
+
 NS_ASSUME_NONNULL_END
```