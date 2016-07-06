#CoreSpotlight.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchQuery.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchQuery.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchQuery.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchQuery.h	2016-05-19 08:18:07.000000000 +0200
@@ -0,0 +1,56 @@
+//
+//  CSSearchQuery.h
+//  CoreSpotlight
+//
+//  Copyright © 2015 Apple. All rights reserved.
+//
+
+#import <CoreSpotlight/CSBase.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+CORESPOTLIGHT_EXPORT NSString * const CSSearchQueryErrorDomain CS_AVAILABLE(NA, 10_0) CS_TVOS_UNAVAILABLE;
+
+typedef NS_ENUM(NSInteger, CSSearchQueryErrorCode) {
+    CSSearchQueryErrorCodeUnknown = -2000,
+    CSSearchQueryErrorCodeIndexUnreachable = -2001,
+    CSSearchQueryErrorCodeInvalidQuery = -2002,
+    CSSearchQueryErrorCodeCancelled = -2003,
+} CS_AVAILABLE(NA, 10_0) CS_TVOS_UNAVAILABLE;
+
+@class CSSearchableItem;
+
+CS_CLASS_AVAILABLE(NA, 10_0) CS_TVOS_UNAVAILABLE
+@interface CSSearchQuery : NSObject
+
+- (instancetype)init NS_UNAVAILABLE;
+
+// queryString: The query string (e.g., 'contentType == "public.email-message" && subject != "Re:*"')
+// attributes: The attributes to be fetched for the searchable items
+- (instancetype)initWithQueryString:(NSString *)queryString attributes:(NSArray<NSString *> * _Nullable)attributes;
+
+@property (readonly, getter=isCancelled) BOOL cancelled;
+
+// The query will update the count before each foundItemsHandler invocation to reflect
+// the number of items found so far; if foundItemsHandler is nil then the count will
+// contain the total number of found items when the query completes.
+@property (readonly) NSUInteger foundItemCount;
+
+// The foundItemsHandler will be invoked repeatedly with a new batch of searchable items.
+// The query serializes all the foundItemsHandler invocations.
+@property (nullable, copy) void (^foundItemsHandler)(NSArray<CSSearchableItem *> *items);
+
+@property (nullable, copy) void (^completionHandler)(NSError * _Nullable error);
+
+// An array of NSFileProtectionComplete, NSFileProtectionCompleteUnlessOpen,
+// or NSFileProtectionCompleteUntilFirstUserAuthentication.
+// By default the data protection will be read from the "com.apple.developer.default-data-protection"
+// entitlement if any or NSFileProtectionCompleteUntilFirstUserAuthentication will be used otherwise.
+@property (copy) NSArray<NSString *> *protectionClasses;
+
+- (void)start;
+- (void)cancel;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableIndex.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableIndex.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableIndex.h	2015-09-30 22:28:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableIndex.h	2016-05-19 08:04:32.000000000 +0200
@@ -50,7 +50,9 @@
 // reindexSearchableItemsWithIdentifiers will be called if the journaling completed successfully but the data was not able to be indexed for some reason.
 - (void)deleteSearchableItemsWithIdentifiers:(NSArray<NSString *> *)identifiers completionHandler:(void (^ __nullable)(NSError * __nullable error))completionHandler;
 
-// Call this method on the index to remove any items from the index with the given domain identifiers.  The delete is recursive so if domain identifiers are of the form <account-id>.<mailbox-id>, for example, calling delete with <account-id> will items with that account and any mailbox.
+// Call this method on the index to remove any items from the index with the given domain identifiers.
+// The delete is recursive so if domain identifiers are of the form <account-id>.<mailbox-id>, for example,
+// calling delete with <account-id> will delte all the searchable items with that account and any mailbox.
 - (void)deleteSearchableItemsWithDomainIdentifiers:(NSArray<NSString *> *)domainIdentifiers completionHandler:(void (^ __nullable)(NSError * __nullable error))completionHandler;
 
 // Call this method to delete all searchable items from the index.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItem.h	2015-09-30 22:28:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItem.h	2016-05-19 08:18:07.000000000 +0200
@@ -11,10 +11,17 @@
 NS_ASSUME_NONNULL_BEGIN
 
 // When opening a document from Spotlight, the application's application:willContinueUserActivityWithType:
-// method will get called with CSSearchableItemActionType, followed by  application:continueUserActivity:restorationHandler: with an NSUserActivity where the userInfo dictionary has a single key value pair where CSSearchableItemActivityIdentifier is the key and the value is the uniqueIdentifier used when creating the item.
+// method will get called with CSSearchableItemActionType, followed by  application:continueUserActivity:restorationHandler: with an NSUserActivity where the userInfo dictionary has a key value pair where CSSearchableItemActivityIdentifier is the key and the value is the uniqueIdentifier used when creating the item.
 CORESPOTLIGHT_EXPORT NSString * const CSSearchableItemActionType CS_AVAILABLE(NA, 9_0) CS_TVOS_UNAVAILABLE;
 CORESPOTLIGHT_EXPORT NSString * const CSSearchableItemActivityIdentifier CS_AVAILABLE(NA, 9_0) CS_TVOS_UNAVAILABLE;
 
+// When continuing a query from Spotlight, the application's application:willContinueUserActivityWithType:
+// method will get called with CSQueryContinuationActionType, followed by  application:continueUserActivity:restorationHandler: with an NSUserActivity where the userInfo dictionary has a key value pair with CSSearchQueryString as the key and the value is a user string the app should use when performing its query.
+// The application should declare that it supports query continuation by adding CoreSpotlightContinuation = true to its Info.plist.
+CORESPOTLIGHT_EXPORT NSString * const CSQueryContinuationActionType CS_AVAILABLE(NA, 10_0) CS_TVOS_UNAVAILABLE;
+CORESPOTLIGHT_EXPORT NSString * const CSSearchQueryString CS_AVAILABLE(NA, 10_0) CS_TVOS_UNAVAILABLE;
+
+
 CS_CLASS_AVAILABLE(NA, 9_0)
 CS_TVOS_UNAVAILABLE
 @interface CSSearchableItem : NSObject <NSSecureCoding, NSCopying>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet.h	2015-09-30 22:28:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet.h	2016-05-19 08:18:07.000000000 +0200
@@ -39,6 +39,8 @@
 CS_TVOS_UNAVAILABLE
 @interface CSCustomAttributeKey : NSObject <NSCopying,NSSecureCoding>
 
+- (instancetype)init NS_UNAVAILABLE;
+
 //Key names should be ASCII only, with no punctuation other than '_'.
 //It is recommended keys be of the form "com_mycompany_myapp_keyname"
 //Keys starting with 'kMD' are reserved.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_General.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_General.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_General.h	2015-09-30 22:28:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_General.h	2016-05-19 08:18:07.000000000 +0200
@@ -27,9 +27,13 @@
 //Optional image data for thumbnail for this item
 @property(nullable, copy) NSData *thumbnailData;
 
-//For activities, this is the unique identifier for the item this activity is related to
+//For activities, this is the unique identifier for the item this activity is related to. If the item doesn't exist in the index, the activity will not get stored. When the item is deleted, the activity will also be deleted.
 @property(nullable, copy) NSString *relatedUniqueIdentifier;
 
+//For activities, this is the unique identifier for an item this activity is related to. Unlike relatedUniqueIdentifier, this attribute does not link the life time of the items.
+@property(nullable, copy) NSString *weakRelatedUniqueIdentifier CS_AVAILABLE(NA, 10_0) CS_TVOS_UNAVAILABLE;
+
+
 //This is the date that the last metadata attribute was changed.
 @property(nullable, strong) NSDate *metadataModificationDate;
 
@@ -46,6 +50,14 @@
 //Title of the document, or it could be the title of this mp3 or a subject of a mail message.
 @property(nullable, copy) NSString *title;
 
+//A version specifier for this item.
+@property(nullable, copy) NSString *version;
+
+// This property has the same semantics as -[CSSearchableItem domainIdentifier].
+// It can be set on the contentAttributeSet property of a NSUserActivity instance and then used to delete the user activity
+// by calling [[CSSearchableIndex defaultSearchableIndex] deleteSearchableItemsWithDomainIdentifiers:].
+@property(nullable, copy) NSString *domainIdentifier CS_AVAILABLE(NA, 10_0) CS_TVOS_UNAVAILABLE;
+
 @end
 
 @interface CSSearchableItemAttributeSet (CSActionExtras)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_Media.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_Media.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_Media.h	2015-09-30 22:28:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_Media.h	2016-05-25 05:02:32.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <CoreSpotlight/CSSearchableItemAttributeSet.h>
+#import <CoreSpotlight/CSSearchableItemAttributeSet_General.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -55,9 +56,6 @@
 //A list of contacts that are somehow associated with this document, beyond what is captured as Author.
 @property(nullable, copy) NSArray<NSString*> *contactKeywords;
 
-//A version specifier for this item.
-@property(nullable, copy) NSString *version;
-
 //The codecs used to encode/decode the media
 @property(nullable, copy) NSArray<NSString*> *codecs;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_Places.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_Places.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_Places.h	2015-09-30 22:28:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_Places.h	2016-05-19 08:18:07.000000000 +0200
@@ -15,6 +15,15 @@
 //Other editorial instructions concerning the use of the item, such as embargoes and warnings.
 @property(nullable, copy) NSString *instructions;
 
+//The location (e.g., street name) for the item according to guidelines established by the provider.
+@property(nullable, copy) NSString *thoroughfare;
+
+//The sub-location (e.g., street number) for the item according to guidelines established by the provider.
+@property(nullable, copy) NSString *subThoroughfare;
+
+//The postal code for the item according to guidelines established by the provider.
+@property(nullable, copy) NSString *postalCode;
+
 //Identifies city of item origin according to guidelines established by the provider.
 @property(nullable, copy) NSString *city;
 
@@ -25,6 +34,9 @@
 //intellectual property of the item was created,according to guidelines of the provider.
 @property(nullable, copy) NSString *country;
 
+// The fully formatted address of the item (obtained from MapKit)
+@property(nullable, copy) NSString *fullyFormattedAddress;
+
 //The altitude of the item in meters above sea level, expressed
 //using the WGS84 datum.  Negative values lie below sea level.
 @property(nullable, strong) NSNumber *altitude;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CoreSpotlight.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CoreSpotlight.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CoreSpotlight.h	2015-09-30 22:28:05.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CoreSpotlight.h	2016-05-19 08:18:07.000000000 +0200
@@ -14,7 +14,7 @@
 #import <CoreSpotlight/CSSearchableItemAttributeSet.h>
 #import <CoreSpotlight/CSSearchableItemAttributeSet_Categories.h>
 #import <CoreSpotlight/CSIndexExtensionRequestHandler.h>
-
+#import <CoreSpotlight/CSSearchQuery.h>
 
 //! Project version number for CoreSpotlight.
 CORESPOTLIGHT_EXPORT double CoreSpotlightVersionNumber;

```