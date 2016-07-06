#Foundation.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/Foundation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/Foundation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/Foundation.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/Foundation.h	2016-05-20 07:24:14.000000000 +0200
@@ -16,11 +16,15 @@
 #import <Foundation/NSCoder.h>
 #import <Foundation/NSData.h>
 #import <Foundation/NSDate.h>
+#import <Foundation/NSDateInterval.h>
 #import <Foundation/NSDateFormatter.h>
 #import <Foundation/NSDateIntervalFormatter.h>
+#import <Foundation/NSISO8601DateFormatter.h>
 #import <Foundation/NSMassFormatter.h>
 #import <Foundation/NSLengthFormatter.h>
 #import <Foundation/NSEnergyFormatter.h>
+#import <Foundation/NSMeasurement.h>
+#import <Foundation/NSMeasurementFormatter.h>
 #import <Foundation/NSPersonNameComponents.h>
 #import <Foundation/NSPersonNameComponentsFormatter.h>
 #import <Foundation/NSDecimal.h>
@@ -73,6 +77,7 @@
 #import <Foundation/NSThread.h>
 #import <Foundation/NSTimeZone.h>
 #import <Foundation/NSTimer.h>
+#import <Foundation/NSUnit.h>
 #import <Foundation/NSURL.h>
 #import <Foundation/NSURLAuthenticationChallenge.h>
 #import <Foundation/NSURLCache.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSArray.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSArray.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSArray.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSArray.h	2016-05-20 07:39:55.000000000 +0200
@@ -18,7 +18,7 @@
 @property (readonly) NSUInteger count;
 - (ObjectType)objectAtIndex:(NSUInteger)index;
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
-- (instancetype)initWithObjects:(const ObjectType [])objects count:(NSUInteger)cnt NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithObjects:(const ObjectType _Nonnull [_Nullable])objects count:(NSUInteger)cnt NS_DESIGNATED_INITIALIZER;
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
 
 @end
@@ -33,7 +33,7 @@
 - (NSString *)descriptionWithLocale:(nullable id)locale;
 - (NSString *)descriptionWithLocale:(nullable id)locale indent:(NSUInteger)level;
 - (nullable ObjectType)firstObjectCommonWithArray:(NSArray<ObjectType> *)otherArray;
-- (void)getObjects:(ObjectType __unsafe_unretained [])objects range:(NSRange)range;
+- (void)getObjects:(ObjectType __unsafe_unretained [])objects range:(NSRange)range NS_SWIFT_UNAVAILABLE("Use 'subarrayWithRange()' instead");
 - (NSUInteger)indexOfObject:(ObjectType)anObject;
 - (NSUInteger)indexOfObject:(ObjectType)anObject inRange:(NSRange)range;
 - (NSUInteger)indexOfObjectIdenticalTo:(ObjectType)anObject;
@@ -44,8 +44,8 @@
 - (NSEnumerator<ObjectType> *)objectEnumerator;
 - (NSEnumerator<ObjectType> *)reverseObjectEnumerator;
 @property (readonly, copy) NSData *sortedArrayHint;
-- (NSArray<ObjectType> *)sortedArrayUsingFunction:(NSInteger (*)(ObjectType, ObjectType, void * __nullable))comparator context:(nullable void *)context;
-- (NSArray<ObjectType> *)sortedArrayUsingFunction:(NSInteger (*)(ObjectType, ObjectType, void * __nullable))comparator context:(nullable void *)context hint:(nullable NSData *)hint;
+- (NSArray<ObjectType> *)sortedArrayUsingFunction:(NSInteger (NS_NOESCAPE *)(ObjectType, ObjectType, void * _Nullable))comparator context:(nullable void *)context;
+- (NSArray<ObjectType> *)sortedArrayUsingFunction:(NSInteger (NS_NOESCAPE *)(ObjectType, ObjectType, void * _Nullable))comparator context:(nullable void *)context hint:(nullable NSData *)hint;
 - (NSArray<ObjectType> *)sortedArrayUsingSelector:(SEL)comparator;
 - (NSArray<ObjectType> *)subarrayWithRange:(NSRange)range;
 - (BOOL)writeToFile:(NSString *)path atomically:(BOOL)useAuxiliaryFile;
@@ -58,20 +58,20 @@
 
 - (ObjectType)objectAtIndexedSubscript:(NSUInteger)idx NS_AVAILABLE(10_8, 6_0);
 
-- (void)enumerateObjectsUsingBlock:(void (^)(ObjectType obj, NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
-- (void)enumerateObjectsWithOptions:(NSEnumerationOptions)opts usingBlock:(void (^)(ObjectType obj, NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
-- (void)enumerateObjectsAtIndexes:(NSIndexSet *)s options:(NSEnumerationOptions)opts usingBlock:(void (^)(ObjectType obj, NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
-
-- (NSUInteger)indexOfObjectPassingTest:(BOOL (^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
-- (NSUInteger)indexOfObjectWithOptions:(NSEnumerationOptions)opts passingTest:(BOOL (^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
-- (NSUInteger)indexOfObjectAtIndexes:(NSIndexSet *)s options:(NSEnumerationOptions)opts passingTest:(BOOL (^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
-
-- (NSIndexSet *)indexesOfObjectsPassingTest:(BOOL (^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
-- (NSIndexSet *)indexesOfObjectsWithOptions:(NSEnumerationOptions)opts passingTest:(BOOL (^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
-- (NSIndexSet *)indexesOfObjectsAtIndexes:(NSIndexSet *)s options:(NSEnumerationOptions)opts passingTest:(BOOL (^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
+- (void)enumerateObjectsUsingBlock:(void (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
+- (void)enumerateObjectsWithOptions:(NSEnumerationOptions)opts usingBlock:(void (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
+- (void)enumerateObjectsAtIndexes:(NSIndexSet *)s options:(NSEnumerationOptions)opts usingBlock:(void (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
+
+- (NSUInteger)indexOfObjectPassingTest:(BOOL (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
+- (NSUInteger)indexOfObjectWithOptions:(NSEnumerationOptions)opts passingTest:(BOOL (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
+- (NSUInteger)indexOfObjectAtIndexes:(NSIndexSet *)s options:(NSEnumerationOptions)opts passingTest:(BOOL (NS_NOESCAPE^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
+
+- (NSIndexSet *)indexesOfObjectsPassingTest:(BOOL (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
+- (NSIndexSet *)indexesOfObjectsWithOptions:(NSEnumerationOptions)opts passingTest:(BOOL (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
+- (NSIndexSet *)indexesOfObjectsAtIndexes:(NSIndexSet *)s options:(NSEnumerationOptions)opts passingTest:(BOOL (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
 
-- (NSArray<ObjectType> *)sortedArrayUsingComparator:(NSComparator)cmptr NS_AVAILABLE(10_6, 4_0);
-- (NSArray<ObjectType> *)sortedArrayWithOptions:(NSSortOptions)opts usingComparator:(NSComparator)cmptr NS_AVAILABLE(10_6, 4_0);
+- (NSArray<ObjectType> *)sortedArrayUsingComparator:(NSComparator NS_NOESCAPE)cmptr NS_AVAILABLE(10_6, 4_0);
+- (NSArray<ObjectType> *)sortedArrayWithOptions:(NSSortOptions)opts usingComparator:(NSComparator NS_NOESCAPE)cmptr NS_AVAILABLE(10_6, 4_0);
 
 typedef NS_OPTIONS(NSUInteger, NSBinarySearchingOptions) {
 	NSBinarySearchingFirstEqual = (1UL << 8),
@@ -79,7 +79,7 @@
 	NSBinarySearchingInsertionIndex = (1UL << 10),
 };
 
-- (NSUInteger)indexOfObject:(ObjectType)obj inSortedRange:(NSRange)r options:(NSBinarySearchingOptions)opts usingComparator:(NSComparator)cmp NS_AVAILABLE(10_6, 4_0); // binary search
+- (NSUInteger)indexOfObject:(ObjectType)obj inSortedRange:(NSRange)r options:(NSBinarySearchingOptions)opts usingComparator:(NSComparator NS_NOESCAPE)cmp NS_AVAILABLE(10_6, 4_0); // binary search
 
 @end
 
@@ -106,7 +106,7 @@
 
 /* This method is unsafe because it could potentially cause buffer overruns. You should use -getObjects:range: instead.
 */
-- (void)getObjects:(ObjectType __unsafe_unretained [])objects;
+- (void)getObjects:(ObjectType __unsafe_unretained [])objects NS_SWIFT_UNAVAILABLE("Use 'as [AnyObject]' instead");
 
 @end
 
@@ -140,7 +140,7 @@
 - (void)replaceObjectsInRange:(NSRange)range withObjectsFromArray:(NSArray<ObjectType> *)otherArray range:(NSRange)otherRange;
 - (void)replaceObjectsInRange:(NSRange)range withObjectsFromArray:(NSArray<ObjectType> *)otherArray;
 - (void)setArray:(NSArray<ObjectType> *)otherArray;
-- (void)sortUsingFunction:(NSInteger (*)(ObjectType,  ObjectType, void * __nullable))compare context:(nullable void *)context;
+- (void)sortUsingFunction:(NSInteger (NS_NOESCAPE *)(ObjectType,  ObjectType, void * _Nullable))compare context:(nullable void *)context;
 - (void)sortUsingSelector:(SEL)comparator;
 
 - (void)insertObjects:(NSArray<ObjectType> *)objects atIndexes:(NSIndexSet *)indexes;
@@ -149,8 +149,8 @@
 
 - (void)setObject:(ObjectType)obj atIndexedSubscript:(NSUInteger)idx NS_AVAILABLE(10_8, 6_0);
 
-- (void)sortUsingComparator:(NSComparator)cmptr NS_AVAILABLE(10_6, 4_0);
-- (void)sortWithOptions:(NSSortOptions)opts usingComparator:(NSComparator)cmptr NS_AVAILABLE(10_6, 4_0);
+- (void)sortUsingComparator:(NSComparator NS_NOESCAPE)cmptr NS_AVAILABLE(10_6, 4_0);
+- (void)sortWithOptions:(NSSortOptions)opts usingComparator:(NSComparator NS_NOESCAPE)cmptr NS_AVAILABLE(10_6, 4_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSAttributedString.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSAttributedString.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSAttributedString.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSAttributedString.h	2016-05-20 06:24:14.000000000 +0200
@@ -36,8 +36,8 @@
   NSAttributedStringEnumerationLongestEffectiveRangeNotRequired = (1UL << 20)
 };
 
-- (void)enumerateAttributesInRange:(NSRange)enumerationRange options:(NSAttributedStringEnumerationOptions)opts usingBlock:(void (^)(NSDictionary<NSString *, id> *attrs, NSRange range, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
-- (void)enumerateAttribute:(NSString *)attrName inRange:(NSRange)enumerationRange options:(NSAttributedStringEnumerationOptions)opts usingBlock:(void (^)(id __nullable value, NSRange range, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
+- (void)enumerateAttributesInRange:(NSRange)enumerationRange options:(NSAttributedStringEnumerationOptions)opts usingBlock:(void (NS_NOESCAPE ^)(NSDictionary<NSString *, id> *attrs, NSRange range, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
+- (void)enumerateAttribute:(NSString *)attrName inRange:(NSRange)enumerationRange options:(NSAttributedStringEnumerationOptions)opts usingBlock:(void (NS_NOESCAPE ^)(id _Nullable value, NSRange range, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSBundle.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSBundle.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSBundle.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSBundle.h	2016-05-20 06:25:32.000000000 +0200
@@ -8,6 +8,7 @@
 #import <Foundation/NSDictionary.h>
 #import <Foundation/NSSet.h>
 #import <Foundation/NSProgress.h>
+#import <Foundation/NSNotification.h>
 
 @class NSString, NSURL, NSError, NSUUID, NSLock, NSNumber;
 
@@ -143,7 +144,7 @@
 
 @end
 
-FOUNDATION_EXPORT NSString * const NSBundleDidLoadNotification;
+FOUNDATION_EXPORT NSNotificationName const NSBundleDidLoadNotification;
 FOUNDATION_EXPORT NSString * const NSLoadedClasses;	// notification key
 
 
@@ -199,7 +200,7 @@
  
  If you want to access the resources again, create a new NSBundleResourceRequest object.
  */
-- (void)beginAccessingResourcesWithCompletionHandler:(void (^)(NSError * __nullable error))completionHandler;
+- (void)beginAccessingResourcesWithCompletionHandler:(void (^)(NSError * _Nullable error))completionHandler;
 
 /*
  Inform the system that you wish to begin accessing the resources that are part of this request, but do not attempt to download any content over the network. The completion handler will be invoked with a YES argument if the resources are available.
@@ -240,7 +241,7 @@
  
  Note that this notification may not be the same as low disk space on the system, as applications can have a smaller quota.
  */
-FOUNDATION_EXPORT NSString * const NSBundleResourceRequestLowDiskSpaceNotification NS_AVAILABLE(NA, 9_0);
+FOUNDATION_EXPORT NSNotificationName const NSBundleResourceRequestLowDiskSpaceNotification NS_AVAILABLE(NA, 9_0);
 
 /* Use this value for the loadingPriority property if the user is doing nothing but waiting on the result of this request. The system will dedicate the maximum amount of resources available to finishing this request as soon as possible.
  */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCalendar.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCalendar.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCalendar.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCalendar.h	2016-05-20 07:35:40.000000000 +0200
@@ -5,6 +5,7 @@
 #import <Foundation/NSObject.h>
 #import <Foundation/NSRange.h>
 #import <Foundation/NSDate.h>
+#import <Foundation/NSNotification.h>
 #include <CoreFoundation/CFCalendar.h>
 
 @class NSDateComponents, NSLocale, NSTimeZone, NSString, NSArray<ObjectType>;
@@ -17,24 +18,26 @@
 #define NS_CALENDAR_DEPRECATED_MAC(A, B, ...) NS_DEPRECATED_MAC(A, B, __VA_ARGS__)
 #endif
 
-FOUNDATION_EXPORT NSString * const NSCalendarIdentifierGregorian  NS_AVAILABLE(10_6, 4_0); // the common calendar in Europe, the Western Hemisphere, and elsewhere
-FOUNDATION_EXPORT NSString * const NSCalendarIdentifierBuddhist            NS_AVAILABLE(10_6, 4_0);
-FOUNDATION_EXPORT NSString * const NSCalendarIdentifierChinese             NS_AVAILABLE(10_6, 4_0);
-FOUNDATION_EXPORT NSString * const NSCalendarIdentifierCoptic              NS_AVAILABLE(10_6, 4_0);
-FOUNDATION_EXPORT NSString * const NSCalendarIdentifierEthiopicAmeteMihret NS_AVAILABLE(10_6, 4_0);
-FOUNDATION_EXPORT NSString * const NSCalendarIdentifierEthiopicAmeteAlem   NS_AVAILABLE(10_6, 4_0);
-FOUNDATION_EXPORT NSString * const NSCalendarIdentifierHebrew              NS_AVAILABLE(10_6, 4_0);
-FOUNDATION_EXPORT NSString * const NSCalendarIdentifierISO8601             NS_AVAILABLE(10_6, 4_0);
-FOUNDATION_EXPORT NSString * const NSCalendarIdentifierIndian              NS_AVAILABLE(10_6, 4_0);
-FOUNDATION_EXPORT NSString * const NSCalendarIdentifierIslamic             NS_AVAILABLE(10_6, 4_0);
-FOUNDATION_EXPORT NSString * const NSCalendarIdentifierIslamicCivil        NS_AVAILABLE(10_6, 4_0);
-FOUNDATION_EXPORT NSString * const NSCalendarIdentifierJapanese            NS_AVAILABLE(10_6, 4_0);
-FOUNDATION_EXPORT NSString * const NSCalendarIdentifierPersian             NS_AVAILABLE(10_6, 4_0);
-FOUNDATION_EXPORT NSString * const NSCalendarIdentifierRepublicOfChina     NS_AVAILABLE(10_6, 4_0);
+typedef NSString * NSCalendarIdentifier NS_EXTENSIBLE_STRING_ENUM;
+
+FOUNDATION_EXPORT NSCalendarIdentifier const NSCalendarIdentifierGregorian  NS_AVAILABLE(10_6, 4_0); // the common calendar in Europe, the Western Hemisphere, and elsewhere
+FOUNDATION_EXPORT NSCalendarIdentifier const NSCalendarIdentifierBuddhist            NS_AVAILABLE(10_6, 4_0);
+FOUNDATION_EXPORT NSCalendarIdentifier const NSCalendarIdentifierChinese             NS_AVAILABLE(10_6, 4_0);
+FOUNDATION_EXPORT NSCalendarIdentifier const NSCalendarIdentifierCoptic              NS_AVAILABLE(10_6, 4_0);
+FOUNDATION_EXPORT NSCalendarIdentifier const NSCalendarIdentifierEthiopicAmeteMihret NS_AVAILABLE(10_6, 4_0);
+FOUNDATION_EXPORT NSCalendarIdentifier const NSCalendarIdentifierEthiopicAmeteAlem   NS_AVAILABLE(10_6, 4_0);
+FOUNDATION_EXPORT NSCalendarIdentifier const NSCalendarIdentifierHebrew              NS_AVAILABLE(10_6, 4_0);
+FOUNDATION_EXPORT NSCalendarIdentifier const NSCalendarIdentifierISO8601             NS_AVAILABLE(10_6, 4_0);
+FOUNDATION_EXPORT NSCalendarIdentifier const NSCalendarIdentifierIndian              NS_AVAILABLE(10_6, 4_0);
+FOUNDATION_EXPORT NSCalendarIdentifier const NSCalendarIdentifierIslamic             NS_AVAILABLE(10_6, 4_0);
+FOUNDATION_EXPORT NSCalendarIdentifier const NSCalendarIdentifierIslamicCivil        NS_AVAILABLE(10_6, 4_0);
+FOUNDATION_EXPORT NSCalendarIdentifier const NSCalendarIdentifierJapanese            NS_AVAILABLE(10_6, 4_0);
+FOUNDATION_EXPORT NSCalendarIdentifier const NSCalendarIdentifierPersian             NS_AVAILABLE(10_6, 4_0);
+FOUNDATION_EXPORT NSCalendarIdentifier const NSCalendarIdentifierRepublicOfChina     NS_AVAILABLE(10_6, 4_0);
 // A simple tabular Islamic calendar using the astronomical/Thursday epoch of CE 622 July 15
-FOUNDATION_EXPORT NSString * const NSCalendarIdentifierIslamicTabular      NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXPORT NSCalendarIdentifier const NSCalendarIdentifierIslamicTabular      NS_AVAILABLE(10_10, 8_0);
 // The Islamic Umm al-Qura calendar used in Saudi Arabia. This is based on astronomical calculation, instead of tabular behavior.
-FOUNDATION_EXPORT NSString * const NSCalendarIdentifierIslamicUmmAlQura    NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXPORT NSCalendarIdentifier const NSCalendarIdentifierIslamicUmmAlQura    NS_AVAILABLE(10_10, 8_0);
 
 
 typedef NS_OPTIONS(NSUInteger, NSCalendarUnit) {
@@ -102,13 +105,13 @@
 	This method returns a new autoreleased calendar object of the given type, specified by a calendar identifier constant.
 	The calendar defaults to having the current locale and default time zone, for those properties.
 */
-+ (nullable NSCalendar *)calendarWithIdentifier:(NSString *)calendarIdentifierConstant NS_AVAILABLE(10_9, 8_0);
++ (nullable NSCalendar *)calendarWithIdentifier:(NSCalendarIdentifier)calendarIdentifierConstant NS_AVAILABLE(10_9, 8_0);
 
 - (instancetype)init NS_UNAVAILABLE;
 
-- (nullable id)initWithCalendarIdentifier:(NSString *)ident NS_DESIGNATED_INITIALIZER;
+- (nullable id)initWithCalendarIdentifier:(NSCalendarIdentifier)ident NS_DESIGNATED_INITIALIZER;
 
-@property (readonly, copy) NSString *calendarIdentifier;
+@property (readonly, copy) NSCalendarIdentifier calendarIdentifier;
 @property (nullable, copy) NSLocale *locale;
 @property (copy) NSTimeZone *timeZone;
 @property NSUInteger firstWeekday;
@@ -150,7 +153,7 @@
 - (NSRange)rangeOfUnit:(NSCalendarUnit)smaller inUnit:(NSCalendarUnit)larger forDate:(NSDate *)date;
 - (NSUInteger)ordinalityOfUnit:(NSCalendarUnit)smaller inUnit:(NSCalendarUnit)larger forDate:(NSDate *)date;
 
-- (BOOL)rangeOfUnit:(NSCalendarUnit)unit startDate:(NSDate * __nullable * __nullable)datep interval:(nullable NSTimeInterval *)tip forDate:(NSDate *)date NS_AVAILABLE(10_5, 2_0);
+- (BOOL)rangeOfUnit:(NSCalendarUnit)unit startDate:(NSDate * _Nullable * _Nullable)datep interval:(nullable NSTimeInterval *)tip forDate:(NSDate *)date NS_AVAILABLE(10_5, 2_0);
 
 - (nullable NSDate *)dateFromComponents:(NSDateComponents *)comps;
 - (NSDateComponents *)components:(NSCalendarUnit)unitFlags fromDate:(NSDate *)date;
@@ -264,7 +267,7 @@
 	Returns NO if the given date is not in a weekend.
 	Note that a given entire Day within a calendar is not necessarily all in a weekend or not; weekends can start in the middle of a Day in some calendars and locales.
 */
-- (BOOL)rangeOfWeekendStartDate:(out NSDate * __nullable * __nullable)datep interval:(out nullable NSTimeInterval *)tip containingDate:(NSDate *)date NS_AVAILABLE(10_9, 8_0);
+- (BOOL)rangeOfWeekendStartDate:(out NSDate * _Nullable * _Nullable)datep interval:(out nullable NSTimeInterval *)tip containingDate:(NSDate *)date NS_AVAILABLE(10_9, 8_0);
 
 
 /*
@@ -273,7 +276,7 @@
 	Returns NO if there are no such things as weekend in the calendar and its locale.
 	Note that a given entire Day within a calendar is not necessarily all in a weekend or not; weekends can start in the middle of a Day in some calendars and locales.
 */
-- (BOOL)nextWeekendStartDate:(out NSDate * __nullable * __nullable)datep interval:(out nullable NSTimeInterval *)tip options:(NSCalendarOptions)options afterDate:(NSDate *)date NS_AVAILABLE(10_9, 8_0);
+- (BOOL)nextWeekendStartDate:(out NSDate * _Nullable * _Nullable)datep interval:(out nullable NSTimeInterval *)tip options:(NSCalendarOptions)options afterDate:(NSDate *)date NS_AVAILABLE(10_9, 8_0);
 
 
 /* 
@@ -315,7 +318,7 @@
 	Result dates have an integer number of seconds (as if 0 was specified for the nanoseconds property of the NSDateComponents matching parameter), unless a value was set in the nanoseconds property, in which case the result date will have that number of nanoseconds (or as close as possible with floating point numbers).
 	The enumeration is stopped by setting *stop = YES in the block and return.  It is not necessary to set *stop to NO to keep the enumeration going.
 */
-- (void)enumerateDatesStartingAfterDate:(NSDate *)start matchingComponents:(NSDateComponents *)comps options:(NSCalendarOptions)opts usingBlock:(void (^)(NSDate * __nullable date, BOOL exactMatch, BOOL *stop))block NS_AVAILABLE(10_9, 8_0);
+- (void)enumerateDatesStartingAfterDate:(NSDate *)start matchingComponents:(NSDateComponents *)comps options:(NSCalendarOptions)opts usingBlock:(void (NS_NOESCAPE ^)(NSDate * _Nullable date, BOOL exactMatch, BOOL *stop))block NS_AVAILABLE(10_9, 8_0);
 
 /*
 	This method computes the next date which matches (or most closely matches) a given set of components.
@@ -377,7 +380,7 @@
 // notification is received by observers in a "timely" manner, same as
 // with distributed notifications.
 
-FOUNDATION_EXPORT NSString * const NSCalendarDayChangedNotification NS_AVAILABLE(10_9, 8_0);
+FOUNDATION_EXPORT NSNotificationName const NSCalendarDayChangedNotification NS_AVAILABLE(10_9, 8_0);
 
 
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCharacterSet.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCharacterSet.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCharacterSet.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCharacterSet.h	2016-05-20 06:24:14.000000000 +0200
@@ -15,7 +15,7 @@
     NSOpenStepUnicodeReservedBase = 0xF400
 };
 
-@interface NSCharacterSet : NSObject <NSCopying, NSMutableCopying, NSCoding>
+@interface NSCharacterSet : NSObject <NSCopying, NSMutableCopying, NSSecureCoding>
 
 + (NSCharacterSet *)controlCharacterSet;
 + (NSCharacterSet *)whitespaceCharacterSet;
@@ -51,7 +51,7 @@
 - (BOOL)hasMemberInPlane:(uint8_t)thePlane;
 @end
 
-@interface NSMutableCharacterSet : NSCharacterSet <NSCopying, NSMutableCopying>
+@interface NSMutableCharacterSet : NSCharacterSet <NSCopying, NSMutableCopying, NSSecureCoding>
 
 - (void)addCharactersInRange:(NSRange)aRange;
 - (void)removeCharactersInRange:(NSRange)aRange;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCoder.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCoder.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCoder.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSCoder.h	2016-05-20 06:13:47.000000000 +0200
@@ -8,6 +8,17 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+/*!
+ Describes the action an NSCoder should take when it encounters decode failures (e.g. corrupt data) for non-TopLevel decodes.
+ */
+typedef NS_ENUM(NSInteger, NSDecodingFailurePolicy) {
+    // On decode failure, the NSCoder will raise an exception internally to propagate failure messages (and unwind the stack). This exception can be transformed into an NSError via any of the TopLevel decode APIs.
+    NSDecodingFailurePolicyRaiseException,
+
+    // On decode failure, the NSCoder will capture the failure as an NSError, and prevent further decodes (by returning 0 / nil equivalent as appropriate). Clients should consider using this policy if they know that all encoded objects behave correctly in the presence of decode failures (e.g. they use -failWithError: to communicate decode failures and don't raise exceptions for error propagation)
+    NSDecodingFailurePolicySetErrorAndReturn,
+} NS_ENUM_AVAILABLE(10_11, 9_0);
+
 @interface NSCoder : NSObject
 
 - (void)encodeValueOfObjCType:(const char *)type at:(const void *)addr;
@@ -88,13 +99,63 @@
 // Get the current set of allowed classes.
 @property (nullable, readonly, copy) NSSet<Class> *allowedClasses NS_AVAILABLE(10_8, 6_0);
 
-// Record that the entire decode has failed, in lieu of raising an exception
+/*!
+ @abstract Signals to this coder that the decode has failed.
+ @parameter non-nil error that describes the reason why the decode failed
+ @discussion
+ Sets an error on this NSCoder once per TopLevel decode; calling it repeatedly will have no effect until the call stack unwinds to one of the TopLevel decode entry-points.
+
+ This method is only meaningful to call for decodes.
+
+ Typically, you would want to call this method in your -initWithCoder: implementation when you detect situations like:
+ - lack of secure coding
+ - corruption of your data
+ - domain validation failures
+
+ After calling -failWithError: within your -initWithCoder: implementation, you should clean up and return nil as early as possible.
+
+ Once an error has been signaled to a decoder, it remains set until it has handed off to the first TopLevel decode invocation above it.  For example, consider the following call graph:
+ A    -decodeTopLevelObjectForKey:error:
+ B        -initWithCoder:
+ C            -decodeObjectForKey:
+ D                -initWithCoder:
+ E                    -decodeObjectForKey:
+ F                        -failWithError:
+
+ In this case the error provided in stack-frame F will be returned via the outError in stack-frame A. Furthermore the result object from decodeTopLevelObjectForKey:error: will be nil, regardless of the result of stack-frame B.
+
+ NSCoder implementations support two mechanisms for the stack-unwinding from F to A:
+ - forced (NSException based)
+ - particpatory (error based)
+
+ The kind of unwinding you get is determined by the decodingFailurePolicy property of this NSCoder (which defaults to NSDecodingFailurePolicyRaiseException to match historical behavior).
+ */
 - (void)failWithError:(NSError *)error NS_AVAILABLE(10_11, 9_0);
 
+/*!
+ @abstract Defines the behavior this NSCoder should take on decode failure (i.e. corrupt archive, invalid data, etc.).
+ @discussion
+ The default result of this property is NSDecodingFailurePolicyRaiseException, subclasses can change this to an alternative policy.
+ */
+@property (readonly) NSDecodingFailurePolicy decodingFailurePolicy NS_AVAILABLE(10_11, 9_0);
+
+/*!
+ @abstract The current error (if there is one) for the current TopLevel decode.
+ @discussion
+ The meaning of this property changes based on the result of the decodingFailurePolicy property:
+ For NSDecodingFailurePolicyRaiseException, this property will always be nil.
+ For NSDecodingFailurePolicySetErrorAndReturn, this property can be non-nil, and if so, indicates that there was a failure while decoding the archive (specifically its the very first error encountered).
+
+ While .error is non-nil, all attempts to decode data from this coder will return a nil/zero-equivalent value.
+
+ This error is consumed by a TopLevel decode API (which resets this coder back to a being able to potentially decode data).
+ */
+@property (nullable, readonly, copy) NSError *error NS_AVAILABLE(10_11, 9_0);
+
 @end
 
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-FOUNDATION_EXPORT NSObject * __nullable NXReadNSObjectFromCoder(NSCoder *decoder) NS_DEPRECATED(10_0, 10_5, 2_0, 2_0);
+FOUNDATION_EXPORT NSObject * _Nullable NXReadNSObjectFromCoder(NSCoder *decoder) NS_DEPRECATED(10_0, 10_5, 2_0, 2_0);
 /* Given an NSCoder, returns an object previously written with
    NXWriteNSObject(). The returned object is autoreleased. */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSData.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSData.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSData.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSData.h	2016-05-20 06:13:47.000000000 +0200
@@ -95,7 +95,7 @@
 /*
  'block' is called once for each contiguous region of memory in the receiver (once total for contiguous NSDatas), until either all bytes have been enumerated, or the 'stop' parameter is set to YES.
  */
-- (void) enumerateByteRangesUsingBlock:(void (^)(const void *bytes, NSRange byteRange, BOOL *stop))block NS_AVAILABLE(10_9, 7_0);
+- (void) enumerateByteRangesUsingBlock:(void (NS_NOESCAPE ^)(const void *bytes, NSRange byteRange, BOOL *stop))block NS_AVAILABLE(10_9, 7_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDate.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDate.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDate.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDate.h	2016-05-20 06:24:14.000000000 +0200
@@ -3,12 +3,13 @@
 */
 
 #import <Foundation/NSObject.h>
+#import <Foundation/NSNotification.h>
 
 @class NSString;
 
 NS_ASSUME_NONNULL_BEGIN
 
-FOUNDATION_EXPORT NSString * const NSSystemClockDidChangeNotification NS_AVAILABLE(10_6, 4_0);
+FOUNDATION_EXPORT NSNotificationName const NSSystemClockDidChangeNotification NS_AVAILABLE(10_6, 4_0);
 
 typedef double NSTimeInterval;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateComponentsFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateComponentsFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateComponentsFormatter.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateComponentsFormatter.h	2016-05-20 07:39:55.000000000 +0200
@@ -12,9 +12,10 @@
 typedef NS_ENUM(NSInteger, NSDateComponentsFormatterUnitsStyle) {
     NSDateComponentsFormatterUnitsStylePositional = 0, // "1:10; may fall back to abbreviated units in some cases, e.g. 3d"
     NSDateComponentsFormatterUnitsStyleAbbreviated, // "1h 10m"
-    NSDateComponentsFormatterUnitsStyleShort, // "1hr 10min"
+    NSDateComponentsFormatterUnitsStyleShort, // "1hr, 10min"
     NSDateComponentsFormatterUnitsStyleFull, // "1 hour, 10 minutes"
-    NSDateComponentsFormatterUnitsStyleSpellOut // "One hour, ten minutes"
+    NSDateComponentsFormatterUnitsStyleSpellOut, // "One hour, ten minutes"
+    NSDateComponentsFormatterUnitsStyleBrief API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) // "1hr 10min" - Brief is shorter than Short (e.g. in English, it removes the comma)
 };
 
 NS_ENUM_AVAILABLE(10_10, 8_0)
@@ -32,7 +33,7 @@
 
 /* NSDateComponentsFormatter provides locale-correct and flexible string formatting of quantities of time, such as "1 day" or "1h 10m", as specified by NSDateComponents. For formatting intervals of time (such as "2PM to 5PM"), see NSDateIntervalFormatter. NSDateComponentsFormatter is thread-safe, in that calling methods on it from multiple threads will not cause crashes or incorrect results, but it makes no attempt to prevent confusion when one thread sets something and another thread isn't expecting it to change.
  */
-NS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_10, 8_0)
 @interface NSDateComponentsFormatter : NSFormatter {
     @private
     pthread_mutex_t _lock;
@@ -56,7 +57,7 @@
 
 /* 'obj' must be an instance of NSDateComponents.
  */
-- (nullable NSString *)stringForObjectValue:(id)obj;
+- (nullable NSString *)stringForObjectValue:(nullable id)obj;
 
 - (nullable NSString *)stringFromDateComponents:(NSDateComponents *)components;
 
@@ -139,7 +140,7 @@
 
 /* NSDateComponentsFormatter currently only implements formatting, not parsing. Until it implements parsing, this will always return NO.
  */
-- (BOOL)getObjectValue:(out id __nullable * __nullable)obj forString:(NSString *)string errorDescription:(out NSString * __nullable * __nullable)error;
+- (BOOL)getObjectValue:(out id _Nullable * _Nullable)obj forString:(NSString *)string errorDescription:(out NSString * _Nullable * _Nullable)error;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateFormatter.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateFormatter.h	2016-05-20 06:25:32.000000000 +0200
@@ -19,7 +19,7 @@
 @interface NSDateFormatter : NSFormatter {
 @private
     NSMutableDictionary *_attributes;
-    __strong CFDateFormatterRef _formatter;
+    CFDateFormatterRef _formatter;
     NSUInteger _counter;
 }
 
@@ -29,7 +29,7 @@
 
 // Report the used range of the string and an NSError, in addition to the usual stuff from NSFormatter
 
-- (BOOL)getObjectValue:(out id __nullable * __nullable)obj forString:(NSString *)string range:(inout nullable NSRange *)rangep error:(out NSError **)error;
+- (BOOL)getObjectValue:(out id _Nullable * _Nullable)obj forString:(NSString *)string range:(inout nullable NSRange *)rangep error:(out NSError **)error;
 
 // Even though NSDateFormatter responds to the usual NSFormatter methods,
 //   here are some convenience methods which are a little more obvious.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateInterval.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateInterval.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateInterval.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateInterval.h	2016-05-20 06:24:14.000000000 +0200
@@ -0,0 +1,64 @@
+/*	NSDateInterval.h
+	Copyright © 2015, Apple Inc. All rights reserved.
+ */
+
+#import <Foundation/NSObject.h>
+#import <Foundation/NSDate.h>
+#import <Foundation/NSCoder.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSDateInterval : NSObject <NSCopying, NSSecureCoding>
+
+/*
+ NSDateInterval represents a closed date interval in the form of [startDate, endDate].  It is possible for the start and end dates to be the same with a duration of 0.  NSDateInterval does not support reverse intervals i.e. intervals where the duration is less than 0 and the end date occurs earlier in time than the start date.
+ */
+
+@property (readonly, copy) NSDate *startDate;
+@property (readonly, copy) NSDate *endDate;
+@property (readonly) NSTimeInterval duration;
+
+// This method initializes an NSDateInterval object with start and end dates set to the current date and the duration set to 0.
+- (instancetype)init;
+
+- (instancetype)initWithCoder:(NSCoder *)coder NS_DESIGNATED_INITIALIZER;
+
+// This method will throw an exception if the duration is less than 0.
+- (instancetype)initWithStartDate:(NSDate *)startDate duration:(NSTimeInterval)duration NS_DESIGNATED_INITIALIZER;
+
+// This method will throw an exception if the end date comes before the start date.
+- (instancetype)initWithStartDate:(NSDate *)startDate endDate:(NSDate *)endDate;
+
+/*
+ (NSComparisonResult)compare:(NSDateInterval *) prioritizes ordering by start date. If the start dates are equal, then it will order by duration.
+ e.g.
+    Given intervals a and b
+        a.   |-----|
+        b.      |-----|
+ [a compare:b] would return NSOrderAscending because a's startDate is earlier in time than b's start date.
+
+ In the event that the start dates are equal, the compare method will attempt to order by duration.
+ e.g.
+    Given intervals c and d
+        c.  |-----|
+        d.  |---|
+ [c compare:d] would result in NSOrderDescending because c is longer than d.
+
+ If both the start dates and the durations are equal, then the intervals are considered equal and NSOrderedSame is returned as the result.
+ */
+- (NSComparisonResult)compare:(NSDateInterval *)dateInterval;
+
+- (BOOL)isEqualToDateInterval:(NSDateInterval *)dateInterval;
+- (BOOL)intersectsDateInterval:(NSDateInterval *)dateInterval;
+
+/*
+ This method returns an NSDateInterval object that represents the interval where the given date interval and the current instance intersect. In the event that there is no intersection, the method returns nil.
+ */
+- (nullable NSDateInterval *)intersectionWithDateInterval:(NSDateInterval *)dateInterval;
+
+- (BOOL)containsDate:(NSDate *)date;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateIntervalFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateIntervalFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateIntervalFormatter.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDateIntervalFormatter.h	2016-05-20 06:24:14.000000000 +0200
@@ -3,6 +3,7 @@
  */
 
 #import <Foundation/NSFormatter.h>
+#import <Foundation/NSDateInterval.h>
 #include <dispatch/dispatch.h>
 @class NSLocale, NSCalendar, NSTimeZone, NSDate;
 
@@ -64,6 +65,8 @@
 */
 - (NSString *)stringFromDate:(NSDate *)fromDate toDate:(NSDate *)toDate;
 
+- (nullable NSString *)stringFromDateInterval:(NSDateInterval *)dateInterval API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDecimal.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDecimal.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDecimal.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDecimal.h	2016-05-20 06:24:14.000000000 +0200
@@ -84,6 +84,6 @@
 
 FOUNDATION_EXPORT NSCalculationError NSDecimalMultiplyByPowerOf10(NSDecimal *result, const NSDecimal *number, short power, NSRoundingMode roundingMode);
 
-FOUNDATION_EXPORT NSString *NSDecimalString(const NSDecimal *dcm, id __nullable locale);
+FOUNDATION_EXPORT NSString *NSDecimalString(const NSDecimal *dcm, id _Nullable locale);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDecimalNumber.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDecimalNumber.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDecimalNumber.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDecimalNumber.h	2016-05-20 07:35:40.000000000 +0200
@@ -6,15 +6,16 @@
 #import <Foundation/NSScanner.h>
 #import <Foundation/NSDecimal.h>
 #import <Foundation/NSDictionary.h>
+#import <Foundation/NSException.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
 /***************	Exceptions		***********/
 
-FOUNDATION_EXPORT NSString * const NSDecimalNumberExactnessException;
-FOUNDATION_EXPORT NSString * const NSDecimalNumberOverflowException;
-FOUNDATION_EXPORT NSString * const NSDecimalNumberUnderflowException;
-FOUNDATION_EXPORT NSString * const NSDecimalNumberDivideByZeroException;
+FOUNDATION_EXPORT NSExceptionName const NSDecimalNumberExactnessException;
+FOUNDATION_EXPORT NSExceptionName const NSDecimalNumberOverflowException;
+FOUNDATION_EXPORT NSExceptionName const NSDecimalNumberUnderflowException;
+FOUNDATION_EXPORT NSExceptionName const NSDecimalNumberDivideByZeroException;
 
 /***************	Rounding and Exception behavior		***********/
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDictionary.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDictionary.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDictionary.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDictionary.h	2016-05-20 06:12:55.000000000 +0200
@@ -18,9 +18,9 @@
 - (NSEnumerator<KeyType> *)keyEnumerator;
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
 #if TARGET_OS_WIN32
-- (instancetype)initWithObjects:(const ObjectType [])objects forKeys:(const KeyType [])keys count:(NSUInteger)cnt;
+- (instancetype)initWithObjects:(const ObjectType _Nonnull [_Nullable])objects forKeys:(const KeyType _Nonnull [_Nullable])keys count:(NSUInteger)cnt;
 #else
-- (instancetype)initWithObjects:(const ObjectType [])objects forKeys:(const KeyType <NSCopying> [])keys count:(NSUInteger)cnt NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithObjects:(const ObjectType _Nonnull [_Nullable])objects forKeys:(const KeyType <NSCopying> _Nonnull [_Nullable])keys count:(NSUInteger)cnt NS_DESIGNATED_INITIALIZER;
 #endif
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
 
@@ -43,24 +43,24 @@
 
 - (NSArray<KeyType> *)keysSortedByValueUsingSelector:(SEL)comparator;
 // count refers to the number of elements in the dictionary
-- (void)getObjects:(ObjectType __unsafe_unretained [])objects andKeys:(KeyType __unsafe_unretained [])keys count:(NSUInteger)count NS_AVAILABLE(10_7, 5_0);
+- (void)getObjects:(ObjectType __unsafe_unretained [])objects andKeys:(KeyType __unsafe_unretained [])keys count:(NSUInteger)count NS_AVAILABLE(10_7, 5_0) NS_SWIFT_UNAVAILABLE("Use 'allKeys' and/or 'allValues' instead");
 
 - (nullable ObjectType)objectForKeyedSubscript:(KeyType)key NS_AVAILABLE(10_8, 6_0);
 
-- (void)enumerateKeysAndObjectsUsingBlock:(void (^)(KeyType key, ObjectType obj, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
-- (void)enumerateKeysAndObjectsWithOptions:(NSEnumerationOptions)opts usingBlock:(void (^)(KeyType key, ObjectType obj, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
+- (void)enumerateKeysAndObjectsUsingBlock:(void (NS_NOESCAPE ^)(KeyType key, ObjectType obj, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
+- (void)enumerateKeysAndObjectsWithOptions:(NSEnumerationOptions)opts usingBlock:(void (NS_NOESCAPE ^)(KeyType key, ObjectType obj, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
 
-- (NSArray<KeyType> *)keysSortedByValueUsingComparator:(NSComparator)cmptr NS_AVAILABLE(10_6, 4_0);
-- (NSArray<KeyType> *)keysSortedByValueWithOptions:(NSSortOptions)opts usingComparator:(NSComparator)cmptr NS_AVAILABLE(10_6, 4_0);
+- (NSArray<KeyType> *)keysSortedByValueUsingComparator:(NSComparator NS_NOESCAPE)cmptr NS_AVAILABLE(10_6, 4_0);
+- (NSArray<KeyType> *)keysSortedByValueWithOptions:(NSSortOptions)opts usingComparator:(NSComparator NS_NOESCAPE)cmptr NS_AVAILABLE(10_6, 4_0);
 
-- (NSSet<KeyType> *)keysOfEntriesPassingTest:(BOOL (^)(KeyType key, ObjectType obj, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
-- (NSSet<KeyType> *)keysOfEntriesWithOptions:(NSEnumerationOptions)opts passingTest:(BOOL (^)(KeyType key, ObjectType obj, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
+- (NSSet<KeyType> *)keysOfEntriesPassingTest:(BOOL (NS_NOESCAPE ^)(KeyType key, ObjectType obj, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
+- (NSSet<KeyType> *)keysOfEntriesWithOptions:(NSEnumerationOptions)opts passingTest:(BOOL (NS_NOESCAPE ^)(KeyType key, ObjectType obj, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
 
 @end
 
 @interface NSDictionary<KeyType, ObjectType> (NSDeprecated)
 /// This method is unsafe because it could potentially cause buffer overruns. You should use -getObjects:andKeys:count:
-- (void)getObjects:(ObjectType __unsafe_unretained [])objects andKeys:(KeyType __unsafe_unretained [])keys;
+- (void)getObjects:(ObjectType __unsafe_unretained [])objects andKeys:(KeyType __unsafe_unretained [])keys  NS_SWIFT_UNAVAILABLE("Use 'allKeys' and/or 'allValues' instead");
 @end
 
 @interface NSDictionary<KeyType, ObjectType> (NSDictionaryCreation)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSEnergyFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSEnergyFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSEnergyFormatter.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSEnergyFormatter.h	2016-05-20 06:24:14.000000000 +0200
@@ -37,7 +37,7 @@
 - (NSString *)unitStringFromJoules:(double)numberInJoules usedUnit:(nullable NSEnergyFormatterUnit *)unitp;
 
 // No parsing is supported. This method will return NO.
-- (BOOL)getObjectValue:(out id __nullable * __nullable)obj forString:(NSString *)string errorDescription:(out NSString * __nullable * __nullable)error;
+- (BOOL)getObjectValue:(out id _Nullable * _Nullable)obj forString:(NSString *)string errorDescription:(out NSString * _Nullable * _Nullable)error;
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSEnumerator.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSEnumerator.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSEnumerator.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSEnumerator.h	2016-05-20 06:24:14.000000000 +0200
@@ -20,14 +20,14 @@
 
 typedef struct {
     unsigned long state;
-    id __unsafe_unretained __nullable * __nullable itemsPtr;
-    unsigned long * __nullable mutationsPtr;
+    id __unsafe_unretained _Nullable * _Nullable itemsPtr;
+    unsigned long * _Nullable mutationsPtr;
     unsigned long extra[5];
 } NSFastEnumerationState;
 
 @protocol NSFastEnumeration
 
-- (NSUInteger)countByEnumeratingWithState:(NSFastEnumerationState *)state objects:(id __unsafe_unretained [])buffer count:(NSUInteger)len;
+- (NSUInteger)countByEnumeratingWithState:(NSFastEnumerationState *)state objects:(id __unsafe_unretained _Nullable [_Nonnull])buffer count:(NSUInteger)len;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSError.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSError.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSError.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSError.h	2016-05-20 07:35:40.000000000 +0200
@@ -6,20 +6,32 @@
 
 @class NSDictionary, NSArray<ObjectType>, NSString;
 
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 7)
+typedef NSString *NSErrorDomain;
+#else
+typedef NSString *NSErrorDomain NS_EXTENSIBLE_STRING_ENUM;
+#endif
+
 NS_ASSUME_NONNULL_BEGIN
 
 // Predefined domain for errors from most AppKit and Foundation APIs.
-FOUNDATION_EXPORT NSString *const NSCocoaErrorDomain;
+FOUNDATION_EXPORT NSErrorDomain const NSCocoaErrorDomain;
 
 // Other predefined domains; value of "code" will correspond to preexisting values in these domains.
-FOUNDATION_EXPORT NSString *const NSPOSIXErrorDomain;
-FOUNDATION_EXPORT NSString *const NSOSStatusErrorDomain;
-FOUNDATION_EXPORT NSString *const NSMachErrorDomain;
+FOUNDATION_EXPORT NSErrorDomain const NSPOSIXErrorDomain;
+FOUNDATION_EXPORT NSErrorDomain const NSOSStatusErrorDomain;
+FOUNDATION_EXPORT NSErrorDomain const NSMachErrorDomain;
 
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 7)
 // Key in userInfo. A recommended standard way to embed NSErrors from underlying calls. The value of this key should be an NSError.
 FOUNDATION_EXPORT NSString *const NSUnderlyingErrorKey;
+#else
+typedef NSString *NSErrorUserInfoKey NS_EXTENSIBLE_STRING_ENUM;
+FOUNDATION_EXPORT NSErrorUserInfoKey const NSUnderlyingErrorKey;
+#endif
 
 // Keys in userInfo, for subsystems wishing to provide their error messages up-front. Note that NSError will also consult the userInfoValueProvider for the domain when these values are not present in the userInfo dictionary.
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 7)
 FOUNDATION_EXPORT NSString *const NSLocalizedDescriptionKey;             // NSString
 FOUNDATION_EXPORT NSString *const NSLocalizedFailureReasonErrorKey;      // NSString
 FOUNDATION_EXPORT NSString *const NSLocalizedRecoverySuggestionErrorKey; // NSString
@@ -31,7 +43,19 @@
 FOUNDATION_EXPORT NSString *const NSStringEncodingErrorKey ;  // NSNumber containing NSStringEncoding
 FOUNDATION_EXPORT NSString *const NSURLErrorKey;              // NSURL
 FOUNDATION_EXPORT NSString *const NSFilePathErrorKey;         // NSString
+#else
+FOUNDATION_EXPORT NSErrorUserInfoKey const NSLocalizedDescriptionKey;             // NSString
+FOUNDATION_EXPORT NSErrorUserInfoKey const NSLocalizedFailureReasonErrorKey;      // NSString
+FOUNDATION_EXPORT NSErrorUserInfoKey const NSLocalizedRecoverySuggestionErrorKey; // NSString
+FOUNDATION_EXPORT NSErrorUserInfoKey const NSLocalizedRecoveryOptionsErrorKey;    // NSArray of NSStrings
+FOUNDATION_EXPORT NSErrorUserInfoKey const NSRecoveryAttempterErrorKey;           // Instance of a subclass of NSObject that conforms to the NSErrorRecoveryAttempting informal protocol
+FOUNDATION_EXPORT NSErrorUserInfoKey const NSHelpAnchorErrorKey;                  // NSString containing a help anchor
 
+// Other standard keys in userInfo, for various error codes
+FOUNDATION_EXPORT NSErrorUserInfoKey const NSStringEncodingErrorKey ;  // NSNumber containing NSStringEncoding
+FOUNDATION_EXPORT NSErrorUserInfoKey const NSURLErrorKey;              // NSURL
+FOUNDATION_EXPORT NSErrorUserInfoKey const NSFilePathErrorKey;         // NSString
+#endif
 
 
 @interface NSError : NSObject <NSCopying, NSSecureCoding> {
@@ -44,12 +68,12 @@
 
 /* Domain cannot be nil; dict may be nil if no userInfo desired.
 */
-- (instancetype)initWithDomain:(NSString *)domain code:(NSInteger)code userInfo:(nullable NSDictionary *)dict NS_DESIGNATED_INITIALIZER;
-+ (instancetype)errorWithDomain:(NSString *)domain code:(NSInteger)code userInfo:(nullable NSDictionary *)dict;
+- (instancetype)initWithDomain:(NSErrorDomain)domain code:(NSInteger)code userInfo:(nullable NSDictionary *)dict NS_DESIGNATED_INITIALIZER;
++ (instancetype)errorWithDomain:(NSErrorDomain)domain code:(NSInteger)code userInfo:(nullable NSDictionary *)dict;
 
 /* These define the error. Domains are described by names that are arbitrary strings used to differentiate groups of codes; for custom domain using reverse-DNS naming will help avoid conflicts. Codes are domain-specific.
 */
-@property (readonly, copy) NSString *domain;
+@property (readonly, copy) NSErrorDomain domain;
 @property (readonly) NSInteger code;
 
 /* Additional info which may be used to describe the error further. Examples of keys that might be included in here are "Line Number", "Failed URL", etc. Embedding other errors in here can also be used as a way to communicate underlying reasons for failures; for instance "File System Error" embedded in the userInfo of an NSError returned from a higher level document object. If the embedded error information is itself NSError, the standard key NSUnderlyingErrorKey can be used.
@@ -91,8 +115,13 @@
  
 If an appropriate result for the requested key cannot be provided, return nil rather than choosing to manufacture a generic fallback response such as "Operation could not be completed, error 42." NSError will take care of the fallback cases.
 */
-+ (void)setUserInfoValueProviderForDomain:(NSString *)errorDomain provider:(id __nullable (^ __nullable)(NSError *err, NSString *userInfoKey))provider NS_AVAILABLE(10_11, 9_0);
-+ (id __nullable (^ __nullable)(NSError *err, NSString *userInfoKey))userInfoValueProviderForDomain:(NSString *)errorDomain NS_AVAILABLE(10_11, 9_0);
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 7)
++ (void)setUserInfoValueProviderForDomain:(NSErrorDomain)errorDomain provider:(id _Nullable (^ _Nullable)(NSError *err, NSString *userInfoKey))provider NS_AVAILABLE(10_11, 9_0);
++ (id _Nullable (^ _Nullable)(NSError *err, NSString *userInfoKey))userInfoValueProviderForDomain:(NSErrorDomain)errorDomain NS_AVAILABLE(10_11, 9_0);
+#else
++ (void)setUserInfoValueProviderForDomain:(NSErrorDomain)errorDomain provider:(id _Nullable (^ _Nullable)(NSError *err, NSErrorUserInfoKey userInfoKey))provider NS_AVAILABLE(10_11, 9_0);
++ (id _Nullable (^ _Nullable)(NSError *err, NSErrorUserInfoKey userInfoKey))userInfoValueProviderForDomain:(NSErrorDomain)errorDomain NS_AVAILABLE(10_11, 9_0);
+#endif
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSException.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSException.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSException.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSException.h	2016-05-20 06:13:47.000000000 +0200
@@ -13,24 +13,24 @@
 
 /***************	Generic Exception names		***************/
 
-FOUNDATION_EXPORT NSString * const NSGenericException;
-FOUNDATION_EXPORT NSString * const NSRangeException;
-FOUNDATION_EXPORT NSString * const NSInvalidArgumentException;
-FOUNDATION_EXPORT NSString * const NSInternalInconsistencyException;
-
-FOUNDATION_EXPORT NSString * const NSMallocException;
-
-FOUNDATION_EXPORT NSString * const NSObjectInaccessibleException;
-FOUNDATION_EXPORT NSString * const NSObjectNotAvailableException;
-FOUNDATION_EXPORT NSString * const NSDestinationInvalidException;
+FOUNDATION_EXPORT NSExceptionName const NSGenericException;
+FOUNDATION_EXPORT NSExceptionName const NSRangeException;
+FOUNDATION_EXPORT NSExceptionName const NSInvalidArgumentException;
+FOUNDATION_EXPORT NSExceptionName const NSInternalInconsistencyException;
+
+FOUNDATION_EXPORT NSExceptionName const NSMallocException;
+
+FOUNDATION_EXPORT NSExceptionName const NSObjectInaccessibleException;
+FOUNDATION_EXPORT NSExceptionName const NSObjectNotAvailableException;
+FOUNDATION_EXPORT NSExceptionName const NSDestinationInvalidException;
     
-FOUNDATION_EXPORT NSString * const NSPortTimeoutException;
-FOUNDATION_EXPORT NSString * const NSInvalidSendPortException;
-FOUNDATION_EXPORT NSString * const NSInvalidReceivePortException;
-FOUNDATION_EXPORT NSString * const NSPortSendException;
-FOUNDATION_EXPORT NSString * const NSPortReceiveException;
+FOUNDATION_EXPORT NSExceptionName const NSPortTimeoutException;
+FOUNDATION_EXPORT NSExceptionName const NSInvalidSendPortException;
+FOUNDATION_EXPORT NSExceptionName const NSInvalidReceivePortException;
+FOUNDATION_EXPORT NSExceptionName const NSPortSendException;
+FOUNDATION_EXPORT NSExceptionName const NSPortReceiveException;
 
-FOUNDATION_EXPORT NSString * const NSOldStyleException;
+FOUNDATION_EXPORT NSExceptionName const NSOldStyleException;
 
 /***************	Exception object	***************/
 
@@ -45,10 +45,10 @@
     id			reserved;
 }
 
-+ (NSException *)exceptionWithName:(NSString *)name reason:(nullable NSString *)reason userInfo:(nullable NSDictionary *)userInfo;
-- (instancetype)initWithName:(NSString *)aName reason:(nullable NSString *)aReason userInfo:(nullable NSDictionary *)aUserInfo NS_DESIGNATED_INITIALIZER;
++ (NSException *)exceptionWithName:(NSExceptionName)name reason:(nullable NSString *)reason userInfo:(nullable NSDictionary *)userInfo;
+- (instancetype)initWithName:(NSExceptionName)aName reason:(nullable NSString *)aReason userInfo:(nullable NSDictionary *)aUserInfo NS_DESIGNATED_INITIALIZER;
 
-@property (readonly, copy) NSString *name;
+@property (readonly, copy) NSExceptionName name;
 @property (nullable, readonly, copy) NSString *reason;
 @property (nullable, readonly, copy) NSDictionary *userInfo;
 
@@ -61,8 +61,8 @@
 
 @interface NSException (NSExceptionRaisingConveniences)
 
-+ (void)raise:(NSString *)name format:(NSString *)format, ... NS_FORMAT_FUNCTION(2,3);
-+ (void)raise:(NSString *)name format:(NSString *)format arguments:(va_list)argList NS_FORMAT_FUNCTION(2,0);
++ (void)raise:(NSExceptionName)name format:(NSString *)format, ... NS_FORMAT_FUNCTION(2,3);
++ (void)raise:(NSExceptionName)name format:(NSString *)format arguments:(va_list)argList NS_FORMAT_FUNCTION(2,0);
 
 @end
 
@@ -76,8 +76,8 @@
 
 typedef void NSUncaughtExceptionHandler(NSException *exception);
 
-FOUNDATION_EXPORT NSUncaughtExceptionHandler * __nullable NSGetUncaughtExceptionHandler(void);
-FOUNDATION_EXPORT void NSSetUncaughtExceptionHandler(NSUncaughtExceptionHandler * __nullable);
+FOUNDATION_EXPORT NSUncaughtExceptionHandler * _Nullable NSGetUncaughtExceptionHandler(void);
+FOUNDATION_EXPORT void NSSetUncaughtExceptionHandler(NSUncaughtExceptionHandler * _Nullable);
 
 
 #if __clang__
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSExpression.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSExpression.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSExpression.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSExpression.h	2016-05-20 07:35:40.000000000 +0200
@@ -100,7 +100,7 @@
 + (NSExpression *)expressionForSubquery:(NSExpression *)expression usingIteratorVariable:(NSString *)variable predicate:(id)predicate NS_AVAILABLE(10_5, 3_0); // Expression that filters a collection by storing elements in the collection in the variable variable and keeping the elements for which qualifer returns true; variable is used as a local variable, and will shadow any instances of variable in the bindings dictionary, the variable is removed or the old value replaced once evaluation completes
 + (NSExpression *)expressionForFunction:(NSExpression *)target selectorName:(NSString *)name arguments:(nullable NSArray *)parameters NS_AVAILABLE(10_5, 3_0);    // Expression that invokes the selector on target with parameters. Will throw at runtime if target does not implement selector or if parameters are wrong.
 + (NSExpression *)expressionForAnyKey NS_AVAILABLE(10_9, 7_0);
-+ (NSExpression *)expressionForBlock:(id (^)(id __nullable evaluatedObject, NSArray *expressions, NSMutableDictionary * __nullable context))block arguments:(nullable NSArray<NSExpression *> *)arguments NS_AVAILABLE(10_6, 4_0); // Expression that invokes the block with the parameters; note that block expressions are not encodable or representable as parseable strings.
++ (NSExpression *)expressionForBlock:(id (^)(id _Nullable evaluatedObject, NSArray *expressions, NSMutableDictionary * _Nullable context))block arguments:(nullable NSArray<NSExpression *> *)arguments NS_AVAILABLE(10_6, 4_0); // Expression that invokes the block with the parameters; note that block expressions are not encodable or representable as parseable strings.
 + (NSExpression *)expressionForConditional:(NSPredicate *)predicate trueExpression:(NSExpression *)trueExpression falseExpression:(NSExpression *)falseExpression  NS_AVAILABLE(10_11, 9_0); // Expression that will return the result of trueExpression or falseExpression depending on the value of predicate
 
 - (instancetype)initWithExpressionType:(NSExpressionType)type NS_DESIGNATED_INITIALIZER;
@@ -108,7 +108,11 @@
 
 // accessors for individual parameters - raise if not applicable
 @property (readonly) NSExpressionType expressionType;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 6)
+@property (nullable, readonly, retain) id constantValue;
+#else
 @property (readonly, retain) id constantValue;
+#endif
 @property (readonly, copy) NSString *keyPath;
 @property (readonly, copy) NSString *function;
 @property (readonly, copy) NSString *variable;
@@ -124,10 +128,14 @@
 @property (readonly, copy) NSExpression *trueExpression NS_AVAILABLE(10_11, 9_0); // expression which will be evaluated if a conditional expression's predicate evaluates to true
 @property (readonly, copy) NSExpression *falseExpression NS_AVAILABLE(10_11, 9_0); // expression which will be evaluated if a conditional expression's predicate evaluates to false
 
-@property (readonly, copy) id (^expressionBlock)(id __nullable, NSArray *, NSMutableDictionary * __nullable) NS_AVAILABLE(10_6, 4_0);
+@property (readonly, copy) id (^expressionBlock)(id _Nullable, NSArray *, NSMutableDictionary * _Nullable) NS_AVAILABLE(10_6, 4_0);
 
 // evaluate the expression using the object and bindings- note that context is mutable here and can be used by expressions to store temporary state for one predicate evaluation
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 6)
+- (nullable id)expressionValueWithObject:(nullable id)object context:(nullable NSMutableDictionary *)context;
+#else
 - (id)expressionValueWithObject:(nullable id)object context:(nullable NSMutableDictionary *)context;
+#endif
 
 - (void)allowEvaluation NS_AVAILABLE(10_9, 7_0); // Force an expression which was securely decoded to allow evaluation
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileCoordinator.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileCoordinator.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileCoordinator.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileCoordinator.h	2016-05-20 06:13:48.000000000 +0200
@@ -167,7 +167,7 @@
  
 For both coordinated reading and writing, if there are multiple NSFilePresenters involved then the order in which they are messaged is undefined. If an NSFilePresenter signals failure then waiting will fail and *outError will be set to an NSError describing the failure.
 */
-- (void)coordinateAccessWithIntents:(NSArray<NSFileAccessIntent *> *)intents queue:(NSOperationQueue *)queue byAccessor:(void (^)(NSError * __nullable error))accessor NS_AVAILABLE(10_10, 8_0);
+- (void)coordinateAccessWithIntents:(NSArray<NSFileAccessIntent *> *)intents queue:(NSOperationQueue *)queue byAccessor:(void (^)(NSError * _Nullable error))accessor NS_AVAILABLE(10_10, 8_0);
 
 #pragma mark *** Synchronous File Coordination ***
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileHandle.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileHandle.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileHandle.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileHandle.h	2016-05-20 06:24:14.000000000 +0200
@@ -5,6 +5,9 @@
 #import <Foundation/NSObject.h>
 #import <Foundation/NSArray.h>
 #import <Foundation/NSRange.h>
+#import <Foundation/NSException.h>
+#import <Foundation/NSNotification.h>
+#import <Foundation/NSRunLoop.h>
 
 @class NSString, NSData, NSError;
 
@@ -49,12 +52,12 @@
 
 @end
 
-FOUNDATION_EXPORT NSString * const NSFileHandleOperationException;
+FOUNDATION_EXPORT NSExceptionName const NSFileHandleOperationException;
 
-FOUNDATION_EXPORT NSString * const NSFileHandleReadCompletionNotification;
-FOUNDATION_EXPORT NSString * const NSFileHandleReadToEndOfFileCompletionNotification;
-FOUNDATION_EXPORT NSString * const NSFileHandleConnectionAcceptedNotification;
-FOUNDATION_EXPORT NSString * const NSFileHandleDataAvailableNotification;
+FOUNDATION_EXPORT NSNotificationName const NSFileHandleReadCompletionNotification;
+FOUNDATION_EXPORT NSNotificationName const NSFileHandleReadToEndOfFileCompletionNotification;
+FOUNDATION_EXPORT NSNotificationName const NSFileHandleConnectionAcceptedNotification;
+FOUNDATION_EXPORT NSNotificationName const NSFileHandleDataAvailableNotification;
 
 FOUNDATION_EXPORT NSString * const NSFileHandleNotificationDataItem;
 FOUNDATION_EXPORT NSString * const NSFileHandleNotificationFileHandleItem;
@@ -62,16 +65,16 @@
 
 @interface NSFileHandle (NSFileHandleAsynchronousAccess)
 
-- (void)readInBackgroundAndNotifyForModes:(nullable NSArray<NSString *> *)modes;
+- (void)readInBackgroundAndNotifyForModes:(nullable NSArray<NSRunLoopMode> *)modes;
 - (void)readInBackgroundAndNotify;
 
-- (void)readToEndOfFileInBackgroundAndNotifyForModes:(nullable NSArray<NSString *> *)modes;
+- (void)readToEndOfFileInBackgroundAndNotifyForModes:(nullable NSArray<NSRunLoopMode> *)modes;
 - (void)readToEndOfFileInBackgroundAndNotify;
 
-- (void)acceptConnectionInBackgroundAndNotifyForModes:(nullable NSArray<NSString *> *)modes;
+- (void)acceptConnectionInBackgroundAndNotifyForModes:(nullable NSArray<NSRunLoopMode> *)modes;
 - (void)acceptConnectionInBackgroundAndNotify;
 
-- (void)waitForDataInBackgroundAndNotifyForModes:(nullable NSArray<NSString *> *)modes;
+- (void)waitForDataInBackgroundAndNotifyForModes:(nullable NSArray<NSRunLoopMode> *)modes;
 - (void)waitForDataInBackgroundAndNotify;
 
 #ifdef __BLOCKS__
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileManager.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileManager.h	2016-05-20 07:39:55.000000000 +0200
@@ -6,11 +6,18 @@
 #import <Foundation/NSEnumerator.h>
 #import <Foundation/NSDictionary.h>
 #import <Foundation/NSPathUtilities.h>
+#import <Foundation/NSNotification.h>
+#import <Foundation/NSError.h>
+#import <Foundation/NSURL.h>
 #import <CoreFoundation/CFBase.h>
 
 @class NSArray<ObjectType>, NSData, NSDate, NSDirectoryEnumerator<ObjectType>, NSError, NSNumber;
 @protocol NSFileManagerDelegate;
 
+typedef NSString * NSFileAttributeKey NS_EXTENSIBLE_STRING_ENUM;
+typedef NSString * NSFileAttributeType NS_STRING_ENUM;
+typedef NSString * NSFileProtectionType NS_STRING_ENUM;
+
 NS_ASSUME_NONNULL_BEGIN
 
 /* Version number where NSFileManager can copy/move/enumerate resources forks correctly. 
@@ -69,11 +76,15 @@
 } NS_ENUM_AVAILABLE(10_11, NA);
 
 /* If unmountVolumeAtURL:options:completionHandler: fails, the process identifier of the dissenter can be found in the  NSError's userInfo dictionary with this key */
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 7)
 FOUNDATION_EXPORT NSString *const NSFileManagerUnmountDissentingProcessIdentifierErrorKey NS_AVAILABLE(10_11, NA); // value is NSNumber containing the process identifier of the dissenter
+#else
+FOUNDATION_EXPORT NSErrorUserInfoKey const NSFileManagerUnmountDissentingProcessIdentifierErrorKey NS_AVAILABLE(10_11, NA);
+#endif
 
 /* Notification sent after the current ubiquity identity has changed.
 */
-extern NSString * const NSUbiquityIdentityDidChangeNotification NS_AVAILABLE(10_8, 6_0);
+extern NSNotificationName const NSUbiquityIdentityDidChangeNotification NS_AVAILABLE(10_8, 6_0);
 
 @interface NSFileManager : NSObject
 
@@ -87,7 +98,7 @@
 
 /* This method starts the process of unmounting the volume specified by url. If the volume is encrypted, it is re-locked after being unmounted. The completionHandler will be executed when the operation is complete. If the operation was successful, the block’s errorOrNil argument will be nil; otherwise, errorOrNil will be an error object indicating why the unmount operation failed.
  */
-- (void)unmountVolumeAtURL:(NSURL *)url options:(NSFileManagerUnmountOptions)mask completionHandler:(void (^)(NSError * __nullable errorOrNil))completionHandler NS_AVAILABLE(10_11, NA);
+- (void)unmountVolumeAtURL:(NSURL *)url options:(NSFileManagerUnmountOptions)mask completionHandler:(void (^)(NSError * _Nullable errorOrNil))completionHandler NS_AVAILABLE(10_11, NA);
 
 /* -contentsOfDirectoryAtURL:includingPropertiesForKeys:options:error: returns an NSArray of NSURLs identifying the the directory entries. If this method returns nil, an NSError will be returned by reference in the 'error' parameter. If the directory contains no entries, this method will return the empty array. When an array is specified for the 'keys' parameter, the specified property values will be pre-fetched and cached with each enumerated URL.
  
@@ -194,7 +205,7 @@
 
     To easily discover if an item is in the Trash, you may use [fileManager getRelationship:&result ofDirectory:NSTrashDirectory inDomain:0 toItemAtURL:url error:&error] && result == NSURLRelationshipContains.
  */
-- (BOOL)trashItemAtURL:(NSURL *)url resultingItemURL:(NSURL * __nullable * __nullable)outResultingURL error:(NSError **)error NS_AVAILABLE_MAC(10_8);
+- (BOOL)trashItemAtURL:(NSURL *)url resultingItemURL:(NSURL * _Nullable * _Nullable)outResultingURL error:(NSError **)error NS_AVAILABLE_MAC(10_8);
 
 /* The following methods are deprecated on Mac OS X 10.5. Their URL-based and/or error-returning replacements are listed above.
  */
@@ -260,7 +271,7 @@
 
 /* fileSystemRepresentationWithPath: returns an array of characters suitable for passing to lower-level POSIX style APIs. The string is provided in the representation most appropriate for the filesystem in question.
  */
-- (__strong const char *)fileSystemRepresentationWithPath:(NSString *)path NS_RETURNS_INNER_POINTER;
+- (const char *)fileSystemRepresentationWithPath:(NSString *)path NS_RETURNS_INNER_POINTER;
 
 /* stringWithFileSystemRepresentation:length: returns an NSString created from an array of bytes that are in the filesystem representation.
  */
@@ -273,7 +284,7 @@
     If `backupItemName` is provided, that name will be used to create a backup of the original item. The backup is placed in the same directory as the original item. If an error occurs during the creation of the backup item, the operation will fail. If there is already an item with the same name as the backup item, that item will be removed. The backup item will be removed in the event of success unless the `NSFileManagerItemReplacementWithoutDeletingBackupItem` option is provided in `options`.
     For `options`, pass `0` to get the default behavior, which uses only the metadata from the new item while adjusting some properties using values from the original item. Pass `NSFileManagerItemReplacementUsingNewMetadataOnly` in order to use all possible metadata from the new item.
  */
-- (BOOL)replaceItemAtURL:(NSURL *)originalItemURL withItemAtURL:(NSURL *)newItemURL backupItemName:(nullable NSString *)backupItemName options:(NSFileManagerItemReplacementOptions)options resultingItemURL:(NSURL * __nullable * __nullable)resultingURL error:(NSError **)error NS_AVAILABLE(10_6, 4_0);
+- (BOOL)replaceItemAtURL:(NSURL *)originalItemURL withItemAtURL:(NSURL *)newItemURL backupItemName:(nullable NSString *)backupItemName options:(NSFileManagerItemReplacementOptions)options resultingItemURL:(NSURL * _Nullable * _Nullable)resultingURL error:(NSError **)error NS_AVAILABLE(10_6, 4_0);
 
 
 /* Changes whether the item for the specified URL is ubiquitous and moves the item to the destination URL. When making an item ubiquitous, the destination URL must be prefixed with a URL from -URLForUbiquityContainerIdentifier:. Returns YES if the change is successful, NO otherwise.
@@ -298,7 +309,7 @@
 
 /* Returns a URL that can be shared with other users to allow them download a copy of the specified ubiquitous item. Also returns the date after which the item will no longer be accessible at the returned URL. The URL must be prefixed with a URL from -URLForUbiquityContainerIdentifier:.
  */
-- (nullable NSURL *)URLForPublishingUbiquitousItemAtURL:(NSURL *)url expirationDate:(NSDate * __nullable * __nullable)outDate error:(NSError **)error NS_AVAILABLE(10_7, 5_0);
+- (nullable NSURL *)URLForPublishingUbiquitousItemAtURL:(NSURL *)url expirationDate:(NSDate * _Nullable * _Nullable)outDate error:(NSError **)error NS_AVAILABLE(10_7, 5_0);
 
 /* Returns an opaque token that represents the current ubiquity identity. This object can be copied, encoded, or compared with isEqual:. When ubiquity containers are unavailable because the user has disabled them, or when the user is simply not logged in, this method will return nil. The NSUbiquityIdentityDidChangeNotification notification is posted after this value changes.
 
@@ -313,6 +324,15 @@
 
 @end
 
+@interface NSFileManager (NSUserInformation)
+
+@property (readonly, copy) NSURL *homeDirectoryForCurrentUser API_AVAILABLE(macosx(10.12)) API_UNAVAILABLE(ios, watchos, tvos);
+@property (readonly, copy) NSURL *temporaryDirectory API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+- (nullable NSURL *)homeDirectoryForUser:(NSString *)userName API_AVAILABLE(macosx(10.12)) API_UNAVAILABLE(ios, watchos, tvos);
+
+@end
+
 /* These delegate methods are for the use of the deprecated handler-taking methods on NSFileManager for copying, moving, linking or deleting files.
  */
 @interface NSObject (NSCopyLinkMoveHandler)
@@ -402,42 +422,42 @@
 
 @end
 
-FOUNDATION_EXPORT NSString * const NSFileType;
-FOUNDATION_EXPORT NSString * const NSFileTypeDirectory;
-FOUNDATION_EXPORT NSString * const NSFileTypeRegular;
-FOUNDATION_EXPORT NSString * const NSFileTypeSymbolicLink;
-FOUNDATION_EXPORT NSString * const NSFileTypeSocket;
-FOUNDATION_EXPORT NSString * const NSFileTypeCharacterSpecial;
-FOUNDATION_EXPORT NSString * const NSFileTypeBlockSpecial;
-FOUNDATION_EXPORT NSString * const NSFileTypeUnknown;
-FOUNDATION_EXPORT NSString * const NSFileSize;
-FOUNDATION_EXPORT NSString * const NSFileModificationDate;
-FOUNDATION_EXPORT NSString * const NSFileReferenceCount;
-FOUNDATION_EXPORT NSString * const NSFileDeviceIdentifier;
-FOUNDATION_EXPORT NSString * const NSFileOwnerAccountName;
-FOUNDATION_EXPORT NSString * const NSFileGroupOwnerAccountName;
-FOUNDATION_EXPORT NSString * const NSFilePosixPermissions;
-FOUNDATION_EXPORT NSString * const NSFileSystemNumber;
-FOUNDATION_EXPORT NSString * const NSFileSystemFileNumber;
-FOUNDATION_EXPORT NSString * const NSFileExtensionHidden;
-FOUNDATION_EXPORT NSString * const NSFileHFSCreatorCode;
-FOUNDATION_EXPORT NSString * const NSFileHFSTypeCode;
-FOUNDATION_EXPORT NSString * const NSFileImmutable;
-FOUNDATION_EXPORT NSString * const NSFileAppendOnly;
-FOUNDATION_EXPORT NSString * const NSFileCreationDate;
-FOUNDATION_EXPORT NSString * const NSFileOwnerAccountID;
-FOUNDATION_EXPORT NSString * const NSFileGroupOwnerAccountID;
-FOUNDATION_EXPORT NSString * const NSFileBusy;
-FOUNDATION_EXPORT NSString * const NSFileProtectionKey NS_AVAILABLE_IOS(4_0);
-FOUNDATION_EXPORT NSString * const NSFileProtectionNone NS_AVAILABLE_IOS(4_0);
-FOUNDATION_EXPORT NSString * const NSFileProtectionComplete NS_AVAILABLE_IOS(4_0);
-FOUNDATION_EXPORT NSString * const NSFileProtectionCompleteUnlessOpen NS_AVAILABLE_IOS(5_0);
-FOUNDATION_EXPORT NSString * const NSFileProtectionCompleteUntilFirstUserAuthentication NS_AVAILABLE_IOS(5_0);
-
-FOUNDATION_EXPORT NSString * const NSFileSystemSize;
-FOUNDATION_EXPORT NSString * const NSFileSystemFreeSize;
-FOUNDATION_EXPORT NSString * const NSFileSystemNodes;
-FOUNDATION_EXPORT NSString * const NSFileSystemFreeNodes;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileType;
+FOUNDATION_EXPORT NSFileAttributeType const NSFileTypeDirectory;
+FOUNDATION_EXPORT NSFileAttributeType const NSFileTypeRegular;
+FOUNDATION_EXPORT NSFileAttributeType const NSFileTypeSymbolicLink;
+FOUNDATION_EXPORT NSFileAttributeType const NSFileTypeSocket;
+FOUNDATION_EXPORT NSFileAttributeType const NSFileTypeCharacterSpecial;
+FOUNDATION_EXPORT NSFileAttributeType const NSFileTypeBlockSpecial;
+FOUNDATION_EXPORT NSFileAttributeType const NSFileTypeUnknown;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileSize;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileModificationDate;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileReferenceCount;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileDeviceIdentifier;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileOwnerAccountName;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileGroupOwnerAccountName;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFilePosixPermissions;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileSystemNumber;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileSystemFileNumber;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileExtensionHidden;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileHFSCreatorCode;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileHFSTypeCode;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileImmutable;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileAppendOnly;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileCreationDate;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileOwnerAccountID;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileGroupOwnerAccountID;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileBusy;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileProtectionKey NS_AVAILABLE_IOS(4_0);
+FOUNDATION_EXPORT NSFileProtectionType const NSFileProtectionNone NS_AVAILABLE_IOS(4_0);
+FOUNDATION_EXPORT NSFileProtectionType const NSFileProtectionComplete NS_AVAILABLE_IOS(4_0);
+FOUNDATION_EXPORT NSFileProtectionType const NSFileProtectionCompleteUnlessOpen NS_AVAILABLE_IOS(5_0);
+FOUNDATION_EXPORT NSFileProtectionType const NSFileProtectionCompleteUntilFirstUserAuthentication NS_AVAILABLE_IOS(5_0);
+
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileSystemSize;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileSystemFreeSize;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileSystemNodes;
+FOUNDATION_EXPORT NSFileAttributeKey const NSFileSystemFreeNodes;
 
 @interface NSDictionary<KeyType, ObjectType> (NSFileAttributes)
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFilePresenter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFilePresenter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFilePresenter.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFilePresenter.h	2016-05-20 06:25:33.000000000 +0200
@@ -42,13 +42,13 @@
 
 A common sequence that your NSFilePresenter must handle is the file coordination mechanism sending this message, then sending -savePresentedItemChangesWithCompletionHandler:, and then, after you have invoked that completion handler, invoking your reacquirer.
 */
-- (void)relinquishPresentedItemToReader:(void (^)(void (^ __nullable reacquirer)(void)))reader;
+- (void)relinquishPresentedItemToReader:(void (^)(void (^ _Nullable reacquirer)(void)))reader;
 
 /* Given that something in the system is waiting to write to the presented file or directory, do whatever it takes to ensure that the application will behave properly while that writing is happening, and then invoke the completion handler. The definition of "properly" depends on what kind of ownership model the application implements. Implementations of this method must always invoke the passed-in writer block because other parts of the system will wait until it is invoked or until the user loses patience and cancels the waiting. When an implementation of this method invokes the passed-in block it can pass that block yet another block, which will be invoked in the receiver's operation queue when writing is complete.
 
 A common sequence that your NSFilePresenter must handle is the file coordination mechanism sending this message, then sending -accommodatePresentedItemDeletionWithCompletionHandler: or -savePresentedItemChangesWithCompletionHandler:, and then, after you have invoked that completion handler, invoking your reacquirer. It is also common for your NSFilePresenter to be sent a combination of the -presented... messages listed below in between relinquishing and reacquiring.
 */
-- (void)relinquishPresentedItemToWriter:(void (^)(void (^ __nullable reacquirer)(void)))writer;
+- (void)relinquishPresentedItemToWriter:(void (^)(void (^ _Nullable reacquirer)(void)))writer;
 
 /* Given that something in the system is waiting to read from the presented file or directory, do whatever it takes to ensure that the contents of the presented file or directory is completely up to date, and then invoke the completion handler. If successful (including when there is simply nothing to do) pass nil to the completion handler, or if not successful pass an NSError that encapsulates the reason why saving failed. Implementations of this method must always invoke the completion handler because other parts of the system will wait until it is invoked or the user loses patience and cancels the waiting. If this method is not implemented then the NSFilePresenter is assumed to be one that never lets the user make changes that need to be saved.
 
@@ -56,7 +56,7 @@
 
 The file coordination mechanism does not always send -relinquishPresentedItemToReader: or -relinquishPresentedItemToWriter: to your NSFilePresenter before sending this message. For example, other process' use of -[NSFileCoordinator prepareForReadingItemsAtURLs:options:writingItemsAtURLs:options:error:byAccessor:] can cause this to happen.
 */
-- (void)savePresentedItemChangesWithCompletionHandler:(void (^)(NSError * __nullable errorOrNil))completionHandler;
+- (void)savePresentedItemChangesWithCompletionHandler:(void (^)(NSError * _Nullable errorOrNil))completionHandler;
 
 /* Given that something in the system is waiting to delete the presented file or directory, do whatever it takes to ensure that the deleting will succeed and that the receiver's application will behave properly when the deleting has happened, and then invoke the completion handler. If successful (including when there is simply nothing to do) pass nil to the completion handler, or if not successful pass an NSError that encapsulates the reason why preparation failed. Implementations of this method must always invoke the completion handler because other parts of the system will wait until it is invoked or until the user loses patience and cancels the waiting.
 
@@ -64,7 +64,7 @@
 
 The file coordination mechanism does not always send -relinquishPresentedItemToReader: or -relinquishPresentedItemToWriter: to your NSFilePresenter before sending this message. For example, other process' use of -[NSFileCoordinator prepareForReadingItemsAtURLs:options:writingItemsAtURLs:options:error:byAccessor:] can cause this to happen.
 */
-- (void)accommodatePresentedItemDeletionWithCompletionHandler:(void (^)(NSError * __nullable errorOrNil))completionHandler;
+- (void)accommodatePresentedItemDeletionWithCompletionHandler:(void (^)(NSError * _Nullable errorOrNil))completionHandler;
 
 /* Be notified that the file or directory has been moved or renamed, or a directory containing it has been moved or renamed. A typical implementation of this method will cause subsequent invocations of -presentedItemURL to return the new URL.
 
@@ -106,7 +106,7 @@
 
 The file coordination mechanism does not always send -relinquishPresentedItemToReader: or -relinquishPresentedItemToWriter: to your NSFilePresenter before sending this message. For example, other process' use of -[NSFileCoordinator prepareForReadingItemsAtURLs:options:writingItemsAtURLs:options:error:byAccessor:] can cause this to happen.
 */
-- (void)accommodatePresentedSubitemDeletionAtURL:(NSURL *)url completionHandler:(void (^)(NSError * __nullable errorOrNil))completionHandler;
+- (void)accommodatePresentedSubitemDeletionAtURL:(NSURL *)url completionHandler:(void (^)(NSError * _Nullable errorOrNil))completionHandler;
 
 /* Be notified that a file or directory contained by the directory has been added. If this method is not implemented but -presentedItemDidChange is, and the directory is actually a file package, then the file coordination machinery will invoke -presentedItemDidChange instead.
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileVersion.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileVersion.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileVersion.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFileVersion.h	2016-05-20 06:13:48.000000000 +0200
@@ -6,7 +6,7 @@
 
 #import <Foundation/NSObject.h>
 
-@class NSArray<ObjectType>, NSDate, NSDictionary, NSError, NSString, NSURL;
+@class NSArray<ObjectType>, NSDate, NSDictionary, NSError, NSString, NSURL, NSPersonNameComponents;
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -64,7 +64,7 @@
  
 If you need to get all versions for a document, both local and non-local, you should use an NSFilePresenter that implements -presentedItemDidGainVersion: and -presentedItemDidLoseVersion: and invoke +[NSFileCoordinator addFilePresenter:], +[NSFileVersion otherVersionsOfItemAtURL:], and this method within a single coordinated read.
 */
-+ (void)getNonlocalVersionsOfItemAtURL:(NSURL *)url completionHandler:(void (^)(NSArray<NSFileVersion *> * __nullable nonlocalFileVersions, NSError * __nullable error))completionHandler NS_AVAILABLE(10_10, 8_0);
++ (void)getNonlocalVersionsOfItemAtURL:(NSURL *)url completionHandler:(void (^)(NSArray<NSFileVersion *> * _Nullable nonlocalFileVersions, NSError * _Nullable error))completionHandler NS_AVAILABLE(10_10, 8_0);
 
 /* For a file located by a URL, return the NSFileVersion identified by a persistent identifier of the sort returned by -persistentIdentifier, or nil if the version no longer exists.
 */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFormatter.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSFormatter.h	2016-05-20 06:24:14.000000000 +0200
@@ -46,18 +46,18 @@
 
 @interface NSFormatter : NSObject <NSCopying, NSCoding>
 
-- (nullable NSString *)stringForObjectValue:(id)obj;
+- (nullable NSString *)stringForObjectValue:(nullable id)obj;
 
 - (nullable NSAttributedString *)attributedStringForObjectValue:(id)obj withDefaultAttributes:(nullable NSDictionary<NSString *, id> *)attrs;
 
 - (nullable NSString *)editingStringForObjectValue:(id)obj;
 
-- (BOOL)getObjectValue:(out id __nullable * __nullable)obj forString:(NSString *)string errorDescription:(out NSString * __nullable * __nullable)error;
+- (BOOL)getObjectValue:(out id _Nullable * _Nullable)obj forString:(NSString *)string errorDescription:(out NSString * _Nullable * _Nullable)error;
 
-- (BOOL)isPartialStringValid:(NSString *)partialString newEditingString:(NSString * __nullable * __nullable)newString errorDescription:(NSString * __nullable * __nullable)error;
+- (BOOL)isPartialStringValid:(NSString *)partialString newEditingString:(NSString * _Nullable * _Nullable)newString errorDescription:(NSString * _Nullable * _Nullable)error;
     // Compatibility method.  If a subclass overrides this and does not override the new method below, this will be called as before (the new method just calls this one by default).  The selection range will always be set to the end of the text with this method if replacement occurs.
 
-- (BOOL)isPartialStringValid:(NSString * __nonnull * __nonnull)partialStringPtr proposedSelectedRange:(nullable NSRangePointer)proposedSelRangePtr originalString:(NSString *)origString originalSelectedRange:(NSRange)origSelRange errorDescription:(NSString * __nullable * __nullable)error;
+- (BOOL)isPartialStringValid:(NSString * _Nonnull * _Nonnull)partialStringPtr proposedSelectedRange:(nullable NSRangePointer)proposedSelRangePtr originalString:(NSString *)origString originalSelectedRange:(NSRange)origSelRange errorDescription:(NSString * _Nullable * _Nullable)error;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHTTPCookie.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHTTPCookie.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHTTPCookie.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHTTPCookie.h	2016-05-20 07:35:40.000000000 +0200
@@ -14,85 +14,87 @@
 @class NSString;
 @class NSURL;
 
+typedef NSString * NSHTTPCookiePropertyKey NS_EXTENSIBLE_STRING_ENUM;
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*!
     @const NSHTTPCookieName
     @discussion Key for cookie name
 */
-FOUNDATION_EXPORT NSString * const NSHTTPCookieName;
+FOUNDATION_EXPORT NSHTTPCookiePropertyKey const NSHTTPCookieName;
 
 /*!
     @const NSHTTPCookieValue
     @discussion Key for cookie value
 */
-FOUNDATION_EXPORT NSString * const NSHTTPCookieValue;
+FOUNDATION_EXPORT NSHTTPCookiePropertyKey const NSHTTPCookieValue;
 
 /*!
     @const NSHTTPCookieOriginURL
     @discussion Key for cookie origin URL
 */
-FOUNDATION_EXPORT NSString * const NSHTTPCookieOriginURL;
+FOUNDATION_EXPORT NSHTTPCookiePropertyKey const NSHTTPCookieOriginURL;
 
 /*!
     @const NSHTTPCookieVersion
     @discussion Key for cookie version
 */
-FOUNDATION_EXPORT NSString * const NSHTTPCookieVersion;
+FOUNDATION_EXPORT NSHTTPCookiePropertyKey const NSHTTPCookieVersion;
 
 /*!
     @const NSHTTPCookieDomain
     @discussion Key for cookie domain
 */
-FOUNDATION_EXPORT NSString * const NSHTTPCookieDomain;
+FOUNDATION_EXPORT NSHTTPCookiePropertyKey const NSHTTPCookieDomain;
 
 /*!
     @const NSHTTPCookiePath
     @discussion Key for cookie path
 */
-FOUNDATION_EXPORT NSString * const NSHTTPCookiePath;
+FOUNDATION_EXPORT NSHTTPCookiePropertyKey const NSHTTPCookiePath;
 
 /*!
     @const NSHTTPCookieSecure
     @discussion Key for cookie secure flag
 */
-FOUNDATION_EXPORT NSString * const NSHTTPCookieSecure;
+FOUNDATION_EXPORT NSHTTPCookiePropertyKey const NSHTTPCookieSecure;
 
 /*!
     @const NSHTTPCookieExpires
     @discussion Key for cookie expiration date
 */
-FOUNDATION_EXPORT NSString * const NSHTTPCookieExpires;
+FOUNDATION_EXPORT NSHTTPCookiePropertyKey const NSHTTPCookieExpires;
 
 /*!
     @const NSHTTPCookieComment
     @discussion Key for cookie comment text
 */
-FOUNDATION_EXPORT NSString * const NSHTTPCookieComment;
+FOUNDATION_EXPORT NSHTTPCookiePropertyKey const NSHTTPCookieComment;
 
 /*!
     @const NSHTTPCookieCommentURL
     @discussion Key for cookie comment URL
 */
-FOUNDATION_EXPORT NSString * const NSHTTPCookieCommentURL;
+FOUNDATION_EXPORT NSHTTPCookiePropertyKey const NSHTTPCookieCommentURL;
 
 /*!
     @const NSHTTPCookieDiscard
     @discussion Key for cookie discard (session-only) flag
 */
-FOUNDATION_EXPORT NSString * const NSHTTPCookieDiscard;
+FOUNDATION_EXPORT NSHTTPCookiePropertyKey const NSHTTPCookieDiscard;
 
 /*!
     @const NSHTTPCookieMaximumAge
     @discussion Key for cookie maximum age (an alternate way of specifying the expiration)
 */
-FOUNDATION_EXPORT NSString * const NSHTTPCookieMaximumAge;
+FOUNDATION_EXPORT NSHTTPCookiePropertyKey const NSHTTPCookieMaximumAge;
 
 /*!
     @const NSHTTPCookiePort
     @discussion Key for cookie ports
 */
-FOUNDATION_EXPORT NSString * const NSHTTPCookiePort;
+FOUNDATION_EXPORT NSHTTPCookiePropertyKey const NSHTTPCookiePort;
 
 
 @class NSHTTPCookieInternal;
@@ -235,7 +237,7 @@
     dictionary keys is invalid, for example because a required key is
     missing, or a recognized key maps to an illegal value.
 */
-- (nullable instancetype)initWithProperties:(NSDictionary<NSString *, id> *)properties;
+- (nullable instancetype)initWithProperties:(NSDictionary<NSHTTPCookiePropertyKey, id> *)properties;
 
 /*!
     @method cookieWithProperties:
@@ -250,7 +252,7 @@
     a required key is missing, or a recognized key maps to an illegal
     value.
 */
-+ (nullable NSHTTPCookie *)cookieWithProperties:(NSDictionary<NSString *, id> *)properties;
++ (nullable NSHTTPCookie *)cookieWithProperties:(NSDictionary<NSHTTPCookiePropertyKey, id> *)properties;
 
 /*!
     @method requestHeaderFieldsWithCookies:
@@ -285,7 +287,7 @@
     for descriptions of the supported keys and values.
     @result The dictionary representation of the receiver.
 */
-@property (nullable, readonly, copy) NSDictionary<NSString *, id> *properties;
+@property (nullable, readonly, copy) NSDictionary<NSHTTPCookiePropertyKey, id> *properties;
 
 /*!
     @method version
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHTTPCookieStorage.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHTTPCookieStorage.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHTTPCookieStorage.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHTTPCookieStorage.h	2016-05-20 07:35:40.000000000 +0200
@@ -6,6 +6,7 @@
 */
 
 #import <Foundation/NSObject.h>
+#import <Foundation/NSNotification.h>
 
 @class NSArray<ObjectType>;
 @class NSHTTPCookie;
@@ -147,7 +148,7 @@
 
 @interface NSHTTPCookieStorage (NSURLSessionTaskAdditions)
 - (void)storeCookies:(NSArray<NSHTTPCookie *> *)cookies forTask:(NSURLSessionTask *)task NS_AVAILABLE(10_10, 8_0);
-- (void)getCookiesForTask:(NSURLSessionTask *)task completionHandler:(void (^) (NSArray<NSHTTPCookie *> * __nullable cookies))completionHandler NS_AVAILABLE(10_10, 8_0);
+- (void)getCookiesForTask:(NSURLSessionTask *)task completionHandler:(void (^) (NSArray<NSHTTPCookie *> * _Nullable cookies))completionHandler NS_AVAILABLE(10_10, 8_0);
 @end
 
 /*!
@@ -156,12 +157,12 @@
     distributed notification center whenever the accept cookies
     preference is changed
 */
-FOUNDATION_EXPORT NSString * const NSHTTPCookieManagerAcceptPolicyChangedNotification;
+FOUNDATION_EXPORT NSNotificationName const NSHTTPCookieManagerAcceptPolicyChangedNotification;
 
 /*!
     @const NSHTTPCookieManagerCookiesChangedNotification
     @abstract Notification sent when the set of cookies changes
 */
-FOUNDATION_EXPORT NSString * const NSHTTPCookieManagerCookiesChangedNotification;
+FOUNDATION_EXPORT NSNotificationName const NSHTTPCookieManagerCookiesChangedNotification;
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHashTable.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHashTable.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHashTable.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSHashTable.h	2016-05-20 06:24:14.000000000 +0200
@@ -82,19 +82,19 @@
 
 /****************	(void *) Hash table operations	****************/
 
-typedef struct {NSUInteger _pi; NSUInteger _si; void * __nullable _bs;} NSHashEnumerator;
+typedef struct {NSUInteger _pi; NSUInteger _si; void * _Nullable _bs;} NSHashEnumerator;
 
 FOUNDATION_EXPORT void NSFreeHashTable(NSHashTable *table);
 FOUNDATION_EXPORT void NSResetHashTable(NSHashTable *table);
 FOUNDATION_EXPORT BOOL NSCompareHashTables(NSHashTable *table1, NSHashTable *table2);
-FOUNDATION_EXPORT NSHashTable *NSCopyHashTableWithZone(NSHashTable *table, NSZone * __nullable zone);
-FOUNDATION_EXPORT void *NSHashGet(NSHashTable *table, const void * __nullable pointer);
-FOUNDATION_EXPORT void NSHashInsert(NSHashTable *table, const void * __nullable pointer);
-FOUNDATION_EXPORT void NSHashInsertKnownAbsent(NSHashTable *table, const void * __nullable pointer);
-FOUNDATION_EXPORT void * __nullable NSHashInsertIfAbsent(NSHashTable *table, const void * __nullable pointer);
-FOUNDATION_EXPORT void NSHashRemove(NSHashTable *table, const void * __nullable pointer);
+FOUNDATION_EXPORT NSHashTable *NSCopyHashTableWithZone(NSHashTable *table, NSZone * _Nullable zone);
+FOUNDATION_EXPORT void *NSHashGet(NSHashTable *table, const void * _Nullable pointer);
+FOUNDATION_EXPORT void NSHashInsert(NSHashTable *table, const void * _Nullable pointer);
+FOUNDATION_EXPORT void NSHashInsertKnownAbsent(NSHashTable *table, const void * _Nullable pointer);
+FOUNDATION_EXPORT void * _Nullable NSHashInsertIfAbsent(NSHashTable *table, const void * _Nullable pointer);
+FOUNDATION_EXPORT void NSHashRemove(NSHashTable *table, const void * _Nullable pointer);
 FOUNDATION_EXPORT NSHashEnumerator NSEnumerateHashTable(NSHashTable *table);
-FOUNDATION_EXPORT void * __nullable NSNextHashEnumeratorItem(NSHashEnumerator *enumerator);
+FOUNDATION_EXPORT void * _Nullable NSNextHashEnumeratorItem(NSHashEnumerator *enumerator);
 FOUNDATION_EXPORT void NSEndHashTableEnumeration(NSHashEnumerator *enumerator);
 FOUNDATION_EXPORT NSUInteger NSCountHashTable(NSHashTable *table);
 FOUNDATION_EXPORT NSString *NSStringFromHashTable(NSHashTable *table);
@@ -104,14 +104,14 @@
 /****************	Legacy	****************/
 
 typedef struct {
-    NSUInteger	(* __nullable hash)(NSHashTable *table, const void *);
-    BOOL	(* __nullable isEqual)(NSHashTable *table, const void *, const void *);
-    void	(* __nullable retain)(NSHashTable *table, const void *);
-    void	(* __nullable release)(NSHashTable *table, void *);
-    NSString 	* __nullable (* __nullable describe)(NSHashTable *table, const void *);
+    NSUInteger	(* _Nullable hash)(NSHashTable *table, const void *);
+    BOOL	(* _Nullable isEqual)(NSHashTable *table, const void *, const void *);
+    void	(* _Nullable retain)(NSHashTable *table, const void *);
+    void	(* _Nullable release)(NSHashTable *table, void *);
+    NSString 	* _Nullable (* _Nullable describe)(NSHashTable *table, const void *);
 } NSHashTableCallBacks;
 
-FOUNDATION_EXPORT NSHashTable *NSCreateHashTableWithZone(NSHashTableCallBacks callBacks, NSUInteger capacity, NSZone * __nullable zone);
+FOUNDATION_EXPORT NSHashTable *NSCreateHashTableWithZone(NSHashTableCallBacks callBacks, NSUInteger capacity, NSZone * _Nullable zone);
 FOUNDATION_EXPORT NSHashTable *NSCreateHashTable(NSHashTableCallBacks callBacks, NSUInteger capacity);
 
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSISO8601DateFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSISO8601DateFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSISO8601DateFormatter.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSISO8601DateFormatter.h	2016-05-20 07:24:14.000000000 +0200
@@ -0,0 +1,70 @@
+/*
+    NSISO8601DateFormatter.h
+    Copyright © 2015
+    All rights reserved.
+ */
+
+#include <CoreFoundation/CFDateFormatter.h>
+#import <Foundation/NSFormatter.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class NSString, NSDate, NSTimeZone;
+
+typedef NS_OPTIONS(NSUInteger, NSISO8601DateFormatOptions) {
+    /* The format for year is inferred based on whether or not the week of year option is specified.
+     - if week of year is present, "YYYY" is used to display week dates.
+     - if week of year is not present, "yyyy" is used by default.
+     */
+    NSISO8601DateFormatWithYear API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = kCFISO8601DateFormatWithYear,
+    NSISO8601DateFormatWithMonth API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = kCFISO8601DateFormatWithMonth,
+
+    NSISO8601DateFormatWithWeekOfYear API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = kCFISO8601DateFormatWithWeekOfYear,  // This includes the "W" prefix (e.g. "W49")
+
+    /* The format for day is inferred based on provided options.
+     - if month is not present, day of year ("DDD") is used.
+     - if month is present, day of month ("dd") is used.
+     - if either weekOfMonth or weekOfYear is present, local day of week ("ee") is used.
+     */
+    NSISO8601DateFormatWithDay API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = kCFISO8601DateFormatWithDay,
+
+    NSISO8601DateFormatWithTime API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = kCFISO8601DateFormatWithTime,  // This uses the format "HH:mm:ss"
+    NSISO8601DateFormatWithTimeZone API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = kCFISO8601DateFormatWithTimeZone,
+
+    NSISO8601DateFormatWithSpaceBetweenDateAndTime API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = kCFISO8601DateFormatWithSpaceBetweenDateAndTime,  // Use space instead of "T"
+    NSISO8601DateFormatWithDashSeparatorInDate API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = kCFISO8601DateFormatWithDashSeparatorInDate,  // Add separator for date ("-")
+    NSISO8601DateFormatWithColonSeparatorInTime API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = kCFISO8601DateFormatWithColonSeparatorInTime,  // Add separator for time (":")
+    NSISO8601DateFormatWithColonSeparatorInTimeZone API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = kCFISO8601DateFormatWithColonSeparatorInTimeZone,  // Add ":" separator in timezone (e.g. +08:00)
+
+    NSISO8601DateFormatWithFullDate API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = kCFISO8601DateFormatWithFullDate,
+    NSISO8601DateFormatWithFullTime API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = kCFISO8601DateFormatWithFullTime,
+
+    NSISO8601DateFormatWithInternetDateTime API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)) = kCFISO8601DateFormatWithInternetDateTime,  // RFC 3339
+};
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSISO8601DateFormatter : NSFormatter <NSSecureCoding> {
+@private
+    CFDateFormatterRef _formatter;
+    NSTimeZone *_timeZone;
+    NSISO8601DateFormatOptions _formatOptions;
+}
+
+/* Please note that there can be a significant performance cost when resetting these properties.  Resetting each property can result in regenerating the entire CFDateFormatterRef, which can be very expensive. */
+@property (null_resettable, copy) NSTimeZone *timeZone;  // The default time zone is GMT.
+
+@property NSISO8601DateFormatOptions formatOptions;
+
+/* This init method creates a formatter object set to the GMT time zone and preconfigured with the RFC 3339 standard format ("yyyy-MM-dd'T'HH:mm:ssXXXXX") using the following options:
+ NSISO8601DateFormatWithInternetDateTime | NSISO8601DateFormatWithDashSeparatorInDate | NSISO8601DateFormatWithColonSeparatorInTime | NSISO8601DateFormatWithColonSeparatorInTimeZone
+ */
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
+
+- (NSString *)stringFromDate:(NSDate *)date;
+- (NSDate *)dateFromString:(NSString *)string;
+
++ (NSString *)stringFromDate:(NSDate *)date timeZone:(NSTimeZone *)timeZone formatOptions:(NSISO8601DateFormatOptions)formatOptions;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSIndexPath.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSIndexPath.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSIndexPath.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSIndexPath.h	2016-05-20 06:24:14.000000000 +0200
@@ -9,7 +9,7 @@
 
 @interface NSIndexPath : NSObject <NSCopying, NSSecureCoding> {
 	@private
-	__strong NSUInteger *_indexes;
+	NSUInteger *_indexes;
 #if !__OBJC2__
 	NSUInteger _hash;
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSIndexSet.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSIndexSet.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSIndexSet.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSIndexSet.h	2016-05-20 06:12:55.000000000 +0200
@@ -41,7 +41,7 @@
             NSRange _range;
         } _singleRange;
         struct {
-            void *  __strong _data;
+            void * _data;
             void *_reserved;
         } _multipleRanges;
     } _internal;
@@ -81,26 +81,26 @@
 
 - (BOOL)intersectsIndexesInRange:(NSRange)range;
 
-- (void)enumerateIndexesUsingBlock:(void (^)(NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
-- (void)enumerateIndexesWithOptions:(NSEnumerationOptions)opts usingBlock:(void (^)(NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
-- (void)enumerateIndexesInRange:(NSRange)range options:(NSEnumerationOptions)opts usingBlock:(void (^)(NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
-
-- (NSUInteger)indexPassingTest:(BOOL (^)(NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
-- (NSUInteger)indexWithOptions:(NSEnumerationOptions)opts passingTest:(BOOL (^)(NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
-- (NSUInteger)indexInRange:(NSRange)range options:(NSEnumerationOptions)opts passingTest:(BOOL (^)(NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
-
-- (NSIndexSet *)indexesPassingTest:(BOOL (^)(NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
-- (NSIndexSet *)indexesWithOptions:(NSEnumerationOptions)opts passingTest:(BOOL (^)(NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
-- (NSIndexSet *)indexesInRange:(NSRange)range options:(NSEnumerationOptions)opts passingTest:(BOOL (^)(NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
+- (void)enumerateIndexesUsingBlock:(void (NS_NOESCAPE ^)(NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
+- (void)enumerateIndexesWithOptions:(NSEnumerationOptions)opts usingBlock:(void (NS_NOESCAPE ^)(NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
+- (void)enumerateIndexesInRange:(NSRange)range options:(NSEnumerationOptions)opts usingBlock:(void (NS_NOESCAPE ^)(NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
+
+- (NSUInteger)indexPassingTest:(BOOL (NS_NOESCAPE ^)(NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
+- (NSUInteger)indexWithOptions:(NSEnumerationOptions)opts passingTest:(BOOL (NS_NOESCAPE ^)(NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
+- (NSUInteger)indexInRange:(NSRange)range options:(NSEnumerationOptions)opts passingTest:(BOOL (NS_NOESCAPE ^)(NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
+
+- (NSIndexSet *)indexesPassingTest:(BOOL (NS_NOESCAPE ^)(NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
+- (NSIndexSet *)indexesWithOptions:(NSEnumerationOptions)opts passingTest:(BOOL (NS_NOESCAPE ^)(NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
+- (NSIndexSet *)indexesInRange:(NSRange)range options:(NSEnumerationOptions)opts passingTest:(BOOL (NS_NOESCAPE ^)(NSUInteger idx, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
 
 /*
  The following three convenience methods allow you to enumerate the indexes in the receiver by ranges of contiguous indexes. The performance of these methods is not guaranteed to be any better than if they were implemented with enumerateIndexesInRange:options:usingBlock:. However, depending on the receiver's implementation, they may perform better than that.
  
  If the specified range for enumeration intersects a range of contiguous indexes in the receiver, then the block will be invoked with the intersection of those two ranges.
 */
-- (void)enumerateRangesUsingBlock:(void (^)(NSRange range, BOOL *stop))block NS_AVAILABLE(10_7, 5_0);
-- (void)enumerateRangesWithOptions:(NSEnumerationOptions)opts usingBlock:(void (^)(NSRange range, BOOL *stop))block NS_AVAILABLE(10_7, 5_0);
-- (void)enumerateRangesInRange:(NSRange)range options:(NSEnumerationOptions)opts usingBlock:(void (^)(NSRange range, BOOL *stop))block NS_AVAILABLE(10_7, 5_0);
+- (void)enumerateRangesUsingBlock:(void (NS_NOESCAPE ^)(NSRange range, BOOL *stop))block NS_AVAILABLE(10_7, 5_0);
+- (void)enumerateRangesWithOptions:(NSEnumerationOptions)opts usingBlock:(void (NS_NOESCAPE ^)(NSRange range, BOOL *stop))block NS_AVAILABLE(10_7, 5_0);
+- (void)enumerateRangesInRange:(NSRange)range options:(NSEnumerationOptions)opts usingBlock:(void (NS_NOESCAPE ^)(NSRange range, BOOL *stop))block NS_AVAILABLE(10_7, 5_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSInvocation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSInvocation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSInvocation.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSInvocation.h	2016-05-20 06:24:14.000000000 +0200
@@ -12,8 +12,8 @@
 NS_SWIFT_UNAVAILABLE("NSInvocation and related APIs not available")
 @interface NSInvocation : NSObject {
 @private
-    __strong void *_frame;
-    __strong void *_retdata;
+    void *_frame;
+    void *_retdata;
     id _signature;
     id _container;
     uint8_t _retainedArgs;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyValueCoding.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyValueCoding.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyValueCoding.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyValueCoding.h	2016-05-20 07:39:55.000000000 +0200
@@ -7,6 +7,7 @@
 #import <Foundation/NSDictionary.h>
 #import <Foundation/NSOrderedSet.h>
 #import <Foundation/NSSet.h>
+#import <Foundation/NSException.h>
 
 @class NSError, NSString;
 
@@ -18,21 +19,23 @@
 
 The actual value of this constant string is "NSUnknownKeyException," to match the exceptions that are thrown by KVC methods that were deprecated in Mac OS 10.3.
 */
-FOUNDATION_EXPORT NSString *const NSUndefinedKeyException;
+FOUNDATION_EXPORT NSExceptionName const NSUndefinedKeyException;
+
+typedef NSString * NSKeyValueOperator NS_STRING_ENUM;
 
 /* Strings for the names of array operators supported by key-value coding. Only these string declarations are new in Mac OS 10.4. The actual support for array operators appeared in Mac OS 10.3. The values of these do not include "@" prefixes.
 */
-FOUNDATION_EXPORT NSString *const NSAverageKeyValueOperator;
-FOUNDATION_EXPORT NSString *const NSCountKeyValueOperator;
-FOUNDATION_EXPORT NSString *const NSDistinctUnionOfArraysKeyValueOperator;
-FOUNDATION_EXPORT NSString *const NSDistinctUnionOfObjectsKeyValueOperator;
-FOUNDATION_EXPORT NSString *const NSDistinctUnionOfSetsKeyValueOperator;
-FOUNDATION_EXPORT NSString *const NSMaximumKeyValueOperator;
-FOUNDATION_EXPORT NSString *const NSMinimumKeyValueOperator;
-FOUNDATION_EXPORT NSString *const NSSumKeyValueOperator;
-FOUNDATION_EXPORT NSString *const NSUnionOfArraysKeyValueOperator;
-FOUNDATION_EXPORT NSString *const NSUnionOfObjectsKeyValueOperator;
-FOUNDATION_EXPORT NSString *const NSUnionOfSetsKeyValueOperator;
+FOUNDATION_EXPORT NSKeyValueOperator const NSAverageKeyValueOperator;
+FOUNDATION_EXPORT NSKeyValueOperator const NSCountKeyValueOperator;
+FOUNDATION_EXPORT NSKeyValueOperator const NSDistinctUnionOfArraysKeyValueOperator;
+FOUNDATION_EXPORT NSKeyValueOperator const NSDistinctUnionOfObjectsKeyValueOperator;
+FOUNDATION_EXPORT NSKeyValueOperator const NSDistinctUnionOfSetsKeyValueOperator;
+FOUNDATION_EXPORT NSKeyValueOperator const NSMaximumKeyValueOperator;
+FOUNDATION_EXPORT NSKeyValueOperator const NSMinimumKeyValueOperator;
+FOUNDATION_EXPORT NSKeyValueOperator const NSSumKeyValueOperator;
+FOUNDATION_EXPORT NSKeyValueOperator const NSUnionOfArraysKeyValueOperator;
+FOUNDATION_EXPORT NSKeyValueOperator const NSUnionOfObjectsKeyValueOperator;
+FOUNDATION_EXPORT NSKeyValueOperator const NSUnionOfSetsKeyValueOperator;
 
 @interface NSObject(NSKeyValueCoding)
 
@@ -76,7 +79,7 @@
 
 The default implementation of this method searches the class of the receiver for a validator method whose name matches the pattern -validate<Key>:error:. If such a method is found it is invoked and the result is returned. If no such method is found, YES is returned.
 */
-- (BOOL)validateValue:(inout id __nullable * __nonnull)ioValue forKey:(NSString *)inKey error:(out NSError **)outError;
+- (BOOL)validateValue:(inout id _Nullable * _Nonnull)ioValue forKey:(NSString *)inKey error:(out NSError **)outError;
 
 /* Given a key that identifies an _ordered_ to-many relationship, return a mutable array that provides read-write access to the related objects. Objects added to the mutable array will become related to the receiver, and objects removed from the mutable array will become unrelated.
 
@@ -118,7 +121,7 @@
 */
 - (nullable id)valueForKeyPath:(NSString *)keyPath;
 - (void)setValue:(nullable id)value forKeyPath:(NSString *)keyPath;
-- (BOOL)validateValue:(inout id __nullable * __nonnull)ioValue forKeyPath:(NSString *)inKeyPath error:(out NSError **)outError;
+- (BOOL)validateValue:(inout id _Nullable * _Nonnull)ioValue forKeyPath:(NSString *)inKeyPath error:(out NSError **)outError;
 - (NSMutableArray *)mutableArrayValueForKeyPath:(NSString *)keyPath;
 - (NSMutableOrderedSet *)mutableOrderedSetValueForKeyPath:(NSString *)keyPath NS_AVAILABLE(10_7, 5_0);
 - (NSMutableSet *)mutableSetValueForKeyPath:(NSString *)keyPath;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyValueObserving.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyValueObserving.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyValueObserving.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyValueObserving.h	2016-05-20 07:35:40.000000000 +0200
@@ -52,13 +52,14 @@
     NSKeyValueSetSetMutation = 4
 };
 
+typedef NSString * NSKeyValueChangeKey NS_STRING_ENUM;
 /* Keys for entries in change dictionaries. See the comments for -observeValueForKeyPath:ofObject:change:context: for more information.
 */
-FOUNDATION_EXPORT NSString *const NSKeyValueChangeKindKey;
-FOUNDATION_EXPORT NSString *const NSKeyValueChangeNewKey;
-FOUNDATION_EXPORT NSString *const NSKeyValueChangeOldKey;
-FOUNDATION_EXPORT NSString *const NSKeyValueChangeIndexesKey;
-FOUNDATION_EXPORT NSString *const NSKeyValueChangeNotificationIsPriorKey NS_AVAILABLE(10_5, 2_0);
+FOUNDATION_EXPORT NSKeyValueChangeKey const NSKeyValueChangeKindKey;
+FOUNDATION_EXPORT NSKeyValueChangeKey const NSKeyValueChangeNewKey;
+FOUNDATION_EXPORT NSKeyValueChangeKey const NSKeyValueChangeOldKey;
+FOUNDATION_EXPORT NSKeyValueChangeKey const NSKeyValueChangeIndexesKey;
+FOUNDATION_EXPORT NSKeyValueChangeKey const NSKeyValueChangeNotificationIsPriorKey NS_AVAILABLE(10_5, 2_0);
 
 @interface NSObject(NSKeyValueObserving)
 
@@ -77,7 +78,7 @@
 
 context is always the same pointer that was passed in at observer registration time.
 */
-- (void)observeValueForKeyPath:(nullable NSString *)keyPath ofObject:(nullable id)object change:(nullable NSDictionary<NSString*, id> *)change context:(nullable void *)context;
+- (void)observeValueForKeyPath:(nullable NSString *)keyPath ofObject:(nullable id)object change:(nullable NSDictionary<NSKeyValueChangeKey, id> *)change context:(nullable void *)context;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyedArchiver.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyedArchiver.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyedArchiver.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyedArchiver.h	2016-05-20 07:39:55.000000000 +0200
@@ -4,6 +4,7 @@
 
 #import <Foundation/NSCoder.h>
 #import <Foundation/NSPropertyList.h>
+#import <Foundation/NSException.h>
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
 #import <Foundation/NSGeometry.h>
 #endif
@@ -14,8 +15,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-FOUNDATION_EXPORT NSString * const NSInvalidArchiveOperationException;
-FOUNDATION_EXPORT NSString * const NSInvalidUnarchiveOperationException;
+FOUNDATION_EXPORT NSExceptionName const NSInvalidArchiveOperationException;
+FOUNDATION_EXPORT NSExceptionName const NSInvalidUnarchiveOperationException;
 // Archives created using the class method archivedRootDataWithObject used this key for the root object in the hierarchy of encoded objects. The NSKeyedUnarchiver class method unarchiveObjectWithData: will look for this root key as well. You can also use it as the key for the root object in your own archives.
 FOUNDATION_EXPORT NSString * const NSKeyedArchiveRootObjectKey NS_AVAILABLE(10_9, 7_0);
 
@@ -37,9 +38,12 @@
     NSUInteger _estimatedCount;
     void *_reserved2;
     id _visited;
-    void *  __strong _reserved0;
+    void *_reserved0;
 }
 
+/// Initialize the archiver with empty data, ready for writing.
+- (instancetype)init API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
 + (NSData *)archivedDataWithRootObject:(id)rootObject;
 + (BOOL)archiveRootObject:(id)rootObject toFile:(NSString *)path;
 
@@ -49,6 +53,9 @@
 
 @property NSPropertyListFormat outputFormat;
 
+/// If encoding has not yet finished, then invoking this property will call finishEncoding and return the data. If you initialized the keyed archiver with a specific mutable data instance, then it will be returned from this property after finishEncoding is called.
+@property (readonly, strong) NSData *encodedData API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
 - (void)finishEncoding;
 
 + (void)setClassName:(nullable NSString *)codedName forClass:(Class)cls;
@@ -91,7 +98,7 @@
     const uint8_t *_bytes;
     uint64_t _len;
     id _helper;
-    void *  __strong _reserved0;
+    void *_reserved0;
 }
 
 + (nullable id)unarchiveObjectWithData:(NSData *)data;
@@ -126,6 +133,8 @@
 // Enables secure coding support on this keyed unarchiver. When enabled, anarchiving a disallowed class throws an exception. Once enabled, attempting to set requiresSecureCoding to NO will throw an exception. This is to prevent classes from selectively turning secure coding off. This is designed to be set once at the top level and remain on. Note that the getter is on the superclass, NSCoder. See NSCoder for more information about secure coding.
 @property (readwrite) BOOL requiresSecureCoding NS_AVAILABLE(10_8, 6_0);
 
+@property (readwrite) NSDecodingFailurePolicy decodingFailurePolicy NS_AVAILABLE(10_11, 9_0);
+
 @end
 
 @protocol NSKeyedArchiverDelegate <NSObject>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLengthFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLengthFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLengthFormatter.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLengthFormatter.h	2016-05-20 06:24:14.000000000 +0200
@@ -42,7 +42,7 @@
 - (NSString *)unitStringFromMeters:(double)numberInMeters usedUnit:(nullable NSLengthFormatterUnit *)unitp;
 
 // No parsing is supported. This method will return NO.
-- (BOOL)getObjectValue:(out id __nullable * __nullable)obj forString:(NSString *)string errorDescription:(out NSString * __nullable * __nullable)error;
+- (BOOL)getObjectValue:(out id _Nullable * _Nullable)obj forString:(NSString *)string errorDescription:(out NSString * _Nullable * _Nullable)error;
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLinguisticTagger.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLinguisticTagger.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLinguisticTagger.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLinguisticTagger.h	2016-05-20 06:13:48.000000000 +0200
@@ -103,12 +103,12 @@
 
 /* The tagger will segment the string as needed into sentences and tokens, and return those ranges along with a tag for any scheme in its array of tag schemes.  The fundamental tagging method on NSLinguisticTagger is a block iterator, that iterates over all tokens intersecting a given range, supplying tags and ranges.  There are several additional convenience methods, for obtaining a sentence range, information about a single token, or for obtaining information about all tokens intersecting a given range at once, in arrays.  In each case, the charIndex or range passed in must not extend beyond the end of the tagger's string, or the methods will raise an exception.  Note that a given instance of NSLinguisticTagger should not be used from more than one thread simultaneously.
 */
-- (void)enumerateTagsInRange:(NSRange)range scheme:(NSString *)tagScheme options:(NSLinguisticTaggerOptions)opts usingBlock:(void (^)(NSString *tag, NSRange tokenRange, NSRange sentenceRange, BOOL *stop))block NS_AVAILABLE(10_7, 5_0);
+- (void)enumerateTagsInRange:(NSRange)range scheme:(NSString *)tagScheme options:(NSLinguisticTaggerOptions)opts usingBlock:(void (NS_NOESCAPE ^)(NSString *tag, NSRange tokenRange, NSRange sentenceRange, BOOL *stop))block NS_AVAILABLE(10_7, 5_0);
 
 - (NSRange)sentenceRangeForRange:(NSRange)range NS_AVAILABLE(10_7, 5_0);
 - (nullable NSString *)tagAtIndex:(NSUInteger)charIndex scheme:(NSString *)tagScheme tokenRange:(nullable NSRangePointer)tokenRange sentenceRange:(nullable NSRangePointer)sentenceRange NS_AVAILABLE(10_7, 5_0);
-- (NSArray<NSString *> *)tagsInRange:(NSRange)range scheme:(NSString *)tagScheme options:(NSLinguisticTaggerOptions)opts tokenRanges:(NSArray<NSValue *> * __nullable * __nullable)tokenRanges NS_AVAILABLE(10_7, 5_0);
-- (nullable NSArray<NSString *> *)possibleTagsAtIndex:(NSUInteger)charIndex scheme:(NSString *)tagScheme tokenRange:(nullable NSRangePointer)tokenRange sentenceRange:(nullable NSRangePointer)sentenceRange scores:(NSArray<NSValue *> * __nullable * __nullable)scores NS_AVAILABLE(10_7, 5_0);
+- (NSArray<NSString *> *)tagsInRange:(NSRange)range scheme:(NSString *)tagScheme options:(NSLinguisticTaggerOptions)opts tokenRanges:(NSArray<NSValue *> * _Nullable * _Nullable)tokenRanges NS_AVAILABLE(10_7, 5_0);
+- (nullable NSArray<NSString *> *)possibleTagsAtIndex:(NSUInteger)charIndex scheme:(NSString *)tagScheme tokenRange:(nullable NSRangePointer)tokenRange sentenceRange:(nullable NSRangePointer)sentenceRange scores:(NSArray<NSValue *> * _Nullable * _Nullable)scores NS_AVAILABLE(10_7, 5_0);
 
 @end
 
@@ -116,8 +116,8 @@
 
 /* Clients wishing to analyze a given string once may use these NSString APIs without having to create an instance of NSLinguisticTagger.  If more than one tagging operation is needed on a given string, it is more efficient to use an explicit NSLinguisticTagger instance.
 */
-- (NSArray<NSString *> *)linguisticTagsInRange:(NSRange)range scheme:(NSString *)tagScheme options:(NSLinguisticTaggerOptions)opts orthography:(nullable NSOrthography *)orthography tokenRanges:(NSArray<NSValue *> * __nullable * __nullable)tokenRanges NS_AVAILABLE(10_7, 5_0);
-- (void)enumerateLinguisticTagsInRange:(NSRange)range scheme:(NSString *)tagScheme options:(NSLinguisticTaggerOptions)opts orthography:(nullable NSOrthography *)orthography usingBlock:(void (^)(NSString *tag, NSRange tokenRange, NSRange sentenceRange, BOOL *stop))block NS_AVAILABLE(10_7, 5_0);
+- (NSArray<NSString *> *)linguisticTagsInRange:(NSRange)range scheme:(NSString *)tagScheme options:(NSLinguisticTaggerOptions)opts orthography:(nullable NSOrthography *)orthography tokenRanges:(NSArray<NSValue *> * _Nullable * _Nullable)tokenRanges NS_AVAILABLE(10_7, 5_0);
+- (void)enumerateLinguisticTagsInRange:(NSRange)range scheme:(NSString *)tagScheme options:(NSLinguisticTaggerOptions)opts orthography:(nullable NSOrthography *)orthography usingBlock:(void (NS_NOESCAPE ^)(NSString *tag, NSRange tokenRange, NSRange sentenceRange, BOOL *stop))block NS_AVAILABLE(10_7, 5_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLocale.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLocale.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLocale.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLocale.h	2016-05-20 07:35:40.000000000 +0200
@@ -4,6 +4,11 @@
 
 #import <Foundation/NSObject.h>
 #import <CoreFoundation/CFLocale.h>
+#import <Foundation/NSNotification.h>
+
+@class NSCalendar;
+
+typedef NSString * NSLocaleKey NS_STRING_ENUM;
 
 @class NSArray<ObjectType>, NSDictionary<KeyType, ObjectType>, NSString;
 
@@ -13,9 +18,9 @@
 
 @interface NSLocale : NSObject <NSCopying, NSSecureCoding>
 
-- (nullable id)objectForKey:(id)key;
+- (nullable id)objectForKey:(NSLocaleKey)key;
 
-- (nullable NSString *)displayNameForKey:(id)key value:(id)value;
+- (nullable NSString *)displayNameForKey:(NSLocaleKey)key value:(id)value;
 
 - (instancetype)initWithLocaleIdentifier:(NSString *)string NS_DESIGNATED_INITIALIZER;
 
@@ -26,6 +31,56 @@
 @interface NSLocale (NSExtendedLocale)
 
 @property (readonly, copy) NSString *localeIdentifier;  // same as NSLocaleIdentifier
+- (NSString *)localizedStringForLocaleIdentifier:(NSString *)localeIdentifier API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly, copy) NSString *languageCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (NSString *)localizedStringForLanguageCode:(NSString *)languageCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly, copy) NSString *countryCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (NSString *)localizedStringForCountryCode:(NSString *)countryCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly, copy) NSString *scriptCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (NSString *)localizedStringForScriptCode:(NSString *)scriptCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly, copy) NSString *variantCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (NSString *)localizedStringForVariantCode:(NSString *)variantCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly, copy) NSCharacterSet *exemplarCharacterSet API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly) NSCalendar *calendar API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (NSString *)localizedStringForCalendar:(NSCalendar *)calendar API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly, copy) NSString *collationIdentifier API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (NSString *)localizedStringForCollationIdentifier:(NSString *)collationIdentifier API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly) BOOL usesMetricSystem API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly, copy) NSString *decimalSeparator API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (NSString *)localizedStringForDecimalSeparator:(NSString *)decimalSeparator API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly, copy) NSString *groupingSeparator API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (NSString *)localizedStringForGroupingSeparator:(NSString *)groupingSeparator API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly, copy) NSString *currencySymbol API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (NSString *)localizedStringForCurrencySymbol:(NSString *)currencySymbol API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly, copy) NSString *currencyCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (NSString *)localizedStringForCurrencyCode:(NSString *)currencyCode API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly, copy) NSString *collatorIdentifier API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (NSString *)localizedStringForCollatorIdentifier:(NSString *)collatorIdentifier API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly, copy) NSString *quotationBeginDelimiter API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (NSString *)localizedStringForQuotationBeginDelimiter:(NSString *)quotationBeginDelimiter API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly, copy) NSString *quotationEndDelimiter API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (NSString *)localizedStringForQuotationEndDelimiter:(NSString *)quotationEndDelimiter API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly, copy) NSString *alternateQuotationBeginDelimiter API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (NSString *)localizedStringForAlternateQuotationBeginDelimiter:(NSString *)alternateQuotationBeginDelimiter API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+@property (readonly, copy) NSString *alternateQuotationEndDelimiter API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+- (NSString *)localizedStringForAlternateQuotationEndDelimiter:(NSString *)alternateQuotationEndDelimiter API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
 
 @end
 
@@ -75,28 +130,28 @@
 @end
 
 
-FOUNDATION_EXPORT NSString * const NSCurrentLocaleDidChangeNotification NS_AVAILABLE(10_5, 2_0);
+FOUNDATION_EXPORT NSNotificationName const NSCurrentLocaleDidChangeNotification NS_AVAILABLE(10_5, 2_0);
 
 
-FOUNDATION_EXPORT NSString * const NSLocaleIdentifier;		// NSString
-FOUNDATION_EXPORT NSString * const NSLocaleLanguageCode;	// NSString
-FOUNDATION_EXPORT NSString * const NSLocaleCountryCode;		// NSString
-FOUNDATION_EXPORT NSString * const NSLocaleScriptCode;		// NSString
-FOUNDATION_EXPORT NSString * const NSLocaleVariantCode;		// NSString
-FOUNDATION_EXPORT NSString * const NSLocaleExemplarCharacterSet;// NSCharacterSet
-FOUNDATION_EXPORT NSString * const NSLocaleCalendar;		// NSCalendar
-FOUNDATION_EXPORT NSString * const NSLocaleCollationIdentifier; // NSString
-FOUNDATION_EXPORT NSString * const NSLocaleUsesMetricSystem;	// NSNumber boolean
-FOUNDATION_EXPORT NSString * const NSLocaleMeasurementSystem;	// NSString
-FOUNDATION_EXPORT NSString * const NSLocaleDecimalSeparator;	// NSString
-FOUNDATION_EXPORT NSString * const NSLocaleGroupingSeparator;	// NSString
-FOUNDATION_EXPORT NSString * const NSLocaleCurrencySymbol;      // NSString
-FOUNDATION_EXPORT NSString * const NSLocaleCurrencyCode;	// NSString
-FOUNDATION_EXPORT NSString * const NSLocaleCollatorIdentifier NS_AVAILABLE(10_6, 4_0);  // NSString
-FOUNDATION_EXPORT NSString * const NSLocaleQuotationBeginDelimiterKey NS_AVAILABLE(10_6, 4_0);	// NSString
-FOUNDATION_EXPORT NSString * const NSLocaleQuotationEndDelimiterKey NS_AVAILABLE(10_6, 4_0);	// NSString
-FOUNDATION_EXPORT NSString * const NSLocaleAlternateQuotationBeginDelimiterKey NS_AVAILABLE(10_6, 4_0);	// NSString
-FOUNDATION_EXPORT NSString * const NSLocaleAlternateQuotationEndDelimiterKey NS_AVAILABLE(10_6, 4_0);	// NSString
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleIdentifier;		// NSString
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleLanguageCode;	// NSString
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleCountryCode;		// NSString
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleScriptCode;		// NSString
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleVariantCode;		// NSString
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleExemplarCharacterSet;// NSCharacterSet
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleCalendar;		// NSCalendar
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleCollationIdentifier; // NSString
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleUsesMetricSystem;	// NSNumber boolean
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleMeasurementSystem;	// NSString
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleDecimalSeparator;	// NSString
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleGroupingSeparator;	// NSString
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleCurrencySymbol;      // NSString
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleCurrencyCode;	// NSString
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleCollatorIdentifier NS_AVAILABLE(10_6, 4_0);  // NSString
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleQuotationBeginDelimiterKey NS_AVAILABLE(10_6, 4_0);	// NSString
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleQuotationEndDelimiterKey NS_AVAILABLE(10_6, 4_0);	// NSString
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleAlternateQuotationBeginDelimiterKey NS_AVAILABLE(10_6, 4_0);	// NSString
+FOUNDATION_EXPORT NSLocaleKey const NSLocaleAlternateQuotationEndDelimiterKey NS_AVAILABLE(10_6, 4_0);	// NSString
 
 
 #if !defined(NS_CALENDAR_ENUM_DEPRECATED)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMapTable.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMapTable.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMapTable.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMapTable.h	2016-05-20 07:35:40.000000000 +0200
@@ -77,22 +77,22 @@
 
 /****************	void * Map table operations	****************/
 
-typedef struct {NSUInteger _pi; NSUInteger _si; void * __nullable _bs;} NSMapEnumerator;
+typedef struct {NSUInteger _pi; NSUInteger _si; void * _Nullable _bs;} NSMapEnumerator;
 
 
 
 FOUNDATION_EXPORT void NSFreeMapTable(NSMapTable *table);
 FOUNDATION_EXPORT void NSResetMapTable(NSMapTable *table);
 FOUNDATION_EXPORT BOOL NSCompareMapTables(NSMapTable *table1, NSMapTable *table2);
-FOUNDATION_EXPORT NSMapTable *NSCopyMapTableWithZone(NSMapTable *table, NSZone * __nullable zone);
-FOUNDATION_EXPORT BOOL NSMapMember(NSMapTable *table, const void *key, void * __nullable * __nullable originalKey, void * __nullable * __nullable value);
-FOUNDATION_EXPORT void * __nullable NSMapGet(NSMapTable *table, const void * __nullable key);
-FOUNDATION_EXPORT void NSMapInsert(NSMapTable *table, const void * __nullable key, const void * __nullable value);
-FOUNDATION_EXPORT void NSMapInsertKnownAbsent(NSMapTable *table, const void * __nullable key, const void * __nullable value);
-FOUNDATION_EXPORT void * __nullable NSMapInsertIfAbsent(NSMapTable *table, const void * __nullable key, const void * __nullable value);
-FOUNDATION_EXPORT void NSMapRemove(NSMapTable *table, const void * __nullable key);
+FOUNDATION_EXPORT NSMapTable *NSCopyMapTableWithZone(NSMapTable *table, NSZone * _Nullable zone);
+FOUNDATION_EXPORT BOOL NSMapMember(NSMapTable *table, const void *key, void * _Nullable * _Nullable originalKey, void * _Nullable * _Nullable value);
+FOUNDATION_EXPORT void * _Nullable NSMapGet(NSMapTable *table, const void * _Nullable key);
+FOUNDATION_EXPORT void NSMapInsert(NSMapTable *table, const void * _Nullable key, const void * _Nullable value);
+FOUNDATION_EXPORT void NSMapInsertKnownAbsent(NSMapTable *table, const void * _Nullable key, const void * _Nullable value);
+FOUNDATION_EXPORT void * _Nullable NSMapInsertIfAbsent(NSMapTable *table, const void * _Nullable key, const void * _Nullable value);
+FOUNDATION_EXPORT void NSMapRemove(NSMapTable *table, const void * _Nullable key);
 FOUNDATION_EXPORT NSMapEnumerator NSEnumerateMapTable(NSMapTable *table);
-FOUNDATION_EXPORT BOOL NSNextMapEnumeratorPair(NSMapEnumerator *enumerator, void * __nullable * __nullable key, void * __nullable * __nullable value);
+FOUNDATION_EXPORT BOOL NSNextMapEnumeratorPair(NSMapEnumerator *enumerator, void * _Nullable * _Nullable key, void * _Nullable * _Nullable value);
 FOUNDATION_EXPORT void NSEndMapTableEnumeration(NSMapEnumerator *enumerator);
 FOUNDATION_EXPORT NSUInteger NSCountMapTable(NSMapTable *table);
 FOUNDATION_EXPORT NSString *NSStringFromMapTable(NSMapTable *table);
@@ -103,12 +103,12 @@
 /****************     Legacy     ***************************************/
 
 typedef struct {
-    NSUInteger	(* __nullable hash)(NSMapTable *table, const void *);
-    BOOL	(* __nullable isEqual)(NSMapTable *table, const void *, const void *);
-    void	(* __nullable retain)(NSMapTable *table, const void *);
-    void	(* __nullable release)(NSMapTable *table, void *);
-    NSString 	* __nullable (* __nullable describe)(NSMapTable *table, const void *);
-    const void	* __nullable notAKeyMarker;
+    NSUInteger	(* _Nullable hash)(NSMapTable *table, const void *);
+    BOOL	(* _Nullable isEqual)(NSMapTable *table, const void *, const void *);
+    void	(* _Nullable retain)(NSMapTable *table, const void *);
+    void	(* _Nullable release)(NSMapTable *table, void *);
+    NSString 	* _Nullable (* _Nullable describe)(NSMapTable *table, const void *);
+    const void	* _Nullable notAKeyMarker;
 } NSMapTableKeyCallBacks;
     
 #define NSNotAnIntMapKey	((const void *)NSIntegerMin)
@@ -116,12 +116,12 @@
 #define NSNotAPointerMapKey	((const void *)UINTPTR_MAX)
 
 typedef struct {
-    void	(* __nullable retain)(NSMapTable *table, const void *);
-    void	(* __nullable release)(NSMapTable *table, void *);
-    NSString 	* __nullable(* __nullable describe)(NSMapTable *table, const void *);
+    void	(* _Nullable retain)(NSMapTable *table, const void *);
+    void	(* _Nullable release)(NSMapTable *table, void *);
+    NSString 	* _Nullable(* _Nullable describe)(NSMapTable *table, const void *);
 } NSMapTableValueCallBacks;
 
-FOUNDATION_EXPORT NSMapTable *NSCreateMapTableWithZone(NSMapTableKeyCallBacks keyCallBacks, NSMapTableValueCallBacks valueCallBacks, NSUInteger capacity, NSZone * __nullable zone);
+FOUNDATION_EXPORT NSMapTable *NSCreateMapTableWithZone(NSMapTableKeyCallBacks keyCallBacks, NSMapTableValueCallBacks valueCallBacks, NSUInteger capacity, NSZone * _Nullable zone);
 FOUNDATION_EXPORT NSMapTable *NSCreateMapTable(NSMapTableKeyCallBacks keyCallBacks, NSMapTableValueCallBacks valueCallBacks, NSUInteger capacity);
 
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMassFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMassFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMassFormatter.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMassFormatter.h	2016-05-20 06:24:14.000000000 +0200
@@ -41,7 +41,7 @@
 - (NSString *)unitStringFromKilograms:(double)numberInKilograms usedUnit:(nullable NSMassFormatterUnit *)unitp;
 
 // No parsing is supported. This method will return NO.
-- (BOOL)getObjectValue:(out id __nullable * __nullable)obj forString:(NSString *)string errorDescription:(out NSString * __nullable * __nullable)error;
+- (BOOL)getObjectValue:(out id _Nullable * _Nullable)obj forString:(NSString *)string errorDescription:(out NSString * _Nullable * _Nullable)error;
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMeasurement.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMeasurement.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMeasurement.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMeasurement.h	2016-05-20 06:24:14.000000000 +0200
@@ -0,0 +1,48 @@
+/*
+    NSMeasurement.h
+    Copyright © 2015, Apple Inc.
+    All rights reserved.
+ */
+
+#import <Foundation/NSObject.h>
+#import <Foundation/NSUnit.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface NSMeasurement<UnitType: NSUnit *> : NSObject<NSCopying, NSSecureCoding> {
+@private
+    UnitType _unit;
+    double _doubleValue;
+}
+
+@property (readonly, copy) UnitType unit;
+@property (readonly) double doubleValue;
+
+- (instancetype)init NS_UNAVAILABLE;
+- (instancetype)initWithDoubleValue:(double)doubleValue unit:(UnitType)unit NS_DESIGNATED_INITIALIZER;
+
+/*
+ Given an NSUnit object, canBeConvertedToUnit: will check for dimensionality i.e. check the unit type (NSUnitAngle, NSUnitLength, NSUnitCustom, etc.) of the NSUnit object.  It will return YES if the unit type of the given unit is the same as the unit type of the unit within the NSMeasurement object and NO if not.
+ Note: This method will return NO if given or called on a dimensionless unit.
+ */
+- (BOOL)canBeConvertedToUnit:(NSUnit *)unit;
+
+/*
+ Given an NSUnit object, measurementByConvertingUnit: will first check for dimensionality i.e. check the unit type (NSUnitAngle, NSUnitLength, NSUnitCustom, etc.) of the NSUnit object.  If the unit type of the given unit is not the same as the unit type of the unit within the NSMeasurement object (i.e. the units are of differing dimensionalities), measurementByConvertingToUnit: will throw an InvalidArgumentException.
+
+ @return A new NSMeasurement object with the given unit and converted value.
+ */
+- (NSMeasurement *)measurementByConvertingToUnit:(NSUnit *)unit;
+
+/*
+ Given an NSMeasurement object, these methods will first check for dimensionality i.e. check the unit type (NSUnitAngle, NSUnitLength, NSUnitCustom, etc.) of the unit contained in that object.  If the unit type of the unit in the given NSMeasurement object is not the same as the unit type of the unit within the current NSMeasurement instance (i.e. the units are of differing dimensionalities), these methods will throw an InvalidArgumentException.
+ 
+ @return A new NSMeasurement object with the adjusted value and a unit that is the same type as the current NSMeasurement instance.
+ */
+- (NSMeasurement<UnitType> *)measurementByAddingMeasurement:(NSMeasurement<UnitType> *)measurement;
+- (NSMeasurement<UnitType> *)measurementBySubtractingMeasurement:(NSMeasurement<UnitType> *)measurement;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMeasurementFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMeasurementFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMeasurementFormatter.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMeasurementFormatter.h	2016-05-20 06:24:14.000000000 +0200
@@ -0,0 +1,75 @@
+/*
+ NSMeasurementFormatter.h
+ Copyright © 2015, Apple Inc.
+ All rights reserved.
+ */
+
+#import <Foundation/NSObject.h>
+#import <Foundation/NSFormatter.h>
+#import <Foundation/NSNumberFormatter.h>
+#import <Foundation/NSMeasurement.h>
+#import <Foundation/NSLocale.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+typedef NS_OPTIONS(NSUInteger, NSMeasurementFormatterUnitOptions) {
+    NSMeasurementFormatterUnitOptionsPreferredUnitOfLocale API_DEPRECATED("No longer necessary - this is now the default behavior of the formatter.", macosx(10.12, 10.12), ios(10.0, 10.0), watchos(3.0, 3.0), tvos(10.0, 10.0)) = 0,
+    NSMeasurementFormatterUnitOptionsProvidedUnit = (1UL << 0),              // e.g  This ensures the formatter uses this unit even if it is not the preferred unit of the set locale.
+    NSMeasurementFormatterUnitOptionsNaturalScale = (1UL << 1),              // e.g. This would make the formatter show "12 kilometers" instead of "12000 meters"
+    NSMeasurementFormatterUnitOptionsTemperatureWithoutUnit = (1UL << 2),    // e.g. This would display "90°" rather than "90°F" or "90°C"
+} API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSMeasurementFormatter : NSFormatter <NSSecureCoding> {
+@private
+    void *_formatter;
+    NSMeasurementFormatterUnitOptions _unitOptions;
+    NSFormattingUnitStyle _unitStyle;
+    NSLocale *_locale;
+    NSNumberFormatter *_numberFormatter;
+}
+
+/*
+ This property can be set to ensure that the formatter behaves in a way the developer expects, even if it is not standard according to the preferences of the user's locale. If not specified, unitOptions defaults to localizing according to the preferences of the locale.
+ 
+ Ex:
+ 
+ By default, if unitOptions is set to the empty set, the formatter will do the following:
+    - kilocalories may be formatted as "C" instead of "kcal" depending on the locale.
+    - kilometersPerHour may be formatted as "miles per hour" for US and UK locales but "kilometers per hour" for other locales.
+ 
+ However, if NSMeasurementFormatterUnitOptionsProvidedUnit is set, the formatter will do the following:
+    - kilocalories would be formatted as "kcal" in the language of the locale, even if the locale prefers "C".
+    - kilometersPerHour would be formatted as "kilometers per hour" for US and UK locales even though the preference is for "miles per hour."
+
+ Note that NSMeasurementFormatter will handle converting measurement objects to the preferred units in a particular locale.  For instance, if provided a measurement object in kilometers and the set locale is en_US, the formatter will implicitly convert the measurement object to miles and return the formatted string as the equivalent measurement in miles.
+
+ */
+@property NSMeasurementFormatterUnitOptions unitOptions;
+
+/*
+ If not specified, unitStyle is set to NSFormattingUnitStyleMedium.
+ */
+@property NSFormattingUnitStyle unitStyle;
+
+/*
+ If not specified, locale is set to the user's current locale.
+ */
+@property (null_resettable, copy) NSLocale *locale;
+
+/*
+ If not specified, the number formatter is set up with NSNumberFormatterDecimalStyle.
+ */
+@property (null_resettable, copy) NSNumberFormatter *numberFormatter;
+
+- (NSString *)stringFromMeasurement:(NSMeasurement *)measurement;
+
+/*
+ @param An NSUnit
+ @return A formatted string representing the localized form of the unit without a value attached to it.  This method will return [unit symbol] if the provided unit cannot be localized.
+ */
+- (NSString *)stringFromUnit:(NSUnit *)unit;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMetadata.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMetadata.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMetadata.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSMetadata.h	2016-05-20 07:39:55.000000000 +0200
@@ -6,6 +6,7 @@
 
 #import <Foundation/NSObject.h>
 #import <Foundation/NSDate.h>
+#import <Foundation/NSNotification.h>
 
 @class NSString, NSURL, NSArray<ObjectType>, NSDictionary<KeyType, ObjectType>, NSPredicate, NSOperationQueue, NSSortDescriptor;
 @class NSMetadataItem, NSMetadataQueryAttributeValueTuple, NSMetadataQueryResultGroup;
@@ -19,7 +20,7 @@
     NSUInteger _flags;
     NSTimeInterval _interval;
     id _private[11];
-    __strong void *_reserved;
+    void *_reserved;
 }
 
 @property (nullable, assign) id<NSMetadataQueryDelegate> delegate;
@@ -57,8 +58,8 @@
 @property (readonly) NSUInteger resultCount;
 - (id)resultAtIndex:(NSUInteger)idx;
 
-- (void)enumerateResultsUsingBlock:(void (^)(id result, NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_9, 7_0);
-- (void)enumerateResultsWithOptions:(NSEnumerationOptions)opts usingBlock:(void (^)(id result, NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_9, 7_0);
+- (void)enumerateResultsUsingBlock:(void (NS_NOESCAPE ^)(id result, NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_9, 7_0);
+- (void)enumerateResultsWithOptions:(NSEnumerationOptions)opts usingBlock:(void (NS_NOESCAPE ^)(id result, NSUInteger idx, BOOL *stop))block NS_AVAILABLE(10_9, 7_0);
 
 @property (readonly, copy) NSArray *results;   // this is for K-V Bindings, and causes side-effects on the query
 
@@ -81,10 +82,10 @@
 @end
 
 // notifications
-FOUNDATION_EXPORT NSString * const NSMetadataQueryDidStartGatheringNotification NS_AVAILABLE(10_4, 5_0);
-FOUNDATION_EXPORT NSString * const NSMetadataQueryGatheringProgressNotification NS_AVAILABLE(10_4, 5_0);
-FOUNDATION_EXPORT NSString * const NSMetadataQueryDidFinishGatheringNotification NS_AVAILABLE(10_4, 5_0);
-FOUNDATION_EXPORT NSString * const NSMetadataQueryDidUpdateNotification NS_AVAILABLE(10_4, 5_0);
+FOUNDATION_EXPORT NSNotificationName const NSMetadataQueryDidStartGatheringNotification NS_AVAILABLE(10_4, 5_0);
+FOUNDATION_EXPORT NSNotificationName const NSMetadataQueryGatheringProgressNotification NS_AVAILABLE(10_4, 5_0);
+FOUNDATION_EXPORT NSNotificationName const NSMetadataQueryDidFinishGatheringNotification NS_AVAILABLE(10_4, 5_0);
+FOUNDATION_EXPORT NSNotificationName const NSMetadataQueryDidUpdateNotification NS_AVAILABLE(10_4, 5_0);
 
 // keys for use with notification info dictionary
 FOUNDATION_EXPORT NSString * const NSMetadataQueryUpdateAddedItemsKey NS_AVAILABLE(10_9, 8_0);
@@ -111,7 +112,7 @@
 @interface NSMetadataItem : NSObject {
 @private
     id _item;
-    __strong void *_reserved;
+    void *_reserved;
 }
 
 - (nullable instancetype)initWithURL:(NSURL *)url NS_DESIGNATED_INITIALIZER NS_AVAILABLE_MAC(10_9);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNetServices.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNetServices.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNetServices.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNetServices.h	2016-05-20 07:35:40.000000000 +0200
@@ -4,6 +4,8 @@
 
 #import <Foundation/NSObject.h>
 #import <Foundation/NSDate.h>
+#import <Foundation/NSError.h>
+#import <Foundation/NSRunLoop.h>
 
 @class NSArray<ObjectType>, NSData, NSDictionary<KeyType, ObjectType>, NSInputStream, NSNumber, NSOutputStream, NSRunLoop, NSString;
 @protocol NSNetServiceDelegate, NSNetServiceBrowserDelegate;
@@ -13,7 +15,7 @@
 #pragma mark Error constants
 
 FOUNDATION_EXPORT NSString * const NSNetServicesErrorCode;
-FOUNDATION_EXPORT NSString * const NSNetServicesErrorDomain;
+FOUNDATION_EXPORT NSErrorDomain const NSNetServicesErrorDomain;
 
 typedef NS_ENUM(NSInteger, NSNetServicesError) {
     
@@ -97,8 +99,8 @@
 
 /* NSNetService instances may be scheduled on NSRunLoops to operate in different modes, or in other threads. It is generally not necessary to schedule NSNetServices in other threads. NSNetServices are scheduled in the current thread's NSRunLoop in the NSDefaultRunLoopMode when they are created.
 */
-- (void)scheduleInRunLoop:(NSRunLoop *)aRunLoop forMode:(NSString *)mode;
-- (void)removeFromRunLoop:(NSRunLoop *)aRunLoop forMode:(NSString *)mode;
+- (void)scheduleInRunLoop:(NSRunLoop *)aRunLoop forMode:(NSRunLoopMode)mode;
+- (void)removeFromRunLoop:(NSRunLoop *)aRunLoop forMode:(NSRunLoopMode)mode;
 
 /* Set a delegate to receive publish, resolve, or monitor events.
  */
@@ -167,7 +169,7 @@
 
 /* Retrieves streams from the NSNetService instance. The instance's delegate methods are not called. Returns YES if the streams requested are created successfully. Returns NO if or any reason the stream could not be created. If only one stream is desired, pass NULL for the address of the other stream. The streams that are created are not open, and are not scheduled in any run loop for any mode.
 */
-- (BOOL)getInputStream:(out __strong NSInputStream * __nullable * __nullable)inputStream outputStream:(out __strong NSOutputStream * __nullable * __nullable)outputStream;
+- (BOOL)getInputStream:(out __strong NSInputStream * _Nullable * _Nullable)inputStream outputStream:(out __strong NSOutputStream * _Nullable * _Nullable)outputStream;
 
 /* Sets the TXT record of the NSNetService instance that has been or will be published. Pass nil to remove the TXT record from the instance.
 */
@@ -210,8 +212,8 @@
 
 /* NSNetServiceBrowser instances may be scheduled on NSRunLoops to operate in different modes, or in other threads. It is generally not necessary to schedule NSNetServiceBrowsers in other threads. NSNetServiceBrowsers are scheduled in the current thread's NSRunLoop in the NSDefaultRunLoopMode when they are created.
 */
-- (void)scheduleInRunLoop:(NSRunLoop *)aRunLoop forMode:(NSString *)mode;
-- (void)removeFromRunLoop:(NSRunLoop *)aRunLoop forMode:(NSString *)mode;
+- (void)scheduleInRunLoop:(NSRunLoop *)aRunLoop forMode:(NSRunLoopMode)mode;
+- (void)removeFromRunLoop:(NSRunLoop *)aRunLoop forMode:(NSRunLoopMode)mode;
 
 /* Starts a search for domains that are browsable via Bonjour and the computer's network configuration. Discovered domains are reported to the delegate's -netServiceBrowser:didFindDomain:moreComing: method. There may be more than one browsable domain.
 */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotification.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotification.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotification.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotification.h	2016-05-20 06:24:14.000000000 +0200
@@ -4,6 +4,8 @@
 
 #import <Foundation/NSObject.h>
 
+typedef NSString *NSNotificationName NS_EXTENSIBLE_STRING_ENUM;
+
 @class NSString, NSDictionary, NSOperationQueue;
 
 NS_ASSUME_NONNULL_BEGIN
@@ -12,19 +14,19 @@
 
 @interface NSNotification : NSObject <NSCopying, NSCoding>
 
-@property (readonly, copy) NSString *name;
+@property (readonly, copy) NSNotificationName name;
 @property (nullable, readonly, retain) id object;
 @property (nullable, readonly, copy) NSDictionary *userInfo;
 
-- (instancetype)initWithName:(NSString *)name object:(nullable id)object userInfo:(nullable NSDictionary *)userInfo NS_AVAILABLE(10_6, 4_0) NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithName:(NSNotificationName)name object:(nullable id)object userInfo:(nullable NSDictionary *)userInfo NS_AVAILABLE(10_6, 4_0) NS_DESIGNATED_INITIALIZER;
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
 
 @end
 
 @interface NSNotification (NSNotificationCreation)
 
-+ (instancetype)notificationWithName:(NSString *)aName object:(nullable id)anObject;
-+ (instancetype)notificationWithName:(NSString *)aName object:(nullable id)anObject userInfo:(nullable NSDictionary *)aUserInfo;
++ (instancetype)notificationWithName:(NSNotificationName)aName object:(nullable id)anObject;
++ (instancetype)notificationWithName:(NSNotificationName)aName object:(nullable id)anObject userInfo:(nullable NSDictionary *)aUserInfo;
 
 - (instancetype)init /*NS_UNAVAILABLE*/;	/* do not invoke; not a valid initializer for this class */
 
@@ -34,8 +36,8 @@
 
 @interface NSNotificationCenter : NSObject {
     @package
-    void * __strong _impl;
-    void * __strong _callback;
+    void *_impl;
+    void *_callback;
     void *_pad[11];
 }
 
@@ -44,13 +46,13 @@
 - (void)addObserver:(id)observer selector:(SEL)aSelector name:(nullable NSString *)aName object:(nullable id)anObject;
 
 - (void)postNotification:(NSNotification *)notification;
-- (void)postNotificationName:(NSString *)aName object:(nullable id)anObject;
-- (void)postNotificationName:(NSString *)aName object:(nullable id)anObject userInfo:(nullable NSDictionary *)aUserInfo;
+- (void)postNotificationName:(NSNotificationName)aName object:(nullable id)anObject;
+- (void)postNotificationName:(NSNotificationName)aName object:(nullable id)anObject userInfo:(nullable NSDictionary *)aUserInfo;
 
 - (void)removeObserver:(id)observer;
-- (void)removeObserver:(id)observer name:(nullable NSString *)aName object:(nullable id)anObject;
+- (void)removeObserver:(id)observer name:(nullable NSNotificationName)aName object:(nullable id)anObject;
 
-- (id <NSObject>)addObserverForName:(nullable NSString *)name object:(nullable id)obj queue:(nullable NSOperationQueue *)queue usingBlock:(void (^)(NSNotification *note))block NS_AVAILABLE(10_6, 4_0);
+- (id <NSObject>)addObserverForName:(nullable NSNotificationName)name object:(nullable id)obj queue:(nullable NSOperationQueue *)queue usingBlock:(void (^)(NSNotification *note))block NS_AVAILABLE(10_6, 4_0);
     // The return value is retained by the system, and should be held onto by the caller in
     // order to remove the observer with removeObserver: later, to stop observation.
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotificationQueue.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotificationQueue.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotificationQueue.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNotificationQueue.h	2016-05-20 06:24:14.000000000 +0200
@@ -3,6 +3,7 @@
 */
 
 #import <Foundation/NSObject.h>
+#import <Foundation/NSRunLoop.h>
 
 @class NSNotification, NSNotificationCenter, NSArray<ObjectType>, NSString;
 
@@ -34,7 +35,7 @@
 - (instancetype)initWithNotificationCenter:(NSNotificationCenter *)notificationCenter NS_DESIGNATED_INITIALIZER;
 
 - (void)enqueueNotification:(NSNotification *)notification postingStyle:(NSPostingStyle)postingStyle;
-- (void)enqueueNotification:(NSNotification *)notification postingStyle:(NSPostingStyle)postingStyle coalesceMask:(NSNotificationCoalescing)coalesceMask forModes:(nullable NSArray<NSString *> *)modes;
+- (void)enqueueNotification:(NSNotification *)notification postingStyle:(NSPostingStyle)postingStyle coalesceMask:(NSNotificationCoalescing)coalesceMask forModes:(nullable NSArray<NSRunLoopMode> *)modes;
 
 - (void)dequeueNotificationsMatching:(NSNotification *)notification coalesceMask:(NSUInteger)coalesceMask;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNumberFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNumberFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNumberFormatter.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSNumberFormatter.h	2016-05-20 06:12:55.000000000 +0200
@@ -20,7 +20,7 @@
 @interface NSNumberFormatter : NSFormatter {
 @private
     NSMutableDictionary	*_attributes;
-    __strong CFNumberFormatterRef _formatter;
+    CFNumberFormatterRef _formatter;
     NSUInteger _counter;
     NSNumberFormatterBehavior _behavior;
     NSRecursiveLock *_lock;
@@ -35,7 +35,7 @@
 
 // Report the used range of the string and an NSError, in addition to the usual stuff from NSFormatter
 
-- (BOOL)getObjectValue:(out id __nullable * __nullable)obj forString:(NSString *)string range:(inout nullable NSRange *)rangep error:(out NSError **)error;
+- (BOOL)getObjectValue:(out id _Nullable * _Nullable)obj forString:(NSString *)string range:(inout nullable NSRange *)rangep error:(out NSError **)error;
 
 // Even though NSNumberFormatter responds to the usual NSFormatter methods,
 //   here are some convenience methods which are a little more obvious.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObjCRuntime.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObjCRuntime.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObjCRuntime.h	2016-02-24 22:14:05.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObjCRuntime.h	2016-05-20 06:24:14.000000000 +0200
@@ -224,6 +224,12 @@
 #endif
 #endif
 
+#if __has_attribute(not_tail_called)
+#define NS_NO_TAIL_CALL __attribute__((not_tail_called))
+#else
+#define NS_NO_TAIL_CALL
+#endif
+
 #if !__has_feature(objc_instancetype)
 #undef instancetype
 #define instancetype id
@@ -280,6 +286,35 @@
 #define NS_ENUM(...) CF_ENUM(__VA_ARGS__)
 #define NS_OPTIONS(_type, _name) CF_OPTIONS(_type, _name)
 
+
+/* <rdar://problem/24976885> Remove Foundation redeclarations of CF_STRING_ENUM macros once FCF builds are in sync */
+#ifndef CF_STRING_ENUM
+#if __has_attribute(swift_wrapper)
+#define _CF_TYPED_ENUM __attribute__((swift_wrapper(enum)))
+#else
+#define _CF_TYPED_ENUM
+#endif
+
+#define CF_STRING_ENUM _CF_TYPED_ENUM
+#endif
+
+#ifndef CF_EXTENSIBLE_STRING_ENUM
+#if __has_attribute(swift_wrapper)
+#define _CF_TYPED_EXTENSIBLE_ENUM __attribute__((swift_wrapper(struct)))
+#else
+#define _CF_TYPED_EXTENSIBLE_ENUM
+#endif
+
+#define CF_EXTENSIBLE_STRING_ENUM _CF_TYPED_EXTENSIBLE_ENUM
+#endif
+/* */
+
+#define _NS_TYPED_ENUM _CF_TYPED_ENUM
+#define _NS_TYPED_EXTENSIBLE_ENUM _CF_TYPED_EXTENSIBLE_ENUM
+
+#define NS_STRING_ENUM _NS_TYPED_ENUM
+#define NS_EXTENSIBLE_STRING_ENUM _NS_TYPED_EXTENSIBLE_ENUM
+
 // This macro is to be used by system frameworks to support the weak linking of classes. Weak linking is supported on iOS 3.1 and Mac OS X 10.6.8 or later.
 #if (__MAC_OS_X_VERSION_MIN_REQUIRED >= __MAC_10_6 || __IPHONE_OS_VERSION_MIN_REQUIRED >= __IPHONE_3_1) && \
     ((__has_feature(objc_weak_class) || \
@@ -311,6 +346,8 @@
 
 #define NS_SWIFT_NAME(_name) CF_SWIFT_NAME(_name)
 
+#define NS_NOESCAPE CF_NOESCAPE
+
 #if __has_attribute(swift_error)
 #define NS_SWIFT_NOTHROW __attribute__((swift_error(none)))
 #else
@@ -396,6 +433,15 @@
 #define NSFoundationVersionNumber10_10_1 1151.16
 #define NSFoundationVersionNumber10_10_2 1152.14
 #define NSFoundationVersionNumber10_10_3 1153.20
+#define NSFoundationVersionNumber10_10_4 1153.20
+#define NSFoundationVersionNumber10_10_5 1154
+#define NSFoundationVersionNumber10_10_Max 1199
+#define NSFoundationVersionNumber10_11   1252
+#define NSFoundationVersionNumber10_11_1 1255.1
+#define NSFoundationVersionNumber10_11_2 1256.1
+#define NSFoundationVersionNumber10_11_3 1256.1
+#define NSFoundationVersionNumber10_11_4 1258
+#define NSFoundationVersionNumber10_11_Max 1299
 #endif
 
 #if TARGET_OS_IPHONE
@@ -420,6 +466,13 @@
 #define NSFoundationVersionNumber_iOS_8_2 1142.14
 #define NSFoundationVersionNumber_iOS_8_3 1144.17
 #define NSFoundationVersionNumber_iOS_8_4 1144.17
+#define NSFoundationVersionNumber_iOS_8_x_Max 1199
+#define NSFoundationVersionNumber_iOS_9_0 1240.1
+#define NSFoundationVersionNumber_iOS_9_1 1241.14
+#define NSFoundationVersionNumber_iOS_9_2 1242.12
+#define NSFoundationVersionNumber_iOS_9_3 1242.12
+#define NSFoundationVersionNumber_iOS_9_4 1280.25
+#define NSFoundationVersionNumber_iOS_9_x_Max 1299
 #endif
 
 #if TARGET_OS_WIN32
@@ -435,19 +488,22 @@
 
 @class NSString, Protocol;
 
+typedef NSString * NSExceptionName NS_EXTENSIBLE_STRING_ENUM;
+typedef NSString * NSRunLoopMode NS_EXTENSIBLE_STRING_ENUM;
+
 FOUNDATION_EXPORT NSString *NSStringFromSelector(SEL aSelector);
 FOUNDATION_EXPORT SEL NSSelectorFromString(NSString *aSelectorName);
 
 FOUNDATION_EXPORT NSString *NSStringFromClass(Class aClass);
-FOUNDATION_EXPORT Class __nullable NSClassFromString(NSString *aClassName);
+FOUNDATION_EXPORT Class _Nullable NSClassFromString(NSString *aClassName);
 
 FOUNDATION_EXPORT NSString *NSStringFromProtocol(Protocol *proto) NS_AVAILABLE(10_5, 2_0);
-FOUNDATION_EXPORT Protocol * __nullable NSProtocolFromString(NSString *namestr) NS_AVAILABLE(10_5, 2_0);
+FOUNDATION_EXPORT Protocol * _Nullable NSProtocolFromString(NSString *namestr) NS_AVAILABLE(10_5, 2_0);
 
-FOUNDATION_EXPORT const char *NSGetSizeAndAlignment(const char *typePtr, NSUInteger * __nullable sizep, NSUInteger * __nullable alignp);
+FOUNDATION_EXPORT const char *NSGetSizeAndAlignment(const char *typePtr, NSUInteger * _Nullable sizep, NSUInteger * _Nullable alignp);
 
-FOUNDATION_EXPORT void NSLog(NSString *format, ...) NS_FORMAT_FUNCTION(1,2);
-FOUNDATION_EXPORT void NSLogv(NSString *format, va_list args) NS_FORMAT_FUNCTION(1,0);
+FOUNDATION_EXPORT void NSLog(NSString *format, ...) NS_FORMAT_FUNCTION(1,2) NS_NO_TAIL_CALL;
+FOUNDATION_EXPORT void NSLogv(NSString *format, va_list args) NS_FORMAT_FUNCTION(1,0) NS_NO_TAIL_CALL;
 
 typedef NS_ENUM(NSInteger, NSComparisonResult) {NSOrderedAscending = -1L, NSOrderedSame, NSOrderedDescending};
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObject.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObject.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObject.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSObject.h	2016-05-20 06:25:32.000000000 +0200
@@ -84,13 +84,13 @@
 
 /***********	Object Allocation / Deallocation		*******/
     
-FOUNDATION_EXPORT id NSAllocateObject(Class aClass, NSUInteger extraBytes, NSZone * __nullable zone) NS_AUTOMATED_REFCOUNT_UNAVAILABLE;
+FOUNDATION_EXPORT id NSAllocateObject(Class aClass, NSUInteger extraBytes, NSZone * _Nullable zone) NS_AUTOMATED_REFCOUNT_UNAVAILABLE;
 
 FOUNDATION_EXPORT void NSDeallocateObject(id object) NS_AUTOMATED_REFCOUNT_UNAVAILABLE;
 
-FOUNDATION_EXPORT id NSCopyObject(id object, NSUInteger extraBytes, NSZone * __nullable zone) NS_AUTOMATED_REFCOUNT_UNAVAILABLE NS_DEPRECATED(10_0, 10_8, 2_0, 6_0);
+FOUNDATION_EXPORT id NSCopyObject(id object, NSUInteger extraBytes, NSZone * _Nullable zone) NS_AUTOMATED_REFCOUNT_UNAVAILABLE NS_DEPRECATED(10_0, 10_8, 2_0, 6_0);
 
-FOUNDATION_EXPORT BOOL NSShouldRetainWithZone(id anObject, NSZone * __nullable requestedZone) NS_AUTOMATED_REFCOUNT_UNAVAILABLE;
+FOUNDATION_EXPORT BOOL NSShouldRetainWithZone(id anObject, NSZone * _Nullable requestedZone) NS_AUTOMATED_REFCOUNT_UNAVAILABLE;
 
 FOUNDATION_EXPORT void NSIncrementExtraRefCount(id object) NS_AUTOMATED_REFCOUNT_UNAVAILABLE;
 
@@ -101,23 +101,23 @@
 #if __has_feature(objc_arc)
 
 // After using a CFBridgingRetain on an NSObject, the caller must take responsibility for calling CFRelease at an appropriate time.
-NS_INLINE CF_RETURNS_RETAINED CFTypeRef __nullable CFBridgingRetain(id __nullable X) {
+NS_INLINE CF_RETURNS_RETAINED CFTypeRef _Nullable CFBridgingRetain(id _Nullable X) {
     return (__bridge_retained CFTypeRef)X;
 }
 
-NS_INLINE id __nullable CFBridgingRelease(CFTypeRef CF_CONSUMED __nullable X) {
+NS_INLINE id _Nullable CFBridgingRelease(CFTypeRef CF_CONSUMED _Nullable X) {
     return (__bridge_transfer id)X;
 }
 
 #else
 
 // This function is intended for use while converting to ARC mode only.
-NS_INLINE CF_RETURNS_RETAINED CFTypeRef __nullable CFBridgingRetain(id __nullable X) {
+NS_INLINE CF_RETURNS_RETAINED CFTypeRef _Nullable CFBridgingRetain(id _Nullable X) {
     return X ? CFRetain((CFTypeRef)X) : NULL;
 }
 
 // This function is intended for use while converting to ARC mode only.
-NS_INLINE id __nullable CFBridgingRelease(CFTypeRef CF_CONSUMED __nullable X) {
+NS_INLINE id _Nullable CFBridgingRelease(CFTypeRef CF_CONSUMED _Nullable X) {
     return [(id)CFMakeCollectable(X) autorelease];
 }
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOperation.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOperation.h	2016-05-20 06:25:32.000000000 +0200
@@ -3,6 +3,7 @@
 */
 
 #import <Foundation/NSObject.h>
+#import <Foundation/NSException.h>
 #import <sys/qos.h>
 #import <dispatch/dispatch.h>
 
@@ -101,8 +102,8 @@
 
 @end
 
-FOUNDATION_EXPORT NSString * const NSInvocationOperationVoidResultException NS_AVAILABLE(10_5, 2_0);
-FOUNDATION_EXPORT NSString * const NSInvocationOperationCancelledException NS_AVAILABLE(10_5, 2_0);
+FOUNDATION_EXPORT NSExceptionName const NSInvocationOperationVoidResultException NS_AVAILABLE(10_5, 2_0);
+FOUNDATION_EXPORT NSExceptionName const NSInvocationOperationCancelledException NS_AVAILABLE(10_5, 2_0);
 
 static const NSInteger NSOperationQueueDefaultMaxConcurrentOperationCount = -1;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOrderedSet.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOrderedSet.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOrderedSet.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOrderedSet.h	2016-05-20 07:35:40.000000000 +0200
@@ -20,14 +20,14 @@
 - (ObjectType)objectAtIndex:(NSUInteger)idx;
 - (NSUInteger)indexOfObject:(ObjectType)object;
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
-- (instancetype)initWithObjects:(const ObjectType [])objects count:(NSUInteger)cnt NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithObjects:(const ObjectType _Nonnull [_Nullable])objects count:(NSUInteger)cnt NS_DESIGNATED_INITIALIZER;
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
 
 @end
 
 @interface NSOrderedSet<ObjectType> (NSExtendedOrderedSet)
 
-- (void)getObjects:(ObjectType __unsafe_unretained [])objects range:(NSRange)range;
+- (void)getObjects:(ObjectType __unsafe_unretained [])objects range:(NSRange)range NS_SWIFT_UNAVAILABLE("Use 'array' instead");
 - (NSArray<ObjectType> *)objectsAtIndexes:(NSIndexSet *)indexes;
 @property (nullable, nonatomic, readonly) ObjectType firstObject;
 @property (nullable, nonatomic, readonly) ObjectType lastObject;
@@ -57,22 +57,22 @@
 @property (readonly, strong) NSArray<ObjectType> *array;
 @property (readonly, strong) NSSet<ObjectType> *set;
 
-- (void)enumerateObjectsUsingBlock:(void (^)(ObjectType obj, NSUInteger idx, BOOL *stop))block;
-- (void)enumerateObjectsWithOptions:(NSEnumerationOptions)opts usingBlock:(void (^)(ObjectType obj, NSUInteger idx, BOOL *stop))block;
-- (void)enumerateObjectsAtIndexes:(NSIndexSet *)s options:(NSEnumerationOptions)opts usingBlock:(void (^)(ObjectType obj, NSUInteger idx, BOOL *stop))block;
-
-- (NSUInteger)indexOfObjectPassingTest:(BOOL (^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate;
-- (NSUInteger)indexOfObjectWithOptions:(NSEnumerationOptions)opts passingTest:(BOOL (^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate;
-- (NSUInteger)indexOfObjectAtIndexes:(NSIndexSet *)s options:(NSEnumerationOptions)opts passingTest:(BOOL (^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate;
-
-- (NSIndexSet *)indexesOfObjectsPassingTest:(BOOL (^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate;
-- (NSIndexSet *)indexesOfObjectsWithOptions:(NSEnumerationOptions)opts passingTest:(BOOL (^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate;
-- (NSIndexSet *)indexesOfObjectsAtIndexes:(NSIndexSet *)s options:(NSEnumerationOptions)opts passingTest:(BOOL (^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate;
+- (void)enumerateObjectsUsingBlock:(void (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))block;
+- (void)enumerateObjectsWithOptions:(NSEnumerationOptions)opts usingBlock:(void (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))block;
+- (void)enumerateObjectsAtIndexes:(NSIndexSet *)s options:(NSEnumerationOptions)opts usingBlock:(void (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))block;
+
+- (NSUInteger)indexOfObjectPassingTest:(BOOL (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate;
+- (NSUInteger)indexOfObjectWithOptions:(NSEnumerationOptions)opts passingTest:(BOOL (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate;
+- (NSUInteger)indexOfObjectAtIndexes:(NSIndexSet *)s options:(NSEnumerationOptions)opts passingTest:(BOOL (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate;
+
+- (NSIndexSet *)indexesOfObjectsPassingTest:(BOOL (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate;
+- (NSIndexSet *)indexesOfObjectsWithOptions:(NSEnumerationOptions)opts passingTest:(BOOL (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate;
+- (NSIndexSet *)indexesOfObjectsAtIndexes:(NSIndexSet *)s options:(NSEnumerationOptions)opts passingTest:(BOOL (NS_NOESCAPE ^)(ObjectType obj, NSUInteger idx, BOOL *stop))predicate;
 
-- (NSUInteger)indexOfObject:(ObjectType)object inSortedRange:(NSRange)range options:(NSBinarySearchingOptions)opts usingComparator:(NSComparator)cmp; // binary search
+- (NSUInteger)indexOfObject:(ObjectType)object inSortedRange:(NSRange)range options:(NSBinarySearchingOptions)opts usingComparator:(NSComparator NS_NOESCAPE)cmp; // binary search
 
-- (NSArray<ObjectType> *)sortedArrayUsingComparator:(NSComparator)cmptr;
-- (NSArray<ObjectType> *)sortedArrayWithOptions:(NSSortOptions)opts usingComparator:(NSComparator)cmptr;
+- (NSArray<ObjectType> *)sortedArrayUsingComparator:(NSComparator NS_NOESCAPE)cmptr;
+- (NSArray<ObjectType> *)sortedArrayWithOptions:(NSSortOptions)opts usingComparator:(NSComparator NS_NOESCAPE)cmptr;
 
 @property (readonly, copy) NSString *description;
 - (NSString *)descriptionWithLocale:(nullable id)locale;
@@ -153,9 +153,9 @@
 - (void)unionSet:(NSSet<ObjectType> *)other;
 
 #if NS_BLOCKS_AVAILABLE
-- (void)sortUsingComparator:(NSComparator)cmptr;
-- (void)sortWithOptions:(NSSortOptions)opts usingComparator:(NSComparator)cmptr;
-- (void)sortRange:(NSRange)range options:(NSSortOptions)opts usingComparator:(NSComparator)cmptr;
+- (void)sortUsingComparator:(NSComparator NS_NOESCAPE)cmptr;
+- (void)sortWithOptions:(NSSortOptions)opts usingComparator:(NSComparator NS_NOESCAPE)cmptr;
+- (void)sortRange:(NSRange)range options:(NSSortOptions)opts usingComparator:(NSComparator NS_NOESCAPE)cmptr;
 #endif
 
 @end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPathUtilities.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPathUtilities.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPathUtilities.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPathUtilities.h	2016-05-20 07:24:14.000000000 +0200
@@ -31,9 +31,14 @@
 
 - (NSArray<NSString *> *)stringsByAppendingPaths:(NSArray<NSString *> *)paths;
 
-- (NSUInteger)completePathIntoString:(NSString * __nonnull * __nullable)outputName caseSensitive:(BOOL)flag matchesIntoArray:(NSArray<NSString *> * __nonnull * __nullable)outputArray filterTypes:(nullable NSArray<NSString *> *)filterTypes;
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 6)
+- (NSUInteger)completePathIntoString:(NSString * _Nullable * _Nullable)outputName caseSensitive:(BOOL)flag matchesIntoArray:(NSArray<NSString *> * _Nullable * _Nullable)outputArray filterTypes:(nullable NSArray<NSString *> *)filterTypes;
+#else
+- (NSUInteger)completePathIntoString:(NSString * _Nonnull * _Nullable)outputName caseSensitive:(BOOL)flag matchesIntoArray:(NSArray<NSString *> * _Nonnull * _Nullable)outputArray filterTypes:(nullable NSArray<NSString *> *)filterTypes;
+#endif
 
-@property (readonly) __strong const char *fileSystemRepresentation NS_RETURNS_INNER_POINTER;
+
+@property (readonly) const char *fileSystemRepresentation NS_RETURNS_INNER_POINTER;
 - (BOOL)getFileSystemRepresentation:(char *)cname maxLength:(NSUInteger)max;
 
 @end
@@ -48,7 +53,7 @@
 FOUNDATION_EXPORT NSString *NSFullUserName(void);
 
 FOUNDATION_EXPORT NSString *NSHomeDirectory(void);
-FOUNDATION_EXPORT NSString * __nullable NSHomeDirectoryForUser(NSString * __nullable userName);
+FOUNDATION_EXPORT NSString * _Nullable NSHomeDirectoryForUser(NSString * _Nullable userName);
 
 FOUNDATION_EXPORT NSString *NSTemporaryDirectory(void);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPersonNameComponentsFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPersonNameComponentsFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPersonNameComponentsFormatter.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPersonNameComponentsFormatter.h	2016-05-20 07:35:40.000000000 +0200
@@ -63,9 +63,12 @@
  */
 - (NSAttributedString *)annotatedStringFromPersonNameComponents:(NSPersonNameComponents *)components;
 
-/* NSPersonNameComponentsFormatter currently only implements formatting, not parsing. Until it implements parsing, this will always return NO.
+
+/* Convenience method on getObjectValue:forString:error:. Returns an NSPersonNameComponents object representing the name components found in the provided string.
  */
-- (BOOL)getObjectValue:(out id __nullable * __nullable)obj forString:(NSString *)string errorDescription:(out NSString * __nullable * __nullable)error;
+- (nullable NSPersonNameComponents *)personNameComponentsFromString:(nonnull NSString *)string API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+- (BOOL)getObjectValue:(out id _Nullable * _Nullable)obj forString:(NSString *)string errorDescription:(out NSString * _Nullable * _Nullable)error;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPointerFunctions.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPointerFunctions.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPointerFunctions.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPointerFunctions.h	2016-05-20 07:24:14.000000000 +0200
@@ -60,18 +60,22 @@
 + (NSPointerFunctions *)pointerFunctionsWithOptions:(NSPointerFunctionsOptions)options;
 
 // pointer personality functions
-@property (nullable) NSUInteger (*hashFunction)(const void *item, NSUInteger (* __nullable size)(const void *item));
-@property (nullable) BOOL (*isEqualFunction)(const void *item1, const void*item2, NSUInteger (* __nullable size)(const void *item));
+@property (nullable) NSUInteger (*hashFunction)(const void *item, NSUInteger (* _Nullable size)(const void *item));
+@property (nullable) BOOL (*isEqualFunction)(const void *item1, const void*item2, NSUInteger (* _Nullable size)(const void *item));
 @property (nullable) NSUInteger (*sizeFunction)(const void *item);
-@property (nullable) NSString * __nullable (*descriptionFunction)(const void *item);
+@property (nullable) NSString * _Nullable (*descriptionFunction)(const void *item);
 
 // custom memory configuration
-@property (nullable) void (*relinquishFunction)(const void *item, NSUInteger (* __nullable size)(const void *item));
-@property (nullable) void * __nonnull (*acquireFunction)(const void *src, NSUInteger (* __nullable size)(const void *item), BOOL shouldCopy);
+@property (nullable) void (*relinquishFunction)(const void *item, NSUInteger (* _Nullable size)(const void *item));
+@property (nullable) void * _Nonnull (*acquireFunction)(const void *src, NSUInteger (* _Nullable size)(const void *item), BOOL shouldCopy);
 
-// GC requires that read and write barrier functions be used when pointers are from GC memory
-@property BOOL usesStrongWriteBarrier;             // pointers should (not) be assigned using the GC strong write barrier
-@property BOOL usesWeakReadAndWriteBarriers;       // pointers should (not) use GC weak read and write barriers
+
+// GC used to require that read and write barrier functions be used when pointers are from GC memory
+@property BOOL usesStrongWriteBarrier // pointers should (not) be assigned using the GC strong write barrier
+    API_DEPRECATED("Garbage collection no longer supported", macosx(10.5, 10.12), ios(2.0, 10.0), watchos(2.0, 3.0), tvos(9.0, 10.0));
+
+@property BOOL usesWeakReadAndWriteBarriers       // pointers should (not) use GC weak read and write barriers
+    API_DEPRECATED("Garbage collection no longer supported", macosx(10.5, 10.12), ios(2.0, 10.0), watchos(2.0, 3.0), tvos(9.0, 10.0));
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPort.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPort.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPort.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPort.h	2016-05-20 07:39:55.000000000 +0200
@@ -3,6 +3,8 @@
 */
 
 #import <Foundation/NSObject.h>
+#import <Foundation/NSNotification.h>
+#import <Foundation/NSRunLoop.h>
 
 typedef int NSSocketNativeHandle;
 
@@ -13,7 +15,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-FOUNDATION_EXPORT NSString * const NSPortDidBecomeInvalidNotification;
+FOUNDATION_EXPORT NSNotificationName const NSPortDidBecomeInvalidNotification;
 
 @interface NSPort : NSObject <NSCopying, NSCoding>
 
@@ -35,8 +37,8 @@
 // to setup monitoring of the port when added to a run loop,
 // and stop monitoring if needed when removed;
 // These methods should not be called directly!
-- (void)scheduleInRunLoop:(NSRunLoop *)runLoop forMode:(NSString *)mode;
-- (void)removeFromRunLoop:(NSRunLoop *)runLoop forMode:(NSString *)mode;
+- (void)scheduleInRunLoop:(NSRunLoop *)runLoop forMode:(NSRunLoopMode)mode;
+- (void)removeFromRunLoop:(NSRunLoop *)runLoop forMode:(NSRunLoopMode)mode;
 
 // DO Transport API; subclassers should implement these methods
 // default is 0
@@ -55,8 +57,8 @@
 	// being used in the same program, this requires some care.
 
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE)) || (TARGET_OS_WIN32)
-- (void)addConnection:(NSConnection *)conn toRunLoop:(NSRunLoop *)runLoop forMode:(NSString *)mode NS_SWIFT_UNAVAILABLE("Use NSXPCConnection instead");
-- (void)removeConnection:(NSConnection *)conn fromRunLoop:(NSRunLoop *)runLoop forMode:(NSString *)mode NS_SWIFT_UNAVAILABLE("Use NSXPCConnection instead");
+- (void)addConnection:(NSConnection *)conn toRunLoop:(NSRunLoop *)runLoop forMode:(NSRunLoopMode)mode NS_SWIFT_UNAVAILABLE("Use NSXPCConnection instead");
+- (void)removeConnection:(NSConnection *)conn fromRunLoop:(NSRunLoop *)runLoop forMode:(NSRunLoopMode)mode NS_SWIFT_UNAVAILABLE("Use NSXPCConnection instead");
 	// The default implementation of these two methods is to
 	// simply add the receiving port to the run loop in the
 	// given mode.  Subclassers need not override these methods,
@@ -102,8 +104,8 @@
 
 @property (readonly) uint32_t machPort;
 
-- (void)scheduleInRunLoop:(NSRunLoop *)runLoop forMode:(NSString *)mode;
-- (void)removeFromRunLoop:(NSRunLoop *)runLoop forMode:(NSString *)mode;
+- (void)scheduleInRunLoop:(NSRunLoop *)runLoop forMode:(NSRunLoopMode)mode;
+- (void)removeFromRunLoop:(NSRunLoop *)runLoop forMode:(NSRunLoopMode)mode;
 	// If you subclass NSMachPort, you have to override these 2
 	// methods from NSPort; since this is complicated, subclassing
 	// NSMachPort is not recommended
@@ -126,7 +128,7 @@
 NS_AUTOMATED_REFCOUNT_WEAK_UNAVAILABLE 
 @interface NSMessagePort : NSPort {
     @private
-    void * __strong _port;
+    void *_port;
     id _delegate;
 }
 
@@ -139,10 +141,10 @@
 
 @interface NSSocketPort : NSPort {
     @private
-    void * __strong _receiver;
+    void *_receiver;
     id _connectors;
-    void * __strong _loops;
-    void * __strong _data;
+    void *_loops;
+    void *_data;
     id _signature;
     id _delegate;
     id _lock;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPredicate.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPredicate.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPredicate.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPredicate.h	2016-05-20 06:24:14.000000000 +0200
@@ -33,8 +33,11 @@
 
 + (NSPredicate *)predicateWithValue:(BOOL)value;    // return predicates that always evaluate to true/false
 
-+ (NSPredicate*)predicateWithBlock:(BOOL (^)(id evaluatedObject, NSDictionary<NSString *, id> * __nullable bindings))block NS_AVAILABLE(10_6, 4_0);
-
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 6)
++ (NSPredicate*)predicateWithBlock:(BOOL (^)(id _Nullable evaluatedObject, NSDictionary<NSString *, id> * _Nullable bindings))block NS_AVAILABLE(10_6, 4_0);
+#else
++ (NSPredicate*)predicateWithBlock:(BOOL (^)(id evaluatedObject, NSDictionary<NSString *, id> * _Nullable bindings))block NS_AVAILABLE(10_6, 4_0);
+#endif
 @property (readonly, copy) NSString *predicateFormat;    // returns the format string of the predicate
 
 - (instancetype)predicateWithSubstitutionVariables:(NSDictionary<NSString *, id> *)variables;    // substitute constant values for variables
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProcessInfo.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProcessInfo.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProcessInfo.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProcessInfo.h	2016-05-20 07:24:14.000000000 +0200
@@ -4,6 +4,7 @@
 
 #import <Foundation/NSObject.h>
 #import <Foundation/NSDate.h>
+#import <Foundation/NSNotification.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -176,6 +177,13 @@
 
 @end
 
+@interface NSProcessInfo (NSUserInformation)
+
+@property (readonly, copy) NSString *userName API_AVAILABLE(macosx(10.12)) API_UNAVAILABLE(ios, watchos, tvos);
+@property (readonly, copy) NSString *fullUserName API_AVAILABLE(macosx(10.12)) API_UNAVAILABLE(ios, watchos, tvos);
+
+@end
+
 // Describes the current thermal state of the system.
 typedef NS_ENUM(NSInteger, NSProcessInfoThermalState) {
     // No corrective action is needed.
@@ -212,7 +220,7 @@
  
  This notification is posted on the global dispatch queue. Register for it using the default notification center. The object associated with the notification is +[NSProcessInfo processInfo].
 */
-FOUNDATION_EXTERN NSString * const NSProcessInfoThermalStateDidChangeNotification NS_AVAILABLE(10_10_3, NA);
+FOUNDATION_EXTERN NSNotificationName const NSProcessInfoThermalStateDidChangeNotification NS_AVAILABLE(10_10_3, NA);
 
 /*
  NSProcessInfoPowerStateDidChangeNotification is posted once any power usage mode of the system has changed. Once the notification is posted, use the isLowPowerModeEnabled property to retrieve the current state of the low power mode setting of the system.
@@ -221,6 +229,6 @@
  
  This notification is posted on the global dispatch queue. Register for it using the default notification center. The object associated with the notification is +[NSProcessInfo processInfo].
  */
-FOUNDATION_EXTERN NSString * const NSProcessInfoPowerStateDidChangeNotification NS_AVAILABLE(NA, 9_0);
+FOUNDATION_EXTERN NSNotificationName const NSProcessInfoPowerStateDidChangeNotification NS_AVAILABLE(NA, 9_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProgress.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProgress.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProgress.h	2015-08-11 04:24:37.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProgress.h	2016-05-20 06:12:55.000000000 +0200
@@ -8,6 +8,9 @@
 
 @class NSDictionary, NSMutableDictionary, NSMutableSet, NSURL, NSUUID, NSXPCConnection, NSLock;
 
+typedef NSString * NSProgressKind NS_EXTENSIBLE_STRING_ENUM;
+typedef NSString * NSProgressFileOperationKind NS_EXTENSIBLE_STRING_ENUM;
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*
@@ -31,7 +34,7 @@
 NS_CLASS_AVAILABLE(10_9, 7_0)
 @interface NSProgress : NSObject {
 @private
-    __weak NSProgress *_parent;
+    NSProgress *_parent;
     int64_t _reserved4;
     id _values;
     void (^ _resumingHandler)(void);
@@ -41,11 +44,11 @@
     uint64_t _flags;
     id _userInfoProxy;
     NSString *_publisherID;
-    NSXPCConnection *_connection;
-    NSInteger _unpublishingBlockageCount;
-    NSInteger _disconnectingBlockageCount;
-    NSInteger _remoteObserverCount;
-    NSMutableDictionary *_acknowledgementHandlersByBundleID;
+    id _reserved5;
+    NSInteger _reserved6;
+    NSInteger _reserved7;
+    NSInteger _reserved8;
+    NSMutableDictionary *_acknowledgementHandlersByLowercaseBundleID;
     NSMutableDictionary *_lastNotificationTimesByKey;
     NSMutableDictionary *_userInfoLastNotificationTimesByKey;
     NSLock *_lock;
@@ -172,7 +175,7 @@
 
 /* Either a string identifying what kind of progress is being made, like NSProgressKindFile, or nil. If the value of the localizedDescription property has not been set to a non-nil value then the default implementation of -localizedDescription uses the progress kind to determine how to use the values of other properties, as well as values in the user info dictionary, to create a string that is presentable to the user. This is most useful when -localizedDescription is actually being invoked in another process, whose localization language may be different, as a result of using the publish and subscribe mechanism described here.
 */
-@property (nullable, copy) NSString *kind;
+@property (nullable, copy) NSProgressKind kind;
 
 #pragma mark *** Reporting Progress to Other Processes (OS X Only) ***
 
@@ -191,7 +194,7 @@
 #pragma mark *** Observing and Controlling File Progress by Other Processes (OS X Only) ***
 
 typedef void (^NSProgressUnpublishingHandler)(void);
-typedef __nullable NSProgressUnpublishingHandler (^NSProgressPublishingHandler)(NSProgress *progress);
+typedef _Nullable NSProgressUnpublishingHandler (^NSProgressPublishingHandler)(NSProgress *progress);
 
 /* Register to hear about file progress. The passed-in block will be invoked when -publish has been sent to an NSProgress whose NSProgressFileURLKey user info dictionary entry is an NSURL locating the same item located by the passed-in NSURL, or an item directly contained by it. The NSProgress passed to your block will be a proxy of the one that was published. The passed-in block may return another block. If it does, then that returned block will be invoked when the corresponding invocation of -unpublish is made, or the publishing process terminates, or +removeSubscriber: is invoked. Your blocks will be invoked on the main thread.
 */
@@ -215,49 +218,51 @@
 @property (readonly) NSProgress *progress;
 @end
 
+typedef NSString * NSProgressKey NS_EXTENSIBLE_STRING_ENUM;
+
 #pragma mark *** Details of General Progress ***
 
 /* How much time is probably left in the operation, as an NSNumber containing a number of seconds.
 */
-FOUNDATION_EXPORT NSString *const NSProgressEstimatedTimeRemainingKey NS_AVAILABLE(10_9, 7_0);
+FOUNDATION_EXPORT NSProgressKey const NSProgressEstimatedTimeRemainingKey NS_AVAILABLE(10_9, 7_0);
 
 /* How fast data is being processed, as an NSNumber containing bytes per second.
 */
-FOUNDATION_EXPORT NSString *const NSProgressThroughputKey NS_AVAILABLE(10_9, 7_0);
+FOUNDATION_EXPORT NSProgressKey const NSProgressThroughputKey NS_AVAILABLE(10_9, 7_0);
 
 #pragma mark *** Details of File Progress ***
 
 /* The value for the kind property that indicates that the work being done is one of the kind of file operations listed below. NSProgress of this kind is assumed to use bytes as the unit of work being done and the default implementation of -localizedDescription takes advantage of that to return more specific text than it could otherwise. The NSProgressFileTotalCountKey and NSProgressFileCompletedCountKey keys in the userInfo dictionary are used for the overall count of files.
 */
-FOUNDATION_EXPORT NSString *const NSProgressKindFile NS_AVAILABLE(10_9, 7_0);
+FOUNDATION_EXPORT NSProgressKind const NSProgressKindFile NS_AVAILABLE(10_9, 7_0);
 
 /* A user info dictionary key, for an entry that is required when the value for the kind property is NSProgressKindFile. The value must be one of the strings listed in the next section. The default implementations of of -localizedDescription and -localizedItemDescription use this value to determine the text that they return.
 */
-FOUNDATION_EXPORT NSString *const NSProgressFileOperationKindKey NS_AVAILABLE(10_9, 7_0);
+FOUNDATION_EXPORT NSProgressKey const NSProgressFileOperationKindKey NS_AVAILABLE(10_9, 7_0);
 
 /* Possible values for NSProgressFileOperationKindKey entries.
 */
-FOUNDATION_EXPORT NSString *const NSProgressFileOperationKindDownloading NS_AVAILABLE(10_9, 7_0);
-FOUNDATION_EXPORT NSString *const NSProgressFileOperationKindDecompressingAfterDownloading NS_AVAILABLE(10_9, 7_0);
-FOUNDATION_EXPORT NSString *const NSProgressFileOperationKindReceiving NS_AVAILABLE(10_9, 7_0);
-FOUNDATION_EXPORT NSString *const NSProgressFileOperationKindCopying NS_AVAILABLE(10_9, 7_0);
+FOUNDATION_EXPORT NSProgressFileOperationKind const NSProgressFileOperationKindDownloading NS_AVAILABLE(10_9, 7_0);
+FOUNDATION_EXPORT NSProgressFileOperationKind const NSProgressFileOperationKindDecompressingAfterDownloading NS_AVAILABLE(10_9, 7_0);
+FOUNDATION_EXPORT NSProgressFileOperationKind const NSProgressFileOperationKindReceiving NS_AVAILABLE(10_9, 7_0);
+FOUNDATION_EXPORT NSProgressFileOperationKind const NSProgressFileOperationKindCopying NS_AVAILABLE(10_9, 7_0);
 
 /* A user info dictionary key. The value must be an NSURL identifying the item on which progress is being made. This is required for any NSProgress that is published using -publish to be reported to subscribers registered with +addSubscriberForFileURL:withPublishingHandler:.
 */
-FOUNDATION_EXPORT NSString *const NSProgressFileURLKey NS_AVAILABLE(10_9, 7_0);
+FOUNDATION_EXPORT NSProgressKey const NSProgressFileURLKey NS_AVAILABLE(10_9, 7_0);
 
 /* User info dictionary keys. The values must be NSNumbers containing integers. These entries are optional but if they are both present then the default implementation of -localizedAdditionalDescription uses them to determine the text that it returns.
 */
-FOUNDATION_EXPORT NSString *const NSProgressFileTotalCountKey NS_AVAILABLE(10_9, 7_0);
-FOUNDATION_EXPORT NSString *const NSProgressFileCompletedCountKey NS_AVAILABLE(10_9, 7_0);
+FOUNDATION_EXPORT NSProgressKey const NSProgressFileTotalCountKey NS_AVAILABLE(10_9, 7_0);
+FOUNDATION_EXPORT NSProgressKey const NSProgressFileCompletedCountKey NS_AVAILABLE(10_9, 7_0);
 
 /* User info dictionary keys. The value for the first entry must be an NSImage, typically an icon. The value for the second entry must be an NSValue containing an NSRect, in screen coordinates, locating the image where it initially appears on the screen.
 */
-FOUNDATION_EXPORT NSString *const NSProgressFileAnimationImageKey NS_AVAILABLE(10_9, NA);
-FOUNDATION_EXPORT NSString *const NSProgressFileAnimationImageOriginalRectKey NS_AVAILABLE(10_9, NA);
+FOUNDATION_EXPORT NSProgressKey const NSProgressFileAnimationImageKey NS_AVAILABLE(10_9, NA);
+FOUNDATION_EXPORT NSProgressKey const NSProgressFileAnimationImageOriginalRectKey NS_AVAILABLE(10_9, NA);
 
 /* A user info dictionary key. The value must be an NSImage containing an icon. This entry is optional but, if it is present, the Finder will use it to show the icon of a file while progress is being made on that file. For example, the App Store uses this to specify an icon for an application being downloaded before the icon can be gotten from the application bundle itself.
 */
-FOUNDATION_EXPORT NSString *const NSProgressFileIconKey NS_AVAILABLE(10_9, NA);
+FOUNDATION_EXPORT NSProgressKey const NSProgressFileIconKey NS_AVAILABLE(10_9, NA);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPropertyList.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPropertyList.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPropertyList.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPropertyList.h	2016-05-20 06:12:55.000000000 +0200
@@ -51,11 +51,11 @@
 
 /* This method is deprecated. Use dataWithPropertyList:format:options:error: instead.
  */
-+ (nullable NSData *)dataFromPropertyList:(id)plist format:(NSPropertyListFormat)format errorDescription:(out __strong NSString * __nullable * __nullable)errorString NS_DEPRECATED(10_0, 10_10, 2_0, 8_0, "Use dataWithPropertyList:format:options:error: instead.");
++ (nullable NSData *)dataFromPropertyList:(id)plist format:(NSPropertyListFormat)format errorDescription:(out __strong NSString * _Nullable * _Nullable)errorString NS_DEPRECATED(10_0, 10_10, 2_0, 8_0, "Use dataWithPropertyList:format:options:error: instead.");
 
 /* This method is deprecated. Use propertyListWithData:options:format:error: instead.
  */
-+ (nullable id)propertyListFromData:(NSData *)data mutabilityOption:(NSPropertyListMutabilityOptions)opt format:(nullable NSPropertyListFormat *)format errorDescription:(out __strong NSString * __nullable * __nullable)errorString NS_DEPRECATED(10_0, 10_10, 2_0, 8_0, "Use propertyListWithData:options:format:error: instead.");
++ (nullable id)propertyListFromData:(NSData *)data mutabilityOption:(NSPropertyListMutabilityOptions)opt format:(nullable NSPropertyListFormat *)format errorDescription:(out __strong NSString * _Nullable * _Nullable)errorString NS_DEPRECATED(10_0, 10_10, 2_0, 8_0, "Use propertyListWithData:options:format:error: instead.");
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSRegularExpression.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSRegularExpression.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSRegularExpression.h	2016-02-20 02:19:18.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSRegularExpression.h	2016-05-20 07:35:40.000000000 +0200
@@ -71,7 +71,7 @@
 /* The fundamental matching method on NSRegularExpression is a block iterator.  There are several additional convenience methods, for returning all matches at once, the number of matches, the first match, or the range of the first match.  Each match is specified by an instance of NSTextCheckingResult (of type NSTextCheckingTypeRegularExpression) in which the overall match range is given by the range property (equivalent to rangeAtIndex:0) and any capture group ranges are given by rangeAtIndex: for indexes from 1 to numberOfCaptureGroups.  {NSNotFound, 0} is used if a particular capture group does not participate in the match.
 */
 
-- (void)enumerateMatchesInString:(NSString *)string options:(NSMatchingOptions)options range:(NSRange)range usingBlock:(void (^)(NSTextCheckingResult * __nullable result, NSMatchingFlags flags, BOOL *stop))block;
+- (void)enumerateMatchesInString:(NSString *)string options:(NSMatchingOptions)options range:(NSRange)range usingBlock:(void (NS_NOESCAPE ^)(NSTextCheckingResult * _Nullable result, NSMatchingFlags flags, BOOL *stop))block;
 
 - (NSArray<NSTextCheckingResult *> *)matchesInString:(NSString *)string options:(NSMatchingOptions)options range:(NSRange)range;
 - (NSUInteger)numberOfMatchesInString:(NSString *)string options:(NSMatchingOptions)options range:(NSRange)range;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSRunLoop.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSRunLoop.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSRunLoop.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSRunLoop.h	2016-05-20 06:24:14.000000000 +0200
@@ -10,8 +10,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-FOUNDATION_EXPORT NSString * const NSDefaultRunLoopMode;
-FOUNDATION_EXPORT NSString * const NSRunLoopCommonModes NS_AVAILABLE(10_5, 2_0);
+FOUNDATION_EXPORT NSRunLoopMode const NSDefaultRunLoopMode;
+FOUNDATION_EXPORT NSRunLoopMode const NSRunLoopCommonModes NS_AVAILABLE(10_5, 2_0);
 
 @interface NSRunLoop : NSObject {
 @private
@@ -26,17 +26,17 @@
 + (NSRunLoop *)currentRunLoop;
 + (NSRunLoop *)mainRunLoop NS_AVAILABLE(10_5, 2_0);
 
-@property (nullable, readonly, copy) NSString *currentMode;
+@property (nullable, readonly, copy) NSRunLoopMode currentMode;
 
 - (CFRunLoopRef)getCFRunLoop CF_RETURNS_NOT_RETAINED;
 
-- (void)addTimer:(NSTimer *)timer forMode:(NSString *)mode;
+- (void)addTimer:(NSTimer *)timer forMode:(NSRunLoopMode)mode;
 
-- (void)addPort:(NSPort *)aPort forMode:(NSString *)mode;
-- (void)removePort:(NSPort *)aPort forMode:(NSString *)mode;
+- (void)addPort:(NSPort *)aPort forMode:(NSRunLoopMode)mode;
+- (void)removePort:(NSPort *)aPort forMode:(NSRunLoopMode)mode;
 
-- (nullable NSDate *)limitDateForMode:(NSString *)mode;
-- (void)acceptInputForMode:(NSString *)mode beforeDate:(NSDate *)limitDate;
+- (nullable NSDate *)limitDateForMode:(NSRunLoopMode)mode;
+- (void)acceptInputForMode:(NSRunLoopMode)mode beforeDate:(NSDate *)limitDate;
 
 @end
 
@@ -44,7 +44,7 @@
 
 - (void)run; 
 - (void)runUntilDate:(NSDate *)limitDate;
-- (BOOL)runMode:(NSString *)mode beforeDate:(NSDate *)limitDate;
+- (BOOL)runMode:(NSRunLoopMode)mode beforeDate:(NSDate *)limitDate;
 
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
 - (void)configureAsServer NS_DEPRECATED(10_0, 10_5, 2_0, 2_0);
@@ -56,7 +56,7 @@
 
 @interface NSObject (NSDelayedPerforming)
 
-- (void)performSelector:(SEL)aSelector withObject:(nullable id)anArgument afterDelay:(NSTimeInterval)delay inModes:(NSArray<NSString *> *)modes;
+- (void)performSelector:(SEL)aSelector withObject:(nullable id)anArgument afterDelay:(NSTimeInterval)delay inModes:(NSArray<NSRunLoopMode> *)modes;
 - (void)performSelector:(SEL)aSelector withObject:(nullable id)anArgument afterDelay:(NSTimeInterval)delay;
 + (void)cancelPreviousPerformRequestsWithTarget:(id)aTarget selector:(SEL)aSelector object:(nullable id)anArgument;
 + (void)cancelPreviousPerformRequestsWithTarget:(id)aTarget;
@@ -65,7 +65,7 @@
 
 @interface NSRunLoop (NSOrderedPerform)
 
-- (void)performSelector:(SEL)aSelector target:(id)target argument:(nullable id)arg order:(NSUInteger)order modes:(NSArray<NSString *> *)modes;
+- (void)performSelector:(SEL)aSelector target:(id)target argument:(nullable id)arg order:(NSUInteger)order modes:(NSArray<NSRunLoopMode> *)modes;
 - (void)cancelPerformSelector:(SEL)aSelector target:(id)target argument:(nullable id)arg;
 - (void)cancelPerformSelectorsWithTarget:(id)target;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSScanner.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSScanner.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSScanner.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSScanner.h	2016-05-20 06:24:14.000000000 +0200
@@ -34,11 +34,11 @@
 - (BOOL)scanHexFloat:(nullable float *)result NS_AVAILABLE(10_5, 2_0);                   // Corresponding to %a or %A formatting. Requires "0x" or "0X" prefix.
 - (BOOL)scanHexDouble:(nullable double *)result NS_AVAILABLE(10_5, 2_0);                 // Corresponding to %a or %A formatting. Requires "0x" or "0X" prefix.
 
-- (BOOL)scanString:(NSString *)string intoString:(NSString * __nullable * __nullable)result;
-- (BOOL)scanCharactersFromSet:(NSCharacterSet *)set intoString:(NSString * __nullable * __nullable)result;
+- (BOOL)scanString:(NSString *)string intoString:(NSString * _Nullable * _Nullable)result;
+- (BOOL)scanCharactersFromSet:(NSCharacterSet *)set intoString:(NSString * _Nullable * _Nullable)result;
 
-- (BOOL)scanUpToString:(NSString *)string intoString:(NSString * __nullable * __nullable)result;
-- (BOOL)scanUpToCharactersFromSet:(NSCharacterSet *)set intoString:(NSString * __nullable * __nullable)result;
+- (BOOL)scanUpToString:(NSString *)string intoString:(NSString * _Nullable * _Nullable)result;
+- (BOOL)scanUpToCharactersFromSet:(NSCharacterSet *)set intoString:(NSString * _Nullable * _Nullable)result;
 
 @property (getter=isAtEnd, readonly) BOOL atEnd;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSSet.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSSet.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSSet.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSSet.h	2016-05-20 07:24:14.000000000 +0200
@@ -17,7 +17,7 @@
 - (nullable ObjectType)member:(ObjectType)object;
 - (NSEnumerator<ObjectType> *)objectEnumerator;
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
-- (instancetype)initWithObjects:(const ObjectType [])objects count:(NSUInteger)cnt NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithObjects:(const ObjectType _Nonnull [_Nullable])objects count:(NSUInteger)cnt NS_DESIGNATED_INITIALIZER;
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
 
 @end
@@ -40,11 +40,11 @@
 - (NSSet<ObjectType> *)setByAddingObjectsFromSet:(NSSet<ObjectType> *)other NS_AVAILABLE(10_5, 2_0);
 - (NSSet<ObjectType> *)setByAddingObjectsFromArray:(NSArray<ObjectType> *)other NS_AVAILABLE(10_5, 2_0);
 
-- (void)enumerateObjectsUsingBlock:(void (^)(ObjectType obj, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
-- (void)enumerateObjectsWithOptions:(NSEnumerationOptions)opts usingBlock:(void (^)(ObjectType obj, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
+- (void)enumerateObjectsUsingBlock:(void (NS_NOESCAPE ^)(ObjectType obj, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
+- (void)enumerateObjectsWithOptions:(NSEnumerationOptions)opts usingBlock:(void (NS_NOESCAPE ^)(ObjectType obj, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
 
-- (NSSet<ObjectType> *)objectsPassingTest:(BOOL (^)(ObjectType obj, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
-- (NSSet<ObjectType> *)objectsWithOptions:(NSEnumerationOptions)opts passingTest:(BOOL (^)(ObjectType obj, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
+- (NSSet<ObjectType> *)objectsPassingTest:(BOOL (NS_NOESCAPE ^)(ObjectType obj, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
+- (NSSet<ObjectType> *)objectsWithOptions:(NSEnumerationOptions)opts passingTest:(BOOL (NS_NOESCAPE ^)(ObjectType obj, BOOL *stop))predicate NS_AVAILABLE(10_6, 4_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSStream.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSStream.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSStream.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSStream.h	2016-05-20 06:24:14.000000000 +0200
@@ -3,10 +3,13 @@
 */
 
 #import <Foundation/NSObject.h>
+#import <Foundation/NSError.h>
 
 @class NSData, NSDictionary, NSError, NSHost, NSInputStream, NSOutputStream, NSRunLoop, NSString, NSURL;
 @protocol NSStreamDelegate;
 
+typedef NSString * NSStreamPropertyKey NS_EXTENSIBLE_STRING_ENUM;
+
 NS_ASSUME_NONNULL_BEGIN
 
 typedef NS_ENUM(NSUInteger, NSStreamStatus) {
@@ -41,8 +44,8 @@
 - (nullable id)propertyForKey:(NSString *)key;
 - (BOOL)setProperty:(nullable id)property forKey:(NSString *)key;
 
-- (void)scheduleInRunLoop:(NSRunLoop *)aRunLoop forMode:(NSString *)mode;
-- (void)removeFromRunLoop:(NSRunLoop *)aRunLoop forMode:(NSString *)mode;
+- (void)scheduleInRunLoop:(NSRunLoop *)aRunLoop forMode:(NSRunLoopMode)mode;
+- (void)removeFromRunLoop:(NSRunLoop *)aRunLoop forMode:(NSRunLoopMode)mode;
 
 @property (readonly) NSStreamStatus streamStatus;
 @property (nullable, readonly, copy) NSError *streamError;
@@ -54,7 +57,7 @@
 - (NSInteger)read:(uint8_t *)buffer maxLength:(NSUInteger)len;
     // reads up to length bytes into the supplied buffer, which must be at least of size len. Returns the actual number of bytes read.
 
-- (BOOL)getBuffer:(uint8_t * __nullable * __nonnull)buffer length:(NSUInteger *)len;
+- (BOOL)getBuffer:(uint8_t * _Nullable * _Nonnull)buffer length:(NSUInteger *)len;
     // returns in O(1) a pointer to the buffer in 'buffer' and by reference in 'len' how many bytes are available. This buffer is only valid until the next stream operation. Subclassers may return NO for this if it is not appropriate for the stream type. This may return NO if the buffer is not available.
 
 @property (readonly) BOOL hasBytesAvailable;
@@ -83,16 +86,16 @@
 
 @interface NSStream (NSSocketStreamCreationExtensions)
 
-+ (void)getStreamsToHostWithName:(NSString *)hostname port:(NSInteger)port inputStream:(NSInputStream * __nullable * __nullable)inputStream outputStream:(NSOutputStream * __nullable * __nullable)outputStream NS_AVAILABLE(10_10, 8_0) __WATCHOS_PROHIBITED;
++ (void)getStreamsToHostWithName:(NSString *)hostname port:(NSInteger)port inputStream:(NSInputStream * _Nullable * _Nullable)inputStream outputStream:(NSOutputStream * _Nullable * _Nullable)outputStream NS_AVAILABLE(10_10, 8_0) __WATCHOS_PROHIBITED;
 
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
-+ (void)getStreamsToHost:(NSHost *)host port:(NSInteger)port inputStream:(NSInputStream * __nullable * __nullable)inputStream outputStream:(NSOutputStream * __nullable * __nullable)outputStream NS_DEPRECATED_MAC(10_3, 10_10, "Please use getStreamsToHostWithName:port:inputStream:outputStream: instead");
++ (void)getStreamsToHost:(NSHost *)host port:(NSInteger)port inputStream:(NSInputStream * _Nullable * _Nullable)inputStream outputStream:(NSOutputStream * _Nullable * _Nullable)outputStream NS_DEPRECATED_MAC(10_3, 10_10, "Please use getStreamsToHostWithName:port:inputStream:outputStream: instead");
 #endif
 
 @end
 
 @interface NSStream (NSStreamBoundPairCreationExtensions)
-+ (void)getBoundStreamsWithBufferSize:(NSUInteger)bufferSize inputStream:(NSInputStream * __nullable * __nullable)inputStream outputStream:(NSOutputStream * __nullable * __nullable)outputStream NS_AVAILABLE(10_10, 8_0);
++ (void)getBoundStreamsWithBufferSize:(NSUInteger)bufferSize inputStream:(NSInputStream * _Nullable * _Nullable)inputStream outputStream:(NSOutputStream * _Nullable * _Nullable)outputStream NS_AVAILABLE(10_10, 8_0);
 @end
 
 // The NSInputStreamExtensions category contains additional initializers and convenience routines for dealing with NSInputStreams.
@@ -121,53 +124,62 @@
 
 // NSString constants for the propertyForKey/setProperty:forKey: API
 // String constants for the setting of the socket security level.
-FOUNDATION_EXPORT NSString * const NSStreamSocketSecurityLevelKey		NS_AVAILABLE(10_3, 2_0);	// use this as the key for setting one of the following values for the security level of the target stream.
+FOUNDATION_EXPORT NSStreamPropertyKey const NSStreamSocketSecurityLevelKey		NS_AVAILABLE(10_3, 2_0);	// use this as the key for setting one of the following values for the security level of the target stream.
+
+typedef NSString * NSStreamSocketSecurityLevel NS_STRING_ENUM;
+
+FOUNDATION_EXPORT NSStreamSocketSecurityLevel const NSStreamSocketSecurityLevelNone		NS_AVAILABLE(10_3, 2_0);
+FOUNDATION_EXPORT NSStreamSocketSecurityLevel const NSStreamSocketSecurityLevelSSLv2		NS_AVAILABLE(10_3, 2_0);
+FOUNDATION_EXPORT NSStreamSocketSecurityLevel const NSStreamSocketSecurityLevelSSLv3		NS_AVAILABLE(10_3, 2_0);
+FOUNDATION_EXPORT NSStreamSocketSecurityLevel const NSStreamSocketSecurityLevelTLSv1		NS_AVAILABLE(10_3, 2_0);
+FOUNDATION_EXPORT NSStreamSocketSecurityLevel const NSStreamSocketSecurityLevelNegotiatedSSL	NS_AVAILABLE(10_3, 2_0);
 
-FOUNDATION_EXPORT NSString * const NSStreamSocketSecurityLevelNone		NS_AVAILABLE(10_3, 2_0);
-FOUNDATION_EXPORT NSString * const NSStreamSocketSecurityLevelSSLv2		NS_AVAILABLE(10_3, 2_0);
-FOUNDATION_EXPORT NSString * const NSStreamSocketSecurityLevelSSLv3		NS_AVAILABLE(10_3, 2_0);
-FOUNDATION_EXPORT NSString * const NSStreamSocketSecurityLevelTLSv1		NS_AVAILABLE(10_3, 2_0);
-FOUNDATION_EXPORT NSString * const NSStreamSocketSecurityLevelNegotiatedSSL	NS_AVAILABLE(10_3, 2_0);
+FOUNDATION_EXPORT NSStreamPropertyKey const NSStreamSOCKSProxyConfigurationKey		NS_AVAILABLE(10_3, 2_0);	// Value is an NSDictionary containing the key/value pairs below. The dictionary returned from SystemConfiguration for SOCKS proxies will work without alteration.
 
-FOUNDATION_EXPORT NSString * const NSStreamSOCKSProxyConfigurationKey		NS_AVAILABLE(10_3, 2_0);	// Value is an NSDictionary containing the key/value pairs below. The dictionary returned from SystemConfiguration for SOCKS proxies will work without alteration.
+typedef NSString * NSStreamSOCKSProxyConfiguration NS_STRING_ENUM;
 
-FOUNDATION_EXPORT NSString * const NSStreamSOCKSProxyHostKey			NS_AVAILABLE(10_3, 2_0);
+FOUNDATION_EXPORT NSStreamSOCKSProxyConfiguration const NSStreamSOCKSProxyHostKey			NS_AVAILABLE(10_3, 2_0);
     // Value is an NSString
-FOUNDATION_EXPORT NSString * const NSStreamSOCKSProxyPortKey			NS_AVAILABLE(10_3, 2_0);
+FOUNDATION_EXPORT NSStreamSOCKSProxyConfiguration const NSStreamSOCKSProxyPortKey			NS_AVAILABLE(10_3, 2_0);
     // Value is an NSNumber
-FOUNDATION_EXPORT NSString * const NSStreamSOCKSProxyVersionKey		NS_AVAILABLE(10_3, 2_0);
+FOUNDATION_EXPORT NSStreamSOCKSProxyConfiguration const NSStreamSOCKSProxyVersionKey		NS_AVAILABLE(10_3, 2_0);
     // Value is one of NSStreamSOCKSProxyVersion4 or NSStreamSOCKSProxyVersion5
-FOUNDATION_EXPORT NSString * const NSStreamSOCKSProxyUserKey			NS_AVAILABLE(10_3, 2_0);
+FOUNDATION_EXPORT NSStreamSOCKSProxyConfiguration const NSStreamSOCKSProxyUserKey			NS_AVAILABLE(10_3, 2_0);
     // Value is an NSString
-FOUNDATION_EXPORT NSString * const NSStreamSOCKSProxyPasswordKey		NS_AVAILABLE(10_3, 2_0);
+FOUNDATION_EXPORT NSStreamSOCKSProxyConfiguration const NSStreamSOCKSProxyPasswordKey		NS_AVAILABLE(10_3, 2_0);
     // Value is an NSString
 
-FOUNDATION_EXPORT NSString * const NSStreamSOCKSProxyVersion4			NS_AVAILABLE(10_3, 2_0);
+typedef NSString * NSStreamSOCKSProxyVersion NS_STRING_ENUM;
+
+FOUNDATION_EXPORT NSStreamSOCKSProxyVersion const NSStreamSOCKSProxyVersion4			NS_AVAILABLE(10_3, 2_0);
     // Value for NSStreamSOCKProxyVersionKey
-FOUNDATION_EXPORT NSString * const NSStreamSOCKSProxyVersion5			NS_AVAILABLE(10_3, 2_0);
+FOUNDATION_EXPORT NSStreamSOCKSProxyVersion const NSStreamSOCKSProxyVersion5			NS_AVAILABLE(10_3, 2_0);
     // Value for NSStreamSOCKProxyVersionKey
 
-FOUNDATION_EXPORT NSString * const NSStreamDataWrittenToMemoryStreamKey	NS_AVAILABLE(10_3, 2_0);
+FOUNDATION_EXPORT NSStreamPropertyKey const NSStreamDataWrittenToMemoryStreamKey	NS_AVAILABLE(10_3, 2_0);
     // Key for obtaining the data written to a memory stream.
 
-FOUNDATION_EXPORT NSString * const NSStreamFileCurrentOffsetKey		NS_AVAILABLE(10_3, 2_0);
+FOUNDATION_EXPORT NSStreamPropertyKey const NSStreamFileCurrentOffsetKey		NS_AVAILABLE(10_3, 2_0);
     // Value is an NSNumber representing the current absolute offset of the stream.
 
 // NSString constants for error domains.
-FOUNDATION_EXPORT NSString * const NSStreamSocketSSLErrorDomain			NS_AVAILABLE(10_3, 2_0);
+FOUNDATION_EXPORT NSErrorDomain const NSStreamSocketSSLErrorDomain			NS_AVAILABLE(10_3, 2_0);
     // SSL errors are to be interpreted via <Security/SecureTransport.h>
-FOUNDATION_EXPORT NSString * const NSStreamSOCKSErrorDomain			NS_AVAILABLE(10_3, 2_0);
+FOUNDATION_EXPORT NSErrorDomain const NSStreamSOCKSErrorDomain			NS_AVAILABLE(10_3, 2_0);
 
 // Property key to specify the type of service for the stream.  This
 // allows the system to properly handle the request with respect to
 // routing, suspension behavior and other networking related attributes
 // appropriate for the given service type.  The service types supported
 // are documented below.
-FOUNDATION_EXPORT NSString * const NSStreamNetworkServiceType		    NS_AVAILABLE(10_7, 4_0);
+FOUNDATION_EXPORT NSStreamPropertyKey const NSStreamNetworkServiceType		    NS_AVAILABLE(10_7, 4_0);
+
+typedef NSString * NSStreamNetworkServiceTypeValue NS_STRING_ENUM;
+
 // Supported network service types:
-FOUNDATION_EXPORT NSString * const NSStreamNetworkServiceTypeVoIP	    NS_AVAILABLE(10_7, 4_0);
-FOUNDATION_EXPORT NSString * const NSStreamNetworkServiceTypeVideo	    NS_AVAILABLE(10_7, 5_0);
-FOUNDATION_EXPORT NSString * const NSStreamNetworkServiceTypeBackground	    NS_AVAILABLE(10_7, 5_0);
-FOUNDATION_EXPORT NSString * const NSStreamNetworkServiceTypeVoice	    NS_AVAILABLE(10_7, 5_0);
+FOUNDATION_EXPORT NSStreamNetworkServiceTypeValue const NSStreamNetworkServiceTypeVoIP	    NS_AVAILABLE(10_7, 4_0);
+FOUNDATION_EXPORT NSStreamNetworkServiceTypeValue const NSStreamNetworkServiceTypeVideo	    NS_AVAILABLE(10_7, 5_0);
+FOUNDATION_EXPORT NSStreamNetworkServiceTypeValue const NSStreamNetworkServiceTypeBackground	    NS_AVAILABLE(10_7, 5_0);
+FOUNDATION_EXPORT NSStreamNetworkServiceTypeValue const NSStreamNetworkServiceTypeVoice	    NS_AVAILABLE(10_7, 5_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSString.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSString.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSString.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSString.h	2016-05-20 06:24:14.000000000 +0200
@@ -215,13 +215,13 @@
 
 /* In the enumerate methods, the blocks will be invoked inside an autorelease pool, so any values assigned inside the block should be retained.
 */
-- (void)enumerateSubstringsInRange:(NSRange)range options:(NSStringEnumerationOptions)opts usingBlock:(void (^)(NSString * __nullable substring, NSRange substringRange, NSRange enclosingRange, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
+- (void)enumerateSubstringsInRange:(NSRange)range options:(NSStringEnumerationOptions)opts usingBlock:(void (^)(NSString * _Nullable substring, NSRange substringRange, NSRange enclosingRange, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
 - (void)enumerateLinesUsingBlock:(void (^)(NSString *line, BOOL *stop))block NS_AVAILABLE(10_6, 4_0);
 
 
 #pragma mark *** Character encoding and converting to/from c-string representations ***
 
-@property (nullable, readonly) __strong const char *UTF8String NS_RETURNS_INNER_POINTER;	// Convenience to return null-terminated UTF8 representation
+@property (nullable, readonly) const char *UTF8String NS_RETURNS_INNER_POINTER;	// Convenience to return null-terminated UTF8 representation
 
 @property (readonly) NSStringEncoding fastestEncoding;    	// Result in O(1) time; a rough estimate
 @property (readonly) NSStringEncoding smallestEncoding;   	// Result in O(n) time; the encoding in which the string is most compact
@@ -233,7 +233,7 @@
 
 /* Methods to convert NSString to a NULL-terminated cString using the specified encoding. Note, these are the "new" cString methods, and are not deprecated like the older cString methods which do not take encoding arguments.
 */
-- (nullable __strong const char *)cStringUsingEncoding:(NSStringEncoding)encoding NS_RETURNS_INNER_POINTER;	// "Autoreleased"; NULL return if encoding conversion not possible; for performance reasons, lifetime of this should not be considered longer than the lifetime of the receiving string (if the receiver string is freed, this might go invalid then, before the end of the autorelease scope)
+- (nullable const char *)cStringUsingEncoding:(NSStringEncoding)encoding NS_RETURNS_INNER_POINTER;	// "Autoreleased"; NULL return if encoding conversion not possible; for performance reasons, lifetime of this should not be considered longer than the lifetime of the receiving string (if the receiver string is freed, this might go invalid then, before the end of the autorelease scope)
 - (BOOL)getCString:(char *)buffer maxLength:(NSUInteger)maxBufferCount encoding:(NSStringEncoding)encoding;	// NO return if conversion not possible due to encoding errors or too small of a buffer. The buffer should include room for maxBufferCount bytes; this number should accomodate the expected size of the return value plus the NULL termination character, which this method adds. (So note that the maxLength passed to this method is one more than the one you would have passed to the deprecated getCString:maxLength:.)
 
 /* Use this to convert string section at a time into a fixed-size buffer, without any allocations.  Does not NULL-terminate. 
@@ -291,26 +291,28 @@
 */
 - (NSString *)stringByReplacingCharactersInRange:(NSRange)range withString:(NSString *)replacement NS_AVAILABLE(10_5, 2_0);
 
+typedef NSString *NSStringTransform NS_EXTENSIBLE_STRING_ENUM;
+
 /* Perform string transliteration.  The transformation represented by transform is applied to the receiver. reverse indicates that the inverse transform should be used instead, if it exists. Attempting to use an invalid transform identifier or reverse an irreversible transform will return nil; otherwise the transformed string value is returned (even if no characters are actually transformed). You can pass one of the predefined transforms below (NSStringTransformLatinToKatakana, etc), or any valid ICU transform ID as defined in the ICU User Guide. Arbitrary ICU transform rules are not supported.
 */
-- (nullable NSString *)stringByApplyingTransform:(NSString *)transform reverse:(BOOL)reverse NS_AVAILABLE(10_11, 9_0);	// Returns nil if reverse not applicable or transform is invalid
+- (nullable NSString *)stringByApplyingTransform:(NSStringTransform)transform reverse:(BOOL)reverse NS_AVAILABLE(10_11, 9_0);	// Returns nil if reverse not applicable or transform is invalid
 
-FOUNDATION_EXPORT NSString * const NSStringTransformLatinToKatakana         NS_AVAILABLE(10_11, 9_0);
-FOUNDATION_EXPORT NSString * const NSStringTransformLatinToHiragana         NS_AVAILABLE(10_11, 9_0);
-FOUNDATION_EXPORT NSString * const NSStringTransformLatinToHangul           NS_AVAILABLE(10_11, 9_0);
-FOUNDATION_EXPORT NSString * const NSStringTransformLatinToArabic           NS_AVAILABLE(10_11, 9_0);
-FOUNDATION_EXPORT NSString * const NSStringTransformLatinToHebrew           NS_AVAILABLE(10_11, 9_0);
-FOUNDATION_EXPORT NSString * const NSStringTransformLatinToThai             NS_AVAILABLE(10_11, 9_0);
-FOUNDATION_EXPORT NSString * const NSStringTransformLatinToCyrillic         NS_AVAILABLE(10_11, 9_0);
-FOUNDATION_EXPORT NSString * const NSStringTransformLatinToGreek            NS_AVAILABLE(10_11, 9_0);
-FOUNDATION_EXPORT NSString * const NSStringTransformToLatin                 NS_AVAILABLE(10_11, 9_0);
-FOUNDATION_EXPORT NSString * const NSStringTransformMandarinToLatin         NS_AVAILABLE(10_11, 9_0);
-FOUNDATION_EXPORT NSString * const NSStringTransformHiraganaToKatakana      NS_AVAILABLE(10_11, 9_0);
-FOUNDATION_EXPORT NSString * const NSStringTransformFullwidthToHalfwidth    NS_AVAILABLE(10_11, 9_0);
-FOUNDATION_EXPORT NSString * const NSStringTransformToXMLHex                NS_AVAILABLE(10_11, 9_0);
-FOUNDATION_EXPORT NSString * const NSStringTransformToUnicodeName           NS_AVAILABLE(10_11, 9_0);
-FOUNDATION_EXPORT NSString * const NSStringTransformStripCombiningMarks     NS_AVAILABLE(10_11, 9_0);
-FOUNDATION_EXPORT NSString * const NSStringTransformStripDiacritics         NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXPORT NSStringTransform const NSStringTransformLatinToKatakana         NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXPORT NSStringTransform const NSStringTransformLatinToHiragana         NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXPORT NSStringTransform const NSStringTransformLatinToHangul           NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXPORT NSStringTransform const NSStringTransformLatinToArabic           NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXPORT NSStringTransform const NSStringTransformLatinToHebrew           NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXPORT NSStringTransform const NSStringTransformLatinToThai             NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXPORT NSStringTransform const NSStringTransformLatinToCyrillic         NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXPORT NSStringTransform const NSStringTransformLatinToGreek            NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXPORT NSStringTransform const NSStringTransformToLatin                 NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXPORT NSStringTransform const NSStringTransformMandarinToLatin         NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXPORT NSStringTransform const NSStringTransformHiraganaToKatakana      NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXPORT NSStringTransform const NSStringTransformFullwidthToHalfwidth    NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXPORT NSStringTransform const NSStringTransformToXMLHex                NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXPORT NSStringTransform const NSStringTransformToUnicodeName           NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXPORT NSStringTransform const NSStringTransformStripCombiningMarks     NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXPORT NSStringTransform const NSStringTransformStripDiacritics         NS_AVAILABLE(10_11, 9_0);
 
 
 /* Write to specified url or path using the specified encoding.  The optional error return is to indicate file system or encoding errors.
@@ -365,6 +367,7 @@
 
 @end
 
+typedef NSString * NSStringEncodingDetectionOptionsKey NS_STRING_ENUM;
 
 @interface NSString (NSStringEncodingDetection)
 
@@ -385,19 +388,19 @@
 If the values in the dictionary are unknown (for example, the value in the array of suggested string encodings is not a valid encoding), the values will be ignored.
 */
 + (NSStringEncoding)stringEncodingForData:(NSData *)data
-                          encodingOptions:(nullable NSDictionary<NSString *, id> *)opts
-                          convertedString:(NSString * __nullable * __nullable)string
+                          encodingOptions:(nullable NSDictionary<NSStringEncodingDetectionOptionsKey, id> *)opts
+                          convertedString:(NSString * _Nullable * _Nullable)string
                       usedLossyConversion:(nullable BOOL *)usedLossyConversion NS_AVAILABLE(10_10, 8_0);
 
 /* The following keys are for the option dictionary for the string encoding detection API.
 */
-FOUNDATION_EXPORT NSString * const NSStringEncodingDetectionSuggestedEncodingsKey           NS_AVAILABLE(10_10, 8_0);   // NSArray of NSNumbers which contain NSStringEncoding values; if this key is not present in the dictionary, all encodings are weighted the same
-FOUNDATION_EXPORT NSString * const NSStringEncodingDetectionDisallowedEncodingsKey          NS_AVAILABLE(10_10, 8_0);   // NSArray of NSNumbers which contain NSStringEncoding values; if this key is not present in the dictionary, all encodings are considered
-FOUNDATION_EXPORT NSString * const NSStringEncodingDetectionUseOnlySuggestedEncodingsKey    NS_AVAILABLE(10_10, 8_0);   // NSNumber boolean value; if this key is not present in the dictionary, the default value is NO
-FOUNDATION_EXPORT NSString * const NSStringEncodingDetectionAllowLossyKey                   NS_AVAILABLE(10_10, 8_0);   // NSNumber boolean value; if this key is not present in the dictionary, the default value is YES
-FOUNDATION_EXPORT NSString * const NSStringEncodingDetectionFromWindowsKey                  NS_AVAILABLE(10_10, 8_0);   // NSNumber boolean value; if this key is not present in the dictionary, the default value is NO
-FOUNDATION_EXPORT NSString * const NSStringEncodingDetectionLossySubstitutionKey            NS_AVAILABLE(10_10, 8_0);   // NSString value; if this key is not present in the dictionary, the default value is U+FFFD
-FOUNDATION_EXPORT NSString * const NSStringEncodingDetectionLikelyLanguageKey               NS_AVAILABLE(10_10, 8_0);   // NSString value; ISO language code; if this key is not present in the dictionary, no such information is considered
+FOUNDATION_EXPORT NSStringEncodingDetectionOptionsKey const NSStringEncodingDetectionSuggestedEncodingsKey           NS_AVAILABLE(10_10, 8_0);   // NSArray of NSNumbers which contain NSStringEncoding values; if this key is not present in the dictionary, all encodings are weighted the same
+FOUNDATION_EXPORT NSStringEncodingDetectionOptionsKey const NSStringEncodingDetectionDisallowedEncodingsKey          NS_AVAILABLE(10_10, 8_0);   // NSArray of NSNumbers which contain NSStringEncoding values; if this key is not present in the dictionary, all encodings are considered
+FOUNDATION_EXPORT NSStringEncodingDetectionOptionsKey const NSStringEncodingDetectionUseOnlySuggestedEncodingsKey    NS_AVAILABLE(10_10, 8_0);   // NSNumber boolean value; if this key is not present in the dictionary, the default value is NO
+FOUNDATION_EXPORT NSStringEncodingDetectionOptionsKey const NSStringEncodingDetectionAllowLossyKey                   NS_AVAILABLE(10_10, 8_0);   // NSNumber boolean value; if this key is not present in the dictionary, the default value is YES
+FOUNDATION_EXPORT NSStringEncodingDetectionOptionsKey const NSStringEncodingDetectionFromWindowsKey                  NS_AVAILABLE(10_10, 8_0);   // NSNumber boolean value; if this key is not present in the dictionary, the default value is NO
+FOUNDATION_EXPORT NSStringEncodingDetectionOptionsKey const NSStringEncodingDetectionLossySubstitutionKey            NS_AVAILABLE(10_10, 8_0);   // NSString value; if this key is not present in the dictionary, the default value is U+FFFD
+FOUNDATION_EXPORT NSStringEncodingDetectionOptionsKey const NSStringEncodingDetectionLikelyLanguageKey               NS_AVAILABLE(10_10, 8_0);   // NSString value; ISO language code; if this key is not present in the dictionary, no such information is considered
 
 @end
 
@@ -440,8 +443,8 @@
 
 
 
-FOUNDATION_EXPORT NSString * const NSCharacterConversionException;
-FOUNDATION_EXPORT NSString * const NSParseErrorException; // raised by -propertyList
+FOUNDATION_EXPORT NSExceptionName const NSCharacterConversionException;
+FOUNDATION_EXPORT NSExceptionName const NSParseErrorException; // raised by -propertyList
 #define NSMaximumStringLength	(INT_MAX-1)
 
 #pragma mark *** Deprecated/discouraged APIs ***
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSThread.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSThread.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSThread.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSThread.h	2016-05-20 06:24:14.000000000 +0200
@@ -4,6 +4,7 @@
 
 #import <Foundation/NSObject.h>
 #import <Foundation/NSDate.h>
+#import <Foundation/NSNotification.h>
 
 @class NSArray<ObjectType>, NSMutableDictionary, NSDate, NSNumber, NSString;
 
@@ -61,9 +62,9 @@
 
 @end
 
-FOUNDATION_EXPORT NSString * const NSWillBecomeMultiThreadedNotification;
-FOUNDATION_EXPORT NSString * const NSDidBecomeSingleThreadedNotification;
-FOUNDATION_EXPORT NSString * const NSThreadWillExitNotification;
+FOUNDATION_EXPORT NSNotificationName const NSWillBecomeMultiThreadedNotification;
+FOUNDATION_EXPORT NSNotificationName const NSDidBecomeSingleThreadedNotification;
+FOUNDATION_EXPORT NSNotificationName const NSThreadWillExitNotification;
 
 @interface NSObject (NSThreadPerformAdditions)
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTimeZone.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTimeZone.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTimeZone.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSTimeZone.h	2016-05-20 06:24:14.000000000 +0200
@@ -4,6 +4,7 @@
 
 #import <Foundation/NSObject.h>
 #import <Foundation/NSDate.h>
+#import <Foundation/NSNotification.h>
 
 @class NSString, NSArray<ObjectType>, NSDictionary<KeyType, ObjectType>, NSDate, NSData, NSLocale;
 
@@ -82,6 +83,6 @@
 
 @end
 
-FOUNDATION_EXPORT NSString * const NSSystemTimeZoneDidChangeNotification NS_AVAILABLE(10_5, 2_0);
+FOUNDATION_EXPORT NSNotificationName const NSSystemTimeZoneDidChangeNotification NS_AVAILABLE(10_5, 2_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURL.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURL.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURL.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURL.h	2016-05-20 06:24:14.000000000 +0200
@@ -11,6 +11,8 @@
 
 @class NSArray<ObjectType>, NSNumber, NSData, NSDictionary<KeyType, ObjectType>;
 
+typedef NSString * NSURLResourceKey NS_EXTENSIBLE_STRING_ENUM;
+
 NS_ASSUME_NONNULL_BEGIN
 
 #if (TARGET_OS_EMBEDDED || TARGET_OS_IPHONE)
@@ -22,15 +24,9 @@
     NSString *_urlString;
     NSURL *_baseURL;
     void *_clients;
-    __strong void *_reserved;
+    void *_reserved;
 }
 
-
-/* As more schemes are used and understood, strong constants for them will be added here
- */
-FOUNDATION_EXPORT NSString *NSURLFileScheme;
-
-
 /* Convenience initializers
  */
 - (nullable instancetype)initWithScheme:(NSString *)scheme host:(nullable NSString *)host path:(NSString *)path NS_DEPRECATED(10_0, 10_11, 2_0, 9_0, "Use NSURLComponents instead, which lets you create a valid URL with any valid combination of URL components and subcomponents (not just scheme, host and path), and lets you set components and subcomponents with either percent-encoded or un-percent-encoded strings."); // this call percent-encodes both the host and path, so this cannot be used to set a username/password or port in the hostname part or with a IPv6 '[...]' type address. NSURLComponents handles IPv6 addresses correctly.
@@ -89,6 +85,17 @@
  */
 @property (readonly, copy) NSData *dataRepresentation NS_AVAILABLE(10_11, 9_0);
 
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 6)
+@property (nullable, readonly, copy) NSString *absoluteString;
+@property (readonly, copy) NSString *relativeString; // The relative portion of a URL.  If baseURL is nil, or if the receiver is itself absolute, this is the same as absoluteString
+@property (nullable, readonly, copy) NSURL *baseURL; // may be nil.
+@property (nullable, readonly, copy) NSURL *absoluteURL; // if the receiver is itself absolute, this will return self.
+
+/* Any URL is composed of these two basic pieces.  The full URL would be the concatenation of [myURL scheme], ':', [myURL resourceSpecifier]
+ */
+@property (nullable, readonly, copy) NSString *scheme;
+@property (nullable, readonly, copy) NSString *resourceSpecifier;
+#else
 @property (readonly, copy) NSString *absoluteString;
 @property (nullable, readonly, copy) NSString *relativeString; // The relative portion of a URL.  If baseURL is nil, or if the receiver is itself absolute, this is the same as absoluteString
 @property (nullable, readonly, copy) NSURL *baseURL; // may be nil.
@@ -98,6 +105,7 @@
  */
 @property (readonly, copy) NSString *scheme;
 @property (readonly, copy) NSString *resourceSpecifier;
+#endif // SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 6
 
 /* If the URL conforms to rfc 1808 (the most common form of URL), the following accessors will return the various components; otherwise they return nil.  The litmus test for conformance is as recommended in RFC 1808 - whether the first two characters of resourceSpecifier is @"//".  In all cases, they return the component's value after resolving the receiver against its base URL.
  */
@@ -121,10 +129,14 @@
 
 /* Returns the URL's path in file system representation. File system representation is a null-terminated C string with canonical UTF-8 encoding. The returned C string will be automatically freed just as a returned object would be released; your code should copy the representation or use getFileSystemRepresentation:maxLength: if it needs to store the representation outside of the autorelease context in which the representation is created.
  */
-@property (readonly) __strong const char *fileSystemRepresentation NS_RETURNS_INNER_POINTER NS_AVAILABLE(10_9, 7_0);
+@property (readonly) const char *fileSystemRepresentation NS_RETURNS_INNER_POINTER NS_AVAILABLE(10_9, 7_0);
 
 @property (readonly, getter=isFileURL) BOOL fileURL; // Whether the scheme is file:; if [myURL isFileURL] is YES, then [myURL path] is suitable for input into NSFileManager or NSPathUtilities.
 
+/* A string constant for the "file" URL scheme. If you are using this to compare to a URL's scheme to see if it is a file URL, you should instead use the NSURL fileURL property -- the fileURL property is much faster. */
+FOUNDATION_EXPORT NSString *NSURLFileScheme;
+
+
 @property (nullable, readonly, copy) NSURL *standardizedURL;
 
 
@@ -160,25 +172,25 @@
 
 /* Returns the resource value identified by a given resource key. This method first checks if the URL object already caches the resource value. If so, it returns the cached resource value to the caller. If not, then this method synchronously obtains the resource value from the backing store, adds the resource value to the URL object's cache, and returns the resource value to the caller. The type of the resource value varies by resource property (see resource key definitions). If this method returns YES and value is populated with nil, it means the resource property is not available for the specified resource and no errors occurred when determining the resource property was not available. If this method returns NO, the optional error is populated. This method is currently applicable only to URLs for file system resources. Symbol is present in iOS 4, but performs no operation.
  */
-- (BOOL)getResourceValue:(out id __nullable * __nonnull)value forKey:(NSString *)key error:(out NSError ** __nullable)error NS_AVAILABLE(10_6, 4_0);
+- (BOOL)getResourceValue:(out id _Nullable * _Nonnull)value forKey:(NSURLResourceKey)key error:(out NSError ** _Nullable)error NS_AVAILABLE(10_6, 4_0);
 
 /* Returns the resource values identified by specified array of resource keys. This method first checks if the URL object already caches the resource values. If so, it returns the cached resource values to the caller. If not, then this method synchronously obtains the resource values from the backing store, adds the resource values to the URL object's cache, and returns the resource values to the caller. The type of the resource values vary by property (see resource key definitions). If the result dictionary does not contain a resource value for one or more of the requested resource keys, it means those resource properties are not available for the specified resource and no errors occurred when determining those resource properties were not available. If this method returns NULL, the optional error is populated. This method is currently applicable only to URLs for file system resources. Symbol is present in iOS 4, but performs no operation.
  */
-- (nullable NSDictionary<NSString *, id> *)resourceValuesForKeys:(NSArray<NSString *> *)keys error:(NSError **)error NS_AVAILABLE(10_6, 4_0);
+- (nullable NSDictionary<NSURLResourceKey, id> *)resourceValuesForKeys:(NSArray<NSURLResourceKey> *)keys error:(NSError **)error NS_AVAILABLE(10_6, 4_0);
 
 /* Sets the resource value identified by a given resource key. This method writes the new resource value out to the backing store. Attempts to set a read-only resource property or to set a resource property not supported by the resource are ignored and are not considered errors. If this method returns NO, the optional error is populated. This method is currently applicable only to URLs for file system resources. Symbol is present in iOS 4, but performs no operation.
  */
-- (BOOL)setResourceValue:(nullable id)value forKey:(NSString *)key error:(NSError **)error NS_AVAILABLE(10_6, 4_0);
+- (BOOL)setResourceValue:(nullable id)value forKey:(NSURLResourceKey)key error:(NSError **)error NS_AVAILABLE(10_6, 4_0);
 
 /* Sets any number of resource values of a URL's resource. This method writes the new resource values out to the backing store. Attempts to set read-only resource properties or to set resource properties not supported by the resource are ignored and are not considered errors. If an error occurs after some resource properties have been successfully changed, the userInfo dictionary in the returned error contains an array of resource keys that were not set with the key kCFURLKeysOfUnsetValuesKey. The order in which the resource values are set is not defined. If you need to guarantee the order resource values are set, you should make multiple requests to this method or to -setResourceValue:forKey:error: to guarantee the order. If this method returns NO, the optional error is populated. This method is currently applicable only to URLs for file system resources. Symbol is present in iOS 4, but performs no operation.
  */
-- (BOOL)setResourceValues:(NSDictionary<NSString *, id> *)keyedValues error:(NSError **)error NS_AVAILABLE(10_6, 4_0);
+- (BOOL)setResourceValues:(NSDictionary<NSURLResourceKey, id> *)keyedValues error:(NSError **)error NS_AVAILABLE(10_6, 4_0);
 
-FOUNDATION_EXPORT NSString * const NSURLKeysOfUnsetValuesKey NS_AVAILABLE(10_7, 5_0); // Key for the resource properties that have not been set after setResourceValues:error: returns an error, returned as an array of of strings.
+FOUNDATION_EXPORT NSURLResourceKey const NSURLKeysOfUnsetValuesKey NS_AVAILABLE(10_7, 5_0); // Key for the resource properties that have not been set after setResourceValues:error: returns an error, returned as an array of of strings.
 
 /* Removes the cached resource value identified by a given resource value key from the URL object. Removing a cached resource value may remove other cached resource values because some resource values are cached as a set of values, and because some resource values depend on other resource values (temporary resource values have no dependencies). This method is currently applicable only to URLs for file system resources.
  */
-- (void)removeCachedResourceValueForKey:(NSString *)key NS_AVAILABLE(10_9, 7_0);
+- (void)removeCachedResourceValueForKey:(NSURLResourceKey)key NS_AVAILABLE(10_9, 7_0);
 
 /* Removes all cached resource values and all temporary resource values from the URL object. This method is currently applicable only to URLs for file system resources.
  */
@@ -186,7 +198,7 @@
 
 /* Sets a temporary resource value on the URL object. Temporary resource values are for client use. Temporary resource values exist only in memory and are never written to the resource's backing store. Once set, a temporary resource value can be copied from the URL object with -getResourceValue:forKey:error: or -resourceValuesForKeys:error:. To remove a temporary resource value from the URL object, use -removeCachedResourceValueForKey:. Care should be taken to ensure the key that identifies a temporary resource value is unique and does not conflict with system defined keys (using reverse domain name notation in your temporary resource value keys is recommended). This method is currently applicable only to URLs for file system resources.
  */
-- (void)setTemporaryResourceValue:(nullable id)value forKey:(NSString *)key NS_AVAILABLE(10_9, 7_0);
+- (void)setTemporaryResourceValue:(nullable id)value forKey:(NSURLResourceKey)key NS_AVAILABLE(10_9, 7_0);
 
 /*
  The File System Resource Keys
@@ -196,142 +208,153 @@
 
 /* Resource keys applicable to all file system objects
  */
-FOUNDATION_EXPORT NSString * const NSURLNameKey                        NS_AVAILABLE(10_6, 4_0); // The resource name provided by the file system (Read-write, value type NSString)
-FOUNDATION_EXPORT NSString * const NSURLLocalizedNameKey               NS_AVAILABLE(10_6, 4_0); // Localized or extension-hidden name as displayed to users (Read-only, value type NSString)
-FOUNDATION_EXPORT NSString * const NSURLIsRegularFileKey               NS_AVAILABLE(10_6, 4_0); // True for regular files (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLIsDirectoryKey                 NS_AVAILABLE(10_6, 4_0); // True for directories (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLIsSymbolicLinkKey              NS_AVAILABLE(10_6, 4_0); // True for symlinks (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLIsVolumeKey                    NS_AVAILABLE(10_6, 4_0); // True for the root directory of a volume (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLIsPackageKey                   NS_AVAILABLE(10_6, 4_0); // True for packaged directories (Read-only 10_6 and 10_7, read-write 10_8, value type boolean NSNumber). Note: You can only set or clear this property on directories; if you try to set this property on non-directory objects, the property is ignored. If the directory is a package for some other reason (extension type, etc), setting this property to false will have no effect.
-FOUNDATION_EXPORT NSString * const NSURLIsApplicationKey               NS_AVAILABLE(10_11, 9_0); // True if resource is an application (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLApplicationIsScriptableKey     NS_AVAILABLE(10_11, NA); // True if the resource is scriptable. Only applies to applications (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLIsSystemImmutableKey           NS_AVAILABLE(10_6, 4_0); // True for system-immutable resources (Read-write, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLIsUserImmutableKey             NS_AVAILABLE(10_6, 4_0); // True for user-immutable resources (Read-write, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLIsHiddenKey                    NS_AVAILABLE(10_6, 4_0); // True for resources normally not displayed to users (Read-write, value type boolean NSNumber). Note: If the resource is a hidden because its name starts with a period, setting this property to false will not change the property.
-FOUNDATION_EXPORT NSString * const NSURLHasHiddenExtensionKey          NS_AVAILABLE(10_6, 4_0); // True for resources whose filename extension is removed from the localized name property (Read-write, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLCreationDateKey                NS_AVAILABLE(10_6, 4_0); // The date the resource was created (Read-write, value type NSDate)
-FOUNDATION_EXPORT NSString * const NSURLContentAccessDateKey           NS_AVAILABLE(10_6, 4_0); // The date the resource was last accessed (Read-only, value type NSDate)
-FOUNDATION_EXPORT NSString * const NSURLContentModificationDateKey     NS_AVAILABLE(10_6, 4_0); // The time the resource content was last modified (Read-write, value type NSDate)
-FOUNDATION_EXPORT NSString * const NSURLAttributeModificationDateKey   NS_AVAILABLE(10_6, 4_0); // The time the resource's attributes were last modified (Read-write, value type NSDate)
-FOUNDATION_EXPORT NSString * const NSURLLinkCountKey                   NS_AVAILABLE(10_6, 4_0); // Number of hard links to the resource (Read-only, value type NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLParentDirectoryURLKey          NS_AVAILABLE(10_6, 4_0); // The resource's parent directory, if any (Read-only, value type NSURL)
-FOUNDATION_EXPORT NSString * const NSURLVolumeURLKey                   NS_AVAILABLE(10_6, 4_0); // URL of the volume on which the resource is stored (Read-only, value type NSURL)
-FOUNDATION_EXPORT NSString * const NSURLTypeIdentifierKey              NS_AVAILABLE(10_6, 4_0); // Uniform type identifier (UTI) for the resource (Read-only, value type NSString)
-FOUNDATION_EXPORT NSString * const NSURLLocalizedTypeDescriptionKey    NS_AVAILABLE(10_6, 4_0); // User-visible type or "kind" description (Read-only, value type NSString)
-FOUNDATION_EXPORT NSString * const NSURLLabelNumberKey                 NS_AVAILABLE(10_6, 4_0); // The label number assigned to the resource (Read-write, value type NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLLabelColorKey                  NS_AVAILABLE(10_6, 4_0); // The color of the assigned label (Read-only, value type NSColor)
-FOUNDATION_EXPORT NSString * const NSURLLocalizedLabelKey              NS_AVAILABLE(10_6, 4_0); // The user-visible label text (Read-only, value type NSString)
-FOUNDATION_EXPORT NSString * const NSURLEffectiveIconKey               NS_AVAILABLE(10_6, 4_0); // The icon normally displayed for the resource (Read-only, value type NSImage)
-FOUNDATION_EXPORT NSString * const NSURLCustomIconKey                  NS_AVAILABLE(10_6, 4_0); // The custom icon assigned to the resource, if any (Currently not implemented, value type NSImage)
-FOUNDATION_EXPORT NSString * const NSURLFileResourceIdentifierKey      NS_AVAILABLE(10_7, 5_0); // An identifier which can be used to compare two file system objects for equality using -isEqual (i.e, two object identifiers are equal if they have the same file system path or if the paths are linked to same inode on the same file system). This identifier is not persistent across system restarts. (Read-only, value type id <NSCopying, NSCoding, NSObject>)
-FOUNDATION_EXPORT NSString * const NSURLVolumeIdentifierKey            NS_AVAILABLE(10_7, 5_0); // An identifier that can be used to identify the volume the file system object is on. Other objects on the same volume will have the same volume identifier and can be compared using for equality using -isEqual. This identifier is not persistent across system restarts. (Read-only, value type id <NSCopying, NSCoding, NSObject>)
-FOUNDATION_EXPORT NSString * const NSURLPreferredIOBlockSizeKey        NS_AVAILABLE(10_7, 5_0); // The optimal block size when reading or writing this file's data, or nil if not available. (Read-only, value type NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLIsReadableKey                  NS_AVAILABLE(10_7, 5_0); // true if this process (as determined by EUID) can read the resource. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLIsWritableKey                  NS_AVAILABLE(10_7, 5_0); // true if this process (as determined by EUID) can write to the resource. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLIsExecutableKey                NS_AVAILABLE(10_7, 5_0); // true if this process (as determined by EUID) can execute a file resource or search a directory resource. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLFileSecurityKey                NS_AVAILABLE(10_7, 5_0); // The file system object's security information encapsulated in a NSFileSecurity object. (Read-write, Value type NSFileSecurity)
-FOUNDATION_EXPORT NSString * const NSURLIsExcludedFromBackupKey        NS_AVAILABLE(10_8, 5_1); // true if resource should be excluded from backups, false otherwise (Read-write, value type boolean NSNumber). This property is only useful for excluding cache and other application support files which are not needed in a backup. Some operations commonly made to user documents will cause this property to be reset to false and so this property should not be used on user documents.
-FOUNDATION_EXPORT NSString * const NSURLTagNamesKey                    NS_AVAILABLE(10_9, NA);	// The array of Tag names (Read-write, value type NSArray of NSString)
-FOUNDATION_EXPORT NSString * const NSURLPathKey                        NS_AVAILABLE(10_8, 6_0); // the URL's path as a file system path (Read-only, value type NSString)
-FOUNDATION_EXPORT NSString * const NSURLIsMountTriggerKey              NS_AVAILABLE(10_7, 5_0); // true if this URL is a file system trigger directory. Traversing or opening a file system trigger will cause an attempt to mount a file system on the trigger directory. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLGenerationIdentifierKey NS_AVAILABLE(10_10, 8_0); // An opaque generation identifier which can be compared using isEqual: to determine if the data in a document has been modified. For URLs which refer to the same file inode, the generation identifier will change when the data in the file's data fork is changed (changes to extended attributes or other file system metadata do not change the generation identifier). For URLs which refer to the same directory inode, the generation identifier will change when direct children of that directory are added, removed or renamed (changes to the data of the direct children of that directory will not change the generation identifier). The generation identifier is persistent across system restarts. The generation identifier is tied to a specific document on a specific volume and is not transferred when the document is copied to another volume. This property is not supported by all volumes. (Read-only, value type id <NSCopying, NSCoding, NSObject>
-FOUNDATION_EXPORT NSString * const NSURLDocumentIdentifierKey NS_AVAILABLE(10_10, 8_0); // The document identifier -- a value assigned by the kernel to a document (which can be either a file or directory) and is used to identify the document regardless of where it gets moved on a volume. The document identifier survives "safe save” operations; i.e it is sticky to the path it was assigned to (-replaceItemAtURL:withItemAtURL:backupItemName:options:resultingItemURL:error: is the preferred safe-save API). The document identifier is persistent across system restarts. The document identifier is not transferred when the file is copied. Document identifiers are only unique within a single volume. This property is not supported by all volumes. (Read-only, value type NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLAddedToDirectoryDateKey NS_AVAILABLE(10_10, 8_0); // The date the resource was created, or renamed into or within its parent directory. Note that inconsistent behavior may be observed when this attribute is requested on hard-linked items. This property is not supported by all volumes. (Read-only, value type NSDate)
-FOUNDATION_EXPORT NSString * const NSURLQuarantinePropertiesKey NS_AVAILABLE(10_10, NA); // The quarantine properties as defined in LSQuarantine.h. To remove quarantine information from a file, pass NSNull as the value when setting this property. (Read-write, value type NSDictionary)
-FOUNDATION_EXPORT NSString * const NSURLFileResourceTypeKey            NS_AVAILABLE(10_7, 5_0); // Returns the file system object type. (Read-only, value type NSString)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLNameKey                        NS_AVAILABLE(10_6, 4_0); // The resource name provided by the file system (Read-write, value type NSString)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLLocalizedNameKey               NS_AVAILABLE(10_6, 4_0); // Localized or extension-hidden name as displayed to users (Read-only, value type NSString)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLIsRegularFileKey               NS_AVAILABLE(10_6, 4_0); // True for regular files (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLIsDirectoryKey                 NS_AVAILABLE(10_6, 4_0); // True for directories (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLIsSymbolicLinkKey              NS_AVAILABLE(10_6, 4_0); // True for symlinks (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLIsVolumeKey                    NS_AVAILABLE(10_6, 4_0); // True for the root directory of a volume (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLIsPackageKey                   NS_AVAILABLE(10_6, 4_0); // True for packaged directories (Read-only 10_6 and 10_7, read-write 10_8, value type boolean NSNumber). Note: You can only set or clear this property on directories; if you try to set this property on non-directory objects, the property is ignored. If the directory is a package for some other reason (extension type, etc), setting this property to false will have no effect.
+FOUNDATION_EXPORT NSURLResourceKey const NSURLIsApplicationKey               NS_AVAILABLE(10_11, 9_0); // True if resource is an application (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLApplicationIsScriptableKey     NS_AVAILABLE(10_11, NA); // True if the resource is scriptable. Only applies to applications (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLIsSystemImmutableKey           NS_AVAILABLE(10_6, 4_0); // True for system-immutable resources (Read-write, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLIsUserImmutableKey             NS_AVAILABLE(10_6, 4_0); // True for user-immutable resources (Read-write, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLIsHiddenKey                    NS_AVAILABLE(10_6, 4_0); // True for resources normally not displayed to users (Read-write, value type boolean NSNumber). Note: If the resource is a hidden because its name starts with a period, setting this property to false will not change the property.
+FOUNDATION_EXPORT NSURLResourceKey const NSURLHasHiddenExtensionKey          NS_AVAILABLE(10_6, 4_0); // True for resources whose filename extension is removed from the localized name property (Read-write, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLCreationDateKey                NS_AVAILABLE(10_6, 4_0); // The date the resource was created (Read-write, value type NSDate)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLContentAccessDateKey           NS_AVAILABLE(10_6, 4_0); // The date the resource was last accessed (Read-only, value type NSDate)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLContentModificationDateKey     NS_AVAILABLE(10_6, 4_0); // The time the resource content was last modified (Read-write, value type NSDate)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLAttributeModificationDateKey   NS_AVAILABLE(10_6, 4_0); // The time the resource's attributes were last modified (Read-only, value type NSDate)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLLinkCountKey                   NS_AVAILABLE(10_6, 4_0); // Number of hard links to the resource (Read-only, value type NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLParentDirectoryURLKey          NS_AVAILABLE(10_6, 4_0); // The resource's parent directory, if any (Read-only, value type NSURL)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeURLKey                   NS_AVAILABLE(10_6, 4_0); // URL of the volume on which the resource is stored (Read-only, value type NSURL)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLTypeIdentifierKey              NS_AVAILABLE(10_6, 4_0); // Uniform type identifier (UTI) for the resource (Read-only, value type NSString)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLLocalizedTypeDescriptionKey    NS_AVAILABLE(10_6, 4_0); // User-visible type or "kind" description (Read-only, value type NSString)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLLabelNumberKey                 NS_AVAILABLE(10_6, 4_0); // The label number assigned to the resource (Read-write, value type NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLLabelColorKey                  NS_AVAILABLE(10_6, 4_0); // The color of the assigned label (Read-only, value type NSColor)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLLocalizedLabelKey              NS_AVAILABLE(10_6, 4_0); // The user-visible label text (Read-only, value type NSString)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLEffectiveIconKey               NS_AVAILABLE(10_6, 4_0); // The icon normally displayed for the resource (Read-only, value type NSImage)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLCustomIconKey                  NS_AVAILABLE(10_6, 4_0); // The custom icon assigned to the resource, if any (Currently not implemented, value type NSImage)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLFileResourceIdentifierKey      NS_AVAILABLE(10_7, 5_0); // An identifier which can be used to compare two file system objects for equality using -isEqual (i.e, two object identifiers are equal if they have the same file system path or if the paths are linked to same inode on the same file system). This identifier is not persistent across system restarts. (Read-only, value type id <NSCopying, NSCoding, NSSecureCoding, NSObject>)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeIdentifierKey            NS_AVAILABLE(10_7, 5_0); // An identifier that can be used to identify the volume the file system object is on. Other objects on the same volume will have the same volume identifier and can be compared using for equality using -isEqual. This identifier is not persistent across system restarts. (Read-only, value type id <NSCopying, NSCoding, NSSecureCoding, NSObject>)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLPreferredIOBlockSizeKey        NS_AVAILABLE(10_7, 5_0); // The optimal block size when reading or writing this file's data, or nil if not available. (Read-only, value type NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLIsReadableKey                  NS_AVAILABLE(10_7, 5_0); // true if this process (as determined by EUID) can read the resource. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLIsWritableKey                  NS_AVAILABLE(10_7, 5_0); // true if this process (as determined by EUID) can write to the resource. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLIsExecutableKey                NS_AVAILABLE(10_7, 5_0); // true if this process (as determined by EUID) can execute a file resource or search a directory resource. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLFileSecurityKey                NS_AVAILABLE(10_7, 5_0); // The file system object's security information encapsulated in a NSFileSecurity object. (Read-write, Value type NSFileSecurity)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLIsExcludedFromBackupKey        NS_AVAILABLE(10_8, 5_1); // true if resource should be excluded from backups, false otherwise (Read-write, value type boolean NSNumber). This property is only useful for excluding cache and other application support files which are not needed in a backup. Some operations commonly made to user documents will cause this property to be reset to false and so this property should not be used on user documents.
+FOUNDATION_EXPORT NSURLResourceKey const NSURLTagNamesKey                    NS_AVAILABLE(10_9, NA);	// The array of Tag names (Read-write, value type NSArray of NSString)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLPathKey                        NS_AVAILABLE(10_8, 6_0); // the URL's path as a file system path (Read-only, value type NSString)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLCanonicalPathKey               API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)); // the URL's path as a canonical absolute file system path (Read-only, value type NSString)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLIsMountTriggerKey              NS_AVAILABLE(10_7, 5_0); // true if this URL is a file system trigger directory. Traversing or opening a file system trigger will cause an attempt to mount a file system on the trigger directory. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLGenerationIdentifierKey NS_AVAILABLE(10_10, 8_0); // An opaque generation identifier which can be compared using isEqual: to determine if the data in a document has been modified. For URLs which refer to the same file inode, the generation identifier will change when the data in the file's data fork is changed (changes to extended attributes or other file system metadata do not change the generation identifier). For URLs which refer to the same directory inode, the generation identifier will change when direct children of that directory are added, removed or renamed (changes to the data of the direct children of that directory will not change the generation identifier). The generation identifier is persistent across system restarts. The generation identifier is tied to a specific document on a specific volume and is not transferred when the document is copied to another volume. This property is not supported by all volumes. (Read-only, value type id <NSCopying, NSCoding, NSSecureCoding, NSObject>)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLDocumentIdentifierKey NS_AVAILABLE(10_10, 8_0); // The document identifier -- a value assigned by the kernel to a document (which can be either a file or directory) and is used to identify the document regardless of where it gets moved on a volume. The document identifier survives "safe save” operations; i.e it is sticky to the path it was assigned to (-replaceItemAtURL:withItemAtURL:backupItemName:options:resultingItemURL:error: is the preferred safe-save API). The document identifier is persistent across system restarts. The document identifier is not transferred when the file is copied. Document identifiers are only unique within a single volume. This property is not supported by all volumes. (Read-only, value type NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLAddedToDirectoryDateKey NS_AVAILABLE(10_10, 8_0); // The date the resource was created, or renamed into or within its parent directory. Note that inconsistent behavior may be observed when this attribute is requested on hard-linked items. This property is not supported by all volumes. (Read-only, value type NSDate)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLQuarantinePropertiesKey NS_AVAILABLE(10_10, NA); // The quarantine properties as defined in LSQuarantine.h. To remove quarantine information from a file, pass NSNull as the value when setting this property. (Read-write, value type NSDictionary)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLFileResourceTypeKey            NS_AVAILABLE(10_7, 5_0); // Returns the file system object type. (Read-only, value type NSString)
+
+typedef NSString * NSURLFileResourceType NS_STRING_ENUM;
 
 /* The file system object type values returned for the NSURLFileResourceTypeKey
  */
-FOUNDATION_EXPORT NSString * const NSURLFileResourceTypeNamedPipe      NS_AVAILABLE(10_7, 5_0);
-FOUNDATION_EXPORT NSString * const NSURLFileResourceTypeCharacterSpecial NS_AVAILABLE(10_7, 5_0);
-FOUNDATION_EXPORT NSString * const NSURLFileResourceTypeDirectory      NS_AVAILABLE(10_7, 5_0);
-FOUNDATION_EXPORT NSString * const NSURLFileResourceTypeBlockSpecial   NS_AVAILABLE(10_7, 5_0);
-FOUNDATION_EXPORT NSString * const NSURLFileResourceTypeRegular        NS_AVAILABLE(10_7, 5_0);
-FOUNDATION_EXPORT NSString * const NSURLFileResourceTypeSymbolicLink   NS_AVAILABLE(10_7, 5_0);
-FOUNDATION_EXPORT NSString * const NSURLFileResourceTypeSocket         NS_AVAILABLE(10_7, 5_0);
-FOUNDATION_EXPORT NSString * const NSURLFileResourceTypeUnknown        NS_AVAILABLE(10_7, 5_0);
+FOUNDATION_EXPORT NSURLFileResourceType const NSURLFileResourceTypeNamedPipe      NS_AVAILABLE(10_7, 5_0);
+FOUNDATION_EXPORT NSURLFileResourceType const NSURLFileResourceTypeCharacterSpecial NS_AVAILABLE(10_7, 5_0);
+FOUNDATION_EXPORT NSURLFileResourceType const NSURLFileResourceTypeDirectory      NS_AVAILABLE(10_7, 5_0);
+FOUNDATION_EXPORT NSURLFileResourceType const NSURLFileResourceTypeBlockSpecial   NS_AVAILABLE(10_7, 5_0);
+FOUNDATION_EXPORT NSURLFileResourceType const NSURLFileResourceTypeRegular        NS_AVAILABLE(10_7, 5_0);
+FOUNDATION_EXPORT NSURLFileResourceType const NSURLFileResourceTypeSymbolicLink   NS_AVAILABLE(10_7, 5_0);
+FOUNDATION_EXPORT NSURLFileResourceType const NSURLFileResourceTypeSocket         NS_AVAILABLE(10_7, 5_0);
+FOUNDATION_EXPORT NSURLFileResourceType const NSURLFileResourceTypeUnknown        NS_AVAILABLE(10_7, 5_0);
 
-FOUNDATION_EXPORT NSString * const NSURLThumbnailDictionaryKey         NS_AVAILABLE(10_10, 8_0); // dictionary of NSImage/UIImage objects keyed by size
-FOUNDATION_EXPORT NSString * const NSURLThumbnailKey                   NS_AVAILABLE_MAC(10_10); // returns all thumbnails as a single NSImage
+FOUNDATION_EXPORT NSURLResourceKey const NSURLThumbnailDictionaryKey         NS_AVAILABLE(10_10, 8_0); // dictionary of NSImage/UIImage objects keyed by size
+FOUNDATION_EXPORT NSURLResourceKey const NSURLThumbnailKey                   NS_AVAILABLE_MAC(10_10); // returns all thumbnails as a single NSImage
 
+typedef NSString *NSURLThumbnailDictionaryItem NS_EXTENSIBLE_STRING_ENUM;
 /* size keys for the dictionary returned by NSURLThumbnailDictionaryKey
  */
-FOUNDATION_EXPORT NSString * const NSThumbnail1024x1024SizeKey         NS_AVAILABLE(10_10, 8_0); // size key for a 1024 x 1024 thumbnail image
+FOUNDATION_EXPORT NSURLThumbnailDictionaryItem const NSThumbnail1024x1024SizeKey         NS_AVAILABLE(10_10, 8_0); // size key for a 1024 x 1024 thumbnail image
 
 /* Resource keys applicable only to regular files
  */
-FOUNDATION_EXPORT NSString * const NSURLFileSizeKey                    NS_AVAILABLE(10_6, 4_0); // Total file size in bytes (Read-only, value type NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLFileAllocatedSizeKey           NS_AVAILABLE(10_6, 4_0); // Total size allocated on disk for the file in bytes (number of blocks times block size) (Read-only, value type NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLTotalFileSizeKey               NS_AVAILABLE(10_7, 5_0); // Total displayable size of the file in bytes (this may include space used by metadata), or nil if not available. (Read-only, value type NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLTotalFileAllocatedSizeKey      NS_AVAILABLE(10_7, 5_0); // Total allocated size of the file in bytes (this may include space used by metadata), or nil if not available. This can be less than the value returned by NSURLTotalFileSizeKey if the resource is compressed. (Read-only, value type NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLIsAliasFileKey                 NS_AVAILABLE(10_6, 4_0); // true if the resource is a Finder alias file or a symlink, false otherwise ( Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLFileProtectionKey              NS_AVAILABLE_IOS(9_0); // The protection level for this file
+FOUNDATION_EXPORT NSURLResourceKey const NSURLFileSizeKey                    NS_AVAILABLE(10_6, 4_0); // Total file size in bytes (Read-only, value type NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLFileAllocatedSizeKey           NS_AVAILABLE(10_6, 4_0); // Total size allocated on disk for the file in bytes (number of blocks times block size) (Read-only, value type NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLTotalFileSizeKey               NS_AVAILABLE(10_7, 5_0); // Total displayable size of the file in bytes (this may include space used by metadata), or nil if not available. (Read-only, value type NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLTotalFileAllocatedSizeKey      NS_AVAILABLE(10_7, 5_0); // Total allocated size of the file in bytes (this may include space used by metadata), or nil if not available. This can be less than the value returned by NSURLTotalFileSizeKey if the resource is compressed. (Read-only, value type NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLIsAliasFileKey                 NS_AVAILABLE(10_6, 4_0); // true if the resource is a Finder alias file or a symlink, false otherwise ( Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLFileProtectionKey              NS_AVAILABLE_IOS(9_0); // The protection level for this file
 
+typedef NSString * NSURLFileProtectionType NS_STRING_ENUM;
 /* The protection level values returned for the NSURLFileProtectionKey
  */
-FOUNDATION_EXPORT NSString * const NSURLFileProtectionNone NS_AVAILABLE_IOS(9_0); // The file has no special protections associated with it. It can be read from or written to at any time.
-FOUNDATION_EXPORT NSString * const NSURLFileProtectionComplete NS_AVAILABLE_IOS(9_0); // The file is stored in an encrypted format on disk and cannot be read from or written to while the device is locked or booting.
-FOUNDATION_EXPORT NSString * const NSURLFileProtectionCompleteUnlessOpen NS_AVAILABLE_IOS(9_0); // The file is stored in an encrypted format on disk. Files can be created while the device is locked, but once closed, cannot be opened again until the device is unlocked. If the file is opened when unlocked, you may continue to access the file normally, even if the user locks the device. There is a small performance penalty when the file is created and opened, though not when being written to or read from. This can be mitigated by changing the file protection to NSURLFileProtectionComplete when the device is unlocked.
-FOUNDATION_EXPORT NSString * const NSURLFileProtectionCompleteUntilFirstUserAuthentication NS_AVAILABLE_IOS(9_0); // The file is stored in an encrypted format on disk and cannot be accessed until after the device has booted. After the user unlocks the device for the first time, your app can access the file and continue to access it even if the user subsequently locks the device.
+FOUNDATION_EXPORT NSURLFileProtectionType const NSURLFileProtectionNone NS_AVAILABLE_IOS(9_0); // The file has no special protections associated with it. It can be read from or written to at any time.
+FOUNDATION_EXPORT NSURLFileProtectionType const NSURLFileProtectionComplete NS_AVAILABLE_IOS(9_0); // The file is stored in an encrypted format on disk and cannot be read from or written to while the device is locked or booting.
+FOUNDATION_EXPORT NSURLFileProtectionType const NSURLFileProtectionCompleteUnlessOpen NS_AVAILABLE_IOS(9_0); // The file is stored in an encrypted format on disk. Files can be created while the device is locked, but once closed, cannot be opened again until the device is unlocked. If the file is opened when unlocked, you may continue to access the file normally, even if the user locks the device. There is a small performance penalty when the file is created and opened, though not when being written to or read from. This can be mitigated by changing the file protection to NSURLFileProtectionComplete when the device is unlocked.
+FOUNDATION_EXPORT NSURLFileProtectionType const NSURLFileProtectionCompleteUntilFirstUserAuthentication NS_AVAILABLE_IOS(9_0); // The file is stored in an encrypted format on disk and cannot be accessed until after the device has booted. After the user unlocks the device for the first time, your app can access the file and continue to access it even if the user subsequently locks the device.
 
 /* Volumes resource keys 
  
  As a convenience, volume resource values can be requested from any file system URL. The value returned will reflect the property value for the volume on which the resource is located.
  */
-FOUNDATION_EXPORT NSString * const NSURLVolumeLocalizedFormatDescriptionKey NS_AVAILABLE(10_6, 4_0); // The user-visible volume format (Read-only, value type NSString)
-FOUNDATION_EXPORT NSString * const NSURLVolumeTotalCapacityKey              NS_AVAILABLE(10_6, 4_0); // Total volume capacity in bytes (Read-only, value type NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeAvailableCapacityKey          NS_AVAILABLE(10_6, 4_0); // Total free space in bytes (Read-only, value type NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeResourceCountKey              NS_AVAILABLE(10_6, 4_0); // Total number of resources on the volume (Read-only, value type NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeSupportsPersistentIDsKey      NS_AVAILABLE(10_6, 4_0); // true if the volume format supports persistent object identifiers and can look up file system objects by their IDs (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeSupportsSymbolicLinksKey      NS_AVAILABLE(10_6, 4_0); // true if the volume format supports symbolic links (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeSupportsHardLinksKey          NS_AVAILABLE(10_6, 4_0); // true if the volume format supports hard links (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeSupportsJournalingKey         NS_AVAILABLE(10_6, 4_0); // true if the volume format supports a journal used to speed recovery in case of unplanned restart (such as a power outage or crash). This does not necessarily mean the volume is actively using a journal. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeIsJournalingKey               NS_AVAILABLE(10_6, 4_0); // true if the volume is currently using a journal for speedy recovery after an unplanned restart. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeSupportsSparseFilesKey        NS_AVAILABLE(10_6, 4_0); // true if the volume format supports sparse files, that is, files which can have 'holes' that have never been written to, and thus do not consume space on disk. A sparse file may have an allocated size on disk that is less than its logical length (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeSupportsZeroRunsKey           NS_AVAILABLE(10_6, 4_0); // For security reasons, parts of a file (runs) that have never been written to must appear to contain zeroes. true if the volume keeps track of allocated but unwritten runs of a file so that it can substitute zeroes without actually writing zeroes to the media. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeSupportsCaseSensitiveNamesKey NS_AVAILABLE(10_6, 4_0); // true if the volume format treats upper and lower case characters in file and directory names as different. Otherwise an upper case character is equivalent to a lower case character, and you can't have two names that differ solely in the case of the characters. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeSupportsCasePreservedNamesKey NS_AVAILABLE(10_6, 4_0); // true if the volume format preserves the case of file and directory names.  Otherwise the volume may change the case of some characters (typically making them all upper or all lower case). (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeSupportsRootDirectoryDatesKey NS_AVAILABLE(10_7, 5_0); // true if the volume supports reliable storage of times for the root directory. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeSupportsVolumeSizesKey        NS_AVAILABLE(10_7, 5_0); // true if the volume supports returning volume size values (NSURLVolumeTotalCapacityKey and NSURLVolumeAvailableCapacityKey). (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeSupportsRenamingKey           NS_AVAILABLE(10_7, 5_0); // true if the volume can be renamed. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeSupportsAdvisoryFileLockingKey NS_AVAILABLE(10_7, 5_0); // true if the volume implements whole-file flock(2) style advisory locks, and the O_EXLOCK and O_SHLOCK flags of the open(2) call. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeSupportsExtendedSecurityKey   NS_AVAILABLE(10_7, 5_0); // true if the volume implements extended security (ACLs). (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeIsBrowsableKey                NS_AVAILABLE(10_7, 5_0); // true if the volume should be visible via the GUI (i.e., appear on the Desktop as a separate volume). (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeMaximumFileSizeKey            NS_AVAILABLE(10_7, 5_0); // The largest file size (in bytes) supported by this file system, or nil if this cannot be determined. (Read-only, value type NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeIsEjectableKey                NS_AVAILABLE(10_7, 5_0); // true if the volume's media is ejectable from the drive mechanism under software control. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeIsRemovableKey                NS_AVAILABLE(10_7, 5_0); // true if the volume's media is removable from the drive mechanism. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeIsInternalKey                 NS_AVAILABLE(10_7, 5_0); // true if the volume's device is connected to an internal bus, false if connected to an external bus, or nil if not available. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeIsAutomountedKey              NS_AVAILABLE(10_7, 5_0); // true if the volume is automounted. Note: do not mistake this with the functionality provided by kCFURLVolumeSupportsBrowsingKey. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeIsLocalKey                    NS_AVAILABLE(10_7, 5_0); // true if the volume is stored on a local device. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeIsReadOnlyKey                 NS_AVAILABLE(10_7, 5_0); // true if the volume is read-only. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLVolumeCreationDateKey               NS_AVAILABLE(10_7, 5_0); // The volume's creation date, or nil if this cannot be determined. (Read-only, value type NSDate)
-FOUNDATION_EXPORT NSString * const NSURLVolumeURLForRemountingKey           NS_AVAILABLE(10_7, 5_0); // The NSURL needed to remount a network volume, or nil if not available. (Read-only, value type NSURL)
-FOUNDATION_EXPORT NSString * const NSURLVolumeUUIDStringKey                 NS_AVAILABLE(10_7, 5_0); // The volume's persistent UUID as a string, or nil if a persistent UUID is not available for the volume. (Read-only, value type NSString)
-FOUNDATION_EXPORT NSString * const NSURLVolumeNameKey                       NS_AVAILABLE(10_7, 5_0); // The name of the volume (Read-write if NSURLVolumeSupportsRenamingKey is YES, otherwise read-only, value type NSString)
-FOUNDATION_EXPORT NSString * const NSURLVolumeLocalizedNameKey              NS_AVAILABLE(10_7, 5_0); // The user-presentable name of the volume (Read-only, value type NSString)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeLocalizedFormatDescriptionKey NS_AVAILABLE(10_6, 4_0); // The user-visible volume format (Read-only, value type NSString)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeTotalCapacityKey              NS_AVAILABLE(10_6, 4_0); // Total volume capacity in bytes (Read-only, value type NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeAvailableCapacityKey          NS_AVAILABLE(10_6, 4_0); // Total free space in bytes (Read-only, value type NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeResourceCountKey              NS_AVAILABLE(10_6, 4_0); // Total number of resources on the volume (Read-only, value type NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsPersistentIDsKey      NS_AVAILABLE(10_6, 4_0); // true if the volume format supports persistent object identifiers and can look up file system objects by their IDs (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsSymbolicLinksKey      NS_AVAILABLE(10_6, 4_0); // true if the volume format supports symbolic links (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsHardLinksKey          NS_AVAILABLE(10_6, 4_0); // true if the volume format supports hard links (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsJournalingKey         NS_AVAILABLE(10_6, 4_0); // true if the volume format supports a journal used to speed recovery in case of unplanned restart (such as a power outage or crash). This does not necessarily mean the volume is actively using a journal. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeIsJournalingKey               NS_AVAILABLE(10_6, 4_0); // true if the volume is currently using a journal for speedy recovery after an unplanned restart. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsSparseFilesKey        NS_AVAILABLE(10_6, 4_0); // true if the volume format supports sparse files, that is, files which can have 'holes' that have never been written to, and thus do not consume space on disk. A sparse file may have an allocated size on disk that is less than its logical length (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsZeroRunsKey           NS_AVAILABLE(10_6, 4_0); // For security reasons, parts of a file (runs) that have never been written to must appear to contain zeroes. true if the volume keeps track of allocated but unwritten runs of a file so that it can substitute zeroes without actually writing zeroes to the media. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsCaseSensitiveNamesKey NS_AVAILABLE(10_6, 4_0); // true if the volume format treats upper and lower case characters in file and directory names as different. Otherwise an upper case character is equivalent to a lower case character, and you can't have two names that differ solely in the case of the characters. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsCasePreservedNamesKey NS_AVAILABLE(10_6, 4_0); // true if the volume format preserves the case of file and directory names.  Otherwise the volume may change the case of some characters (typically making them all upper or all lower case). (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsRootDirectoryDatesKey NS_AVAILABLE(10_7, 5_0); // true if the volume supports reliable storage of times for the root directory. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsVolumeSizesKey        NS_AVAILABLE(10_7, 5_0); // true if the volume supports returning volume size values (NSURLVolumeTotalCapacityKey and NSURLVolumeAvailableCapacityKey). (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsRenamingKey           NS_AVAILABLE(10_7, 5_0); // true if the volume can be renamed. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsAdvisoryFileLockingKey NS_AVAILABLE(10_7, 5_0); // true if the volume implements whole-file flock(2) style advisory locks, and the O_EXLOCK and O_SHLOCK flags of the open(2) call. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsExtendedSecurityKey   NS_AVAILABLE(10_7, 5_0); // true if the volume implements extended security (ACLs). (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeIsBrowsableKey                NS_AVAILABLE(10_7, 5_0); // true if the volume should be visible via the GUI (i.e., appear on the Desktop as a separate volume). (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeMaximumFileSizeKey            NS_AVAILABLE(10_7, 5_0); // The largest file size (in bytes) supported by this file system, or nil if this cannot be determined. (Read-only, value type NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeIsEjectableKey                NS_AVAILABLE(10_7, 5_0); // true if the volume's media is ejectable from the drive mechanism under software control. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeIsRemovableKey                NS_AVAILABLE(10_7, 5_0); // true if the volume's media is removable from the drive mechanism. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeIsInternalKey                 NS_AVAILABLE(10_7, 5_0); // true if the volume's device is connected to an internal bus, false if connected to an external bus, or nil if not available. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeIsAutomountedKey              NS_AVAILABLE(10_7, 5_0); // true if the volume is automounted. Note: do not mistake this with the functionality provided by kCFURLVolumeSupportsBrowsingKey. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeIsLocalKey                    NS_AVAILABLE(10_7, 5_0); // true if the volume is stored on a local device. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeIsReadOnlyKey                 NS_AVAILABLE(10_7, 5_0); // true if the volume is read-only. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeCreationDateKey               NS_AVAILABLE(10_7, 5_0); // The volume's creation date, or nil if this cannot be determined. (Read-only, value type NSDate)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeURLForRemountingKey           NS_AVAILABLE(10_7, 5_0); // The NSURL needed to remount a network volume, or nil if not available. (Read-only, value type NSURL)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeUUIDStringKey                 NS_AVAILABLE(10_7, 5_0); // The volume's persistent UUID as a string, or nil if a persistent UUID is not available for the volume. (Read-only, value type NSString)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeNameKey                       NS_AVAILABLE(10_7, 5_0); // The name of the volume (Read-write if NSURLVolumeSupportsRenamingKey is YES, otherwise read-only, value type NSString)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeLocalizedNameKey              NS_AVAILABLE(10_7, 5_0); // The user-presentable name of the volume (Read-only, value type NSString)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeIsEncryptedKey                API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)); // true if the volume is encrypted. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeIsRootFileSystemKey           API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)); // true if the volume is the root filesystem. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsCompressionKey        API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)); // true if the volume supports transparent decompression of compressed files using decmpfs. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsFileCloningKey API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)); // true if the volume supports clonefile(2) (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsSwapRenamingKey API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)); // true if the volume supports renamex_np(2)'s RENAME_SWAP option (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLVolumeSupportsExclusiveRenamingKey API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0)); // true if the volume supports renamex_np(2)'s RENAME_EXCL option (Read-only, value type boolean NSNumber)
 
 /* Ubiquitous item resource keys
  */
-FOUNDATION_EXPORT NSString * const NSURLIsUbiquitousItemKey                     NS_AVAILABLE(10_7, 5_0); // true if this item is synced to the cloud, false if it is only a local file. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLUbiquitousItemHasUnresolvedConflictsKey NS_AVAILABLE(10_7, 5_0); // true if this item has conflicts outstanding. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLUbiquitousItemIsDownloadedKey           NS_DEPRECATED(10_7, 10_9, 5_0, 7_0, "Use NSURLUbiquitousItemDownloadingStatusKey instead"); // equivalent to NSURLUbiquitousItemDownloadingStatusKey == NSURLUbiquitousItemDownloadingStatusCurrent. Has never behaved as documented in earlier releases, hence deprecated.  (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLUbiquitousItemIsDownloadingKey          NS_AVAILABLE(10_7, 5_0); // true if data is being downloaded for this item. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLUbiquitousItemIsUploadedKey             NS_AVAILABLE(10_7, 5_0); // true if there is data present in the cloud for this item. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLUbiquitousItemIsUploadingKey            NS_AVAILABLE(10_7, 5_0); // true if data is being uploaded for this item. (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLUbiquitousItemPercentDownloadedKey      NS_DEPRECATED(10_7, 10_8, 5_0, 6_0); // Use NSMetadataQuery and NSMetadataUbiquitousItemPercentDownloadedKey on NSMetadataItem instead
-FOUNDATION_EXPORT NSString * const NSURLUbiquitousItemPercentUploadedKey        NS_DEPRECATED(10_7, 10_8, 5_0, 6_0); // Use NSMetadataQuery and NSMetadataUbiquitousItemPercentUploadedKey on NSMetadataItem instead
-FOUNDATION_EXPORT NSString * const NSURLUbiquitousItemDownloadingStatusKey      NS_AVAILABLE(10_9, 7_0); // returns the download status of this item. (Read-only, value type NSString). Possible values below.
-FOUNDATION_EXPORT NSString * const NSURLUbiquitousItemDownloadingErrorKey       NS_AVAILABLE(10_9, 7_0); // returns the error when downloading the item from iCloud failed, see the NSUbiquitousFile section in FoundationErrors.h (Read-only, value type NSError)
-FOUNDATION_EXPORT NSString * const NSURLUbiquitousItemUploadingErrorKey         NS_AVAILABLE(10_9, 7_0); // returns the error when uploading the item to iCloud failed, see the NSUbiquitousFile section in FoundationErrors.h (Read-only, value type NSError)
-FOUNDATION_EXPORT NSString * const NSURLUbiquitousItemDownloadRequestedKey      NS_AVAILABLE(10_10, 8_0); // returns whether a download of this item has already been requested with an API like -startDownloadingUbiquitousItemAtURL:error: (Read-only, value type boolean NSNumber)
-FOUNDATION_EXPORT NSString * const NSURLUbiquitousItemContainerDisplayNameKey   NS_AVAILABLE(10_10, 8_0); // returns the name of this item's container as displayed to users.
-
+FOUNDATION_EXPORT NSURLResourceKey const NSURLIsUbiquitousItemKey                     NS_AVAILABLE(10_7, 5_0); // true if this item is synced to the cloud, false if it is only a local file. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLUbiquitousItemHasUnresolvedConflictsKey NS_AVAILABLE(10_7, 5_0); // true if this item has conflicts outstanding. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLUbiquitousItemIsDownloadedKey           NS_DEPRECATED(10_7, 10_9, 5_0, 7_0, "Use NSURLUbiquitousItemDownloadingStatusKey instead"); // equivalent to NSURLUbiquitousItemDownloadingStatusKey == NSURLUbiquitousItemDownloadingStatusCurrent. Has never behaved as documented in earlier releases, hence deprecated.  (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLUbiquitousItemIsDownloadingKey          NS_AVAILABLE(10_7, 5_0); // true if data is being downloaded for this item. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLUbiquitousItemIsUploadedKey             NS_AVAILABLE(10_7, 5_0); // true if there is data present in the cloud for this item. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLUbiquitousItemIsUploadingKey            NS_AVAILABLE(10_7, 5_0); // true if data is being uploaded for this item. (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLUbiquitousItemPercentDownloadedKey      NS_DEPRECATED(10_7, 10_8, 5_0, 6_0); // Use NSMetadataQuery and NSMetadataUbiquitousItemPercentDownloadedKey on NSMetadataItem instead
+FOUNDATION_EXPORT NSURLResourceKey const NSURLUbiquitousItemPercentUploadedKey        NS_DEPRECATED(10_7, 10_8, 5_0, 6_0); // Use NSMetadataQuery and NSMetadataUbiquitousItemPercentUploadedKey on NSMetadataItem instead
+FOUNDATION_EXPORT NSURLResourceKey const NSURLUbiquitousItemDownloadingStatusKey      NS_AVAILABLE(10_9, 7_0); // returns the download status of this item. (Read-only, value type NSString). Possible values below.
+FOUNDATION_EXPORT NSURLResourceKey const NSURLUbiquitousItemDownloadingErrorKey       NS_AVAILABLE(10_9, 7_0); // returns the error when downloading the item from iCloud failed, see the NSUbiquitousFile section in FoundationErrors.h (Read-only, value type NSError)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLUbiquitousItemUploadingErrorKey         NS_AVAILABLE(10_9, 7_0); // returns the error when uploading the item to iCloud failed, see the NSUbiquitousFile section in FoundationErrors.h (Read-only, value type NSError)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLUbiquitousItemDownloadRequestedKey      NS_AVAILABLE(10_10, 8_0); // returns whether a download of this item has already been requested with an API like -startDownloadingUbiquitousItemAtURL:error: (Read-only, value type boolean NSNumber)
+FOUNDATION_EXPORT NSURLResourceKey const NSURLUbiquitousItemContainerDisplayNameKey   NS_AVAILABLE(10_10, 8_0); // returns the name of this item's container as displayed to users.
 
+typedef NSString * NSURLUbiquitousItemDownloadingStatus NS_STRING_ENUM;
 /* The values returned for the NSURLUbiquitousItemDownloadingStatusKey
  */
-FOUNDATION_EXPORT NSString * const NSURLUbiquitousItemDownloadingStatusNotDownloaded  NS_AVAILABLE(10_9, 7_0); // this item has not been downloaded yet. Use startDownloadingUbiquitousItemAtURL:error: to download it.
-FOUNDATION_EXPORT NSString * const NSURLUbiquitousItemDownloadingStatusDownloaded     NS_AVAILABLE(10_9, 7_0); // there is a local version of this item available. The most current version will get downloaded as soon as possible.
-FOUNDATION_EXPORT NSString * const NSURLUbiquitousItemDownloadingStatusCurrent        NS_AVAILABLE(10_9, 7_0); // there is a local version of this item and it is the most up-to-date version known to this device.
+FOUNDATION_EXPORT NSURLUbiquitousItemDownloadingStatus const NSURLUbiquitousItemDownloadingStatusNotDownloaded  NS_AVAILABLE(10_9, 7_0); // this item has not been downloaded yet. Use startDownloadingUbiquitousItemAtURL:error: to download it.
+FOUNDATION_EXPORT NSURLUbiquitousItemDownloadingStatus const NSURLUbiquitousItemDownloadingStatusDownloaded     NS_AVAILABLE(10_9, 7_0); // there is a local version of this item available. The most current version will get downloaded as soon as possible.
+FOUNDATION_EXPORT NSURLUbiquitousItemDownloadingStatus const NSURLUbiquitousItemDownloadingStatusCurrent        NS_AVAILABLE(10_9, 7_0); // there is a local version of this item and it is the most up-to-date version known to this device.
 
 /* Working with Bookmarks and alias (bookmark) files 
  */
@@ -354,18 +377,18 @@
 
 /* Returns bookmark data for the URL, created with specified options and resource values. If this method returns nil, the optional error is populated.
  */
-- (nullable NSData *)bookmarkDataWithOptions:(NSURLBookmarkCreationOptions)options includingResourceValuesForKeys:(nullable NSArray<NSString *> *)keys relativeToURL:(nullable NSURL *)relativeURL error:(NSError **)error NS_AVAILABLE(10_6, 4_0);
+- (nullable NSData *)bookmarkDataWithOptions:(NSURLBookmarkCreationOptions)options includingResourceValuesForKeys:(nullable NSArray<NSURLResourceKey> *)keys relativeToURL:(nullable NSURL *)relativeURL error:(NSError **)error NS_AVAILABLE(10_6, 4_0);
 
 /* Initializes a newly created NSURL that refers to a location specified by resolving bookmark data. If this method returns nil, the optional error is populated.
  */
-- (nullable instancetype)initByResolvingBookmarkData:(NSData *)bookmarkData options:(NSURLBookmarkResolutionOptions)options relativeToURL:(nullable NSURL *)relativeURL bookmarkDataIsStale:(BOOL * __nullable)isStale error:(NSError **)error NS_AVAILABLE(10_6, 4_0);
+- (nullable instancetype)initByResolvingBookmarkData:(NSData *)bookmarkData options:(NSURLBookmarkResolutionOptions)options relativeToURL:(nullable NSURL *)relativeURL bookmarkDataIsStale:(BOOL * _Nullable)isStale error:(NSError **)error NS_AVAILABLE(10_6, 4_0);
 /* Creates and Initializes an NSURL that refers to a location specified by resolving bookmark data. If this method returns nil, the optional error is populated.
  */
-+ (nullable instancetype)URLByResolvingBookmarkData:(NSData *)bookmarkData options:(NSURLBookmarkResolutionOptions)options relativeToURL:(nullable NSURL *)relativeURL bookmarkDataIsStale:(BOOL * __nullable)isStale error:(NSError **)error NS_AVAILABLE(10_6, 4_0);
++ (nullable instancetype)URLByResolvingBookmarkData:(NSData *)bookmarkData options:(NSURLBookmarkResolutionOptions)options relativeToURL:(nullable NSURL *)relativeURL bookmarkDataIsStale:(BOOL * _Nullable)isStale error:(NSError **)error NS_AVAILABLE(10_6, 4_0);
 
 /* Returns the resource values for properties identified by a specified array of keys contained in specified bookmark data. If the result dictionary does not contain a resource value for one or more of the requested resource keys, it means those resource properties are not available in the bookmark data.
  */
-+ (nullable NSDictionary<NSString *, id> *)resourceValuesForKeys:(NSArray<NSString *> *)keys fromBookmarkData:(NSData *)bookmarkData NS_AVAILABLE(10_6, 4_0);
++ (nullable NSDictionary<NSURLResourceKey, id> *)resourceValuesForKeys:(NSArray<NSURLResourceKey> *)keys fromBookmarkData:(NSData *)bookmarkData NS_AVAILABLE(10_6, 4_0);
 
 /* Creates an alias file on disk at a specified location with specified bookmark data. bookmarkData must have been created with the NSURLBookmarkCreationSuitableForBookmarkFile option. bookmarkFileURL must either refer to an existing file (which will be overwritten), or to location in an existing directory. If this method returns NO, the optional error is populated.
 */
@@ -403,8 +426,8 @@
  
  Most of the NSURL resource value keys will work with these APIs. However, there are some that are tied to the item's contents that will not work, such as NSURLContentAccessDateKey or NSURLGenerationIdentifierKey. If one of these keys is used, the method will return YES, but the value for the key will be nil.
 */
-- (BOOL)getPromisedItemResourceValue:(id __nullable * __nonnull)value forKey:(NSString *)key error:(NSError **)error NS_AVAILABLE(10_10, 8_0);
-- (nullable NSDictionary<NSString *, id> *)promisedItemResourceValuesForKeys:(NSArray<NSString *> *)keys error:(NSError **)error NS_AVAILABLE(10_10, 8_0);
+- (BOOL)getPromisedItemResourceValue:(id _Nullable * _Nonnull)value forKey:(NSURLResourceKey)key error:(NSError **)error NS_AVAILABLE(10_10, 8_0);
+- (nullable NSDictionary<NSURLResourceKey, id> *)promisedItemResourceValuesForKeys:(NSArray<NSURLResourceKey> *)keys error:(NSError **)error NS_AVAILABLE(10_10, 8_0);
 - (BOOL)checkPromisedItemIsReachableAndReturnError:(NSError **)error NS_SWIFT_NOTHROW NS_AVAILABLE(10_10, 8_0);
 
 @end
@@ -539,11 +562,19 @@
 @property (nullable, readonly, copy) NSArray<NSString *> *pathComponents NS_AVAILABLE(10_6, 4_0);
 @property (nullable, readonly, copy) NSString *lastPathComponent NS_AVAILABLE(10_6, 4_0);
 @property (nullable, readonly, copy) NSString *pathExtension NS_AVAILABLE(10_6, 4_0);
+#if !defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH) && SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 6)
+- (nullable NSURL *)URLByAppendingPathComponent:(NSString *)pathComponent NS_AVAILABLE(10_6, 4_0);
+- (nullable NSURL *)URLByAppendingPathComponent:(NSString *)pathComponent isDirectory:(BOOL)isDirectory NS_AVAILABLE(10_7, 5_0);
+@property (nullable, readonly, copy) NSURL *URLByDeletingLastPathComponent NS_AVAILABLE(10_6, 4_0);
+- (nullable NSURL *)URLByAppendingPathExtension:(NSString *)pathExtension NS_AVAILABLE(10_6, 4_0);
+@property (nullable, readonly, copy) NSURL *URLByDeletingPathExtension NS_AVAILABLE(10_6, 4_0);
+#else
 - (NSURL *)URLByAppendingPathComponent:(NSString *)pathComponent NS_AVAILABLE(10_6, 4_0);
 - (NSURL *)URLByAppendingPathComponent:(NSString *)pathComponent isDirectory:(BOOL)isDirectory NS_AVAILABLE(10_7, 5_0);
 @property (nullable, readonly, copy) NSURL *URLByDeletingLastPathComponent NS_AVAILABLE(10_6, 4_0);
 - (NSURL *)URLByAppendingPathExtension:(NSString *)pathExtension NS_AVAILABLE(10_6, 4_0);
 @property (nullable, readonly, copy) NSURL *URLByDeletingPathExtension NS_AVAILABLE(10_6, 4_0);
+#endif // SWIFT_SDK_OVERLAY_FOUNDATION_EPOCH >= 6
 
 /* The following methods work only on `file:` scheme URLs; for non-`file:` scheme URLs, these methods return the URL unchanged.
  */
@@ -572,12 +603,14 @@
 
 /* Client informal protocol for use with the deprecated loadResourceDataNotifyingClient: below.
  */
+#if !defined(SWIFT_CLASS_EXTRA)
 @interface NSObject (NSURLClient)
 - (void)URL:(NSURL *)sender resourceDataDidBecomeAvailable:(NSData *)newBytes NS_DEPRECATED(10_0, 10_4, 2_0, 2_0);
 - (void)URLResourceDidFinishLoading:(NSURL *)sender NS_DEPRECATED(10_0, 10_4, 2_0, 2_0);
 - (void)URLResourceDidCancelLoading:(NSURL *)sender NS_DEPRECATED(10_0, 10_4, 2_0, 2_0);
 - (void)URL:(NSURL *)sender resourceDidFailLoadingWithReason:(NSString *)reason NS_DEPRECATED(10_0, 10_4, 2_0, 2_0);
 @end
+#endif
 
 @interface NSURL (NSURLLoading)
 - (nullable NSData *)resourceDataUsingCache:(BOOL)shouldUseCache NS_DEPRECATED(10_0, 10_4, 2_0, 2_0); // Blocks to load the data if necessary.  If shouldUseCache is YES, then if an equivalent URL has already been loaded and cached, its resource data will be returned immediately.  If shouldUseCache is NO, a new load will be started
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCache.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCache.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCache.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCache.h	2016-05-20 07:24:14.000000000 +0200
@@ -257,7 +257,7 @@
 
 @interface NSURLCache (NSURLSessionTaskAdditions)
 - (void)storeCachedResponse:(NSCachedURLResponse *)cachedResponse forDataTask:(NSURLSessionDataTask *)dataTask NS_AVAILABLE(10_10, 8_0);
-- (void)getCachedResponseForDataTask:(NSURLSessionDataTask *)dataTask completionHandler:(void (^) (NSCachedURLResponse * __nullable cachedResponse))completionHandler NS_AVAILABLE(10_10, 8_0);
+- (void)getCachedResponseForDataTask:(NSURLSessionDataTask *)dataTask completionHandler:(void (^) (NSCachedURLResponse * _Nullable cachedResponse))completionHandler NS_AVAILABLE(10_10, 8_0);
 - (void)removeCachedResponseForDataTask:(NSURLSessionDataTask *)dataTask NS_AVAILABLE(10_10, 8_0);
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLConnection.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLConnection.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLConnection.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLConnection.h	2016-05-20 07:39:55.000000000 +0200
@@ -6,6 +6,7 @@
 */
 
 #import <Foundation/NSObject.h>
+#import <Foundation/NSRunLoop.h>
 
 @class NSArray;
 @class NSURL;
@@ -125,8 +126,8 @@
 - (void)start NS_AVAILABLE(10_5, 2_0);
 - (void)cancel;
 
-- (void)scheduleInRunLoop:(NSRunLoop *)aRunLoop forMode:(NSString *)mode NS_AVAILABLE(10_5, 2_0);
-- (void)unscheduleFromRunLoop:(NSRunLoop *)aRunLoop forMode:(NSString *)mode NS_AVAILABLE(10_5, 2_0);
+- (void)scheduleInRunLoop:(NSRunLoop *)aRunLoop forMode:(NSRunLoopMode)mode NS_AVAILABLE(10_5, 2_0);
+- (void)unscheduleFromRunLoop:(NSRunLoop *)aRunLoop forMode:(NSRunLoopMode)mode NS_AVAILABLE(10_5, 2_0);
 - (void)setDelegateQueue:(nullable NSOperationQueue*) queue NS_AVAILABLE(10_7, 5_0);
 
 
@@ -404,7 +405,7 @@
     @result      The content of the URL resulting from performing the load,
                  or nil if the load failed.
 */
-+ (nullable NSData *)sendSynchronousRequest:(NSURLRequest *)request returningResponse:(NSURLResponse * __nullable * __nullable)response error:(NSError **)error NS_DEPRECATED(10_3, 10_11, 2_0, 9_0, "Use [NSURLSession dataTaskWithRequest:completionHandler:] (see NSURLSession.h") __WATCHOS_PROHIBITED;
++ (nullable NSData *)sendSynchronousRequest:(NSURLRequest *)request returningResponse:(NSURLResponse * _Nullable * _Nullable)response error:(NSError **)error NS_DEPRECATED(10_3, 10_11, 2_0, 9_0, "Use [NSURLSession dataTaskWithRequest:completionHandler:] (see NSURLSession.h") __WATCHOS_PROHIBITED;
 
 @end
 
@@ -455,7 +456,7 @@
  */
 + (void)sendAsynchronousRequest:(NSURLRequest*) request
                           queue:(NSOperationQueue*) queue
-              completionHandler:(void (^)(NSURLResponse* __nullable response, NSData* __nullable data, NSError* __nullable connectionError)) handler NS_DEPRECATED(10_7, 10_11, 5_0, 9_0, "Use [NSURLSession dataTaskWithRequest:completionHandler:] (see NSURLSession.h") __WATCHOS_PROHIBITED;
+              completionHandler:(void (^)(NSURLResponse* _Nullable response, NSData* _Nullable data, NSError* _Nullable connectionError)) handler NS_DEPRECATED(10_7, 10_11, 5_0, 9_0, "Use [NSURLSession dataTaskWithRequest:completionHandler:] (see NSURLSession.h") __WATCHOS_PROHIBITED;
            
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCredentialStorage.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCredentialStorage.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCredentialStorage.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLCredentialStorage.h	2016-05-20 06:24:14.000000000 +0200
@@ -7,6 +7,7 @@
 
 #import <Foundation/NSObject.h>
 #import <Foundation/NSURLProtectionSpace.h>
+#import <Foundation/NSNotification.h>
 
 @class NSDictionary<KeyType, ObjectType>;
 @class NSString;
@@ -106,10 +107,10 @@
 @end
 
 @interface NSURLCredentialStorage (NSURLSessionTaskAdditions)
-- (void)getCredentialsForProtectionSpace:(NSURLProtectionSpace *)protectionSpace task:(NSURLSessionTask *)task completionHandler:(void (^) (NSDictionary<NSString *, NSURLCredential *> * __nullable credentials))completionHandler NS_AVAILABLE(10_10, 8_0);
+- (void)getCredentialsForProtectionSpace:(NSURLProtectionSpace *)protectionSpace task:(NSURLSessionTask *)task completionHandler:(void (^) (NSDictionary<NSString *, NSURLCredential *> * _Nullable credentials))completionHandler NS_AVAILABLE(10_10, 8_0);
 - (void)setCredential:(NSURLCredential *)credential forProtectionSpace:(NSURLProtectionSpace *)protectionSpace task:(NSURLSessionTask *)task NS_AVAILABLE(10_10, 8_0);
 - (void)removeCredential:(NSURLCredential *)credential forProtectionSpace:(NSURLProtectionSpace *)protectionSpace options:(nullable NSDictionary<NSString *, id> *)options task:(NSURLSessionTask *)task NS_AVAILABLE(10_10, 8_0);
-- (void)getDefaultCredentialForProtectionSpace:(NSURLProtectionSpace *)space task:(NSURLSessionTask *)task completionHandler:(void (^) (NSURLCredential * __nullable credential))completionHandler NS_AVAILABLE(10_10, 8_0);
+- (void)getDefaultCredentialForProtectionSpace:(NSURLProtectionSpace *)space task:(NSURLSessionTask *)task completionHandler:(void (^) (NSURLCredential * _Nullable credential))completionHandler NS_AVAILABLE(10_10, 8_0);
 - (void)setDefaultCredential:(NSURLCredential *)credential forProtectionSpace:(NSURLProtectionSpace *)protectionSpace task:(NSURLSessionTask *)task NS_AVAILABLE(10_10, 8_0);
 @end
 
@@ -118,7 +119,7 @@
     @abstract This notification is sent on the main thread whenever
     the set of stored credentials changes.
 */
-FOUNDATION_EXPORT NSString *const NSURLCredentialStorageChangedNotification;
+FOUNDATION_EXPORT NSNotificationName const NSURLCredentialStorageChangedNotification;
 
 /*
  *  NSURLCredentialStorageRemoveSynchronizableCredentials - (NSNumber value)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLError.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLError.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLError.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLError.h	2016-05-20 07:39:55.000000000 +0200
@@ -15,6 +15,7 @@
 #endif
 
 #import <Foundation/NSObjCRuntime.h>
+#import <Foundation/NSError.h>
 
 @class NSString;
 
@@ -24,7 +25,7 @@
     @discussion Constants used by NSError to differentiate between "domains" of error codes, serving as a discriminator for error codes that originate from different subsystems or sources.
     @constant NSURLErrorDomain Indicates an NSURL error.
 */
-FOUNDATION_EXPORT NSString * const NSURLErrorDomain;
+FOUNDATION_EXPORT NSErrorDomain const NSURLErrorDomain;
 
 /*!
     @const NSURLErrorFailingURLErrorKey
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLProtocol.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLProtocol.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLProtocol.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLProtocol.h	2016-05-20 06:24:14.000000000 +0200
@@ -214,8 +214,7 @@
     @discussion A concrete subclass should inspect the given request and
     determine whether or not the implementation can perform a load with
     that request. This is an abstract method. Sublasses must provide an
-    implementation. The implementation in this class calls
-    NSRequestConcreteImplementation.
+    implementation.
     @param request A request to inspect.
     @result YES if the protocol can handle the given request, NO if not.
 */
@@ -234,8 +233,7 @@
     equality checks between NSURLRequest objects.
     <p>
     This is an abstract method; sublasses must provide an
-    implementation. The implementation in this class calls
-    NSRequestConcreteImplementation.
+    implementation.
     @param request A request to make canonical.
     @result The canonical form of the given request. 
 */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLSession.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLSession.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLSession.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLSession.h	2016-05-20 07:39:55.000000000 +0200
@@ -98,6 +98,9 @@
 @class NSURLSessionConfiguration;
 @protocol NSURLSessionDelegate;
 
+@class NSURLSessionTaskMetrics;
+@class NSDateInterval;
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*
@@ -230,14 +233,14 @@
  * see <Foundation/NSURLError.h>.  The delegate, if any, will still be
  * called for authentication challenges.
  */
-- (NSURLSessionDataTask *)dataTaskWithRequest:(NSURLRequest *)request completionHandler:(void (^)(NSData * __nullable data, NSURLResponse * __nullable response, NSError * __nullable error))completionHandler;
-- (NSURLSessionDataTask *)dataTaskWithURL:(NSURL *)url completionHandler:(void (^)(NSData * __nullable data, NSURLResponse * __nullable response, NSError * __nullable error))completionHandler;
+- (NSURLSessionDataTask *)dataTaskWithRequest:(NSURLRequest *)request completionHandler:(void (^)(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error))completionHandler;
+- (NSURLSessionDataTask *)dataTaskWithURL:(NSURL *)url completionHandler:(void (^)(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error))completionHandler;
 
 /*
  * upload convenience method.
  */
-- (NSURLSessionUploadTask *)uploadTaskWithRequest:(NSURLRequest *)request fromFile:(NSURL *)fileURL completionHandler:(void (^)(NSData * __nullable data, NSURLResponse * __nullable response, NSError * __nullable error))completionHandler;
-- (NSURLSessionUploadTask *)uploadTaskWithRequest:(NSURLRequest *)request fromData:(nullable NSData *)bodyData completionHandler:(void (^)(NSData * __nullable data, NSURLResponse * __nullable response, NSError * __nullable error))completionHandler;
+- (NSURLSessionUploadTask *)uploadTaskWithRequest:(NSURLRequest *)request fromFile:(NSURL *)fileURL completionHandler:(void (^)(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error))completionHandler;
+- (NSURLSessionUploadTask *)uploadTaskWithRequest:(NSURLRequest *)request fromData:(nullable NSData *)bodyData completionHandler:(void (^)(NSData * _Nullable data, NSURLResponse * _Nullable response, NSError * _Nullable error))completionHandler;
 
 /*
  * download task convenience methods.  When a download successfully
@@ -245,9 +248,9 @@
  * copied during the invocation of the completion routine.  The file
  * will be removed automatically.
  */
-- (NSURLSessionDownloadTask *)downloadTaskWithRequest:(NSURLRequest *)request completionHandler:(void (^)(NSURL * __nullable location, NSURLResponse * __nullable response, NSError * __nullable error))completionHandler;
-- (NSURLSessionDownloadTask *)downloadTaskWithURL:(NSURL *)url completionHandler:(void (^)(NSURL * __nullable location, NSURLResponse * __nullable response, NSError * __nullable error))completionHandler;
-- (NSURLSessionDownloadTask *)downloadTaskWithResumeData:(NSData *)resumeData completionHandler:(void (^)(NSURL * __nullable location, NSURLResponse * __nullable response, NSError * __nullable error))completionHandler;
+- (NSURLSessionDownloadTask *)downloadTaskWithRequest:(NSURLRequest *)request completionHandler:(void (^)(NSURL * _Nullable location, NSURLResponse * _Nullable response, NSError * _Nullable error))completionHandler;
+- (NSURLSessionDownloadTask *)downloadTaskWithURL:(NSURL *)url completionHandler:(void (^)(NSURL * _Nullable location, NSURLResponse * _Nullable response, NSError * _Nullable error))completionHandler;
+- (NSURLSessionDownloadTask *)downloadTaskWithResumeData:(NSData *)resumeData completionHandler:(void (^)(NSURL * _Nullable location, NSURLResponse * _Nullable response, NSError * _Nullable error))completionHandler;
 
 @end
 
@@ -377,7 +380,7 @@
  * If resume data cannot be created, the completion handler will be
  * called with nil resumeData.
  */
-- (void)cancelByProducingResumeData:(void (^)(NSData * __nullable resumeData))completionHandler;
+- (void)cancelByProducingResumeData:(void (^)(NSData * _Nullable resumeData))completionHandler;
 
 @end
 
@@ -412,14 +415,14 @@
  * If an error occurs, any outstanding reads will also fail, and new
  * read requests will error out immediately.
  */
-- (void)readDataOfMinLength:(NSUInteger)minBytes maxLength:(NSUInteger)maxBytes timeout:(NSTimeInterval)timeout completionHandler:(void (^) (NSData * __nullable data, BOOL atEOF, NSError * __nullable error))completionHandler;
+- (void)readDataOfMinLength:(NSUInteger)minBytes maxLength:(NSUInteger)maxBytes timeout:(NSTimeInterval)timeout completionHandler:(void (^) (NSData * _Nullable data, BOOL atEOF, NSError * _Nullable error))completionHandler;
 
 /* Write the data completely to the underlying socket.  If all the
  * bytes have not been written by the timeout, a timeout error will
  * occur.  Note that invocation of the completion handler does not
  * guarantee that the remote side has received all the bytes, only
  * that they have been written to the kernel. */
-- (void)writeData:(NSData *)data timeout:(NSTimeInterval)timeout completionHandler:(void (^) (NSError * __nullable error))completionHandler;
+- (void)writeData:(NSData *)data timeout:(NSTimeInterval)timeout completionHandler:(void (^) (NSError * _Nullable error))completionHandler;
 
 /* -captureStreams completes any already enqueued reads
  * and writes, and then invokes the
@@ -611,7 +614,7 @@
  * interaction. 
  */
 - (void)URLSession:(NSURLSession *)session didReceiveChallenge:(NSURLAuthenticationChallenge *)challenge
-                                             completionHandler:(void (^)(NSURLSessionAuthChallengeDisposition disposition, NSURLCredential * __nullable credential))completionHandler;
+                                             completionHandler:(void (^)(NSURLSessionAuthChallengeDisposition disposition, NSURLCredential * _Nullable credential))completionHandler;
 
 /* If an application has received an
  * -application:handleEventsForBackgroundURLSession:completionHandler:
@@ -643,7 +646,7 @@
 - (void)URLSession:(NSURLSession *)session task:(NSURLSessionTask *)task
                      willPerformHTTPRedirection:(NSHTTPURLResponse *)response
                                      newRequest:(NSURLRequest *)request
-                              completionHandler:(void (^)(NSURLRequest * __nullable))completionHandler;
+                              completionHandler:(void (^)(NSURLRequest * _Nullable))completionHandler;
 
 /* The task has received a request specific authentication challenge.
  * If this delegate is not implemented, the session specific authentication challenge
@@ -652,14 +655,14 @@
  */
 - (void)URLSession:(NSURLSession *)session task:(NSURLSessionTask *)task
                             didReceiveChallenge:(NSURLAuthenticationChallenge *)challenge 
-                              completionHandler:(void (^)(NSURLSessionAuthChallengeDisposition disposition, NSURLCredential * __nullable credential))completionHandler;
+                              completionHandler:(void (^)(NSURLSessionAuthChallengeDisposition disposition, NSURLCredential * _Nullable credential))completionHandler;
 
 /* Sent if a task requires a new, unopened body stream.  This may be
  * necessary when authentication has failed for any request that
  * involves a body stream. 
  */
 - (void)URLSession:(NSURLSession *)session task:(NSURLSessionTask *)task
-                              needNewBodyStream:(void (^)(NSInputStream * __nullable bodyStream))completionHandler;
+                              needNewBodyStream:(void (^)(NSInputStream * _Nullable bodyStream))completionHandler;
 
 /* Sent periodically to notify the delegate of upload progress.  This
  * information is also available as properties of the task.
@@ -669,6 +672,11 @@
                                  totalBytesSent:(int64_t)totalBytesSent
                        totalBytesExpectedToSend:(int64_t)totalBytesExpectedToSend;
 
+/*
+ * Sent when complete statistics information has been collected for the task.
+ */
+- (void)URLSession:(NSURLSession *)session task:(NSURLSessionTask *)task didFinishCollectingMetrics:(NSURLSessionTaskMetrics *)metrics API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
 /* Sent as the last message related to a specific task.  Error may be
  * nil, which implies that no error occurred and this task is complete. 
  */
@@ -736,7 +744,7 @@
  */
 - (void)URLSession:(NSURLSession *)session dataTask:(NSURLSessionDataTask *)dataTask
                                   willCacheResponse:(NSCachedURLResponse *)proposedResponse 
-                                  completionHandler:(void (^)(NSCachedURLResponse * __nullable cachedResponse))completionHandler;
+                                  completionHandler:(void (^)(NSCachedURLResponse * _Nullable cachedResponse))completionHandler;
 
 @end
 
@@ -817,4 +825,173 @@
 + (NSURLSessionConfiguration *)backgroundSessionConfiguration:(NSString *)identifier NS_DEPRECATED(NSURLSESSION_AVAILABLE, 10_10, 7_0, 8_0, "Please use backgroundSessionConfigurationWithIdentifier: instead");
 @end
 
+/*
+ * The resource fetch type.
+ */
+typedef NS_ENUM(NSInteger, NSURLSessionTaskMetricsResourceFetchType) {
+    NSURLSessionTaskMetricsResourceFetchTypeUnknown,
+    NSURLSessionTaskMetricsResourceFetchTypeNetworkLoad,   /* The resource was loaded over the network. */
+    NSURLSessionTaskMetricsResourceFetchTypeServerPush,    /* The resource was pushed by the server to the client. */
+    NSURLSessionTaskMetricsResourceFetchTypeLocalCache,    /* The resource was retrieved from the local storage. */
+} API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0));
+
+/*
+ * This class defines the performance metrics collected for a request/response transaction during the task execution.
+ */
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSURLSessionTaskTransactionMetrics : NSObject
+
+/*
+ * Represents the transaction request.
+ */
+@property (copy, readonly) NSURLRequest *request;
+
+/*
+ * Represents the transaction response. Can be nil if error occurred and no response was generated.
+ */
+@property (nullable, copy, readonly) NSURLResponse *response;
+
+/*
+ * For all NSDate metrics below, if that aspect of the task could not be completed, then the corresponding “EndDate” metric will be nil.
+ * For example, if a name lookup was started but the name lookup timed out, failed, or the client canceled the task before the name could be resolved -- then while domainLookupStartDate may be set, domainLookupEndDate will be nil along with all later metrics.
+ */
+
+/*
+ * fetchStartDate returns the time when the user agent started fetching the resource, whether or not the resource was retrieved from the server or local resources.
+ *
+ * The following metrics will be set to nil, if a persistent connection was used or the resource was retrieved from local resources:
+ *
+ *   domainLookupStartDate
+ *   domainLookupEndDate
+ *   connectStartDate
+ *   connectEndDate
+ *   secureConnectionStartDate
+ *   secureConnectionEndDate
+ */
+@property (nullable, copy, readonly) NSDate *fetchStartDate;
+
+/*
+ * domainLookupStartDate returns the time immediately before the user agent started the name lookup for the resource.
+ */
+@property (nullable, copy, readonly) NSDate *domainLookupStartDate;
+
+/*
+ * domainLookupEndDate returns the time after the name lookup was completed.
+ */
+@property (nullable, copy, readonly) NSDate *domainLookupEndDate;
+
+/*
+ * connectStartDate is the time immediately before the user agent started establishing the connection to the server.
+ *
+ * For example, this would correspond to the time immediately before the user agent started trying to establish the TCP connection.
+ */
+@property (nullable, copy, readonly) NSDate *connectStartDate;
+
+/*
+ * If an encrypted connection was used, secureConnectionStartDate is the time immediately before the user agent started the security handshake to secure the current connection.
+ *
+ * For example, this would correspond to the time immediately before the user agent started the TLS handshake.
+ *
+ * If an encrypted connection was not used, this attribute is set to nil.
+ */
+@property (nullable, copy, readonly) NSDate *secureConnectionStartDate;
+
+/*
+ * If an encrypted connection was used, secureConnectionEndDate is the time immediately after the security handshake completed.
+ *
+ * If an encrypted connection was not used, this attribute is set to nil.
+ */
+@property (nullable, copy, readonly) NSDate *secureConnectionEndDate;
+
+/*
+ * connectEndDate is the time immediately after the user agent finished establishing the connection to the server, including completion of security-related and other handshakes.
+ */
+@property (nullable, copy, readonly) NSDate *connectEndDate;
+
+/*
+ * requestStartDate is the time immediately before the user agent started requesting the source, regardless of whether the resource was retrieved from the server or local resources.
+ *
+ * For example, this would correspond to the time immediately before the user agent sent an HTTP GET request.
+ */
+@property (nullable, copy, readonly) NSDate *requestStartDate;
+
+/*
+ * requestEndDate is the time immediately after the user agent finished requesting the source, regardless of whether the resource was retrieved from the server or local resources.
+ *
+ * For example, this would correspond to the time immediately after the user agent finished sending the last byte of the request.
+ */
+@property (nullable, copy, readonly) NSDate *requestEndDate;
+
+/*
+ * responseStartDate is the time immediately after the user agent received the first byte of the response from the server or from local resources.
+ *
+ * For example, this would correspond to the time immediately after the user agent received the first byte of an HTTP response.
+ */
+@property (nullable, copy, readonly) NSDate *responseStartDate;
+
+/*
+ * responseEndDate is the time immediately after the user agent received the last byte of the resource.
+ */
+@property (nullable, copy, readonly) NSDate *responseEndDate;
+
+/*
+ * The network protocol used to fetch the resource, as identified by the ALPN Protocol ID Identification Sequence [RFC7301].
+ * E.g., http/2, http/1.1, spdy/3.1.
+ *
+ * When a proxy is configured AND a tunnel connection is established, then this attribute returns the value for the tunneled protocol.
+ *
+ * For example:
+ * If no proxy were used, and http/2 was negotiated, then http/2 would be returned.
+ * If HTTP/1.1 were used to the proxy, and the tunneled connection was HTTP/2, then http/2 would be returned.
+ * If HTTP/1.1 were used to the proxy, and there were no tunnel, then http/1.1 would be returned.
+ *
+ */
+@property (nullable, copy, readonly) NSString *networkProtocolName;
+
+/*
+ * This property is set to YES if a proxy connection was used to fetch the resource.
+ */
+@property (assign, readonly, getter=isProxyConnection) BOOL proxyConnection;
+
+/*
+ * This property is set to YES if a persistent connection was used to fetch the resource.
+ */
+@property (assign, readonly, getter=isReusedConnection) BOOL reusedConnection;
+
+/*
+ * Indicates whether the resource was loaded, pushed or retrieved from the local cache.
+ */
+@property (assign, readonly) NSURLSessionTaskMetricsResourceFetchType resourceFetchType;
+
+
+-(instancetype)init;
+
+
+@end
+
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSURLSessionTaskMetrics : NSObject
+
+/*
+ * transactionMetrics array contains the metrics collected for every request/response transaction created during the task execution.
+ */
+@property (copy, readonly) NSArray<NSURLSessionTaskTransactionMetrics *> *transactionMetrics;
+
+/*
+ * Interval from the task creation time to the task completion time.
+ * Task creation time is the time when the task was instantiated.
+ * Task completion time is the time when the task is about to change its internal state to completed.
+ */
+@property (copy, readonly) NSDateInterval *taskInterval;
+
+/*
+ * redirectCount is the number of redirects that were recorded.
+ */
+@property (assign, readonly) NSUInteger redirectCount;
+
+-(instancetype)init;
+
+@end
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUbiquitousKeyValueStore.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUbiquitousKeyValueStore.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUbiquitousKeyValueStore.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUbiquitousKeyValueStore.h	2016-05-20 06:24:14.000000000 +0200
@@ -3,6 +3,7 @@
 */
 
 #import <Foundation/NSObject.h>
+#import <Foundation/NSNotification.h>
 
 @class NSArray, NSDictionary<KeyType, ObjectType>, NSData, NSString;
 
@@ -50,7 +51,7 @@
 
 @end
 
-FOUNDATION_EXPORT NSString * const NSUbiquitousKeyValueStoreDidChangeExternallyNotification NS_AVAILABLE(10_7, 5_0);
+FOUNDATION_EXPORT NSNotificationName const NSUbiquitousKeyValueStoreDidChangeExternallyNotification NS_AVAILABLE(10_7, 5_0);
 FOUNDATION_EXPORT NSString * const NSUbiquitousKeyValueStoreChangeReasonKey NS_AVAILABLE(10_7, 5_0);
 FOUNDATION_EXPORT NSString * const NSUbiquitousKeyValueStoreChangedKeysKey NS_AVAILABLE(10_7, 5_0);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUndoManager.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUndoManager.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUndoManager.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUndoManager.h	2016-05-20 06:12:55.000000000 +0200
@@ -10,6 +10,8 @@
 
 #import <Foundation/NSObject.h>
 #include <stdint.h>
+#import <Foundation/NSNotification.h>
+#import <Foundation/NSRunLoop.h>
 
 @class NSArray<ObjectType>;
 @class NSString;
@@ -63,7 +65,7 @@
 
         /* Run Loop Modes */
 
-@property (copy) NSArray<NSString *> *runLoopModes;
+@property (copy) NSArray<NSRunLoopMode> *runLoopModes;
 
         /* Undo/Redo */
 
@@ -152,21 +154,21 @@
 
 @end
 
-FOUNDATION_EXPORT NSString * const NSUndoManagerCheckpointNotification NS_AVAILABLE(10_0, 3_0);
+FOUNDATION_EXPORT NSNotificationName const NSUndoManagerCheckpointNotification NS_AVAILABLE(10_0, 3_0);
     // This is called before an undo group is begun or ended so any
     // clients that need to lazily register undos can do so in the
     // correct group.
 
-FOUNDATION_EXPORT NSString * const NSUndoManagerWillUndoChangeNotification NS_AVAILABLE(10_0, 3_0);
-FOUNDATION_EXPORT NSString * const NSUndoManagerWillRedoChangeNotification NS_AVAILABLE(10_0, 3_0);
+FOUNDATION_EXPORT NSNotificationName const NSUndoManagerWillUndoChangeNotification NS_AVAILABLE(10_0, 3_0);
+FOUNDATION_EXPORT NSNotificationName const NSUndoManagerWillRedoChangeNotification NS_AVAILABLE(10_0, 3_0);
 
-FOUNDATION_EXPORT NSString * const NSUndoManagerDidUndoChangeNotification NS_AVAILABLE(10_0, 3_0);
-FOUNDATION_EXPORT NSString * const NSUndoManagerDidRedoChangeNotification NS_AVAILABLE(10_0, 3_0);
+FOUNDATION_EXPORT NSNotificationName const NSUndoManagerDidUndoChangeNotification NS_AVAILABLE(10_0, 3_0);
+FOUNDATION_EXPORT NSNotificationName const NSUndoManagerDidRedoChangeNotification NS_AVAILABLE(10_0, 3_0);
 
-FOUNDATION_EXPORT NSString * const NSUndoManagerDidOpenUndoGroupNotification NS_AVAILABLE(10_0, 3_0);
-FOUNDATION_EXPORT NSString * const NSUndoManagerWillCloseUndoGroupNotification NS_AVAILABLE(10_0, 3_0);
+FOUNDATION_EXPORT NSNotificationName const NSUndoManagerDidOpenUndoGroupNotification NS_AVAILABLE(10_0, 3_0);
+FOUNDATION_EXPORT NSNotificationName const NSUndoManagerWillCloseUndoGroupNotification NS_AVAILABLE(10_0, 3_0);
 
 // This notification is sent after an undo group closes. It should be safe to undo at this time.
-FOUNDATION_EXPORT NSString * const NSUndoManagerDidCloseUndoGroupNotification NS_AVAILABLE(10_7, 5_0);
+FOUNDATION_EXPORT NSNotificationName const NSUndoManagerDidCloseUndoGroupNotification NS_AVAILABLE(10_7, 5_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUnit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUnit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUnit.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUnit.h	2016-05-20 06:12:55.000000000 +0200
@@ -0,0 +1,485 @@
+/*
+ NSUnit.h
+ Copyright (c) 2015-2016, Apple Inc.
+ All rights reserved.
+ */
+
+#import <Foundation/NSObject.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+#pragma mark Unit Converters
+/*
+ NSUnitConverter describes how to convert a unit to and from the base unit of its dimension.  Use the NSUnitConverter protocol to implement new ways of converting a unit.
+ */
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitConverter : NSObject
+
+/*
+ The following methods perform conversions to and from the base unit of a unit class's dimension.  Each unit is defined against the base unit for the dimension to which the unit belongs.
+
+ These methods are implemented differently depending on the type of conversion.  The default implementation in NSUnitConverter simply returns the value.
+
+ These methods exist for the sole purpose of creating custom conversions for units in order to support converting a value from one kind of unit to another in the same dimension.  NSUnitConverter is an abstract class that is meant to be subclassed.  There is no need to call these methods directly to do a conversion -- the correct way to convert a measurement is to use [NSMeasurement measurementByConvertingToUnit:].  measurementByConvertingToUnit: uses the following 2 methods internally to perform the conversion.
+ 
+ When creating a custom unit converter, you must override these two methods to implement the conversion to and from a value in terms of a unit and the corresponding value in terms of the base unit of that unit's dimension in order for conversion to work correctly.
+ */
+
+/*
+ This method takes a value in terms of a unit and returns the corresponding value in terms of the base unit of the original unit's dimension.
+ @param value Value in terms of the unit class
+ @return Value in terms of the base unit
+ */
+- (double)baseUnitValueFromValue:(double)value;
+
+/*
+ This method takes in a value in terms of the base unit of a unit's dimension and returns the equivalent value in terms of the unit.
+ @param baseUnitValue Value in terms of the base unit
+ @return Value in terms of the unit class
+ */
+- (double)valueFromBaseUnitValue:(double)baseUnitValue;
+
+@end
+
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitConverterLinear : NSUnitConverter <NSSecureCoding> {
+@private
+    double _coefficient;
+    double _constant;
+}
+
+/*
+ For units that require linear conversion, the methods perform calculations in the form of y = ax + b, where
+    - x is the value in terms of the unit on which this method is called
+    - y is the value in terms of the base unit of the dimension
+    - a is the known coefficient used for this unit's conversion
+    - b is the known constant used for this unit's conversion
+
+ baseUnitValueFromValue: performs the conversion in the form of y = ax + b, where x represents the value passed in and y represents the value returned.
+ valueFromBaseUnitValue: performs the inverse conversion in the form of x = (y + (-1 * b))/a, where y represents the value passed in and x represents the value returned.
+
+ An example of this is NSUnitTemperature.  For Celsius, baseUnitValueFromValue: calculates the value in Kelvin using the formula
+            K = 1 * °C + 273.15
+ and valueFromBaseUnitValue: calculates the value in Celsius using the formula
+            C° = (K + (-1 * 273.15))/1
+ where the coefficient is 1 and the constant is 273.15.
+
+ For units that only require conversion by scale factor, the coefficient is the scale factor and the constant is always 0.  baseUnitValueFromValue: calculates the value in meters using the formula
+            valueInMeters = 1000 * valueInKilometers + 0
+ and valueFromBaseUnitValue: calculates the value in kilometers using the formula
+            valueInKilometers = valueInMeters / 1000
+ where the coefficient is 1000 and the constant is 0.  This API provides a convenience initializer initWithCoefficient: that assumes the constant is 0.
+ */
+@property (readonly) double coefficient;
+@property (readonly) double constant;
+
+- (instancetype)initWithCoefficient:(double)coefficient;
+
+- (instancetype)initWithCoefficient:(double)coefficient constant:(double)constant NS_DESIGNATED_INITIALIZER;
+
+@end
+
+
+#pragma mark Unit
+/*
+ NSUnit is the base class for all unit types (dimensional and dimensionless).
+ */
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnit : NSObject <NSCopying, NSSecureCoding> {
+@private
+    NSString *_symbol;
+}
+
+@property (readonly, copy) NSString *symbol;
+
+- (instancetype)initWithSymbol:(NSString *)symbol;
+
+@end
+
+
+#pragma mark Dimensions
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSDimension : NSUnit <NSSecureCoding> {
+@private
+    NSUInteger _reserved;
+@protected
+    NSUnitConverter *_converter;
+}
+
+@property (readonly, copy) NSUnitConverter *converter;
+
+- (instancetype)initWithSymbol:(NSString *)symbol converter:(NSUnitConverter *)converter NS_DESIGNATED_INITIALIZER;
+
+/*
+ This class method returns an instance of the dimension class that represents the base unit of that dimension.
+ e.g.
+    NSUnitSpeed *metersPerSecond = [NSUnitSpeed baseUnit];
+ */
++ (instancetype)baseUnit;
+
+@end
+
+
+#pragma mark - Predefined Dimensions
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitAcceleration : NSDimension <NSSecureCoding>
+/*
+ Base unit - metersPerSecondSquared
+ */
+
+@property (class, readonly, copy) NSUnitAcceleration *metersPerSecondSquared;
+@property (class, readonly, copy) NSUnitAcceleration *gravity;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitAngle : NSDimension <NSSecureCoding>
+/*
+ Base unit - degrees
+ */
+
+@property (class, readonly, copy) NSUnitAngle *degrees;
+@property (class, readonly, copy) NSUnitAngle *arcMinutes;
+@property (class, readonly, copy) NSUnitAngle *arcSeconds;
+@property (class, readonly, copy) NSUnitAngle *radians;
+@property (class, readonly, copy) NSUnitAngle *gradians;
+@property (class, readonly, copy) NSUnitAngle *revolutions;
+
+@property (class, readonly, copy) NSUnitAngle *degree API_DEPRECATED("No longer supported - use degrees instead", macosx(10.12, 10.12), ios(10.0, 10.0), watchos(3.0, 3.0), tvos(10.0, 10.0));
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitArea : NSDimension <NSSecureCoding>
+/*
+ Base unit - squareMeters
+ */
+
+@property (class, readonly, copy) NSUnitArea *squareMegameters;
+@property (class, readonly, copy) NSUnitArea *squareKilometers;
+@property (class, readonly, copy) NSUnitArea *squareMeters;
+@property (class, readonly, copy) NSUnitArea *squareCentimeters;
+@property (class, readonly, copy) NSUnitArea *squareMillimeters;
+@property (class, readonly, copy) NSUnitArea *squareMicrometers;
+@property (class, readonly, copy) NSUnitArea *squareNanometers;
+@property (class, readonly, copy) NSUnitArea *squareInches;
+@property (class, readonly, copy) NSUnitArea *squareFeet;
+@property (class, readonly, copy) NSUnitArea *squareYards;
+@property (class, readonly, copy) NSUnitArea *squareMiles;
+@property (class, readonly, copy) NSUnitArea *acres;
+@property (class, readonly, copy) NSUnitArea *ares;
+@property (class, readonly, copy) NSUnitArea *hectares;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitConcentrationMass : NSDimension <NSSecureCoding>
+/*
+ Base unit - gramsPerLiter
+ */
+
+@property (class, readonly, copy) NSUnitConcentrationMass *gramsPerLiter;
+@property (class, readonly, copy) NSUnitConcentrationMass *milligramsPerDeciliter;
+
++ (NSUnitConcentrationMass *)millimolesPerLiterWithGramsPerMole:(double)gramsPerMole;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitDispersion : NSDimension <NSSecureCoding>
+/*
+ Base unit - partsPerMillion
+ */
+@property (class, readonly, copy) NSUnitDispersion *partsPerMillion;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitDuration : NSDimension <NSSecureCoding>
+/*
+ Base unit - seconds
+ */
+
+@property (class, readonly, copy) NSUnitDuration *seconds;
+@property (class, readonly, copy) NSUnitDuration *minutes;
+@property (class, readonly, copy) NSUnitDuration *hours;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitElectricCharge : NSDimension <NSSecureCoding>
+/*
+ Base unit - coulombs
+ */
+
+@property (class, readonly, copy) NSUnitElectricCharge *coulombs;
+@property (class, readonly, copy) NSUnitElectricCharge *megaampereHours;
+@property (class, readonly, copy) NSUnitElectricCharge *kiloampereHours;
+@property (class, readonly, copy) NSUnitElectricCharge *ampereHours;
+@property (class, readonly, copy) NSUnitElectricCharge *milliampereHours;
+@property (class, readonly, copy) NSUnitElectricCharge *microampereHours;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitElectricCurrent : NSDimension <NSSecureCoding>
+/*
+ Base unit - amperes
+ */
+
+@property (class, readonly, copy) NSUnitElectricCurrent *megaamperes;
+@property (class, readonly, copy) NSUnitElectricCurrent *kiloamperes;
+@property (class, readonly, copy) NSUnitElectricCurrent *amperes;
+@property (class, readonly, copy) NSUnitElectricCurrent *milliamperes;
+@property (class, readonly, copy) NSUnitElectricCurrent *microamperes;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitElectricPotentialDifference : NSDimension <NSSecureCoding>
+/*
+ Base unit - volts
+ */
+
+@property (class, readonly, copy) NSUnitElectricPotentialDifference *megavolts;
+@property (class, readonly, copy) NSUnitElectricPotentialDifference *kilovolts;
+@property (class, readonly, copy) NSUnitElectricPotentialDifference *volts;
+@property (class, readonly, copy) NSUnitElectricPotentialDifference *millivolts;
+@property (class, readonly, copy) NSUnitElectricPotentialDifference *microvolts;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitElectricResistance : NSDimension <NSSecureCoding>
+/*
+ Base unit - ohms
+ */
+
+@property (class, readonly, copy) NSUnitElectricResistance *megaohms;
+@property (class, readonly, copy) NSUnitElectricResistance *kiloohms;
+@property (class, readonly, copy) NSUnitElectricResistance *ohms;
+@property (class, readonly, copy) NSUnitElectricResistance *milliohms;
+@property (class, readonly, copy) NSUnitElectricResistance *microohms;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitEnergy : NSDimension <NSSecureCoding>
+/*
+ Base unit - joules
+ */
+
+@property (class, readonly, copy) NSUnitEnergy *kilojoules;
+@property (class, readonly, copy) NSUnitEnergy *joules;
+@property (class, readonly, copy) NSUnitEnergy *kilocalories;
+@property (class, readonly, copy) NSUnitEnergy *calories;
+@property (class, readonly, copy) NSUnitEnergy *kilowattHours;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitFrequency : NSDimension <NSSecureCoding>
+/*
+ Base unit - hertz
+ */
+
+@property (class, readonly, copy) NSUnitFrequency *terahertz;
+@property (class, readonly, copy) NSUnitFrequency *gigahertz;
+@property (class, readonly, copy) NSUnitFrequency *megahertz;
+@property (class, readonly, copy) NSUnitFrequency *kilohertz;
+@property (class, readonly, copy) NSUnitFrequency *hertz;
+@property (class, readonly, copy) NSUnitFrequency *millihertz;
+@property (class, readonly, copy) NSUnitFrequency *microhertz;
+@property (class, readonly, copy) NSUnitFrequency *nanohertz;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitFuelEfficiency : NSDimension <NSSecureCoding>
+/*
+ Base unit - litersPer100Kilometers
+ */
+
+@property (class, readonly, copy) NSUnitFuelEfficiency *litersPer100Kilometers;
+@property (class, readonly, copy) NSUnitFuelEfficiency *milesPerImperialGallon;
+@property (class, readonly, copy) NSUnitFuelEfficiency *milesPerGallon;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitLength : NSDimension <NSSecureCoding>
+/*
+ Base unit - meters
+ */
+
+@property (class, readonly, copy) NSUnitLength *megameters;
+@property (class, readonly, copy) NSUnitLength *kilometers;
+@property (class, readonly, copy) NSUnitLength *hectometers;
+@property (class, readonly, copy) NSUnitLength *decameters;
+@property (class, readonly, copy) NSUnitLength *meters;
+@property (class, readonly, copy) NSUnitLength *decimeters;
+@property (class, readonly, copy) NSUnitLength *centimeters;
+@property (class, readonly, copy) NSUnitLength *millimeters;
+@property (class, readonly, copy) NSUnitLength *micrometers;
+@property (class, readonly, copy) NSUnitLength *nanometers;
+@property (class, readonly, copy) NSUnitLength *picometers;
+@property (class, readonly, copy) NSUnitLength *inches;
+@property (class, readonly, copy) NSUnitLength *feet;
+@property (class, readonly, copy) NSUnitLength *yards;
+@property (class, readonly, copy) NSUnitLength *miles;
+@property (class, readonly, copy) NSUnitLength *scandinavianMiles;
+@property (class, readonly, copy) NSUnitLength *lightyears;
+@property (class, readonly, copy) NSUnitLength *nauticalMiles;
+@property (class, readonly, copy) NSUnitLength *fathoms;
+@property (class, readonly, copy) NSUnitLength *furlongs;
+@property (class, readonly, copy) NSUnitLength *astronomicalUnits;
+@property (class, readonly, copy) NSUnitLength *parsecs;
+
+@property (class, readonly, copy) NSUnitLength *meter API_DEPRECATED("No longer supported - use meters instead", macosx(10.12, 10.12), ios(10.0, 10.0), watchos(3.0, 3.0), tvos(10.0, 10.0));
+@property (class, readonly, copy) NSUnitLength *foot API_DEPRECATED("No longer supported - use feet instead", macosx(10.12, 10.12), ios(10.0, 10.0), watchos(3.0, 3.0), tvos(10.0, 10.0));
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitIlluminance : NSDimension <NSSecureCoding>
+/*
+ Base unit - lux
+ */
+
+@property (class, readonly, copy) NSUnitIlluminance *lux;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitMass : NSDimension <NSSecureCoding>
+/*
+ Base unit - kilograms
+ */
+
+@property (class, readonly, copy) NSUnitMass *kilograms;
+@property (class, readonly, copy) NSUnitMass *grams;
+@property (class, readonly, copy) NSUnitMass *decigrams;
+@property (class, readonly, copy) NSUnitMass *centigrams;
+@property (class, readonly, copy) NSUnitMass *milligrams;
+@property (class, readonly, copy) NSUnitMass *micrograms;
+@property (class, readonly, copy) NSUnitMass *nanograms;
+@property (class, readonly, copy) NSUnitMass *picograms;
+@property (class, readonly, copy) NSUnitMass *ounces;
+@property (class, readonly, copy) NSUnitMass *poundsMass;
+@property (class, readonly, copy) NSUnitMass *stones;
+@property (class, readonly, copy) NSUnitMass *metricTons;
+@property (class, readonly, copy) NSUnitMass *shortTons;
+@property (class, readonly, copy) NSUnitMass *carats;
+@property (class, readonly, copy) NSUnitMass *ouncesTroy;
+@property (class, readonly, copy) NSUnitMass *slugs;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitPower : NSDimension <NSSecureCoding>
+/*
+ Base unit - watts
+ */
+
+@property (class, readonly, copy) NSUnitPower *terawatts;
+@property (class, readonly, copy) NSUnitPower *gigawatts;
+@property (class, readonly, copy) NSUnitPower *megawatts;
+@property (class, readonly, copy) NSUnitPower *kilowatts;
+@property (class, readonly, copy) NSUnitPower *watts;
+@property (class, readonly, copy) NSUnitPower *milliwatts;
+@property (class, readonly, copy) NSUnitPower *microwatts;
+@property (class, readonly, copy) NSUnitPower *nanowatts;
+@property (class, readonly, copy) NSUnitPower *picowatts;
+@property (class, readonly, copy) NSUnitPower *femtowatts;
+@property (class, readonly, copy) NSUnitPower *horsepower;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitPressure : NSDimension <NSSecureCoding>
+/*
+ Base unit - newtonsPerMetersSquared (equivalent to 1 pascal)
+ */
+
+@property (class, readonly, copy) NSUnitPressure *newtonsPerMetersSquared;
+@property (class, readonly, copy) NSUnitPressure *gigapascals;
+@property (class, readonly, copy) NSUnitPressure *megapascals;
+@property (class, readonly, copy) NSUnitPressure *kilopascals;
+@property (class, readonly, copy) NSUnitPressure *hectopascals;
+@property (class, readonly, copy) NSUnitPressure *inchesOfMercury;
+@property (class, readonly, copy) NSUnitPressure *bars;
+@property (class, readonly, copy) NSUnitPressure *millibars;
+@property (class, readonly, copy) NSUnitPressure *millimetersOfMercury;
+@property (class, readonly, copy) NSUnitPressure *poundsForcePerSquareInch;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitSpeed : NSDimension <NSSecureCoding>
+/*
+ Base unit - metersPerSecond
+ */
+
+@property (class, readonly, copy) NSUnitSpeed *metersPerSecond;
+@property (class, readonly, copy) NSUnitSpeed *kilometersPerHour;
+@property (class, readonly, copy) NSUnitSpeed *milesPerHour;
+@property (class, readonly, copy) NSUnitSpeed *knots;
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitTemperature : NSDimension <NSSecureCoding>
+/*
+ Base unit - kelvin
+ */
+@property (class, readonly, copy) NSUnitTemperature *kelvin;
+@property (class, readonly, copy) NSUnitTemperature *celsius; 
+@property (class, readonly, copy) NSUnitTemperature *fahrenheit;
+
+
+@end
+
+API_AVAILABLE(macosx(10.12), ios(10.0), watchos(3.0), tvos(10.0))
+@interface NSUnitVolume : NSDimension <NSSecureCoding>
+/*
+ Base unit - liters
+ */
+
+@property (class, readonly, copy) NSUnitVolume *megaliters;
+@property (class, readonly, copy) NSUnitVolume *kiloliters;
+@property (class, readonly, copy) NSUnitVolume *liters;
+@property (class, readonly, copy) NSUnitVolume *deciliters;
+@property (class, readonly, copy) NSUnitVolume *centiliters;
+@property (class, readonly, copy) NSUnitVolume *milliliters;
+@property (class, readonly, copy) NSUnitVolume *cubicKilometers;
+@property (class, readonly, copy) NSUnitVolume *cubicMeters;
+@property (class, readonly, copy) NSUnitVolume *cubicDecimeters;
+@property (class, readonly, copy) NSUnitVolume *cubicCentimeters;
+@property (class, readonly, copy) NSUnitVolume *cubicMillimeters;
+@property (class, readonly, copy) NSUnitVolume *cubicInches;
+@property (class, readonly, copy) NSUnitVolume *cubicFeet;
+@property (class, readonly, copy) NSUnitVolume *cubicYards;
+@property (class, readonly, copy) NSUnitVolume *cubicMiles;
+@property (class, readonly, copy) NSUnitVolume *acreFeet;
+@property (class, readonly, copy) NSUnitVolume *bushels;
+@property (class, readonly, copy) NSUnitVolume *teaspoons;
+@property (class, readonly, copy) NSUnitVolume *tablespoons;
+@property (class, readonly, copy) NSUnitVolume *fluidOunces;
+@property (class, readonly, copy) NSUnitVolume *cups;
+@property (class, readonly, copy) NSUnitVolume *pints;
+@property (class, readonly, copy) NSUnitVolume *quarts;
+@property (class, readonly, copy) NSUnitVolume *gallons;
+@property (class, readonly, copy) NSUnitVolume *imperialTeaspoons;
+@property (class, readonly, copy) NSUnitVolume *imperialTablespoons;
+@property (class, readonly, copy) NSUnitVolume *imperialFluidOunces;
+@property (class, readonly, copy) NSUnitVolume *imperialPints;
+@property (class, readonly, copy) NSUnitVolume *imperialQuarts;
+@property (class, readonly, copy) NSUnitVolume *imperialGallons;
+@property (class, readonly, copy) NSUnitVolume *metricCups;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserActivity.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserActivity.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserActivity.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserActivity.h	2016-05-20 06:25:33.000000000 +0200
@@ -78,7 +78,7 @@
 
 /* When an app is launched for a continuation event it can request streams back to the originating side. Streams can only be successfully retrieved from the NSUserActivity in the NS/UIApplication delegate that is called for a continuation event. This functionality is optional and is not expected to be needed in most continuation cases. The streams returned in the completion handler will be in an unopened state. The streams should be opened immediately to start requesting information from the other side.
 */
-- (void)getContinuationStreamsWithCompletionHandler:(void (^)(NSInputStream * __nullable inputStream, NSOutputStream * __nullable outputStream, NSError * __nullable error))completionHandler;
+- (void)getContinuationStreamsWithCompletionHandler:(void (^)(NSInputStream * _Nullable inputStream, NSOutputStream * _Nullable outputStream, NSError * _Nullable error))completionHandler;
 
 /* Set to YES if this user activity should be eligible to be handed off to another device */
 @property (getter=isEligibleForHandoff) BOOL eligibleForHandoff NS_AVAILABLE(10_11, 9_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserDefaults.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserDefaults.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserDefaults.h	2016-02-20 01:49:18.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserDefaults.h	2016-05-20 06:13:48.000000000 +0200
@@ -3,6 +3,7 @@
  */
 
 #import <Foundation/NSObject.h>
+#import <Foundation/NSNotification.h>
 
 @class NSArray<ObjectType>, NSData, NSDictionary<KeyValue, ObjectValue>, NSMutableDictionary, NSString, NSURL;
 
@@ -184,22 +185,29 @@
 /*!
  NSUserDefaultsSizeLimitExceededNotification is posted on the main queue when more data is stored in user defaults than is allowed. Currently there is no limit for local user defaults except on tvOS, where a warning notification will be posted at 512kB, and the process terminated at 1MB. For ubiquitous defaults, the limit depends on the logged in iCloud user.
  */
-FOUNDATION_EXPORT NSString * const NSUserDefaultsSizeLimitExceededNotification NS_AVAILABLE_IOS(9_3);
+FOUNDATION_EXPORT NSNotificationName const NSUserDefaultsSizeLimitExceededNotification NS_AVAILABLE_IOS(9_3);
+
+/*!
+ NSUbiquitousUserDefaultsNoCloudAccountNotification is posted on the main queue to the default notification center when a cloud default is set, but no iCloud user is logged in.
+ 
+ This is not necessarily an error: ubiquitous defaults set when no iCloud user is logged in will be uploaded the next time one is available if configured to do so.
+ */
+FOUNDATION_EXPORT NSNotificationName const NSUbiquitousUserDefaultsNoCloudAccountNotification NS_AVAILABLE_IOS(9_3);
 
 /*!
  NSUbiquitousUserDefaultsDidChangeAccountsNotification is posted on the main queue to the default notification center when the user changes the primary iCloud account. The keys and values in the local key-value store have been replaced with those from the new account, regardless of the relative timestamps.
  */
-FOUNDATION_EXPORT NSString * const NSUbiquitousUserDefaultsDidChangeAccountsNotification NS_AVAILABLE_IOS(9_3);
+FOUNDATION_EXPORT NSNotificationName const NSUbiquitousUserDefaultsDidChangeAccountsNotification NS_AVAILABLE_IOS(9_3);
 
 /*!
  NSUbiquitousUserDefaultsCompletedInitialSyncNotification is posted on the main queue when ubiquitous defaults finish downloading the first time a device is connected to an iCloud account, and when a user switches their primary iCloud account.
  */
-FOUNDATION_EXPORT NSString * const NSUbiquitousUserDefaultsCompletedInitialSyncNotification NS_AVAILABLE_IOS(9_3);
+FOUNDATION_EXPORT NSNotificationName const NSUbiquitousUserDefaultsCompletedInitialSyncNotification NS_AVAILABLE_IOS(9_3);
 
 /*!
  NSUserDefaultsDidChangeNotification is posted whenever any user defaults changed within the current process, but is not posted when ubiquitous defaults change, or when an outside process changes defaults. Using key-value observing to register observers for the specific keys of interest will inform you of all updates, regardless of where they're from.
  */
-FOUNDATION_EXPORT NSString * const NSUserDefaultsDidChangeNotification;
+FOUNDATION_EXPORT NSNotificationName const NSUserDefaultsDidChangeNotification;
 
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE)) || TARGET_OS_WIN32
 /* The following keys and their values are deprecated in Mac OS X 10.5 "Leopard". Developers should use NSLocale, NSDateFormatter and NSNumberFormatter to retrieve the values formerly returned by these keys.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSValueTransformer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSValueTransformer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSValueTransformer.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSValueTransformer.h	2016-05-20 06:24:14.000000000 +0200
@@ -8,11 +8,13 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-FOUNDATION_EXPORT NSString * const NSNegateBooleanTransformerName	NS_AVAILABLE(10_3, 3_0);
-FOUNDATION_EXPORT NSString * const NSIsNilTransformerName		NS_AVAILABLE(10_3, 3_0);
-FOUNDATION_EXPORT NSString * const NSIsNotNilTransformerName		NS_AVAILABLE(10_3, 3_0);
-FOUNDATION_EXPORT NSString * const NSUnarchiveFromDataTransformerName	NS_AVAILABLE(10_3, 3_0);
-FOUNDATION_EXPORT NSString * const NSKeyedUnarchiveFromDataTransformerName	NS_AVAILABLE(10_5, 3_0);
+typedef NSString *NSValueTransformerName NS_EXTENSIBLE_STRING_ENUM;
+
+FOUNDATION_EXPORT NSValueTransformerName const NSNegateBooleanTransformerName	NS_AVAILABLE(10_3, 3_0);
+FOUNDATION_EXPORT NSValueTransformerName const NSIsNilTransformerName		NS_AVAILABLE(10_3, 3_0);
+FOUNDATION_EXPORT NSValueTransformerName const NSIsNotNilTransformerName		NS_AVAILABLE(10_3, 3_0);
+FOUNDATION_EXPORT NSValueTransformerName const NSUnarchiveFromDataTransformerName	NS_AVAILABLE(10_3, 3_0);
+FOUNDATION_EXPORT NSValueTransformerName const NSKeyedUnarchiveFromDataTransformerName	NS_AVAILABLE(10_5, 3_0);
 
 NS_CLASS_AVAILABLE(10_3, 3_0)
 @interface NSValueTransformer : NSObject {
@@ -20,9 +22,9 @@
 
 // name-based registry for shared objects (especially used when loading nib files with transformers specified by name in Interface Builder) - also useful for localization (developers can register different kind of transformers or differently configured transformers at application startup and refer to them by name from within nib files or other code)
 // if valueTransformerForName: does not find a registered transformer instance, it will fall back to looking up a class with the specified name - if one is found, it will instantiate a transformer with the default -init method and automatically register it
-+ (void)setValueTransformer:(nullable NSValueTransformer *)transformer forName:(NSString *)name;
-+ (nullable NSValueTransformer *)valueTransformerForName:(NSString *)name;
-+ (NSArray<NSString *> *)valueTransformerNames;
++ (void)setValueTransformer:(nullable NSValueTransformer *)transformer forName:(NSValueTransformerName)name;
++ (nullable NSValueTransformer *)valueTransformerForName:(NSValueTransformerName)name;
++ (NSArray<NSValueTransformerName> *)valueTransformerNames;
 
 // information that can be used to analyze available transformer instances (especially used inside Interface Builder)
 + (Class)transformedValueClass;    // class of the "output" objects, as returned by transformedValue:
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSXMLParser.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSXMLParser.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSXMLParser.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSXMLParser.h	2016-05-20 07:35:40.000000000 +0200
@@ -3,6 +3,7 @@
 */
 
 #import <Foundation/NSObject.h>
+#import <Foundation/NSError.h>
 
 @class NSData, NSDictionary<KeyType, ObjectType>, NSError, NSString, NSURL, NSInputStream, NSSet<ObjectType>;
 @protocol NSXMLParserDelegate;
@@ -143,7 +144,7 @@
     // If validation is on, this will report a fatal validation error to the delegate. The parser will stop parsing.
 @end
 
-FOUNDATION_EXPORT NSString * const NSXMLParserErrorDomain	NS_AVAILABLE(10_3, 2_0);  // for use with NSError.
+FOUNDATION_EXPORT NSErrorDomain const NSXMLParserErrorDomain	NS_AVAILABLE(10_3, 2_0);  // for use with NSError.
 
 // Error reporting
 typedef NS_ENUM(NSInteger, NSXMLParserError) {
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSZone.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSZone.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSZone.h	2015-08-11 04:24:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSZone.h	2016-05-20 06:24:14.000000000 +0200
@@ -15,29 +15,26 @@
 FOUNDATION_EXPORT NSZone *NSCreateZone(NSUInteger startSize, NSUInteger granularity, BOOL canFree) NS_SWIFT_UNAVAILABLE("Zone-based memory management is unavailable");
 FOUNDATION_EXPORT void NSRecycleZone(NSZone *zone)NS_SWIFT_UNAVAILABLE("Zone-based memory management is unavailable");
 
-FOUNDATION_EXPORT void NSSetZoneName(NSZone * __nullable zone, NSString *name)NS_SWIFT_UNAVAILABLE("Zone-based memory management is unavailable");
-FOUNDATION_EXPORT NSString *NSZoneName(NSZone * __nullable zone) NS_SWIFT_UNAVAILABLE("Zone-based memory management is unavailable");
-FOUNDATION_EXPORT NSZone * __nullable NSZoneFromPointer(void *ptr) NS_SWIFT_UNAVAILABLE("Zone-based memory management is unavailable");
-
-FOUNDATION_EXPORT void *NSZoneMalloc(NSZone * __nullable zone, NSUInteger size) NS_SWIFT_UNAVAILABLE("Zone-based memory management is unavailable");
-FOUNDATION_EXPORT void *NSZoneCalloc(NSZone * __nullable zone, NSUInteger numElems, NSUInteger byteSize) NS_SWIFT_UNAVAILABLE("Zone-based memory management is unavailable");
-FOUNDATION_EXPORT void *NSZoneRealloc(NSZone * __nullable zone, void * __nullable ptr, NSUInteger size) NS_SWIFT_UNAVAILABLE("Zone-based memory management is unavailable");
-FOUNDATION_EXPORT void NSZoneFree(NSZone * __nullable zone, void *ptr) NS_SWIFT_UNAVAILABLE("Zone-based memory management is unavailable");
+FOUNDATION_EXPORT void NSSetZoneName(NSZone * _Nullable zone, NSString *name)NS_SWIFT_UNAVAILABLE("Zone-based memory management is unavailable");
+FOUNDATION_EXPORT NSString *NSZoneName(NSZone * _Nullable zone) NS_SWIFT_UNAVAILABLE("Zone-based memory management is unavailable");
+FOUNDATION_EXPORT NSZone * _Nullable NSZoneFromPointer(void *ptr) NS_SWIFT_UNAVAILABLE("Zone-based memory management is unavailable");
+
+FOUNDATION_EXPORT void *NSZoneMalloc(NSZone * _Nullable zone, NSUInteger size) NS_SWIFT_UNAVAILABLE("Zone-based memory management is unavailable");
+FOUNDATION_EXPORT void *NSZoneCalloc(NSZone * _Nullable zone, NSUInteger numElems, NSUInteger byteSize) NS_SWIFT_UNAVAILABLE("Zone-based memory management is unavailable");
+FOUNDATION_EXPORT void *NSZoneRealloc(NSZone * _Nullable zone, void * _Nullable ptr, NSUInteger size) NS_SWIFT_UNAVAILABLE("Zone-based memory management is unavailable");
+FOUNDATION_EXPORT void NSZoneFree(NSZone * _Nullable zone, void *ptr) NS_SWIFT_UNAVAILABLE("Zone-based memory management is unavailable");
 
 #if (TARGET_OS_MAC && !(TARGET_OS_EMBEDDED || TARGET_OS_IPHONE))
 
-/* Garbage Collected memory allocation.
-   Raw memory may be directly allocated (and "realloc"ed) from the collector. The default unscanned memory returned by this call should not be used to hold live pointers to garbage collected memory.  Use the scanned option.  Further, the pointer type of the stored location must be marked with the __strong attribute in order for the write-barrier assignment primitive to be generated.  
-   The NSCollectorDisabledOption provides an allocation for use as an external reference.
-*/
+/* Garbage Collected memory allocation. Garbage Collection is deprecated. */
 
 NS_ENUM(NSUInteger) {
     NSScannedOption = (1UL << 0),
     NSCollectorDisabledOption = (1UL << 1),
 };
 
-FOUNDATION_EXPORT void *__strong NSAllocateCollectable(NSUInteger size, NSUInteger options) NS_SWIFT_UNAVAILABLE("Garbage Collection is not supported");
-FOUNDATION_EXPORT void *__strong NSReallocateCollectable(void * __nullable ptr, NSUInteger size, NSUInteger options) NS_SWIFT_UNAVAILABLE("Garbage Collection is not supported");
+FOUNDATION_EXPORT void *NSAllocateCollectable(NSUInteger size, NSUInteger options) NS_SWIFT_UNAVAILABLE("Garbage Collection is not supported");
+FOUNDATION_EXPORT void *NSReallocateCollectable(void * _Nullable ptr, NSUInteger size, NSUInteger options) NS_SWIFT_UNAVAILABLE("Garbage Collection is not supported");
 
 #endif
 
@@ -54,12 +51,12 @@
  CFTypeRef style objects are garbage collected, yet only sometime after the last CFRelease() is performed.  Particulary for fully-bridged CFTypeRef objects such as CFStrings and collections (CFDictionaryRef et alia) it is imperative that either CFMakeCollectable or the more type safe NSMakeCollectable be performed, preferably right upon allocation.  Conceptually, this moves them from a "C" style opaque pointer into an "id" style object.
  This function is unavailable in ARC mode. Use CFBridgingRelease instead.
 */
-NS_INLINE NS_RETURNS_RETAINED id __nullable NSMakeCollectable(CFTypeRef __nullable CF_CONSUMED cf) NS_AUTOMATED_REFCOUNT_UNAVAILABLE NS_SWIFT_UNAVAILABLE("Garbage Collection is not supported");
-NS_INLINE NS_RETURNS_RETAINED id __nullable NSMakeCollectable(CFTypeRef __nullable CF_CONSUMED cf) {
+NS_INLINE NS_RETURNS_RETAINED id _Nullable NSMakeCollectable(CFTypeRef _Nullable CF_CONSUMED cf) NS_AUTOMATED_REFCOUNT_UNAVAILABLE NS_SWIFT_UNAVAILABLE("Garbage Collection is not supported");
+NS_INLINE NS_RETURNS_RETAINED id _Nullable NSMakeCollectable(CFTypeRef _Nullable CF_CONSUMED cf) {
 #if __has_feature(objc_arc)
     return nil;
 #else
-    return (cf ? (id)CFMakeCollectable(cf) : nil);
+    return (id)cf;
 #endif
 }
 

```