#HealthKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKAnchoredObjectQuery.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKAnchoredObjectQuery.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKAnchoredObjectQuery.h	2016-06-05 05:29:10.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKAnchoredObjectQuery.h	2016-06-27 07:58:05.000000000 +0200
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
```