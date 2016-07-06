#CloudKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKContainer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKContainer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKContainer.h	2016-06-02 07:24:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKContainer.h	2016-06-27 06:05:17.000000000 +0200
@@ -11,7 +11,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-@class CKDatabase, CKOperation, CKRecordID, CKUserIdentity, CKShareParticipant, CKDiscoveredUserInfo;
+@class CKDatabase, CKOperation, CKRecordID, CKUserIdentity, CKShareParticipant, CKDiscoveredUserInfo, CKShare, CKShareMetadata;
 
 // This constant represents the current user's ID for zone ID
 CK_EXTERN NSString * const CKCurrentUserDefaultName NS_AVAILABLE(10_12, 10_0);
@@ -139,9 +139,12 @@
 
 /* Fetches share participants matching the provided info .
  CKFetchShareParticipantsOperation is the more configurable, CKOperation-based alternative to these methods. */
-- (void)fetchShareParticipantWithEmailAddress:(NSString *)emailAddress completionHandler:(void (^)(CKShareParticipant *shareParticipant, NSError *error))completionHandler;
-- (void)fetchShareParticipantWithPhoneNumber:(NSString *)phoneNumber completionHandler:(void (^)(CKShareParticipant *shareParticipant, NSError *error))completionHandler;
-- (void)fetchShareParticipantWithUserRecordID:(CKRecordID *)userRecordID completionHandler:(void (^)(CKShareParticipant *shareParticipant, NSError *error))completionHandler;
+- (void)fetchShareParticipantWithEmailAddress:(NSString *)emailAddress completionHandler:(void (^)(CKShareParticipant *shareParticipant, NSError *error))completionHandler NS_AVAILABLE(10_12, 10_0);
+- (void)fetchShareParticipantWithPhoneNumber:(NSString *)phoneNumber completionHandler:(void (^)(CKShareParticipant *shareParticipant, NSError *error))completionHandler NS_AVAILABLE(10_12, 10_0);
+- (void)fetchShareParticipantWithUserRecordID:(CKRecordID *)userRecordID completionHandler:(void (^)(CKShareParticipant *shareParticipant, NSError *error))completionHandler NS_AVAILABLE(10_12, 10_0);
+
+- (void)fetchShareMetadataWithURL:(NSURL *)url completionHandler:(void (^)(CKShareMetadata *metadata, NSError *error))completionHandler NS_AVAILABLE(10_12, 10_0);
+- (void)acceptShareMetadata:(CKShareMetadata *)metadata completionHandler:(void (^)(CKShare *acceptedShare, NSError *error))completionHandler NS_AVAILABLE(10_12, 10_0);
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h	2016-05-27 06:59:12.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h	2016-06-27 07:34:22.000000000 +0200
@@ -59,10 +59,10 @@
 #pragma mark Subscription Convenience Methods
 /* CKFetchSubscriptionsOperation and CKModifySubscriptionsOperation are the more configurable,
  CKOperation-based alternative to these methods */
-- (void)fetchSubscriptionWithID:(NSString *)subscriptionID completionHandler:(void (^)(CKSubscription * _Nullable subscription, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(fetch(withSubscriptionID:completionHandler:));
-- (void)fetchAllSubscriptionsWithCompletionHandler:(void (^)(NSArray<CKSubscription *> * _Nullable subscriptions, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(fetchAll(completionHandler:));
-- (void)saveSubscription:(CKSubscription *)subscription completionHandler:(void (^)(CKSubscription * _Nullable subscription, NSError * _Nullable error))completionHandler;
-- (void)deleteSubscriptionWithID:(NSString *)subscriptionID completionHandler:(void (^)(NSString * _Nullable subscriptionID, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(delete(withSubscriptionID:completionHandler:));
+- (void)fetchSubscriptionWithID:(NSString *)subscriptionID completionHandler:(void (^)(CKSubscription * _Nullable subscription, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(fetch(withSubscriptionID:completionHandler:)) __WATCHOS_PROHIBITED;
+- (void)fetchAllSubscriptionsWithCompletionHandler:(void (^)(NSArray<CKSubscription *> * _Nullable subscriptions, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(fetchAll(completionHandler:)) __WATCHOS_PROHIBITED;
+- (void)saveSubscription:(CKSubscription *)subscription completionHandler:(void (^)(CKSubscription * _Nullable subscription, NSError * _Nullable error))completionHandler __WATCHOS_PROHIBITED;
+- (void)deleteSubscriptionWithID:(NSString *)subscriptionID completionHandler:(void (^)(NSString * _Nullable subscriptionID, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(delete(withSubscriptionID:completionHandler:)) __WATCHOS_PROHIBITED;
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchDatabaseChangesOperation.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchDatabaseChangesOperation.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchDatabaseChangesOperation.h	2016-05-27 07:20:24.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchDatabaseChangesOperation.h	2016-06-27 07:34:22.000000000 +0200
@@ -18,7 +18,8 @@
  This per-database serverChangeToken is not to be confused with the per-recordZone serverChangeToken from
  CKFetchRecordZoneChangesOperation.
  If this is your first fetch or if you wish to re-fetch all zones, pass nil for the change token.
- Change token are opaque tokens and clients should not infer any behavior based on their content. */
+ Change token are opaque tokens and clients should not infer any behavior based on their content.
+ CKFetchDatabaseChangesOperations are supported in a privateCloudDatabase and sharedCloudDatabase */
 - (instancetype)initWithPreviousServerChangeToken:(nullable CKServerChangeToken *)previousServerChangeToken;
 
 @property (nonatomic, copy, nullable) CKServerChangeToken *previousServerChangeToken;
@@ -41,8 +42,7 @@
  If the server returns a CKErrorChangeTokenExpired error, the previousServerChangeToken value was too old and the client should toss its local cache and
  re-fetch the changes in this record zone starting with a nil previousServerChangeToken.
  If moreComing is true then the server wasn't able to return all the changes in this response.
- Another CKFetchDatabaseChangesOperation operation should be run with the previousServerChangeToken token from this operation.
- */
+ Another CKFetchDatabaseChangesOperation operation should be run with the previousServerChangeToken token from this operation. */
 @property (nonatomic, copy, nullable) void (^fetchDatabaseChangesCompletionBlock)(CKServerChangeToken * _Nullable serverChangeToken, BOOL moreComing, NSError * _Nullable operationError);
 
 @end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZoneChangesOperation.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZoneChangesOperation.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZoneChangesOperation.h	2016-06-02 07:24:52.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZoneChangesOperation.h	2016-06-27 06:05:17.000000000 +0200
@@ -30,7 +30,9 @@
 
 /* When set to YES, this operation will send repeated requests to the server until all record changes have been fetched.
  recordZoneChangeTokensUpdatedBlock will be invoked periodically, to give clients an updated change token so that already-fetched
- record changes don't need to be re-fetched on a subsequent operation.
+ record changes don't need to be re-fetched on a subsequent operation. recordZoneFetchCompletionBlock will only be called once and moreComing 
+ will always be NO.
+ 
  When set to NO, it is the responsibility of the caller to issue subsequent fetch-changes operations when moreComing is YES
  in a recordZoneFetchCompletionBlock invocation.
  fetchAllChanges is YES by default */
@@ -41,9 +43,11 @@
 
 /* Clients are responsible for saving this per-recordZone serverChangeToken and passing it in to the next call to CKFetchRecordZoneChangesOperation.
  Note that a fetch can fail partway. If that happens, an updated change token may be returned in this
- block so that already fetched records don't need to be re-downloaded on a subsequent operation.
+  block so that already fetched records don't need to be re-downloaded on a subsequent operation.
+ recordZoneChangeTokensUpdatedBlock will not be called after the last batch of changes in a zone; the recordZoneFetchCompletionBlock block will be called instead.
  The clientChangeTokenData from the most recent CKModifyRecordsOperation issued on this zone is also returned, or nil if none was provided.
- If the server returns a CKErrorChangeTokenExpired error, the serverChangeToken used for this record zone when initting this operation was too old and the client should toss its local cache and re-fetch the changes in this record zone starting with a nil serverChangeToken. */
+ If the server returns a CKErrorChangeTokenExpired error, the serverChangeToken used for this record zone when initting this operation was too old and the client should toss its local cache and re-fetch the changes in this record zone starting with a nil serverChangeToken. 
+ recordZoneChangeTokensUpdatedBlock will not be called if fetchAllChanges is NO. */
 @property (nonatomic, copy, nullable) void (^recordZoneChangeTokensUpdatedBlock)(CKRecordZoneID *recordZoneID, CKServerChangeToken * _Nullable serverChangeToken, NSData * _Nullable clientChangeTokenData);
 @property (nonatomic, copy, nullable) void (^recordZoneFetchCompletionBlock)(CKRecordZoneID *recordZoneID, CKServerChangeToken * _Nullable serverChangeToken, NSData * _Nullable clientChangeTokenData, BOOL moreComing, NSError * _Nullable recordZoneError);
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchSubscriptionsOperation.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchSubscriptionsOperation.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchSubscriptionsOperation.h	2016-05-27 07:20:24.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchSubscriptionsOperation.h	2016-06-27 07:34:22.000000000 +0200
@@ -11,7 +11,7 @@
 @class CKSubscription;
 
 NS_ASSUME_NONNULL_BEGIN
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_10, 8_0) __WATCHOS_PROHIBITED
 @interface CKFetchSubscriptionsOperation : CKDatabaseOperation
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifySubscriptionsOperation.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifySubscriptionsOperation.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifySubscriptionsOperation.h	2016-05-27 07:20:24.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifySubscriptionsOperation.h	2016-06-27 07:34:22.000000000 +0200
@@ -10,7 +10,7 @@
 @class CKSubscription;
 
 NS_ASSUME_NONNULL_BEGIN
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_10, 8_0) __WATCHOS_PROHIBITED
 @interface CKModifySubscriptionsOperation : CKDatabaseOperation
 
 - (instancetype)initWithSubscriptionsToSave:(nullable NSArray<CKSubscription *> *)subscriptionsToSave subscriptionIDsToDelete:(nullable NSArray<NSString *> *)subscriptionIDsToDelete NS_DESIGNATED_INITIALIZER;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKOperation.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKOperation.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKOperation.h	2016-05-27 07:20:24.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKOperation.h	2016-06-27 07:34:22.000000000 +0200
@@ -59,7 +59,7 @@
    If non-zero, overrides the timeout interval for any network requests issued by this operation.
    See NSURLSessionConfiguration.timeoutIntervalForRequest 
 */
-@property (nonatomic, assign) NSTimeInterval timeoutIntervalForRequest NS_AVAILABLE(10_12, 9_3);
+@property (nonatomic, assign) NSTimeInterval timeoutIntervalForRequest NS_AVAILABLE(10_12, 10_0);
 
 /*
  If non-zero, overrides the timeout interval for any network resources retrieved by this operation.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKSubscription.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKSubscription.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKSubscription.h	2016-05-27 05:15:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKSubscription.h	2016-06-27 06:24:49.000000000 +0200
@@ -14,11 +14,11 @@
     CKSubscriptionTypeQuery                                     = 1,
     CKSubscriptionTypeRecordZone                                = 2,
     CKSubscriptionTypeDatabase NS_ENUM_AVAILABLE(10_12, 10_0)   = 3,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} NS_ENUM_AVAILABLE(10_10, 8_0) __WATCHOS_PROHIBITED;
 
 @class CKNotificationInfo, CKRecordZoneID;
 
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_10, 8_0) __WATCHOS_PROHIBITED
 @interface CKSubscription : NSObject <NSSecureCoding, NSCopying>
 
 - (instancetype)init NS_UNAVAILABLE;
@@ -37,11 +37,11 @@
     CKQuerySubscriptionOptionsFiresOnRecordUpdate       = 1 << 1,
     CKQuerySubscriptionOptionsFiresOnRecordDeletion     = 1 << 2,
     CKQuerySubscriptionOptionsFiresOnce                 = 1 << 3,
-} NS_ENUM_AVAILABLE(10_12, 10_0);
+} NS_ENUM_AVAILABLE(10_12, 10_0) __WATCHOS_PROHIBITED;
 
 /* A subscription that fires whenever a change matching the predicate occurs.
  CKQuerySubscriptions are not supported in a sharedCloudDatabase */
-NS_CLASS_AVAILABLE(10_12, 10_0)
+NS_CLASS_AVAILABLE(10_12, 10_0) __WATCHOS_PROHIBITED
 @interface CKQuerySubscription : CKSubscription <NSSecureCoding, NSCopying>
 
 - (instancetype)initWithRecordType:(NSString *)recordType predicate:(NSPredicate *)predicate options:(CKQuerySubscriptionOptions)querySubscriptionOptions;
@@ -69,7 +69,7 @@
 /* A subscription that fires whenever any change happens in the indicated Record Zone.
  The RecordZone must have the capability CKRecordZoneCapabilityFetchChanges
  CKRecordZoneSubscriptions are not supported in a sharedCloudDatabase */
-NS_CLASS_AVAILABLE(10_12, 10_0)
+NS_CLASS_AVAILABLE(10_12, 10_0) __WATCHOS_PROHIBITED
 @interface CKRecordZoneSubscription : CKSubscription <NSSecureCoding, NSCopying>
 
 - (instancetype)initWithZoneID:(CKRecordZoneID *)zoneID;
@@ -85,7 +85,7 @@
 
 /* This subscription fires whenever any change happens in the database that this subscription was saved in.
    CKDatabaseSubscription is only supported in the Private and Shared databases. */
-NS_CLASS_AVAILABLE(10_12, 10_0)
+NS_CLASS_AVAILABLE(10_12, 10_0) __WATCHOS_PROHIBITED
 @interface CKDatabaseSubscription : CKSubscription <NSSecureCoding, NSCopying>
 
 - (instancetype)init;
@@ -103,7 +103,7 @@
    On tvOS, alerts, badges, sounds, and categories are not handled in push notifications. However,
    CKSubscriptions remain available to help you avoid polling the servers */
 
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_10, 8_0) __WATCHOS_PROHIBITED
 @interface CKNotificationInfo : NSObject <NSSecureCoding, NSCopying>
 
 /* Optional alert string to display in a push notification. */
@@ -153,7 +153,7 @@
     CKSubscriptionOptionsFiresOnRecordUpdate       = 1 << 1,
     CKSubscriptionOptionsFiresOnRecordDeletion     = 1 << 2,
     CKSubscriptionOptionsFiresOnce                 = 1 << 3,
-} NS_ENUM_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use CKQuerySubscriptionOptions instead");
+} NS_ENUM_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use CKQuerySubscriptionOptions instead") __WATCHOS_PROHIBITED;
 
 @interface CKSubscription (CKSubscriptionDeprecated)
 

```