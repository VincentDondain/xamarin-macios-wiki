#HealthKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKActivitySummaryQuery.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKActivitySummaryQuery.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKActivitySummaryQuery.h	2016-02-23 04:42:22.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKActivitySummaryQuery.h	2016-06-05 05:29:10.000000000 +0200
@@ -21,19 +21,20 @@
   @discussion    This property may not be modified once the query has been executed. If this property is nonnull, then
                  the query must be manually stopped.
   */
-@property (nonatomic, copy, nullable) void(^updateHandler)(HKActivitySummaryQuery *query, NSArray<HKActivitySummary *> * __nullable updatedActivitySummaries, NSError * __nullable error);
+@property (nonatomic, copy, nullable) void(^updateHandler)(HKActivitySummaryQuery *query, NSArray<HKActivitySummary *> * _Nullable updatedActivitySummaries, NSError * _Nullable error);
 
 /*!
   @method        initWithPredicate:resultsHandler:
   @abstract      Returns a query that will retrieve HKActivitySummaries matching the given predicate.
   @discussion    If no updateHandler is set on the query, the query will automatically stop after calling resultsHandler.
-                 Otherwise, the query continues to run and calls the updateHandler as HKActivitySummaries matching the predicate are updated.
+                 Otherwise, the query continues to run and calls the updateHandler as HKActivitySummaries matching the
+                 predicate are updated.
   
   @param         predicate       The predicate which HKActivitySummaries should match.
   @param         resultsHandler  The block to invoke with results when the query has finished.
   */
 - (instancetype)initWithPredicate:(nullable NSPredicate *)predicate
-                   resultsHandler:(void(^)(HKActivitySummaryQuery *query, NSArray<HKActivitySummary *> * __nullable activitySummaries, NSError * __nullable error))handler;
+                   resultsHandler:(void(^)(HKActivitySummaryQuery *query, NSArray<HKActivitySummary *> * _Nullable activitySummaries, NSError * _Nullable error))handler;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKAnchoredObjectQuery.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKAnchoredObjectQuery.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKAnchoredObjectQuery.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKAnchoredObjectQuery.h	2016-06-05 05:29:10.000000000 +0200
@@ -17,7 +17,7 @@
  @class         HKQueryAnchor
  @discussion    This object encapsulates the state of an HKAnchoredObjectQuery
  */
-HK_CLASS_AVAILABLE_IOS(9_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(9_0, 2_0)
 @interface HKQueryAnchor : NSObject <NSSecureCoding, NSCopying>
 
 /*!
@@ -35,7 +35,7 @@
  @discussion    This query can be used by an application to find out about new or deleted samples in the HealthKit
                 database.
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKAnchoredObjectQuery : HKQuery
 
 /*!
@@ -44,13 +44,7 @@
  @discussion    This property may not be modified once the query has been executed.  It may only be set if the query has
                 no limit.
  */
-@property (nonatomic, copy, nullable) void(^updateHandler)(HKAnchoredObjectQuery *query, NSArray<__kindof HKSample *> * __nullable addedObjects, NSArray<HKDeletedObject *> * __nullable deletedObjects, HKQueryAnchor * __nullable newAnchor, NSError * __nullable error) NS_AVAILABLE_IOS(9_0);
-
-- (instancetype)initWithType:(HKSampleType *)type
-                   predicate:(nullable NSPredicate *)predicate
-                      anchor:(NSUInteger)anchor
-                       limit:(NSUInteger)limit
-           completionHandler:(void(^)(HKAnchoredObjectQuery *query, NSArray<__kindof HKSample *> * __nullable results, NSUInteger newAnchor, NSError * __nullable error))handler NS_DEPRECATED_IOS(8_0, 9_0);
+@property (nonatomic, copy, nullable) void(^updateHandler)(HKAnchoredObjectQuery *query, NSArray<__kindof HKSample *> * _Nullable addedObjects, NSArray<HKDeletedObject *> * _Nullable deletedObjects, HKQueryAnchor * _Nullable newAnchor, NSError * _Nullable error) HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @method        initWithType:predicate:anchor:limit:resultsHandler:
@@ -72,7 +66,7 @@
                    predicate:(nullable NSPredicate *)predicate
                       anchor:(nullable HKQueryAnchor *)anchor
                        limit:(NSUInteger)limit
-              resultsHandler:(void(^)(HKAnchoredObjectQuery *query, NSArray<__kindof HKSample *> * __nullable sampleObjects, NSArray<HKDeletedObject *> * __nullable deletedObjects, HKQueryAnchor * __nullable newAnchor, NSError * __nullable error))handler NS_AVAILABLE_IOS(9_0);
+              resultsHandler:(void(^)(HKAnchoredObjectQuery *query, NSArray<__kindof HKSample *> * _Nullable sampleObjects, NSArray<HKDeletedObject *> * _Nullable deletedObjects, HKQueryAnchor * _Nullable newAnchor, NSError * _Nullable error))handler HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCDADocumentSample.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCDADocumentSample.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCDADocumentSample.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCDADocumentSample.h	2016-06-05 05:29:10.000000000 +0200
@@ -0,0 +1,124 @@
+//
+//  HKCDADocumentSample.h
+//  HealthKit
+//
+//  Copyright © 2015 Apple. All rights reserved.
+//
+//  HealthKit support for storing and retrieving
+//  Consolidated Clinical Document records.
+//
+
+#import <HealthKit/HKDocumentSample.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class HKCDADocument;
+
+/*!
+ @class         HKCDADocumentSample
+ @abstract      A sample object representing a CDA document.
+ */
+HK_CLASS_AVAILABLE_IOS_ONLY(10_0)
+@interface HKCDADocumentSample : HKDocumentSample
+
+/*!
+ @property      document
+ @abstract      The contents of the document.
+ @discussion    Access to each CDA instance must be authorized by the user in order for the document data to be
+                accessible to an app.  The authorization request occurs the first time a document matches the predicate
+                of an executed HKDocumentQuery.  This property will always be nil if the sample is returned by an
+                HKSampleQuery or an HKAnchoredObjectQuery.
+ */
+@property (readonly, nullable) HKCDADocument *document;
+
+/*!
+ @method                CDADocumentSampleWithData:startDate:endDate:device:metadata:validationError:
+ @abstract              Creates a new document sample with the specified attributes.
+ @param documentData    Document contents in an XML format that meets the CDA standard.
+ @param startDate       The start date for the document.
+ @param endDate         The end date for the document.
+ @param metadata        Metadata for the document.
+ @param validationError The XML content will be validated against the standard for CDA content.  If that validation
+                        fails, then this parameter will be set with the relavant error.  Detailed information about the
+                        failure may be obtained by examining the value for the HKDetailedCDAValidationErrorKey key of
+                        the NSError's userInfo dictionary.
+ @return                The new instance or nil if the documentData does not pass validation.
+ @discussion            Attributes of the document, such as title, patient name, etc. will be extracted automatically
+                        from the document content.
+ */
++ (nullable instancetype)CDADocumentSampleWithData:(NSData *)documentData
+                                         startDate:(NSDate *)startDate
+                                           endDate:(NSDate *)endDate
+                                          metadata:(nullable NSDictionary<NSString *, id> *)metadata
+                                   validationError:(NSError **)validationError __WATCHOS_UNAVAILABLE;
+
+@end
+
+@interface HKCDADocument : NSObject
+
+/*!
+ @property  documentData
+ @abstract  The CDA document content in XML format as specified in the CDA standard. This may be nil if the
+            includeDocumentData option in HKDocumentQuery is specified as NO.
+ */
+@property (readonly, copy, nullable) NSData *documentData;
+
+/*!
+ @property      title
+ @abstract      The title of the document.
+ @discussion    This property is extracted automatically from the document.
+ */
+@property (readonly, copy) NSString *title;
+
+/*!
+ @property      patientName
+ @abstract      The name of the patient receiving treatment.
+ @discussion    This property is extracted automatically from the document.
+ */
+@property (readonly, copy) NSString *patientName;
+
+/*!
+ @property      authorName
+ @abstract      The person responsible for authoring the document.  Usually, this is the treating physician.
+ @discussion    This property is extracted automatically from the document.
+ */
+@property (readonly, copy) NSString *authorName;
+
+/*!
+ @property      custodianName
+ @abstract      The organization responsible for the document.  This is usually the treating institution name.
+ @discussion    This property is extracted automatically from the document.
+ */
+@property (readonly, copy) NSString *custodianName;
+
+@end
+
+/*!
+ @constant  HKPredicateKeyPathCDATitle
+ */
+HK_EXTERN NSString * const HKPredicateKeyPathCDATitle HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
+
+/*!
+ @constant  HKPredicateKeyPathCDAPatientName
+ */
+HK_EXTERN NSString * const HKPredicateKeyPathCDAPatientName HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
+
+/*!
+ @constant  HKPredicateKeyPathCDAAuthorName
+ */
+HK_EXTERN NSString * const HKPredicateKeyPathCDAAuthorName HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
+
+/*!
+ @constant  HKPredicateKeyPathCDACustodianName
+ */
+HK_EXTERN NSString * const HKPredicateKeyPathCDACustodianName HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
+
+/*!
+ @constant      HKDetailedCDAValidationErrorKey
+ @discussion    This may be used with the validationError parameter of
+                CDADocumentSampleWithData:startDate:endDate:device:metadata:validationError: to obtain a detailed
+                description of the validation errors encountered when creating a CDA document.
+ */
+HK_EXTERN NSString * const HKDetailedCDAValidationErrorKey HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCategorySample.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCategorySample.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCategorySample.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCategorySample.h	2016-06-05 05:29:10.000000000 +0200
@@ -17,7 +17,7 @@
  @abstract   An HKObject subclass representing an category measurement
  @discussion Category samples are samples that can be categorized into an enum of concrete values
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKCategorySample : HKSample
 
 @property (readonly, strong) HKCategoryType *categoryType;
@@ -76,13 +76,13 @@
                              startDate:(NSDate *)startDate
                                endDate:(NSDate *)endDate
                                 device:(nullable HKDevice *)device
-                              metadata:(nullable NSDictionary<NSString *, id> *)metadata NS_AVAILABLE_IOS(9_0);
+                              metadata:(nullable NSDictionary<NSString *, id> *)metadata HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 @end
 
 /*!
  @constant     HKPredicateKeyPathCategoryValue
  */
-HK_EXTERN NSString * const HKPredicateKeyPathCategoryValue NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKPredicateKeyPathCategoryValue HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCharacteristicObjects.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCharacteristicObjects.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCharacteristicObjects.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCharacteristicObjects.h	2016-06-05 05:29:10.000000000 +0200
@@ -0,0 +1,54 @@
+//
+//  HKCharacteristicObjects.h
+//  HealthKit
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <HealthKit/HKDefines.h>
+
+#import <Foundation/Foundation.h>
+
+/*!
+ @class     HKBiologicalSexObject
+ @abstract  A wrapper object for HKBiologicalSex enumeration.
+ */
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
+@interface HKBiologicalSexObject : NSObject <NSCopying, NSSecureCoding>
+
+@property (readonly) HKBiologicalSex biologicalSex;
+
+@end
+
+/*!
+ @class     HKBloodTypeObject
+ @abstract  A wrapper object for HKBloodType enumeration.
+ */
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
+@interface HKBloodTypeObject : NSObject <NSCopying, NSSecureCoding>
+
+@property (readonly) HKBloodType bloodType;
+
+@end
+
+/*!
+ @class     HKFitzpatrickSkinTypeObject
+ @abstract  A wrapper object for HKFitzpatrickSkinType enumeration.
+ */
+HK_CLASS_AVAILABLE_IOS_WATCHOS(9_0, 2_0)
+@interface HKFitzpatrickSkinTypeObject : NSObject <NSCopying, NSSecureCoding>
+
+@property (readonly) HKFitzpatrickSkinType skinType;
+
+@end
+
+/*!
+ @class     HKWheelchairUseObject
+ @abstract  A wrapper object for HKWheelchairUse enumeration.
+ */
+HK_CLASS_AVAILABLE_IOS_WATCHOS(10_0, 3_0)
+@interface HKWheelchairUseObject : NSObject <NSCopying, NSSecureCoding>
+
+@property (readonly) HKWheelchairUse wheelchairUse;
+
+@end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCorrelation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCorrelation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCorrelation.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCorrelation.h	2016-06-05 05:29:10.000000000 +0200
@@ -21,7 +21,7 @@
                 For example, systolic and diastolic blood pressure readings are typically presented together so these
                 readings should be saved with a correlation of type blood pressure.
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKCorrelation : HKSample
 
 @property (readonly) HKCorrelationType *correlationType;
@@ -68,7 +68,7 @@
                             endDate:(NSDate *)endDate
                             objects:(NSSet<HKSample *> *)objects
                              device:(nullable HKDevice *)device
-                           metadata:(nullable NSDictionary<NSString *, id> *)metadata NS_AVAILABLE_IOS(9_0);
+                           metadata:(nullable NSDictionary<NSString *, id> *)metadata HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @method    objectsForType:
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCorrelationQuery.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCorrelationQuery.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCorrelationQuery.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKCorrelationQuery.h	2016-06-05 05:29:10.000000000 +0200
@@ -19,7 +19,7 @@
                 accepts a predicate to filter HKCorrelations and a dictionary of predicates to filter the
                 correlated samples.
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKCorrelationQuery : HKQuery
 
 @property (readonly, copy) HKCorrelationType *correlationType;
@@ -47,7 +47,7 @@
 - (instancetype)initWithType:(HKCorrelationType *)correlationType
                    predicate:(nullable NSPredicate *)predicate
             samplePredicates:(nullable NSDictionary<HKSampleType *, NSPredicate *> *)samplePredicates
-                  completion:(void(^)(HKCorrelationQuery *query, NSArray<HKCorrelation *> * __nullable correlations, NSError * __nullable error))completion;
+                  completion:(void(^)(HKCorrelationQuery *query, NSArray<HKCorrelation *> * _Nullable correlations, NSError * _Nullable error))completion;
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDefines.h	2016-02-26 05:11:45.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDefines.h	2016-06-05 05:29:10.000000000 +0200
@@ -15,14 +15,17 @@
 #define HK_EXTERN extern "C" __attribute__((visibility("default")))
 #endif
 
-#define HK_CLASS_AVAILABLE_IOS(_iOSIntro)    NS_CLASS_AVAILABLE_IOS(_iOSIntro)
+#define HK_AVAILABLE_IOS_WATCHOS(_iOSIntro, _watchOSIntro)    NS_AVAILABLE_IOS(_iOSIntro) __WATCHOS_AVAILABLE(_watchOSIntro)
+#define HK_AVAILABLE_IOS_ONLY(_iOSIntro)    NS_AVAILABLE_IOS(_iOSIntro) __WATCHOS_UNAVAILABLE
 #define HK_AVAILABLE_WATCHOS_ONLY(_watchOSIntro)    __WATCHOS_AVAILABLE(_watchOSIntro) __IOS_UNAVAILABLE
+
+#define HK_CLASS_AVAILABLE_IOS_ONLY(_iOSIntro)    NS_CLASS_AVAILABLE_IOS(_iOSIntro) __WATCHOS_PROHIBITED
 #define HK_CLASS_AVAILABLE_WATCHOS_ONLY(_watchOSIntro)    HK_EXTERN HK_AVAILABLE_WATCHOS_ONLY(_watchOSIntro)
 #define HK_CLASS_AVAILABLE_IOS_WATCHOS(_iOSIntro, _watchOSIntro)    NS_CLASS_AVAILABLE_IOS(_iOSIntro) __WATCHOS_AVAILABLE(_watchOSIntro)
+
 #define HK_ENUM_AVAILABLE_IOS_WATCHOS(_iOSIntro, _watchOSIntro)    NS_ENUM_AVAILABLE_IOS(_iOSIntro) __WATCHOS_AVAILABLE(_watchOSIntro)
-#define HK_AVAILABLE_IOS_WATCHOS(_iOSIntro, _watchOSIntro)    NS_AVAILABLE_IOS(_iOSIntro) __WATCHOS_AVAILABLE(_watchOSIntro)
 
-HK_EXTERN NSString * const HKErrorDomain NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKErrorDomain HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @enum      HKErrorCode
@@ -48,9 +51,9 @@
     HKErrorAuthorizationNotDetermined,
     HKErrorDatabaseInaccessible,
     HKErrorUserCanceled,
-    HKErrorAnotherWorkoutSessionStarted NS_ENUM_AVAILABLE_IOS(9_0),
-    HKErrorUserExitedWorkoutSession     NS_ENUM_AVAILABLE_IOS(9_0),
-} NS_ENUM_AVAILABLE_IOS(8_0);
+    HKErrorAnotherWorkoutSessionStarted HK_ENUM_AVAILABLE_IOS_WATCHOS(9_0, 2_0),
+    HKErrorUserExitedWorkoutSession     HK_ENUM_AVAILABLE_IOS_WATCHOS(9_0, 2_0),
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @enum      HKUpdateFrequency
@@ -60,7 +63,7 @@
     HKUpdateFrequencyHourly,
     HKUpdateFrequencyDaily,
     HKUpdateFrequencyWeekly,
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @enum      HKAuthorizationStatus
@@ -76,7 +79,7 @@
     HKAuthorizationStatusNotDetermined = 0,
     HKAuthorizationStatusSharingDenied,
     HKAuthorizationStatusSharingAuthorized,
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @enum       HKBiologicalSex
@@ -84,10 +87,10 @@
  */
 typedef NS_ENUM(NSInteger, HKBiologicalSex) {
     HKBiologicalSexNotSet = 0,
-    HKBiologicalSexFemale NS_ENUM_AVAILABLE_IOS(8_0),
-    HKBiologicalSexMale NS_ENUM_AVAILABLE_IOS(8_0),
-    HKBiologicalSexOther NS_ENUM_AVAILABLE_IOS(8_2),
-};
+    HKBiologicalSexFemale,
+    HKBiologicalSexMale,
+    HKBiologicalSexOther HK_ENUM_AVAILABLE_IOS_WATCHOS(8_2, 2_0),
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @enum       HKBloodType
@@ -103,7 +106,7 @@
     HKBloodTypeABNegative,
     HKBloodTypeOPositive,
     HKBloodTypeONegative,
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @enum          HKCategoryValueSleepAnalysis
@@ -118,7 +121,8 @@
 typedef NS_ENUM(NSInteger, HKCategoryValueSleepAnalysis) {
     HKCategoryValueSleepAnalysisInBed,
     HKCategoryValueSleepAnalysisAsleep,
-} NS_ENUM_AVAILABLE_IOS(8_0);
+    HKCategoryValueSleepAnalysisAwake HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 
 /*!
@@ -133,7 +137,7 @@
 typedef NS_ENUM(NSInteger, HKCategoryValueAppleStandHour) {
     HKCategoryValueAppleStandHourStood = 0,
     HKCategoryValueAppleStandHourIdle,
-} NS_ENUM_AVAILABLE_IOS(9_0);
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @enum          HKFitzpatrickSkinType
@@ -156,7 +160,20 @@
     HKFitzpatrickSkinTypeIV,
     HKFitzpatrickSkinTypeV,
     HKFitzpatrickSkinTypeVI,
-} NS_ENUM_AVAILABLE_IOS(9_0);
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
+
+/*!
+ @enum          HKWheelchairUse
+ @abstract      This enumerated type is used to represent whether the user uses a wheelchair.
+ 
+ @constant      HKWheelchairUseNo      The user does not use a wheelchair.
+ @constant      HKWheelchairUseYes     The user does use a wheelchair.
+ */
+typedef NS_ENUM(NSInteger, HKWheelchairUse) {
+    HKWheelchairUseNotSet = 0,
+    HKWheelchairUseNo,
+    HKWheelchairUseYes,
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
 
 /*!
  @enum          HKCategoryValueCervicalMucusQuality
@@ -169,7 +186,7 @@
     HKCategoryValueCervicalMucusQualityCreamy,
     HKCategoryValueCervicalMucusQualityWatery,
     HKCategoryValueCervicalMucusQualityEggWhite,
-} NS_ENUM_AVAILABLE_IOS(9_0);
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @enum          HKCategoryValueOvulationTestResult
@@ -181,7 +198,7 @@
     HKCategoryValueOvulationTestResultNegative = 1,
     HKCategoryValueOvulationTestResultPositive,
     HKCategoryValueOvulationTestResultIndeterminate,
-} NS_ENUM_AVAILABLE_IOS(9_0);
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @enum          HKCategoryValueMenstrualFlow
@@ -192,7 +209,7 @@
     HKCategoryValueMenstrualFlowLight,
     HKCategoryValueMenstrualFlowMedium,
     HKCategoryValueMenstrualFlowHeavy
-} NS_ENUM_AVAILABLE_IOS(9_0);
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @enum          HKCategoryValue
@@ -200,6 +217,6 @@
  */
 typedef NS_ENUM(NSInteger, HKCategoryValue) {
     HKCategoryValueNotApplicable = 0,
-} NS_ENUM_AVAILABLE_IOS(9_0);
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDeletedObject.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDeletedObject.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDeletedObject.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDeletedObject.h	2016-06-05 05:29:10.000000000 +0200
@@ -13,7 +13,7 @@
  @class         HKDeletedObject
  @abstract      A class representing an HKObject that was deleted from the HealtKit database.
  */
-HK_CLASS_AVAILABLE_IOS(9_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(9_0, 2_0)
 @interface HKDeletedObject : NSObject <NSSecureCoding>
 
 /*!
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDevice.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDevice.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDevice.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDevice.h	2016-05-28 05:54:34.000000000 +0200
@@ -14,60 +14,60 @@
  @abstract      Used with predicateForObjectsWithDeviceProperty to specify a device name.
  @discussion    The expected value type is an NSString.
  */
-HK_EXTERN NSString * const HKDevicePropertyKeyName NS_AVAILABLE_IOS(9_0);
+HK_EXTERN NSString * const HKDevicePropertyKeyName HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @constant      HKDevicePropertyKeyManufacturer
  @abstract      Used with predicateForObjectsWithDeviceProperty to specify a device manufacturer.
  @discussion    The expected value type is an NSString.
  */
-HK_EXTERN NSString * const HKDevicePropertyKeyManufacturer NS_AVAILABLE_IOS(9_0);
+HK_EXTERN NSString * const HKDevicePropertyKeyManufacturer HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @constant      HKDevicePropertyKeyModel
  @abstract      Used with predicateForObjectsWithDeviceProperty to specify a device model.
  @discussion    The expected value type is an NSString.
  */
-HK_EXTERN NSString * const HKDevicePropertyKeyModel NS_AVAILABLE_IOS(9_0);
+HK_EXTERN NSString * const HKDevicePropertyKeyModel HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @constant      HKDevicePropertyKeyHardwareVersion
  @abstract      Used with predicateForObjectsWithDeviceProperty to specify a hardware version.
  @discussion    The expected value type is an NSString.
  */
-HK_EXTERN NSString * const HKDevicePropertyKeyHardwareVersion NS_AVAILABLE_IOS(9_0);
+HK_EXTERN NSString * const HKDevicePropertyKeyHardwareVersion HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @constant      HKDevicePropertyKeyFirmwareVersion
  @abstract      Used with predicateForObjectsWithDeviceProperty to specify a firmware version.
  @discussion    The expected value type is an NSString.
  */
-HK_EXTERN NSString * const HKDevicePropertyKeyFirmwareVersion NS_AVAILABLE_IOS(9_0);
+HK_EXTERN NSString * const HKDevicePropertyKeyFirmwareVersion HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @constant      HKDevicePropertyKeySoftwareVersion
  @abstract      Used with predicateForObjectsWithDeviceProperty to specify a software version.
  @discussion    The expected value type is an NSString.
  */
-HK_EXTERN NSString * const HKDevicePropertyKeySoftwareVersion NS_AVAILABLE_IOS(9_0);
+HK_EXTERN NSString * const HKDevicePropertyKeySoftwareVersion HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @constant      HKDevicePropertyKeyLocalIdentifier
  @abstract      Used with predicateForObjectsWithDeviceProperty to specify a local identifier.
  @discussion    The expected value type is an NSString.
  */
-HK_EXTERN NSString * const HKDevicePropertyKeyLocalIdentifier NS_AVAILABLE_IOS(9_0);
+HK_EXTERN NSString * const HKDevicePropertyKeyLocalIdentifier HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @constant      HKDevicePropertyKeyUDIDeviceIdentifier
  @abstract      Used with predicateForObjectsWithDeviceProperty to specify a UDI device identifier.
  @discussion    The expected value type is an NSString.
  */
-HK_EXTERN NSString * const HKDevicePropertyKeyUDIDeviceIdentifier NS_AVAILABLE_IOS(9_0);
+HK_EXTERN NSString * const HKDevicePropertyKeyUDIDeviceIdentifier HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 
 
-HK_CLASS_AVAILABLE_IOS(9_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(9_0, 2_0)
 @interface HKDevice : NSObject <NSSecureCoding, NSCopying>
 
 /*!
@@ -75,7 +75,7 @@
  @abstract      The name of the receiver.
  @discussion    The user-facing name, such as the one displayed in the Bluetooth Settings for a BLE device.
  */
-@property (readonly) NSString *name;
+@property (readonly, nullable) NSString *name;
 
 /*!
  @property      manufacturer
@@ -136,14 +136,14 @@
  @discussion    This allows initialization of an HKDevice object based on the
                 information provided.
  */
-- (instancetype)initWithName:(NSString * __nullable)name
-                manufacturer:(NSString * __nullable)manufacturer
-                       model:(NSString * __nullable)model
-             hardwareVersion:(NSString * __nullable)hardwareVersion
-             firmwareVersion:(NSString * __nullable)firmwareVersion
-             softwareVersion:(NSString * __nullable)softwareVersion
-             localIdentifier:(NSString * __nullable)localIdentifier
-         UDIDeviceIdentifier:(NSString * __nullable)UDIDeviceIdentifier;
+- (instancetype)initWithName:(nullable NSString *)name
+                manufacturer:(NSString * _Nullable)manufacturer
+                       model:(NSString * _Nullable)model
+             hardwareVersion:(NSString * _Nullable)hardwareVersion
+             firmwareVersion:(NSString * _Nullable)firmwareVersion
+             softwareVersion:(NSString * _Nullable)softwareVersion
+             localIdentifier:(NSString * _Nullable)localIdentifier
+         UDIDeviceIdentifier:(NSString * _Nullable)UDIDeviceIdentifier;
 
 - (instancetype)init NS_UNAVAILABLE;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDocumentQuery.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDocumentQuery.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDocumentQuery.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDocumentQuery.h	2016-06-05 05:29:10.000000000 +0200
@@ -0,0 +1,79 @@
+//
+//  HKDocumentQuery.h
+//  HealthKit
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#include <HealthKit/HKQuery.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class HKDocumentSample;
+@class HKDocumentType;
+
+/*!
+ @class         HKDocumentQuery
+ @abstract      A concrete subclass of HKQuery that provides an interface to retrieve documents from the Health store.
+ 
+ */
+HK_CLASS_AVAILABLE_IOS_ONLY(10_0)
+@interface HKDocumentQuery : HKQuery
+
+/*!
+ @property      limit
+ @abstract      The maximum number of documents the receiver will return upon completion.
+ */
+@property (readonly) NSUInteger limit;
+
+/*!
+ @property      sortDescriptors
+ @abstract      An array of NSSortDescriptors.
+ */
+@property (readonly, copy, nullable) NSArray<NSSortDescriptor *> *sortDescriptors;
+
+/*!
+ @property      includeDocumentData
+ @abstract      The XML content for documents may be large.  This property can be used to control whether the query
+                returns the XML content for each record.
+ */
+@property (readonly) BOOL includeDocumentData;
+
+/*!
+ @method        initWithDocumentType:predicate:limit:sortDescriptors:includeDocumentData:resultsHandler:
+ @abstract      Returns a query that will retrieve HKDocumentSamples matching the given predicate.
+ 
+ @param         documentType        The type of document to retreive.
+ @param         predicate           The predicate which documents should match.
+ @param         limit               The maximum number of documents to return.  Pass HKObjectQueryNoLimit for no limit.
+ @param         sortDescriptors     The sort descriptors to use to order the resulting documents.
+ @param         includeDocumentData If true, the document content will be returned with the HKDocumentSample instance.
+                                    This option can be used to limit the size of the content returned since the content
+                                    may be large.
+ @param         resultsHandler      The block that will receive query results.  Results will be returned incrementally
+                                    through several calls to this block.  When there are no more results, the done 
+                                    parameter will be YES and the results array will be empty.  If results is nil, then
+                                    an error has occurred and the error parameter will be set.  Delivery of results can
+                                    be stopped by calling HKHealthStore's stopQuery: method.
+
+ @discussion    Health documents may contain sensitive data that a user may want to control explicitly. HKDocumentSample
+                objects returned by HKSampleQuery and HKAnchoredObjectQuery do not include this data (i.e., the document
+                property is nil).  This query can be used to retrieve fully populated HKDocumentSample instances.  The 
+                query will prompt the user to authorize your app to read individual documents.  The query will then
+                return the documents that your app is authorized to read. The user will only be asked to authorize your
+                app to read documents that are new since the last time an HKDocumentQuery was executed.
+ */
+- (instancetype)initWithDocumentType:(HKDocumentType *)documentType
+                           predicate:(nullable NSPredicate *)predicate
+                               limit:(NSUInteger)limit
+                     sortDescriptors:(nullable NSArray<NSSortDescriptor *> *)sortDescriptors
+                 includeDocumentData:(BOOL)includeDocumentData
+                      resultsHandler:(void(^)(HKDocumentQuery *query,
+                                              NSArray<__kindof HKDocumentSample *> * _Nullable results,
+                                              BOOL done,
+                                              NSError * _Nullable error))resultsHandler;
+
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDocumentSample.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDocumentSample.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDocumentSample.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKDocumentSample.h	2016-06-05 05:29:10.000000000 +0200
@@ -0,0 +1,25 @@
+//
+//  HKDocumentSample.h
+//  HealthKit
+//
+//  Copyright © 2016 Apple. All rights reserved.
+//
+
+#import <HealthKit/HKSample.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class HKDocumentType;
+
+/*!
+ @class         HKDocumentSample
+ @abstract      An abstract class representing a health document.
+ */
+HK_CLASS_AVAILABLE_IOS_WATCHOS(10_0, 3_0)
+@interface HKDocumentSample : HKSample
+
+@property (readonly, strong) HKDocumentType *documentType;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKHealthStore.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKHealthStore.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKHealthStore.h	2016-02-23 04:42:21.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKHealthStore.h	2016-06-05 05:29:03.000000000 +0200
@@ -6,13 +6,11 @@
 //
 
 #import <HealthKit/HKDefines.h>
+#import <HealthKit/HKCharacteristicObjects.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-@class HKBiologicalSexObject;
-@class HKBloodTypeObject;
 @class HKDevice;
-@class HKFitzpatrickSkinTypeObject;
 @class HKObject;
 @class HKObjectType;
 @class HKQuantity;
@@ -24,13 +22,14 @@
 @class HKSourceRevision;
 @class HKUnit;
 @class HKWorkout;
+@class HKWorkoutConfiguration;
 @class HKWorkoutSession;
 
 /*!
  @class         HKHealthStore
  @abstract      The HKHealthStore class provides an interface for accessing and storing the user's health data.
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKHealthStore : NSObject
 
 /*!
@@ -62,12 +61,12 @@
                 granted authorization.
  
                 To customize the messages displayed on the authorization sheet, set the following keys in your app's
-                Info.plist file. Set the NSHealthShareUsageDescription key to customize the message for reading data. Set
-                the NSHealthUpdateUsageDescription key to customize the message for writing data.
+                Info.plist file. Set the NSHealthShareUsageDescription key to customize the message for reading data.
+                Set the NSHealthUpdateUsageDescription key to customize the message for writing data.
  */
 - (void)requestAuthorizationToShareTypes:(nullable NSSet<HKSampleType *> *)typesToShare
                                readTypes:(nullable NSSet<HKObjectType *> *)typesToRead
-                              completion:(void (^)(BOOL success, NSError * __nullable error))completion;
+                              completion:(void (^)(BOOL success, NSError * _Nullable error))completion;
 
 /*!
  @method        handleAuthorizationForExtensionWithCompletion:
@@ -81,15 +80,15 @@
                 the user, if necessary, completed successfully and was not cancelled by the user.  It does NOT indicate
                 whether the application was granted authorization.
  */
-- (void)handleAuthorizationForExtensionWithCompletion:(void (^)(BOOL success, NSError * __nullable error))completion NS_AVAILABLE_IOS(9_0) __WATCHOS_UNAVAILABLE NS_EXTENSION_UNAVAILABLE("Not available to extensions") ;
+- (void)handleAuthorizationForExtensionWithCompletion:(void (^)(BOOL success, NSError * _Nullable error))completion HK_AVAILABLE_IOS_ONLY(9_0) NS_EXTENSION_UNAVAILABLE("Not available to extensions") ;
 
 /*!
  @method        earliestPermittedSampleDate
  @abstract      Samples prior to the earliestPermittedSampleDate cannot be saved or queried.
  @discussion    On some platforms, only samples with end dates newer than the value returned by earliestPermittedSampleDate
-                may be saved or retreived.
+                may be saved or retrieved.
  */
-- (NSDate *)earliestPermittedSampleDate NS_AVAILABLE_IOS(9_0);
+- (NSDate *)earliestPermittedSampleDate HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @method        saveObject:withCompletion:
@@ -107,21 +106,21 @@
                 This operation is performed asynchronously and the completion will be executed on an arbitrary
                 background queue.
  */
-- (void)saveObject:(HKObject *)object withCompletion:(void(^)(BOOL success, NSError * __nullable error))completion;
+- (void)saveObject:(HKObject *)object withCompletion:(void(^)(BOOL success, NSError * _Nullable error))completion;
 
 /*!
  @method        saveObjects:withCompletion:
  @abstract      Saves an array of HKObjects.
  @discussion    See discussion of saveObject:withCompletion:.
  */
-- (void)saveObjects:(NSArray<HKObject *> *)objects withCompletion:(void(^)(BOOL success, NSError * __nullable error))completion;
+- (void)saveObjects:(NSArray<HKObject *> *)objects withCompletion:(void(^)(BOOL success, NSError * _Nullable error))completion;
 
 /*!
  @method        deleteObject:withCompletion:
  @abstract      Deletes a single HKObject from the HealthKit database.
  @discussion    See deleteObjects:withCompletion:.
  */
-- (void)deleteObject:(HKObject *)object withCompletion:(void(^)(BOOL success, NSError * __nullable error))completion;
+- (void)deleteObject:(HKObject *)object withCompletion:(void(^)(BOOL success, NSError * _Nullable error))completion;
 
 /*!
  @method        deleteObjects:withCompletion:
@@ -129,7 +128,7 @@
  @discussion    An application may only delete objects that it previously saved.  This operation is performed
                 asynchronously and the completion will be executed on an arbitrary background queue.
  */
-- (void)deleteObjects:(NSArray<HKObject *> *)objects withCompletion:(void(^)(BOOL success, NSError * __nullable error))completion NS_AVAILABLE_IOS(9_0);
+- (void)deleteObjects:(NSArray<HKObject *> *)objects withCompletion:(void(^)(BOOL success, NSError * _Nullable error))completion HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @method        deleteObjectsOfType:predicate:withCompletion:
@@ -137,17 +136,21 @@
  @discussion    An application may only delete objects that it previously saved.  This operation is performed
                 asynchronously and the completion will be executed on an arbitrary background queue.
  */
-- (void)deleteObjectsOfType:(HKObjectType *)objectType predicate:(NSPredicate *)predicate withCompletion:(void(^)(BOOL success, NSUInteger deletedObjectCount, NSError * __nullable error))completion NS_AVAILABLE_IOS(9_0);
+- (void)deleteObjectsOfType:(HKObjectType *)objectType predicate:(NSPredicate *)predicate withCompletion:(void(^)(BOOL success, NSUInteger deletedObjectCount, NSError * _Nullable error))completion HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @method        executeQuery:
  @abstract      Begins executing the given query.
- @discussion    After executing a query the completion, update, and/or results handlers of that query will be invoked
+ @discussion    After executing a query, the completion, update, and/or results handlers of that query will be invoked
                 asynchronously on an arbitrary background queue as results become available.  Errors that prevent a
                 query from executing will be delivered to one of the query's handlers.  Which handler the error will be
-                delivered to is defined by the HKQuery subclass.  The behavior of calling this method with a query that
-                is already executing is undefined.  If a query would retrieve objects with an HKObjectType property,
-                then the application must request authorization to access objects of that type before executing the query.
+                delivered to is defined by the HKQuery subclass.  
+ 
+                Each HKQuery instance may only be executed once and calling this method with a currently executing query
+                or one that was previously executed will result in an exception.
+                
+                If a query would retrieve objects with an HKObjectType property, then the application must request
+                authorization to access objects of that type before executing the query.
  */
 - (void)executeQuery:(HKQuery *)query;
 
@@ -170,15 +173,17 @@
 - (void)splitTotalEnergy:(HKQuantity *)totalEnergy
                startDate:(NSDate *)startDate
                  endDate:(NSDate *)endDate
-          resultsHandler:(void(^)(HKQuantity * __nullable restingEnergy, HKQuantity * __nullable activeEnergy, NSError * __nullable error))resultsHandler NS_AVAILABLE_IOS(9_0);
+          resultsHandler:(void(^)(HKQuantity * _Nullable restingEnergy, HKQuantity * _Nullable activeEnergy, NSError * _Nullable error))resultsHandler HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
+
+- (nullable NSDate *)dateOfBirthWithError:(NSError **)error NS_DEPRECATED_IOS(8_0, 10_0, "Use dateOfBirthComponentsWithError:") __WATCHOS_DEPRECATED(2_0, 3_0, "Use dateOfBirthComponentsWithError:");
 
 /*!
- @method        dateOfBirthWithError:
- @abstract      Returns the user's date of birth.
+ @method        dateOfBirthComponentsWithError:
+ @abstract      Returns the user's date of birth in the Gregorian calendar.
  @discussion    Before calling this method, the application should request authorization to access objects with the
                 HKCharacteristicType identified by HKCharacteristicTypeIdentifierDateOfBirth.
  */
-- (nullable NSDate *)dateOfBirthWithError:(NSError **)error;
+- (nullable NSDateComponents *)dateOfBirthComponentsWithError:(NSError **)error HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
 
 /*!
  @method        biologicalSexWithError:
@@ -202,7 +207,15 @@
  @discussion    Before calling this method, the application should request authorization to access objects with the
                 HKCharacteristicType identified by HKCharacteristicTypeIdentifierFitzpatrickSkinType.
  */
-- (nullable HKFitzpatrickSkinTypeObject *)fitzpatrickSkinTypeWithError:(NSError **)error NS_AVAILABLE_IOS(9_0);
+- (nullable HKFitzpatrickSkinTypeObject *)fitzpatrickSkinTypeWithError:(NSError **)error HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
+
+/*!
+ @method        wheelchairUseWithError:
+ @abstract      Returns an object encapsulating the user's wheelchair use.
+ @discussion    Before calling this method, the application should request authorization to access objects with the
+                HKCharacteristicType identified by HKCharacteristicTypeIdentifierWheelchairUse.
+ */
+- (nullable HKWheelchairUseObject *)wheelchairUseWithError:(NSError **)error HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
 
 @end
 
@@ -217,7 +230,7 @@
  
                 The workout provided must be one that has already been saved to HealthKit.
  */
-- (void)addSamples:(NSArray<HKSample *> *)samples toWorkout:(HKWorkout *)workout completion:(void(^)(BOOL success, NSError * __nullable error))completion;
+- (void)addSamples:(NSArray<HKSample *> *)samples toWorkout:(HKWorkout *)workout completion:(void(^)(BOOL success, NSError * _Nullable error))completion;
 
 /*!
  @method        startWorkoutSession:
@@ -236,6 +249,34 @@
  */
 - (void)endWorkoutSession:(HKWorkoutSession *)workoutSession HK_AVAILABLE_WATCHOS_ONLY(2_0);
 
+/*!
+ @method        pauseWorkoutSession:
+ @abstract      Pauses the given workout session.
+ @discussion    This method will pause the given session if it is currently running. The state of the workout session
+                will transition to HKWorkoutSessionStatePaused. An HKWorkoutEventTypePause will be generated and
+                delivered to the workout session's delegate.
+ */
+- (void)pauseWorkoutSession:(HKWorkoutSession *)workoutSession HK_AVAILABLE_WATCHOS_ONLY(3_0);
+
+/*!
+ @method        resumeWorkoutSession:
+ @abstract      Resumes the given workout session.
+ @discussion    This method will resume the given session if it is currently paused. The state of the workout session
+                will transition to HKWorkoutSessionStateRunning. An HKWorkoutEventTypeResume will be generated and
+                delivered to the workout session's delegate.
+ */
+- (void)resumeWorkoutSession:(HKWorkoutSession *)workoutSession HK_AVAILABLE_WATCHOS_ONLY(3_0);
+
+/*!
+ @method        startWatchAppWithWorkoutConfiguration:completion:
+ @abstract      Launches or wakes up the WatchKit app on the watch
+ @discussion    This method will launch the WatchKit app corresponding to the calling iOS application on the currently
+                active Apple Watch. After launching, the handleWorkoutConfiguration: method on the WKExtensionDelegate
+                protocol will be called with the HKWorkoutConfiguration as a parameter. The receiving Watch app can use
+                this configuration object to create an HKWorkoutSession and start it with -startWorkoutSession:.
+ */
+- (void)startWatchAppWithWorkoutConfiguration:(HKWorkoutConfiguration *)workoutConfiguration completion:(void (^)(BOOL success, NSError * _Nullable error))completion HK_AVAILABLE_IOS_ONLY(10_0);
+
 @end
 
 
@@ -250,11 +291,11 @@
                 HKQuantityTypeIdentifierStepCount) have a minimum frequency of HKUpdateFrequencyHourly. This is enforced
                 transparently to the caller.
  */
-- (void)enableBackgroundDeliveryForType:(HKObjectType *)type frequency:(HKUpdateFrequency)frequency withCompletion:(void(^)(BOOL success, NSError * __nullable error))completion __WATCHOS_UNAVAILABLE;
+- (void)enableBackgroundDeliveryForType:(HKObjectType *)type frequency:(HKUpdateFrequency)frequency withCompletion:(void(^)(BOOL success, NSError * _Nullable error))completion __WATCHOS_UNAVAILABLE;
 
-- (void)disableBackgroundDeliveryForType:(HKObjectType *)type withCompletion:(void(^)(BOOL success, NSError * __nullable error))completion __WATCHOS_UNAVAILABLE;
+- (void)disableBackgroundDeliveryForType:(HKObjectType *)type withCompletion:(void(^)(BOOL success, NSError * _Nullable error))completion __WATCHOS_UNAVAILABLE;
 
-- (void)disableAllBackgroundDeliveryWithCompletion:(void(^)(BOOL success, NSError * __nullable error))completion __WATCHOS_UNAVAILABLE;
+- (void)disableAllBackgroundDeliveryWithCompletion:(void(^)(BOOL success, NSError * _Nullable error))completion __WATCHOS_UNAVAILABLE;
 
 @end
 
@@ -266,7 +307,7 @@
                 notification when this occurs, it is necessary to provide an HKHealthStore instance for the object
                 parameter of NSNotificationCenter's addObserver methods.
  */
-HK_EXTERN NSString * const HKUserPreferencesDidChangeNotification NS_AVAILABLE_IOS(8_2);
+HK_EXTERN NSString * const HKUserPreferencesDidChangeNotification HK_AVAILABLE_IOS_WATCHOS(8_2, 2_0);
 
 @interface HKHealthStore (HKUserPreferences)
 
@@ -284,40 +325,7 @@
  
                 The returned dictionary will map HKQuantityType to HKUnit.
  */
-- (void)preferredUnitsForQuantityTypes:(NSSet<HKQuantityType *> *)quantityTypes completion:(void(^)(NSDictionary<HKQuantityType*, HKUnit *> *preferredUnits, NSError * __nullable error))completion NS_AVAILABLE_IOS(8_2);
-
-@end
-
-/*!
- @class     HKBiologicalSexObject
- @abstract  A wrapper object for HKBiologicalSex enumeration.
- */
-HK_CLASS_AVAILABLE_IOS(8_0)
-@interface HKBiologicalSexObject : NSObject <NSCopying, NSSecureCoding>
-
-@property (readonly) HKBiologicalSex biologicalSex;
-
-@end
-
-/*!
- @class     HKBloodTypeObject
- @abstract  A wrapper object for HKBloodType enumeration.
- */
-HK_CLASS_AVAILABLE_IOS(8_0)
-@interface HKBloodTypeObject : NSObject <NSCopying, NSSecureCoding>
-
-@property (readonly) HKBloodType bloodType;
-
-@end
-
-/*!
- @class     HKFitzpatrickSkinTypeObject
- @abstract  A wrapper object for HKFitzpatrickSkinType enumeration.
- */
-HK_CLASS_AVAILABLE_IOS(9_0)
-@interface HKFitzpatrickSkinTypeObject : NSObject <NSCopying, NSSecureCoding>
-
-@property (readonly) HKFitzpatrickSkinType skinType;
+- (void)preferredUnitsForQuantityTypes:(NSSet<HKQuantityType *> *)quantityTypes completion:(void(^)(NSDictionary<HKQuantityType*, HKUnit *> *preferredUnits, NSError * _Nullable error))completion HK_AVAILABLE_IOS_WATCHOS(8_2, 2_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKMetadata.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKMetadata.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKMetadata.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKMetadata.h	2016-06-05 05:29:03.000000000 +0200
@@ -14,14 +14,14 @@
  @abstract      Represents the serial number of the device that created the HKObject.
  @discussion    The expected value type is NSString.
  */
-HK_EXTERN NSString * const HKMetadataKeyDeviceSerialNumber NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyDeviceSerialNumber HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyBodyTemperatureSensorLocation
  @abstract      Represents the location where a particular body temperature reading was taken.
  @discussion    The expected value type is an NSNumber containing a HKBodyTemperatureSensorLocation value.
  */
-HK_EXTERN NSString * const HKMetadataKeyBodyTemperatureSensorLocation NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyBodyTemperatureSensorLocation HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 typedef NS_ENUM(NSInteger, HKBodyTemperatureSensorLocation) {
     HKBodyTemperatureSensorLocationOther = 0,
@@ -36,14 +36,14 @@
     HKBodyTemperatureSensorLocationEarDrum,
     HKBodyTemperatureSensorLocationTemporalArtery,
     HKBodyTemperatureSensorLocationForehead,
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyHeartRateSensorLocation
  @abstract      Represents the location where a particular heart rate reading was taken.
  @discussion    The expected value type is an NSNumber containing a HKHeartRateSensorLocation value.
  */
-HK_EXTERN NSString * const HKMetadataKeyHeartRateSensorLocation NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyHeartRateSensorLocation HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 typedef NS_ENUM(NSInteger, HKHeartRateSensorLocation) {
     HKHeartRateSensorLocationOther = 0,
@@ -53,7 +53,7 @@
     HKHeartRateSensorLocationHand,
     HKHeartRateSensorLocationEarLobe,
     HKHeartRateSensorLocationFoot,
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyFoodType
@@ -61,7 +61,7 @@
  @discussion    This should be a short string representing the type of food, such as 'Banana'. The expected value type
                 is NSString.
  */
-HK_EXTERN NSString * const HKMetadataKeyFoodType NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyFoodType HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyUDIDeviceIdentifier
@@ -71,7 +71,7 @@
  
                 ** Note that the use of this key is now discouraged in favor of the HKDevice class.
  */
-HK_EXTERN NSString * const HKMetadataKeyUDIDeviceIdentifier NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyUDIDeviceIdentifier HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyUDIProductionIdentifier
@@ -82,7 +82,7 @@
                 needed.
                 The expected value type is NSString.
  */
-HK_EXTERN NSString * const HKMetadataKeyUDIProductionIdentifier NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyUDIProductionIdentifier HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyDigitalSignature
@@ -95,21 +95,21 @@
                 Standard Elliptic Curve P-256. See documentation for details.
 
  */
-HK_EXTERN NSString * const HKMetadataKeyDigitalSignature NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyDigitalSignature HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyExternalUUID
  @abstract      Represents a unique identifier for an HKObject that is set by its source. 
  @discussion    The expected value type is NSString.
  */
-HK_EXTERN NSString * const HKMetadataKeyExternalUUID NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyExternalUUID HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyTimeZone
  @abstract      Represents the time zone that the user was in when the HKObject was created.
  @discussion    The expected value type is an NSString compatible with NSTimeZone's +timeZoneWithName:.
  */
-HK_EXTERN NSString * const HKMetadataKeyTimeZone NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyTimeZone HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 
 /*!
@@ -119,7 +119,7 @@
  
                 ** Note that the use of this key is now discouraged in favor of the HKDevice class.
  */
-HK_EXTERN NSString * const HKMetadataKeyDeviceName NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyDeviceName HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyDeviceManufacturerName
@@ -128,63 +128,118 @@
  
                 ** Note that the use of this key is now discouraged in favor of the HKDevice class.
  */
-HK_EXTERN NSString * const HKMetadataKeyDeviceManufacturerName NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyDeviceManufacturerName HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyWasTakenInLab
  @abstract      Represents whether or not the reading was taken in a lab.
  @discussion    The expected value type is an NSNumber containing a BOOL value.
  */
-HK_EXTERN NSString * const HKMetadataKeyWasTakenInLab NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyWasTakenInLab HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyReferenceRangeLowerLimit
  @abstract      Represents the lower limit of the reference range for a lab result.
  @discussion    The expected value type is an NSNumber.
  */
-HK_EXTERN NSString * const HKMetadataKeyReferenceRangeLowerLimit NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyReferenceRangeLowerLimit HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyReferenceRangeUpperLimit
  @abstract      Represents the upper limit of the reference range for a lab result.
  @discussion    The expected value type is an NSNumber.
  */
-HK_EXTERN NSString * const HKMetadataKeyReferenceRangeUpperLimit NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyReferenceRangeUpperLimit HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyWasUserEntered
  @abstract      Represents whether or not the reading was entered by the user.
  @discussion    The expected value type is an NSNumber containing a BOOL value.
  */
-HK_EXTERN NSString * const HKMetadataKeyWasUserEntered NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyWasUserEntered HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyWorkoutBrandName
  @abstract      Represents the brand name of a particular workout.
  @discussion    The expected value type is NSString.
  */
-HK_EXTERN NSString * const HKMetadataKeyWorkoutBrandName NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyWorkoutBrandName HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyGroupFitness
  @abstract      Represents whether or not a workout was performed as part of a group fitness class.
  @discussion    The expected value type is an NSNumber containing a BOOL value.
  */
-HK_EXTERN NSString * const HKMetadataKeyGroupFitness NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyGroupFitness HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyIndoorWorkout
  @abstract      Represents whether or not a workout was performed indoors as opposed to outdoors.
  @discussion    The expected value type is an NSNumber containing a BOOL value.
  */
-HK_EXTERN NSString * const HKMetadataKeyIndoorWorkout NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyIndoorWorkout HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyCoachedWorkout
  @abstract      Represents whether or not a workout was performed with a coach or personal trainer.
  @discussion    The expected value type is an NSNumber containing a BOOL value.
  */
-HK_EXTERN NSString * const HKMetadataKeyCoachedWorkout NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKMetadataKeyCoachedWorkout HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+
+typedef NS_ENUM(NSInteger, HKWeatherCondition) {
+    HKWeatherConditionNone = 0,
+    HKWeatherConditionClear,
+    HKWeatherConditionFair,
+    HKWeatherConditionPartlyCloudy,
+    HKWeatherConditionMostlyCloudy,
+    HKWeatherConditionCloudy,
+    HKWeatherConditionFoggy,
+    HKWeatherConditionHaze,
+    HKWeatherConditionWindy,
+    HKWeatherConditionBlustery,
+    HKWeatherConditionSmoky,
+    HKWeatherConditionDust,
+    HKWeatherConditionSnow,
+    HKWeatherConditionHail,
+    HKWeatherConditionSleet,
+    HKWeatherConditionFreezingDrizzle,
+    HKWeatherConditionFreezingRain,
+    HKWeatherConditionMixedRainAndHail,
+    HKWeatherConditionMixedRainAndSnow,
+    HKWeatherConditionMixedRainAndSleet,
+    HKWeatherConditionMixedSnowAndSleet,
+    HKWeatherConditionDrizzle,
+    HKWeatherConditionScatteredShowers,
+    HKWeatherConditionShowers,
+    HKWeatherConditionThunderstorms,
+    HKWeatherConditionTropicalStorm,
+    HKWeatherConditionHurricane,
+    HKWeatherConditionTornado,
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
+
+/*!
+ @constant      HKMetadataKeyWeatherCondition
+ @abstract      Represents the weather condition during the sample.
+ @discussion    The expected value type is an NSNumber containing an HKWeatherCondition value. This key may be set on an
+                HKWorkout object to represent the overall weather condition during the workout.
+ */
+HK_EXTERN NSString * const HKMetadataKeyWeatherCondition HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
+
+/*!
+ @constant      HKMetadataKeyWeatherTemperature
+ @abstract      Represents the weather temperature during the sample.
+ @discussion    The expected value type is an HKQuantity expressed in a temperature unit. This key may be set on an
+                HKWorkout object to represent the overall temperature during the workout.
+ */
+HK_EXTERN NSString * const HKMetadataKeyWeatherTemperature HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
+
+/*!
+ @constant      HKMetadataKeyHumidity
+ @abstract      Represents the weather humidity during the sample.
+ @discussion    The expected value type is an HKQuantity expressed in percent. This key may be set on an HKWorkout
+                object to represent the overall humidity during the workout.
+ */
+HK_EXTERN NSString * const HKMetadataKeyWeatherHumidity HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
 
 /*!
  @constant      HKMetadataKeySexualActivityProtectionUsed
@@ -192,7 +247,7 @@
                 protection from STIs or protection from pregnancy.
  @discussion    The expected value type is an NSNumber containing a BOOL value.
  */
-HK_EXTERN NSString * const HKMetadataKeySexualActivityProtectionUsed NS_AVAILABLE_IOS(9_0);
+HK_EXTERN NSString * const HKMetadataKeySexualActivityProtectionUsed HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @constant      HKMetadataKeyMenstrualCycleStart
@@ -200,6 +255,6 @@
                 metadata key for category samples of type HKCategorySampleMenstrualFlow.
  @discussion    The expected value type is an NSNumber containing a BOOL value.
  */
-HK_EXTERN NSString * const HKMetadataKeyMenstrualCycleStart NS_AVAILABLE_IOS(9_0);
+HK_EXTERN NSString * const HKMetadataKeyMenstrualCycleStart HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKObject.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKObject.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKObject.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKObject.h	2016-06-05 05:29:10.000000000 +0200
@@ -14,7 +14,7 @@
 @class HKSourceRevision;
 @class HKDevice;
 
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKObject : NSObject <NSSecureCoding>
 
 /*!
@@ -29,19 +29,19 @@
  @property      sourceRevision
  @abstract      Represents the revision of the source responsible for saving the receiver.
  */
-@property (readonly, strong) HKSourceRevision *sourceRevision NS_AVAILABLE_IOS(9_0);
+@property (readonly, strong) HKSourceRevision *sourceRevision HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @property      device
  @abstract      Represents the device that generated the data of the receiver.
  */
-@property (readonly, strong, nullable) HKDevice *device NS_AVAILABLE_IOS(9_0);
+@property (readonly, strong, nullable) HKDevice *device HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @property      metadata
  @abstract      Extra information describing properties of the receiver.
- @discussion    Keys must be NSString and values must be either NSString, NSNumber, or NSDate.
-                See HKMetadata.h for potential metadata keys and values.
+ @discussion    Keys must be NSString and values must be either NSString, NSNumber, NSDate, or
+                HKQuantity. See HKMetadata.h for potential metadata keys and values.
  */
 @property (readonly, copy, nullable) NSDictionary<NSString *, id> *metadata;
 
@@ -50,12 +50,12 @@
 @end
 
 // Predicate Key Paths
-HK_EXTERN NSString * const HKPredicateKeyPathUUID NS_AVAILABLE_IOS(8_0);
-HK_EXTERN NSString * const HKPredicateKeyPathSource NS_AVAILABLE_IOS(8_0);
-HK_EXTERN NSString * const HKPredicateKeyPathMetadata NS_AVAILABLE_IOS(8_0);
-HK_EXTERN NSString * const HKPredicateKeyPathCorrelation NS_AVAILABLE_IOS(8_0);
-HK_EXTERN NSString * const HKPredicateKeyPathWorkout NS_AVAILABLE_IOS(8_0);
-HK_EXTERN NSString * const HKPredicateKeyPathDevice NS_AVAILABLE_IOS(9_0);
-HK_EXTERN NSString * const HKPredicateKeyPathSourceRevision NS_AVAILABLE_IOS(9_0);
+HK_EXTERN NSString * const HKPredicateKeyPathUUID HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+HK_EXTERN NSString * const HKPredicateKeyPathSource HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+HK_EXTERN NSString * const HKPredicateKeyPathMetadata HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+HK_EXTERN NSString * const HKPredicateKeyPathCorrelation HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+HK_EXTERN NSString * const HKPredicateKeyPathWorkout HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+HK_EXTERN NSString * const HKPredicateKeyPathDevice HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
+HK_EXTERN NSString * const HKPredicateKeyPathSourceRevision HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKObjectType.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKObjectType.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKObjectType.h	2016-02-23 04:42:22.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKObjectType.h	2016-06-05 05:29:10.000000000 +0200
@@ -14,6 +14,7 @@
 @class HKCategoryType;
 @class HKCharacteristicType;
 @class HKCorrelationType;
+@class HKDocumentType;
 @class HKQuantityType;
 @class HKUnit;
 @class HKWorkoutType;
@@ -22,7 +23,7 @@
  @class         HKObjectType
  @abstract      An abstract class representing a type of object that can be stored by HealthKit.
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKObjectType : NSObject <NSSecureCoding, NSCopying>
 
 /*!
@@ -34,20 +35,21 @@
 
 - (instancetype)init NS_UNAVAILABLE;
 
-+ (nullable HKQuantityType *)quantityTypeForIdentifier:(NSString *)identifier;
-+ (nullable HKCategoryType *)categoryTypeForIdentifier:(NSString *)identifier;
-+ (nullable HKCharacteristicType *)characteristicTypeForIdentifier:(NSString *)identifier;
-+ (nullable HKCorrelationType *)correlationTypeForIdentifier:(NSString *)identifier;
++ (nullable HKQuantityType *)quantityTypeForIdentifier:(HKQuantityTypeIdentifier)identifier;
++ (nullable HKCategoryType *)categoryTypeForIdentifier:(HKCategoryTypeIdentifier)identifier;
++ (nullable HKCharacteristicType *)characteristicTypeForIdentifier:(HKCharacteristicTypeIdentifier)identifier;
++ (nullable HKCorrelationType *)correlationTypeForIdentifier:(HKCorrelationTypeIdentifier)identifier;
++ (nullable HKDocumentType *)documentTypeForIdentifier:(HKDocumentTypeIdentifier)identifier HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
 + (HKWorkoutType *)workoutType;
-+ (HKActivitySummaryType *)activitySummaryType NS_AVAILABLE_IOS(9_3);
++ (HKActivitySummaryType *)activitySummaryType HK_AVAILABLE_IOS_WATCHOS(9_3, 2_2);
 
 @end
 
 /*!
  @class         HKCharacteristicType
- @abstract      Represents a type of object that desribes a characteristic of the user (such as date of birth).
+ @abstract      Represents a type of object that describes a characteristic of the user (such as date of birth).
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKCharacteristicType : HKObjectType
 @end
 
@@ -55,7 +57,7 @@
  @class         HKSampleType
  @abstract      Represents a type of HKSample.
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKSampleType : HKObjectType
 @end
 
@@ -63,7 +65,7 @@
  @class         HKCategoryType
  @abstract      Represent a type of HKCategorySample.
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKCategoryType : HKSampleType
 @end
 
@@ -71,7 +73,7 @@
  @class         HKCorrelationType
  @abstract      Represents a type of HKCorrelation
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKCorrelationType : HKSampleType
 @end
 
@@ -85,13 +87,21 @@
 typedef NS_ENUM(NSInteger, HKQuantityAggregationStyle) {
     HKQuantityAggregationStyleCumulative = 0,
     HKQuantityAggregationStyleDiscrete,
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+
+/*!
+ @class         HKDocumentType
+ @abstract      Represents a type of HKDocument.
+ */
+HK_CLASS_AVAILABLE_IOS_ONLY(10_0)
+@interface HKDocumentType : HKSampleType
+@end
 
 /*!
  @class         HKQuantityType
  @abstract      Represents types of HKQuantitySamples.
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKQuantityType : HKSampleType
 
 @property (readonly) HKQuantityAggregationStyle aggregationStyle;
@@ -109,7 +119,7 @@
  @class         HKCategoryType
  @abstract      Represents a workout or exercise
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKWorkoutType : HKSampleType
 @end
 
@@ -121,4 +131,5 @@
 @interface HKActivitySummaryType : HKObjectType
 @end
 
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKObserverQuery.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKObserverQuery.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKObserverQuery.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKObserverQuery.h	2016-06-05 05:29:10.000000000 +0200
@@ -11,7 +11,7 @@
 
 typedef void(^HKObserverQueryCompletionHandler)(void);
 
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKObserverQuery : HKQuery
 
 /*!
@@ -24,7 +24,7 @@
 
 - (instancetype)initWithSampleType:(HKSampleType *)sampleType
                          predicate:(nullable NSPredicate *)predicate
-                     updateHandler:(void(^)(HKObserverQuery *query, HKObserverQueryCompletionHandler completionHandler, NSError * __nullable error))updateHandler;
+                     updateHandler:(void(^)(HKObserverQuery *query, HKObserverQueryCompletionHandler completionHandler, NSError * _Nullable error))updateHandler;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuantity.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuantity.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuantity.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuantity.h	2016-06-05 05:29:10.000000000 +0200
@@ -15,7 +15,7 @@
  @class         HKQuantity
  @abstract      The HKQuantity class provides an encapsulation of a quantity value and the unit of measurement.
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKQuantity : NSObject <NSSecureCoding, NSCopying>
 
 - (instancetype)init NS_UNAVAILABLE;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuantitySample.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuantitySample.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuantitySample.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuantitySample.h	2016-06-05 05:29:10.000000000 +0200
@@ -16,7 +16,7 @@
  @class         HKQuantitySample
  @abstract      An HKObject subclass representing a quantity measurement.
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKQuantitySample : HKSample
 
 @property (readonly, strong) HKQuantityType *quantityType;
@@ -61,11 +61,11 @@
                              startDate:(NSDate *)startDate
                                endDate:(NSDate *)endDate
                                 device:(nullable HKDevice *)device
-                              metadata:(nullable NSDictionary<NSString *, id> *)metadata NS_AVAILABLE_IOS(9_0);
+                              metadata:(nullable NSDictionary<NSString *, id> *)metadata HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 @end
 
 // Predicate Key Paths
-HK_EXTERN NSString * const HKPredicateKeyPathQuantity NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKPredicateKeyPathQuantity HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuery.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuery.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuery.h	2016-02-23 04:42:22.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKQuery.h	2016-05-28 06:22:21.000000000 +0200
@@ -16,7 +16,7 @@
 @class HKSampleType;
 @class HKSource;
 
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKQuery : NSObject
 
 @property (readonly, strong, nullable) HKObjectType *objectType HK_AVAILABLE_IOS_WATCHOS(9_3, 2_2);
@@ -41,7 +41,7 @@
     HKQueryOptionNone               = 0,
     HKQueryOptionStrictStartDate    = 1 << 0,
     HKQueryOptionStrictEndDate      = 1 << 1,
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 
 @interface HKQuery (HKObjectPredicates)
@@ -103,7 +103,7 @@
  
  @param         sourceRevisions The list of source revisions.
  */
-+ (NSPredicate *)predicateForObjectsFromSourceRevisions:(NSSet<HKSourceRevision *> *)sourceRevisions NS_AVAILABLE_IOS(9_0);
++ (NSPredicate *)predicateForObjectsFromSourceRevisions:(NSSet<HKSourceRevision *> *)sourceRevisions HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @method        predicateForObjectsFromDevices:
@@ -114,7 +114,7 @@
  
  @param         devices     The set of devices that generated data.
  */
-+ (NSPredicate *)predicateForObjectsFromDevices:(NSSet<HKDevice *> *)devices NS_AVAILABLE_IOS(9_0);
++ (NSPredicate *)predicateForObjectsFromDevices:(NSSet<HKDevice *> *)devices HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @method        predicateForObjectsWithDeviceProperty:allowedValues:
@@ -127,7 +127,7 @@
  @param         allowedValues   The set of values for which the device property can match. An empty set will match all
                 devices whose property value is nil.
  */
-+ (NSPredicate *)predicateForObjectsWithDeviceProperty:(NSString *)key allowedValues:(NSSet<NSString *> *)allowedValues NS_AVAILABLE_IOS(9_0);
++ (NSPredicate *)predicateForObjectsWithDeviceProperty:(NSString *)key allowedValues:(NSSet<NSString *> *)allowedValues HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @method        predicateForObjectWithUUID:
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSample.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSample.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSample.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSample.h	2016-06-05 05:29:10.000000000 +0200
@@ -15,7 +15,7 @@
  @class         HKSample
  @abstract      An abstract class representing measurements taken over a period of time.
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKSample : HKObject
 
 @property (readonly, strong) HKSampleType *sampleType;
@@ -26,11 +26,11 @@
 @end
 
 // Sort Identifiers
-HK_EXTERN NSString * const HKSampleSortIdentifierStartDate NS_AVAILABLE_IOS(8_0);
-HK_EXTERN NSString * const HKSampleSortIdentifierEndDate NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKSampleSortIdentifierStartDate HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+HK_EXTERN NSString * const HKSampleSortIdentifierEndDate HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 // Predicate Key Paths
-HK_EXTERN NSString * const HKPredicateKeyPathStartDate NS_AVAILABLE_IOS(8_0);
-HK_EXTERN NSString * const HKPredicateKeyPathEndDate NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKPredicateKeyPathStartDate HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+HK_EXTERN NSString * const HKPredicateKeyPathEndDate HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSampleQuery.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSampleQuery.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSampleQuery.h	2016-02-23 04:42:22.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSampleQuery.h	2016-06-05 05:29:10.000000000 +0200
@@ -5,7 +5,6 @@
 //  Copyright (c) 2014 Apple Inc. All rights reserved.
 //
 
-#import <HealthKit/HealthKit.h>
 #import <HealthKit/HKQuery.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -17,7 +16,7 @@
  @class         HKSampleQuery
  @abstract      A concrete subclass of HKQuery that provides an interface to retrieve HKSample objects.
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKSampleQuery : HKQuery
 
 /*!
@@ -46,7 +45,7 @@
                          predicate:(nullable NSPredicate *)predicate
                              limit:(NSUInteger)limit
                    sortDescriptors:(nullable NSArray<NSSortDescriptor *> *)sortDescriptors
-                    resultsHandler:(void(^)(HKSampleQuery *query, NSArray<__kindof HKSample *> * __nullable results, NSError * __nullable error))resultsHandler;
+                    resultsHandler:(void(^)(HKSampleQuery *query, NSArray<__kindof HKSample *> * _Nullable results, NSError * _Nullable error))resultsHandler;
 
 
 @end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSource.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSource.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSource.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSource.h	2016-06-05 05:29:10.000000000 +0200
@@ -13,7 +13,7 @@
  @class     HKSource
  @abstract  Represents the entity that created an object stored by HealthKit.
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKSource : NSObject <NSSecureCoding, NSCopying>
 
 /*!
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSourceQuery.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSourceQuery.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSourceQuery.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSourceQuery.h	2016-06-05 05:29:10.000000000 +0200
@@ -13,7 +13,7 @@
  @class         HKSourceQuery
  @abstract      A query that returns a set of sources that have saved objects matching certain criteria.
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKSourceQuery : HKQuery
 
 /*!
@@ -27,7 +27,7 @@
  */
 - (instancetype)initWithSampleType:(HKSampleType *)sampleType
                    samplePredicate:(nullable NSPredicate *)objectPredicate
-                 completionHandler:(void(^)(HKSourceQuery *query, NSSet<HKSource *> * __nullable sources, NSError * __nullable error))completionHandler;
+                 completionHandler:(void(^)(HKSourceQuery *query, NSSet<HKSource *> * _Nullable sources, NSError * _Nullable error))completionHandler;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSourceRevision.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSourceRevision.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSourceRevision.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKSourceRevision.h	2016-06-05 05:29:10.000000000 +0200
@@ -16,7 +16,7 @@
  @abstract      Represents a specific revision of an HKSource.
  */
 
-HK_CLASS_AVAILABLE_IOS(9_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(9_0, 2_0)
 @interface HKSourceRevision : NSObject <NSSecureCoding, NSCopying>
 
 /*!
@@ -36,7 +36,7 @@
  @method        initWithSource:version:
  @abstract      Initializes a new HKSourceRevision with the given source and version.
  */
-- (instancetype)initWithSource:(HKSource *)source version:(NSString *)version;
+- (instancetype)initWithSource:(HKSource *)source version:(nullable NSString *)version;
 
 - (instancetype)init NS_UNAVAILABLE;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKStatistics.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKStatistics.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKStatistics.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKStatistics.h	2016-05-28 05:54:34.000000000 +0200
@@ -37,13 +37,13 @@
     HKStatisticsOptionDiscreteMin               = 1 << 2,
     HKStatisticsOptionDiscreteMax               = 1 << 3,
     HKStatisticsOptionCumulativeSum             = 1 << 4,
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @class         HKStatistics
  @abstract      Represents statistics for quantity samples over a period of time.
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKStatistics : NSObject <NSSecureCoding, NSCopying>
 
 @property (readonly, strong) HKQuantityType *quantityType;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKStatisticsCollectionQuery.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKStatisticsCollectionQuery.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKStatisticsCollectionQuery.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKStatisticsCollectionQuery.h	2016-06-05 05:29:10.000000000 +0200
@@ -12,7 +12,7 @@
 
 @class HKStatistics;
 
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKStatisticsCollection : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
@@ -49,15 +49,15 @@
 
 @end
 
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKStatisticsCollectionQuery : HKQuery
 
 @property (readonly, strong) NSDate *anchorDate;
 @property (readonly) HKStatisticsOptions options;
 @property (readonly, copy) NSDateComponents *intervalComponents;
 
-@property (nonatomic, copy, nullable) void(^initialResultsHandler)(HKStatisticsCollectionQuery *query, HKStatisticsCollection * __nullable result, NSError * __nullable error);
-@property (nonatomic, copy, nullable) void(^statisticsUpdateHandler)(HKStatisticsCollectionQuery *query, HKStatistics * __nullable statistics, HKStatisticsCollection * __nullable collection, NSError * __nullable error);
+@property (nonatomic, copy, nullable) void(^initialResultsHandler)(HKStatisticsCollectionQuery *query, HKStatisticsCollection * _Nullable result, NSError * _Nullable error);
+@property (nonatomic, copy, nullable) void(^statisticsUpdateHandler)(HKStatisticsCollectionQuery *query, HKStatistics * _Nullable statistics, HKStatisticsCollection * _Nullable collection, NSError * _Nullable error);
 
 - (instancetype)initWithQuantityType:(HKQuantityType *)quantityType
              quantitySamplePredicate:(nullable NSPredicate *)quantitySamplePredicate
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKStatisticsQuery.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKStatisticsQuery.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKStatisticsQuery.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKStatisticsQuery.h	2016-06-05 05:29:10.000000000 +0200
@@ -16,13 +16,13 @@
  @class     HKStatisticsQuery
  @abstract  Calculates statistics on quantity samples matching the given quantity type and predicate.
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKStatisticsQuery : HKQuery
 
 - (instancetype)initWithQuantityType:(HKQuantityType *)quantityType
              quantitySamplePredicate:(nullable NSPredicate *)quantitySamplePredicate
                              options:(HKStatisticsOptions)options
-                   completionHandler:(void(^)(HKStatisticsQuery *query, HKStatistics * __nullable result, NSError * __nullable error))handler;
+                   completionHandler:(void(^)(HKStatisticsQuery *query, HKStatistics * _Nullable result, NSError * _Nullable error))handler;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKTypeIdentifiers.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKTypeIdentifiers.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKTypeIdentifiers.h	2016-02-23 04:42:22.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKTypeIdentifiers.h	2016-05-28 06:22:22.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <HealthKit/HKDefines.h>
+#import <objc/NSObjCRuntime.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -13,120 +14,139 @@
 /*   HKQuantityType Identifiers   */
 /*--------------------------------*/
 
+typedef NSString * HKQuantityTypeIdentifier NS_STRING_ENUM;
+
 // Body Measurements
-HK_EXTERN NSString * const HKQuantityTypeIdentifierBodyMassIndex NS_AVAILABLE_IOS(8_0);             // Scalar(Count),               Discrete
-HK_EXTERN NSString * const HKQuantityTypeIdentifierBodyFatPercentage NS_AVAILABLE_IOS(8_0);         // Scalar(Percent, 0.0 - 1.0),  Discrete
-HK_EXTERN NSString * const HKQuantityTypeIdentifierHeight NS_AVAILABLE_IOS(8_0);                    // Length,                      Discrete
-HK_EXTERN NSString * const HKQuantityTypeIdentifierBodyMass NS_AVAILABLE_IOS(8_0);                  // Mass,                        Discrete
-HK_EXTERN NSString * const HKQuantityTypeIdentifierLeanBodyMass NS_AVAILABLE_IOS(8_0);              // Mass,                        Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierBodyMassIndex HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);             // Scalar(Count),               Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierBodyFatPercentage HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);         // Scalar(Percent, 0.0 - 1.0),  Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierHeight HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);                    // Length,                      Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierBodyMass HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);                  // Mass,                        Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierLeanBodyMass HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);              // Mass,                        Discrete
 
 // Fitness
-HK_EXTERN NSString * const HKQuantityTypeIdentifierStepCount NS_AVAILABLE_IOS(8_0);                 // Scalar(Count),               Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDistanceWalkingRunning NS_AVAILABLE_IOS(8_0);    // Length,                      Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDistanceCycling NS_AVAILABLE_IOS(8_0);           // Length,                      Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierBasalEnergyBurned NS_AVAILABLE_IOS(8_0);         // Energy,                      Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierActiveEnergyBurned NS_AVAILABLE_IOS(8_0);        // Energy,                      Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierFlightsClimbed NS_AVAILABLE_IOS(8_0);            // Scalar(Count),               Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierNikeFuel NS_AVAILABLE_IOS(8_0);                  // Scalar(Count),               Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierAppleExerciseTime HK_AVAILABLE_IOS_WATCHOS(9_3, 2_2);    // Time                         Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierStepCount HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);                 // Scalar(Count),               Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDistanceWalkingRunning HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);    // Length,                      Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDistanceCycling HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);           // Length,                      Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDistanceWheelchair HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);       // Length,               Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierBasalEnergyBurned HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);         // Energy,                      Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierActiveEnergyBurned HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);        // Energy,                      Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierFlightsClimbed HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);            // Scalar(Count),               Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierNikeFuel HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);                  // Scalar(Count),               Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierAppleExerciseTime HK_AVAILABLE_IOS_WATCHOS(9_3, 2_2);         // Time                         Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierPushCount HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);                // Scalar(Count),               Cumulative
 
 // Vitals
-HK_EXTERN NSString * const HKQuantityTypeIdentifierHeartRate NS_AVAILABLE_IOS(8_0);                 // Scalar(Count)/Time,          Discrete
-HK_EXTERN NSString * const HKQuantityTypeIdentifierBodyTemperature NS_AVAILABLE_IOS(8_0);           // Temperature,                 Discrete
-HK_EXTERN NSString * const HKQuantityTypeIdentifierBasalBodyTemperature NS_AVAILABLE_IOS(9_0);      // Basal Body Temperature,      Discrete
-HK_EXTERN NSString * const HKQuantityTypeIdentifierBloodPressureSystolic NS_AVAILABLE_IOS(8_0);     // Pressure,                    Discrete
-HK_EXTERN NSString * const HKQuantityTypeIdentifierBloodPressureDiastolic NS_AVAILABLE_IOS(8_0);    // Pressure,                    Discrete
-HK_EXTERN NSString * const HKQuantityTypeIdentifierRespiratoryRate NS_AVAILABLE_IOS(8_0);           // Scalar(Count)/Time,          Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierHeartRate HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);                 // Scalar(Count)/Time,          Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierBodyTemperature HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);           // Temperature,                 Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierBasalBodyTemperature HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);                   // Basal Body Temperature,      Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierBloodPressureSystolic HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);     // Pressure,                    Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierBloodPressureDiastolic HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);    // Pressure,                    Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierRespiratoryRate HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);           // Scalar(Count)/Time,          Discrete
 
 // Results
-HK_EXTERN NSString * const HKQuantityTypeIdentifierOxygenSaturation NS_AVAILABLE_IOS(8_0);          // Scalar (Percent, 0.0 - 1.0,  Discrete
-HK_EXTERN NSString * const HKQuantityTypeIdentifierPeripheralPerfusionIndex NS_AVAILABLE_IOS(8_0);  // Scalar(Percent, 0.0 - 1.0),  Discrete
-HK_EXTERN NSString * const HKQuantityTypeIdentifierBloodGlucose NS_AVAILABLE_IOS(8_0);              // Mass/Volume,                 Discrete
-HK_EXTERN NSString * const HKQuantityTypeIdentifierNumberOfTimesFallen NS_AVAILABLE_IOS(8_0);       // Scalar(Count),               Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierElectrodermalActivity NS_AVAILABLE_IOS(8_0);     // Conductance,                 Discrete
-HK_EXTERN NSString * const HKQuantityTypeIdentifierInhalerUsage NS_AVAILABLE_IOS(8_0);              // Scalar(Count),               Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierBloodAlcoholContent NS_AVAILABLE_IOS(8_0);       // Scalar(Percent, 0.0 - 1.0),  Discrete
-HK_EXTERN NSString * const HKQuantityTypeIdentifierForcedVitalCapacity NS_AVAILABLE_IOS(8_0);       // Volume,                      Discrete
-HK_EXTERN NSString * const HKQuantityTypeIdentifierForcedExpiratoryVolume1 NS_AVAILABLE_IOS(8_0);   // Volume,                      Discrete
-HK_EXTERN NSString * const HKQuantityTypeIdentifierPeakExpiratoryFlowRate NS_AVAILABLE_IOS(8_0);    // Volume/Time,                 Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierOxygenSaturation HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);          // Scalar (Percent, 0.0 - 1.0,  Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierPeripheralPerfusionIndex HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);  // Scalar(Percent, 0.0 - 1.0),  Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierBloodGlucose HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);              // Mass/Volume,                 Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierNumberOfTimesFallen HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);       // Scalar(Count),               Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierElectrodermalActivity HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);     // Conductance,                 Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierInhalerUsage HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);              // Scalar(Count),               Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierBloodAlcoholContent HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);       // Scalar(Percent, 0.0 - 1.0),  Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierForcedVitalCapacity HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);       // Volume,                      Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierForcedExpiratoryVolume1 HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);   // Volume,                      Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierPeakExpiratoryFlowRate HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);    // Volume/Time,                 Discrete
 
 // Nutrition
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryFatTotal NS_AVAILABLE_IOS(8_0);           // Mass,   Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryFatPolyunsaturated NS_AVAILABLE_IOS(8_0); // Mass,   Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryFatMonounsaturated NS_AVAILABLE_IOS(8_0); // Mass,   Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryFatSaturated NS_AVAILABLE_IOS(8_0);       // Mass,   Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryCholesterol NS_AVAILABLE_IOS(8_0);        // Mass,   Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietarySodium NS_AVAILABLE_IOS(8_0);             // Mass,   Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryCarbohydrates NS_AVAILABLE_IOS(8_0);      // Mass,   Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryFiber NS_AVAILABLE_IOS(8_0);              // Mass,   Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietarySugar NS_AVAILABLE_IOS(8_0);              // Mass,   Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryEnergyConsumed NS_AVAILABLE_IOS(8_0);     // Energy, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryProtein NS_AVAILABLE_IOS(8_0);            // Mass,   Cumulative
-
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryVitaminA NS_AVAILABLE_IOS(8_0);           // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryVitaminB6 NS_AVAILABLE_IOS(8_0);          // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryVitaminB12 NS_AVAILABLE_IOS(8_0);         // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryVitaminC NS_AVAILABLE_IOS(8_0);           // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryVitaminD NS_AVAILABLE_IOS(8_0);           // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryVitaminE NS_AVAILABLE_IOS(8_0);           // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryVitaminK NS_AVAILABLE_IOS(8_0);           // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryCalcium NS_AVAILABLE_IOS(8_0);            // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryIron NS_AVAILABLE_IOS(8_0);               // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryThiamin NS_AVAILABLE_IOS(8_0);            // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryRiboflavin NS_AVAILABLE_IOS(8_0);         // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryNiacin NS_AVAILABLE_IOS(8_0);             // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryFolate NS_AVAILABLE_IOS(8_0);             // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryBiotin NS_AVAILABLE_IOS(8_0);             // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryPantothenicAcid NS_AVAILABLE_IOS(8_0);    // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryPhosphorus NS_AVAILABLE_IOS(8_0);         // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryIodine NS_AVAILABLE_IOS(8_0);             // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryMagnesium NS_AVAILABLE_IOS(8_0);          // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryZinc NS_AVAILABLE_IOS(8_0);               // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietarySelenium NS_AVAILABLE_IOS(8_0);           // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryCopper NS_AVAILABLE_IOS(8_0);             // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryManganese NS_AVAILABLE_IOS(8_0);          // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryChromium NS_AVAILABLE_IOS(8_0);           // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryMolybdenum NS_AVAILABLE_IOS(8_0);         // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryChloride NS_AVAILABLE_IOS(8_0);           // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryPotassium NS_AVAILABLE_IOS(8_0);          // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryCaffeine NS_AVAILABLE_IOS(8_0);           // Mass, Cumulative
-HK_EXTERN NSString * const HKQuantityTypeIdentifierDietaryWater NS_AVAILABLE_IOS(9_0);              // Volume, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryFatTotal HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);           // Mass,   Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryFatPolyunsaturated HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0); // Mass,   Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryFatMonounsaturated HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0); // Mass,   Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryFatSaturated HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);       // Mass,   Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryCholesterol HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);        // Mass,   Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietarySodium HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);             // Mass,   Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryCarbohydrates HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);      // Mass,   Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryFiber HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);              // Mass,   Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietarySugar HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);              // Mass,   Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryEnergyConsumed HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);     // Energy, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryProtein HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);            // Mass,   Cumulative
+
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryVitaminA HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);           // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryVitaminB6 HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);          // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryVitaminB12 HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);         // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryVitaminC HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);           // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryVitaminD HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);           // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryVitaminE HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);           // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryVitaminK HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);           // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryCalcium HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);            // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryIron HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);               // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryThiamin HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);            // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryRiboflavin HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);         // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryNiacin HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);             // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryFolate HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);             // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryBiotin HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);             // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryPantothenicAcid HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);    // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryPhosphorus HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);         // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryIodine HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);             // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryMagnesium HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);          // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryZinc HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);               // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietarySelenium HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);           // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryCopper HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);             // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryManganese HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);          // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryChromium HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);           // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryMolybdenum HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);         // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryChloride HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);           // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryPotassium HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);          // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryCaffeine HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);           // Mass, Cumulative
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierDietaryWater HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);              // Volume, Cumulative
 
-HK_EXTERN NSString * const HKQuantityTypeIdentifierUVExposure NS_AVAILABLE_IOS(9_0);                // Scalar (Count), Discrete
+HK_EXTERN HKQuantityTypeIdentifier const HKQuantityTypeIdentifierUVExposure HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);                // Scalar (Count), Discrete
 
 /*--------------------------------*/
 /*   HKCategoryType Identifiers   */
 /*--------------------------------*/
 
-HK_EXTERN NSString * const HKCategoryTypeIdentifierSleepAnalysis NS_AVAILABLE_IOS(8_0);             // HKCategoryValueSleepAnalysis
-HK_EXTERN NSString * const HKCategoryTypeIdentifierAppleStandHour NS_AVAILABLE_IOS(9_0);            // HKCategoryValueAppleStandHour
-HK_EXTERN NSString * const HKCategoryTypeIdentifierCervicalMucusQuality NS_AVAILABLE_IOS(9_0);      // HKCategoryValueCervicalMucusQuality
-HK_EXTERN NSString * const HKCategoryTypeIdentifierOvulationTestResult NS_AVAILABLE_IOS(9_0);       // HKCategoryValueOvulationTestResult
-HK_EXTERN NSString * const HKCategoryTypeIdentifierMenstrualFlow NS_AVAILABLE_IOS(9_0);             // HKCategoryValueMenstrualFlow
-HK_EXTERN NSString * const HKCategoryTypeIdentifierIntermenstrualBleeding NS_AVAILABLE_IOS(9_0);    // (Spotting) HKCategoryValue
-HK_EXTERN NSString * const HKCategoryTypeIdentifierSexualActivity NS_AVAILABLE_IOS(9_0);            // HKCategoryValue
+typedef NSString * HKCategoryTypeIdentifier NS_STRING_ENUM;
 
+HK_EXTERN HKCategoryTypeIdentifier const HKCategoryTypeIdentifierSleepAnalysis HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);             // HKCategoryValueSleepAnalysis
+HK_EXTERN HKCategoryTypeIdentifier const HKCategoryTypeIdentifierAppleStandHour HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);            // HKCategoryValueAppleStandHour
+HK_EXTERN HKCategoryTypeIdentifier const HKCategoryTypeIdentifierCervicalMucusQuality HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);      // HKCategoryValueCervicalMucusQuality
+HK_EXTERN HKCategoryTypeIdentifier const HKCategoryTypeIdentifierOvulationTestResult HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);       // HKCategoryValueOvulationTestResult
+HK_EXTERN HKCategoryTypeIdentifier const HKCategoryTypeIdentifierMenstrualFlow HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);             // HKCategoryValueMenstrualFlow
+HK_EXTERN HKCategoryTypeIdentifier const HKCategoryTypeIdentifierIntermenstrualBleeding HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);    // (Spotting) HKCategoryValue
+HK_EXTERN HKCategoryTypeIdentifier const HKCategoryTypeIdentifierSexualActivity HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);            // HKCategoryValue
+HK_EXTERN HKCategoryTypeIdentifier const HKCategoryTypeIdentifierMindfulSession HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);           // HKCategoryValue
 
 /*--------------------------------------*/
 /*   HKCharacteristicType Identifiers   */
 /*--------------------------------------*/
 
-HK_EXTERN NSString * const HKCharacteristicTypeIdentifierBiologicalSex NS_AVAILABLE_IOS(8_0); // NSNumber (HKCharacteristicBiologicalSex)
-HK_EXTERN NSString * const HKCharacteristicTypeIdentifierBloodType NS_AVAILABLE_IOS(8_0);     // NSNumber (HKCharacteristicBloodType)
-HK_EXTERN NSString * const HKCharacteristicTypeIdentifierDateOfBirth NS_AVAILABLE_IOS(8_0);   // NSDate
-HK_EXTERN NSString * const HKCharacteristicTypeIdentifierFitzpatrickSkinType NS_AVAILABLE_IOS(9_0); // HKFitzpatrickSkinType
+typedef NSString * HKCharacteristicTypeIdentifier NS_STRING_ENUM;
+
+HK_EXTERN HKCharacteristicTypeIdentifier const HKCharacteristicTypeIdentifierBiologicalSex HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);          // HKBiologicalSexObject
+HK_EXTERN HKCharacteristicTypeIdentifier const HKCharacteristicTypeIdentifierBloodType HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);              // HKBloodTypeObject
+HK_EXTERN HKCharacteristicTypeIdentifier const HKCharacteristicTypeIdentifierDateOfBirth HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);            // NSDateComponents
+HK_EXTERN HKCharacteristicTypeIdentifier const HKCharacteristicTypeIdentifierFitzpatrickSkinType HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);    // HKFitzpatrickSkinTypeObject
+HK_EXTERN HKCharacteristicTypeIdentifier const HKCharacteristicTypeIdentifierWheelchairUse HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);         // HKWheelchairUseObject
 
 /*-----------------------------------*/
 /*   HKCorrelationType Identifiers   */
 /*-----------------------------------*/
 
-HK_EXTERN NSString * const HKCorrelationTypeIdentifierBloodPressure NS_AVAILABLE_IOS(8_0);
-HK_EXTERN NSString * const HKCorrelationTypeIdentifierFood NS_AVAILABLE_IOS(8_0);
+typedef NSString * HKCorrelationTypeIdentifier NS_STRING_ENUM;
+
+HK_EXTERN HKCorrelationTypeIdentifier const HKCorrelationTypeIdentifierBloodPressure HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+HK_EXTERN HKCorrelationTypeIdentifier const HKCorrelationTypeIdentifierFood HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+
+/*--------------------------------*/
+/*   HKDocumentType Identifiers   */
+/*--------------------------------*/
+
+typedef NSString * HKDocumentTypeIdentifier NS_STRING_ENUM;
+
+HK_EXTERN HKDocumentTypeIdentifier const HKDocumentTypeIdentifierCDA HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
 
 /*------------------------------*/
 /*   HKWorkoutType Identifier   */
 /*------------------------------*/
 
-HK_EXTERN NSString * const HKWorkoutTypeIdentifier NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKWorkoutTypeIdentifier HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKUnit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKUnit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKUnit.h	2016-02-26 05:11:45.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKUnit.h	2016-05-28 05:54:34.000000000 +0200
@@ -9,7 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKUnit : NSObject <NSSecureCoding, NSCopying>
 
 /// Returns a unique string representation for the unit that could be used with +unitFromString:
@@ -118,7 +118,7 @@
     HKMetricPrefixMega,     //10^6
     HKMetricPrefixGiga,     //10^9
     HKMetricPrefixTera      //10^12
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /* Mass Units */
 @interface HKUnit (Mass)
@@ -137,7 +137,7 @@
 + (instancetype)meterUnit;  // m
 + (instancetype)inchUnit;   // in
 + (instancetype)footUnit;   // ft
-+ (instancetype)yardUnit NS_AVAILABLE_IOS(9_0);   // yd
++ (instancetype)yardUnit HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);   // yd
 + (instancetype)mileUnit;   // mi
 @end
 
@@ -149,8 +149,8 @@
 + (instancetype)fluidOunceImperialUnit; // fl_oz_imp
 + (instancetype)pintUSUnit;             // pt_us
 + (instancetype)pintImperialUnit;       // pt_imp
-+ (instancetype)cupUSUnit NS_AVAILABLE_IOS(9_0);       // cup_us
-+ (instancetype)cupImperialUnit NS_AVAILABLE_IOS(9_0); // cup_imp
++ (instancetype)cupUSUnit HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);       // cup_us
++ (instancetype)cupImperialUnit HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0); // cup_imp
 @end
 
 /* Pressure Units */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkout.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkout.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkout.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkout.h	2016-06-05 05:29:03.000000000 +0200
@@ -10,7 +10,6 @@
 NS_ASSUME_NONNULL_BEGIN
 
 @class HKQuantity;
-@class HKWorkoutEvent;
 
 /*!
  @enum          HKWorkoutActivityType
@@ -24,14 +23,14 @@
     HKWorkoutActivityTypeBaseball,
     HKWorkoutActivityTypeBasketball,
     HKWorkoutActivityTypeBowling,
-    HKWorkoutActivityTypeBoxing, // Kickboxing, Boxing, etc.
+    HKWorkoutActivityTypeBoxing, // See also HKWorkoutActivityTypeKickboxing.
     HKWorkoutActivityTypeClimbing,
     HKWorkoutActivityTypeCricket,
-    HKWorkoutActivityTypeCrossTraining, // Any mix of cardio and/or strength and/or flexibility
+    HKWorkoutActivityTypeCrossTraining, // Any mix of cardio and/or strength training. See also HKWorkoutActivityTypeCoreTraining and HKWorkoutActivityTypeFlexibility.
     HKWorkoutActivityTypeCurling,
     HKWorkoutActivityTypeCycling,
     HKWorkoutActivityTypeDance,
-    HKWorkoutActivityTypeDanceInspiredTraining, // Pilates, Barre, Feldenkrais, etc.
+    HKWorkoutActivityTypeDanceInspiredTraining NS_ENUM_DEPRECATED_IOS(8_0, 10_0, "Use HKWorkoutActivityTypeDance, HKWorkoutActivityTypeBarre, or HKWorkoutActivityTypePilates"), // This enum remains available to access older data.
     HKWorkoutActivityTypeElliptical,
     HKWorkoutActivityTypeEquestrianSports, // Polo, Horse Racing, Horse Riding, etc.
     HKWorkoutActivityTypeFencing,
@@ -56,11 +55,11 @@
     HKWorkoutActivityTypeRunning,
     HKWorkoutActivityTypeSailing,
     HKWorkoutActivityTypeSkatingSports, // Ice Skating, Speed Skating, Inline Skating, Skateboarding, etc.
-    HKWorkoutActivityTypeSnowSports, // Skiing, Snowboarding, Cross-Country Skiing, etc.
+    HKWorkoutActivityTypeSnowSports, // Sledding, Snowmobiling, Building a Snowman, etc. See also HKWorkoutActivityTypeCrossCountrySkiing, HKWorkoutActivityTypeSnowboarding, and HKWorkoutActivityTypeDownhillSkiing.
     HKWorkoutActivityTypeSoccer,
     HKWorkoutActivityTypeSoftball,
     HKWorkoutActivityTypeSquash,
-    HKWorkoutActivityTypeStairClimbing,
+    HKWorkoutActivityTypeStairClimbing, // See also HKWorkoutActivityTypeStairs and HKWorkoutActivityTypeStepTraining.
     HKWorkoutActivityTypeSurfingSports, // Traditional Surfing, Kite Surfing, Wind Surfing, etc.
     HKWorkoutActivityTypeSwimming,
     HKWorkoutActivityTypeTableTennis,
@@ -75,25 +74,46 @@
     HKWorkoutActivityTypeWrestling,
     HKWorkoutActivityTypeYoga,
     
+    HKWorkoutActivityTypeBarre              HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),    // HKWorkoutActivityTypeDanceInspiredTraining
+    HKWorkoutActivityTypeCoreTraining       HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+    HKWorkoutActivityTypeCrossCountrySkiing HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+    HKWorkoutActivityTypeDownhillSkiing     HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+    HKWorkoutActivityTypeFlexibility        HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+    HKWorkoutActivityTypeHighIntensityIntervalTraining    HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+    HKWorkoutActivityTypeJumpRope           HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+    HKWorkoutActivityTypeKickboxing         HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+    HKWorkoutActivityTypePilates            HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),    // HKWorkoutActivityTypeDanceInspiredTraining
+    HKWorkoutActivityTypeSnowboarding       HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+    HKWorkoutActivityTypeStairs             HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+    HKWorkoutActivityTypeStepTraining       HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+    HKWorkoutActivityTypeWheelchairWalkPace HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+    HKWorkoutActivityTypeWheelchairRunPace  HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+    
     HKWorkoutActivityTypeOther = 3000,
-} NS_ENUM_AVAILABLE_IOS(8_0);
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 typedef NS_ENUM(NSInteger, HKWorkoutEventType) {
     HKWorkoutEventTypePause = 1,
-    HKWorkoutEventTypeResume
-} NS_ENUM_AVAILABLE_IOS(8_0);
+    HKWorkoutEventTypeResume,
+    HKWorkoutEventTypeLap           HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+    HKWorkoutEventTypeMarker        HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+    HKWorkoutEventTypeMotionPaused  HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+    HKWorkoutEventTypeMotionResumed HK_ENUM_AVAILABLE_IOS_WATCHOS(10_0, 3_0),
+} HK_ENUM_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 /*!
  @class         HKWorkoutEvent
  @abstract      Represents a particular event that occurred during a workout
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKWorkoutEvent : NSObject <NSSecureCoding>
 
 @property (readonly, assign) HKWorkoutEventType type;
 @property (readonly, copy) NSDate *date;
+@property (readonly, copy, nullable) NSDictionary<NSString *, id> *metadata HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
 
 + (instancetype)workoutEventWithType:(HKWorkoutEventType)type date:(NSDate *)date;
++ (instancetype)workoutEventWithType:(HKWorkoutEventType)type date:(NSDate *)date metadata:(NSDictionary<NSString *, id> *)metadata HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
 - (instancetype)init NS_UNAVAILABLE;
 
 @end
@@ -102,7 +122,7 @@
  @class         HKWorkout
  @abstract      An HKObject subclass representing a workout or activity
  */
-HK_CLASS_AVAILABLE_IOS(8_0)
+HK_CLASS_AVAILABLE_IOS_WATCHOS(8_0, 2_0)
 @interface HKWorkout : HKSample
 
 /*!
@@ -197,7 +217,7 @@
                       totalEnergyBurned:(nullable HKQuantity *)totalEnergyBurned
                           totalDistance:(nullable HKQuantity *)totalDistance
                                  device:(nullable HKDevice *)device
-                               metadata:(nullable NSDictionary<NSString *, id> *)metadata NS_AVAILABLE_IOS(9_0);
+                               metadata:(nullable NSDictionary<NSString *, id> *)metadata HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 /*!
  @method        workoutWithActivityType:startDate:endDate:duration:totalEnergyBurned:totalDistance:metadata:
@@ -241,19 +261,19 @@
                       totalEnergyBurned:(nullable HKQuantity *)totalEnergyBurned
                           totalDistance:(nullable HKQuantity *)totalDistance
                                  device:(nullable HKDevice *)device
-                               metadata:(nullable NSDictionary<NSString *, id> *)metadata NS_AVAILABLE_IOS(9_0);
+                               metadata:(nullable NSDictionary<NSString *, id> *)metadata HK_AVAILABLE_IOS_WATCHOS(9_0, 2_0);
 
 @end
 
 // Predicate Key Paths
-HK_EXTERN NSString * const HKPredicateKeyPathWorkoutDuration NS_AVAILABLE_IOS(8_0);
-HK_EXTERN NSString * const HKPredicateKeyPathWorkoutTotalDistance NS_AVAILABLE_IOS(8_0);
-HK_EXTERN NSString * const HKPredicateKeyPathWorkoutTotalEnergyBurned NS_AVAILABLE_IOS(8_0);
-HK_EXTERN NSString * const HKPredicateKeyPathWorkoutType NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKPredicateKeyPathWorkoutDuration HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+HK_EXTERN NSString * const HKPredicateKeyPathWorkoutTotalDistance HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+HK_EXTERN NSString * const HKPredicateKeyPathWorkoutTotalEnergyBurned HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+HK_EXTERN NSString * const HKPredicateKeyPathWorkoutType HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 // Sort Identifiers
-HK_EXTERN NSString * const HKWorkoutSortIdentifierDuration NS_AVAILABLE_IOS(8_0);
-HK_EXTERN NSString * const HKWorkoutSortIdentifierTotalDistance NS_AVAILABLE_IOS(8_0);
-HK_EXTERN NSString * const HKWorkoutSortIdentifierTotalEnergyBurned NS_AVAILABLE_IOS(8_0);
+HK_EXTERN NSString * const HKWorkoutSortIdentifierDuration HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+HK_EXTERN NSString * const HKWorkoutSortIdentifierTotalDistance HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
+HK_EXTERN NSString * const HKWorkoutSortIdentifierTotalEnergyBurned HK_AVAILABLE_IOS_WATCHOS(8_0, 2_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkoutSession.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkoutSession.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkoutSession.h	2015-10-03 02:00:28.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HKWorkoutSession.h	2016-06-05 05:29:10.000000000 +0200
@@ -9,6 +9,8 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+@protocol HKWorkoutSessionDelegate;
+
 /*!
  @enum          HKWorkoutSessionState
  @abstract      This enumerated type is used to represent the state of a workout session.
@@ -17,6 +19,7 @@
     HKWorkoutSessionStateNotStarted = 1,
     HKWorkoutSessionStateRunning,
     HKWorkoutSessionStateEnded,
+    HKWorkoutSessionStatePaused HK_AVAILABLE_WATCHOS_ONLY(3_0),
 } HK_AVAILABLE_WATCHOS_ONLY(2_0);
 
 
@@ -45,14 +68,22 @@
  @property      activityType
  @abstract      Indicates the type of workout that will be performed during the session.
  */
-@property (readonly) HKWorkoutActivityType activityType;
+@property (readonly) HKWorkoutActivityType activityType __WATCHOS_DEPRECATED(2_0, 3_0, "Use workoutConfiguration");
 
 /*!
  @property      locationType
  @abstract      Indicates the type of location (indoors vs. outdoors) where the workout will take place.
  @discussion    Knowing the location type allows for more accurate measurements and better performance.
  */
-@property (readonly) HKWorkoutSessionLocationType locationType;
+@property (readonly) HKWorkoutSessionLocationType locationType __WATCHOS_DEPRECATED(2_0, 3_0, "Use workoutConfiguration");
+
+/*!
+ @property      workoutConfiguration
+ @abstract      The configuration object describing the workout.
+ @discussion    This returns a copy of the configuration passed when creating the HKWorkoutSession. Changes made to
+                the returned object have no impact on the HKWorkoutSession.
+ */
+@property (readonly, copy) HKWorkoutConfiguration *workoutConfiguration HK_AVAILABLE_WATCHOS_ONLY(3_0);
 
 /*!
  @property      delegate
@@ -93,7 +124,16 @@
  @param         locationType    The type of location where the workout will be performed.
  */
 - (instancetype)initWithActivityType:(HKWorkoutActivityType)activityType
-                        locationType:(HKWorkoutSessionLocationType)locationType;
+                        locationType:(HKWorkoutSessionLocationType)locationType __WATCHOS_DEPRECATED(2_0, 3_0, "Use initWithConfiguration:error:");
+
+/*!
+ @method        initWithConfiguration:
+
+ @param         workoutConfiguration Configuration object describing the various properties of a workout.
+ @param         error                If the configuration does not specify valid configuration properties, an
+                                     an NSError describing the error is set and nil is returned.
+ */
+- (nullable instancetype)initWithConfiguration:(HKWorkoutConfiguration *)workoutConfiguration error:(NSError **)error HK_AVAILABLE_WATCHOS_ONLY(3_0);
 
 - (instancetype)init NS_UNAVAILABLE;
 
@@ -128,6 +168,17 @@
  */
 - (void)workoutSession:(HKWorkoutSession *)workoutSession didFailWithError:(NSError *)error;
 
+@optional
+
+/*!
+ @method        workoutSession:didGenerateEvent:
+ @abstract      This method is called whenever the system generates a workout event.
+ @discussion    Whenever a workout event is generated, such as pause or resume detection, the event will be passed
+                to the session delegate via this method. Clients may save the generated events to use when creating an
+                HKWorkout object.
+ */
+- (void)workoutSession:(HKWorkoutSession *)workoutSession didGenerateEvent:(HKWorkoutEvent *)event HK_AVAILABLE_IOS_WATCHOS(10_0, 3_0);
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HealthKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HealthKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HealthKit.h	2016-02-23 04:42:22.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HealthKit.framework/Headers/HealthKit.h	2016-06-05 05:29:10.000000000 +0200
@@ -9,11 +9,15 @@
 #import <HealthKit/HKActivitySummaryQuery.h>
 #import <HealthKit/HKAnchoredObjectQuery.h>
 #import <HealthKit/HKCategorySample.h>
+#import <HealthKit/HKCDADocumentSample.h>
+#import <HealthKit/HKCharacteristicObjects.h>
 #import <HealthKit/HKCorrelation.h>
 #import <HealthKit/HKCorrelationQuery.h>
 #import <HealthKit/HKDefines.h>
 #import <HealthKit/HKDeletedObject.h>
 #import <HealthKit/HKDevice.h>
+#import <HealthKit/HKDocumentQuery.h>
+#import <HealthKit/HKDocumentSample.h>
 #import <HealthKit/HKHealthStore.h>
 #import <HealthKit/HKMetadata.h>
 #import <HealthKit/HKObject.h>

```