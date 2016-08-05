#Foundation.framework

``` diff
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
```