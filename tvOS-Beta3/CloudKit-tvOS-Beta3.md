#CloudKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h	2016-06-27 07:34:22.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKDatabase.h	2016-07-11 07:24:12.000000000 +0200
@@ -51,7 +51,7 @@
 #pragma mark Record Zone Convenience Methods
 /* CKFetchRecordZonesOperation and CKModifyRecordZonesOperation are the more configurable,
  CKOperation-based alternatives to these methods */
-- (void)fetchAllRecordZonesWithCompletionHandler:(void (^)(NSArray<CKRecordZone *> * _Nullable zones, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(fetchAll(completionHandler:));
+- (void)fetchAllRecordZonesWithCompletionHandler:(void (^)(NSArray<CKRecordZone *> * _Nullable zones, NSError * _Nullable error))completionHandler;
 - (void)fetchRecordZoneWithID:(CKRecordZoneID *)zoneID completionHandler:(void (^)(CKRecordZone * _Nullable zone, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(fetch(withRecordZoneID:completionHandler:));
 - (void)saveRecordZone:(CKRecordZone *)zone completionHandler:(void (^)(CKRecordZone * _Nullable zone, NSError * _Nullable error))completionHandler;
 - (void)deleteRecordZoneWithID:(CKRecordZoneID *)zoneID completionHandler:(void (^)(CKRecordZoneID * _Nullable zoneID, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(delete(withRecordZoneID:completionHandler:));
@@ -60,7 +60,7 @@
 /* CKFetchSubscriptionsOperation and CKModifySubscriptionsOperation are the more configurable,
  CKOperation-based alternative to these methods */
 - (void)fetchSubscriptionWithID:(NSString *)subscriptionID completionHandler:(void (^)(CKSubscription * _Nullable subscription, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(fetch(withSubscriptionID:completionHandler:)) __WATCHOS_PROHIBITED;
-- (void)fetchAllSubscriptionsWithCompletionHandler:(void (^)(NSArray<CKSubscription *> * _Nullable subscriptions, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(fetchAll(completionHandler:)) __WATCHOS_PROHIBITED;
+- (void)fetchAllSubscriptionsWithCompletionHandler:(void (^)(NSArray<CKSubscription *> * _Nullable subscriptions, NSError * _Nullable error))completionHandler __WATCHOS_PROHIBITED;
 - (void)saveSubscription:(CKSubscription *)subscription completionHandler:(void (^)(CKSubscription * _Nullable subscription, NSError * _Nullable error))completionHandler __WATCHOS_PROHIBITED;
 - (void)deleteSubscriptionWithID:(NSString *)subscriptionID completionHandler:(void (^)(NSString * _Nullable subscriptionID, NSError * _Nullable error))completionHandler NS_SWIFT_NAME(delete(withSubscriptionID:completionHandler:)) __WATCHOS_PROHIBITED;
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShare.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShare.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShare.h	2016-06-27 06:24:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CloudKit.framework/Headers/CKShare.h	2016-07-11 07:27:39.000000000 +0200
@@ -19,7 +19,7 @@
 CK_EXTERN NSString * const CKShareTitleKey NS_AVAILABLE(10_12, 10_0);
 /* Value is a data blob suitable to pass into -[NSImage imageWithData:] or -[UIImage imageWithData:] */
 CK_EXTERN NSString * const CKShareThumbnailImageDataKey NS_AVAILABLE(10_12, 10_0);
-/* Value is a string.  Example for a recipe sharing app: "Recipe" */
+/* Value is a string representing a UTI.  Example for a recipe sharing app: "com.mycompany.recipe" */
 CK_EXTERN NSString * const CKShareTypeKey NS_AVAILABLE(10_12, 10_0);
 
 /*
@@ -47,7 +47,8 @@
  Shares with publicPermission more permissive than CKShareParticipantPermissionNone can be joined by any user with access to the share's shareURL.
  This property defines what permission those users will have.
  By default, public permission is CKShareParticipantPermissionNone.
- Changing the public permission to CKShareParticipantPermissionNone will result in all public participants being removed when the share is saved. */
+ Changing the public permission to CKShareParticipantPermissionReadOnly or CKShareParticipantPermissionReadWrite will result in all pending participants being removed.  Already-accepted participants will remain on the share.
+ Changing the public permission to CKShareParticipantPermissionNone will result in all participants being removed from the share.  You may subsequently choose to call addParticipant: before saving the share, those participants will be added to the share. */
 @property (nonatomic, assign) CKShareParticipantPermission publicPermission;
 
 /* A URL that can be used to invite participants to this share. Only available after share record has been saved to the server.  This url is stable, and is tied to the rootRecord.  That is, if you share a rootRecord, delete the share, and re-share the same rootRecord via a newly created share, that newly created share's url will be identical to the prior share's url */

```