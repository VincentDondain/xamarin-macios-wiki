#CoreSpotlight.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableIndex.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableIndex.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableIndex.h	2016-05-19 08:04:32.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableIndex.h	2016-06-25 01:30:49.000000000 +0200
@@ -35,6 +35,7 @@
 
 + (instancetype)defaultSearchableIndex;
 
+// Apps can set a name for the index instance. This name is used as a handle for the client state used with the batch API, allowing a single client to have multiple client states; you have to retrieve the client state for an index instance with the same name as you used when setting the client state.
 - (instancetype)initWithName:(NSString *)name;
 
 //Apps can set a default protection class for items in their entitlements.  You can alternately create an instance with a custom protection class to use on iOS.  It should be one of NSFileProtectionComplete, NSFileProtectionCompleteUnlessOpen, or NSFileProtectionCompleteUntilFirstUserAuthentication.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItem.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItem.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItem.h	2016-05-19 08:18:07.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItem.h	2016-06-25 01:30:49.000000000 +0200
@@ -11,13 +11,21 @@
 NS_ASSUME_NONNULL_BEGIN
 
 // When opening a document from Spotlight, the application's application:willContinueUserActivityWithType:
-// method will get called with CSSearchableItemActionType, followed by  application:continueUserActivity:restorationHandler: with an NSUserActivity where the userInfo dictionary has a key value pair where CSSearchableItemActivityIdentifier is the key and the value is the uniqueIdentifier used when creating the item.
+// method will get called with CSSearchableItemActionType, followed by  application:continueUserActivity:restorationHandler:
+// with an NSUserActivity where the userInfo dictionary has a key value pair where CSSearchableItemActivityIdentifier is the key
+// and the value is the uniqueIdentifier used when creating the item.
 CORESPOTLIGHT_EXPORT NSString * const CSSearchableItemActionType CS_AVAILABLE(NA, 9_0) CS_TVOS_UNAVAILABLE;
 CORESPOTLIGHT_EXPORT NSString * const CSSearchableItemActivityIdentifier CS_AVAILABLE(NA, 9_0) CS_TVOS_UNAVAILABLE;
 
-// When continuing a query from Spotlight, the application's application:willContinueUserActivityWithType:
-// method will get called with CSQueryContinuationActionType, followed by  application:continueUserActivity:restorationHandler: with an NSUserActivity where the userInfo dictionary has a key value pair with CSSearchQueryString as the key and the value is a user string the app should use when performing its query.
-// The application should declare that it supports query continuation by adding CoreSpotlightContinuation = true to its Info.plist.
+// When continuing a query from Spotlight, the application's -application:willContinueUserActivityWithType:
+// method will get called with CSQueryContinuationActionType, followed by -application:continueUserActivity:restorationHandler:
+// with an NSUserActivity where the userInfo dictionary has a key value pair with CSSearchQueryString as the key
+// and the value is the string the application should use when performing its query.
+// The application should declare that it supports the query continuation by adding the CoreSpotlightContinuation key to its Info.plist:
+//
+//    <key>CoreSpotlightContinuation</key>
+//    <true/>
+//
 CORESPOTLIGHT_EXPORT NSString * const CSQueryContinuationActionType CS_AVAILABLE(NA, 10_0) CS_TVOS_UNAVAILABLE;
 CORESPOTLIGHT_EXPORT NSString * const CSSearchQueryString CS_AVAILABLE(NA, 10_0) CS_TVOS_UNAVAILABLE;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_General.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_General.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_General.h	2016-05-19 08:18:07.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreSpotlight.framework/Headers/CSSearchableItemAttributeSet_General.h	2016-06-25 01:30:49.000000000 +0200
@@ -19,6 +19,9 @@
 @property(nullable, copy) NSString *path;
 
 //Optional file URL representing the content to be indexed
+//Applications that are also 'Documents & Data' clients can set this property to allow Spotlight to deduplicate
+//their searchable items against the iCloud Drive's items. When this property is set, Spotlight will not display
+//the iCloud Drive's searchable items that have the same contentURL property.
 @property(nullable, strong) NSURL *contentURL;
 
 //Optional file URL pointing to a thumbnail image for this item

```