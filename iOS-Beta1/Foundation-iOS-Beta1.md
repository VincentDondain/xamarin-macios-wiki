#Foundation.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/Foundation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/Foundation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/Foundation.h	2015-10-02 23:32:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/Foundation.h	2016-05-20 07:24:14.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSArray.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSArray.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSArray.h	2015-10-02 23:32:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSArray.h	2016-05-20 07:39:55.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDictionary.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDictionary.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDictionary.h	2015-10-02 23:32:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSDictionary.h	2016-05-20 06:12:55.000000000 +0200
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

diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSIndexSet.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSIndexSet.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSIndexSet.h	2015-10-02 23:32:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSIndexSet.h	2016-05-20 06:12:55.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyedArchiver.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyedArchiver.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyedArchiver.h	2015-10-02 23:32:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSKeyedArchiver.h	2016-05-20 07:39:55.000000000 +0200
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
@@ -126,6 +133,8 @@
 // Enables secure coding support on this keyed unarchiver. When enabled, anarchiving a disallowed class throws an exception. Once enabled, attempting to set requiresSecureCoding to NO will throw an exception. This is to prevent classes from selectively turning secure coding off. This is designed to be set once at the top level and remain on. Note that the getter is on the superclass, NSCoder. See NSCoder for more information about secure coding.
 @property (readwrite) BOOL requiresSecureCoding NS_AVAILABLE(10_8, 6_0);
 
+@property (readwrite) NSDecodingFailurePolicy decodingFailurePolicy NS_AVAILABLE(10_11, 9_0);
+
 @end
 
 @protocol NSKeyedArchiverDelegate <NSObject>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLinguisticTagger.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLinguisticTagger.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLinguisticTagger.h	2015-10-02 23:32:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLinguisticTagger.h	2016-05-20 06:13:48.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLocale.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLocale.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLocale.h	2015-10-02 23:32:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSLocale.h	2016-05-20 07:35:40.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOrderedSet.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOrderedSet.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOrderedSet.h	2015-10-02 23:32:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSOrderedSet.h	2016-05-20 07:35:40.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPathUtilities.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPathUtilities.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPathUtilities.h	2015-10-02 23:32:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPathUtilities.h	2016-05-20 07:24:14.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPersonNameComponentsFormatter.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPersonNameComponentsFormatter.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPersonNameComponentsFormatter.h	2015-10-02 23:32:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPersonNameComponentsFormatter.h	2016-05-20 07:35:40.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPredicate.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPredicate.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPredicate.h	2015-10-02 23:32:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSPredicate.h	2016-05-20 07:35:40.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProcessInfo.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProcessInfo.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProcessInfo.h	2015-10-02 23:32:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSProcessInfo.h	2016-05-20 07:24:14.000000000 +0200
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
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURL.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURL.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURL.h	2015-10-02 23:32:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURL.h	2016-05-20 06:24:14.000000000 +0200
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
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLSession.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLSession.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLSession.h	2016-02-20 01:49:18.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSURLSession.h	2016-05-20 07:39:55.000000000 +0200
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
@@ -817,4 +825,173 @@
 + (NSURLSessionConfiguration *)backgroundSessionConfiguration:(NSString *)identifier NS_DEPRECATED(NSURLSESSION_AVAILABLE, 10_10, 7_0, 8_0, "Please use backgroundSessionConfigurationWithIdentifier: instead");
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserDefaults.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserDefaults.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserDefaults.h	2016-02-20 01:49:18.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSUserDefaults.h	2016-05-20 06:13:48.000000000 +0200
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
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSZone.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSZone.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSZone.h	2015-10-02 23:32:35.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSZone.h	2016-05-20 07:35:40.000000000 +0200
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
 
 
```