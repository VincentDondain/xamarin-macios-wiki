#UIKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSTextStorage.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSTextStorage.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSTextStorage.h	2016-07-14 06:20:58.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/NSTextStorage.h	2016-07-28 05:52:57.000000000 +0200
@@ -6,6 +6,7 @@
 //
 
 #import <Foundation/NSObject.h>
+#import <Foundation/NSNotification.h>
 #import <UIKit/NSAttributedString.h>
 
 @class NSArray, NSLayoutManager, NSNotification;
@@ -101,8 +102,8 @@
 
 /**** Notifications ****/
 
-UIKIT_EXTERN NSString * const NSTextStorageWillProcessEditingNotification NS_AVAILABLE(10_0, 7_0);
-UIKIT_EXTERN NSString * const NSTextStorageDidProcessEditingNotification NS_AVAILABLE(10_0, 7_0);
+UIKIT_EXTERN NSNotificationName const NSTextStorageWillProcessEditingNotification NS_AVAILABLE(10_0, 7_0);
+UIKIT_EXTERN NSNotificationName const NSTextStorageDidProcessEditingNotification NS_AVAILABLE(10_0, 7_0);
 
 
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivity.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivity.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivity.h	2016-07-14 06:20:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivity.h	2016-07-28 05:01:12.000000000 +0200
@@ -12,21 +12,27 @@
 
 @class UIImage, UIViewController;
 
-UIKIT_EXTERN NSString *const UIActivityTypePostToFacebook     NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIActivityTypePostToTwitter      NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIActivityTypePostToWeibo        NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;    // SinaWeibo
-UIKIT_EXTERN NSString *const UIActivityTypeMessage            NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIActivityTypeMail               NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIActivityTypePrint              NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIActivityTypeCopyToPasteboard   NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIActivityTypeAssignToContact    NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIActivityTypeSaveToCameraRoll   NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIActivityTypeAddToReadingList   NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIActivityTypePostToFlickr       NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIActivityTypePostToVimeo        NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIActivityTypePostToTencentWeibo NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIActivityTypeAirDrop            NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIActivityTypeOpenInIBooks       NS_AVAILABLE_IOS(9_0) __TVOS_PROHIBITED;
+#if UIKIT_STRING_ENUMS
+typedef NSString * UIActivityType NS_EXTENSIBLE_STRING_ENUM;
+#else
+typedef NSString * UIActivityType;
+#endif
+
+UIKIT_EXTERN UIActivityType const UIActivityTypePostToFacebook     NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN UIActivityType const UIActivityTypePostToTwitter      NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN UIActivityType const UIActivityTypePostToWeibo        NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;    // SinaWeibo
+UIKIT_EXTERN UIActivityType const UIActivityTypeMessage            NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN UIActivityType const UIActivityTypeMail               NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN UIActivityType const UIActivityTypePrint              NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN UIActivityType const UIActivityTypeCopyToPasteboard   NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN UIActivityType const UIActivityTypeAssignToContact    NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN UIActivityType const UIActivityTypeSaveToCameraRoll   NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN UIActivityType const UIActivityTypeAddToReadingList   NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN UIActivityType const UIActivityTypePostToFlickr       NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN UIActivityType const UIActivityTypePostToVimeo        NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN UIActivityType const UIActivityTypePostToTencentWeibo NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN UIActivityType const UIActivityTypeAirDrop            NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN UIActivityType const UIActivityTypeOpenInIBooks       NS_AVAILABLE_IOS(9_0) __TVOS_PROHIBITED;
 
 typedef NS_ENUM(NSInteger, UIActivityCategory) {
     UIActivityCategoryAction,
@@ -43,11 +49,11 @@
 #endif
 
 #if UIKIT_DEFINE_AS_PROPERTIES
-@property(nonatomic, readonly, nullable) NSString *activityType;       // default returns nil. subclass may override to return custom activity type that is reported to completion handler
+@property(nonatomic, readonly, nullable) UIActivityType activityType;       // default returns nil. subclass may override to return custom activity type that is reported to completion handler
 @property(nonatomic, readonly, nullable) NSString *activityTitle;      // default returns nil. subclass must override and must return non-nil value
 @property(nonatomic, readonly, nullable) UIImage *activityImage;       // default returns nil. subclass must override and must return non-nil value
 #else
-- (nullable NSString *)activityType;       // default returns nil. subclass may override to return custom activity type that is reported to completion handler
+- (nullable UIActivityType)activityType;       // default returns nil. subclass may override to return custom activity type that is reported to completion handler
 - (nullable NSString *)activityTitle;      // default returns nil. subclass must override and must return non-nil value
 - (nullable UIImage *)activityImage;       // default returns nil. subclass must override and must return non-nil value
 #endif
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityItemProvider.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityItemProvider.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityItemProvider.h	2016-07-14 06:20:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityItemProvider.h	2016-07-28 05:53:09.000000000 +0200
@@ -7,6 +7,7 @@
 #import <Foundation/Foundation.h>
 #import <CoreGraphics/CoreGraphics.h>
 #import <UIKit/UIKitDefines.h>
+#import <UIKit/UIActivity.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -17,13 +18,13 @@
 @required
 
 - (id)activityViewControllerPlaceholderItem:(UIActivityViewController *)activityViewController;	// called to determine data type. only the class of the return type is consulted. it should match what -itemForActivityType: returns later
-- (nullable id)activityViewController:(UIActivityViewController *)activityViewController itemForActivityType:(NSString *)activityType;	// called to fetch data after an activity is selected. you can return nil.
+- (nullable id)activityViewController:(UIActivityViewController *)activityViewController itemForActivityType:(UIActivityType)activityType;	// called to fetch data after an activity is selected. you can return nil.
 
 @optional
 
-- (NSString *)activityViewController:(UIActivityViewController *)activityViewController subjectForActivityType:(nullable NSString *)activityType; // if activity supports a Subject field. iOS 7.0
-- (NSString *)activityViewController:(UIActivityViewController *)activityViewController dataTypeIdentifierForActivityType:(nullable NSString *)activityType; // UTI for item if it is an NSData. iOS 7.0. will be called with nil activity and then selected activity
-- (nullable UIImage *)activityViewController:(UIActivityViewController *)activityViewController thumbnailImageForActivityType:(nullable NSString *)activityType suggestedSize:(CGSize)size; // if activity supports preview image. iOS 7.0
+- (NSString *)activityViewController:(UIActivityViewController *)activityViewController subjectForActivityType:(nullable UIActivityType)activityType; // if activity supports a Subject field. iOS 7.0
+- (NSString *)activityViewController:(UIActivityViewController *)activityViewController dataTypeIdentifierForActivityType:(nullable UIActivityType)activityType; // UTI for item if it is an NSData. iOS 7.0. will be called with nil activity and then selected activity
+- (nullable UIImage *)activityViewController:(UIActivityViewController *)activityViewController thumbnailImageForActivityType:(nullable UIActivityType)activityType suggestedSize:(CGSize)size; // if activity supports preview image. iOS 7.0
 
 @end
 
@@ -33,7 +34,7 @@
 - (instancetype)initWithPlaceholderItem:(id)placeholderItem NS_DESIGNATED_INITIALIZER;               // placeHolder is the return value for -activityViewControllerPlaceholderItem:
 
 @property(nullable,nonatomic,strong,readonly) id        placeholderItem;
-@property(nullable,nonatomic,copy,readonly)   NSString *activityType;     // activity type available when -item is called. nil at other times. use this in your -item method to customize the data to return
+@property(nullable,nonatomic,copy,readonly)   UIActivityType activityType;     // activity type available when -item is called. nil at other times. use this in your -item method to customize the data to return
 
 #if UIKIT_DEFINE_AS_PROPERTIES
 @property(nonnull, nonatomic, readonly) id item;   // called on secondary thread when user selects an activity. you must subclass and return a non-nil value. The item can use the UIActivityItemSource protocol to return extra information
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityViewController.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityViewController.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityViewController.h	2016-07-14 06:20:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIActivityViewController.h	2016-07-28 05:53:09.000000000 +0200
@@ -8,13 +8,12 @@
 #import <Foundation/Foundation.h>
 #import <UIKit/UIViewController.h>
 #import <UIKit/UIKitDefines.h>
+#import <UIKit/UIActivity.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
-@class UIActivity;
-
-typedef void (^UIActivityViewControllerCompletionHandler)(NSString * __nullable activityType, BOOL completed);
-typedef void (^UIActivityViewControllerCompletionWithItemsHandler)(NSString * __nullable activityType, BOOL completed, NSArray * __nullable returnedItems, NSError * __nullable activityError);
+typedef void (^UIActivityViewControllerCompletionHandler)(UIActivityType __nullable activityType, BOOL completed);
+typedef void (^UIActivityViewControllerCompletionWithItemsHandler)(UIActivityType __nullable activityType, BOOL completed, NSArray * __nullable returnedItems, NSError * __nullable activityError);
 
 NS_CLASS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED @interface UIActivityViewController : UIViewController
 
@@ -26,7 +25,7 @@
 @property(nullable, nonatomic, copy) UIActivityViewControllerCompletionHandler completionHandler NS_DEPRECATED_IOS(6_0, 8_0, "Use completionWithItemsHandler instead.");  // set to nil after call
 @property(nullable, nonatomic, copy) UIActivityViewControllerCompletionWithItemsHandler completionWithItemsHandler NS_AVAILABLE_IOS(8_0); // set to nil after call
 
-@property(nullable, nonatomic, copy) NSArray<NSString *> *excludedActivityTypes; // default is nil. activity types listed will not be displayed
+@property(nullable, nonatomic, copy) NSArray<UIActivityType> *excludedActivityTypes; // default is nil. activity types listed will not be displayed
 
 @end
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h	2016-07-13 05:29:34.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIApplication.h	2016-07-28 05:52:57.000000000 +0200
@@ -43,7 +43,7 @@
 /* This exception is raised if supportedInterfaceOrientations returns 0, or if preferredInterfaceOrientationForPresentation
    returns an orientation that is not supported.
 */
-UIKIT_EXTERN NSString *const UIApplicationInvalidInterfaceOrientationException NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN NSExceptionName const UIApplicationInvalidInterfaceOrientationException NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
 
 typedef NS_OPTIONS(NSUInteger, UIInterfaceOrientationMask) {
     UIInterfaceOrientationMaskPortrait = (1 << UIInterfaceOrientationPortrait),
@@ -279,19 +279,38 @@
 @end
 
 
+#if UIKIT_STRING_ENUMS
+typedef NSString * UIApplicationLaunchOptionsKey NS_EXTENSIBLE_STRING_ENUM;
+#else
+typedef NSString * UIApplicationLaunchOptionsKey;
+#endif
+
 @protocol UIApplicationDelegate<NSObject>
 
 @optional
 
 - (void)applicationDidFinishLaunching:(UIApplication *)application;
+#if UIKIT_STRING_ENUMS
+- (BOOL)application:(UIApplication *)application willFinishLaunchingWithOptions:(nullable NSDictionary<UIApplicationLaunchOptionsKey, id> *)launchOptions NS_AVAILABLE_IOS(6_0);
+- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(nullable NSDictionary<UIApplicationLaunchOptionsKey, id> *)launchOptions NS_AVAILABLE_IOS(3_0);
+#else
 - (BOOL)application:(UIApplication *)application willFinishLaunchingWithOptions:(nullable NSDictionary *)launchOptions NS_AVAILABLE_IOS(6_0);
 - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(nullable NSDictionary *)launchOptions NS_AVAILABLE_IOS(3_0);
+#endif
 
 - (void)applicationDidBecomeActive:(UIApplication *)application;
 - (void)applicationWillResignActive:(UIApplication *)application;
 - (BOOL)application:(UIApplication *)application handleOpenURL:(NSURL *)url NS_DEPRECATED_IOS(2_0, 9_0, "Please use application:openURL:options:") __TVOS_PROHIBITED;
 - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url sourceApplication:(nullable NSString *)sourceApplication annotation:(id)annotation NS_DEPRECATED_IOS(4_2, 9_0, "Please use application:openURL:options:") __TVOS_PROHIBITED;
-- (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<NSString*, id> *)options NS_AVAILABLE_IOS(9_0); // no equiv. notification. return NO if the application can't open for some reason
+
+
+#if UIKIT_STRING_ENUMS
+typedef NSString * UIApplicationOpenURLOptionsKey NS_EXTENSIBLE_STRING_ENUM;
+#else
+typedef NSString * UIApplicationOpenURLOptionsKey;
+#endif
+
+- (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey, id> *)options NS_AVAILABLE_IOS(9_0); // no equiv. notification. return NO if the application can't open for some reason
 
 - (void)applicationDidReceiveMemoryWarning:(UIApplication *)application;      // try to clean up as much memory as possible. next step is to terminate app
 - (void)applicationWillTerminate:(UIApplication *)application;
@@ -361,10 +380,16 @@
 
 - (UIInterfaceOrientationMask)application:(UIApplication *)application supportedInterfaceOrientationsForWindow:(nullable UIWindow *)window  NS_AVAILABLE_IOS(6_0) __TVOS_PROHIBITED;
 
+#if UIKIT_STRING_ENUMS
+typedef NSString * UIApplicationExtensionPointIdentifier NS_EXTENSIBLE_STRING_ENUM;
+#else
+typedef NSString * UIApplicationExtensionPointIdentifier;
+#endif
+
 // Applications may reject specific types of extensions based on the extension point identifier.
 // Constants representing common extension point identifiers are provided further down.
 // If unimplemented, the default behavior is to allow the extension point identifier.
-- (BOOL)application:(UIApplication *)application shouldAllowExtensionPointIdentifier:(NSString *)extensionPointIdentifier NS_AVAILABLE_IOS(8_0);
+- (BOOL)application:(UIApplication *)application shouldAllowExtensionPointIdentifier:(UIApplicationExtensionPointIdentifier)extensionPointIdentifier NS_AVAILABLE_IOS(8_0);
 
 #pragma mark -- State Restoration protocol adopted by UIApplication delegate --
 
@@ -395,6 +420,9 @@
 - (void)application:(UIApplication *)application didUpdateUserActivity:(NSUserActivity *)userActivity NS_AVAILABLE_IOS(8_0);
 
 #pragma mark -- CloudKit Sharing Invitation Handling --
+// This will be called on the main thread after the user indicates they want to accept a CloudKit sharing invitation in your application.
+// You should use the CKShareMetadata object's shareURL and containerIdentifier to schedule a CKAcceptSharesOperation, then start using
+// the resulting CKShare and its associated record(s), which will appear in the CKContainer's shared database in a zone matching that of the record's owner.
 - (void) application:(UIApplication *)application userDidAcceptCloudKitShareWithMetadata:(CKShareMetadata *)cloudKitShareMetadata NS_AVAILABLE_IOS(10_0);
 
 @end
@@ -425,54 +453,83 @@
 // NSPrincipalClass key specified, the UIApplication class is used. The delegate class will be instantiated using init.
 UIKIT_EXTERN int UIApplicationMain(int argc, char *argv[], NSString * __nullable principalClassName, NSString * __nullable delegateClassName);
 
-UIKIT_EXTERN NSString *const UITrackingRunLoopMode;
+UIKIT_EXTERN NSRunLoopMode const UITrackingRunLoopMode;
 
 // These notifications are sent out after the equivalent delegate message is called
-UIKIT_EXTERN NSString *const UIApplicationDidEnterBackgroundNotification       NS_AVAILABLE_IOS(4_0);
-UIKIT_EXTERN NSString *const UIApplicationWillEnterForegroundNotification      NS_AVAILABLE_IOS(4_0);
-UIKIT_EXTERN NSString *const UIApplicationDidFinishLaunchingNotification;
-UIKIT_EXTERN NSString *const UIApplicationDidBecomeActiveNotification;
-UIKIT_EXTERN NSString *const UIApplicationWillResignActiveNotification;
-UIKIT_EXTERN NSString *const UIApplicationDidReceiveMemoryWarningNotification;
-UIKIT_EXTERN NSString *const UIApplicationWillTerminateNotification;
-UIKIT_EXTERN NSString *const UIApplicationSignificantTimeChangeNotification;
-UIKIT_EXTERN NSString *const UIApplicationWillChangeStatusBarOrientationNotification __TVOS_PROHIBITED; // userInfo contains NSNumber with new orientation
-UIKIT_EXTERN NSString *const UIApplicationDidChangeStatusBarOrientationNotification __TVOS_PROHIBITED;  // userInfo contains NSNumber with old orientation
+UIKIT_EXTERN NSNotificationName const UIApplicationDidEnterBackgroundNotification       NS_AVAILABLE_IOS(4_0);
+UIKIT_EXTERN NSNotificationName const UIApplicationWillEnterForegroundNotification      NS_AVAILABLE_IOS(4_0);
+UIKIT_EXTERN NSNotificationName const UIApplicationDidFinishLaunchingNotification;
+UIKIT_EXTERN NSNotificationName const UIApplicationDidBecomeActiveNotification;
+UIKIT_EXTERN NSNotificationName const UIApplicationWillResignActiveNotification;
+UIKIT_EXTERN NSNotificationName const UIApplicationDidReceiveMemoryWarningNotification;
+UIKIT_EXTERN NSNotificationName const UIApplicationWillTerminateNotification;
+UIKIT_EXTERN NSNotificationName const UIApplicationSignificantTimeChangeNotification;
+UIKIT_EXTERN NSNotificationName const UIApplicationWillChangeStatusBarOrientationNotification __TVOS_PROHIBITED; // userInfo contains NSNumber with new orientation
+UIKIT_EXTERN NSNotificationName const UIApplicationDidChangeStatusBarOrientationNotification __TVOS_PROHIBITED;  // userInfo contains NSNumber with old orientation
 UIKIT_EXTERN NSString *const UIApplicationStatusBarOrientationUserInfoKey __TVOS_PROHIBITED;            // userInfo dictionary key for status bar orientation
-UIKIT_EXTERN NSString *const UIApplicationWillChangeStatusBarFrameNotification __TVOS_PROHIBITED;       // userInfo contains NSValue with new frame
-UIKIT_EXTERN NSString *const UIApplicationDidChangeStatusBarFrameNotification __TVOS_PROHIBITED;        // userInfo contains NSValue with old frame
+UIKIT_EXTERN NSNotificationName const UIApplicationWillChangeStatusBarFrameNotification __TVOS_PROHIBITED;       // userInfo contains NSValue with new frame
+UIKIT_EXTERN NSNotificationName const UIApplicationDidChangeStatusBarFrameNotification __TVOS_PROHIBITED;        // userInfo contains NSValue with old frame
 UIKIT_EXTERN NSString *const UIApplicationStatusBarFrameUserInfoKey __TVOS_PROHIBITED;                  // userInfo dictionary key for status bar frame
-UIKIT_EXTERN NSString *const UIApplicationBackgroundRefreshStatusDidChangeNotification NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsURLKey                   NS_AVAILABLE_IOS(3_0); // userInfo contains NSURL with launch URL
-UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsSourceApplicationKey     NS_AVAILABLE_IOS(3_0); // userInfo contains NSString with launch app bundle ID
-UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsRemoteNotificationKey    NS_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED; // userInfo contains NSDictionary with payload
-UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsLocalNotificationKey     NS_DEPRECATED_IOS(4_0, 10_0, "Use UserNotifications Framework's -[UNUserNotificationCenterDelegate didReceiveNotificationResponse:withCompletionHandler:]") __TVOS_PROHIBITED; // userInfo contains a UILocalNotification
-UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsAnnotationKey            NS_AVAILABLE_IOS(3_2); // userInfo contains object with annotation property list
-UIKIT_EXTERN NSString *const UIApplicationProtectedDataWillBecomeUnavailable    NS_AVAILABLE_IOS(4_0);
-UIKIT_EXTERN NSString *const UIApplicationProtectedDataDidBecomeAvailable       NS_AVAILABLE_IOS(4_0);
-UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsLocationKey              NS_AVAILABLE_IOS(4_0); // app was launched in response to a CoreLocation event.
-UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsNewsstandDownloadsKey    NS_AVAILABLE_IOS(5_0) __TVOS_PROHIBITED; // userInfo contains an NSArray of NKAssetDownload identifiers
-UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsBluetoothCentralsKey     NS_AVAILABLE_IOS(7_0); // userInfo contains an NSArray of CBCentralManager restore identifiers
-UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsBluetoothPeripheralsKey  NS_AVAILABLE_IOS(7_0); // userInfo contains an NSArray of CBPeripheralManager restore identifiers
-UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsShortcutItemKey          NS_AVAILABLE_IOS(9_0) __TVOS_PROHIBITED; // userInfo contains the UIApplicationShortcutItem used to launch the app.
+UIKIT_EXTERN NSNotificationName const UIApplicationBackgroundRefreshStatusDidChangeNotification NS_AVAILABLE_IOS(7_0) __TVOS_PROHIBITED;
+
+UIKIT_EXTERN NSNotificationName const UIApplicationProtectedDataWillBecomeUnavailable    NS_AVAILABLE_IOS(4_0);
+UIKIT_EXTERN NSNotificationName const UIApplicationProtectedDataDidBecomeAvailable       NS_AVAILABLE_IOS(4_0);
 
+#if UIKIT_STRING_ENUMS
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsURLKey                   NS_SWIFT_NAME(url) NS_AVAILABLE_IOS(3_0); // userInfo contains NSURL with launch URL
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsSourceApplicationKey     NS_SWIFT_NAME(sourceApplication) NS_AVAILABLE_IOS(3_0); // userInfo contains NSString with launch app bundle ID
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsRemoteNotificationKey    NS_SWIFT_NAME(remoteNotification) NS_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED; // userInfo contains NSDictionary with payload
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsLocalNotificationKey     NS_SWIFT_NAME(localNotification) NS_DEPRECATED_IOS(4_0, 10_0, "Use UserNotifications Framework's -[UNUserNotificationCenterDelegate didReceiveNotificationResponse:withCompletionHandler:]") __TVOS_PROHIBITED; // userInfo contains a UILocalNotification
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsAnnotationKey            NS_SWIFT_NAME(annotation) NS_AVAILABLE_IOS(3_2); // userInfo contains object with annotation property list
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsLocationKey              NS_SWIFT_NAME(location) NS_AVAILABLE_IOS(4_0); // app was launched in response to a CoreLocation event.
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsNewsstandDownloadsKey    NS_SWIFT_NAME(newsstandDownloads) NS_AVAILABLE_IOS(5_0) __TVOS_PROHIBITED; // userInfo contains an NSArray of NKAssetDownload identifiers
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsBluetoothCentralsKey     NS_SWIFT_NAME(bluetoothCentrals) NS_AVAILABLE_IOS(7_0); // userInfo contains an NSArray of CBCentralManager restore identifiers
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsBluetoothPeripheralsKey  NS_SWIFT_NAME(bluetoothPeripherals) NS_AVAILABLE_IOS(7_0); // userInfo contains an NSArray of CBPeripheralManager restore identifiers
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsShortcutItemKey          NS_SWIFT_NAME(shortcutItem) NS_AVAILABLE_IOS(9_0) __TVOS_PROHIBITED; // userInfo contains the UIApplicationShortcutItem used to launch the app.
+
+// Key in options dict passed to application:[will | did]FinishLaunchingWithOptions and info for UIApplicationDidFinishLaunchingNotification
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsUserActivityDictionaryKey    NS_SWIFT_NAME(userActivityDictionary) NS_AVAILABLE_IOS(8_0); // Sub-Dictionary present in launch options when user activity is present
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsUserActivityTypeKey          NS_SWIFT_NAME(userActivityType) NS_AVAILABLE_IOS(8_0); // Key in user activity dictionary for the activity type
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsCloudKitShareMetadataKey NS_SWIFT_NAME(cloudKitShareMetadata) NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED; // The presence of this key indicates that the app was launched in order to handle a CloudKit sharing invitation. The value of this key is a CKShareMetadata object.
+#else
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsURLKey                   NS_AVAILABLE_IOS(3_0); // userInfo contains NSURL with launch URL
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsSourceApplicationKey     NS_AVAILABLE_IOS(3_0); // userInfo contains NSString with launch app bundle ID
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsRemoteNotificationKey    NS_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED; // userInfo contains NSDictionary with payload
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsLocalNotificationKey     NS_DEPRECATED_IOS(4_0, 10_0, "Use UserNotifications Framework's -[UNUserNotificationCenterDelegate didReceiveNotificationResponse:withCompletionHandler:]") __TVOS_PROHIBITED; // userInfo contains a UILocalNotification
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsAnnotationKey            NS_AVAILABLE_IOS(3_2); // userInfo contains object with annotation property list
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsLocationKey              NS_AVAILABLE_IOS(4_0); // app was launched in response to a CoreLocation event.
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsNewsstandDownloadsKey    NS_AVAILABLE_IOS(5_0) __TVOS_PROHIBITED; // userInfo contains an NSArray of NKAssetDownload identifiers
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsBluetoothCentralsKey     NS_AVAILABLE_IOS(7_0); // userInfo contains an NSArray of CBCentralManager restore identifiers
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsBluetoothPeripheralsKey  NS_AVAILABLE_IOS(7_0); // userInfo contains an NSArray of CBPeripheralManager restore identifiers
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsShortcutItemKey          NS_AVAILABLE_IOS(9_0) __TVOS_PROHIBITED; // userInfo contains the UIApplicationShortcutItem used to launch the app.
 // Key in options dict passed to application:[will | did]FinishLaunchingWithOptions and info for UIApplicationDidFinishLaunchingNotification
-UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsUserActivityDictionaryKey    NS_AVAILABLE_IOS(8_0); // Sub-Dictionary present in launch options when user activity is present
-UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsUserActivityTypeKey          NS_AVAILABLE_IOS(8_0); // Key in user activity dictionary for the activity type
-UIKIT_EXTERN NSString *const UIApplicationLaunchOptionsCloudKitShareMetadataKey NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED; // The presence of this key indicates that the app was launched in order to handle a CloudKit sharing invitation. The value of this key is a CKShareMetadata object.
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsUserActivityDictionaryKey NS_AVAILABLE_IOS(8_0); // Sub-Dictionary present in launch options when user activity is present
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsUserActivityTypeKey NS_AVAILABLE_IOS(8_0); // Key in user activity dictionary for the activity type
+UIKIT_EXTERN UIApplicationLaunchOptionsKey const UIApplicationLaunchOptionsCloudKitShareMetadataKey NS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED; // The presence of this key indicates that the app was launched in order to handle a CloudKit sharing invitation. The value of this key is a CKShareMetadata object.
+#endif
 
 UIKIT_EXTERN NSString *const UIApplicationOpenSettingsURLString NS_AVAILABLE_IOS(8_0);
 
 // Keys for application:openURL:options:
-UIKIT_EXTERN NSString *const UIApplicationOpenURLOptionsSourceApplicationKey NS_AVAILABLE_IOS(9_0);   // value is an NSString containing the bundle ID of the originating application
-UIKIT_EXTERN NSString *const UIApplicationOpenURLOptionsAnnotationKey NS_AVAILABLE_IOS(9_0);   // value is a property-list typed object corresponding to what the originating application passed in UIDocumentInteractionController's annotation property
-UIKIT_EXTERN NSString *const UIApplicationOpenURLOptionsOpenInPlaceKey NS_AVAILABLE_IOS(9_0);   // value is a bool NSNumber, set to YES if the file needs to be copied before use
+#if UIKIT_STRING_ENUMS
+UIKIT_EXTERN UIApplicationOpenURLOptionsKey const UIApplicationOpenURLOptionsSourceApplicationKey NS_SWIFT_NAME(sourceApplication) NS_AVAILABLE_IOS(9_0);   // value is an NSString containing the bundle ID of the originating application
+UIKIT_EXTERN UIApplicationOpenURLOptionsKey const UIApplicationOpenURLOptionsAnnotationKey NS_SWIFT_NAME(annotation) NS_AVAILABLE_IOS(9_0);   // value is a property-list typed object corresponding to what the originating application passed in UIDocumentInteractionController's annotation property
+UIKIT_EXTERN UIApplicationOpenURLOptionsKey const UIApplicationOpenURLOptionsOpenInPlaceKey NS_SWIFT_NAME(openInPlace) NS_AVAILABLE_IOS(9_0);   // value is a bool NSNumber, set to YES if the file needs to be copied before use
+#else
+UIKIT_EXTERN UIApplicationOpenURLOptionsKey const UIApplicationOpenURLOptionsSourceApplicationKey NS_AVAILABLE_IOS(9_0);   // value is an NSString containing the bundle ID of the originating application
+UIKIT_EXTERN UIApplicationOpenURLOptionsKey const UIApplicationOpenURLOptionsAnnotationKey NS_AVAILABLE_IOS(9_0);   // value is a property-list typed object corresponding to what the originating application passed in UIDocumentInteractionController's annotation property
+UIKIT_EXTERN UIApplicationOpenURLOptionsKey const UIApplicationOpenURLOptionsOpenInPlaceKey NS_AVAILABLE_IOS(9_0);   // value is a bool NSNumber, set to YES if the file needs to be copied before use
+#endif
 
 // This notification is posted after the user takes a screenshot (for example by pressing both the home and lock screen buttons)
-UIKIT_EXTERN NSString *const UIApplicationUserDidTakeScreenshotNotification NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN NSNotificationName const UIApplicationUserDidTakeScreenshotNotification NS_AVAILABLE_IOS(7_0);
 
 // Extension point identifier constants
-UIKIT_EXTERN NSString *const UIApplicationKeyboardExtensionPointIdentifier NS_AVAILABLE_IOS(8_0);
+#if UIKIT_STRING_ENUMS
+UIKIT_EXTERN UIApplicationExtensionPointIdentifier const UIApplicationKeyboardExtensionPointIdentifier NS_SWIFT_NAME(keyboard) NS_AVAILABLE_IOS(8_0);
+#else
+UIKIT_EXTERN UIApplicationExtensionPointIdentifier const UIApplicationKeyboardExtensionPointIdentifier NS_AVAILABLE_IOS(8_0);
+#endif
 
 #pragma mark -- openURL options --
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICloudSharingController.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICloudSharingController.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICloudSharingController.h	2016-07-14 06:20:58.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICloudSharingController.h	2016-07-28 05:53:08.000000000 +0200
@@ -15,20 +15,28 @@
 @class UICloudSharingController, CKShare, CKContainer;
 
 typedef NS_OPTIONS(NSUInteger, UICloudSharingPermissionOptions) {
-    // Choose one or none of the following
-    UICloudSharingPermissionPublicOnly = 1 << 0,    // The user is only allowed to share publicly
-    UICloudSharingPermissionPrivateOnly = 1 << 1,   // The user is only allowed to share privately
-
-    // Choose one or none of the following
-    UICloudSharingPermissionReadOnly = 1 << 2,  // The user is only allowed to grant participants read-only permissions
-    UICloudSharingPermissionReadWrite = 1 << 3, // The user is only allowed to grant participants read/write permissions
-};
+    UICloudSharingPermissionStandard = 0, // Allow the user to configure the share with the standard set of options
+
+    UICloudSharingPermissionAllowPublic = 1 << 0,    // The user is allowed to share publicly
+    UICloudSharingPermissionAllowPrivate = 1 << 1,   // The user is allowed to share privately
+
+    UICloudSharingPermissionAllowReadOnly = 1 << 2,  // The user is allowed to grant participants read-only permissions
+    UICloudSharingPermissionAllowReadWrite = 1 << 3, // The user is allowed to grant participants read/write permissions
+} NS_ENUM_AVAILABLE_IOS(10_0);
 
 @protocol UICloudSharingControllerDelegate <NSObject>
 
 - (void)cloudSharingController:(UICloudSharingController *)csc failedToSaveShareWithError:(NSError *)error;
 
+// corresponds to CKShareTitleKey on the expected share
+- (nullable NSString *)itemTitleForCloudSharingController:(UICloudSharingController *)csc;
+
 @optional
+// corresponds to CKShareThumbnailImageDataKey on the expected share
+- (nullable NSData *)itemThumbnailDataForCloudSharingController:(UICloudSharingController *)csc;
+// corresponds to CKShareTypeKey on the expected share
+- (nullable NSString *)itemTypeForCloudSharingController:(UICloudSharingController *)csc;
+
 - (void)cloudSharingControllerDidSaveShare:(UICloudSharingController *)csc;
 - (void)cloudSharingControllerDidStopSharing:(UICloudSharingController *)csc;
 
@@ -40,12 +48,11 @@
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_UNAVAILABLE;
 
 /* Use this initializer when you want to share a set of CKRecords but haven't yet saved a CKShare.
- The passed-in, not-yet-saved share can have keys such as the title or thumbnail set.
  The preparation handler is called when it is time to save the share to the server.
  After ensuring the share and record have been saved to the server, invoke the preparationCompletionHandler
  with either the resulting CKShare, or an NSError if saving failed.
  */
-- (instancetype)initWithShare:(CKShare *)share preparationHandler:(void (^)(UICloudSharingController *controller, void (^preparationCompletionHandler)(CKShare * _Nullable, CKContainer * _Nullable, NSError * _Nullable)))preparationHandler;
+- (instancetype)initWithPreparationHandler:(void (^)(UICloudSharingController *controller, void (^preparationCompletionHandler)(CKShare * _Nullable, CKContainer * _Nullable, NSError * _Nullable)))preparationHandler;
 
 /* Use this initializer when you already have an active CKShare that was set up previously.
  */
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIContentSizeCategory.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIContentSizeCategory.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIContentSizeCategory.h	2016-07-14 06:20:58.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIContentSizeCategory.h	2016-07-28 05:53:08.000000000 +0200
@@ -10,7 +10,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-typedef NSString * UIContentSizeCategory NS_STRING_ENUM NS_AVAILABLE_IOS(10_0);
+typedef NSString * UIContentSizeCategory NS_STRING_ENUM NS_AVAILABLE_IOS(7_0);
 
 // Content size category constants
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDevice.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDevice.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDevice.h	2016-07-14 06:20:58.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDevice.h	2016-07-28 05:52:58.000000000 +0200
@@ -94,9 +94,9 @@
             UIUserInterfaceIdiomPhone);
 }
 
-UIKIT_EXTERN NSString *const UIDeviceOrientationDidChangeNotification __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIDeviceBatteryStateDidChangeNotification   NS_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIDeviceBatteryLevelDidChangeNotification   NS_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIDeviceProximityStateDidChangeNotification NS_AVAILABLE_IOS(3_0);
+UIKIT_EXTERN NSNotificationName const UIDeviceOrientationDidChangeNotification __TVOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIDeviceBatteryStateDidChangeNotification   NS_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIDeviceBatteryLevelDidChangeNotification   NS_AVAILABLE_IOS(3_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIDeviceProximityStateDidChangeNotification NS_AVAILABLE_IOS(3_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDocument.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDocument.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDocument.h	2016-07-14 06:20:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIDocument.h	2016-07-28 05:52:58.000000000 +0200
@@ -31,7 +31,7 @@
     UIDocumentStateProgressAvailable = 1 << 4  // Set if the document is busy loading or saving. Progress is valid while this is set.
 } __TVOS_PROHIBITED;
 
-UIKIT_EXTERN NSString *const UIDocumentStateChangedNotification NS_AVAILABLE_IOS(5_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIDocumentStateChangedNotification NS_AVAILABLE_IOS(5_0) __TVOS_PROHIBITED;
 
 NS_CLASS_AVAILABLE_IOS(5_0) __TVOS_PROHIBITED @interface UIDocument : NSObject <NSFilePresenter, NSProgressReporting>
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h	2016-07-14 06:20:58.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFont.h	2016-07-28 05:53:08.000000000 +0200
@@ -17,9 +17,9 @@
 NS_CLASS_AVAILABLE_IOS(2_0) @interface UIFont : NSObject <NSCopying>
 
 // Returns an instance of the font associated with the text style and scaled appropriately for the user's selected content size category. See UIFontDescriptor.h for the complete list.
-+ (UIFont *)preferredFontForTextStyle:(NSString *)style NS_AVAILABLE_IOS(7_0);
++ (UIFont *)preferredFontForTextStyle:(UIFontTextStyle)style NS_AVAILABLE_IOS(7_0);
 // Returns an instance of the font associated with the text style and scaled appropriately for the content size category defined in the trait collection.
-+ (UIFont *)preferredFontForTextStyle:(NSString *)style compatibleWithTraitCollection:(nullable UITraitCollection *)traitCollection NS_AVAILABLE_IOS(10_0);
++ (UIFont *)preferredFontForTextStyle:(UIFontTextStyle)style compatibleWithTraitCollection:(nullable UITraitCollection *)traitCollection NS_AVAILABLE_IOS(10_0);
 
 // Returns a font using CSS name matching semantics.
 + (nullable UIFont *)fontWithName:(NSString *)fontName size:(CGFloat)fontSize;
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h	2016-07-11 07:32:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIFontDescriptor.h	2016-07-28 04:43:52.000000000 +0200
@@ -46,6 +46,11 @@
 } NS_ENUM_AVAILABLE_IOS(7_0);
 
 typedef NSUInteger UIFontDescriptorClass;
+#if UIKIT_STRING_ENUMS
+typedef NSString * UIFontTextStyle NS_EXTENSIBLE_STRING_ENUM;
+#else
+typedef NSString * UIFontTextStyle;
+#endif
 
 @class NSMutableDictionary, NSDictionary, NSArray, NSSet, UITraitCollection;
 
@@ -78,9 +83,9 @@
 + (UIFontDescriptor *)fontDescriptorWithName:(NSString *)fontName matrix:(CGAffineTransform)matrix;
 
 // Returns a font descriptor containing the text style and containing the user's selected content size category.
-+ (UIFontDescriptor *)preferredFontDescriptorWithTextStyle:(NSString *)style;
++ (UIFontDescriptor *)preferredFontDescriptorWithTextStyle:(UIFontTextStyle)style;
 // Returns a font descriptor containing the text style and containing the content size category defined in the trait collection.
-+ (UIFontDescriptor *)preferredFontDescriptorWithTextStyle:(NSString *)style compatibleWithTraitCollection:(nullable UITraitCollection *)traitCollection NS_AVAILABLE_IOS(10_0);
++ (UIFontDescriptor *)preferredFontDescriptorWithTextStyle:(UIFontTextStyle)style compatibleWithTraitCollection:(nullable UITraitCollection *)traitCollection NS_AVAILABLE_IOS(10_0);
 
 - (instancetype)initWithFontAttributes:(NSDictionary<NSString *, id> *)attributes NS_DESIGNATED_INITIALIZER;
 
@@ -146,16 +151,16 @@
 UIKIT_EXTERN NSString *const UIFontFeatureSelectorIdentifierKey NS_AVAILABLE_IOS(7_0);
 
 // Font text styles, semantic descriptions of the intended use for a font returned by +[UIFont preferredFontForTextStyle:]
-UIKIT_EXTERN NSString *const UIFontTextStyleTitle1 NS_AVAILABLE_IOS(9_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleTitle2 NS_AVAILABLE_IOS(9_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleTitle3 NS_AVAILABLE_IOS(9_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleHeadline NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleSubheadline NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleBody NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleCallout NS_AVAILABLE_IOS(9_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleFootnote NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleCaption1 NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UIFontTextStyleCaption2 NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleTitle1 NS_AVAILABLE_IOS(9_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleTitle2 NS_AVAILABLE_IOS(9_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleTitle3 NS_AVAILABLE_IOS(9_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleHeadline NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleSubheadline NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleBody NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleCallout NS_AVAILABLE_IOS(9_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleFootnote NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleCaption1 NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UIFontTextStyle const UIFontTextStyleCaption2 NS_AVAILABLE_IOS(7_0);
 
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizer.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizer.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizer.h	2016-07-13 05:29:35.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIGestureRecognizer.h	2016-07-28 04:43:53.000000000 +0200
@@ -51,7 +51,7 @@
 @property(nonatomic) BOOL delaysTouchesBegan;         // default is NO.  causes all touch or press events to be delivered to the target view only after this gesture has failed recognition. set to YES to prevent views from processing any touches or presses that may be recognized as part of this gesture
 @property(nonatomic) BOOL delaysTouchesEnded;         // default is YES. causes touchesEnded or pressesEnded events to be delivered to the target view only after this gesture has failed recognition. this ensures that a touch or press that is part of the gesture can be cancelled if the gesture is recognized
 
-@property(nonatomic, copy) NSArray<NSNumber *> *allowedTouchTypes NS_AVAILABLE_IOS(9_0); // Array of UITouchType's as NSNumbers.
+@property(nonatomic, copy) NSArray<NSNumber *> *allowedTouchTypes NS_AVAILABLE_IOS(9_0); // Array of UITouchTypes as NSNumbers.
 @property(nonatomic, copy) NSArray<NSNumber *> *allowedPressTypes NS_AVAILABLE_IOS(9_0); // Array of UIPressTypes as NSNumbers.
 
 // Indicates whether the gesture recognizer will consider touches of different touch types simultaneously.
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-07-11 07:25:47.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKit.h	2016-07-28 05:06:41.000000000 +0200
@@ -218,3 +218,4 @@
 #if __has_include(<UIKit/UIViewPropertyAnimator.h>)
 #import <UIKit/UIViewPropertyAnimator.h>
 #endif
+
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h	2016-07-14 06:20:58.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIKitDefines.h	2016-07-28 05:53:08.000000000 +0200
@@ -29,3 +29,4 @@
 
 #define UIKIT_DEFINE_AS_PROPERTIES (!defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_UIKIT_EPOCH) && SWIFT_SDK_OVERLAY_UIKIT_EPOCH >= 1))
 #define UIKIT_REMOVE_ZERO_FROM_SWIFT (!defined(SWIFT_CLASS_EXTRA) || (defined(SWIFT_SDK_OVERLAY_UIKIT_EPOCH) && SWIFT_SDK_OVERLAY_UIKIT_EPOCH >= 1))
+#define UIKIT_STRING_ENUMS ((defined(SWIFT_SDK_OVERLAY_UIKIT_EPOCH) && SWIFT_SDK_OVERLAY_UIKIT_EPOCH >= 2))
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIMenuController.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIMenuController.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIMenuController.h	2016-07-14 06:20:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIMenuController.h	2016-07-28 05:53:09.000000000 +0200
@@ -43,11 +43,11 @@
 
 @end
 
-UIKIT_EXTERN NSString *const UIMenuControllerWillShowMenuNotification __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIMenuControllerDidShowMenuNotification __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIMenuControllerWillHideMenuNotification __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIMenuControllerDidHideMenuNotification __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIMenuControllerMenuFrameDidChangeNotification __TVOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIMenuControllerWillShowMenuNotification __TVOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIMenuControllerDidShowMenuNotification __TVOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIMenuControllerWillHideMenuNotification __TVOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIMenuControllerDidHideMenuNotification __TVOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIMenuControllerMenuFrameDidChangeNotification __TVOS_PROHIBITED;
 
 NS_CLASS_AVAILABLE_IOS(3_2) __TVOS_PROHIBITED @interface UIMenuItem : NSObject 
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPasteboard.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPasteboard.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPasteboard.h	2016-07-13 05:29:35.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPasteboard.h	2016-07-28 05:52:58.000000000 +0200
@@ -10,7 +10,13 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-UIKIT_EXTERN NSString *const UIPasteboardNameGeneral __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+#if UIKIT_STRING_ENUMS
+typedef NSString * UIPasteboardName NS_EXTENSIBLE_STRING_ENUM;
+#else
+typedef NSString * UIPasteboardName;
+#endif
+
+UIKIT_EXTERN UIPasteboardName const UIPasteboardNameGeneral __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 UIKIT_EXTERN NSString *const UIPasteboardNameFind __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_DEPRECATED_IOS(3_0, 10_0, "The Find pasteboard is no longer available.");
 
 @class UIColor, UIImage;
@@ -23,12 +29,12 @@
 + (UIPasteboard *)generalPasteboard;
 #endif
 
-+ (nullable UIPasteboard *)pasteboardWithName:(NSString *)pasteboardName create:(BOOL)create;
++ (nullable UIPasteboard *)pasteboardWithName:(UIPasteboardName)pasteboardName create:(BOOL)create;
 + (UIPasteboard *)pasteboardWithUniqueName;
 
-@property(readonly,nonatomic) NSString *name;
+@property(readonly,nonatomic) UIPasteboardName name;
 
-+ (void)removePasteboardWithName:(NSString *)pasteboardName;
++ (void)removePasteboardWithName:(UIPasteboardName)pasteboardName;
 
 @property(readonly,getter=isPersistent,nonatomic) BOOL persistent;
 - (void)setPersistent:(BOOL)persistent NS_DEPRECATED_IOS(3_0, 10_0, "Do not set persistence on pasteboards. This property is set automatically.");
@@ -65,6 +71,7 @@
 - (void)addItems:(NSArray<NSDictionary<NSString *, id> *> *)items;
 
 typedef NSString * UIPasteboardOption NS_EXTENSIBLE_STRING_ENUM NS_AVAILABLE_IOS(10_0);
+
 UIKIT_EXTERN UIPasteboardOption const UIPasteboardOptionExpirationDate __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_AVAILABLE_IOS(10_0) NS_SWIFT_NAME(UIPasteboardOption.expirationDate); // Value: NSDate.
 UIKIT_EXTERN UIPasteboardOption const UIPasteboardOptionLocalOnly __TVOS_PROHIBITED __WATCHOS_PROHIBITED NS_AVAILABLE_IOS(10_0) NS_SWIFT_NAME(UIPasteboardOption.localOnly); // Value: NSNumber, boolean.
 
@@ -93,11 +100,11 @@
 
 // Notification
 
-UIKIT_EXTERN NSString *const UIPasteboardChangedNotification __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIPasteboardChangedNotification __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 UIKIT_EXTERN NSString *const UIPasteboardChangedTypesAddedKey __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 UIKIT_EXTERN NSString *const UIPasteboardChangedTypesRemovedKey __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
-UIKIT_EXTERN NSString *const UIPasteboardRemovedNotification __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIPasteboardRemovedNotification __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
 // Types
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintError.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintError.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintError.h	2016-07-14 06:20:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIPrintError.h	2016-07-28 05:53:09.000000000 +0200
@@ -10,7 +10,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-UIKIT_EXTERN NSString *const UIPrintErrorDomain __TVOS_PROHIBITED;
+UIKIT_EXTERN NSErrorDomain const UIPrintErrorDomain __TVOS_PROHIBITED;
 
 enum {
     UIPrintingNotAvailableError = 1,  // cannot print at this time
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScreen.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScreen.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScreen.h	2016-07-14 06:20:58.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIScreen.h	2016-07-28 05:01:11.000000000 +0200
@@ -16,12 +16,12 @@
 @class UIScreenMode, CADisplayLink, UIView;
 
 // Object is the UIScreen that represents the new screen. Connection notifications are not sent for screens present when the application is first launched
-UIKIT_EXTERN NSString *const UIScreenDidConnectNotification NS_AVAILABLE_IOS(3_2);
+UIKIT_EXTERN NSNotificationName const UIScreenDidConnectNotification NS_AVAILABLE_IOS(3_2);
 // Object is the UIScreen that represented the disconnected screen.
-UIKIT_EXTERN NSString *const UIScreenDidDisconnectNotification NS_AVAILABLE_IOS(3_2);
+UIKIT_EXTERN NSNotificationName const UIScreenDidDisconnectNotification NS_AVAILABLE_IOS(3_2);
 // Object is the UIScreen which changed. [object currentMode] is the new UIScreenMode.
-UIKIT_EXTERN NSString *const UIScreenModeDidChangeNotification NS_AVAILABLE_IOS(3_2);
-UIKIT_EXTERN NSString *const UIScreenBrightnessDidChangeNotification NS_AVAILABLE_IOS(5_0);
+UIKIT_EXTERN NSNotificationName const UIScreenModeDidChangeNotification NS_AVAILABLE_IOS(3_2);
+UIKIT_EXTERN NSNotificationName const UIScreenBrightnessDidChangeNotification NS_AVAILABLE_IOS(5_0);
 
 // when the connected screen is overscanning, UIScreen can attempt to compensate for the overscan to avoid clipping
 typedef NS_ENUM(NSInteger, UIScreenOverscanCompensation) {
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableView.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableView.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableView.h	2016-07-14 06:20:58.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITableView.h	2016-07-28 04:43:52.000000000 +0200
@@ -169,7 +169,7 @@
 
 @end
 
-UIKIT_EXTERN NSString *const UITableViewSelectionDidChangeNotification;
+UIKIT_EXTERN NSNotificationName const UITableViewSelectionDidChangeNotification;
 
 
 //_______________________________________________________________________________________________________________
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextField.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextField.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextField.h	2016-07-14 06:20:58.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextField.h	2016-07-28 04:43:52.000000000 +0200
@@ -123,9 +123,9 @@
 
 @end
 
-UIKIT_EXTERN NSString *const UITextFieldTextDidBeginEditingNotification;
-UIKIT_EXTERN NSString *const UITextFieldTextDidEndEditingNotification;
-UIKIT_EXTERN NSString *const UITextFieldTextDidChangeNotification;
+UIKIT_EXTERN NSNotificationName const UITextFieldTextDidBeginEditingNotification;
+UIKIT_EXTERN NSNotificationName const UITextFieldTextDidEndEditingNotification;
+UIKIT_EXTERN NSNotificationName const UITextFieldTextDidChangeNotification;
 
 NS_ASSUME_NONNULL_END
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInput.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInput.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInput.h	2016-07-14 06:20:59.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInput.h	2016-07-28 05:01:12.000000000 +0200
@@ -295,6 +295,6 @@
 
 @end
 
-UIKIT_EXTERN NSString *const UITextInputCurrentInputModeDidChangeNotification NS_AVAILABLE_IOS(4_2);
+UIKIT_EXTERN NSNotificationName const UITextInputCurrentInputModeDidChangeNotification NS_AVAILABLE_IOS(4_2);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInputTraits.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInputTraits.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInputTraits.h	2016-07-14 06:20:58.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextInputTraits.h	2016-07-28 04:43:52.000000000 +0200
@@ -114,6 +114,12 @@
     UIReturnKeyContinue NS_ENUM_AVAILABLE_IOS(9_0),
 };
 
+#if UIKIT_STRING_ENUMS
+typedef NSString * UITextContentType NS_EXTENSIBLE_STRING_ENUM;
+#else
+typedef NSString * UITextContentType;
+#endif
+
 //
 // UITextInputTraits
 //
@@ -134,31 +140,32 @@
 @property(nonatomic,getter=isSecureTextEntry) BOOL secureTextEntry;       // default is NO
 
 // The textContentType property is to provide the keyboard with extra information about the semantic intent of the text document.
-@property(nonatomic,copy) NSString *textContentType NS_AVAILABLE_IOS(10_0); // default is nil
+@property(nonatomic,copy) UITextContentType textContentType NS_AVAILABLE_IOS(10_0); // default is nil
 
 @end
 
-UIKIT_EXTERN NSString *const UITextContentTypeName                      NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeNamePrefix                NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeGivenName                 NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeMiddleName                NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeFamilyName                NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeNameSuffix                NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeNickname                  NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeJobTitle                  NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeOrganizationName          NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeLocation                  NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeFullStreetAddress         NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeStreetAddressLine1        NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeStreetAddressLine2        NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeAddressCity               NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeAddressState              NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeAddressCityAndState       NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeSublocality               NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeCountryName               NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypePostalCode                NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeTelephoneNumber           NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeEmailAddress              NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeURL                       NS_AVAILABLE_IOS(10_0);
-UIKIT_EXTERN NSString *const UITextContentTypeCreditCardNumber          NS_AVAILABLE_IOS(10_0);
+
+UIKIT_EXTERN UITextContentType const UITextContentTypeName                      NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeNamePrefix                NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeGivenName                 NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeMiddleName                NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeFamilyName                NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeNameSuffix                NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeNickname                  NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeJobTitle                  NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeOrganizationName          NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeLocation                  NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeFullStreetAddress         NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeStreetAddressLine1        NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeStreetAddressLine2        NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeAddressCity               NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeAddressState              NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeAddressCityAndState       NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeSublocality               NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeCountryName               NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypePostalCode                NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeTelephoneNumber           NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeEmailAddress              NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeURL                       NS_AVAILABLE_IOS(10_0);
+UIKIT_EXTERN UITextContentType const UITextContentTypeCreditCardNumber          NS_AVAILABLE_IOS(10_0);
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextView.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextView.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextView.h	2016-07-14 06:20:58.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UITextView.h	2016-07-28 04:43:52.000000000 +0200
@@ -86,8 +86,8 @@
 
 @end
 
-UIKIT_EXTERN NSString * const UITextViewTextDidBeginEditingNotification;
-UIKIT_EXTERN NSString * const UITextViewTextDidChangeNotification;
-UIKIT_EXTERN NSString * const UITextViewTextDidEndEditingNotification;
+UIKIT_EXTERN NSNotificationName const UITextViewTextDidBeginEditingNotification;
+UIKIT_EXTERN NSNotificationName const UITextViewTextDidChangeNotification;
+UIKIT_EXTERN NSNotificationName const UITextViewTextDidEndEditingNotification;
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewController.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewController.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewController.h	2016-07-13 05:30:12.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewController.h	2016-07-28 05:52:58.000000000 +0200
@@ -88,7 +88,7 @@
 @end
 
 // Sometimes view controllers that are using showViewController:sender and showDetailViewController:sender: will need to know when the split view controller environment above it has changed. This notification will be posted when that happens (for example, when a split view controller is collapsing or expanding). The NSNotification's object will be the view controller that caused the change.
-UIKIT_EXTERN NSString *const UIViewControllerShowDetailTargetDidChangeNotification NS_AVAILABLE_IOS(8_0);
+UIKIT_EXTERN NSNotificationName const UIViewControllerShowDetailTargetDidChangeNotification NS_AVAILABLE_IOS(8_0);
 
 NS_CLASS_AVAILABLE_IOS(2_0) @interface UIViewController : UIResponder <NSCoding, UIAppearanceContainer, UITraitEnvironment, UIContentContainer, UIFocusEnvironment>
 
@@ -352,7 +352,7 @@
   superview of the child view controller's view that has a view controller is NOT the child view controller's
   parent.
 */
-UIKIT_EXTERN NSString *const UIViewControllerHierarchyInconsistencyException NS_AVAILABLE_IOS(5_0);
+UIKIT_EXTERN NSExceptionName const UIViewControllerHierarchyInconsistencyException NS_AVAILABLE_IOS(5_0);
 
 /*
   The methods in the UIContainerViewControllerProtectedMethods and the UIContainerViewControllerCallbacks
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitionCoordinator.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitionCoordinator.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitionCoordinator.h	2016-07-13 05:30:13.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitionCoordinator.h	2016-07-28 04:43:53.000000000 +0200
@@ -12,6 +12,14 @@
 // view controller transition.
 NS_ASSUME_NONNULL_BEGIN
 
+#if UIKIT_STRING_ENUMS
+typedef NSString * UITransitionContextViewControllerKey NS_EXTENSIBLE_STRING_ENUM;
+typedef NSString * UITransitionContextViewKey NS_EXTENSIBLE_STRING_ENUM;
+#else
+typedef NSString * UITransitionContextViewControllerKey;
+typedef NSString * UITransitionContextViewKey;
+#endif
+
 @protocol UIViewControllerTransitionCoordinatorContext <NSObject>
 
 // Most of the time isAnimated will be YES. For custom transitions that use the
@@ -81,12 +89,12 @@
 // Currently only two keys are defined by the system:
 //   UITransitionContextToViewControllerKey
 //   UITransitionContextFromViewControllerKey
-- (nullable __kindof UIViewController *)viewControllerForKey:(NSString *)key;
+- (nullable __kindof UIViewController *)viewControllerForKey:(UITransitionContextViewControllerKey)key;
 
 // Currently only two keys are defined by the system:
 //   UITransitionContextToViewKey
 //   UITransitionContextFromViewKey
-- (nullable __kindof UIView *)viewForKey:(NSString *)key NS_AVAILABLE_IOS(8_0);
+- (nullable __kindof UIView *)viewForKey:(UITransitionContextViewKey)key NS_AVAILABLE_IOS(8_0);
 
 // The view in which the animated transition is taking place.
 #if UIKIT_DEFINE_AS_PROPERTIES
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitioning.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitioning.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitioning.h	2016-07-14 06:20:58.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIViewControllerTransitioning.h	2016-07-28 05:52:57.000000000 +0200
@@ -18,11 +18,20 @@
 // The following keys are understood by UIViewControllerContextTransitioning context objects
 // that are created by the system.
 
-UIKIT_EXTERN NSString *const UITransitionContextFromViewControllerKey NS_AVAILABLE_IOS(7_0);
-UIKIT_EXTERN NSString *const UITransitionContextToViewControllerKey NS_AVAILABLE_IOS(7_0);
+#if UIKIT_STRING_ENUMS
+UIKIT_EXTERN UITransitionContextViewControllerKey const UITransitionContextFromViewControllerKey NS_SWIFT_NAME(from) NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UITransitionContextViewControllerKey const UITransitionContextToViewControllerKey NS_SWIFT_NAME(to) NS_AVAILABLE_IOS(7_0);
+
+UIKIT_EXTERN UITransitionContextViewKey const UITransitionContextFromViewKey NS_SWIFT_NAME(from) NS_AVAILABLE_IOS(8_0);
+UIKIT_EXTERN UITransitionContextViewKey const UITransitionContextToViewKey NS_SWIFT_NAME(to) NS_AVAILABLE_IOS(8_0);
+#else
+UIKIT_EXTERN UITransitionContextViewControllerKey const UITransitionContextFromViewControllerKey NS_AVAILABLE_IOS(7_0);
+UIKIT_EXTERN UITransitionContextViewControllerKey const UITransitionContextToViewControllerKey NS_AVAILABLE_IOS(7_0);
+
+UIKIT_EXTERN UITransitionContextViewKey const UITransitionContextFromViewKey NS_AVAILABLE_IOS(8_0);
+UIKIT_EXTERN UITransitionContextViewKey const UITransitionContextToViewKey NS_AVAILABLE_IOS(8_0);
+#endif
 
-UIKIT_EXTERN NSString *const UITransitionContextFromViewKey NS_AVAILABLE_IOS(8_0);
-UIKIT_EXTERN NSString *const UITransitionContextToViewKey NS_AVAILABLE_IOS(8_0);
 
 // A transition context object is constructed by the system and passed to the
 // animator in its animateTransition: and transitionDuration: methods as well as
@@ -122,13 +131,13 @@
 // UITransitionContextFromViewControllerKey. 
 // Animators should not directly manipulate a view controller's views and should
 // use viewForKey: to get views instead.
-- (nullable __kindof UIViewController *)viewControllerForKey:(NSString *)key;
+- (nullable __kindof UIViewController *)viewControllerForKey:(UITransitionContextViewControllerKey)key;
 
 // Currently only two keys are defined by the system -
 // UITransitionContextFromViewKey, and UITransitionContextToViewKey
 // viewForKey: may return nil which would indicate that the animator should not
 // manipulate the associated view controller's view.
-- (nullable __kindof UIView *)viewForKey:(NSString *)key NS_AVAILABLE_IOS(8_0);
+- (nullable __kindof UIView *)viewForKey:(UITransitionContextViewKey)key NS_AVAILABLE_IOS(8_0);
 
 #if UIKIT_DEFINE_AS_PROPERTIES
 @property(nonatomic, readonly) CGAffineTransform targetTransform NS_AVAILABLE_IOS(8_0);
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIWebView.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIWebView.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIWebView.h	2016-07-14 06:20:58.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIWebView.h	2016-07-28 05:53:08.000000000 +0200
@@ -92,7 +92,7 @@
 - (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType;
 - (void)webViewDidStartLoad:(UIWebView *)webView;
 - (void)webViewDidFinishLoad:(UIWebView *)webView;
-- (void)webView:(UIWebView *)webView didFailLoadWithError:(nullable NSError *)error;
+- (void)webView:(UIWebView *)webView didFailLoadWithError:(NSError *)error;
 
 @end
 
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIWindow.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIWindow.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIWindow.h	2016-07-14 06:20:58.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UIWindow.h	2016-07-28 05:01:11.000000000 +0200
@@ -44,19 +44,19 @@
 UIKIT_EXTERN const UIWindowLevel UIWindowLevelAlert;
 UIKIT_EXTERN const UIWindowLevel UIWindowLevelStatusBar __TVOS_PROHIBITED;
 
-UIKIT_EXTERN NSString *const UIWindowDidBecomeVisibleNotification; // nil
-UIKIT_EXTERN NSString *const UIWindowDidBecomeHiddenNotification;  // nil
-UIKIT_EXTERN NSString *const UIWindowDidBecomeKeyNotification;     // nil
-UIKIT_EXTERN NSString *const UIWindowDidResignKeyNotification;     // nil
+UIKIT_EXTERN NSNotificationName const UIWindowDidBecomeVisibleNotification; // nil
+UIKIT_EXTERN NSNotificationName const UIWindowDidBecomeHiddenNotification;  // nil
+UIKIT_EXTERN NSNotificationName const UIWindowDidBecomeKeyNotification;     // nil
+UIKIT_EXTERN NSNotificationName const UIWindowDidResignKeyNotification;     // nil
 
 // Each notification includes a nil object and a userInfo dictionary containing the
 // begining and ending keyboard frame in screen coordinates. Use the various UIView and
 // UIWindow convertRect facilities to get the frame in the desired coordinate system.
 // Animation key/value pairs are only available for the "will" family of notification.
-UIKIT_EXTERN NSString *const UIKeyboardWillShowNotification __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIKeyboardDidShowNotification __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIKeyboardWillHideNotification __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIKeyboardDidHideNotification __TVOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIKeyboardWillShowNotification __TVOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIKeyboardDidShowNotification __TVOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIKeyboardWillHideNotification __TVOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIKeyboardDidHideNotification __TVOS_PROHIBITED;
 
 UIKIT_EXTERN NSString *const UIKeyboardFrameBeginUserInfoKey        NS_AVAILABLE_IOS(3_2) __TVOS_PROHIBITED; // NSValue of CGRect
 UIKIT_EXTERN NSString *const UIKeyboardFrameEndUserInfoKey          NS_AVAILABLE_IOS(3_2) __TVOS_PROHIBITED; // NSValue of CGRect
@@ -66,8 +66,8 @@
 
 // Like the standard keyboard notifications above, these additional notifications include
 // a nil object and begin/end frames of the keyboard in screen coordinates in the userInfo dictionary.
-UIKIT_EXTERN NSString *const UIKeyboardWillChangeFrameNotification  NS_AVAILABLE_IOS(5_0) __TVOS_PROHIBITED;
-UIKIT_EXTERN NSString *const UIKeyboardDidChangeFrameNotification   NS_AVAILABLE_IOS(5_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIKeyboardWillChangeFrameNotification  NS_AVAILABLE_IOS(5_0) __TVOS_PROHIBITED;
+UIKIT_EXTERN NSNotificationName const UIKeyboardDidChangeFrameNotification   NS_AVAILABLE_IOS(5_0) __TVOS_PROHIBITED;
 
 // These keys are superseded by UIKeyboardFrameBeginUserInfoKey and UIKeyboardFrameEndUserInfoKey.
 UIKIT_EXTERN NSString *const UIKeyboardCenterBeginUserInfoKey   NS_DEPRECATED_IOS(2_0, 3_2) __TVOS_PROHIBITED;

```