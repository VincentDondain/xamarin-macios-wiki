#HomeKit.framework

``` diff
diff -ruN /Applications/Xcode8-GM.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshotControl.h /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshotControl.h
--- /Applications/Xcode8-GM.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshotControl.h	2016-08-13 07:35:43.000000000 +0200
+++ /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/HomeKit.framework/Headers/HMCameraSnapshotControl.h	2016-09-15 02:06:44.000000000 +0200
@@ -8,8 +8,6 @@
 #import <Foundation/Foundation.h>
 #import <HomeKit/HMCameraControl.h>
 
-#import <CoreGraphics/CoreGraphics.h>
-
 NS_ASSUME_NONNULL_BEGIN
 
 @class HMCameraSnapshot;
@@ -22,7 +20,7 @@
 @interface HMCameraSnapshotControl : HMCameraControl
 
 /*!
- * @brief Delegate that receives updates on the camera stream changes.
+ * @brief Delegate that receives updates on the camera snapshot changes.
  */
 @property(weak, nonatomic) id<HMCameraSnapshotControlDelegate> delegate;
 
@@ -33,8 +31,6 @@
 
 /*!
  * @brief Takes an image snapshot.
- *
- * @param resolution Desired video resolution of the stream. This parameter is only a suggested resolution.
  */
 - (void)takeSnapshot;
 
@@ -42,7 +38,7 @@
 
 
 /*!
- * @brief This delegate receives updates on the camera stream.
+ * @brief This delegate receives updates on the camera snapshot.
  */
 __IOS_AVAILABLE(10_0) __WATCHOS_AVAILABLE(3_0) __TVOS_AVAILABLE(10_0)
 @protocol HMCameraSnapshotControlDelegate <NSObject>
@@ -62,6 +58,13 @@
               didTakeSnapshot:(HMCameraSnapshot *__nullable)snapshot
                         error:(NSError *__nullable)error;
 
+/*!
+ * @brief Informs the delegate that the mostRecentSnapshot was updated.
+ *
+ * @param cameraStreamControl Sender of this message.
+ */
+- (void)cameraSnapshotControlDidUpdateMostRecentSnapshot:(HMCameraSnapshotControl *)cameraSnapshotControl;
+
 @end
 
 NS_ASSUME_NONNULL_END

```