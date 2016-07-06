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