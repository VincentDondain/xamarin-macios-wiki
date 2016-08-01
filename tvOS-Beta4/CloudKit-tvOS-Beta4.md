#CloudKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKAcceptSharesOperation.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKAcceptSharesOperation.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKAcceptSharesOperation.h	2016-07-11 07:27:39.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKAcceptSharesOperation.h	2016-07-25 07:30:48.000000000 +0200
@@ -30,7 +30,7 @@
  seen all record changes, and may be invoked while the server is processing the side effects
  of those changes.
  */
-@property (nonatomic, copy, nullable) void (^acceptSharesCompletionBlock)(NSError *operationError);
+@property (nonatomic, copy, nullable) void (^acceptSharesCompletionBlock)(NSError * _Nullable operationError);
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h	2016-07-11 07:24:12.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h	2016-07-23 21:07:54.000000000 +0200
@@ -36,9 +36,9 @@
 #pragma mark Record Convenience Methods
 /* CKFetchRecordsOperation and CKModifyRecordsOperation are the more configurable,
  CKOperation-based alternatives to these methods */
-- (void)fetchRecordWithID:(CKRecordID *)recordID completionHandler:(void (^)(CKRecord * _Nullable record, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(fetch(withRecordID:completionHandler:));
+- (void)fetchRecordWithID:(CKRecordID *)recordID completionHandler:(void (^)(CKRecord * _Nullable record, NSError * _Nullable error))completionHandler;
 - (void)saveRecord:(CKRecord *)record completionHandler:(void (^)(CKRecord * _Nullable record, NSError * _Nullable error))completionHandler;
-- (void)deleteRecordWithID:(CKRecordID *)recordID completionHandler:(void (^)(CKRecordID * _Nullable recordID, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(delete(withRecordID:completionHandler:));
+- (void)deleteRecordWithID:(CKRecordID *)recordID completionHandler:(void (^)(CKRecordID * _Nullable recordID, NSError * _Nullable error))completionHandler;
 
 #pragma mark Query Convenience Method
 /* CKQueryOperation is the more configurable, CKOperation-based alternative to this method 
@@ -52,17 +52,17 @@
 /* CKFetchRecordZonesOperation and CKModifyRecordZonesOperation are the more configurable,
  CKOperation-based alternatives to these methods */
 - (void)fetchAllRecordZonesWithCompletionHandler:(void (^)(NSArray<CKRecordZone *> * _Nullable zones, NSError * _Nullable error))completionHandler;
-- (void)fetchRecordZoneWithID:(CKRecordZoneID *)zoneID completionHandler:(void (^)(CKRecordZone * _Nullable zone, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(fetch(withRecordZoneID:completionHandler:));
+- (void)fetchRecordZoneWithID:(CKRecordZoneID *)zoneID completionHandler:(void (^)(CKRecordZone * _Nullable zone, NSError * _Nullable error))completionHandler;
 - (void)saveRecordZone:(CKRecordZone *)zone completionHandler:(void (^)(CKRecordZone * _Nullable zone, NSError * _Nullable error))completionHandler;
-- (void)deleteRecordZoneWithID:(CKRecordZoneID *)zoneID completionHandler:(void (^)(CKRecordZoneID * _Nullable zoneID, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(delete(withRecordZoneID:completionHandler:));
+- (void)deleteRecordZoneWithID:(CKRecordZoneID *)zoneID completionHandler:(void (^)(CKRecordZoneID * _Nullable zoneID, NSError * _Nullable error))completionHandler;
 
 #pragma mark Subscription Convenience Methods
 /* CKFetchSubscriptionsOperation and CKModifySubscriptionsOperation are the more configurable,
  CKOperation-based alternative to these methods */
-- (void)fetchSubscriptionWithID:(NSString *)subscriptionID completionHandler:(void (^)(CKSubscription * _Nullable subscription, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(fetch(withSubscriptionID:completionHandler:)) __WATCHOS_PROHIBITED;
+- (void)fetchSubscriptionWithID:(NSString *)subscriptionID completionHandler:(void (^)(CKSubscription * _Nullable subscription, NSError * _Nullable error))completionHandler __WATCHOS_PROHIBITED;
 - (void)fetchAllSubscriptionsWithCompletionHandler:(void (^)(NSArray<CKSubscription *> * _Nullable subscriptions, NSError * _Nullable error))completionHandler __WATCHOS_PROHIBITED;
 - (void)saveSubscription:(CKSubscription *)subscription completionHandler:(void (^)(CKSubscription * _Nullable subscription, NSError * _Nullable error))completionHandler __WATCHOS_PROHIBITED;
-- (void)deleteSubscriptionWithID:(NSString *)subscriptionID completionHandler:(void (^)(NSString * _Nullable subscriptionID, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(delete(withSubscriptionID:completionHandler:)) __WATCHOS_PROHIBITED;
+- (void)deleteSubscriptionWithID:(NSString *)subscriptionID completionHandler:(void (^)(NSString * _Nullable subscriptionID, NSError * _Nullable error))completionHandler __WATCHOS_PROHIBITED;
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZonesOperation.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZonesOperation.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZonesOperation.h	2016-07-11 07:27:39.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZonesOperation.h	2016-07-25 07:30:48.000000000 +0200
@@ -13,7 +13,7 @@
 NS_CLASS_AVAILABLE(10_10, 8_0)
 @interface CKFetchRecordZonesOperation : CKDatabaseOperation
 
-+ (instancetype)fetchAllRecordZonesOperation NS_SWIFT_NAME(fetchAllRecordZonesOperation());
++ (instancetype)fetchAllRecordZonesOperation;
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
 - (instancetype)initWithRecordZoneIDs:(NSArray<CKRecordZoneID *> *)zoneIDs;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordsOperation.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordsOperation.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordsOperation.h	2016-07-11 07:27:39.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordsOperation.h	2016-07-25 07:30:48.000000000 +0200
@@ -16,7 +16,7 @@
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
 - (instancetype)initWithRecordIDs:(NSArray<CKRecordID *> *)recordIDs;
 
-+ (instancetype)fetchCurrentUserRecordOperation NS_SWIFT_NAME(fetchCurrentUserRecordOperation());
++ (instancetype)fetchCurrentUserRecordOperation;
 
 @property (nonatomic, copy, nullable) NSArray<CKRecordID *> *recordIDs;
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareParticipantsOperation.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareParticipantsOperation.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareParticipantsOperation.h	2016-07-11 07:27:39.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareParticipantsOperation.h	2016-07-25 07:30:48.000000000 +0200
@@ -26,7 +26,7 @@
  If the error is CKErrorPartialFailure, the error's userInfo dictionary contains
  a dictionary of lookup infos to errors keyed off of CKPartialErrorsByItemIDKey.
  */
-@property (nonatomic, copy, nullable) void (^fetchShareParticipantsCompletionBlock)(NSError *operationError);
+@property (nonatomic, copy, nullable) void (^fetchShareParticipantsCompletionBlock)(NSError * _Nullable operationError);
 
 @end
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchSubscriptionsOperation.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchSubscriptionsOperation.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchSubscriptionsOperation.h	2016-07-11 07:27:39.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchSubscriptionsOperation.h	2016-07-25 07:30:48.000000000 +0200
@@ -16,7 +16,7 @@
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
 
-+ (instancetype)fetchAllSubscriptionsOperation NS_SWIFT_NAME(fetchAllSubscriptionsOperation());
++ (instancetype)fetchAllSubscriptionsOperation;
 
 - (instancetype)initWithSubscriptionIDs:(NSArray<NSString *> *)subscriptionIDs;
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyRecordsOperation.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyRecordsOperation.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyRecordsOperation.h	2016-07-11 07:27:39.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyRecordsOperation.h	2016-07-25 07:30:48.000000000 +0200
@@ -11,7 +11,9 @@
 
 typedef NS_ENUM(NSInteger, CKRecordSavePolicy) {
     CKRecordSaveIfServerRecordUnchanged = 0, /* Locally-edited keys are sent to the server. If the record on the server has been modified,
-                                                fail the write and return an error. */
+                                                fail the write and return an error. A CKShare's participants array is always treated as
+                                                CKRecordSaveIfServerRecordUnchanged, regardless of the savePolicy of the operation that
+                                                modifies the share. */
     CKRecordSaveChangedKeys             = 1, /* Locally-edited keys are written to the server.  Any unseen changes on the server
                                                will be overwritten to the locally-edited value. */
     CKRecordSaveAllKeys                 = 2, /* All local keys are written to the server.  Any unseen changes on the server will be
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecord.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecord.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecord.h	2016-07-11 07:27:39.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecord.h	2016-07-25 07:36:17.000000000 +0200
@@ -18,6 +18,10 @@
 /* Use this constant for the recordType parameter when fetching User Records. */
 CK_EXTERN NSString * const CKRecordTypeUserRecord NS_AVAILABLE(10_10, 8_0);
 
+/* Use these keys in queries to match on the record's parent or share reference */
+CK_EXTERN NSString * const CKRecordParentKey NS_AVAILABLE(10_12, 10_0);
+CK_EXTERN NSString * const CKRecordShareKey NS_AVAILABLE(10_12, 10_0);
+
 @protocol CKRecordValue <NSObject>
 @end
 
@@ -119,8 +123,8 @@
 @property (nonatomic, copy, nullable) CKReference *parent;
 
 /* Convenience wrappers around creating a CKReference to a parent record. The resulting CKReference will have action = CKReferenceActionNone */
-- (void)setParentReferenceFromRecord:(nullable CKRecord *)parentRecord NS_SWIFT_NAME(setParent(_:));
-- (void)setParentReferenceFromRecordID:(nullable CKRecordID *)parentRecordID NS_SWIFT_NAME(setParent(_:));
+- (void)setParentReferenceFromRecord:(nullable CKRecord *)parentRecord;
+- (void)setParentReferenceFromRecordID:(nullable CKRecordID *)parentRecordID;
 
 @end
 

```