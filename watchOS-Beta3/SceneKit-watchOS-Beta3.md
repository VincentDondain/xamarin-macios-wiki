#SceneKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBoundingVolume.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBoundingVolume.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBoundingVolume.h	2016-06-26 08:59:07.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBoundingVolume.h	2016-07-10 12:48:58.000000000 +0200
@@ -23,7 +23,7 @@
  @param min A pointer to a SCNVector3 to store the min vertex of the bounding box into.
  @param max A pointer to a SCNVector3 to store the max vertex of the bounding box into.
  */
-- (BOOL)getBoundingBoxMin:(nullable SCNVector3 *)min max:(nullable SCNVector3 *)max;
+- (BOOL)getBoundingBoxMin:(nullable SCNVector3 *)min max:(nullable SCNVector3 *)max NS_REFINED_FOR_SWIFT;
 
 /*!
  @method setBoundingBoxMin:max:
@@ -32,7 +32,7 @@
  @param max A pointer to a SCNVector3 representing the max vertex of the desired bounding box.
  @discussion Passing nil as arguments will recompute the original bounding box of the receiver.
  */
-- (void)setBoundingBoxMin:(nullable SCNVector3 *)min max:(nullable SCNVector3 *)max API_AVAILABLE(macosx(10.9));
+- (void)setBoundingBoxMin:(nullable SCNVector3 *)min max:(nullable SCNVector3 *)max API_AVAILABLE(macosx(10.9)) NS_REFINED_FOR_SWIFT;
 
 /*!
  @method getBoundingSphereCenter:radius:
@@ -40,7 +40,7 @@
  @param center A pointer to a SCNVector3 to store the center of the bounding sphere into.
  @param radius A pointer to a CGFloat to store the radius of the bounding sphere into.
  */
-- (BOOL)getBoundingSphereCenter:(nullable SCNVector3 *)center radius:(nullable CGFloat *)radius;
+- (BOOL)getBoundingSphereCenter:(nullable SCNVector3 *)center radius:(nullable CGFloat *)radius NS_REFINED_FOR_SWIFT;
 
 @end
 

```