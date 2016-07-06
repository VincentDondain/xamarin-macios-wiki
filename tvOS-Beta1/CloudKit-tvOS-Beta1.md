#CloudKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKAcceptSharesOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKAcceptSharesOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKAcceptSharesOperation.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKAcceptSharesOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -0,0 +1,36 @@
+//
+//  CKAcceptSharesOperation.h
+//  CloudKit
+//
+//  Copyright (c) 2014 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <CloudKit/CKDatabaseOperation.h>
+
+@class CKShare, CKShareMetadata;
+
+NS_ASSUME_NONNULL_BEGIN
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CKAcceptSharesOperation : CKOperation
+
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithShareMetadatas:(NSArray<CKShareMetadata *> *)shareMetadatas;
+
+@property (nonatomic, copy) NSArray<CKShareMetadata *> *shareMetadatas;
+
+/* Called once for each share metadata that the server processed. If error is nil then the share was successfully accepted. */
+@property (nonatomic, copy, nullable) void (^perShareCompletionBlock)(CKShareMetadata *shareMetadata, CKShare * _Nullable acceptedShare, NSError * _Nullable error);
+
+/*  This block is called when the operation completes.
+ The [NSOperation completionBlock] will also be called if both are set.
+ If the error is CKErrorPartialFailure, the error's userInfo dictionary contains
+ a dictionary of shareURLs to errors keyed off of CKPartialErrorsByItemIDKey.
+ This call happens as soon as the server has
+ seen all record changes, and may be invoked while the server is processing the side effects
+ of those changes.
+ */
+@property (nonatomic, copy, nullable) void (^acceptSharesCompletionBlock)(NSError *operationError);
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKContainer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKContainer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKContainer.h	2016-02-20 00:59:37.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKContainer.h	2016-06-02 07:24:45.000000000 +0200
@@ -7,13 +7,16 @@
 
 #import <Foundation/Foundation.h>
 #import <CloudKit/CKDefines.h>
+#import <CloudKit/CKDatabase.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-@class CKDatabase, CKOperation, CKRecordID, CKDiscoveredUserInfo;
+@class CKDatabase, CKOperation, CKRecordID, CKUserIdentity, CKShareParticipant, CKDiscoveredUserInfo;
 
 // This constant represents the current user's ID for zone ID
-CK_EXTERN NSString * const CKOwnerDefaultName NS_AVAILABLE(10_10, 8_0);
+CK_EXTERN NSString * const CKCurrentUserDefaultName NS_AVAILABLE(10_12, 10_0);
+
+CK_EXTERN NSString * const CKOwnerDefaultName NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use CKCurrentUserDefaultName instead");
 
 NS_CLASS_AVAILABLE(10_10, 8_0)
 @interface CKContainer : NSObject
@@ -39,7 +42,7 @@
 
 @interface CKContainer (Database)
 
-/* Public vs. Private databases:
+/* Database properties:
  Records in a public database
  - By default are world readable, owner writable.
  - Can be locked down by Roles, a process done in the Developer Portal, a web interface.  Roles are not present in the client API.
@@ -49,9 +52,17 @@
  - By default are only owner readable and owner writable.
  - Are not visible to the application developer via the Developer Portal.
  - Are counted towards the owner's iCloud account storage quota.
+ Records in a shared database
+ - Are available to share participants based on the permissions of the enclosing CKShare
+ - Are not visible to the application developer via the Developer Portal.
+ - Are counted towards the originating owner's iCloud account storage quota.
  */
 @property (nonatomic, readonly) CKDatabase *privateCloudDatabase;
 @property (nonatomic, readonly) CKDatabase *publicCloudDatabase;
+@property (nonatomic, readonly) CKDatabase *sharedCloudDatabase;
+
+/* Convenience method, will return a database that's pointer-equal to one of the above properties */
+- (CKDatabase *)databaseWithDatabaseScope:(CKDatabaseScope)databaseScope;
 
 @end
 
@@ -74,7 +85,7 @@
 
 @interface CKContainer (AccountStatus)
 
-- (void)accountStatusWithCompletionHandler:(void (^)(CKAccountStatus accountStatus, NSError * __nullable error))completionHandler;
+- (void)accountStatusWithCompletionHandler:(void (^)(CKAccountStatus accountStatus, NSError * _Nullable error))completionHandler;
 
 @end
 
@@ -94,7 +105,7 @@
     CKApplicationPermissionStatusGranted               = 3,
 } NS_ENUM_AVAILABLE(10_10, 8_0);
 
-typedef void(^CKApplicationPermissionBlock)(CKApplicationPermissionStatus applicationPermissionStatus, NSError * __nullable error);
+typedef void(^CKApplicationPermissionBlock)(CKApplicationPermissionStatus applicationPermissionStatus, NSError * _Nullable error);
 
 @interface CKContainer (ApplicationPermission)
 
@@ -108,14 +119,29 @@
 /* If there is no iCloud account configured, or if access is restricted, a CKErrorNotAuthenticated error will be returned. 
    This work is treated as having NSQualityOfServiceUserInitiated quality of service.
  */
-- (void)fetchUserRecordIDWithCompletionHandler:(void (^)(CKRecordID * __nullable recordID, NSError * __nullable error))completionHandler;
+- (void)fetchUserRecordIDWithCompletionHandler:(void (^)(CKRecordID * _Nullable recordID, NSError * _Nullable error))completionHandler;
 
 /* This fetches all user records that match an entry in the user's address book.
- CKDiscoverAllContactsOperation and CKDiscoverUserInfosOperation are the more configurable,
+ CKDiscoverAllContactsOperation and CKDiscoverUserIdentityOperation are the more configurable,
  CKOperation-based alternatives to these methods */
-- (void)discoverAllContactUserInfosWithCompletionHandler:(void (^)(NSArray <CKDiscoveredUserInfo *> * __nullable userInfos, NSError * __nullable error))completionHandler __TVOS_UNAVAILABLE;
-- (void)discoverUserInfoWithEmailAddress:(NSString *)email completionHandler:(void (^)(CKDiscoveredUserInfo * __nullable userInfo, NSError * __nullable error))completionHandler;
-- (void)discoverUserInfoWithUserRecordID:(CKRecordID *)userRecordID completionHandler:(void (^)(CKDiscoveredUserInfo * __nullable userInfo, NSError * __nullable error))completionHandler;
+- (void)discoverAllIdentitiesWithCompletionHandler:(void (^)(NSArray<CKUserIdentity *> * _Nullable userIdentities, NSError * _Nullable error))completionHandler __TVOS_UNAVAILABLE;
+- (void)discoverUserIdentityWithEmailAddress:(NSString *)email completionHandler:(void (^)(CKUserIdentity * _Nullable userInfo, NSError * _Nullable error))completionHandler;
+- (void)discoverUserIdentityWithPhoneNumber:(NSString *)phoneNumber completionHandler:(void (^)(CKUserIdentity * _Nullable userInfo, NSError * _Nullable error))completionHandler;
+- (void)discoverUserIdentityWithUserRecordID:(CKRecordID *)userRecordID completionHandler:(void (^)(CKUserIdentity * _Nullable userInfo, NSError * _Nullable error))completionHandler;
+
+- (void)discoverAllContactUserInfosWithCompletionHandler:(void (^)(NSArray<CKDiscoveredUserInfo *> * _Nullable userInfos, NSError * _Nullable error))completionHandler __TVOS_UNAVAILABLE NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use -[CKContainer discoverAllIdentitiesWithCompletionHandler:] instead");
+- (void)discoverUserInfoWithEmailAddress:(NSString *)email completionHandler:(void (^)(CKDiscoveredUserInfo * _Nullable userInfo, NSError * _Nullable error))completionHandler NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use -[CKContainer discoverUserIdentityWithEmailAddress:completionHandler:] instead");
+- (void)discoverUserInfoWithUserRecordID:(CKRecordID *)userRecordID completionHandler:(void (^)(CKDiscoveredUserInfo * _Nullable userInfo, NSError * _Nullable error))completionHandler NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use -[CKContainer discoverUserIdentityWithUserRecordID:completionHandler:] instead");
+
+@end
+
+@interface CKContainer (Sharing)
+
+/* Fetches share participants matching the provided info .
+ CKFetchShareParticipantsOperation is the more configurable, CKOperation-based alternative to these methods. */
+- (void)fetchShareParticipantWithEmailAddress:(NSString *)emailAddress completionHandler:(void (^)(CKShareParticipant *shareParticipant, NSError *error))completionHandler;
+- (void)fetchShareParticipantWithPhoneNumber:(NSString *)phoneNumber completionHandler:(void (^)(CKShareParticipant *shareParticipant, NSError *error))completionHandler;
+- (void)fetchShareParticipantWithUserRecordID:(CKRecordID *)userRecordID completionHandler:(void (^)(CKShareParticipant *shareParticipant, NSError *error))completionHandler;
 
 @end
 
@@ -127,7 +153,7 @@
   its callbacks from the start of the operation, but the request will not be re-sent to the server.
  If a long lived operation is cancelled or finishes completely it is no longer returned by these calls.
  */
-- (void)fetchAllLongLivedOperationIDsWithCompletionHandler:(void (^)(NSArray <NSString *> * __nullable outstandingOperationIDs, NSError * __nullable error))completionHandler NS_AVAILABLE(10_12, 9_3);
-- (void)fetchLongLivedOperationWithID:(NSString *)operationID completionHandler:(void (^)(CKOperation * __nullable outstandingOperation, NSError * __nullable error))completionHandler NS_AVAILABLE(10_12, 9_3);
+- (void)fetchAllLongLivedOperationIDsWithCompletionHandler:(void (^)(NSArray<NSString *> * _Nullable outstandingOperationIDs, NSError * _Nullable error))completionHandler NS_AVAILABLE(10_12, 9_3);
+- (void)fetchLongLivedOperationWithID:(NSString *)operationID completionHandler:(void (^)(CKOperation * _Nullable outstandingOperation, NSError * _Nullable error))completionHandler NS_AVAILABLE(10_12, 9_3);
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h	2016-05-27 06:59:12.000000000 +0200
@@ -10,10 +10,18 @@
 @class CKDatabaseOperation, CKRecord, CKRecordID, CKRecordZone, CKRecordZoneID, CKQuery, CKSubscription;
 
 NS_ASSUME_NONNULL_BEGIN
+
+typedef NS_ENUM(NSInteger, CKDatabaseScope) {
+    CKDatabaseScopePublic = 1,
+    CKDatabaseScopePrivate,
+    CKDatabaseScopeShared,
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
 NS_CLASS_AVAILABLE(10_10, 8_0)
 @interface CKDatabase : NSObject
 - (instancetype)init NS_UNAVAILABLE;
 - (void)addOperation:(CKDatabaseOperation *)operation;
+@property (nonatomic, readonly, assign) CKDatabaseScope databaseScope;
 @end
 
 @interface CKDatabase (ConvenienceMethods)
@@ -28,30 +36,33 @@
 #pragma mark Record Convenience Methods
 /* CKFetchRecordsOperation and CKModifyRecordsOperation are the more configurable,
  CKOperation-based alternatives to these methods */
-- (void)fetchRecordWithID:(CKRecordID *)recordID completionHandler:(void (^)(CKRecord * __nullable record, NSError * __nullable error))completionHandler;
-- (void)saveRecord:(CKRecord *)record completionHandler:(void (^)(CKRecord * __nullable record, NSError * __nullable error))completionHandler;
-- (void)deleteRecordWithID:(CKRecordID *)recordID completionHandler:(void (^)(CKRecordID * __nullable recordID, NSError * __nullable error))completionHandler;
+- (void)fetchRecordWithID:(CKRecordID *)recordID completionHandler:(void (^)(CKRecord * _Nullable record, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(fetch(withRecordID:completionHandler:));
+- (void)saveRecord:(CKRecord *)record completionHandler:(void (^)(CKRecord * _Nullable record, NSError * _Nullable error))completionHandler;
+- (void)deleteRecordWithID:(CKRecordID *)recordID completionHandler:(void (^)(CKRecordID * _Nullable recordID, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(delete(withRecordID:completionHandler:));
 
 #pragma mark Query Convenience Method
-/* CKQueryOperation is the more configurable, CKOperation-based
- alternative to this method */
-- (void)performQuery:(CKQuery *)query inZoneWithID:(nullable CKRecordZoneID *)zoneID completionHandler:(void (^)(NSArray <CKRecord *> * __nullable results, NSError * __nullable error))completionHandler;
+/* CKQueryOperation is the more configurable, CKOperation-based alternative to this method 
+ Queries can potentially return a large number of records, and the server will return those records in batches.
+ This convenience API will only fetch the first batch of results (equivalent to using CKQueryOperationMaximumResults).
+ If you would like to fetch all results, use CKQueryOperation and its CKQueryCursor instead.
+ Queries invoked within a sharedCloudDatabase must specify a zoneID.  Cross-zone queries are not supported in a sharedCloudDatabase */
+- (void)performQuery:(CKQuery *)query inZoneWithID:(nullable CKRecordZoneID *)zoneID completionHandler:(void (^)(NSArray<CKRecord *> * _Nullable results, NSError * _Nullable error))completionHandler;
 
 #pragma mark Record Zone Convenience Methods
 /* CKFetchRecordZonesOperation and CKModifyRecordZonesOperation are the more configurable,
  CKOperation-based alternatives to these methods */
-- (void)fetchAllRecordZonesWithCompletionHandler:(void (^)(NSArray <CKRecordZone *> * __nullable zones, NSError * __nullable error))completionHandler;
-- (void)fetchRecordZoneWithID:(CKRecordZoneID *)zoneID completionHandler:(void (^)(CKRecordZone * __nullable zone, NSError * __nullable error))completionHandler;
-- (void)saveRecordZone:(CKRecordZone *)zone completionHandler:(void (^)(CKRecordZone * __nullable zone, NSError * __nullable error))completionHandler;
-- (void)deleteRecordZoneWithID:(CKRecordZoneID *)zoneID completionHandler:(void (^)(CKRecordZoneID * __nullable zoneID, NSError * __nullable error))completionHandler;
+- (void)fetchAllRecordZonesWithCompletionHandler:(void (^)(NSArray<CKRecordZone *> * _Nullable zones, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(fetchAll(completionHandler:));
+- (void)fetchRecordZoneWithID:(CKRecordZoneID *)zoneID completionHandler:(void (^)(CKRecordZone * _Nullable zone, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(fetch(withRecordZoneID:completionHandler:));
+- (void)saveRecordZone:(CKRecordZone *)zone completionHandler:(void (^)(CKRecordZone * _Nullable zone, NSError * _Nullable error))completionHandler;
+- (void)deleteRecordZoneWithID:(CKRecordZoneID *)zoneID completionHandler:(void (^)(CKRecordZoneID * _Nullable zoneID, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(delete(withRecordZoneID:completionHandler:));
 
 #pragma mark Subscription Convenience Methods
 /* CKFetchSubscriptionsOperation and CKModifySubscriptionsOperation are the more configurable,
  CKOperation-based alternative to these methods */
-- (void)fetchSubscriptionWithID:(NSString *)subscriptionID completionHandler:(void (^)(CKSubscription * __nullable subscription, NSError * __nullable error))completionHandler;
-- (void)fetchAllSubscriptionsWithCompletionHandler:(void (^)(NSArray <CKSubscription *> * __nullable subscriptions, NSError * __nullable error))completionHandler;
-- (void)saveSubscription:(CKSubscription *)subscription completionHandler:(void (^)(CKSubscription * __nullable subscription, NSError * __nullable error))completionHandler;
-- (void)deleteSubscriptionWithID:(NSString *)subscriptionID completionHandler:(void (^)(NSString * __nullable subscriptionID, NSError * __nullable error))completionHandler;
+- (void)fetchSubscriptionWithID:(NSString *)subscriptionID completionHandler:(void (^)(CKSubscription * _Nullable subscription, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(fetch(withSubscriptionID:completionHandler:));
+- (void)fetchAllSubscriptionsWithCompletionHandler:(void (^)(NSArray<CKSubscription *> * _Nullable subscriptions, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(fetchAll(completionHandler:));
+- (void)saveSubscription:(CKSubscription *)subscription completionHandler:(void (^)(CKSubscription * _Nullable subscription, NSError * _Nullable error))completionHandler;
+- (void)deleteSubscriptionWithID:(NSString *)subscriptionID completionHandler:(void (^)(NSString * _Nullable subscriptionID, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(delete(withSubscriptionID:completionHandler:));
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDefines.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDefines.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDefines.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDefines.h	2016-05-27 06:59:12.000000000 +0200
@@ -13,11 +13,15 @@
 #endif
 #endif
 
+#ifndef CK_HIDDEN
+#define CK_HIDDEN   __attribute__((visibility("hidden")))
+#endif
+
 
 #if DEBUG
     #define CK_UNIT_TESTS_AVAILABLE NS_CLASS_AVAILABLE(10_10, 8_0)
     #define CK_UNIT_TESTS_EXTERN CK_EXTERN
 #else
-    #define CK_UNIT_TESTS_AVAILABLE NS_CLASS_AVAILABLE(10_10, 8_0)
-    #define CK_UNIT_TESTS_EXTERN CK_EXTERN
+    #define CK_UNIT_TESTS_AVAILABLE CK_HIDDEN
+    #define CK_UNIT_TESTS_EXTERN CK_HIDDEN
 #endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoverAllContactsOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoverAllContactsOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoverAllContactsOperation.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoverAllContactsOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -12,13 +12,13 @@
 
 /* Finds all discoverable users in the device's address book. No Address Book access dialog will be displayed */
 NS_ASSUME_NONNULL_BEGIN
-NS_CLASS_AVAILABLE(10_10, 8_0)
 __TVOS_UNAVAILABLE
+NS_CLASS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use CKDiscoverAllUserIdentitiesOperation instead")
 @interface CKDiscoverAllContactsOperation : CKOperation
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
 
-@property (nonatomic, copy, nullable) void (^discoverAllContactsCompletionBlock)(NSArray <CKDiscoveredUserInfo *> * __nullable userInfos, NSError * __nullable operationError);
+@property (nonatomic, copy, nullable) void (^discoverAllContactsCompletionBlock)(NSArray<CKDiscoveredUserInfo *> * _Nullable userInfos, NSError * _Nullable operationError);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoverAllUserIdentitiesOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoverAllUserIdentitiesOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoverAllUserIdentitiesOperation.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoverAllUserIdentitiesOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -0,0 +1,25 @@
+//
+//  CKDiscoverAllUserIdentitiesOperation.h
+//  CloudKit
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <CloudKit/CKOperation.h>
+
+@class CKUserIdentity;
+
+/* Finds all discoverable users in the device's address book. No Address Book access dialog will be displayed */
+NS_ASSUME_NONNULL_BEGIN
+NS_CLASS_AVAILABLE(10_12, 10_0)
+__TVOS_UNAVAILABLE
+@interface CKDiscoverAllUserIdentitiesOperation : CKOperation
+
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
+
+@property (nonatomic, copy, nullable) void (^userIdentityDiscoveredBlock)(CKUserIdentity *identity);
+@property (nonatomic, copy, nullable) void (^discoverAllUserIdentitiesCompletionBlock)(NSError * _Nullable operationError);
+
+@end
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoverUserIdentitiesOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoverUserIdentitiesOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoverUserIdentitiesOperation.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoverUserIdentitiesOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -0,0 +1,31 @@
+//
+//  CKDiscoverUserIdentitiesOperation.h
+//  CloudKit
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <CloudKit/CKOperation.h>
+
+@class CKRecordID, CKUserIdentity, CKUserIdentityLookupInfo;
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CKDiscoverUserIdentitiesOperation : CKOperation
+
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithUserIdentityLookupInfos:(NSArray<CKUserIdentityLookupInfo *> *)userIdentityLookupInfos;
+
+@property (nonatomic, copy) NSArray<CKUserIdentityLookupInfo *> *userIdentityLookupInfos;
+
+@property (nonatomic, copy, nullable) void (^userIdentityDiscoveredBlock)(CKUserIdentity *identity, CKUserIdentityLookupInfo * lookupInfo);
+
+/*  This block is called when the operation completes.
+ The [NSOperation completionBlock] will also be called if both are set. */
+@property (nonatomic, copy, nullable) void (^discoverUserIdentitiesCompletionBlock)(NSError * _Nullable operationError);
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoverUserInfosOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoverUserInfosOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoverUserInfosOperation.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoverUserInfosOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -11,18 +11,18 @@
 @class CKRecordID, CKDiscoveredUserInfo;
 
 NS_ASSUME_NONNULL_BEGIN
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use CKDiscoverUserIdentitiesOperation instead")
 @interface CKDiscoverUserInfosOperation : CKOperation
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
-- (instancetype)initWithEmailAddresses:(nullable NSArray <NSString *> *)emailAddresses userRecordIDs:(nullable NSArray <CKRecordID *> *)userRecordIDs;
+- (instancetype)initWithEmailAddresses:(nullable NSArray<NSString *> *)emailAddresses userRecordIDs:(nullable NSArray<CKRecordID *> *)userRecordIDs;
 
-@property (nonatomic, copy, nullable) NSArray <NSString *> *emailAddresses;
-@property (nonatomic, copy, nullable) NSArray <CKRecordID *> *userRecordIDs;
+@property (nonatomic, copy, nullable) NSArray<NSString *> *emailAddresses;
+@property (nonatomic, copy, nullable) NSArray<CKRecordID *> *userRecordIDs;
 
 /*  This block is called when the operation completes.
     The [NSOperation completionBlock] will also be called if both are set. */
-@property (nonatomic, copy, nullable) void (^discoverUserInfosCompletionBlock)(NSDictionary <NSString *, CKDiscoveredUserInfo *> * __nullable emailsToUserInfos, NSDictionary <CKRecordID *, CKDiscoveredUserInfo *> * __nullable userRecordIDsToUserInfos, NSError * __nullable operationError);
+@property (nonatomic, copy, nullable) void (^discoverUserInfosCompletionBlock)(NSDictionary<NSString *, CKDiscoveredUserInfo *> * _Nullable emailsToUserInfos, NSDictionary<CKRecordID *, CKDiscoveredUserInfo *> * _Nullable userRecordIDsToUserInfos, NSError * _Nullable operationError);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoveredUserInfo.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoveredUserInfo.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoveredUserInfo.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDiscoveredUserInfo.h	2016-05-27 06:59:12.000000000 +0200
@@ -7,21 +7,21 @@
 
 #import <Foundation/Foundation.h>
 
-#if (TARGET_OS_MAC && !TARGET_OS_IPHONE && !TARGET_OS_SIMULATOR && !TARGET_OS_EMBEDDED) || TARGET_OS_IOS
+#if (TARGET_OS_MAC && !defined(__i386__) && !TARGET_OS_IPHONE && !TARGET_OS_SIMULATOR && !TARGET_OS_EMBEDDED) || TARGET_OS_IOS
 #import <Contacts/CNContact.h>
 #endif
 
 @class CKRecordID;
 
 NS_ASSUME_NONNULL_BEGIN
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Replaced by CKUserIdentity")
 @interface CKDiscoveredUserInfo : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
 
 @property (nonatomic, readonly, copy, nullable) CKRecordID *userRecordID;
 
-#if (TARGET_OS_MAC && !TARGET_OS_IPHONE && !TARGET_OS_SIMULATOR && !TARGET_OS_EMBEDDED) || TARGET_OS_IOS
+#if (TARGET_OS_MAC && !defined(__i386__) && !TARGET_OS_IPHONE && !TARGET_OS_SIMULATOR && !TARGET_OS_EMBEDDED) || TARGET_OS_IOS
 
 @property (nonatomic, readonly, copy, nullable) NSString *firstName NS_DEPRECATED(10_10, 10_11, 8_0, 9_0, "Use -[[CKDiscoveredUserInfo displayContact] givenName]");
 @property (nonatomic, readonly, copy, nullable) NSString *lastName NS_DEPRECATED(10_10, 10_11, 8_0, 9_0, "Use -[[CKDiscoveredUserInfo displayContact] familyName]");
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKError.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKError.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKError.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKError.h	2016-06-02 07:24:52.000000000 +0200
@@ -12,6 +12,8 @@
 
 CK_EXTERN NSString * const CKErrorDomain NS_AVAILABLE(10_10, 8_0);
 
+/* When a CKErrorPartialFailure happens this key will be set in the error's userInfo dictionary.
+   The value of this key will be a dictionary, and the values will be errors for individual items with the keys being the item IDs that failed. */ 
 CK_EXTERN NSString * const CKPartialErrorsByItemIDKey NS_AVAILABLE(10_10, 8_0);
 
 /* If the server rejects a record save because it has been modified since the last time it was read, 
@@ -29,34 +31,39 @@
 CK_EXTERN NSString * const CKErrorRetryAfterKey NS_AVAILABLE(10_10, 8_0);
 
 typedef NS_ENUM(NSInteger, CKErrorCode) {
-    CKErrorInternalError           = 1,  /* CloudKit.framework encountered an error.  This is a non-recoverable error. */
-    CKErrorPartialFailure          = 2,  /* Some items failed, but the operation succeeded overall */
-    CKErrorNetworkUnavailable      = 3,  /* Network not available */
-    CKErrorNetworkFailure          = 4,  /* Network error (available but CFNetwork gave us an error) */
-    CKErrorBadContainer            = 5,  /* Un-provisioned or unauthorized container. Try provisioning the container before retrying the operation. */
-    CKErrorServiceUnavailable      = 6,  /* Service unavailable */
-    CKErrorRequestRateLimited      = 7,  /* Client is being rate limited */
-    CKErrorMissingEntitlement      = 8,  /* Missing entitlement */
-    CKErrorNotAuthenticated        = 9,  /* Not authenticated (writing without being logged in, no user record) */
-    CKErrorPermissionFailure       = 10, /* Access failure (save or fetch) */
-    CKErrorUnknownItem             = 11, /* Record does not exist */
-    CKErrorInvalidArguments        = 12, /* Bad client request (bad record graph, malformed predicate) */
-    CKErrorResultsTruncated        = 13, /* Query results were truncated by the server */
-    CKErrorServerRecordChanged     = 14, /* The record was rejected because the version on the server was different */
-    CKErrorServerRejectedRequest   = 15, /* The server rejected this request.  This is a non-recoverable error */
-    CKErrorAssetFileNotFound       = 16, /* Asset file was not found */
-    CKErrorAssetFileModified       = 17, /* Asset file content was modified while being saved */
-    CKErrorIncompatibleVersion     = 18, /* App version is less than the minimum allowed version */
-    CKErrorConstraintViolation     = 19, /* The server rejected the request because there was a conflict with a unique field. */
-    CKErrorOperationCancelled      = 20, /* A CKOperation was explicitly cancelled */
-    CKErrorChangeTokenExpired      = 21, /* The previousServerChangeToken value is too old and the client must re-sync from scratch */
-    CKErrorBatchRequestFailed      = 22, /* One of the items in this batch operation failed in a zone with atomic updates, so the entire batch was rejected. */
-    CKErrorZoneBusy                = 23, /* The server is too busy to handle this zone operation. Try the operation again in a few seconds. */
-    CKErrorBadDatabase             = 24, /* Operation could not be completed on the given database. Likely caused by attempting to modify zones in the public database. */
-    CKErrorQuotaExceeded           = 25, /* Saving a record would exceed quota */
-    CKErrorZoneNotFound            = 26, /* The specified zone does not exist on the server */
-    CKErrorLimitExceeded           = 27, /* The request to the server was too large. Retry this request as a smaller batch. */
-    CKErrorUserDeletedZone         = 28, /* The user deleted this zone through the settings UI. Your client should either remove its local data or prompt the user before attempting to re-upload any data to this zone. */
+    CKErrorInternalError                  = 1,  /* CloudKit.framework encountered an error.  This is a non-recoverable error. */
+    CKErrorPartialFailure                 = 2,  /* Some items failed, but the operation succeeded overall. Check CKPartialErrorsByItemIDKey in the userInfo dictionary for more details. */
+    CKErrorNetworkUnavailable             = 3,  /* Network not available */
+    CKErrorNetworkFailure                 = 4,  /* Network error (available but CFNetwork gave us an error) */
+    CKErrorBadContainer                   = 5,  /* Un-provisioned or unauthorized container. Try provisioning the container before retrying the operation. */
+    CKErrorServiceUnavailable             = 6,  /* Service unavailable */
+    CKErrorRequestRateLimited             = 7,  /* Client is being rate limited */
+    CKErrorMissingEntitlement             = 8,  /* Missing entitlement */
+    CKErrorNotAuthenticated               = 9,  /* Not authenticated (writing without being logged in, no user record) */
+    CKErrorPermissionFailure              = 10, /* Access failure (save, fetch, or shareAccept) */
+    CKErrorUnknownItem                    = 11, /* Record does not exist */
+    CKErrorInvalidArguments               = 12, /* Bad client request (bad record graph, malformed predicate) */
+    CKErrorResultsTruncated NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Will not be returned") = 13,
+    CKErrorServerRecordChanged            = 14, /* The record was rejected because the version on the server was different */
+    CKErrorServerRejectedRequest          = 15, /* The server rejected this request.  This is a non-recoverable error */
+    CKErrorAssetFileNotFound              = 16, /* Asset file was not found */
+    CKErrorAssetFileModified              = 17, /* Asset file content was modified while being saved */
+    CKErrorIncompatibleVersion            = 18, /* App version is less than the minimum allowed version */
+    CKErrorConstraintViolation            = 19, /* The server rejected the request because there was a conflict with a unique field. */
+    CKErrorOperationCancelled             = 20, /* A CKOperation was explicitly cancelled */
+    CKErrorChangeTokenExpired             = 21, /* The previousServerChangeToken value is too old and the client must re-sync from scratch */
+    CKErrorBatchRequestFailed             = 22, /* One of the items in this batch operation failed in a zone with atomic updates, so the entire batch was rejected. */
+    CKErrorZoneBusy                       = 23, /* The server is too busy to handle this zone operation. Try the operation again in a few seconds. */
+    CKErrorBadDatabase                    = 24, /* Operation could not be completed on the given database. Likely caused by attempting to modify zones in the public database. */
+    CKErrorQuotaExceeded                  = 25, /* Saving a record would exceed quota */
+    CKErrorZoneNotFound                   = 26, /* The specified zone does not exist on the server */
+    CKErrorLimitExceeded                  = 27, /* The request to the server was too large. Retry this request as a smaller batch. */
+    CKErrorUserDeletedZone                = 28, /* The user deleted this zone through the settings UI. Your client should either remove its local data or prompt the user before attempting to re-upload any data to this zone. */
+    CKErrorTooManyParticipants            = 29, /* A share cannot be saved because there are too many participants attached to the share */
+    CKErrorAlreadyShared                  = 30, /* A record/share cannot be saved, doing so would cause a hierarchy of records to exist in multiple shares */
+    CKErrorReferenceViolation             = 31, /* The target of a record's parent or share reference was not found */
+    CKErrorManagedAccountRestricted       = 32, /* Request was rejected due to a managed account restriction */
+    CKErrorParticipantMayNeedVerification = 33, /* Share Metadata cannot be determined, because the user is not a member of the share.  There are invited participants on the share with email addresses or phone numbers not associated with any iCloud account. The user may be able to join the share if they can associate one of those email addresses or phone numbers with their iCloud account via the system Share Accept UI. Call UIApplication's openURL on this share URL to have the user attempt to verify their information. */
 } NS_ENUM_AVAILABLE(10_10, 8_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchDatabaseChangesOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchDatabaseChangesOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchDatabaseChangesOperation.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchDatabaseChangesOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -0,0 +1,49 @@
+//
+//  CKFetchDatabaseChangesOperation.h
+//  CloudKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <CloudKit/CKDatabaseOperation.h>
+
+@class CKRecordZoneID, CKServerChangeToken;
+
+NS_ASSUME_NONNULL_BEGIN
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CKFetchDatabaseChangesOperation : CKDatabaseOperation
+
+/* This operation will fetch changes to record zones within a database
+ If a change anchor from a previous CKFetchDatabaseChangesOperation is passed in, only the zones that have changed since that anchor will be returned.
+ This per-database serverChangeToken is not to be confused with the per-recordZone serverChangeToken from
+ CKFetchRecordZoneChangesOperation.
+ If this is your first fetch or if you wish to re-fetch all zones, pass nil for the change token.
+ Change token are opaque tokens and clients should not infer any behavior based on their content. */
+- (instancetype)initWithPreviousServerChangeToken:(nullable CKServerChangeToken *)previousServerChangeToken;
+
+@property (nonatomic, copy, nullable) CKServerChangeToken *previousServerChangeToken;
+@property (nonatomic, assign) NSUInteger resultsLimit;
+
+/* When set to YES, this operation will send repeated requests to the server until all record zone changes have been fetched.
+ changeTokenUpdatedBlock will be invoked periodically, to give clients an updated change token so that already-fetched
+ record zone changes don't need to be re-fetched on a subsequent operation.
+ When set to NO, it is the responsibility of the caller to issue subsequent fetch-changes operations when moreComing is YES
+ in a fetchDatabaseChangesCompletionBlock invocation.
+ fetchAllChanges is YES by default */
+@property (nonatomic, assign) BOOL fetchAllChanges;
+
+@property (nonatomic, copy, nullable) void (^recordZoneWithIDChangedBlock)(CKRecordZoneID *zoneID);
+@property (nonatomic, copy, nullable) void (^recordZoneWithIDWasDeletedBlock)(CKRecordZoneID *zoneID);
+
+@property (nonatomic, copy, nullable) void (^changeTokenUpdatedBlock)(CKServerChangeToken * serverChangeToken);
+
+/* Clients are responsible for saving the change token at the end of the operation and passing it in to the next call to CKFetchDatabaseChangesOperation.
+ If the server returns a CKErrorChangeTokenExpired error, the previousServerChangeToken value was too old and the client should toss its local cache and
+ re-fetch the changes in this record zone starting with a nil previousServerChangeToken.
+ If moreComing is true then the server wasn't able to return all the changes in this response.
+ Another CKFetchDatabaseChangesOperation operation should be run with the previousServerChangeToken token from this operation.
+ */
+@property (nonatomic, copy, nullable) void (^fetchDatabaseChangesCompletionBlock)(CKServerChangeToken * _Nullable serverChangeToken, BOOL moreComing, NSError * _Nullable operationError);
+
+@end
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchNotificationChangesOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchNotificationChangesOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchNotificationChangesOperation.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchNotificationChangesOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -35,7 +35,7 @@
     block so that already fetched notifications don't need to be re-downloaded on a subsequent operation.
    If the server returns a CKErrorChangeTokenExpired error, the previousServerChangeToken value was too old and the client should toss its local cache and
    re-fetch notification changes starting with a nil previousServerChangeToken. */
-@property (nonatomic, copy, nullable) void (^fetchNotificationChangesCompletionBlock)(CKServerChangeToken * __nullable serverChangeToken, NSError * __nullable operationError);
+@property (nonatomic, copy, nullable) void (^fetchNotificationChangesCompletionBlock)(CKServerChangeToken * _Nullable serverChangeToken, NSError * _Nullable operationError);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordChangesOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordChangesOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordChangesOperation.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordChangesOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -10,8 +10,11 @@
 
 @class CKRecord, CKRecordID, CKRecordZoneID;
 
+/* Use CKFetchRecordZoneChangesOperation instead of this class.
+ Any serverChangeTokens saved from a CKFetchRecordChangesOperation are usable as a serverRecordZoneChangeToken in CKFetchRecordZoneChangesOperation */
+
 NS_ASSUME_NONNULL_BEGIN
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use CKFetchRecordZoneChangesOperation instead")
 @interface CKFetchRecordChangesOperation : CKDatabaseOperation
 
 /* This operation will fetch records changes in the given record zone.
@@ -30,7 +33,7 @@
 @property (nonatomic, assign) NSUInteger resultsLimit;
 
 /* Declares which user-defined keys should be fetched and added to the resulting CKRecords.  If nil, declares the entire record should be downloaded. If set to an empty array, declares that no user fields should be downloaded.  Defaults to nil. */
-@property (nonatomic, copy, nullable) NSArray <NSString *> *desiredKeys;
+@property (nonatomic, copy, nullable) NSArray<NSString *> *desiredKeys;
 
 @property (nonatomic, copy, nullable) void (^recordChangedBlock)(CKRecord *record);
 @property (nonatomic, copy, nullable) void (^recordWithIDWasDeletedBlock)(CKRecordID *recordID);
@@ -42,10 +45,10 @@
 /* Clients are responsible for saving the change token at the end of the operation and passing it in to the next call to CKFetchRecordChangesOperation.
    Note that a fetch can fail partway. If that happens, an updated change token may be returned in the completion
     block so that already fetched records don't need to be re-downloaded on a subsequent operation.
-   The clientChangeToken from the most recent CKModifyRecordsOperation is also returned, or nil if none was provided. 
+   The clientChangeTokenData from the most recent CKModifyRecordsOperation is also returned, or nil if none was provided.
    If the server returns a CKErrorChangeTokenExpired error, the previousServerChangeToken value was too old and the client should toss its local cache and 
     re-fetch the changes in this record zone starting with a nil previousServerChangeToken. */
-@property (nonatomic, copy, nullable) void (^fetchRecordChangesCompletionBlock)(CKServerChangeToken * __nullable serverChangeToken, NSData * __nullable clientChangeTokenData, NSError * __nullable operationError);
+@property (nonatomic, copy, nullable) void (^fetchRecordChangesCompletionBlock)(CKServerChangeToken * _Nullable serverChangeToken, NSData * _Nullable clientChangeTokenData, NSError * _Nullable operationError);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZoneChangesOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZoneChangesOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZoneChangesOperation.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZoneChangesOperation.h	2016-06-02 07:24:52.000000000 +0200
@@ -0,0 +1,68 @@
+//
+//  CKFetchRecordZoneChangesOperation.h
+//  CloudKit
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <CloudKit/CKDatabaseOperation.h>
+#import <CloudKit/CKServerChangeToken.h>
+
+@class CKRecord, CKRecordID, CKRecordZoneID, CKFetchRecordZoneChangesOptions;
+
+NS_ASSUME_NONNULL_BEGIN
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CKFetchRecordZoneChangesOperation : CKDatabaseOperation
+
+/* This operation will fetch records changes across the given record zones
+
+ For each previousServerChangeToken passed in with a CKFetchRecordZoneChangesOptions, 
+ only records that have changed since that anchor will be fetched.
+
+ If this is your first fetch of a zone or if you wish to re-fetch all records within a zone, do not
+ include a previousServerChangeToken.
+
+ Change tokens are opaque tokens and clients should not infer any behavior based on their content. */
+- (instancetype)initWithRecordZoneIDs:(NSArray<CKRecordZoneID *> *)recordZoneIDs optionsByRecordZoneID:(nullable NSDictionary<CKRecordZoneID *, CKFetchRecordZoneChangesOptions *> *)optionsByRecordZoneID;
+
+@property (nonatomic, copy) NSArray<CKRecordZoneID *> *recordZoneIDs;
+@property (nonatomic, copy, nullable) NSDictionary<CKRecordZoneID *, CKFetchRecordZoneChangesOptions *> *optionsByRecordZoneID;
+
+/* When set to YES, this operation will send repeated requests to the server until all record changes have been fetched.
+ recordZoneChangeTokensUpdatedBlock will be invoked periodically, to give clients an updated change token so that already-fetched
+ record changes don't need to be re-fetched on a subsequent operation.
+ When set to NO, it is the responsibility of the caller to issue subsequent fetch-changes operations when moreComing is YES
+ in a recordZoneFetchCompletionBlock invocation.
+ fetchAllChanges is YES by default */
+@property (nonatomic, assign) BOOL fetchAllChanges;
+
+@property (nonatomic, copy, nullable) void (^recordChangedBlock)(CKRecord *record);
+@property (nonatomic, copy, nullable) void (^recordWithIDWasDeletedBlock)(CKRecordID *recordID, NSString *recordType);
+
+/* Clients are responsible for saving this per-recordZone serverChangeToken and passing it in to the next call to CKFetchRecordZoneChangesOperation.
+ Note that a fetch can fail partway. If that happens, an updated change token may be returned in this
+ block so that already fetched records don't need to be re-downloaded on a subsequent operation.
+ The clientChangeTokenData from the most recent CKModifyRecordsOperation issued on this zone is also returned, or nil if none was provided.
+ If the server returns a CKErrorChangeTokenExpired error, the serverChangeToken used for this record zone when initting this operation was too old and the client should toss its local cache and re-fetch the changes in this record zone starting with a nil serverChangeToken. */
+@property (nonatomic, copy, nullable) void (^recordZoneChangeTokensUpdatedBlock)(CKRecordZoneID *recordZoneID, CKServerChangeToken * _Nullable serverChangeToken, NSData * _Nullable clientChangeTokenData);
+@property (nonatomic, copy, nullable) void (^recordZoneFetchCompletionBlock)(CKRecordZoneID *recordZoneID, CKServerChangeToken * _Nullable serverChangeToken, NSData * _Nullable clientChangeTokenData, BOOL moreComing, NSError * _Nullable recordZoneError);
+
+/* serverChangeTokens previously returned via a recordZoneFetchCompletionBlock invocation,
+ along with the record changes that preceded it, are valid even if there is a subsequent operationError */
+@property (nonatomic, copy, nullable) void (^fetchRecordZoneChangesCompletionBlock)(NSError * _Nullable operationError);
+
+@end
+
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CKFetchRecordZoneChangesOptions : NSObject <NSSecureCoding>
+
+@property (nonatomic, copy, nullable) CKServerChangeToken *previousServerChangeToken;
+
+@property (nonatomic, assign) NSUInteger resultsLimit;
+
+/* Declares which user-defined keys should be fetched and added to the resulting CKRecords.  If nil, declares the entire record should be downloaded. If set to an empty array, declares that no user fields should be downloaded.  Defaults to nil. */
+@property (nonatomic, copy, nullable) NSArray<NSString *> *desiredKeys;
+
+@end
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZonesOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZonesOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZonesOperation.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZonesOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -13,19 +13,19 @@
 NS_CLASS_AVAILABLE(10_10, 8_0)
 @interface CKFetchRecordZonesOperation : CKDatabaseOperation
 
-+ (instancetype)fetchAllRecordZonesOperation;
++ (instancetype)fetchAllRecordZonesOperation NS_SWIFT_NAME(fetchAllRecordZonesOperation());
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
-- (instancetype)initWithRecordZoneIDs:(NSArray <CKRecordZoneID *> *)zoneIDs;
+- (instancetype)initWithRecordZoneIDs:(NSArray<CKRecordZoneID *> *)zoneIDs;
 
-@property (nonatomic, copy, nullable) NSArray <CKRecordZoneID *> *recordZoneIDs;
+@property (nonatomic, copy, nullable) NSArray<CKRecordZoneID *> *recordZoneIDs;
 
 /*  This block is called when the operation completes.
     The [NSOperation completionBlock] will also be called if both are set.
     If the error is CKErrorPartialFailure, the error's userInfo dictionary contains
     a dictionary of zoneIDs to errors keyed off of CKPartialErrorsByItemIDKey.
 */
-@property (nonatomic, copy, nullable) void (^fetchRecordZonesCompletionBlock)(NSDictionary <CKRecordZoneID *, CKRecordZone *> * __nullable recordZonesByZoneID, NSError * __nullable operationError);
+@property (nonatomic, copy, nullable) void (^fetchRecordZonesCompletionBlock)(NSDictionary<CKRecordZoneID *, CKRecordZone *> * _Nullable recordZonesByZoneID, NSError * _Nullable operationError);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordsOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordsOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordsOperation.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordsOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -14,26 +14,26 @@
 @interface CKFetchRecordsOperation : CKDatabaseOperation
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
-- (instancetype)initWithRecordIDs:(NSArray <CKRecordID *> *)recordIDs;
+- (instancetype)initWithRecordIDs:(NSArray<CKRecordID *> *)recordIDs;
 
-+ (instancetype)fetchCurrentUserRecordOperation;
++ (instancetype)fetchCurrentUserRecordOperation NS_SWIFT_NAME(fetchCurrentUserRecordOperation());
 
-@property (nonatomic, copy, nullable) NSArray <CKRecordID *> *recordIDs;
+@property (nonatomic, copy, nullable) NSArray<CKRecordID *> *recordIDs;
 
 /* Declares which user-defined keys should be fetched and added to the resulting CKRecords.  If nil, declares the entire record should be downloaded. If set to an empty array, declares that no user fields should be downloaded.  Defaults to nil. */
-@property (nonatomic, copy, nullable) NSArray <NSString *> *desiredKeys;
+@property (nonatomic, copy, nullable) NSArray<NSString *> *desiredKeys;
 
 /* Called repeatedly during transfer. */
 @property (nonatomic, copy, nullable) void (^perRecordProgressBlock)(CKRecordID *recordID, double progress);
 /* Called on success or failure for each record. */
-@property (nonatomic, copy, nullable) void (^perRecordCompletionBlock)(CKRecord * __nullable record, CKRecordID * __nullable recordID, NSError * __nullable error);
+@property (nonatomic, copy, nullable) void (^perRecordCompletionBlock)(CKRecord * _Nullable record, CKRecordID * _Nullable recordID, NSError * _Nullable error);
 
 /*  This block is called when the operation completes.
     The [NSOperation completionBlock] will also be called if both are set.
     If the error is CKErrorPartialFailure, the error's userInfo dictionary contains
     a dictionary of recordIDs to errors keyed off of CKPartialErrorsByItemIDKey.
 */
-@property (nonatomic, copy, nullable) void (^fetchRecordsCompletionBlock)(NSDictionary <CKRecordID * , CKRecord *> * __nullable recordsByRecordID, NSError * __nullable operationError);
+@property (nonatomic, copy, nullable) void (^fetchRecordsCompletionBlock)(NSDictionary<CKRecordID * , CKRecord *> * _Nullable recordsByRecordID, NSError * _Nullable operationError);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareMetadataOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareMetadataOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareMetadataOperation.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareMetadataOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -0,0 +1,35 @@
+//
+//  CKFetchShareMetadataOperation.h
+//  CloudKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <CloudKit/CKOperation.h>
+
+/* Since you can't know what container this share is in before you fetch its metadata, you may run this operation in any container you have access to */
+
+@class CKShareMetadata, CKFetchShareMetadataOptions;
+
+NS_ASSUME_NONNULL_BEGIN
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CKFetchShareMetadataOperation : CKOperation
+
+- (instancetype)initWithShareURLs:(NSArray<NSURL *> *)shareURLs;
+
+@property (nonatomic, copy) NSArray<NSURL *> *shareURLs;
+
+/* If set to YES, the resulting CKShareMetadata will have a rootRecord object filled out.  Defaults to NO.
+ The resulting CKShareMetadata will have a rootRecordID property regardless of the value of this property. */
+@property (nonatomic, assign) BOOL shouldFetchRootRecord;
+
+/* Declares which user-defined keys should be fetched and added to the resulting rootRecord.  Only consulted if shouldFetchRootRecord is YES.
+ If nil, declares the entire root record should be downloaded. If set to an empty array, declares that no user fields should be downloaded.  Defaults to nil. */
+@property (nonatomic, copy, nullable) NSArray<NSString *> *rootRecordDesiredKeys;
+
+@property (nonatomic, copy, nullable) void (^perShareMetadataBlock)(NSURL *shareURL, CKShareMetadata * _Nullable shareMetadata, NSError * _Nullable error);
+
+@property (nonatomic, copy, nullable) void (^fetchShareMetadataCompletionBlock)(NSError * _Nullable operationError);
+
+@end
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareParticipantsOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareParticipantsOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareParticipantsOperation.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareParticipantsOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -0,0 +1,33 @@
+//
+//  CKFetchShareParticipantsOperation.h
+//  CloudKit
+//
+//  Copyright (c) 2014 Apple Inc. All rights reserved.
+//
+
+#import <CloudKit/CKOperation.h>
+
+@class CKUserIdentityLookupInfo, CKShareParticipant, CKRecordID;
+
+NS_ASSUME_NONNULL_BEGIN
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CKFetchShareParticipantsOperation : CKOperation
+
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
+
+- (instancetype)initWithUserIdentityLookupInfos:(NSArray<CKUserIdentityLookupInfo *> *)userIdentityLookupInfos;
+
+@property (nonatomic, copy) NSArray<CKUserIdentityLookupInfo *> *userIdentityLookupInfos;
+
+@property (nonatomic, copy, nullable) void (^shareParticipantFetchedBlock)(CKShareParticipant *participant);
+
+/*  This block is called when the operation completes.
+ The [NSOperation completionBlock] will also be called if both are set.
+ If the error is CKErrorPartialFailure, the error's userInfo dictionary contains
+ a dictionary of lookup infos to errors keyed off of CKPartialErrorsByItemIDKey.
+ */
+@property (nonatomic, copy, nullable) void (^fetchShareParticipantsCompletionBlock)(NSError *operationError);
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchSubscriptionsOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchSubscriptionsOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchSubscriptionsOperation.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchSubscriptionsOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -16,18 +16,18 @@
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
 
-+ (instancetype)fetchAllSubscriptionsOperation;
++ (instancetype)fetchAllSubscriptionsOperation NS_SWIFT_NAME(fetchAllSubscriptionsOperation());
 
-- (instancetype)initWithSubscriptionIDs:(NSArray <NSString *> *)subscriptionIDs;
+- (instancetype)initWithSubscriptionIDs:(NSArray<NSString *> *)subscriptionIDs;
 
-@property (nonatomic, copy, nullable) NSArray <NSString *> *subscriptionIDs;
+@property (nonatomic, copy, nullable) NSArray<NSString *> *subscriptionIDs;
 
 /*  This block is called when the operation completes.
     The [NSOperation completionBlock] will also be called if both are set.
     If the error is CKErrorPartialFailure, the error's userInfo dictionary contains
     a dictionary of subscriptionID to errors keyed off of CKPartialErrorsByItemIDKey.
 */
-@property (nonatomic, copy, nullable) void (^fetchSubscriptionCompletionBlock)(NSDictionary <NSString *, CKSubscription *> * __nullable subscriptionsBySubscriptionID, NSError * __nullable operationError);
+@property (nonatomic, copy, nullable) void (^fetchSubscriptionCompletionBlock)(NSDictionary<NSString *, CKSubscription *> * _Nullable subscriptionsBySubscriptionID, NSError * _Nullable operationError);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchWebAuthTokenOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchWebAuthTokenOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchWebAuthTokenOperation.h	2015-10-30 02:03:56.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchWebAuthTokenOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -16,9 +16,10 @@
  */
 - (instancetype)initWithAPIToken:(NSString *)APIToken NS_DESIGNATED_INITIALIZER;
 
-@property (nonatomic, copy) NSString *APIToken;
+/* APIToken is expected to be set before you begin this operation. */
+@property (nonatomic, copy, nullable) NSString *APIToken;
 
 @property (nonatomic, copy, nullable) void (^fetchWebAuthTokenCompletionBlock)(NSString *webAuthToken, NSError *operationError);
 
 @end
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKMarkNotificationsReadOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKMarkNotificationsReadOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKMarkNotificationsReadOperation.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKMarkNotificationsReadOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -14,13 +14,13 @@
 NS_CLASS_AVAILABLE(10_10, 8_0)
 @interface CKMarkNotificationsReadOperation : CKOperation
 
-- (instancetype)init NS_UNAVAILABLE;
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
 
-- (instancetype)initWithNotificationIDsToMarkRead:(NSArray <CKNotificationID *> *)notificationIDs NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithNotificationIDsToMarkRead:(NSArray<CKNotificationID *> *)notificationIDs;
 
-@property (nonatomic, copy) NSArray <CKNotificationID *> *notificationIDs;
+@property (nonatomic, copy) NSArray<CKNotificationID *> *notificationIDs;
 
-@property (nonatomic, copy, nullable) void (^markNotificationsReadCompletionBlock)(NSArray <CKNotificationID *> * __nullable notificationIDsMarkedRead, NSError * __nullable operationError);
+@property (nonatomic, copy, nullable) void (^markNotificationsReadCompletionBlock)(NSArray<CKNotificationID *> * _Nullable notificationIDsMarkedRead, NSError * _Nullable operationError);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyBadgeOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyBadgeOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyBadgeOperation.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyBadgeOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -18,7 +18,7 @@
 
 /*  This block is called when the operation completes.
     The [NSOperation completionBlock] will also be called if both are set. */
-@property (nonatomic, copy, nullable) void (^modifyBadgeCompletionBlock)(NSError * __nullable operationError);
+@property (nonatomic, copy, nullable) void (^modifyBadgeCompletionBlock)(NSError * _Nullable operationError);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyRecordZonesOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyRecordZonesOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyRecordZonesOperation.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyRecordZonesOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -7,15 +7,17 @@
 
 #import <CloudKit/CKDatabaseOperation.h>
 
+@class CKRecordZone, CKRecordZoneID;
+
 NS_ASSUME_NONNULL_BEGIN
 NS_CLASS_AVAILABLE(10_10, 8_0)
 @interface CKModifyRecordZonesOperation : CKDatabaseOperation
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
-- (instancetype)initWithRecordZonesToSave:(nullable NSArray <CKRecordZone *> *)recordZonesToSave recordZoneIDsToDelete:(nullable NSArray <CKRecordZoneID *> *)recordZoneIDsToDelete;
+- (instancetype)initWithRecordZonesToSave:(nullable NSArray<CKRecordZone *> *)recordZonesToSave recordZoneIDsToDelete:(nullable NSArray<CKRecordZoneID *> *)recordZoneIDsToDelete;
 
-@property (nonatomic, copy, nullable) NSArray <CKRecordZone *> *recordZonesToSave;
-@property (nonatomic, copy, nullable) NSArray <CKRecordZoneID *> *recordZoneIDsToDelete;
+@property (nonatomic, copy, nullable) NSArray<CKRecordZone *> *recordZonesToSave;
+@property (nonatomic, copy, nullable) NSArray<CKRecordZoneID *> *recordZoneIDsToDelete;
 
 /*  This block is called when the operation completes.
  The [NSOperation completionBlock] will also be called if both are set.
@@ -25,7 +27,7 @@
  seen all record changes, and may be invoked while the server is processing the side effects
  of those changes.
  */
-@property (nonatomic, copy, nullable) void (^modifyRecordZonesCompletionBlock)(NSArray <CKRecordZone *> * __nullable savedRecordZones, NSArray <CKRecordZoneID *> * __nullable deletedRecordZoneIDs, NSError * __nullable operationError);
+@property (nonatomic, copy, nullable) void (^modifyRecordZonesCompletionBlock)(NSArray<CKRecordZone *> * _Nullable savedRecordZones, NSArray<CKRecordZoneID *> * _Nullable deletedRecordZoneIDs, NSError * _Nullable operationError);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyRecordsOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyRecordsOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyRecordsOperation.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyRecordsOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -27,10 +27,10 @@
 @interface CKModifyRecordsOperation : CKDatabaseOperation
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
-- (instancetype)initWithRecordsToSave:(nullable NSArray <CKRecord *> *)records recordIDsToDelete:(nullable NSArray <CKRecordID *> *)recordIDs;
+- (instancetype)initWithRecordsToSave:(nullable NSArray<CKRecord *> *)records recordIDsToDelete:(nullable NSArray<CKRecordID *> *)recordIDs;
 
-@property (nonatomic, copy, nullable) NSArray <CKRecord *> *recordsToSave;
-@property (nonatomic, copy, nullable) NSArray <CKRecordID *> *recordIDsToDelete;
+@property (nonatomic, copy, nullable) NSArray<CKRecord *> *recordsToSave;
+@property (nonatomic, copy, nullable) NSArray<CKRecordID *> *recordIDsToDelete;
 
 /* The default value is CKRecordSaveIfServerRecordUnchanged. */
 @property (nonatomic, assign) CKRecordSavePolicy savePolicy;
@@ -40,15 +40,15 @@
 @property (nonatomic, copy, nullable) NSData *clientChangeTokenData;
 
 /* Determines whether the batch should fail atomically or not. YES by default.
-   This only applies to zones that support CKRecordZoneCapabilityAtomic */
-@property (nonatomic, assign) BOOL atomic;
+   This only applies to zones that support CKRecordZoneCapabilityAtomic. */
+@property (nonatomic, assign) BOOL atomic NS_SWIFT_NAME(isAtomic);
 
 /* Called repeatedly during transfer.
  It is possible for progress to regress when a retry is automatically triggered.
 */
 @property (nonatomic, copy, nullable) void (^perRecordProgressBlock)(CKRecord *record, double progress);
 /* Called on success or failure for each record. */
-@property (nonatomic, copy, nullable) void (^perRecordCompletionBlock)(CKRecord * __nullable record, NSError * __nullable error);
+@property (nonatomic, copy, nullable) void (^perRecordCompletionBlock)(CKRecord * _Nullable record, NSError * _Nullable error);
 
 /*  This block is called when the operation completes.
  The [NSOperation completionBlock] will also be called if both are set.
@@ -58,7 +58,7 @@
  seen all record changes, and may be invoked while the server is processing the side effects
  of those changes.
 */
-@property (nonatomic, copy, nullable) void (^modifyRecordsCompletionBlock)(NSArray <CKRecord *> * __nullable savedRecords, NSArray <CKRecordID *> * __nullable deletedRecordIDs, NSError * __nullable operationError);
+@property (nonatomic, copy, nullable) void (^modifyRecordsCompletionBlock)(NSArray<CKRecord *> * _Nullable savedRecords, NSArray<CKRecordID *> * _Nullable deletedRecordIDs, NSError * _Nullable operationError);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifySubscriptionsOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifySubscriptionsOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifySubscriptionsOperation.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifySubscriptionsOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -13,17 +13,17 @@
 NS_CLASS_AVAILABLE(10_10, 8_0)
 @interface CKModifySubscriptionsOperation : CKDatabaseOperation
 
-- (instancetype)initWithSubscriptionsToSave:(nullable NSArray <CKSubscription *> *)subscriptionsToSave subscriptionIDsToDelete:(nullable NSArray <NSString *> *)subscriptionIDsToDelete NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithSubscriptionsToSave:(nullable NSArray<CKSubscription *> *)subscriptionsToSave subscriptionIDsToDelete:(nullable NSArray<NSString *> *)subscriptionIDsToDelete NS_DESIGNATED_INITIALIZER;
 
-@property (nonatomic, copy, nullable) NSArray <CKSubscription *> *subscriptionsToSave;
-@property (nonatomic, copy, nullable) NSArray <NSString *> *subscriptionIDsToDelete;
+@property (nonatomic, copy, nullable) NSArray<CKSubscription *> *subscriptionsToSave;
+@property (nonatomic, copy, nullable) NSArray<NSString *> *subscriptionIDsToDelete;
 
 /*  This block is called when the operation completes.
     The [NSOperation completionBlock] will also be called if both are set.
     If the error is CKErrorPartialFailure, the error's userInfo dictionary contains
     a dictionary of subscriptionIDs to errors keyed off of CKPartialErrorsByItemIDKey.
 */
-@property (nonatomic, copy, nullable) void (^modifySubscriptionsCompletionBlock)(NSArray <CKSubscription *> * __nullable savedSubscriptions, NSArray <NSString *> * __nullable deletedSubscriptionIDs, NSError * __nullable operationError);
+@property (nonatomic, copy, nullable) void (^modifySubscriptionsCompletionBlock)(NSArray<CKSubscription *> * _Nullable savedSubscriptions, NSArray<NSString *> * _Nullable deletedSubscriptionIDs, NSError * _Nullable operationError);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKNotification.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKNotification.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKNotification.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKNotification.h	2016-05-27 07:20:20.000000000 +0200
@@ -8,6 +8,7 @@
 
 #import <Foundation/Foundation.h>
 #import <CloudKit/CKRecord.h>
+#import <CloudKit/CKDatabase.h>
 
 @class CKRecordID, CKRecordZoneID;
 
@@ -17,9 +18,10 @@
 @end
 
 typedef NS_ENUM(NSInteger, CKNotificationType) {
-    CKNotificationTypeQuery            = 1,
-    CKNotificationTypeRecordZone       = 2,
+    CKNotificationTypeQuery            = 1, /* Generated by CKQuerySubscriptions */
+    CKNotificationTypeRecordZone       = 2, /* Generated by CKRecordZoneSubscriptions */
     CKNotificationTypeReadNotification = 3, /* Indicates a notification that a client had previously marked as read. */
+    CKNotificationTypeDatabase         = 4, /* Generated by CKDatabaseSubscriptions */
 } NS_ENUM_AVAILABLE(10_10, 8_0);
 
 NS_CLASS_AVAILABLE(10_10, 8_0)
@@ -27,7 +29,7 @@
 
 - (instancetype)init NS_UNAVAILABLE;
 
-+ (instancetype)notificationFromRemoteNotificationDictionary:(NSDictionary <NSString *, NSObject *> *)notificationDictionary;
++ (instancetype)notificationFromRemoteNotificationDictionary:(NSDictionary<NSString *, NSObject *> *)notificationDictionary;
 
 /* When you instantiate a CKNotification from a remote notification dictionary, you will get back a concrete
  subclass defined below.  Use the type of notification to avoid -isKindOfClass: checks */
@@ -52,14 +54,14 @@
 /* Instead of a raw alert string, you may optionally specify a key for a localized string in your app's Localizable.strings file. */
 @property (nonatomic, readonly, copy, nullable) NSString *alertLocalizationKey __TVOS_PROHIBITED;
 /* A list of field names to take from the matching record that is used as substitution variables in a formatted alert string. */
-@property (nonatomic, readonly, copy, nullable) NSArray <NSString *> *alertLocalizationArgs __TVOS_PROHIBITED;
+@property (nonatomic, readonly, copy, nullable) NSArray<NSString *> *alertLocalizationArgs __TVOS_PROHIBITED;
 /* A key for a localized string to be used as the alert action in a modal style notification. */
 @property (nonatomic, readonly, copy, nullable) NSString *alertActionLocalizationKey __TVOS_PROHIBITED;
 /* The name of an image in your app bundle to be used as the launch image when launching in response to the notification. */
 @property (nonatomic, readonly, copy, nullable) NSString *alertLaunchImage __TVOS_PROHIBITED;
 
 /* The number to display as the badge of the application icon */
-@property (nonatomic, readonly, copy, nullable) NSNumber *badge __TVOS_PROHIBITED;
+@property (nonatomic, readonly, copy, nullable) NSNumber *badge __TVOS_AVAILABLE(10_0);
 /* The name of a sound file in your app bundle to play upon receiving the notification. */
 @property (nonatomic, readonly, copy, nullable) NSString *soundName __TVOS_PROHIBITED;
 
@@ -101,12 +103,14 @@
 
 /* A set of key->value pairs for creates and updates.  You request the server fill out this property via the
  "desiredKeys" property of CKNotificationInfo */
-@property (nonatomic, readonly, copy, nullable) NSDictionary <NSString *, __kindof id <CKRecordValue>> *recordFields;
+@property (nonatomic, readonly, copy, nullable) NSDictionary<NSString *, id> *recordFields;
 
 @property (nonatomic, readonly, copy, nullable) CKRecordID *recordID;
 
 /* If YES, this record is in the public database.  Else, it's in the private database */
-@property (nonatomic, readonly, assign) BOOL isPublicDatabase;
+@property (nonatomic, readonly, assign) BOOL isPublicDatabase NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use databaseScope instead");
+
+@property (nonatomic, readonly, assign) CKDatabaseScope databaseScope NS_AVAILABLE(10_12, 10_0);
 
 @end
 
@@ -131,5 +135,30 @@
 
 @property (nonatomic, readonly, copy, nullable) CKRecordZoneID *recordZoneID;
 
+@property (nonatomic, readonly, assign) CKDatabaseScope databaseScope NS_AVAILABLE(10_12, 10_0);
+
 @end
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+
+
+/* notificationType == CKNotificationTypeDatabase
+ When properties must be dropped (see isPruned), here's the order of importance.  The most important properties are first,
+ they'll be the last ones to be dropped.
+ - notificationID
+ - badge
+ - alertLocalizationKey
+ - alertLocalizationArgs
+ - alertBody
+ - alertActionLocalizationKey
+ - alertLaunchImage
+ - soundName
+ - containerIdentifier
+ */
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CKDatabaseNotification : CKNotification
+
+@property (nonatomic, readonly, assign) CKDatabaseScope databaseScope;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKOperation.h	2016-02-25 00:22:27.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -55,6 +55,18 @@
  */
 @property (nonatomic, assign, getter=isLongLived) BOOL longLived NS_AVAILABLE(10_12, 9_3);
 
+/* 
+   If non-zero, overrides the timeout interval for any network requests issued by this operation.
+   See NSURLSessionConfiguration.timeoutIntervalForRequest 
+*/
+@property (nonatomic, assign) NSTimeInterval timeoutIntervalForRequest NS_AVAILABLE(10_12, 9_3);
+
+/*
+ If non-zero, overrides the timeout interval for any network resources retrieved by this operation.
+ See NSURLSessionConfiguration.timeoutIntervalForResource
+ */
+@property (nonatomic, assign) NSTimeInterval timeoutIntervalForResource NS_AVAILABLE(10_12, 10_0);
+
 /*
    This callback is called after a long lived operation has begun running and is persisted. Once this callback is called the operation will continue running even if the current process exits.
  */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKQuery.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKQuery.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKQuery.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKQuery.h	2016-05-27 06:59:12.000000000 +0200
@@ -40,7 +40,7 @@
 @property (nonatomic, readonly, copy) NSString *recordType;
 @property (nonatomic, readonly, copy) NSPredicate *predicate;
 
-@property (nonatomic, copy, nullable) NSArray <NSSortDescriptor *> *sortDescriptors;
+@property (nonatomic, copy, nullable) NSArray<NSSortDescriptor *> *sortDescriptors;
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKQueryOperation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKQueryOperation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKQueryOperation.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKQueryOperation.h	2016-05-27 06:59:12.000000000 +0200
@@ -24,6 +24,7 @@
 NS_CLASS_AVAILABLE(10_10, 8_0)
 @interface CKQueryOperation : CKDatabaseOperation
 
+/* Queries invoked within a sharedCloudDatabase must specify a zoneID.  Cross-zone queries are not supported in a sharedCloudDatabase */
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
 - (instancetype)initWithQuery:(CKQuery *)query;
 - (instancetype)initWithCursor:(CKQueryCursor *)cursor;
@@ -43,14 +44,14 @@
 @property (nonatomic, assign) NSUInteger resultsLimit;
 
 /* Declares which user-defined keys should be fetched and added to the resulting CKRecords.  If nil, declares the entire record should be downloaded. If set to an empty array, declares that no user fields should be downloaded.  Defaults to nil. */
-@property (nonatomic, copy, nullable) NSArray <NSString *> *desiredKeys;
+@property (nonatomic, copy, nullable) NSArray<NSString *> *desiredKeys;
 
 /* This block will be called once for every record that is returned as a result of the query. The callbacks will happen in the order that the results were sorted in. */
 @property (nonatomic, copy, nullable) void (^recordFetchedBlock)(CKRecord *record);
 
 /*  This block is called when the operation completes.
  The [NSOperation completionBlock] will also be called if both are set. */
-@property (nonatomic, copy, nullable) void (^queryCompletionBlock)(CKQueryCursor * __nullable cursor, NSError * __nullable operationError);
+@property (nonatomic, copy, nullable) void (^queryCompletionBlock)(CKQueryCursor * _Nullable cursor, NSError * _Nullable operationError);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecord.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecord.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecord.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecord.h	2016-05-27 05:15:23.000000000 +0200
@@ -69,17 +69,17 @@
 */
 - (nullable __kindof id <CKRecordValue>)objectForKey:(NSString *)key;
 - (void)setObject:(nullable __kindof id <CKRecordValue>)object forKey:(NSString *)key;
-- (NSArray <NSString *> *)allKeys;
+- (NSArray<NSString *> *)allKeys;
 
 /* A special property that returns an array of token generated from all the string field values in the record.
    These tokens have been normalized for the current locale, so they are suitable for performing full-text searches. */
-- (NSArray <NSString *> *)allTokens;
+- (NSArray<NSString *> *)allTokens;
 
 - (nullable __kindof id <CKRecordValue>)objectForKeyedSubscript:(NSString *)key;
 - (void)setObject:(nullable __kindof id <CKRecordValue>)object forKeyedSubscript:(NSString *)key;
 
 /* A list of keys that have been modified on the local CKRecord instance */
-- (NSArray <NSString *> *)changedKeys;
+- (NSArray<NSString *> *)changedKeys;
 
 /* CKRecord supports NSSecureCoding.  When you invoke
  -encodeWithCoder: on a CKRecord, it encodes all its values.  Including the record values you've set.
@@ -93,6 +93,35 @@
  */
 - (void)encodeSystemFieldsWithCoder:(NSCoder *)coder;
 
+/* The share property on a record can be set by creating a share using -[CKShare initWithRootRecord:].
+ 
+ The share property on a record will be removed when the corresponding CKShare is deleted from the server. Send this record in the same batch as the share delete and this record's share property will be updated.
+ 
+ Sharing is only supported in zones with the CKRecordZoneCapabilitySharing capability. The default zone does not support sharing.
+ 
+ If any records have a parent reference to this record, they are implicitly shared alongside this record.
+ 
+ Note that records in a hierarchy must only exist within one share. If a child record in a hierarchy already has a share reference set then you will get a CKErrorAlreadyShared error if you try to share any of that record's parents.
+ 
+ Whenever possible, it is suggested that you construct your parent hierarchies such that you will only need to share the topmost record of that hierarchy.
+*/
+@property (nonatomic, readonly, copy, nullable) CKReference *share;
+
+/* Use a parent reference to teach CloudKit about the hierarchy of your records. This hierarchy of records will be shared if the share reference is set on a record.
+ 
+ A parent record reference must have CKReferenceActionNone set. You can create a separate reference with CKReferenceActionDeleteSelf if you would like your hierarchy cleaned up when the parent record is deleted.
+ 
+ The target of a parent reference must exist at save time - either already on the server, or part of the same CKModifyRecordsOperation batch.
+
+ You are encouraged to set up the parent relationships as part of normal record saves, even if you're not planning on sharing records at this time.  
+ This allows you to share and unshare a hierarchy of records at a later date by only modifying the "top level" record, setting or clearing its 'share' reference.
+*/
+@property (nonatomic, copy, nullable) CKReference *parent;
+
+/* Convenience wrappers around creating a CKReference to a parent record. The resulting CKReference will have action = CKReferenceActionNone */
+- (void)setParentReferenceFromRecord:(nullable CKRecord *)parentRecord NS_SWIFT_NAME(setParent(_:));
+- (void)setParentReferenceFromRecordID:(nullable CKRecordID *)parentRecordID NS_SWIFT_NAME(setParent(_:));
+
 @end
 
 @interface NSString (CKRecordValue) <CKRecordValue>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecordZone.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecordZone.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecordZone.h	2015-09-30 23:33:08.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecordZone.h	2016-05-27 06:59:12.000000000 +0200
@@ -16,6 +16,8 @@
     CKRecordZoneCapabilityFetchChanges   = 1 << 0,
     /* Batched changes to this zone happen atomically */
     CKRecordZoneCapabilityAtomic         = 1 << 1,
+    /* Records in this zone can be shared */
+    CKRecordZoneCapabilitySharing        = 1 << 2,
 } NS_AVAILABLE(10_10, 8_0);
 
 /* The default zone has no capabilities */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShare.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShare.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShare.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShare.h	2016-05-27 05:15:23.000000000 +0200
@@ -0,0 +1,73 @@
+//
+//  CKShare.h
+//  CloudKit
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <CloudKit/CKRecord.h>
+#import <CloudKit/CKShareParticipant.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+CK_EXTERN NSString * const CKRecordTypeShare NS_AVAILABLE(10_12, 10_0);
+
+/* Predefined keys in the CKRecordTypeShare schema.  They're used by the out of process UI flow to send a share, and as part of the share acceptance flow.  These are optional */
+
+/* Value is a string.  Example for a recipe sharing app: "Pot Roast" */
+CK_EXTERN NSString * const CKShareTitleKey NS_AVAILABLE(10_12, 10_0);
+/* Value is a data blob suitable to pass into -[NSImage imageWithData:] or -[UIImage imageWithData:] */
+CK_EXTERN NSString * const CKShareThumbnailImageDataKey NS_AVAILABLE(10_12, 10_0);
+/* Value is a string.  Example for a recipe sharing app: "Recipe" */
+CK_EXTERN NSString * const CKShareTypeKey NS_AVAILABLE(10_12, 10_0);
+
+/*
+ Like CKRecords, CKShares can store arbitrary key-value pairs.  They are modified and fetched in the same manner.
+ A share, its root record (and its root record's children records), will only appear in a participant's CKFetchRecordChangesOperation's results after the share has been accepted by that participant.
+ Clients have access to the share (and optionally the root record) before accepting a share, via the CKShareMetadata object.  Note that in order to access a root record before accepting a share, a third party must run a CKFetchShareMetadataOperation requesting the root record.
+ A CKShare will appear in a CKFetchRecordChangesOperation's results set whenever the participant list is updated.  For that reason, you shouldn't place heavy key-value pairs in it.
+ */
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CKShare : CKRecord
+
+- (instancetype)init NS_UNAVAILABLE;
+- (instancetype)initWithRecordType:(NSString *)recordType NS_UNAVAILABLE;
+- (instancetype)initWithRecordType:(NSString *)recordType recordID:(CKRecordID *)recordID NS_UNAVAILABLE;
+- (instancetype)initWithRecordType:(NSString *)recordType zoneID:(CKRecordZoneID *)zoneID NS_UNAVAILABLE;
+
+/* When saving a newly created CKShare, you must save the share and its rootRecord in the same CKModifyRecordsOperation batch. */
+- (instancetype)initWithRootRecord:(CKRecord *)rootRecord;
+- (instancetype)initWithRootRecord:(CKRecord *)rootRecord shareID:(CKRecordID *)shareID NS_DESIGNATED_INITIALIZER;
+
+- (instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
+
+/*
+ Shares with publicPermission more permissive than CKShareParticipantPermissionNone can be joined by any user with access to the share's shareURL.
+ This property defines what permission those users will have.
+ By default, public permission is CKShareParticipantPermissionNone.
+ Changing the public permission to CKShareParticipantPermissionNone will result in all public participants being removed when the share is saved. */
+@property (nonatomic, assign) CKShareParticipantPermission publicPermission;
+
+/* A URL that can be used to invite participants to this share. Only available after share record has been saved to the server.  This url is stable, and is tied to the rootRecord.  That is, if you share a rootRecord, delete the share, and re-share the same rootRecord via a newly created share, that newly created share's url will be identical to the prior share's url */
+@property (nonatomic, readonly, copy) NSURL *URL;
+
+/* The participants array will contain all participants on the share that the current user has permissions to see. 
+   At the minimum that will include the owner and the current user. */
+@property (nonatomic, readonly, strong) NSArray<CKShareParticipant *> *participants;
+
+/* Convenience methods for fetching special users from the participant array */
+@property (nonatomic, readonly, strong) CKShareParticipant *owner;
+@property (nonatomic, readonly, strong, nullable) CKShareParticipant *currentUserParticipant;
+
+/*
+ If a participant with a matching userIdentity already exists, then that existing participant's properties will be updated; no new participant will be added.
+ In order to modify the list of participants, a share must have publicPermission set to CKShareParticipantPermissionNone.  That is, you cannot mix-and-match private users and public users in the same share.
+ Only certain participant types may be added via this API, see the comments around CKShareParticipantType
+*/
+- (void)addParticipant:(CKShareParticipant *)participant;
+- (void)removeParticipant:(CKShareParticipant *)participant;
+
+@end
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShareMetadata.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShareMetadata.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShareMetadata.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShareMetadata.h	2016-05-27 06:59:12.000000000 +0200
@@ -0,0 +1,31 @@
+//
+//  CKShareMetadata.h
+//  CloudKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <CloudKit/CKShareParticipant.h>
+
+@class CKShare, CKRecord, CKRecordID;
+
+NS_ASSUME_NONNULL_BEGIN
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CKShareMetadata : NSObject <NSCopying, NSSecureCoding>
+
+@property (nonatomic, readonly, copy) NSString *containerIdentifier;
+@property (nonatomic, readonly, strong) CKShare *share;
+@property (nonatomic, readonly, copy) CKRecordID *rootRecordID;
+
+/* These properties reflect the participant properties of the user invoking CKFetchShareMetadataOperation */
+@property (nonatomic, readonly, assign) CKShareParticipantType participantType;
+@property (nonatomic, readonly, assign) CKShareParticipantAcceptanceStatus participantStatus;
+@property (nonatomic, readonly, assign) CKShareParticipantPermission participantPermission;
+
+@property (nonatomic, readonly, strong) CKUserIdentity *ownerIdentity;
+
+/* This is only present if the share metadata was returned from a CKFetchShareMetadataOperation with shouldFetchRootRecord set to YES */  
+@property (nonatomic, readonly, strong, nullable) CKRecord *rootRecord;
+
+@end
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShareParticipant.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShareParticipant.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShareParticipant.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShareParticipant.h	2016-05-27 06:59:12.000000000 +0200
@@ -0,0 +1,58 @@
+//
+//  CKShareParticipant.h
+//  CloudKit
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+@class CKUserIdentity;
+
+NS_ASSUME_NONNULL_BEGIN
+typedef NS_ENUM(NSInteger, CKShareParticipantAcceptanceStatus) {
+    CKShareParticipantAcceptanceStatusUnknown,
+    CKShareParticipantAcceptanceStatusPending,
+    CKShareParticipantAcceptanceStatusAccepted,
+    CKShareParticipantAcceptanceStatusRemoved,
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
+/* These permissions determine what share participants can do with records inside that share */
+typedef NS_ENUM(NSInteger, CKShareParticipantPermission) {
+    CKShareParticipantPermissionUnknown,
+    CKShareParticipantPermissionNone,
+    CKShareParticipantPermissionReadOnly,
+    CKShareParticipantPermissionReadWrite,
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
+/* The participant type determines whether a participant can modify the list of participants on a share.
+    - Owners can add private users
+    - Private users can access the share
+    - Public users are "self-added" when the participant accesses the shareURL.  Owners cannot add public users.
+ */
+typedef NS_ENUM(NSInteger, CKShareParticipantType) {
+    CKShareParticipantTypeUnknown = 0,
+    CKShareParticipantTypeOwner = 1,
+    CKShareParticipantTypePrivateUser = 3,
+    CKShareParticipantTypePublicUser = 4,
+} NS_ENUM_AVAILABLE(10_10, 8_0);
+
+
+NS_CLASS_AVAILABLE(10_10, 8_0)
+@interface CKShareParticipant : NSObject <NSSecureCoding, NSCopying>
+
+/* Use CKFetchShareParticipantsOperation to create a CKShareParticipant object */
+- (instancetype)init NS_UNAVAILABLE;
+
+@property (nonatomic, readonly, strong) CKUserIdentity *userIdentity;
+
+/* The default participant type is CKShareParticipantTypePrivateUser. */
+@property (nonatomic, assign) CKShareParticipantType type;
+
+@property (nonatomic, readonly, assign) CKShareParticipantAcceptanceStatus acceptanceStatus;
+
+/* The default permission for a new participant is CKShareParticipantPermissionReadOnly. */
+@property (nonatomic, assign) CKShareParticipantPermission permission;
+
+@end
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKSubscription.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKSubscription.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKSubscription.h	2015-10-30 02:03:56.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKSubscription.h	2016-05-27 05:15:23.000000000 +0200
@@ -11,15 +11,9 @@
 NS_ASSUME_NONNULL_BEGIN
 
 typedef NS_ENUM(NSInteger, CKSubscriptionType) {
-    CKSubscriptionTypeQuery      = 1,
-    CKSubscriptionTypeRecordZone = 2,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
-
-typedef NS_OPTIONS(NSUInteger, CKSubscriptionOptions) {
-    CKSubscriptionOptionsFiresOnRecordCreation     = 1 << 0, // Applies to CKSubscriptionTypeQuery
-    CKSubscriptionOptionsFiresOnRecordUpdate       = 1 << 1, // Applies to CKSubscriptionTypeQuery
-    CKSubscriptionOptionsFiresOnRecordDeletion     = 1 << 2, // Applies to CKSubscriptionTypeQuery
-    CKSubscriptionOptionsFiresOnce                 = 1 << 3, // Applies to CKSubscriptionTypeQuery
+    CKSubscriptionTypeQuery                                     = 1,
+    CKSubscriptionTypeRecordZone                                = 2,
+    CKSubscriptionTypeDatabase NS_ENUM_AVAILABLE(10_12, 10_0)   = 3,
 } NS_ENUM_AVAILABLE(10_10, 8_0);
 
 @class CKNotificationInfo, CKRecordZoneID;
@@ -28,39 +22,81 @@
 @interface CKSubscription : NSObject <NSSecureCoding, NSCopying>
 
 - (instancetype)init NS_UNAVAILABLE;
-- (instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
 
-- (instancetype)initWithRecordType:(NSString *)recordType predicate:(NSPredicate *)predicate options:(CKSubscriptionOptions)subscriptionOptions;
+@property (nonatomic, readonly, copy) NSString *subscriptionID;
+@property (nonatomic, readonly, assign) CKSubscriptionType subscriptionType;
 
-- (instancetype)initWithRecordType:(NSString *)recordType predicate:(NSPredicate *)predicate subscriptionID:(NSString *)subscriptionID options:(CKSubscriptionOptions)subscriptionOptions NS_DESIGNATED_INITIALIZER;
+/* Optional property describing the notification that will be sent when the subscription fires. */
+@property (nonatomic, copy, nullable) CKNotificationInfo *notificationInfo;
 
-/* This subscription fires whenever any change happens in the indicated RecordZone.
- The RecordZone must have the capability CKRecordZoneCapabilityFetchChanges */
-- (instancetype)initWithZoneID:(CKRecordZoneID *)zoneID options:(CKSubscriptionOptions)subscriptionOptions;
-- (instancetype)initWithZoneID:(CKRecordZoneID *)zoneID subscriptionID:(NSString *)subscriptionID options:(CKSubscriptionOptions)subscriptionOptions NS_DESIGNATED_INITIALIZER;
+@end
 
-@property (nonatomic, readonly, copy) NSString *subscriptionID;
 
-@property (nonatomic, readonly, assign) CKSubscriptionType subscriptionType;
+typedef NS_OPTIONS(NSUInteger, CKQuerySubscriptionOptions) {
+    CKQuerySubscriptionOptionsFiresOnRecordCreation     = 1 << 0,
+    CKQuerySubscriptionOptionsFiresOnRecordUpdate       = 1 << 1,
+    CKQuerySubscriptionOptionsFiresOnRecordDeletion     = 1 << 2,
+    CKQuerySubscriptionOptionsFiresOnce                 = 1 << 3,
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
+/* A subscription that fires whenever a change matching the predicate occurs.
+ CKQuerySubscriptions are not supported in a sharedCloudDatabase */
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CKQuerySubscription : CKSubscription <NSSecureCoding, NSCopying>
+
+- (instancetype)initWithRecordType:(NSString *)recordType predicate:(NSPredicate *)predicate options:(CKQuerySubscriptionOptions)querySubscriptionOptions;
+- (instancetype)initWithRecordType:(NSString *)recordType predicate:(NSPredicate *)predicate subscriptionID:(NSString *)subscriptionID options:(CKQuerySubscriptionOptions)querySubscriptionOptions NS_DESIGNATED_INITIALIZER;
 
-/* The record type that this subscription watches. This property is only used by query subscriptions, and must be set. */
-@property (nonatomic, readonly, copy, nullable) NSString *recordType;
+/* The record type that this subscription watches */
+@property (nonatomic, readonly, copy) NSString *recordType;
 
-/* A predicate that determines when the subscription fires. This property is only used by query subscriptions, and must be set */
-@property (nonatomic, readonly, copy, nullable) NSPredicate *predicate;
+/* A predicate that determines when the subscription fires. */
+@property (nonatomic, readonly, copy) NSPredicate *predicate;
 
-/* Options flags describing the firing behavior subscription. For query subscriptions, one of CKSubscriptionOptionsFiresOnRecordCreation, CKSubscriptionOptionsFiresOnRecordUpdate, or CKSubscriptionOptionsFiresOnRecordDeletion must be specified or an NSInvalidArgumentException will be thrown. */
-@property (nonatomic, readonly, assign) CKSubscriptionOptions subscriptionOptions;
+/* Optional property.  If set, a query subscription is scoped to only record changes in the indicated zone. */
+@property (nonatomic, copy, nullable) CKRecordZoneID *zoneID;
 
-/* Optional property describing the notification that will be sent when the subscription fires. */
-@property (nonatomic, copy, nullable) CKNotificationInfo *notificationInfo;
+/* Options flags describing the firing behavior subscription. One of
+ CKQuerySubscriptionOptionsFiresOnRecordCreation,
+ CKQuerySubscriptionOptionsFiresOnRecordUpdate, or
+ CKQuerySubscriptionOptionsFiresOnRecordDeletion must be specified or an
+ NSInvalidArgumentException will be thrown. */
+@property (nonatomic, readonly, assign) CKQuerySubscriptionOptions querySubscriptionOptions;
 
-/* Query subscriptions: Optional property.  If set, a query subscription is scoped to only record changes in the indicated zone.
-   RecordZone subscriptions: */
-@property (nonatomic, copy, nullable) CKRecordZoneID *zoneID;
+@end
+
+
+/* A subscription that fires whenever any change happens in the indicated Record Zone.
+ The RecordZone must have the capability CKRecordZoneCapabilityFetchChanges
+ CKRecordZoneSubscriptions are not supported in a sharedCloudDatabase */
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CKRecordZoneSubscription : CKSubscription <NSSecureCoding, NSCopying>
+
+- (instancetype)initWithZoneID:(CKRecordZoneID *)zoneID;
+- (instancetype)initWithZoneID:(CKRecordZoneID *)zoneID subscriptionID:(NSString *)subscriptionID NS_DESIGNATED_INITIALIZER;
+
+@property (nonatomic, readonly, copy) CKRecordZoneID *zoneID;
+
+/* Optional property. If set, a zone subscription is scoped to record changes for this record type */
+@property (nonatomic, copy, nullable) NSString *recordType;
+
+@end
+
+
+/* This subscription fires whenever any change happens in the database that this subscription was saved in.
+   CKDatabaseSubscription is only supported in the Private and Shared databases. */
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CKDatabaseSubscription : CKSubscription <NSSecureCoding, NSCopying>
+
+- (instancetype)init;
+- (instancetype)initWithSubscriptionID:(NSString *)subscriptionID NS_DESIGNATED_INITIALIZER;
+
+/* Optional property. If set, a database subscription is scoped to record changes for this record type */
+@property (nonatomic, copy, nullable) NSString *recordType;
 
 @end
 
+
 /* The payload of a push notification delivered in the UIApplication application:didReceiveRemoteNotification: delegate method contains information about the firing subscription.   Use
    +[CKNotification notificationFromRemoteNotificationDictionary:] to parse that payload.
  
@@ -77,7 +113,7 @@
 @property (nonatomic, copy, nullable) NSString *alertLocalizationKey __TVOS_PROHIBITED;
 
 /* A list of field names to take from the matching record that is used as substitution variables in a formatted alert string. */
-@property (nonatomic, copy, nullable) NSArray <NSString *> *alertLocalizationArgs __TVOS_PROHIBITED;
+@property (nonatomic, copy, nullable) NSArray<NSString *> *alertLocalizationArgs __TVOS_PROHIBITED;
 
 /* A key for a localized string to be used as the alert action in a modal style notification. */
 @property (nonatomic, copy, nullable) NSString *alertActionLocalizationKey __TVOS_PROHIBITED;
@@ -95,17 +131,49 @@
      NSDate
      NSNumber
      NSString */
-@property (nonatomic, copy, nullable) NSArray <NSString *> *desiredKeys;
+@property (nonatomic, copy, nullable) NSArray<NSString *> *desiredKeys;
 
 /* Indicates that the notification should increment the app's badge count. Default value is NO. */
-@property (nonatomic, assign) BOOL shouldBadge __TVOS_PROHIBITED;
+@property (nonatomic, assign) BOOL shouldBadge __TVOS_AVAILABLE(10_0);
 
 /* Indicates that the notification should be sent with the "content-available" flag to allow for background downloads in the application. 
    Default value is NO. */
-@property (nonatomic, assign) BOOL shouldSendContentAvailable __TVOS_PROHIBITED;
+@property (nonatomic, assign) BOOL shouldSendContentAvailable;
 
 /* Optional property for the category to be sent with the push when this subscription fires. Categories allow you to present custom actions to the user on your push notifications. See UIMutableUserNotificationCategory for more information. */
 @property (nonatomic, copy, nullable) NSString *category NS_AVAILABLE(10_11, 9_0) __TVOS_PROHIBITED;
 
 @end
+
+#pragma mark - Deprecated CKSubscription
+
+/* Replaced with CKQuerySubscriptionOptions */
+typedef NS_OPTIONS(NSUInteger, CKSubscriptionOptions) {
+    CKSubscriptionOptionsFiresOnRecordCreation     = 1 << 0,
+    CKSubscriptionOptionsFiresOnRecordUpdate       = 1 << 1,
+    CKSubscriptionOptionsFiresOnRecordDeletion     = 1 << 2,
+    CKSubscriptionOptionsFiresOnce                 = 1 << 3,
+} NS_ENUM_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use CKQuerySubscriptionOptions instead");
+
+@interface CKSubscription (CKSubscriptionDeprecated)
+
+- (instancetype)initWithCoder:(NSCoder *)aDecoder NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Init the appropriate CKSubscription subclass");
+
+/* Replaced with CKQuerySubscription */
+- (instancetype)initWithRecordType:(NSString *)recordType predicate:(NSPredicate *)predicate options:(CKSubscriptionOptions)subscriptionOptions NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use CKQuerySubscription instead");
+- (instancetype)initWithRecordType:(NSString *)recordType predicate:(NSPredicate *)predicate subscriptionID:(NSString *)subscriptionID options:(CKSubscriptionOptions)subscriptionOptions NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use CKQuerySubscription instead");
+@property (nonatomic, readonly, copy, nullable) NSString *recordType NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use CKQuerySubscription instead");
+@property (nonatomic, readonly, copy, nullable) NSPredicate *predicate NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use CKQuerySubscription instead");
+
+/* Replaced with CKQuerySubscriptionOptions */
+@property (nonatomic, readonly, assign) CKSubscriptionOptions subscriptionOptions NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use CKQuerySubscriptionOptions instead");
+
+/* Replaced with CKRecordZoneSubscription */
+- (instancetype)initWithZoneID:(CKRecordZoneID *)zoneID options:(CKSubscriptionOptions)subscriptionOptions NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use CKRecordZoneSubscription instead");
+- (instancetype)initWithZoneID:(CKRecordZoneID *)zoneID subscriptionID:(NSString *)subscriptionID options:(CKSubscriptionOptions)subscriptionOptions NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use CKRecordZoneSubscription instead");
+@property (nonatomic, copy, nullable) CKRecordZoneID *zoneID NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use CKRecordZoneSubscription instead");
+
+@end
+
+
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKUserIdentity.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKUserIdentity.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKUserIdentity.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKUserIdentity.h	2016-05-27 06:59:12.000000000 +0200
@@ -0,0 +1,28 @@
+//
+//  CKUserIdentity.h
+//  CloudKit
+//
+//  Copyright (c) 2014 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+@class CKRecordID, CKUserIdentityLookupInfo;
+
+NS_ASSUME_NONNULL_BEGIN
+
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CKUserIdentity : NSObject <NSSecureCoding, NSCopying>
+// Use CKDiscoverUserIdentitiesOperation or CKFetchShareParticipantsOperation to create a CKUserIdentity
+- (instancetype)init NS_UNAVAILABLE;
+
+// This is the lookupInfo you passed in to CKDiscoverUserIdentitiesOperation or CKFetchShareParticipantsOperation
+@property (nonatomic, readonly, copy, nullable) CKUserIdentityLookupInfo *lookupInfo;
+@property (nonatomic, readonly, copy, nullable) NSPersonNameComponents *nameComponents;
+@property (nonatomic, readonly, copy, nullable) CKRecordID *userRecordID;
+
+@property (nonatomic, readonly, assign) BOOL hasiCloudAccount;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKUserIdentityLookupInfo.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKUserIdentityLookupInfo.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKUserIdentityLookupInfo.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKUserIdentityLookupInfo.h	2016-05-27 06:59:12.000000000 +0200
@@ -0,0 +1,30 @@
+//
+//  CKUserIdentityLookupInfo.h
+//  CloudKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+
+@class CKRecordID;
+
+NS_ASSUME_NONNULL_BEGIN
+NS_CLASS_AVAILABLE(10_12, 10_0)
+@interface CKUserIdentityLookupInfo : NSObject <NSSecureCoding, NSCopying>
+- (instancetype)init NS_UNAVAILABLE;
+
+- (instancetype)initWithEmailAddress:(NSString *)emailAddress;
+- (instancetype)initWithPhoneNumber:(NSString *)phoneNumber;
+- (instancetype)initWithUserRecordID:(CKRecordID *)userRecordID;
+
++ (NSArray<CKUserIdentityLookupInfo *> *)lookupInfosWithEmails:(NSArray<NSString *> *)emails;
++ (NSArray<CKUserIdentityLookupInfo *> *)lookupInfosWithPhoneNumbers:(NSArray<NSString *> *)phoneNumbers;
++ (NSArray<CKUserIdentityLookupInfo *> *)lookupInfosWithRecordIDs:(NSArray<CKRecordID *> *)recordIDs;
+
+@property (nonatomic, readonly, copy, nullable) NSString *emailAddress;
+@property (nonatomic, readonly, copy, nullable) NSString *phoneNumber;
+@property (nonatomic, readonly, copy, nullable) CKRecordID *userRecordID;
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CloudKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CloudKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CloudKit.h	2016-02-25 00:22:27.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CloudKit.h	2016-05-27 06:59:12.000000000 +0200
@@ -21,16 +21,21 @@
 #import <CloudKit/CKRecordID.h>
 #import <CloudKit/CKRecordZoneID.h>
 #import <CloudKit/CKReference.h>
+#import <CloudKit/CKServerChangeToken.h>
+#import <CloudKit/CKShare.h>
+#import <CloudKit/CKShareMetadata.h>
+#import <CloudKit/CKShareParticipant.h>
 #import <CloudKit/CKSubscription.h>
 #import <CloudKit/CKDiscoveredUserInfo.h>
+#import <CloudKit/CKUserIdentity.h>
+#import <CloudKit/CKUserIdentityLookupInfo.h>
 
 #import <CloudKit/CKOperation.h>
 #import <CloudKit/CKDatabaseOperation.h>
 #import <CloudKit/CKModifyRecordsOperation.h>
-#import <CloudKit/CKDiscoverAllContactsOperation.h>
-#import <CloudKit/CKDiscoverUserInfosOperation.h>
 #import <CloudKit/CKFetchRecordsOperation.h>
 #import <CloudKit/CKFetchRecordChangesOperation.h>
+#import <CloudKit/CKFetchRecordZoneChangesOperation.h>
 #import <CloudKit/CKQueryOperation.h>
 #import <CloudKit/CKModifyBadgeOperation.h>
 #import <CloudKit/CKFetchNotificationChangesOperation.h>
@@ -40,3 +45,11 @@
 #import <CloudKit/CKModifyRecordZonesOperation.h>
 #import <CloudKit/CKFetchRecordZonesOperation.h>
 #import <CloudKit/CKFetchWebAuthTokenOperation.h>
+#import <CloudKit/CKDiscoverUserInfosOperation.h>
+#import <CloudKit/CKDiscoverAllContactsOperation.h>
+#import <CloudKit/CKDiscoverUserIdentitiesOperation.h>
+#import <CloudKit/CKDiscoverAllUserIdentitiesOperation.h>
+#import <CloudKit/CKFetchShareParticipantsOperation.h>
+#import <CloudKit/CKAcceptSharesOperation.h>
+#import <CloudKit/CKFetchShareMetadataOperation.h>
+#import <CloudKit/CKFetchDatabaseChangesOperation.h>

```