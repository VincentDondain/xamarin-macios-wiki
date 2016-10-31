#CloudKit.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKAcceptSharesOperation.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKAcceptSharesOperation.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKAcceptSharesOperation.h	2016-09-24 03:59:51.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKAcceptSharesOperation.h	2016-10-23 09:27:49.000000000 +0200
@@ -17,7 +17,7 @@
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
 - (instancetype)initWithShareMetadatas:(NSArray<CKShareMetadata *> *)shareMetadatas;
 
-@property (nonatomic, copy) NSArray<CKShareMetadata *> *shareMetadatas;
+@property (nonatomic, copy, nullable) NSArray<CKShareMetadata *> *shareMetadatas;
 
 /* Called once for each share metadata that the server processed. If error is nil then the share was successfully accepted. */
 @property (nonatomic, copy, nullable) void (^perShareCompletionBlock)(CKShareMetadata *shareMetadata, CKShare * _Nullable acceptedShare, NSError * _Nullable error);
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKContainer.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKContainer.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKContainer.h	2016-09-24 02:54:50.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKContainer.h	2016-10-23 10:16:19.000000000 +0200
@@ -59,10 +59,10 @@
  */
 @property (nonatomic, readonly) CKDatabase *privateCloudDatabase;
 @property (nonatomic, readonly) CKDatabase *publicCloudDatabase;
-@property (nonatomic, readonly) CKDatabase *sharedCloudDatabase;
+@property (nonatomic, readonly) CKDatabase *sharedCloudDatabase NS_AVAILABLE(10_12, 10_0);
 
 /* Convenience method, will return a database that's pointer-equal to one of the above properties */
-- (CKDatabase *)databaseWithDatabaseScope:(CKDatabaseScope)databaseScope;
+- (CKDatabase *)databaseWithDatabaseScope:(CKDatabaseScope)databaseScope NS_AVAILABLE(10_12, 10_0);
 
 @end
 
@@ -124,10 +124,10 @@
 /* This fetches all user records that match an entry in the user's address book.
  CKDiscoverAllContactsOperation and CKDiscoverUserIdentityOperation are the more configurable,
  CKOperation-based alternatives to these methods */
-- (void)discoverAllIdentitiesWithCompletionHandler:(void (^)(NSArray<CKUserIdentity *> * _Nullable userIdentities, NSError * _Nullable error))completionHandler __TVOS_UNAVAILABLE;
-- (void)discoverUserIdentityWithEmailAddress:(NSString *)email completionHandler:(void (^)(CKUserIdentity * _Nullable userInfo, NSError * _Nullable error))completionHandler;
-- (void)discoverUserIdentityWithPhoneNumber:(NSString *)phoneNumber completionHandler:(void (^)(CKUserIdentity * _Nullable userInfo, NSError * _Nullable error))completionHandler;
-- (void)discoverUserIdentityWithUserRecordID:(CKRecordID *)userRecordID completionHandler:(void (^)(CKUserIdentity * _Nullable userInfo, NSError * _Nullable error))completionHandler;
+- (void)discoverAllIdentitiesWithCompletionHandler:(void (^)(NSArray<CKUserIdentity *> * _Nullable userIdentities, NSError * _Nullable error))completionHandler NS_AVAILABLE(10_12, 10_0) __TVOS_UNAVAILABLE;
+- (void)discoverUserIdentityWithEmailAddress:(NSString *)email completionHandler:(void (^)(CKUserIdentity * _Nullable userInfo, NSError * _Nullable error))completionHandler NS_AVAILABLE(10_12, 10_0);
+- (void)discoverUserIdentityWithPhoneNumber:(NSString *)phoneNumber completionHandler:(void (^)(CKUserIdentity * _Nullable userInfo, NSError * _Nullable error))completionHandler NS_AVAILABLE(10_12, 10_0);
+- (void)discoverUserIdentityWithUserRecordID:(CKRecordID *)userRecordID completionHandler:(void (^)(CKUserIdentity * _Nullable userInfo, NSError * _Nullable error))completionHandler NS_AVAILABLE(10_12, 10_0);
 
 - (void)discoverAllContactUserInfosWithCompletionHandler:(void (^)(NSArray<CKDiscoveredUserInfo *> * _Nullable userInfos, NSError * _Nullable error))completionHandler __TVOS_UNAVAILABLE NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use -[CKContainer discoverAllIdentitiesWithCompletionHandler:] instead");
 - (void)discoverUserInfoWithEmailAddress:(NSString *)email completionHandler:(void (^)(CKDiscoveredUserInfo * _Nullable userInfo, NSError * _Nullable error))completionHandler NS_DEPRECATED(10_10, 10_12, 8_0, 10_0, "Use -[CKContainer discoverUserIdentityWithEmailAddress:completionHandler:] instead");
@@ -139,12 +139,12 @@
 
 /* Fetches share participants matching the provided info .
  CKFetchShareParticipantsOperation is the more configurable, CKOperation-based alternative to these methods. */
-- (void)fetchShareParticipantWithEmailAddress:(NSString *)emailAddress completionHandler:(void (^)(CKShareParticipant *shareParticipant, NSError *error))completionHandler NS_AVAILABLE(10_12, 10_0);
-- (void)fetchShareParticipantWithPhoneNumber:(NSString *)phoneNumber completionHandler:(void (^)(CKShareParticipant *shareParticipant, NSError *error))completionHandler NS_AVAILABLE(10_12, 10_0);
-- (void)fetchShareParticipantWithUserRecordID:(CKRecordID *)userRecordID completionHandler:(void (^)(CKShareParticipant *shareParticipant, NSError *error))completionHandler NS_AVAILABLE(10_12, 10_0);
+- (void)fetchShareParticipantWithEmailAddress:(NSString *)emailAddress completionHandler:(void (^)(CKShareParticipant * _Nullable shareParticipant, NSError * _Nullable error))completionHandler NS_AVAILABLE(10_12, 10_0);
+- (void)fetchShareParticipantWithPhoneNumber:(NSString *)phoneNumber completionHandler:(void (^)(CKShareParticipant * _Nullable shareParticipant, NSError *_Nullable error))completionHandler NS_AVAILABLE(10_12, 10_0);
+- (void)fetchShareParticipantWithUserRecordID:(CKRecordID *)userRecordID completionHandler:(void (^)(CKShareParticipant *_Nullable shareParticipant, NSError *_Nullable error))completionHandler NS_AVAILABLE(10_12, 10_0);
 
-- (void)fetchShareMetadataWithURL:(NSURL *)url completionHandler:(void (^)(CKShareMetadata *metadata, NSError *error))completionHandler NS_AVAILABLE(10_12, 10_0);
-- (void)acceptShareMetadata:(CKShareMetadata *)metadata completionHandler:(void (^)(CKShare *acceptedShare, NSError *error))completionHandler NS_AVAILABLE(10_12, 10_0);
+- (void)fetchShareMetadataWithURL:(NSURL *)url completionHandler:(void (^)(CKShareMetadata *_Nullable metadata, NSError * _Nullable error))completionHandler NS_AVAILABLE(10_12, 10_0);
+- (void)acceptShareMetadata:(CKShareMetadata *)metadata completionHandler:(void (^)(CKShare *_Nullable acceptedShare, NSError *_Nullable error))completionHandler NS_AVAILABLE(10_12, 10_0);
 
 @end
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h	2016-09-22 02:19:37.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h	2016-10-24 05:26:00.000000000 +0200
@@ -21,7 +21,7 @@
 @interface CKDatabase : NSObject
 - (instancetype)init NS_UNAVAILABLE;
 - (void)addOperation:(CKDatabaseOperation *)operation;
-@property (nonatomic, readonly, assign) CKDatabaseScope databaseScope;
+@property (nonatomic, readonly, assign) CKDatabaseScope databaseScope NS_AVAILABLE(10_12, 10_0);
 @end
 
 @interface CKDatabase (ConvenienceMethods)
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKError.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKError.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKError.h	2016-08-04 08:26:15.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKError.h	2016-10-23 10:16:19.000000000 +0200
@@ -59,11 +59,11 @@
     CKErrorZoneNotFound                   = 26, /* The specified zone does not exist on the server */
     CKErrorLimitExceeded                  = 27, /* The request to the server was too large. Retry this request as a smaller batch. */
     CKErrorUserDeletedZone                = 28, /* The user deleted this zone through the settings UI. Your client should either remove its local data or prompt the user before attempting to re-upload any data to this zone. */
-    CKErrorTooManyParticipants            = 29, /* A share cannot be saved because there are too many participants attached to the share */
-    CKErrorAlreadyShared                  = 30, /* A record/share cannot be saved, doing so would cause a hierarchy of records to exist in multiple shares */
-    CKErrorReferenceViolation             = 31, /* The target of a record's parent or share reference was not found */
-    CKErrorManagedAccountRestricted       = 32, /* Request was rejected due to a managed account restriction */
-    CKErrorParticipantMayNeedVerification = 33, /* Share Metadata cannot be determined, because the user is not a member of the share.  There are invited participants on the share with email addresses or phone numbers not associated with any iCloud account. The user may be able to join the share if they can associate one of those email addresses or phone numbers with their iCloud account via the system Share Accept UI. Call UIApplication's openURL on this share URL to have the user attempt to verify their information. */
+    CKErrorTooManyParticipants            NS_AVAILABLE(10_12, 10_0) = 29, /* A share cannot be saved because there are too many participants attached to the share */
+    CKErrorAlreadyShared                  NS_AVAILABLE(10_12, 10_0) = 30, /* A record/share cannot be saved, doing so would cause a hierarchy of records to exist in multiple shares */
+    CKErrorReferenceViolation             NS_AVAILABLE(10_12, 10_0) = 31, /* The target of a record's parent or share reference was not found */
+    CKErrorManagedAccountRestricted       NS_AVAILABLE(10_12, 10_0) = 32, /* Request was rejected due to a managed account restriction */
+    CKErrorParticipantMayNeedVerification NS_AVAILABLE(10_12, 10_0) = 33, /* Share Metadata cannot be determined, because the user is not a member of the share.  There are invited participants on the share with email addresses or phone numbers not associated with any iCloud account. The user may be able to join the share if they can associate one of those email addresses or phone numbers with their iCloud account via the system Share Accept UI. Call UIApplication's openURL on this share URL to have the user attempt to verify their information. */
 } NS_ENUM_AVAILABLE(10_10, 8_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchDatabaseChangesOperation.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchDatabaseChangesOperation.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchDatabaseChangesOperation.h	2016-09-24 03:59:51.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchDatabaseChangesOperation.h	2016-10-23 09:27:49.000000000 +0200
@@ -20,6 +20,7 @@
  If this is your first fetch or if you wish to re-fetch all zones, pass nil for the change token.
  Change token are opaque tokens and clients should not infer any behavior based on their content.
  CKFetchDatabaseChangesOperations are supported in a privateCloudDatabase and sharedCloudDatabase */
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
 - (instancetype)initWithPreviousServerChangeToken:(nullable CKServerChangeToken *)previousServerChangeToken;
 
 @property (nonatomic, copy, nullable) CKServerChangeToken *previousServerChangeToken;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchNotificationChangesOperation.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchNotificationChangesOperation.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchNotificationChangesOperation.h	2016-09-24 03:59:51.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchNotificationChangesOperation.h	2016-10-23 09:27:49.000000000 +0200
@@ -18,6 +18,7 @@
     since that anchor will be fetched.
    If this is your first fetch, pass nil for the change anchor.
    Change anchors are opaque tokens and clients should not infer any behavior based on their content. */
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
 - (instancetype)initWithPreviousServerChangeToken:(nullable CKServerChangeToken *)previousServerChangeToken;
 
 @property (nonatomic, copy, nullable) CKServerChangeToken *previousServerChangeToken;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordChangesOperation.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordChangesOperation.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordChangesOperation.h	2016-09-24 03:59:51.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordChangesOperation.h	2016-10-23 09:27:49.000000000 +0200
@@ -25,9 +25,10 @@
    If this is your first fetch or if you wish to re-fetch all records, pass nil for the change anchor.
 
    Change anchors are opaque tokens and clients should not infer any behavior based on their content. */
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
 - (instancetype)initWithRecordZoneID:(CKRecordZoneID *)recordZoneID previousServerChangeToken:(nullable CKServerChangeToken *)previousServerChangeToken;
 
-@property (nonatomic, copy) CKRecordZoneID *recordZoneID;
+@property (nonatomic, copy, nullable) CKRecordZoneID *recordZoneID;
 @property (nonatomic, copy, nullable) CKServerChangeToken *previousServerChangeToken;
 
 @property (nonatomic, assign) NSUInteger resultsLimit;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZoneChangesOperation.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZoneChangesOperation.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZoneChangesOperation.h	2016-09-23 00:51:37.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchRecordZoneChangesOperation.h	2016-10-23 09:18:47.000000000 +0200
@@ -23,9 +23,10 @@
  include a previousServerChangeToken.
 
  Change tokens are opaque tokens and clients should not infer any behavior based on their content. */
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
 - (instancetype)initWithRecordZoneIDs:(NSArray<CKRecordZoneID *> *)recordZoneIDs optionsByRecordZoneID:(nullable NSDictionary<CKRecordZoneID *, CKFetchRecordZoneChangesOptions *> *)optionsByRecordZoneID;
 
-@property (nonatomic, copy) NSArray<CKRecordZoneID *> *recordZoneIDs;
+@property (nonatomic, copy, nullable) NSArray<CKRecordZoneID *> *recordZoneIDs;
 @property (nonatomic, copy, nullable) NSDictionary<CKRecordZoneID *, CKFetchRecordZoneChangesOptions *> *optionsByRecordZoneID;
 
 /* When set to YES, this operation will send repeated requests to the server until all record changes have been fetched.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareMetadataOperation.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareMetadataOperation.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareMetadataOperation.h	2016-09-24 03:59:51.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareMetadataOperation.h	2016-10-23 09:27:49.000000000 +0200
@@ -15,9 +15,10 @@
 NS_CLASS_AVAILABLE(10_12, 10_0)
 @interface CKFetchShareMetadataOperation : CKOperation
 
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
 - (instancetype)initWithShareURLs:(NSArray<NSURL *> *)shareURLs;
 
-@property (nonatomic, copy) NSArray<NSURL *> *shareURLs;
+@property (nonatomic, copy, nullable) NSArray<NSURL *> *shareURLs;
 
 /* If set to YES, the resulting CKShareMetadata will have a rootRecord object filled out.  Defaults to NO.
  The resulting CKShareMetadata will have a rootRecordID property regardless of the value of this property. */
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareParticipantsOperation.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareParticipantsOperation.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareParticipantsOperation.h	2016-09-24 03:59:51.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchShareParticipantsOperation.h	2016-10-23 09:27:49.000000000 +0200
@@ -14,10 +14,9 @@
 @interface CKFetchShareParticipantsOperation : CKOperation
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
-
 - (instancetype)initWithUserIdentityLookupInfos:(NSArray<CKUserIdentityLookupInfo *> *)userIdentityLookupInfos;
 
-@property (nonatomic, copy) NSArray<CKUserIdentityLookupInfo *> *userIdentityLookupInfos;
+@property (nonatomic, copy, nullable) NSArray<CKUserIdentityLookupInfo *> *userIdentityLookupInfos;
 
 @property (nonatomic, copy, nullable) void (^shareParticipantFetchedBlock)(CKShareParticipant *participant);
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchSubscriptionsOperation.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchSubscriptionsOperation.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchSubscriptionsOperation.h	2016-09-24 03:59:51.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchSubscriptionsOperation.h	2016-10-23 09:27:49.000000000 +0200
@@ -14,10 +14,9 @@
 NS_CLASS_AVAILABLE(10_10, 8_0) __WATCHOS_PROHIBITED
 @interface CKFetchSubscriptionsOperation : CKDatabaseOperation
 
-- (instancetype)init NS_DESIGNATED_INITIALIZER;
-
 + (instancetype)fetchAllSubscriptionsOperation;
 
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
 - (instancetype)initWithSubscriptionIDs:(NSArray<NSString *> *)subscriptionIDs;
 
 @property (nonatomic, copy, nullable) NSArray<NSString *> *subscriptionIDs;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchWebAuthTokenOperation.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchWebAuthTokenOperation.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchWebAuthTokenOperation.h	2016-09-24 03:59:51.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKFetchWebAuthTokenOperation.h	2016-10-23 09:27:49.000000000 +0200
@@ -14,12 +14,13 @@
 /* This operation will fetch a web auth token given an API token obtained
  * from the CloudKit Dashboard for your container
  */
-- (instancetype)initWithAPIToken:(NSString *)APIToken NS_DESIGNATED_INITIALIZER;
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithAPIToken:(NSString *)APIToken;
 
 /* APIToken is expected to be set before you begin this operation. */
 @property (nonatomic, copy, nullable) NSString *APIToken;
 
-@property (nonatomic, copy, nullable) void (^fetchWebAuthTokenCompletionBlock)(NSString *webAuthToken, NSError *operationError);
+@property (nonatomic, copy, nullable) void (^fetchWebAuthTokenCompletionBlock)(NSString * _Nullable webAuthToken, NSError * _Nullable operationError);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKMarkNotificationsReadOperation.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKMarkNotificationsReadOperation.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKMarkNotificationsReadOperation.h	2016-09-24 03:59:51.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKMarkNotificationsReadOperation.h	2016-10-23 09:27:49.000000000 +0200
@@ -15,10 +15,9 @@
 @interface CKMarkNotificationsReadOperation : CKOperation
 
 - (instancetype)init NS_DESIGNATED_INITIALIZER;
-
 - (instancetype)initWithNotificationIDsToMarkRead:(NSArray<CKNotificationID *> *)notificationIDs;
 
-@property (nonatomic, copy) NSArray<CKNotificationID *> *notificationIDs;
+@property (nonatomic, copy, nullable) NSArray<CKNotificationID *> *notificationIDs;
 
 @property (nonatomic, copy, nullable) void (^markNotificationsReadCompletionBlock)(NSArray<CKNotificationID *> * _Nullable notificationIDsMarkedRead, NSError * _Nullable operationError);
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyRecordsOperation.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyRecordsOperation.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyRecordsOperation.h	2016-09-24 03:59:51.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifyRecordsOperation.h	2016-10-23 09:27:49.000000000 +0200
@@ -50,7 +50,7 @@
 */
 @property (nonatomic, copy, nullable) void (^perRecordProgressBlock)(CKRecord *record, double progress);
 /* Called on success or failure for each record. */
-@property (nonatomic, copy, nullable) void (^perRecordCompletionBlock)(CKRecord * _Nullable record, NSError * _Nullable error);
+@property (nonatomic, copy, nullable) void (^perRecordCompletionBlock)(CKRecord *record, NSError * _Nullable error);
 
 /*  This block is called when the operation completes.
  The [NSOperation completionBlock] will also be called if both are set.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifySubscriptionsOperation.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifySubscriptionsOperation.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifySubscriptionsOperation.h	2016-09-24 03:59:51.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKModifySubscriptionsOperation.h	2016-10-23 09:27:49.000000000 +0200
@@ -13,7 +13,8 @@
 NS_CLASS_AVAILABLE(10_10, 8_0) __WATCHOS_PROHIBITED
 @interface CKModifySubscriptionsOperation : CKDatabaseOperation
 
-- (instancetype)initWithSubscriptionsToSave:(nullable NSArray<CKSubscription *> *)subscriptionsToSave subscriptionIDsToDelete:(nullable NSArray<NSString *> *)subscriptionIDsToDelete NS_DESIGNATED_INITIALIZER;
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
+- (instancetype)initWithSubscriptionsToSave:(nullable NSArray<CKSubscription *> *)subscriptionsToSave subscriptionIDsToDelete:(nullable NSArray<NSString *> *)subscriptionIDsToDelete;
 
 @property (nonatomic, copy, nullable) NSArray<CKSubscription *> *subscriptionsToSave;
 @property (nonatomic, copy, nullable) NSArray<NSString *> *subscriptionIDsToDelete;
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKNotification.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKNotification.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKNotification.h	2016-09-23 00:51:46.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKNotification.h	2016-10-23 10:24:57.000000000 +0200
@@ -21,7 +21,7 @@
     CKNotificationTypeQuery            = 1, /* Generated by CKQuerySubscriptions */
     CKNotificationTypeRecordZone       = 2, /* Generated by CKRecordZoneSubscriptions */
     CKNotificationTypeReadNotification = 3, /* Indicates a notification that a client had previously marked as read. */
-    CKNotificationTypeDatabase         = 4, /* Generated by CKDatabaseSubscriptions */
+    CKNotificationTypeDatabase         NS_AVAILABLE(10_12, 10_0) = 4, /* Generated by CKDatabaseSubscriptions */
 } NS_ENUM_AVAILABLE(10_10, 8_0);
 
 NS_CLASS_AVAILABLE(10_10, 8_0)
@@ -29,7 +29,7 @@
 
 - (instancetype)init NS_UNAVAILABLE;
 
-+ (instancetype)notificationFromRemoteNotificationDictionary:(NSDictionary<NSString *, NSObject *> *)notificationDictionary;
++ (instancetype)notificationFromRemoteNotificationDictionary:(NSDictionary *)notificationDictionary;
 
 /* When you instantiate a CKNotification from a remote notification dictionary, you will get back a concrete
  subclass defined below.  Use the type of notification to avoid -isKindOfClass: checks */
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKOperation.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKOperation.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKOperation.h	2016-09-24 03:59:51.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKOperation.h	2016-10-23 09:27:49.000000000 +0200
@@ -70,7 +70,7 @@
 /*
    This callback is called after a long lived operation has begun running and is persisted. Once this callback is called the operation will continue running even if the current process exits.
  */
-@property (nonatomic, strong) void (^longLivedOperationWasPersistedBlock)(void) NS_AVAILABLE(10_12, 9_3);
+@property (nonatomic, strong, nullable) void (^longLivedOperationWasPersistedBlock)(void) NS_AVAILABLE(10_12, 9_3);
 
 @end
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecord.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecord.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecord.h	2016-09-24 02:54:49.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecord.h	2016-10-24 05:26:00.000000000 +0200
@@ -109,7 +109,7 @@
  
  Whenever possible, it is suggested that you construct your parent hierarchies such that you will only need to share the topmost record of that hierarchy.
 */
-@property (nonatomic, readonly, copy, nullable) CKReference *share;
+@property (nonatomic, readonly, copy, nullable) CKReference *share NS_AVAILABLE(10_12, 10_0);
 
 /* Use a parent reference to teach CloudKit about the hierarchy of your records. This hierarchy of records will be shared if the share reference is set on a record.
  
@@ -120,11 +120,11 @@
  You are encouraged to set up the parent relationships as part of normal record saves, even if you're not planning on sharing records at this time.  
  This allows you to share and unshare a hierarchy of records at a later date by only modifying the "top level" record, setting or clearing its 'share' reference.
 */
-@property (nonatomic, copy, nullable) CKReference *parent;
+@property (nonatomic, copy, nullable) CKReference *parent NS_AVAILABLE(10_12, 10_0);
 
 /* Convenience wrappers around creating a CKReference to a parent record. The resulting CKReference will have action = CKReferenceActionNone */
-- (void)setParentReferenceFromRecord:(nullable CKRecord *)parentRecord;
-- (void)setParentReferenceFromRecordID:(nullable CKRecordID *)parentRecordID;
+- (void)setParentReferenceFromRecord:(nullable CKRecord *)parentRecord NS_AVAILABLE(10_12, 10_0);
+- (void)setParentReferenceFromRecordID:(nullable CKRecordID *)parentRecordID NS_AVAILABLE(10_12, 10_0);
 
 @end
 
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecordZone.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecordZone.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecordZone.h	2016-09-24 03:59:51.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKRecordZone.h	2016-10-23 09:27:49.000000000 +0200
@@ -17,7 +17,7 @@
     /* Batched changes to this zone happen atomically */
     CKRecordZoneCapabilityAtomic         = 1 << 1,
     /* Records in this zone can be shared */
-    CKRecordZoneCapabilitySharing        = 1 << 2,
+    CKRecordZoneCapabilitySharing        NS_AVAILABLE(10_12, 10_0) = 1 << 2,
 } NS_AVAILABLE(10_10, 8_0);
 
 /* The default zone has no capabilities */
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShare.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShare.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShare.h	2016-09-23 00:51:37.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShare.h	2016-10-23 10:16:19.000000000 +0200
@@ -52,7 +52,7 @@
 @property (nonatomic, assign) CKShareParticipantPermission publicPermission;
 
 /* A URL that can be used to invite participants to this share. Only available after share record has been saved to the server.  This url is stable, and is tied to the rootRecord.  That is, if you share a rootRecord, delete the share, and re-share the same rootRecord via a newly created share, that newly created share's url will be identical to the prior share's url */
-@property (nonatomic, readonly, copy) NSURL *URL;
+@property (nonatomic, readonly, copy, nullable) NSURL *URL;
 
 /* The participants array will contain all participants on the share that the current user has permissions to see. 
    At the minimum that will include the owner and the current user. */
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShareParticipant.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShareParticipant.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShareParticipant.h	2016-09-24 03:59:51.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShareParticipant.h	2016-10-23 09:27:49.000000000 +0200
@@ -35,10 +35,10 @@
     CKShareParticipantTypeOwner = 1,
     CKShareParticipantTypePrivateUser = 3,
     CKShareParticipantTypePublicUser = 4,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} NS_ENUM_AVAILABLE(10_12, 10_0);
 
 
-NS_CLASS_AVAILABLE(10_10, 8_0)
+NS_CLASS_AVAILABLE(10_12, 10_0)
 @interface CKShareParticipant : NSObject <NSSecureCoding, NSCopying>
 
 /* Use CKFetchShareParticipantsOperation to create a CKShareParticipant object */

```