#UIKit.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICloudSharingController.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICloudSharingController.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICloudSharingController.h	2016-09-24 03:43:02.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/UIKit.framework/Headers/UICloudSharingController.h	2016-10-24 05:40:49.000000000 +0200
@@ -22,8 +22,9 @@
 
     UICloudSharingPermissionAllowReadOnly = 1 << 2,  // The user is allowed to grant participants read-only permissions
     UICloudSharingPermissionAllowReadWrite = 1 << 3, // The user is allowed to grant participants read/write permissions
-} NS_ENUM_AVAILABLE_IOS(10_0);
+} NS_ENUM_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED;
 
+__TVOS_PROHIBITED __WATCHOS_PROHIBITED
 @protocol UICloudSharingControllerDelegate <NSObject>
 
 - (void)cloudSharingController:(UICloudSharingController *)csc failedToSaveShareWithError:(NSError *)error;
@@ -42,7 +43,7 @@
 
 @end
 
-NS_CLASS_AVAILABLE_IOS(10_0) @interface UICloudSharingController : UIViewController
+NS_CLASS_AVAILABLE_IOS(10_0) __TVOS_PROHIBITED __WATCHOS_PROHIBITED @interface UICloudSharingController : UIViewController
 
 - (instancetype)initWithNibName:(nullable NSString *)nibNameOrNil bundle:(nullable NSBundle *)nibBundleOrNil NS_UNAVAILABLE;
 - (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_UNAVAILABLE;

```