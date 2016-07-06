#HealthKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKActivitySummaryQuery.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKActivitySummaryQuery.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKActivitySummaryQuery.h	2016-06-05 05:29:10.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKActivitySummaryQuery.h	2016-06-27 07:58:05.000000000 +0200
@@ -30,8 +30,8 @@
                  Otherwise, the query continues to run and calls the updateHandler as HKActivitySummaries matching the
                  predicate are updated.
   
-  @param         predicate       The predicate which HKActivitySummaries should match.
-  @param         resultsHandler  The block to invoke with results when the query has finished.
+  @param         predicate  The predicate which HKActivitySummaries should match.
+  @param         handler    The block to invoke with results when the query has finished.
   */
 - (instancetype)initWithPredicate:(nullable NSPredicate *)predicate
                    resultsHandler:(void(^)(HKActivitySummaryQuery *query, NSArray<HKActivitySummary *> * _Nullable activitySummaries, NSError * _Nullable error))handler;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKAnchoredObjectQuery.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKAnchoredObjectQuery.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKAnchoredObjectQuery.h	2016-06-05 05:29:10.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKAnchoredObjectQuery.h	2016-06-27 07:58:05.000000000 +0200
@@ -60,7 +60,7 @@
                                 handler.  Pass nil when querying for the first time.
  @param         limit           The maximum number of samples and deleted objects to return.  Pass HKObjectQueryNoLimit
                                 for no limit.
- @param         resultsHandler  The block to invoke with results when the query has finished finding.
+ @param         handler         The block to invoke with results when the query has finished finding.
  */
 - (instancetype)initWithType:(HKSampleType *)type
                    predicate:(nullable NSPredicate *)predicate
@@ -68,6 +68,12 @@
                        limit:(NSUInteger)limit
               resultsHandler:(void(^)(HKAnchoredObjectQuery *query, NSArray<__kindof HKSample *> * _Nullable sampleObjects, NSArray<HKDeletedObject *> * _Nullable deletedObjects, HKQueryAnchor * _Nullable newAnchor, NSError * _Nullable error))handler HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
+- (instancetype)initWithType:(HKSampleType *)type
+                   predicate:(nullable NSPredicate *)predicate
+                      anchor:(NSUInteger)anchor
+                       limit:(NSUInteger)limit
+           completionHandler:(void(^)(HKAnchoredObjectQuery *query, NSArray<__kindof HKSample *> * __nullable results, NSUInteger newAnchor, NSError * __nullable error))handler NS_DEPRECATED_IOS(8_0, 9_0, "Use initWithType:predicate:anchor:limit:resultsHandler:");
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCorrelation.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCorrelation.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCorrelation.h	2016-06-05 05:29:10.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCorrelation.h	2016-06-27 07:58:05.000000000 +0200
@@ -56,11 +56,11 @@
 /*!
  @method        correlationWithType:startDate:endDate:objects:device:metadata:
  @abstract      Creates a new HKCorrelation with the given type, start date, end date, objects, and metadata.
- @param         type        The correlation type of the objects set.
- @param         startDate   The start date of the correlation.
- @param         endDate     The end date of the correlation.
- @param         device      The HKDevice that generated the samples (optional).
- @param         metadata    Metadata for the correlation (optional).
+ @param         correlationType The correlation type of the objects set.
+ @param         startDate       The start date of the correlation.
+ @param         endDate         The end date of the correlation.
+ @param         device          The HKDevice that generated the samples (optional).
+ @param         metadata        Metadata for the correlation (optional).
  @discussion    objects must be a set of HKQuantitySamples and HKCategorySamples
  */
 + (instancetype)correlationWithType:(HKCorrelationType *)correlationType
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuantitySample.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuantitySample.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuantitySample.h	2016-06-05 05:29:10.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuantitySample.h	2016-06-27 07:58:05.000000000 +0200
@@ -48,11 +48,11 @@
 /*!
  @method        quantitySampleWithType:quantity:startDate:endDate:device:metadata:
  @abstract      Creates a new HKQuantitySample with the given type, quantity, start date, end date, and metadata.
- @param         type        The type of the sample.
- @param         startDate   The start date of the sample.
- @param         endDate     The end date of the sample.
- @param         device      The HKDevice that generated the sample (optional).
- @param         metadata    Metadata for the sample (optional).
+ @param         quantityType    The type of the sample.
+ @param         startDate       The start date of the sample.
+ @param         endDate         The end date of the sample.
+ @param         device          The HKDevice that generated the sample (optional).
+ @param         metadata        Metadata for the sample (optional).
  @discussion    The quantity must have a unit that is compatible with the given quantity type.
                 See -[HKQuantityType isCompatibleWithUnit:].
  */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSourceQuery.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSourceQuery.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSourceQuery.h	2016-06-05 05:29:10.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSourceQuery.h	2016-06-27 07:58:05.000000000 +0200
@@ -22,7 +22,7 @@
                 given predicate.
  
  @param         sampleType          The type of sample.
- @param         samplePredicate     The predicate which samples must match.
+ @param         objectPredicate     The predicate which samples must match.
  @param         completionHandler   The block to be called when the query has finished executing.
  */
 - (instancetype)initWithSampleType:(HKSampleType *)sampleType

```