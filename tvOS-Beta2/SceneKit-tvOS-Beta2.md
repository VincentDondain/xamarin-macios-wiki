#SceneKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNAnimation.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNAnimation.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNAnimation.h	2016-05-31 04:56:13.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNAnimation.h	2016-06-26 08:35:21.000000000 +0200
@@ -19,7 +19,7 @@
  @abstract SCNAnimationEvent encapsulate a block to trigger at a specific time.
  */
 
-NS_CLASS_AVAILABLE(10_9, 8_0)
+API_AVAILABLE(macosx(10.9))
 @interface SCNAnimationEvent : NSObject
 
 /*!
@@ -80,21 +80,21 @@
  @abstract Pause the animation with the given identifier.
  @param key The identifier for the animation to pause.
  */
-- (void)pauseAnimationForKey:(NSString *)key NS_AVAILABLE(10_9, 8_0);
+- (void)pauseAnimationForKey:(NSString *)key API_AVAILABLE(macosx(10.9));
 
 /*!
  @method resumeAnimationForKey:
  @abstract Resume the animation with the given identifier.
  @param key The identifier for the animation to resume.
  */
-- (void)resumeAnimationForKey:(NSString *)key NS_AVAILABLE(10_9, 8_0);
+- (void)resumeAnimationForKey:(NSString *)key API_AVAILABLE(macosx(10.9));
 
 /*!
  @method isAnimationForKeyPaused:
  @abstract Returns whether the animation for the specified identifier is paused.
  @param key The identifier for the animation to query.
  */
-- (BOOL)isAnimationForKeyPaused:(NSString *)key NS_AVAILABLE(10_9, 8_0);
+- (BOOL)isAnimationForKeyPaused:(NSString *)key API_AVAILABLE(macosx(10.9));
 
 /*!
  @method removeAnimationForKey:fadeOutDuration:
@@ -102,7 +102,7 @@
  @param key The identifier for the animation to remove.
  @param duration The fade out duration used to remove the animation.
  */
-- (void)removeAnimationForKey:(NSString *)key fadeOutDuration:(CGFloat)duration NS_AVAILABLE(10_10, 8_0);
+- (void)removeAnimationForKey:(NSString *)key fadeOutDuration:(CGFloat)duration API_AVAILABLE(macosx(10.10));
 
 /*!
  @method setSpeed:forAnimationKey:
@@ -110,7 +110,7 @@
  @param speed The new speed of the animation.
  @param key The identifier for the animation to update.
  */
-- (void)setSpeed:(CGFloat)speed forAnimationKey:(NSString *)key NS_AVAILABLE(10_12, 10_0);
+- (void)setSpeed:(CGFloat)speed forAnimationKey:(NSString *)key API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 @end
 
@@ -132,20 +132,20 @@
  @abstract Determines the receiver's fade-in duration.
  @discussion When the fadeInDuration is greater than zero, the effect of the animation progressively increase from 0% to 100% during the specified duration.
  */
-@property CGFloat fadeInDuration NS_AVAILABLE(10_9, 8_0);
+@property CGFloat fadeInDuration API_AVAILABLE(macosx(10.9));
  
 /*!
  @property fadeOutDuration
  @abstract Determines the receiver's fade-out duration.
  @discussion When the fadeOutDuration is greater than zero, the effect of the animation progressively decrease from 100% to 0% at the end of the animation duration.
  */
-@property CGFloat fadeOutDuration NS_AVAILABLE(10_9, 8_0);
+@property CGFloat fadeOutDuration API_AVAILABLE(macosx(10.9));
 
 /*!
  @property animationEvents
  @abstract Specifies the animation events attached to the receiver.
  */
-@property(nonatomic, copy, nullable) NSArray<SCNAnimationEvent *> *animationEvents NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic, copy, nullable) NSArray<SCNAnimationEvent *> *animationEvents API_AVAILABLE(macosx(10.9));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNAudioSource.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNAudioSource.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNAudioSource.h	2016-05-22 05:48:21.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNAudioSource.h	2016-06-26 09:42:49.000000000 +0200
@@ -14,7 +14,7 @@
  @class SCNAudioSource
  @abstract The SCNAudioSource class represents an audio source that can be added to a SCNNode.
  */
-NS_CLASS_AVAILABLE(10_11, 9_0)
+API_AVAILABLE(macosx(10.11), ios(9.0))
 @interface SCNAudioSource : NSObject <NSCopying, NSSecureCoding>
 
 /*!
@@ -81,7 +81,7 @@
 
 @end
 
-NS_CLASS_AVAILABLE(10_11, 9_0)
+API_AVAILABLE(macosx(10.11), ios(9.0))
 @interface SCNAudioPlayer : NSObject
 
 - (instancetype)init NS_UNAVAILABLE;
@@ -143,25 +143,25 @@
  @method addAudioPlayer:
  @abstract Add an audio player to the node and starts playing it right away.
  */
-- (void)addAudioPlayer:(SCNAudioPlayer *)player NS_AVAILABLE(10_11, 9_0);
+- (void)addAudioPlayer:(SCNAudioPlayer *)player API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @method removeAllAudioPlayers
  @abstract Remove all audio players from this node and stop playing them.
  */
-- (void)removeAllAudioPlayers NS_AVAILABLE(10_11, 9_0);
+- (void)removeAllAudioPlayers API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @method removeAudioPlayer:
  @abstract Remove the given audio player from this node and stop playing it.
  */
-- (void)removeAudioPlayer:(SCNAudioPlayer *)player NS_AVAILABLE(10_11, 9_0);
+- (void)removeAudioPlayer:(SCNAudioPlayer *)player API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @property audioPlayers
  @abstract Get an array with all the audio players connected and playing on this node.
  */
-@property(nonatomic, readonly) NSArray<SCNAudioPlayer *> *audioPlayers NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, readonly) NSArray<SCNAudioPlayer *> *audioPlayers API_AVAILABLE(macosx(10.11), ios(9.0));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBoundingVolume.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBoundingVolume.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBoundingVolume.h	2016-05-31 05:16:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBoundingVolume.h	2016-06-26 08:35:21.000000000 +0200
@@ -32,7 +32,7 @@
  @param max A pointer to a SCNVector3 representing the max vertex of the desired bounding box.
  @discussion Passing nil as arguments will recompute the original bounding box of the receiver.
  */
-- (void)setBoundingBoxMin:(nullable SCNVector3 *)min max:(nullable SCNVector3 *)max NS_AVAILABLE(10_9, 8_0);
+- (void)setBoundingBoxMin:(nullable SCNVector3 *)min max:(nullable SCNVector3 *)max API_AVAILABLE(macosx(10.9));
 
 /*!
  @method getBoundingSphereCenter:radius:
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNCamera.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNCamera.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNCamera.h	2016-05-31 04:56:13.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNCamera.h	2016-06-26 09:42:49.000000000 +0200
@@ -16,7 +16,6 @@
  @discussion A node with a camera can be used as a point of view to visualize a 3D scene.
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNCamera : NSObject <SCNAnimatable, SCNTechniqueSupport, NSCopying, NSSecureCoding>
 
 /*! 
@@ -64,7 +63,7 @@
  @abstract Determines whether the receiver automatically adjusts the zNear and zFar values. Defaults to NO.
  @discussion When set to YES, the near and far planes are automatically set to fit the bounding box of the entire scene at render time. Setting the property zNear or zFar automatically resets this property to NO.
  */
-@property(nonatomic) BOOL automaticallyAdjustsZRange NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic) BOOL automaticallyAdjustsZRange API_AVAILABLE(macosx(10.9));
 
 /*! 
  @property usesOrthographicProjection
@@ -77,7 +76,7 @@
  @abstract Determines the receiver's orthographic scale value. Animatable. Defaults to 1.
  @discussion This setting determines the size of the camera's visible area. This is only enabled when usesOrthographicProjection is set to YES.
  */
-@property(nonatomic) double orthographicScale NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic) double orthographicScale API_AVAILABLE(macosx(10.9));
 
 /*!
  @property projectionTransform
@@ -93,35 +92,35 @@
  @abstract Determines the receiver's focal distance. Animatable.
  @discussion When non zero, the focal distance determines how the camera focuses the objects in the 3d scene. Defaults to 10.0
  */
-@property(nonatomic) CGFloat focalDistance NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic) CGFloat focalDistance API_AVAILABLE(macosx(10.9));
 
 /*!
  @property focalSize
  @abstract Determines the receiver's focal size. Animatable.
  @discussion Determines the size of the area around focalDistance where the objects are in focus. Defaults to 0.
  */
-@property(nonatomic) CGFloat focalSize NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic) CGFloat focalSize API_AVAILABLE(macosx(10.9));
 
 /*!
  @property focalBlurRadius
  @abstract Determines the receiver's focal radius. Animatable.
  @discussion Determines the maximum amount of blur for objects out of focus. Defaults to 0.
  */
-@property(nonatomic) CGFloat focalBlurRadius NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic) CGFloat focalBlurRadius API_AVAILABLE(macosx(10.9));
 
 /*!
  @property aperture
  @abstract Determines the receiver's aperture. Animatable.
  @discussion Determines how fast the transition between in-focus and out-of-focus areas is. The greater the aperture is the faster the transition is. Defaults to 1/8.
  */
-@property(nonatomic) CGFloat aperture NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic) CGFloat aperture API_AVAILABLE(macosx(10.9));
 
 /*!
  @property motionBlurIntensity
  @abstract Determines the intensity of the motion blur. Animatable. Defaults to 0.
  @discussion An intensity of zero means no motion blur. The intensity should not exceeed 1.
  */
-@property(nonatomic) CGFloat motionBlurIntensity NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat motionBlurIntensity API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @functiongroup High Dynamic Range
@@ -130,121 +129,121 @@
  @property wantsHDR
  @abstract Determines if the receiver has a high dynamic range. Defaults to NO.
  */
-@property(nonatomic) BOOL wantsHDR NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) BOOL wantsHDR API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property exposureOffset
  @abstract Determines the logarithimc exposure biasing, in EV. Defaults to 0.
  */
-@property(nonatomic) CGFloat exposureOffset NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat exposureOffset API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property averageGray
  @abstract Determines the average gray level desired in the final image. Defaults to 0.18.
  */
-@property(nonatomic) CGFloat averageGray NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat averageGray API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property whitePoint
  @abstract Determines the smallest luminance level that will be mapped to white in the final image. Defaults to 1.
  */
-@property(nonatomic) CGFloat whitePoint NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat whitePoint API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property wantsExposureAdaptation
  @abstract Determines if the receiver should simulate an eye and continuously adjust to luminance. Defaults to YES.
  */
-@property(nonatomic) BOOL wantsExposureAdaptation NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) BOOL wantsExposureAdaptation API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property exposureAdaptationBrighteningSpeedFactor
  @abstract Determines the exposure adaptation speed when going from bright areas to dark areas. Defaults to 0.4.
  */
-@property(nonatomic) CGFloat exposureAdaptationBrighteningSpeedFactor NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat exposureAdaptationBrighteningSpeedFactor API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property exposureAdaptationBrighteningSpeedFactor
  @abstract Determines the exposure adaptation speed whien going from dark areas to bright areas. Defaults to 0.6.
  */
-@property(nonatomic) CGFloat exposureAdaptationDarkeningSpeedFactor NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat exposureAdaptationDarkeningSpeedFactor API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property minimumExposure
  @abstract Determines the minimum exposure offset of the adaptation, in EV. Defaults to -15.
  */
-@property(nonatomic) CGFloat minimumExposure NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat minimumExposure API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property maximumExposure
  @abstract Determines the maximum exposure offset of the adaptation, in EV. Defaults to -15.
  */
-@property(nonatomic) CGFloat maximumExposure NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat maximumExposure API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property bloomThreshold
  @abstract Determines the luminance threshold for the bloom effect. Animatable. Defaults to 1.
  */
-@property(nonatomic) CGFloat bloomThreshold NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat bloomThreshold API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property bloomIntensity
  @abstract Determines the intensity of the bloom effect. Animatable. Defaults to 0 (no effect).
  */
-@property(nonatomic) CGFloat bloomIntensity NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat bloomIntensity API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property bloomBlurRadius
  @abstract Determines the radius of the bloom effect in pixels. Animatable. Defaults to 4.
  */
-@property(nonatomic) CGFloat bloomBlurRadius NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat bloomBlurRadius API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property vignettingPower
  @abstract Controls the shape of the vignetting effect. Defaults to 0 (no effect).
  */
-@property(nonatomic) CGFloat vignettingPower NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat vignettingPower API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property vignettingIntensity
  @abstract Controls the intensity of the vignetting effect. Defaults to 0 (no effect).
  */
-@property(nonatomic) CGFloat vignettingIntensity NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat vignettingIntensity API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property colorFringeStrength
  @abstract Controls the strength of the color shift effect. Defaults to 0 (no effect).
  */
-@property(nonatomic) CGFloat colorFringeStrength NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat colorFringeStrength API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property colorFringeIntensity
  @abstract Controls the intensity of the color shift effect. Defaults to 1.
  */
-@property(nonatomic) CGFloat colorFringeIntensity NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat colorFringeIntensity API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property saturation
  @abstract Controls the overall saturation of the scene. Defaults to 1 (no effect).
  */
-@property(nonatomic) CGFloat saturation NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat saturation API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property contrast
  @abstract Controls the overall contrast of the scene. Defaults to 0 (no effect).
  */
-@property(nonatomic) CGFloat contrast NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat contrast API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property colorGrading
  @abstract Specifies a lookup texture to apply color grading. The contents must a 2D image representing `n` slices of a unit color cube texture, arranged in an horizontal row of `n` images. For instance, a color cube of dimension 16x16x16 should be provided as an image of size 256x16.
  */
-@property(nonatomic, readonly) SCNMaterialProperty *colorGrading NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic, readonly) SCNMaterialProperty *colorGrading API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property categoryBitMask
  @abstract Determines the node categories that are visible from the receiver. Defaults to all bits set.
  */
-@property(nonatomic) NSUInteger categoryBitMask NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) NSUInteger categoryBitMask API_AVAILABLE(macosx(10.10));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNConstraint.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNConstraint.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNConstraint.h	2016-05-31 04:56:13.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNConstraint.h	2016-06-26 09:09:04.000000000 +0200
@@ -16,14 +16,14 @@
  @abstract A SCNConstraint is an abstract class that represents a single constraint that can be applied to a node.
  */
 
-NS_CLASS_AVAILABLE(10_9, 8_0)
+API_AVAILABLE(macosx(10.9))
 @interface SCNConstraint : NSObject <NSCopying, NSSecureCoding, SCNAnimatable>
 
 /*!
  @property influenceFactor
  @abstract Specifies the inflence factor of the receiver. Defaults to 1. Animatable
  */
-@property(nonatomic) CGFloat influenceFactor NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) CGFloat influenceFactor API_AVAILABLE(macosx(10.10));
 
 @end
 
@@ -32,7 +32,7 @@
  @abstract A SCNLookAtConstraint applies on a node's orientation so that it always look at another node.
  */
 
-NS_CLASS_AVAILABLE(10_9, 8_0)
+API_AVAILABLE(macosx(10.9))
 @interface SCNLookAtConstraint : SCNConstraint
 
 /*!
@@ -48,7 +48,7 @@
  */
 @property(nonatomic, retain, nullable) SCNNode *target;
 - (nullable SCNNode *)target;
-- (void)setTarget:(nullable SCNNode *)target NS_AVAILABLE(10_12, 10_0);
+- (void)setTarget:(nullable SCNNode *)target API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property gimbalLockEnabled
@@ -66,7 +66,7 @@
     SCNBillboardAxisAll = SCNBillboardAxisX | SCNBillboardAxisY | SCNBillboardAxisZ
 };
 
-NS_CLASS_AVAILABLE(10_11, 9_0)
+API_AVAILABLE(macosx(10.11), ios(9.0))
 @interface SCNBillboardConstraint : SCNConstraint
 
 /*!
@@ -88,7 +88,7 @@
  @class SCNTransformConstraint
  @abstract A SCNTransformConstraint applies on the transform of a node via a custom block.
  */
-NS_CLASS_AVAILABLE(10_9, 8_0)
+API_AVAILABLE(macosx(10.9))
 @interface SCNTransformConstraint : SCNConstraint
 
 /*!
@@ -107,7 +107,7 @@
  @class SCNIKConstraint
  @abstract A SCNIKConstraint applies an inverse kinematics constraint
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10))
 @interface SCNIKConstraint : SCNConstraint
 
 /*!
@@ -116,7 +116,7 @@
  @param chainRootNode The root node of the kinematic chain.
  @discussion "chainRootNode" must be an ancestor of the node on which the constraint is applied.
  */
-- (instancetype)initWithChainRootNode:(SCNNode *)chainRootNode NS_AVAILABLE(10_11, 9_0);
+- (instancetype)initWithChainRootNode:(SCNNode *)chainRootNode API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @method inverseKinematicsConstraintWithChainRootNode:
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNGeometry.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNGeometry.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNGeometry.h	2016-05-31 05:16:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNGeometry.h	2016-06-26 09:21:12.000000000 +0200
@@ -17,12 +17,12 @@
 @protocol MTLBuffer;
 
 typedef NS_ENUM(NSInteger, SCNGeometryPrimitiveType) {
-	SCNGeometryPrimitiveTypeTriangles                              = 0,
-	SCNGeometryPrimitiveTypeTriangleStrip                          = 1,
-	SCNGeometryPrimitiveTypeLine                                   = 2,
-	SCNGeometryPrimitiveTypePoint                                  = 3,
+	SCNGeometryPrimitiveTypeTriangles                                                   = 0,
+	SCNGeometryPrimitiveTypeTriangleStrip                                               = 1,
+	SCNGeometryPrimitiveTypeLine                                                        = 2,
+	SCNGeometryPrimitiveTypePoint                                                       = 3,
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 2
-    SCNGeometryPrimitiveTypePolygon NS_ENUM_AVAILABLE(10_12, 10_0) = 4
+    SCNGeometryPrimitiveTypePolygon API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)) = 4
 #endif
 };
 
@@ -40,18 +40,17 @@
 FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticNormal;
 FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticColor;
 FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticTexcoord;
-FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticTangent NS_AVAILABLE(10_12, 10_0);
-FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticVertexCrease NS_AVAILABLE(10_10, 8_0);
-FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticEdgeCrease NS_AVAILABLE(10_10, 8_0);
-FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticBoneWeights NS_AVAILABLE(10_10, 8_0);
-FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticBoneIndices NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticTangent API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticVertexCrease API_AVAILABLE(macosx(10.10));
+FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticEdgeCrease API_AVAILABLE(macosx(10.10));
+FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticBoneWeights API_AVAILABLE(macosx(10.10));
+FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticBoneIndices API_AVAILABLE(macosx(10.10));
 
 /*!
  @class SCNGeometry
  @abstract SCNGeometry is an abstract class that represents the geometry that can be attached to a SCNNode. 
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNGeometry : NSObject <SCNAnimatable, SCNBoundingVolume, SCNShadable, NSCopying, NSSecureCoding>
 
 /*!
@@ -59,7 +58,7 @@
  @abstract Creates and returns an empty geometry object.
  @discussion An empty geometry may be used as the lowest level of detail of a geometry.
  */
-+ (instancetype)geometry NS_AVAILABLE(10_9, 8_0);
++ (instancetype)geometry API_AVAILABLE(macosx(10.9));
 
 /*!
  @property name
@@ -124,7 +123,7 @@
  @property geometrySources
  @abstract The array of geometry sources of the receiver.
  */
-@property(nonatomic, readonly) NSArray<SCNGeometrySource *> *geometrySources NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic, readonly) NSArray<SCNGeometrySource *> *geometrySources API_AVAILABLE(macosx(10.10));
 
 /*! 
  @method geometrySourcesForSemantic:
@@ -138,7 +137,7 @@
  @property geometryElements
  @abstract The array of geometry elements of the receiver.
  */
-@property(nonatomic, readonly) NSArray<SCNGeometryElement *> *geometryElements NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic, readonly) NSArray<SCNGeometryElement *> *geometryElements API_AVAILABLE(macosx(10.10));
 
 /*!
  @property geometryElementCount
@@ -157,28 +156,28 @@
  @property levelsOfDetail
  @abstract Determines the receiver's levels of detail. Defaults to nil.
  */
-@property(nonatomic, copy, nullable) NSArray<SCNLevelOfDetail *> *levelsOfDetail NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic, copy, nullable) NSArray<SCNLevelOfDetail *> *levelsOfDetail API_AVAILABLE(macosx(10.9));
 
 /*!
  @property subdivisionLevel
  @abstract Specifies the subdivision level of the receiver. Defaults to 0.
  @discussion A subdivision level of 0 means no subdivision.
  */
-@property(nonatomic) NSUInteger subdivisionLevel NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) NSUInteger subdivisionLevel API_AVAILABLE(macosx(10.10));
 
 /*!
  @property edgeCreasesElement
  @abstract Specifies the edges creases that control the subdivision. Defaults to nil.
  @discussion The primitive type of this geometry element must be SCNGeometryPrimitiveTypeLine. See subdivisionLevel above to control the level of subdivision. See edgeCreasesElement above to specify edges for edge creases.
  */
-@property(nonatomic, retain, nullable) SCNGeometryElement *edgeCreasesElement NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic, retain, nullable) SCNGeometryElement *edgeCreasesElement API_AVAILABLE(macosx(10.10));
 
 /*!
  @property edgeCreasesSource
  @abstract Specifies the crease value of the edges specified by edgeCreasesElement. Defaults to nil.
  @discussion The semantic of this geometry source must be "SCNGeometrySourceSemanticEdgeCrease". The creases values are floating values between 0 and 10, where 0 means smooth and 10 means infinitely sharp. See subdivisionLevel above to control the level of subdivision. See edgeCreasesElement above to specify edges for edge creases.
  */
-@property(nonatomic, retain, nullable) SCNGeometrySource *edgeCreasesSource NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic, retain, nullable) SCNGeometrySource *edgeCreasesSource API_AVAILABLE(macosx(10.10));
 
 @end
 
@@ -188,7 +187,6 @@
  @abstract A geometry source contains geometry data for a specific semantic. The data format is described by properties.
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNGeometrySource : NSObject <NSSecureCoding>
 
 /*! 
@@ -264,7 +262,7 @@
  }
  
  */
-+ (instancetype)geometrySourceWithBuffer:(id <MTLBuffer>)mtlBuffer vertexFormat:(MTLVertexFormat)vertexFormat semantic:(SCNGeometrySourceSemantic)semantic vertexCount:(NSInteger)vertexCount dataOffset:(NSInteger)offset dataStride:(NSInteger)stride NS_AVAILABLE(10_11, 9_0);
++ (instancetype)geometrySourceWithBuffer:(id <MTLBuffer>)mtlBuffer vertexFormat:(MTLVertexFormat)vertexFormat semantic:(SCNGeometrySourceSemantic)semantic vertexCount:(NSInteger)vertexCount dataOffset:(NSInteger)offset dataStride:(NSInteger)stride API_AVAILABLE(macosx(10.11), ios(9.0));
 #endif
 
 /*! 
@@ -323,7 +321,6 @@
  @abstract A geometry element describes how vertices from a geometry source are connected together.
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNGeometryElement : NSObject <NSSecureCoding>
 
 /*!
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNHitTest.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNHitTest.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNHitTest.h	2016-05-22 05:48:21.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNHitTest.h	2016-06-26 09:42:49.000000000 +0200
@@ -18,30 +18,29 @@
 typedef NSString * SCNHitTestOption;
 #endif
 
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionFirstFoundOnly    NS_AVAILABLE(10_12, 10_0); // If set to YES, returns the first object found. This object is not necessarily the nearest. Defaults to NO.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionSortResults       NS_AVAILABLE(10_12, 10_0); // Determines whether the results should be sorted. If set to YES sorts nearest objects first. Defaults to YES.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionClipToZRange      NS_AVAILABLE(10_12, 10_0); // If set to YES ignores the objects clipped by the zNear/zFar range of the current point of view. Defaults to YES.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionBackFaceCulling   NS_AVAILABLE(10_12, 10_0); // If set to YES ignores the faces not facing to the camera. Defaults to YES.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionBoundingBoxOnly   NS_AVAILABLE(10_12, 10_0); // If set to YES only tests the bounding boxes of the 3D objects. Defaults to NO.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionIgnoreChildNodes  NS_AVAILABLE(10_12, 10_0); // Determines whether the child nodes are ignored. Defaults to NO.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionRootNode          NS_AVAILABLE(10_12, 10_0); // Specifies the root node to use for the hit test. Defaults to the root node of the scene.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionIgnoreHiddenNodes NS_AVAILABLE(10_12, 10_0); // Determines whether hidden nodes should be ignored. Defaults to YES.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionCategoryBitMask   NS_AVAILABLE(10_12, 10_0); // Determines the node categories to test. Defaults to all bits set.
-
-FOUNDATION_EXTERN NSString * const SCNHitTestFirstFoundOnlyKey;                            // Please use SCNHitTestOption.firstFoundOnly instead.
-FOUNDATION_EXTERN NSString * const SCNHitTestSortResultsKey;                               // Please use SCNHitTestOption.sortResults instead.
-FOUNDATION_EXTERN NSString * const SCNHitTestClipToZRangeKey;                              // Please use SCNHitTestOption.clipToZRange instead.
-FOUNDATION_EXTERN NSString * const SCNHitTestBackFaceCullingKey;                           // Please use SCNHitTestOption.backFaceCulling instead.
-FOUNDATION_EXTERN NSString * const SCNHitTestBoundingBoxOnlyKey;                           // Please use SCNHitTestOption.boundingBoxOnly instead.
-FOUNDATION_EXTERN NSString * const SCNHitTestIgnoreChildNodesKey;                          // Please use SCNHitTestOption.ignoreChildNodes instead.
-FOUNDATION_EXTERN NSString * const SCNHitTestRootNodeKey;                                  // Please use SCNHitTestOption.rootNode instead.
-FOUNDATION_EXTERN NSString * const SCNHitTestIgnoreHiddenNodesKey NS_AVAILABLE(10_9, 8_0); // Please use SCNHitTestOption.ignoreHiddenNodes instead.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionFirstFoundOnly    API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // If set to YES, returns the first object found. This object is not necessarily the nearest. Defaults to NO.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionSortResults       API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Determines whether the results should be sorted. If set to YES sorts nearest objects first. Defaults to YES.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionClipToZRange      API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // If set to YES ignores the objects clipped by the zNear/zFar range of the current point of view. Defaults to YES.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionBackFaceCulling   API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // If set to YES ignores the faces not facing to the camera. Defaults to YES.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionBoundingBoxOnly   API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // If set to YES only tests the bounding boxes of the 3D objects. Defaults to NO.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionIgnoreChildNodes  API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Determines whether the child nodes are ignored. Defaults to NO.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionRootNode          API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Specifies the root node to use for the hit test. Defaults to the root node of the scene.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionIgnoreHiddenNodes API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Determines whether hidden nodes should be ignored. Defaults to YES.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionCategoryBitMask   API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Determines the node categories to test. Defaults to all bits set.
+
+FOUNDATION_EXTERN NSString * const SCNHitTestFirstFoundOnlyKey;                                // Please use SCNHitTestOption.firstFoundOnly instead.
+FOUNDATION_EXTERN NSString * const SCNHitTestSortResultsKey;                                   // Please use SCNHitTestOption.sortResults instead.
+FOUNDATION_EXTERN NSString * const SCNHitTestClipToZRangeKey;                                  // Please use SCNHitTestOption.clipToZRange instead.
+FOUNDATION_EXTERN NSString * const SCNHitTestBackFaceCullingKey;                               // Please use SCNHitTestOption.backFaceCulling instead.
+FOUNDATION_EXTERN NSString * const SCNHitTestBoundingBoxOnlyKey;                               // Please use SCNHitTestOption.boundingBoxOnly instead.
+FOUNDATION_EXTERN NSString * const SCNHitTestIgnoreChildNodesKey;                              // Please use SCNHitTestOption.ignoreChildNodes instead.
+FOUNDATION_EXTERN NSString * const SCNHitTestRootNodeKey;                                      // Please use SCNHitTestOption.rootNode instead.
+FOUNDATION_EXTERN NSString * const SCNHitTestIgnoreHiddenNodesKey API_AVAILABLE(macosx(10.9)); // Please use SCNHitTestOption.ignoreHiddenNodes instead.
 
 /*! @class SCNHitTestResult
  @abstract Results returned by the hit-test methods.
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNHitTestResult : NSObject
 
 /*! The node hit. */
@@ -69,7 +68,7 @@
 @property(nonatomic, readonly) SCNMatrix4 modelTransform;
 
 /*! The bone node hit. Only available if the node hit has a SCNSkinner attached. */
-@property(nonatomic, readonly) SCNNode *boneNode NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic, readonly) SCNNode *boneNode API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @method textureCoordinatesWithMappingChannel:
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNJavascript.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNJavascript.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNJavascript.h	2016-05-31 05:16:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNJavascript.h	2016-06-26 08:35:21.000000000 +0200
@@ -52,6 +52,6 @@
  aNode.transform = {m11:1, m12:0, m13:0 ... m44:1};
  */
 
-FOUNDATION_EXTERN void SCNExportJavaScriptModule(JSContext *context) NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN void SCNExportJavaScriptModule(JSContext *context) API_AVAILABLE(macosx(10.10));
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLevelOfDetail.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLevelOfDetail.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLevelOfDetail.h	2016-05-31 05:16:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLevelOfDetail.h	2016-06-26 08:35:21.000000000 +0200
@@ -13,7 +13,7 @@
  @class SCNLevelOfDetail
  @abstract SCNLevelOfDetail represents a level of detail of a geometry.
  */
-NS_CLASS_AVAILABLE(10_9, 8_0)
+API_AVAILABLE(macosx(10.9))
 @interface SCNLevelOfDetail : NSObject <NSCopying, NSSecureCoding>
 
 /*!
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLight.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLight.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLight.h	2016-05-31 04:56:02.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLight.h	2016-06-26 09:21:12.000000000 +0200
@@ -23,12 +23,12 @@
 typedef NSString * SCNLightType;
 #endif
 
-FOUNDATION_EXTERN SCNLightType const SCNLightTypeAmbient;                         // Ambient light
-FOUNDATION_EXTERN SCNLightType const SCNLightTypeOmni;                            // Omnidirectional light
-FOUNDATION_EXTERN SCNLightType const SCNLightTypeDirectional;                     // Directional light
-FOUNDATION_EXTERN SCNLightType const SCNLightTypeSpot;                            // Spot light
-FOUNDATION_EXTERN SCNLightType const SCNLightTypeIES NS_AVAILABLE(10_12, 10_0);   // IES light
-FOUNDATION_EXTERN SCNLightType const SCNLightTypeProbe NS_AVAILABLE(10_12, 10_0); // Light probe
+FOUNDATION_EXTERN SCNLightType const SCNLightTypeAmbient;                                                   // Ambient light
+FOUNDATION_EXTERN SCNLightType const SCNLightTypeOmni;                                                      // Omnidirectional light
+FOUNDATION_EXTERN SCNLightType const SCNLightTypeDirectional;                                               // Directional light
+FOUNDATION_EXTERN SCNLightType const SCNLightTypeSpot;                                                      // Spot light
+FOUNDATION_EXTERN SCNLightType const SCNLightTypeIES API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));   // IES light
+FOUNDATION_EXTERN SCNLightType const SCNLightTypeProbe API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Light probe
 
 /*! @enum SCNShadowMode
  @abstract The different modes available to compute shadows.
@@ -40,14 +40,13 @@
     SCNShadowModeForward   = 0,
     SCNShadowModeDeferred  = 1,
     SCNShadowModeModulated = 2
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10));
 
 /*!
  @class SCNLight
  @abstract SCNLight represents a light that can be attached to a SCNNode. 
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNLight : NSObject <SCNAnimatable, SCNTechniqueSupport, NSCopying, NSSecureCoding>
 
 /*! 
@@ -59,7 +58,7 @@
 /*! 
  @property type
  @abstract Specifies the receiver's type.
- @discussion Defaults to SCNLightTypeOmni on iOS 8 and later, and on OSX 10.10 and later (otherwise defaults to SCNLightTypeAmbient).
+ @discussion Defaults to SCNLightTypeOmni on iOS 8 and later, and on macOS 10.10 and later (otherwise defaults to SCNLightTypeAmbient).
  */
 @property(nonatomic, copy) SCNLightType type;
 
@@ -75,14 +74,14 @@
  @abstract Specifies the receiver's temperature.
  @discussion This specifies the temperature of the light in Kelvin. The renderer multiplies the light's color by the color derived from the light's temperature. Defaults to 6500 (pure white). Animatable.
  */
-@property(nonatomic) CGFloat temperature NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat temperature API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property intensity
  @abstract Specifies the receiver's intensity.
  @discussion This intensity is used to modulate the light color. When used with a physically-based material, this corresponds to the luminous flux of the light, expressed in lumens (lm). Defaults to 1000. Animatable.
  */
-@property(nonatomic) CGFloat intensity NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) CGFloat intensity API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property name
@@ -103,7 +102,7 @@
 /*! 
  @property shadowColor
  @abstract Specifies the color (CGColorRef or NSColor) of the shadow casted by the receiver. Defaults to black. Animatable.
- @discussion on iOS9 / OS X 10.11 or earlier, this defaults to black 50% transparent.
+ @discussion on iOS 9 / macOS 10.11 or earlier, this defaults to black 50% transparent.
  */
 @property(nonatomic, retain) id shadowColor;
 
@@ -118,27 +117,27 @@
  @abstract Specifies the size of the shadow map.
  @discussion The larger the shadow map is the more precise the shadows are but the slower the computation is. If set to {0,0} the size of the shadow map is automatically chosen. Defaults to {0,0}.
  */
-@property(nonatomic) CGSize shadowMapSize NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) CGSize shadowMapSize API_AVAILABLE(macosx(10.10));
 
 /*!
  @property shadowSampleCount
  @abstract Specifies the number of sample per fragment to compute the shadow map. Defaults to 0.
- @discussion on OS X 10.11 or lower, the shadowSampleCount defaults to 16. On iOS 9.0 or lower it defaults to 1.0.
- On OS X 10.12, iOS 10.0 and greater, when the shadowSampleCount is set to 0, a default sample count is chosen depending on the platform.
+ @discussion on macOS 10.11 or lower, the shadowSampleCount defaults to 16. On iOS 9 or lower it defaults to 1.0.
+ On macOS 10.12, iOS 10 and greater, when the shadowSampleCount is set to 0, a default sample count is chosen depending on the platform.
  */
-@property(nonatomic) NSUInteger shadowSampleCount NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) NSUInteger shadowSampleCount API_AVAILABLE(macosx(10.10));
 
 /*!
  @property shadowMode
  @abstract Specified the mode to use to cast shadows. See above for the available modes and their description. Defaults to SCNShadowModeForward.
  */
-@property(nonatomic) SCNShadowMode shadowMode NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) SCNShadowMode shadowMode API_AVAILABLE(macosx(10.10));
 
 /*!
  @property shadowBias
  @abstrat Specifies the correction to apply to the shadow map to correct acne artefacts. It is multiplied by an implementation-specific value to create a constant depth offset. Defaults to 1.0
  */
-@property(nonatomic) CGFloat shadowBias NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) CGFloat shadowBias API_AVAILABLE(macosx(10.10));
 
 
 #pragma mark - Light projection settings for shadows
@@ -148,19 +147,19 @@
  @abstract Specifies the orthographic scale used to render from the directional light into the shadow map. Defaults to 1.
  @discussion This is only applicable for directional lights.
  */
-@property(nonatomic) CGFloat orthographicScale NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) CGFloat orthographicScale API_AVAILABLE(macosx(10.10));
 
 /*!
  @property zNear
  @abstract Specifies the minimal distance between the light and the surface to cast shadow on.  If a surface is closer to the light than this minimal distance, then the surface won't be shadowed. The near value must be different than zero. Animatable. Defaults to 1.
  */
-@property(nonatomic) CGFloat zNear NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) CGFloat zNear API_AVAILABLE(macosx(10.10));
 
 /*!
  @property zFar
  @abstract Specifies the maximal distance between the light and a visible surface to cast shadow on. If a surface is further from the light than this maximal distance, then the surface won't be shadowed. Animatable. Defaults to 100.
  */
-@property(nonatomic) CGFloat zFar NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) CGFloat zFar API_AVAILABLE(macosx(10.10));
 
 
 #pragma mark - Attenuation
@@ -169,19 +168,19 @@
  @property attenuationStartDistance
  @abstract The distance at which the attenuation starts (Omni or Spot light types only). Animatable. Defaults to 0.
  */
-@property(nonatomic) CGFloat attenuationStartDistance NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) CGFloat attenuationStartDistance API_AVAILABLE(macosx(10.10));
 
 /*!
  @property attenuationEndDistance
  @abstract The distance at which the attenuation ends (Omni or Spot light types only). Animatable. Defaults to 0.
  */
-@property(nonatomic) CGFloat attenuationEndDistance NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) CGFloat attenuationEndDistance API_AVAILABLE(macosx(10.10));
 
 /*!
  @property attenuationFalloffExponent
  @abstract Specifies the attenuation between the start and end attenuation distances. 0 means a constant attenuation, 1 a linear attenuation and 2 a quadratic attenuation, but any positive value will work (Omni or Spot light types only). Animatable. Defaults to 2.
  */
-@property(nonatomic) CGFloat attenuationFalloffExponent NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) CGFloat attenuationFalloffExponent API_AVAILABLE(macosx(10.10));
 
 
 #pragma mark - Spot parameters
@@ -190,13 +189,13 @@
  @property spotInnerAngle
  @abstract The angle in degrees between the spot direction and the lit element below which the lighting is at full strength. Animatable. Defaults to 0.
  */
-@property(nonatomic) CGFloat spotInnerAngle  NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) CGFloat spotInnerAngle  API_AVAILABLE(macosx(10.10));
 
 /*!
  @property spotOuterAngle
  @abstract The angle in degrees between the spot direction and the lit element after which the lighting is at zero strength. Animatable. Defaults to 45 degrees.
  */
-@property(nonatomic) CGFloat spotOuterAngle  NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) CGFloat spotOuterAngle  API_AVAILABLE(macosx(10.10));
 
 
 #pragma mark - Other
@@ -206,19 +205,19 @@
  @abstract Specifies the gobo (or "cookie") of the light, used to control the shape of emitted light. Defaults to nil.
  @discussion Gobos are only supported by spot lights.
  */
-@property(nonatomic, readonly, nullable) SCNMaterialProperty *gobo NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic, readonly, nullable) SCNMaterialProperty *gobo API_AVAILABLE(macosx(10.9));
 
 /*!
  @property IESProfileURL
  @abstract Specifies the IES file from which the shape, direction, and intensity of illumination is determined. Defaults to nil.
  */
-@property(nonatomic, retain, nullable) NSURL *IESProfileURL NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic, retain, nullable) NSURL *IESProfileURL API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property categoryBitMask
  @abstract Determines the node categories that will be lit by the receiver. Defaults to all bit set.
  */
-@property(nonatomic) NSUInteger categoryBitMask NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) NSUInteger categoryBitMask API_AVAILABLE(macosx(10.10));
 
 
 @end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterial.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterial.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterial.h	2016-05-22 05:48:21.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterial.h	2016-06-26 09:42:49.000000000 +0200
@@ -88,7 +88,7 @@
 FOUNDATION_EXTERN SCNLightingModel const SCNLightingModelBlinn;
 FOUNDATION_EXTERN SCNLightingModel const SCNLightingModelLambert;
 FOUNDATION_EXTERN SCNLightingModel const SCNLightingModelConstant;
-FOUNDATION_EXTERN SCNLightingModel const SCNLightingModelPhysicallyBased NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNLightingModel const SCNLightingModelPhysicallyBased API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 typedef NS_ENUM(NSInteger, SCNCullMode) {
 	SCNCullModeBack  = 0,
@@ -114,7 +114,7 @@
     SCNBlendModeMultiply     = 3, // Blends the source and destination colors by multiplying them.
     SCNBlendModeScreen       = 4, // Blends the source and destination colors by multiplying one minus the source with the destination and adding the source.
     SCNBlendModeReplace      = 5  // Replaces the destination with the source (ignores alpha).
-} NS_ENUM_AVAILABLE(10_11, 9_0);
+} API_AVAILABLE(macosx(10.11), ios(9.0));
 
 @class SCNMaterialProperty;
 @class SCNProgram;
@@ -126,7 +126,6 @@
  @abstract A SCNMaterial determines how a geometry is rendered. It encapsulates the colors and textures that define the appearance of 3d geometries.
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNMaterial : NSObject <SCNAnimatable, SCNShadable, NSCopying, NSSecureCoding>
 
 /*! 
@@ -197,25 +196,25 @@
  @property ambientOcclusion
  @abstract The ambientOcclusion property specifies the ambient occlusion of the surface. The ambient occlusion is multiplied with the ambient light, then the result is added to the lighting contribution. This property has no visual impact on scenes that have no ambient light. When an ambient occlusion map is set, the ambient property is ignored.
  */
-@property(nonatomic, readonly) SCNMaterialProperty *ambientOcclusion NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, readonly) SCNMaterialProperty *ambientOcclusion API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @property selfIllumination
  @abstract The selfIllumination property specifies a texture or a color that is added to the lighting contribution of the surface. When a selfIllumination is set, the emission property is ignored.
  */
-@property(nonatomic, readonly) SCNMaterialProperty *selfIllumination NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, readonly) SCNMaterialProperty *selfIllumination API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @property metalness
  @abstract The metalness property specifies how metallic the material's surface appears. Lower values (darker colors) cause the material to appear more like a dielectric surface. Higher values (brighter colors) cause the surface to appear more metallic. This property is only used when 'lightingModelName' is 'SCNLightingModelPhysicallyBased'.
  */
-@property(nonatomic, readonly) SCNMaterialProperty *metalness NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic, readonly) SCNMaterialProperty *metalness API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property roughness
  @abstract The roughness property specifies the apparent smoothness of the surface. Lower values (darker colors) cause the material to appear shiny, with well-defined specular highlights. Higher values (brighter colors) cause specular highlights to spread out and the diffuse property of the material to become more retroreflective. This property is only used when 'lightingModelName' is 'SCNLightingModelPhysicallyBased'.
  */
-@property(nonatomic, readonly) SCNMaterialProperty *roughness NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic, readonly) SCNMaterialProperty *roughness API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*! 
  @property shininess
@@ -278,20 +277,20 @@
  @property readsFromDepthBuffer
  @abstract Determines whether the receiver reads from the depth buffer when rendered. Defaults to YES.
  */
-@property(nonatomic) BOOL readsFromDepthBuffer NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic) BOOL readsFromDepthBuffer API_AVAILABLE(macosx(10.9));
 
 /*!
  @property fresnelExponent
  @abstract Specifies the receiver's fresnel exponent value. Defaults to 0.0. Animatable.
  @discussion The effect of the reflectivity property is modulated by this property. The fresnelExponent changes the exponent of the reflectance. The bigger the exponent, the more concentrated the reflection is around the edges.
  */
-@property(nonatomic) CGFloat fresnelExponent NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic) CGFloat fresnelExponent API_AVAILABLE(macosx(10.9));
 
 /*!
  @property blendMode
  @abstract Specifies the receiver's blend mode. Defaults to SCNBlendModeAlpha.
  */
-@property(nonatomic) SCNBlendMode blendMode NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic) SCNBlendMode blendMode API_AVAILABLE(macosx(10.11), ios(9.0));
 
 @end
     
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterialProperty.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterialProperty.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterialProperty.h	2016-05-22 05:48:16.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterialProperty.h	2016-06-26 09:21:12.000000000 +0200
@@ -16,7 +16,7 @@
     SCNFilterModeNone    = 0,
     SCNFilterModeNearest = 1,
     SCNFilterModeLinear  = 2
-} NS_ENUM_AVAILABLE(10_9, 8_0);
+} API_AVAILABLE(macosx(10.9));
 
 /*! @enum SCNWrapeMode
  @abstract Wrap modes
@@ -26,25 +26,24 @@
     SCNWrapModeRepeat        = 2,
     SCNWrapModeClampToBorder = 3,
     SCNWrapModeMirror        = 4
-} NS_ENUM_AVAILABLE(10_9, 8_0);
+} API_AVAILABLE(macosx(10.9));
 
 /*! @class SCNMaterialProperty
     @abstract The contents of a SCNMaterial slot
     @discussion This can be used to specify the various properties of SCNMaterial slots such as diffuse, ambient, etc.
 */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNMaterialProperty : NSObject <SCNAnimatable, NSSecureCoding>
 
 /*!
  @method materialPropertyWithContents:
  @abstract Creates and initialize a property instance with the specified contents.
  */
-+ (instancetype)materialPropertyWithContents:(id)contents NS_AVAILABLE(10_9, 8_0);
++ (instancetype)materialPropertyWithContents:(id)contents API_AVAILABLE(macosx(10.9));
 
 /*! 
  @property contents
- @abstract Specifies the receiver's contents. This can be a color (NSColor, UIColor, CGColorRef), an image (NSImage, UIImage, CGImageRef), a layer (CALayer), a path (NSString or NSURL), a SpriteKit scene (SKScene) or a texture (SKTexture, id<MTLTexture> or GLKTextureInfo). Animatable when set to a color.
+ @abstract Specifies the receiver's contents. This can be a color (NSColor, UIColor, CGColorRef), an image (NSImage, UIImage, CGImageRef), a layer (CALayer), a path (NSString or NSURL), a SpriteKit scene (SKScene), a texture (SKTexture, id<MTLTexture> or GLKTextureInfo), or a floating value between 0 and 1 (NSNumber) for metalness and roughness properties. Animatable when set to a color.
  @discussion Setting the contents to an instance of SKTexture will automatically update the wrapS, wrapT, contentsTransform, minification, magnification and mip filters according to the SKTexture settings.
              When a cube map is expected (e.g. SCNMaterial.reflective, SCNScene.background, SCNScene.lightingEnvironment) you can use
                1. A horizontal strip image  where `6 * image.height ==     image.width`
@@ -62,7 +61,7 @@
  It dims the diffuse, specular and emission properties, it varies the bumpiness of the normal property and the
  filter property is blended with white. Default value is 1.0. Animatable.
  */
-@property(nonatomic) CGFloat intensity NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic) CGFloat intensity API_AVAILABLE(macosx(10.9));
 
 /*! 
  @property minificationFilter
@@ -81,7 +80,7 @@
 /*! 
  @property mipFilter
  @abstract Specifies the mipmap filter to use during minification.
- @discussion Defaults to SCNFilterModeNone on OS X 10.11 and iOS 9 or earlier, SCNFilterModeNearest starting in OS X 10.12 and iOS 10.
+ @discussion Defaults to SCNFilterModeNone on macOS 10.11 and iOS 9 or earlier, SCNFilterModeNearest starting in macOS 10.12 and iOS 10.
  */
 @property(nonatomic) SCNFilterMode mipFilter;
 
@@ -108,7 +107,7 @@
  @abstract Determines the receiver's border color (CGColorRef or UIColor). Animatable.
  @discussion The border color is ignored on iOS and is always considered as clear color (0,0,0,0) when the texture has an alpha channel and opaque back (0,0,0,1) otherwise.
  */
-@property(nonatomic, retain, nullable) id borderColor NS_DEPRECATED(10_7, 10_12, 8_0, 10_0) __WATCHOS_UNAVAILABLE;
+@property(nonatomic, retain, nullable) id borderColor API_DEPRECATED("Deprecated", macosx(10.8, 10.12), ios(8.0, 10.0)) API_UNAVAILABLE(watchos, tvos);
 
 /*! 
  @property mappingChannel
@@ -122,7 +121,7 @@
  @abstract Specifies the receiver's max anisotropy. Defaults to 1.0.
  @discussion Anisotropic filtering reduces blur and preserves detail at extreme viewing angles.
  */
-@property(nonatomic) CGFloat maxAnisotropy NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic) CGFloat maxAnisotropy API_AVAILABLE(macosx(10.9));
 
 @end
     
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMorpher.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMorpher.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMorpher.h	2016-05-31 05:16:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMorpher.h	2016-06-26 08:35:21.000000000 +0200
@@ -21,7 +21,7 @@
     SCNMorpherCalculationModeAdditive   = 1  // BaseMesh + w0 * Target0 + w1 * Target1 + ...
 };
 
-NS_CLASS_AVAILABLE(10_9, 8_0)
+API_AVAILABLE(macosx(10.9))
 @interface SCNMorpher : NSObject <SCNAnimatable, NSSecureCoding>
 
 /*!
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNNode.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNNode.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNNode.h	2016-05-31 05:16:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNNode.h	2016-06-26 08:35:21.000000000 +0200
@@ -30,12 +30,12 @@
 typedef NSString * SCNTransformSemantic;
 #endif
 
-FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticModel NS_AVAILABLE(10_12, 10_0);
-FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticView NS_AVAILABLE(10_12, 10_0);
-FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticProjection NS_AVAILABLE(10_12, 10_0);
-FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticNormal NS_AVAILABLE(10_12, 10_0);
-FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticModelView NS_AVAILABLE(10_12, 10_0);
-FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticModelViewProjection NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticModel API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticView API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticProjection API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticNormal API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticModelView API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticModelViewProjection API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*! @group Rendering arguments
     @discussion These keys are used for the 'semantic' argument of -[SCNProgram setSemantic:forSymbol:options:]
@@ -56,7 +56,7 @@
 typedef NS_ENUM(NSInteger, SCNMovabilityHint) {
     SCNMovabilityHintFixed,
     SCNMovabilityHintMovable,
-} NS_ENUM_AVAILABLE(10_12, 10_0);
+} API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @class SCNNode
@@ -65,7 +65,6 @@
 		     The coordinate systems of all the sub-nodes are relative to the one of their parent node.
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNNode : NSObject <NSCopying, NSSecureCoding, SCNAnimatable, SCNActionable, SCNBoundingVolume>
 
 #pragma mark - Creating a Node
@@ -102,7 +101,7 @@
  @abstract Returns a clone of the node containing a geometry that concatenates all the geometries contained in the node hierarchy.
  The returned clone is autoreleased.
  */
-- (instancetype)flattenedClone NS_AVAILABLE(10_9, 8_0);
+- (instancetype)flattenedClone API_AVAILABLE(macosx(10.9));
 
 
 
@@ -137,13 +136,13 @@
  @property skinner
  @abstract Returns the skinner attached to the receiver.
  */
-@property(nonatomic, retain, nullable) SCNSkinner *skinner NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic, retain, nullable) SCNSkinner *skinner API_AVAILABLE(macosx(10.9));
 
 /*!
  @property morpher
  @abstract Returns the morpher attached to the receiver.
  */
-@property(nonatomic, retain, nullable) SCNMorpher *morpher NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic, retain, nullable) SCNMorpher *morpher API_AVAILABLE(macosx(10.9));
 
 
 
@@ -173,7 +172,7 @@
  @property orientation
  @abstract Determines the receiver's orientation as a unit quaternion. Animatable.
  */
-@property(nonatomic) SCNQuaternion orientation NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) SCNQuaternion orientation API_AVAILABLE(macosx(10.10));
 
 /*!
  @property eulerAngles
@@ -187,7 +186,7 @@
                2. then yaw
                3. then pitch
  */
-@property(nonatomic) SCNVector3 eulerAngles NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) SCNVector3 eulerAngles API_AVAILABLE(macosx(10.10));
 
 /*! 
  @property scale
@@ -235,13 +234,13 @@
  @property castsShadow
  @abstract Determines if the node is rendered in shadow maps. Defaults to YES.
  */
-@property(nonatomic) BOOL castsShadow NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) BOOL castsShadow API_AVAILABLE(macosx(10.10));
 
 /*!
  @property movabilityHint
  @abstract Give hints oregarding the movability of the receiver. See enum above for details. Defaults to SCNMovabilityHintFixed.
  */
-@property (nonatomic) SCNMovabilityHint movabilityHint NS_AVAILABLE(10_12, 10_0);
+@property (nonatomic) SCNMovabilityHint movabilityHint API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 
 #pragma mark - Managing the Node Hierarchy
@@ -307,7 +306,7 @@
  @discussion The search is recursive and uses a pre-order tree traversal.
  @param predicate The block to apply to child nodes of the receiver. The block takes two arguments: "child" is a child node and "stop" is a reference to a Boolean value. The block can set the value to YES to stop further processing of the node hierarchy. The stop argument is an out-only argument. You should only ever set this Boolean to YES within the Block. The Block returns a Boolean value that indicates whether "child" passed the test.
  */
-- (NSArray<SCNNode *> *)childNodesPassingTest:(__attribute__((noescape)) BOOL (^)(SCNNode *child, BOOL *stop))predicate;
+- (NSArray<SCNNode *> *)childNodesPassingTest:(NS_NOESCAPE BOOL (^)(SCNNode *child, BOOL *stop))predicate;
 
 /*!
  @method enumerateChildNodesUsingBlock:
@@ -315,7 +314,7 @@
  @discussion The search is recursive and uses a pre-order tree traversal.
  @param block The block to apply to child nodes of the receiver. The block takes two arguments: "child" is a child node and "stop" is a reference to a Boolean value. The block can set the value to YES to stop further processing of the node hierarchy. The stop argument is an out-only argument. You should only ever set this Boolean to YES within the Block.
  */
-- (void)enumerateChildNodesUsingBlock:(__attribute__((noescape)) void (^)(SCNNode *child, BOOL *stop))block NS_AVAILABLE(10_10, 8_0);
+- (void)enumerateChildNodesUsingBlock:(NS_NOESCAPE void (^)(SCNNode *child, BOOL *stop))block API_AVAILABLE(macosx(10.10));
 
 /*!
  @method enumerateHierarchyUsingBlock:
@@ -323,7 +322,7 @@
  @discussion The search is recursive and uses a pre-order tree traversal.
  @param block The block to apply to the receiver and its child nodes. The block takes two arguments: "node" is a node in the hierarchy of the receiver (including the receiver) and "stop" is a reference to a Boolean value. The block can set the value to YES to stop further processing of the node hierarchy. The stop argument is an out-only argument. You should only ever set this Boolean to YES within the Block.
  */
-- (void)enumerateHierarchyUsingBlock:(__attribute__((noescape)) void (^)(SCNNode *node, BOOL *stop))block NS_AVAILABLE(10_12, 10_0);
+- (void)enumerateHierarchyUsingBlock:(NS_NOESCAPE void (^)(SCNNode *node, BOOL *stop))block API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 
 #pragma mark - Converting Between Node Coordinate Systems
@@ -334,7 +333,7 @@
  @param position A position specified in the local coordinate system of the receiver.
  @param node The node into whose coordinate system "position" is to be converted. If "node" is nil, this method instead converts to world coordinates.
  */
-- (SCNVector3)convertPosition:(SCNVector3)position toNode:(nullable SCNNode *)node NS_AVAILABLE(10_9, 8_0);
+- (SCNVector3)convertPosition:(SCNVector3)position toNode:(nullable SCNNode *)node API_AVAILABLE(macosx(10.9));
 
 /*!
  @method convertPosition:fromNode:
@@ -342,7 +341,7 @@
  @param position A position specified in the local coordinate system of "node".
  @param node The node from whose coordinate system "position" is to be converted. If "node" is nil, this method instead converts from world coordinates.
  */
-- (SCNVector3)convertPosition:(SCNVector3)position fromNode:(nullable SCNNode *)node NS_AVAILABLE(10_9, 8_0);
+- (SCNVector3)convertPosition:(SCNVector3)position fromNode:(nullable SCNNode *)node API_AVAILABLE(macosx(10.9));
 
 /*!
  @method convertTransform:toNode:
@@ -350,7 +349,7 @@
  @param transform A transform specified in the local coordinate system of the receiver.
  @param node The node into whose coordinate system "transform" is to be converted. If "node" is nil, this method instead converts to world coordinates.
  */
-- (SCNMatrix4)convertTransform:(SCNMatrix4)transform toNode:(nullable SCNNode *)node NS_AVAILABLE(10_9, 8_0);
+- (SCNMatrix4)convertTransform:(SCNMatrix4)transform toNode:(nullable SCNNode *)node API_AVAILABLE(macosx(10.9));
 
 /*!
  @method convertTransform:fromNode:
@@ -358,7 +357,7 @@
  @param transform A transform specified in the local coordinate system of "node".
  @param node The node from whose coordinate system "transform" is to be converted. If "node" is nil, this method instead converts from world coordinates.
  */
-- (SCNMatrix4)convertTransform:(SCNMatrix4)transform fromNode:(nullable SCNNode *)node NS_AVAILABLE(10_9, 8_0);
+- (SCNMatrix4)convertTransform:(SCNMatrix4)transform fromNode:(nullable SCNNode *)node API_AVAILABLE(macosx(10.9));
 
 
 #pragma mark - Managing the SCNNode′s physics body
@@ -368,7 +367,7 @@
  @abstract The description of the physics body of the receiver.
  @discussion Default is nil.
  */
-@property(nonatomic, retain, nullable) SCNPhysicsBody *physicsBody NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic, retain, nullable) SCNPhysicsBody *physicsBody API_AVAILABLE(macosx(10.10));
 
 
 #pragma mark - Managing the Node′s Physics Field
@@ -378,7 +377,7 @@
  @abstract The description of the physics field of the receiver.
  @discussion Default is nil.
  */
-@property(nonatomic, retain, nullable) SCNPhysicsField *physicsField NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic, retain, nullable) SCNPhysicsField *physicsField API_AVAILABLE(macosx(10.10));
 
 
 #pragma mark - Managing the Node′s Constraints
@@ -388,7 +387,7 @@
  @abstract An array of SCNConstraint that are applied to the receiver.
  @discussion Adding or removing a constraint can be implicitly animated based on the current transaction.
  */
-@property(copy, nullable) NSArray<SCNConstraint *> *constraints NS_AVAILABLE(10_9, 8_0);
+@property(copy, nullable) NSArray<SCNConstraint *> *constraints API_AVAILABLE(macosx(10.9));
 
 
 #pragma mark - Accessing the Node′s Filters
@@ -398,7 +397,7 @@
  @abstract An array of Core Image filters that are applied to the rendering of the receiver and its child nodes. Animatable.
  @discussion Defaults to nil. Filter properties should be modified by calling setValue:forKeyPath: on each node that the filter is attached to. If the inputs of the filter are modified directly after the filter is attached to a node, the behavior is undefined.
  */
-@property(nonatomic, copy, nullable) NSArray<CIFilter *> *filters NS_AVAILABLE(10_9, 8_0) __WATCHOS_PROHIBITED;
+@property(nonatomic, copy, nullable) NSArray<CIFilter *> *filters API_AVAILABLE(macosx(10.9)) __WATCHOS_PROHIBITED;
 
 
 #pragma mark - Accessing the Presentation Node
@@ -419,7 +418,7 @@
  @property paused
  @abstract Controls whether or not the node's actions and animations are updated or paused. Defaults to NO.
  */
-@property(nonatomic, getter=isPaused) BOOL paused NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic, getter=isPaused) BOOL paused API_AVAILABLE(macosx(10.10));
 
 
 #pragma mark - Overriding the Rendering with Custom OpenGL Code
@@ -445,7 +444,7 @@
  @param options Optional parameters (see the "Hit test options" section in SCNSceneRenderer.h for the available options).
  @discussion See SCNSceneRenderer.h for a screen-space hit testing method.
  */
-- (NSArray<SCNHitTestResult *> *)hitTestWithSegmentFromPoint:(SCNVector3)pointA toPoint:(SCNVector3)pointB options:(nullable NSDictionary<NSString *, id> *)options NS_AVAILABLE(10_9, 8_0);
+- (NSArray<SCNHitTestResult *> *)hitTestWithSegmentFromPoint:(SCNVector3)pointA toPoint:(SCNVector3)pointB options:(nullable NSDictionary<NSString *, id> *)options API_AVAILABLE(macosx(10.9));
 
 
 #pragma mark - Categories
@@ -458,7 +457,7 @@
                 2. include/exclude nodes from render passes (see SCNTechnique.h)
                 3. specify which nodes to use when hit-testing (see SCNHitTestOptionCategoryBitMask)
  */
-@property(nonatomic) NSUInteger categoryBitMask NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) NSUInteger categoryBitMask API_AVAILABLE(macosx(10.10));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParametricGeometry.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParametricGeometry.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParametricGeometry.h	2016-05-31 05:16:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParametricGeometry.h	2016-06-26 08:39:20.000000000 +0200
@@ -17,7 +17,6 @@
  @abstract SCNPlane represents a rectangle with controllable width and height. The plane has one visible side.
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNPlane : SCNGeometry
 
 /*!
@@ -61,14 +60,14 @@
  @abstract The corner radius. Animatable.
  @discussion If the value is strictly less than 0, the geometry is empty. The default value is 0.
  */
-@property(nonatomic) CGFloat cornerRadius NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic) CGFloat cornerRadius API_AVAILABLE(macosx(10.9));
 
 /*!
  @property cornerSegmentCount
  @abstract The number of subdivisions for the rounded corners. Animatable.
  @discussion If the value is less than 1, the behavior is undefined. The default value is 10.
  */
-@property(nonatomic) NSInteger cornerSegmentCount NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic) NSInteger cornerSegmentCount API_AVAILABLE(macosx(10.9));
 
 @end
 
@@ -78,7 +77,6 @@
  @abstract SCNBox represents a box with rectangular sides and optional chamfers.
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNBox : SCNGeometry
 
 /*!
@@ -155,7 +153,6 @@
  @abstract SCNPyramid represents a right pyramid with a rectangular base.
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNPyramid : SCNGeometry
 
 /*!
@@ -217,7 +214,6 @@
  @abstract SCNSphere represents a sphere with controllable radius
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNSphere : SCNGeometry
 
 /*!
@@ -256,7 +252,6 @@
  @abstract SCNCylinder represents a cylinder with controllable height and radius.
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNCylinder : SCNGeometry
 
 /*!
@@ -303,7 +298,6 @@
  @abstract SCNCone represents a cone with controllable height, top radius and bottom radius.
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNCone : SCNGeometry
 
 /*!
@@ -358,7 +352,6 @@
  @abstract SCNTube represents a tube with controllable height, inner radius and outer radius.
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNTube : SCNGeometry
 
 /*!
@@ -413,7 +406,6 @@
  @abstract SCNCapsule represents a capsule with controllable height and cap radius.
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNCapsule : SCNGeometry
 
 /*!
@@ -467,7 +459,6 @@
  @abstract SCNTorus represents a torus with controllable ring radius and pipe radius.
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNTorus : SCNGeometry
 
 /*!
@@ -514,7 +505,6 @@
  @abstract SCNFloor represents an infinite plane geometry. 
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNFloor : SCNGeometry 
 
 /*!
@@ -549,7 +539,7 @@
  @property reflectionCategoryBitMask
  @abstract Determines the node categories to reflect. Defaults to all bits set.
  */
-@property(nonatomic) NSUInteger reflectionCategoryBitMask NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic) NSUInteger reflectionCategoryBitMask API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @property width
@@ -559,11 +549,11 @@
 @property(nonatomic) CGFloat width;
 
 /*!
- @property height
- @abstract The floor extent along the Y axis. Animatable.
- @discussion If the value is equal to 0, the floor is infinite on the Y axis. The default value is 0.
+ @property length
+ @abstract The floor extent along the Z axis. Animatable.
+ @discussion If the value is equal to 0, the floor is infinite on the Z axis. The default value is 0.
  */
-@property(nonatomic) CGFloat height;
+@property(nonatomic) CGFloat length;
 
 
 /*!
@@ -572,7 +562,7 @@
  @discussion Defaults to 0.5.
 #endif
 */
-@property(nonatomic) CGFloat reflectionResolutionScaleFactor NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) CGFloat reflectionResolutionScaleFactor API_AVAILABLE(macosx(10.10));
 
 @end
 
@@ -581,7 +571,6 @@
  @abstract SCNText represents a block of text that has been extruded
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNText : SCNGeometry 
 
 /*!
@@ -660,7 +649,7 @@
  @abstract Specifies the accuracy (or smoothness) with which fonts are rendered.
  @discussion Smaller numbers give smoother curves at the expense of more computation and heavier geometries in terms of vertices. The default value is 1.0, which yields smooth curves.
  */
-@property(nonatomic) CGFloat flatness NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic) CGFloat flatness API_AVAILABLE(macosx(10.9));
 
 @end
 
@@ -673,9 +662,9 @@
     SCNChamferModeBoth,
     SCNChamferModeFront,
     SCNChamferModeBack
-} NS_ENUM_AVAILABLE(10_9, 8_0);
+} API_AVAILABLE(macosx(10.9));
 
-NS_CLASS_AVAILABLE(10_9, 8_0)
+API_AVAILABLE(macosx(10.9))
 @interface SCNShape : SCNGeometry
 
 /*!
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParticleSystem.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParticleSystem.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParticleSystem.h	2016-05-22 05:48:21.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParticleSystem.h	2016-06-26 08:39:20.000000000 +0200
@@ -19,25 +19,25 @@
 typedef NSString * SCNParticleProperty;
 #endif
 
-FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyPosition NS_AVAILABLE(10_10, 8_0);        // float3 : {x,y,z}     controller animation type : {NSValue(SCNVector3)}
-FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyAngle NS_AVAILABLE(10_10, 8_0);           // float                controller animation type : {NSNumber}
-FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyRotationAxis NS_AVAILABLE(10_10, 8_0);    // float3 : {x,y,z}     controller animation type : {NSValue(SCNVector3)}
-FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyVelocity NS_AVAILABLE(10_10, 8_0);        // float3 : {x,y,z}     controller animation type : {NSValue(SCNVector3)}
-FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyAngularVelocity NS_AVAILABLE(10_10, 8_0); // float                controller animation type : {NSNumber}
-FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyLife NS_AVAILABLE(10_10, 8_0);            // float                not controllable
-FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyColor NS_AVAILABLE(10_10, 8_0);           // float4 : {r,g,b,a}   controller animation type : {UIColor}
-FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyOpacity NS_AVAILABLE(10_10, 8_0);         // float                controller animation type : {NSNumber}
-FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertySize NS_AVAILABLE(10_10, 8_0);            // float                controller animation type : {NSNumber}
-FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyFrame NS_AVAILABLE(10_10, 8_0);           // float                controller animation type : {NSNumber}
-FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyFrameRate NS_AVAILABLE(10_10, 8_0);       // float                controller animation type : {NSNumber}
-FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyBounce NS_AVAILABLE(10_10, 8_0);          // float                controller animation type : {NSNumber}
-FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyCharge NS_AVAILABLE(10_10, 8_0);          // float                controller animation type : {NSNumber}
-FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyFriction NS_AVAILABLE(10_10, 8_0);        // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyPosition API_AVAILABLE(macosx(10.10));        // float3 : {x,y,z}     controller animation type : {NSValue(SCNVector3)}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyAngle API_AVAILABLE(macosx(10.10));           // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyRotationAxis API_AVAILABLE(macosx(10.10));    // float3 : {x,y,z}     controller animation type : {NSValue(SCNVector3)}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyVelocity API_AVAILABLE(macosx(10.10));        // float3 : {x,y,z}     controller animation type : {NSValue(SCNVector3)}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyAngularVelocity API_AVAILABLE(macosx(10.10)); // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyLife API_AVAILABLE(macosx(10.10));            // float                not controllable
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyColor API_AVAILABLE(macosx(10.10));           // float4 : {r,g,b,a}   controller animation type : {UIColor}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyOpacity API_AVAILABLE(macosx(10.10));         // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertySize API_AVAILABLE(macosx(10.10));            // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyFrame API_AVAILABLE(macosx(10.10));           // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyFrameRate API_AVAILABLE(macosx(10.10));       // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyBounce API_AVAILABLE(macosx(10.10));          // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyCharge API_AVAILABLE(macosx(10.10));          // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyFriction API_AVAILABLE(macosx(10.10));        // float                controller animation type : {NSNumber}
 
 // These two properties are only available when handling the events of type SCNParticleEventCollision.
 // They are read-only values.
-FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyContactPoint NS_AVAILABLE(10_10, 8_0);    // float3               not controllable
-FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyContactNormal NS_AVAILABLE(10_10, 8_0);   // float3               not controllable
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyContactPoint API_AVAILABLE(macosx(10.10));    // float3               not controllable
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyContactNormal API_AVAILABLE(macosx(10.10));   // float3               not controllable
 
 /*!
  @typedef SCNParticleEventBlock
@@ -91,7 +91,7 @@
 	SCNParticleSortingModeDistance,                    //particles are sorted by distance from the point of view
 	SCNParticleSortingModeOldestFirst,                 //particles are sorted by birth date - oldest first
 	SCNParticleSortingModeYoungestFirst                //particles are sorted by birth date - yougest first
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10));
 
 // Particle Blend Mode
 typedef NS_ENUM(NSInteger, SCNParticleBlendMode) {
@@ -101,7 +101,7 @@
 	SCNParticleBlendModeScreen,
 	SCNParticleBlendModeAlpha,
 	SCNParticleBlendModeReplace
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10));
 
 // Particle Orientation Mode
 typedef NS_ENUM(NSInteger, SCNParticleOrientationMode) {
@@ -109,35 +109,35 @@
 	SCNParticleOrientationModeBillboardViewAligned,    // particles are perpendicular with the vector from the point of view to the particle.
 	SCNParticleOrientationModeFree, 	                 // free on all axis.
     SCNParticleOrientationModeBillboardYAligned        // fixed on Y axis.
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10));
 
 // Particle Birth Location
 typedef NS_ENUM(NSInteger, SCNParticleBirthLocation) {
     SCNParticleBirthLocationSurface,                   //particles are emitted on the surface of the emitter shape.
     SCNParticleBirthLocationVolume,                    //particles are emitted inside the volume of the emitter shape.
     SCNParticleBirthLocationVertex                     //particles are emitted on the vertices of the emitter shape.
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10));
 
 // Particle Birth Direction
 typedef NS_ENUM(NSInteger, SCNParticleBirthDirection) {
     SCNParticleBirthDirectionConstant,                 // Z Direction of the Emitter.
     SCNParticleBirthDirectionSurfaceNormal,	        // Use the direction induced by the shape
     SCNParticleBirthDirectionRandom                    // Random direction.
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10));
 
 // Texture Animation Mode
 typedef NS_ENUM(NSInteger, SCNParticleImageSequenceAnimationMode) {
     SCNParticleImageSequenceAnimationModeRepeat,             // The animation will loop.
     SCNParticleImageSequenceAnimationModeClamp,              // The animation will stop at both ends.
     SCNParticleImageSequenceAnimationModeAutoReverse         // The animation will reverse when reaching an end.
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10));
 
 // Particle Variation Mode
 typedef NS_ENUM(NSInteger, SCNParticleInputMode) {
 	SCNParticleInputModeOverLife,                  // The input time for the controller animation is the current life duration of the particle
 	SCNParticleInputModeOverDistance,              // The input time for the controller animation is the distance from the variation origin node.
 	SCNParticleInputModeOverOtherProperty,         // The input time for the controller animation is the current value of another specified property.
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10));
 
 // Particle Modifier Stage
 typedef NS_ENUM(NSInteger, SCNParticleModifierStage) {
@@ -145,20 +145,20 @@
 	SCNParticleModifierStagePostDynamics,
 	SCNParticleModifierStagePreCollision,
 	SCNParticleModifierStagePostCollision
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10));
 
 // Particle Event
 typedef NS_ENUM(NSInteger, SCNParticleEvent) {
 	SCNParticleEventBirth,                             // Event triggered when a new particle spawns.
 	SCNParticleEventDeath,                             // Event triggered when a particle dies.
 	SCNParticleEventCollision                          // Event triggered when a particle collides with a collider node.
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10));
 
 /*!
  @class SCNParticlePropertyController
  @abstract The SCNParticlePropertyController class controls the variation over time or over distance of a particle property.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10))
 @interface SCNParticlePropertyController: NSObject <NSSecureCoding, NSCopying>
 
 // Creates and initializes a particle property controller with the specified animation.
@@ -191,7 +191,7 @@
  @class SCNParticleSystem
  @abstract The SCNParticleSystem class represents a system of particles.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10))
 @interface SCNParticleSystem : NSObject <NSCopying, NSSecureCoding, SCNAnimatable>
 
 // Create an instance of a particle system
@@ -418,16 +418,16 @@
 @interface SCNNode (SCNParticleSystemSupport)
 
 // Add a particle system to the receiver.
-- (void)addParticleSystem:(SCNParticleSystem *)system NS_AVAILABLE(10_10, 8_0);
+- (void)addParticleSystem:(SCNParticleSystem *)system API_AVAILABLE(macosx(10.10));
 
 // Remove all particle systems of the receiver.
-- (void)removeAllParticleSystems NS_AVAILABLE(10_10, 8_0);
+- (void)removeAllParticleSystems API_AVAILABLE(macosx(10.10));
 
 // Remove the specified particle system from the receiver.
-- (void)removeParticleSystem:(SCNParticleSystem *)system NS_AVAILABLE(10_10, 8_0);
+- (void)removeParticleSystem:(SCNParticleSystem *)system API_AVAILABLE(macosx(10.10));
 
 // The particle systems attached to the node.
-@property(readonly, nullable) NSArray<SCNParticleSystem *> *particleSystems NS_AVAILABLE(10_10, 8_0);
+@property(readonly, nullable) NSArray<SCNParticleSystem *> *particleSystems API_AVAILABLE(macosx(10.10));
 
 @end
 
@@ -435,16 +435,16 @@
 @interface SCNScene (SCNParticleSystemSupport)
 
 // Add a particle system at the given location.
-- (void)addParticleSystem:(SCNParticleSystem *)system withTransform:(SCNMatrix4)transform NS_AVAILABLE(10_10, 8_0);
+- (void)addParticleSystem:(SCNParticleSystem *)system withTransform:(SCNMatrix4)transform API_AVAILABLE(macosx(10.10));
 
 // Remove all particle systems in the scene.
-- (void)removeAllParticleSystems NS_AVAILABLE(10_10, 8_0);
+- (void)removeAllParticleSystems API_AVAILABLE(macosx(10.10));
 
 // Remove the specified particle system from the receiver.
-- (void)removeParticleSystem:(SCNParticleSystem *)system NS_AVAILABLE(10_10, 8_0);
+- (void)removeParticleSystem:(SCNParticleSystem *)system API_AVAILABLE(macosx(10.10));
 
 // The particle systems attached to the scene.
-@property(readonly, nullable) NSArray<SCNParticleSystem *> *particleSystems NS_AVAILABLE(10_10, 8_0);
+@property(readonly, nullable) NSArray<SCNParticleSystem *> *particleSystems API_AVAILABLE(macosx(10.10));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsBehavior.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsBehavior.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsBehavior.h	2016-05-31 05:16:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsBehavior.h	2016-06-26 09:42:49.000000000 +0200
@@ -15,7 +15,7 @@
  @class SCNPhysicsBehavior
  @abstract SCNPhysicsBehavior is an abstract class that represents a behavior in the physics world.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10))
 @interface SCNPhysicsBehavior : NSObject <NSSecureCoding>
 @end
 
@@ -23,7 +23,7 @@
  @class SCNPhysicsHingeJoint
  @abstract SCNPhysicsHingeJoint makes two bodies to move like they are connected by a hinge. It is for example suitable for doors, chains...
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10))
 @interface SCNPhysicsHingeJoint : SCNPhysicsBehavior
 
 //Initializes and returns a physics hinge joint.
@@ -48,7 +48,7 @@
  @class SCNPhysicsBallSocketJoint
  @abstract SCNPhysicsBallSocketJoint makes two bodies to move like they are connected by a ball-and-socket joint (i.e it allows rotations around all axes).
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10))
 @interface SCNPhysicsBallSocketJoint : SCNPhysicsBehavior
 
 //Initializes and returns a physics ball-and-socket joint.
@@ -71,7 +71,7 @@
  @class SCNPhysicsSliderJoint
  @abstract SCNPhysicsSliderJoint provides a linear sliding joint between two bodies.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10))
 @interface SCNPhysicsSliderJoint : SCNPhysicsBehavior
 
 //Initializes and returns a physics slider joint.
@@ -111,7 +111,7 @@
  @class SCNPhysicsVehicleWheel
  @abstract SCNPhysicsVehicleWheel represents a wheel that can be attached to a SCNPhysicsVehicle instance.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10))
 @interface SCNPhysicsVehicleWheel : NSObject <NSCopying, NSSecureCoding>
 
 //Initializes and returns a wheel.
@@ -159,7 +159,7 @@
  @class SCNPhysicsVehicle
  @abstract SCNPhysicsVehicle provides a vehicle behavior.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10))
 @interface SCNPhysicsVehicle : SCNPhysicsBehavior
 
 // Initializes and returns a physics vehicle that applies on the physics body "chassisBody" with the given wheels.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsBody.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsBody.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsBody.h	2016-05-24 23:53:11.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsBody.h	2016-06-26 09:09:03.000000000 +0200
@@ -15,20 +15,20 @@
 	SCNPhysicsBodyTypeStatic,
 	SCNPhysicsBodyTypeDynamic,
 	SCNPhysicsBodyTypeKinematic
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10));
 
 //Collision default category
 typedef NS_OPTIONS(NSUInteger, SCNPhysicsCollisionCategory) {
 	SCNPhysicsCollisionCategoryDefault = 1 << 0,    // default collision group for dynamic and kinematic objects
 	SCNPhysicsCollisionCategoryStatic  = 1 << 1,    // default collision group for static objects
 	SCNPhysicsCollisionCategoryAll     = ~0UL       // default for collision mask
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10));
 
 /*!
  @class SCNPhysicsBody
  @abstract The SCNPhysicsBody class describes the physics properties (such as mass, friction...) of a node.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10))
 @interface SCNPhysicsBody : NSObject <NSCopying, NSSecureCoding>
 
 //Creates an instance of a static body with default properties.
@@ -50,10 +50,10 @@
 @property(nonatomic) CGFloat mass;
 
 //Specifies the moment of inertia of the body as a vector in 3D. Disable usesDefaultMomentOfInertia for this value to be used instead of the default moment of inertia that is calculated from the shape geometry.
-@property(nonatomic) SCNVector3 momentOfInertia NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic) SCNVector3 momentOfInertia API_AVAILABLE(macosx(10.11), ios(9.0));
 
 //Permits to disable the use of the default moment of inertia in favor of the one stored in momentOfInertia.
-@property(nonatomic) BOOL usesDefaultMomentOfInertia NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic) BOOL usesDefaultMomentOfInertia API_AVAILABLE(macosx(10.11), ios(9.0));
 
 // Specifies the charge on the body. Charge determines the degree to which a body is affected by
 // electric and magnetic fields. Note that this is a unitless quantity, it is up to the developer to
@@ -98,18 +98,18 @@
 
 //Defines what logical 'categories' this body belongs too.
 //Defaults to SCNPhysicsCollisionCategoryStatic for static bodies and SCNPhysicsCollisionCategoryDefault for the other body types.
-//limited to the first 15 bits on OS X 10.10 and iOS 8.
+//limited to the first 15 bits on macOS 10.10 and iOS 8.
 @property(nonatomic) NSUInteger categoryBitMask;
 
 //Defines what logical 'categories' of bodies this body responds to collisions with. Defaults to all bits set (all categories).
 @property(nonatomic) NSUInteger collisionBitMask;
 
 //A mask that defines which categories of bodies cause intersection notifications with this physics body. Defaults to 0.
-//On iOS 8 and OS X 10.10 and lower the intersection notifications are always sent when a collision occurs.
-@property(nonatomic) NSUInteger contactTestBitMask NS_AVAILABLE(10_11, 9_0);
+//On iOS 8 and macOS 10.10 and lower the intersection notifications are always sent when a collision occurs.
+@property(nonatomic) NSUInteger contactTestBitMask API_AVAILABLE(macosx(10.11), ios(9.0));
 
 //If set to YES this node will be affected by gravity. The default is YES.
-@property(nonatomic, getter=isAffectedByGravity) BOOL affectedByGravity NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, getter=isAffectedByGravity) BOOL affectedByGravity API_AVAILABLE(macosx(10.11), ios(9.0));
 
 //Applies a linear force in the specified direction. The linear force is applied on the center of mass of the receiver. If impulse is set to YES then the force is applied for just one frame, otherwise it applies a continuous force.
 - (void)applyForce:(SCNVector3)direction impulse:(BOOL)impulse;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsContact.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsContact.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsContact.h	2016-05-31 05:16:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsContact.h	2016-06-26 08:35:21.000000000 +0200
@@ -14,7 +14,7 @@
  @class SCNPhysicsContact
  @abstract SCNPhysicsContact contains information about a physics contact.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10))
 @interface SCNPhysicsContact : NSObject
 
 //The two nodes in contact
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsField.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsField.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsField.h	2016-05-31 04:56:02.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsField.h	2016-06-26 08:59:07.000000000 +0200
@@ -17,13 +17,13 @@
 typedef NS_ENUM(NSInteger, SCNPhysicsFieldScope) {
     SCNPhysicsFieldScopeInsideExtent,
     SCNPhysicsFieldScopeOutsideExtent,
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10));
 
 /*!
  @class SCNPhysicsField
  @abstract SCNPhysicsField is an abstract class that describes a force field that applies in the physics world.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10))
 @interface SCNPhysicsField : NSObject <NSCopying, NSSecureCoding>
 
 // The following properties control the behavior of the field
@@ -46,7 +46,7 @@
  @property categoryBitMask
  @abstract Determines the node categories that will be influenced by the receiver. Defaults to all bit set.
  */
-@property(nonatomic) NSUInteger categoryBitMask NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) NSUInteger categoryBitMask API_AVAILABLE(macosx(10.10));
 
 
 /**
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsShape.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsShape.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsShape.h	2016-05-31 05:16:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsShape.h	2016-06-26 08:35:21.000000000 +0200
@@ -17,14 +17,14 @@
 typedef NSString * SCNPhysicsShapeOption;
 #endif
 
-FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionType NS_AVAILABLE(10_12, 10_0);            // Type of the physics shape. Default is SCNPhysicsShapeTypeConvexHull. See below for the list of shape types.
-FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionKeepAsCompound NS_AVAILABLE(10_12, 10_0);  // A boolean to decide if a hierarchy is kept as a compound of shapes or flattened as one single volume. Default is true.
-FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionScale NS_AVAILABLE(10_12, 10_0);           // Local scaling of the physics shape (as an SCNVector3 wrapped in a NSValue)
-FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionCollisionMargin NS_AVAILABLE(10_12, 10_0); // Collision margin of the physics shape (as an NSNumber)
-
-FOUNDATION_EXTERN NSString * const SCNPhysicsShapeTypeKey NS_AVAILABLE(10_10, 8_0);           // Please use SCNPhysicsShapeOption.type instead.
-FOUNDATION_EXTERN NSString * const SCNPhysicsShapeKeepAsCompoundKey NS_AVAILABLE(10_10, 8_0); // Please use SCNPhysicsShapeOption.keepAsCompound instead.
-FOUNDATION_EXTERN NSString * const SCNPhysicsShapeScaleKey NS_AVAILABLE(10_10, 8_0);          // Please use SCNPhysicsShapeOption.scale instead.
+FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionType API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));            // Type of the physics shape. Default is SCNPhysicsShapeTypeConvexHull. See below for the list of shape types.
+FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionKeepAsCompound API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));  // A boolean to decide if a hierarchy is kept as a compound of shapes or flattened as one single volume. Default is true.
+FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionScale API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));           // Local scaling of the physics shape (as an SCNVector3 wrapped in a NSValue)
+FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionCollisionMargin API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Collision margin of the physics shape (as an NSNumber)
+
+FOUNDATION_EXTERN NSString * const SCNPhysicsShapeTypeKey API_AVAILABLE(macosx(10.10));           // Please use SCNPhysicsShapeOption.type instead.
+FOUNDATION_EXTERN NSString * const SCNPhysicsShapeKeepAsCompoundKey API_AVAILABLE(macosx(10.10)); // Please use SCNPhysicsShapeOption.keepAsCompound instead.
+FOUNDATION_EXTERN NSString * const SCNPhysicsShapeScaleKey API_AVAILABLE(macosx(10.10));          // Please use SCNPhysicsShapeOption.scale instead.
 
 // Values for SCNPhysicsShapeOptionType
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
@@ -33,15 +33,15 @@
 typedef NSString * SCNPhysicsShapeType;
 #endif
 
-FOUNDATION_EXTERN SCNPhysicsShapeType const SCNPhysicsShapeTypeBoundingBox NS_AVAILABLE(10_10, 8_0);
-FOUNDATION_EXTERN SCNPhysicsShapeType const SCNPhysicsShapeTypeConvexHull NS_AVAILABLE(10_10, 8_0);
-FOUNDATION_EXTERN SCNPhysicsShapeType const SCNPhysicsShapeTypeConcavePolyhedron NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNPhysicsShapeType const SCNPhysicsShapeTypeBoundingBox API_AVAILABLE(macosx(10.10));
+FOUNDATION_EXTERN SCNPhysicsShapeType const SCNPhysicsShapeTypeConvexHull API_AVAILABLE(macosx(10.10));
+FOUNDATION_EXTERN SCNPhysicsShapeType const SCNPhysicsShapeTypeConcavePolyhedron API_AVAILABLE(macosx(10.10));
 
 /*!
  @class SCNPhysicsShape
  @abstract SCNPhysicsShape represents the shape of a physics body.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10))
 @interface SCNPhysicsShape : NSObject <NSCopying, NSSecureCoding>
 
 //Creates an instance of a physics shape based on a geometry. see above for the possible options.
@@ -54,13 +54,13 @@
 + (instancetype)shapeWithShapes:(NSArray<SCNPhysicsShape *> *)shapes transforms:(nullable NSArray<NSValue *> *)transforms;
 
 // Returns the options requested at init time
-@property(readonly, nonatomic, nullable) NSDictionary<SCNPhysicsShapeOption, id> *options NS_AVAILABLE(10_11, 9_0);
+@property(readonly, nonatomic, nullable) NSDictionary<SCNPhysicsShapeOption, id> *options API_AVAILABLE(macosx(10.11), ios(9.0));
 
 // Returns the object from which this physics shape was created. It can be an SCNGeometry*, an SCNNode* or in NSArray* of subshapes.
-@property(readonly, nonatomic) id sourceObject NS_AVAILABLE(10_11, 9_0);
+@property(readonly, nonatomic) id sourceObject API_AVAILABLE(macosx(10.11), ios(9.0));
 
 // If the physics shape was created from an array of sub shapes, transforms contains the associated transforms as SCNMatrix4 wrapped in NSValue.
-@property(readonly, nonatomic, nullable) NSArray<NSValue *> *transforms NS_AVAILABLE(10_11, 9_0);
+@property(readonly, nonatomic, nullable) NSArray<NSValue *> *transforms API_AVAILABLE(macosx(10.11), ios(9.0));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsWorld.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsWorld.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsWorld.h	2016-05-22 05:48:21.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsWorld.h	2016-06-26 08:35:21.000000000 +0200
@@ -22,13 +22,13 @@
 typedef NSString * SCNPhysicsTestOption;
 #endif
 
-FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestOptionCollisionBitMask NS_AVAILABLE(10_12, 10_0); // Allows to filter the objects tested by rayTest, contactTest and convexSweep. Default is SCNPhysicsCollisionCategoryAll
-FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestOptionSearchMode NS_AVAILABLE(10_12, 10_0);       // Specifies how to perform the ray/contact/sweep test. Values are defined below. If not defined, then defaults to SCNPhysicsTestSearchModeAny
-FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestOptionBackfaceCulling NS_AVAILABLE(10_12, 10_0);  // Specifies whether the back faces should be ignored or not. Defaults to YES.
-
-FOUNDATION_EXTERN NSString * const SCNPhysicsTestCollisionBitMaskKey NS_AVAILABLE(10_10, 8_0); // Please use SCNPhysicsTestOption.collisionBitMask instead.
-FOUNDATION_EXTERN NSString * const SCNPhysicsTestSearchModeKey NS_AVAILABLE(10_10, 8_0);       // Please use SCNPhysicsTestOption.searchMode instead.
-FOUNDATION_EXTERN NSString * const SCNPhysicsTestBackfaceCullingKey NS_AVAILABLE(10_10, 8_0);  // Please use SCNPhysicsTestOption.backfaceCulling instead.
+FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestOptionCollisionBitMask API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Allows to filter the objects tested by rayTest, contactTest and convexSweep. Default is SCNPhysicsCollisionCategoryAll
+FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestOptionSearchMode API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));       // Specifies how to perform the ray/contact/sweep test. Values are defined below. If not defined, then defaults to SCNPhysicsTestSearchModeAny
+FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestOptionBackfaceCulling API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));  // Specifies whether the back faces should be ignored or not. Defaults to YES.
+
+FOUNDATION_EXTERN NSString * const SCNPhysicsTestCollisionBitMaskKey API_AVAILABLE(macosx(10.10)); // Please use SCNPhysicsTestOption.collisionBitMask instead.
+FOUNDATION_EXTERN NSString * const SCNPhysicsTestSearchModeKey API_AVAILABLE(macosx(10.10));       // Please use SCNPhysicsTestOption.searchMode instead.
+FOUNDATION_EXTERN NSString * const SCNPhysicsTestBackfaceCullingKey API_AVAILABLE(macosx(10.10));  // Please use SCNPhysicsTestOption.backfaceCulling instead.
 
 // Values for SCNPhysicsTestSearchModeKey
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
@@ -37,15 +37,15 @@
 typedef NSString * SCNPhysicsTestSearchMode;
 #endif
 
-FOUNDATION_EXTERN SCNPhysicsTestSearchMode const SCNPhysicsTestSearchModeAny NS_AVAILABLE(10_10, 8_0);     // Returns the first contact found.
-FOUNDATION_EXTERN SCNPhysicsTestSearchMode const SCNPhysicsTestSearchModeClosest NS_AVAILABLE(10_10, 8_0); // Returns the nearest contact found only.
-FOUNDATION_EXTERN SCNPhysicsTestSearchMode const SCNPhysicsTestSearchModeAll NS_AVAILABLE(10_10, 8_0);     // All contacts are returned.
+FOUNDATION_EXTERN SCNPhysicsTestSearchMode const SCNPhysicsTestSearchModeAny API_AVAILABLE(macosx(10.10));     // Returns the first contact found.
+FOUNDATION_EXTERN SCNPhysicsTestSearchMode const SCNPhysicsTestSearchModeClosest API_AVAILABLE(macosx(10.10)); // Returns the nearest contact found only.
+FOUNDATION_EXTERN SCNPhysicsTestSearchMode const SCNPhysicsTestSearchModeAll API_AVAILABLE(macosx(10.10));     // All contacts are returned.
 
 /*!
  @protocol SCNPhysicsContactDelegate
  @abstract The SCNPhysicsContactDelegate protocol is to be implemented by delegates that want to be notified when a contact occured.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10))
 @protocol SCNPhysicsContactDelegate <NSObject>
 @optional
 - (void)physicsWorld:(SCNPhysicsWorld *)world didBeginContact:(SCNPhysicsContact *)contact;
@@ -58,7 +58,7 @@
  @abstract The SCNPhysicsWorld class describes and allows to control the physics simulation of a 3d scene.
  @discussion The SCNPhysicsWorld class should not be allocated directly but retrieved from the SCNScene class using the physicsWorld property.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10))
 @interface SCNPhysicsWorld : NSObject <NSSecureCoding>
 
 //A global 3D vector specifying the field force acceleration due to gravity. The unit is meter per second. Default is {0, -9.8, 0}.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNReferenceNode.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNReferenceNode.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNReferenceNode.h	2016-05-31 05:16:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNReferenceNode.h	2016-06-26 08:35:21.000000000 +0200
@@ -16,13 +16,13 @@
 typedef NS_ENUM(NSInteger, SCNReferenceLoadingPolicy) {
     SCNReferenceLoadingPolicyImmediate = 0,
     SCNReferenceLoadingPolicyOnDemand  = 1
-} NS_ENUM_AVAILABLE(10_11, 9_0);
+} API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @class SCNReferenceNode
  @abstract Node that references an external file.
  */
-NS_CLASS_AVAILABLE(10_11, 9_0)
+API_AVAILABLE(macosx(10.11), ios(9.0))
 @interface SCNReferenceNode : SCNNode
 
 /*!
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNRenderer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNRenderer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNRenderer.h	2016-05-31 05:16:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNRenderer.h	2016-06-26 08:35:21.000000000 +0200
@@ -18,7 +18,7 @@
 /*! @class SCNRenderer
 	@abstract SCNRenderer lets you use the SceneKit renderer in an OpenGL context or Metal render pass descriptor of your own.
  */
-NS_CLASS_AVAILABLE(10_8, 8_0) __WATCHOS_PROHIBITED
+__WATCHOS_PROHIBITED
 @interface SCNRenderer : NSObject <SCNSceneRenderer, SCNTechniqueSupport>
 
 /*! 
@@ -35,7 +35,7 @@
  @param device The metal device to use. Pass nil to let SceneKit choose a default device.
  @param options An optional dictionary for future extensions.
  */
-+ (instancetype)rendererWithDevice:(nullable id <MTLDevice>)device options:(nullable NSDictionary *)options NS_AVAILABLE(10_11, 9_0);
++ (instancetype)rendererWithDevice:(nullable id <MTLDevice>)device options:(nullable NSDictionary *)options API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*! 
  @property scene
@@ -48,33 +48,43 @@
  @abstract renders the receiver's scene at the specified time (system time).
  @discussion This method only work if the receiver was allocated with an OpenGL context. Use renderAtTime:withEncoder:pass:commandQueue: to render with Metal.
  */
-- (void)renderAtTime:(CFTimeInterval)time NS_AVAILABLE(10_10, 8_0);
+- (void)renderAtTime:(CFTimeInterval)time API_AVAILABLE(macosx(10.10));
 
 /*!
  @method snapshotAtTime:withSize:antialiasingMode:
  @abstract renders the receiver's scene at the specified time (system time) into an image.
  */
-- (UIImage *)snapshotAtTime:(CFTimeInterval)time withSize:(CGSize)size antialiasingMode:(SCNAntialiasingMode)antialiasingMode NS_AVAILABLE(10_12, 10_0);
+- (UIImage *)snapshotAtTime:(CFTimeInterval)time withSize:(CGSize)size antialiasingMode:(SCNAntialiasingMode)antialiasingMode API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @method renderAtTime:viewport:commandBuffer:passDescriptor:
  @abstract renders the receiver's scene at the specified time (system time) viewport, metal command buffer and pass descriptor.
  @discussion Use this method to render using Metal.
  */
-- (void)renderAtTime:(CFTimeInterval)time viewport:(CGRect)viewport commandBuffer:(id <MTLCommandBuffer>)commandBuffer passDescriptor:(MTLRenderPassDescriptor *)renderPassDescriptor NS_AVAILABLE(10_11, 9_0);
+- (void)renderAtTime:(CFTimeInterval)time viewport:(CGRect)viewport commandBuffer:(id <MTLCommandBuffer>)commandBuffer passDescriptor:(MTLRenderPassDescriptor *)renderPassDescriptor API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @property nextFrameTime
  @abstract Returns the time at which the next update should happen. If infinite no update needs to be scheduled yet. If the current frame time, a continuous animation is running and an update should be scheduled after a "natural" delay.
  */
-@property(nonatomic, readonly) CFTimeInterval nextFrameTime NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic, readonly) CFTimeInterval nextFrameTime API_AVAILABLE(macosx(10.10));
 
 /*!
  @method render
  @abstract renders the receiver's scene at the current system time.
- @discussion This method only work if the receiver was allocated with an OpenGL context and it is deprecated (use renderAtIme: instead). Use renderAtTime:withEncoder:pass:commandQueue: to render with Metal.
+ @discussion This method only work if the receiver was allocated with an OpenGL context and it is deprecated (use renderAtTime: instead). Use renderAtTime:withEncoder:pass:commandQueue: to render with Metal.
  */
-- (void)render NS_DEPRECATED(10_8, 10_11, 8_0, 9_0) __WATCHOS_UNAVAILABLE;
+- (void)render API_DEPRECATED_WITH_REPLACEMENT("-renderAtTime:withEncoder:pass:commandQueue:", macosx(10.8, 10.11), ios(8.0, 9.0)) API_UNAVAILABLE(watchos, tvos);
+
+/*!
+ @method updateProbes:atTime:
+ @abstract Update the specified probes by computing their incoming irradiance in the receiver's scene at the specified time.
+ @param lightProbes An array of nodes that must have a light probe attached.
+ @param time The time used to render the scene when computing the light probes irradiance.
+ @discussion Light probes are only supported with Metal. This method is observable using NSProgress.
+ */
+- (void)updateProbes:(NSArray<SCNNode*> *)lightProbes atTime:(CFTimeInterval)time API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNScene.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNScene.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNScene.h	2016-05-22 05:48:21.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNScene.h	2016-06-26 08:26:52.000000000 +0200
@@ -31,7 +31,7 @@
  @abstract Specifies the final destination (as a NSURL) of the scene being exported.
  @discussion The destination URL is required if the scene is exported to a temporary directory and then moved to a final destination. This enables the exported document to get correct relative paths to referenced images.
  */
-FOUNDATION_EXTERN NSString * const SCNSceneExportDestinationURL NS_AVAILABLE(10_9, 8_0);
+FOUNDATION_EXTERN NSString * const SCNSceneExportDestinationURL API_AVAILABLE(macosx(10.9));
 
 
 /*! @group Scene attributes
@@ -43,22 +43,21 @@
 typedef NSString * SCNSceneAttribute;
 #endif
 
-FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneAttributeStartTime NS_AVAILABLE(10_12, 10_0); // A floating point value, encapsulated in a NSNumber, containing the start time of the scene.
-FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneAttributeEndTime NS_AVAILABLE(10_12, 10_0);   // A floating point value, encapsulated in a NSNumber, containing the end time of the scene.
-FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneAttributeFrameRate NS_AVAILABLE(10_12, 10_0); // A floating point value, encapsulated in a NSNumber, containing the framerate of the scene.
-FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneAttributeUpAxis NS_AVAILABLE(10_12, 10_0);    // A vector3 value, encapsulated in a NSValue, containing the up axis of the scene. This is just for information, setting the up axis as no effect.
+FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneAttributeStartTime API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // A floating point value, encapsulated in a NSNumber, containing the start time of the scene.
+FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneAttributeEndTime API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));   // A floating point value, encapsulated in a NSNumber, containing the end time of the scene.
+FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneAttributeFrameRate API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // A floating point value, encapsulated in a NSNumber, containing the framerate of the scene.
+FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneAttributeUpAxis API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));    // A vector3 value, encapsulated in a NSValue, containing the up axis of the scene. This is just for information, setting the up axis as no effect.
 
 FOUNDATION_EXTERN NSString * const SCNSceneStartTimeAttributeKey;                       // Please use SCNSceneAttribute.startTime instead.
 FOUNDATION_EXTERN NSString * const SCNSceneEndTimeAttributeKey;                         // Please use SCNSceneAttribute.endTime instead.
 FOUNDATION_EXTERN NSString * const SCNSceneFrameRateAttributeKey;                       // Please use SCNSceneAttribute.frameRate instead.
-FOUNDATION_EXTERN NSString * const SCNSceneUpAxisAttributeKey NS_AVAILABLE(10_10, 8_0); // Please use SCNSceneAttribute.upAxis instead.
+FOUNDATION_EXTERN NSString * const SCNSceneUpAxisAttributeKey API_AVAILABLE(macosx(10.10)); // Please use SCNSceneAttribute.upAxis instead.
 
 /*!
  @class SCNScene
  @abstract SCNScene is the class that describes a 3d scene. It encapsulates a node hierarchy.
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNScene : NSObject <NSSecureCoding>
 
 + (instancetype)scene;
@@ -77,7 +76,7 @@
  @abstract Specifies the physics world of the receiver.
  @discussion Every scene automatically creates a physics world object to simulate physics on nodes in the scene. You use this property to access the scene’s global physics properties, such as gravity. To add physics to a particular node, see physicsBody.
  */
-@property(nonatomic, readonly) SCNPhysicsWorld *physicsWorld NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic, readonly) SCNPhysicsWorld *physicsWorld API_AVAILABLE(macosx(10.10));
 
 /*!
  @method attributeForKey:
@@ -101,16 +100,16 @@
  @abstract Specifies the background of the receiver.
  @discussion The background is rendered before the rest of the scene.
              The background can be rendered as a skybox by setting a cube map as described in SCNMaterialProperty.h
-             Colors are supported starting OS X 10.12 and iOS 10.0. Prior to that you can use SCNView.backgroundColor.
+             Colors are supported starting macOS 10.12 and iOS 10. Prior to that you can use SCNView.backgroundColor.
  */
-@property(nonatomic, readonly) SCNMaterialProperty *background NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic, readonly) SCNMaterialProperty *background API_AVAILABLE(macosx(10.9));
 
 /*!
  @property lightingEnvironment
  @abstract Specifies the receiver's environment for image-based lighting (IBL).
  @discussion The environment should be a cube map as described in SCNMaterialProperty.h
  */
-@property(nonatomic, readonly) SCNMaterialProperty *lightingEnvironment NS_AVAILABLE(10_12, 10_0);
+@property(nonatomic, readonly) SCNMaterialProperty *lightingEnvironment API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 
 #pragma mark - Loading
@@ -121,7 +120,7 @@
  @param name The name of the file. The method looks for a file with the specified name in the application’s main bundle.
  @discussion This method initializes with no options and does not check for errors. The resulting object is not cached.
  */
-+ (nullable instancetype)sceneNamed:(NSString *)name NS_AVAILABLE(10_9, 8_0);
++ (nullable instancetype)sceneNamed:(NSString *)name API_AVAILABLE(macosx(10.9));
 
 /*!
  @method sceneNamed:options:
@@ -131,7 +130,7 @@
  @param options An options dictionary. The relevant keys are documented in the SCNSceneSource class.
  @discussion This method initializes with no options and does not check for errors. The resulting object is not cached.
  */
-+ (nullable instancetype)sceneNamed:(NSString *)name inDirectory:(nullable NSString *)directory options:(nullable NSDictionary<SCNSceneSourceLoadingOption, id> *)options NS_AVAILABLE(10_10, 8_0);
++ (nullable instancetype)sceneNamed:(NSString *)name inDirectory:(nullable NSString *)directory options:(nullable NSDictionary<SCNSceneSourceLoadingOption, id> *)options API_AVAILABLE(macosx(10.10));
 
 /*!
  @method sceneWithURL:options:error:
@@ -155,11 +154,11 @@
  @param progressHandler an optional block to handle the progress of the operation.
  @return Returns YES if the operation succeeded, NO otherwise. Errors checking can be done via the "error"
  parameter of the 'progressHandler'.
- @discussion OS X 10.10 and lower only supports exporting to .dae files.
-             Starting OS X 10.11 exporting supports .dae, .scn as well as file all formats supported by Model I/O.
-             Starting iOS 10.0 exporting supports .scn as well as all file formats supported by Model I/O.
+ @discussion macOS 10.10 and lower only supports exporting to .dae files.
+             Starting macOS 10.11 exporting supports .dae, .scn as well as file all formats supported by Model I/O.
+             Starting iOS 10 exporting supports .scn as well as all file formats supported by Model I/O.
  */
-- (BOOL)writeToURL:(NSURL *)url options:(nullable NSDictionary<NSString *, id> *)options delegate:(nullable id <SCNSceneExportDelegate>)delegate progressHandler:(nullable SCNSceneExportProgressHandler)progressHandler NS_AVAILABLE(10_9, 10_0);
+- (BOOL)writeToURL:(NSURL *)url options:(nullable NSDictionary<NSString *, id> *)options delegate:(nullable id <SCNSceneExportDelegate>)delegate progressHandler:(nullable SCNSceneExportProgressHandler)progressHandler API_AVAILABLE(macosx(10.9), ios(10.0), tvos(10.0));
 
 #pragma mark - Fog
 
@@ -167,27 +166,27 @@
  @property fogStartDistance
  @abstract Specifies the receiver's fog start distance. Animatable. Defaults to 0.
  */
-@property(nonatomic) CGFloat fogStartDistance NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) CGFloat fogStartDistance API_AVAILABLE(macosx(10.10));
 
 /*!
  @property fogEndDistance
  @abstract Specifies the receiver's fog end distance. Animatable. Defaults to 0.
  */
-@property(nonatomic) CGFloat fogEndDistance NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) CGFloat fogEndDistance API_AVAILABLE(macosx(10.10));
 
 /*!
  @property fogDensityExponent
  @abstract Specifies the receiver's fog power exponent. Animatable. Defaults to 1.
  @discussion Controls the attenuation between the start and end fog distances. 0 means a constant fog, 1 a linear fog and 2 a quadratic fog, but any positive value will work.
  */
-@property(nonatomic) CGFloat fogDensityExponent NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) CGFloat fogDensityExponent API_AVAILABLE(macosx(10.10));
 
 /*!
  @property fogColor
  @abstract Specifies the receiver's fog color (NSColor or CGColorRef). Animatable. Defaults to white.
  @discussion The initial value is a NSColor.
  */
-@property(nonatomic, retain) id fogColor NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic, retain) id fogColor API_AVAILABLE(macosx(10.10));
 
 
 #pragma mark - Pause
@@ -197,7 +196,7 @@
  @abstract Controls whether or not the scene is paused. Defaults to NO.
  @discussion Pausing a scene will pause animations, actions, particles and physics.
  */
-@property(nonatomic, getter=isPaused) BOOL paused NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic, getter=isPaused) BOOL paused API_AVAILABLE(macosx(10.10));
 
 
 @end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneRenderer.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneRenderer.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneRenderer.h	2016-05-31 04:56:02.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneRenderer.h	2016-06-26 08:26:52.000000000 +0200
@@ -28,18 +28,18 @@
     SCNAntialiasingModeNone,
     SCNAntialiasingModeMultisampling2X,
     SCNAntialiasingModeMultisampling4X
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+} API_AVAILABLE(macosx(10.10));
 
 /*!
  @enum SCNRenderingAPI
  @abstract rendering API used by SCNView and SCNRenderer.
- @discussion Default preferred API is SCNRenderingAPIMetal on iOS and it depends on the configuration on OS X.
- If Metal is requested but not available then it fallbacks to SCNRenderingAPIOpenGLES2 on iOS and to SCNRenderingAPIOpenGLLegacy on OS X.
+ @discussion Default preferred API is SCNRenderingAPIMetal on iOS and it depends on the configuration on macOS.
+ If Metal is requested but not available then it fallbacks to SCNRenderingAPIOpenGLES2 on iOS and to SCNRenderingAPIOpenGLLegacy on macOS.
  */
 typedef NS_ENUM(NSUInteger, SCNRenderingAPI) {
     SCNRenderingAPIMetal,
     SCNRenderingAPIOpenGLES2
-} NS_ENUM_AVAILABLE(10_11, 9_0);
+} API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @enum SCNDebugOptions
@@ -53,7 +53,7 @@
     SCNDebugOptionShowLightExtents    = 1 << 3,
     SCNDebugOptionShowPhysicsFields   = 1 << 4,
     SCNDebugOptionShowWireframe       = 1 << 5
-} NS_ENUM_AVAILABLE(10_11, 9_0);
+} API_AVAILABLE(macosx(10.11), ios(9.0));
 
 
 
@@ -77,14 +77,14 @@
  @param pointOfView the point of view to use to render the new scene.
  @param completionHandler the block invoked on completion.
  */
-- (void)presentScene:(SCNScene *)scene withTransition:(SKTransition *)transition incomingPointOfView:(nullable SCNNode *)pointOfView completionHandler:(nullable void (^)())completionHandler NS_AVAILABLE(10_11, 9_0);
+- (void)presentScene:(SCNScene *)scene withTransition:(SKTransition *)transition incomingPointOfView:(nullable SCNNode *)pointOfView completionHandler:(nullable void (^)())completionHandler API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @property sceneTime
  @abstract Specifies the current "scene time" to display the scene.
  @discussion The scene time only affect scene time based animations (see SCNAnimation.h "usesSceneTimeBase" and SCNSceneSource.h "SCNSceneSourceAnimationImportPolicyKey" for how to create scene time based animations). Scene time based animations and this property are typically used by tools and viewer to ease seeking in time while previewing a scene.
  */
-@property(nonatomic) NSTimeInterval sceneTime NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) NSTimeInterval sceneTime API_AVAILABLE(macosx(10.10));
 
 /*! 
  @property delegate
@@ -107,7 +107,7 @@
  @param pointOfView The point of view used to test the visibility.
  @discussion Return YES if the node is inside or intersects the clipping planes of the point of view. This method doesn't test if 'node' is occluded by another node.
  */
-- (BOOL)isNodeInsideFrustum:(SCNNode *)node withPointOfView:(SCNNode *)pointOfView NS_AVAILABLE(10_9, 8_0);
+- (BOOL)isNodeInsideFrustum:(SCNNode *)node withPointOfView:(SCNNode *)pointOfView API_AVAILABLE(macosx(10.9));
 
 /*!
  @method nodesInsideFrustumWithPointOfView:
@@ -115,7 +115,7 @@
  @param pointOfView The point of view used to test the visibility.
  @discussion Returns an array of all the nodes that are inside or intersects the clipping planes of the point of view.
  */
-- (NSArray<SCNNode *> *)nodesInsideFrustumWithPointOfView:(SCNNode *)pointOfView NS_AVAILABLE(10_11, 9_0);
+- (NSArray<SCNNode *> *)nodesInsideFrustumWithPointOfView:(SCNNode *)pointOfView API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @method projectPoint
@@ -123,7 +123,7 @@
  @param point The world position to be projected.
  @discussion A point projected from the near (resp. far) clip plane will have a z component of 0 (resp. 1).
  */
-- (SCNVector3)projectPoint:(SCNVector3)point NS_AVAILABLE(10_9, 8_0);
+- (SCNVector3)projectPoint:(SCNVector3)point API_AVAILABLE(macosx(10.9));
 
 /*!
  @method unprojectPoint
@@ -131,7 +131,7 @@
  @param point The screenspace position to be unprojected.
  @discussion A point whose z component is 0 (resp. 1) is unprojected on the near (resp. far) clip plane.
  */
-- (SCNVector3)unprojectPoint:(SCNVector3)point NS_AVAILABLE(10_9, 8_0);
+- (SCNVector3)unprojectPoint:(SCNVector3)point API_AVAILABLE(macosx(10.9));
 
 /*! 
  @property playing
@@ -174,7 +174,7 @@
  @param block This block will be called repeatedly while the object is prepared. Return YES if you want the operation to abort.
  @discussion Returns YES if the object was prepared successfully, NO if it was canceled. This method may be triggered from a secondary thread. This method is observable using NSProgress.
  */
-- (BOOL)prepareObject:(id)object shouldAbortBlock:(nullable __attribute__((noescape)) BOOL (^)())block NS_AVAILABLE(10_9, 8_0);
+- (BOOL)prepareObject:(id)object shouldAbortBlock:(nullable NS_NOESCAPE BOOL (^)())block API_AVAILABLE(macosx(10.9));
 
 /*!
  @method prepareObjects:withCompletionHandler:
@@ -183,37 +183,37 @@
  @param completionHandler This block will be called when all objects has been prepared, or on failure.
  @discussion This method is observable using NSProgress.
  */
-- (void)prepareObjects:(NSArray *)objects withCompletionHandler:(nullable void (^)(BOOL success))completionHandler NS_AVAILABLE(10_10, 8_0);
+- (void)prepareObjects:(NSArray *)objects withCompletionHandler:(nullable void (^)(BOOL success))completionHandler API_AVAILABLE(macosx(10.10));
 
 /*!
  @property showsStatistics
  @abstract Determines whether the receiver should display statistics info like FPS. Defaults to NO.
  @discussion  When set to YES, statistics are displayed in a overlay on top of the rendered scene.
  */
-@property(nonatomic) BOOL showsStatistics NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic) BOOL showsStatistics API_AVAILABLE(macosx(10.9));
 
 /*!
  @property debugOptions
  @abstract Specifies the debug options of the receiver. Defaults to SCNDebugOptionNone.
  */
-@property(nonatomic) SCNDebugOptions debugOptions NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic) SCNDebugOptions debugOptions API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @property overlaySKScene
  @abstract Specifies the overlay of the receiver as a SpriteKit scene instance. Defaults to nil.
  */
-@property(nonatomic, retain, nullable) SKScene *overlaySKScene NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic, retain, nullable) SKScene *overlaySKScene API_AVAILABLE(macosx(10.10));
 
 /*!
  @property renderingAPI
  @abstract Specifies the rendering API associated to the receiver.
  @discussion This is the rendering API effectively used by the receiver. You can specify a preferred rendering API when initializing a view programmatically (see SCNPreferredRenderingAPI in SCNSceneRenderer.h) or using Interface Builder's SCNView inspector.
  */
-@property(nonatomic, readonly) SCNRenderingAPI renderingAPI NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, readonly) SCNRenderingAPI renderingAPI API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @property context
- @abstract A Core OpenGL render context that is used as the render target (a CGLContextObj on OS X, an EAGLContext on iOS).
+ @abstract A Core OpenGL render context that is used as the render target (a CGLContextObj on macOS, an EAGLContext on iOS).
  */
 @property(nonatomic, readonly, nullable) void *context;
 
@@ -223,37 +223,37 @@
  @property currentRenderCommandEncoder
  @abstract The current render command encoder if any. This property is only valid within the SCNSceneRendererDelegate methods and when renderering with Metal. Otherwise it is set to nil.
  */
-@property(nonatomic, readonly, nullable) id <MTLRenderCommandEncoder> currentRenderCommandEncoder NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, readonly, nullable) id <MTLRenderCommandEncoder> currentRenderCommandEncoder API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @property device
  @abstract The metal device of the renderer. This property is only valid on a renderer created with a Metal device. Otherwise it is set to nil.
  */
-@property(nonatomic, readonly, nullable) id <MTLDevice> device NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, readonly, nullable) id <MTLDevice> device API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @property colorPixelFormat
  @abstract The pixel format of the color attachment 0 of the renderer. This property is only valid on a renderer created with a Metal device.
  */
-@property(nonatomic, readonly) MTLPixelFormat colorPixelFormat NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, readonly) MTLPixelFormat colorPixelFormat API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @property depthPixelFormat
  @abstract The pixel format of the depth attachment of the renderer. This property is only valid on a renderer created with a Metal device.
  */
-@property(nonatomic, readonly) MTLPixelFormat depthPixelFormat NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, readonly) MTLPixelFormat depthPixelFormat API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @property stencilPixelFormat
  @abstract The pixel format of the stencil attachment of the renderer. This property is only valid on a renderer created with a Metal device.
  */
-@property(nonatomic, readonly) MTLPixelFormat stencilPixelFormat NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, readonly) MTLPixelFormat stencilPixelFormat API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @property commandQueue
  @abstract The command queue of the renderer. This property is only valid on a renderer created with a Metal device. Otherwise it is set to nil.
  */
-@property(nonatomic, readonly, nullable) id <MTLCommandQueue> commandQueue NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, readonly, nullable) id <MTLCommandQueue> commandQueue API_AVAILABLE(macosx(10.11), ios(9.0));
 
 #endif
 
@@ -262,19 +262,19 @@
  @abstract Contains the instance of audio engine used by the scene.
  @discussion The audio engine can be used to add custom nodes to the audio graph.
  */
-@property(nonatomic, readonly) AVAudioEngine *audioEngine NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, readonly) AVAudioEngine *audioEngine API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @property audioEnvironmentNode
  @abstract Contains the instance of audio environment node used by the scene to spacialize sounds.
  */
-@property(nonatomic, readonly) AVAudioEnvironmentNode *audioEnvironmentNode NS_AVAILABLE(10_11, 9_0) __WATCHOS_PROHIBITED;
+@property(nonatomic, readonly) AVAudioEnvironmentNode *audioEnvironmentNode API_AVAILABLE(macosx(10.11), ios(9.0)) __WATCHOS_PROHIBITED;
 
 /*!
  @property audioListener
  @abstract Use this property to set the audio node to use as the listener position and orientation when rendering positional audio for this scene. The default is nil which means that the current point of view will be used dynamically.
  */
-@property(nonatomic, retain, nullable) SCNNode *audioListener NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, retain, nullable) SCNNode *audioListener API_AVAILABLE(macosx(10.11), ios(9.0));
 
 
 
@@ -296,7 +296,7 @@
  @param time The time at which to update the scene.
  @discussion All modifications done within this method don't go through the transaction model, they are directly applied on the presentation tree.
  */
-- (void)renderer:(id <SCNSceneRenderer>)renderer updateAtTime:(NSTimeInterval)time NS_AVAILABLE(10_10, 8_0);
+- (void)renderer:(id <SCNSceneRenderer>)renderer updateAtTime:(NSTimeInterval)time API_AVAILABLE(macosx(10.10));
 
 /*!
  @method renderer:didApplyAnimationsAtTime:
@@ -305,7 +305,7 @@
  @param time The time at which the animations were applied.
  @discussion All modifications done within this method don't go through the transaction model, they are directly applied on the presentation tree.
  */
-- (void)renderer:(id <SCNSceneRenderer>)renderer didApplyAnimationsAtTime:(NSTimeInterval)time NS_AVAILABLE(10_10, 8_0);
+- (void)renderer:(id <SCNSceneRenderer>)renderer didApplyAnimationsAtTime:(NSTimeInterval)time API_AVAILABLE(macosx(10.10));
 
 /*!
  @method renderer:didSimulatePhysicsAtTime:
@@ -314,7 +314,7 @@
  @param time The time at which the physics were simulated.
  @discussion All modifications done within this method don't go through the transaction model, they are directly applied on the presentation tree.
  */
-- (void)renderer:(id <SCNSceneRenderer>)renderer didSimulatePhysicsAtTime:(NSTimeInterval)time NS_AVAILABLE(10_10, 8_0);
+- (void)renderer:(id <SCNSceneRenderer>)renderer didSimulatePhysicsAtTime:(NSTimeInterval)time API_AVAILABLE(macosx(10.10));
 
 /*!
  @method renderer:willRenderScene:atTime:
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneSource.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneSource.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneSource.h	2016-05-22 05:48:16.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneSource.h	2016-06-26 09:21:12.000000000 +0200
@@ -45,7 +45,7 @@
 	@abstract Enable to try to guess acceptable normals for the vertices if none are given in the file
     @discussion Use this with a boolean value encapsulated in a NSNumber. The default value is NO.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionCreateNormalsIfAbsent NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionCreateNormalsIfAbsent API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @constant SCNSceneSourceLoadingOptionCheckConsistency
@@ -56,7 +56,7 @@
  If the document doesn't pass the consistency check it is then not loaded and an error is returned.
  This is slower, but for security reasons it should be set to YES if you are not sure the files you load are valid and have not been tampered with. 
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionCheckConsistency NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionCheckConsistency API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @constant SCNSceneSourceLoadingOptionFlattenScene
@@ -66,7 +66,7 @@
  SceneKit will attempt to reduce the scene graph by merging the geometries.
  This option is suitable to preview a 3D scene efficiently and when manipulating the scene graph is not needed.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionFlattenScene NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionFlattenScene API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @constant SCNSceneSourceLoadingOptionUseSafeMode
@@ -76,7 +76,7 @@
  SceneKit will forbid network accesses, prevent the loading of resources from arbitrary directories, and will not execute
  any code present in the loaded files.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionUseSafeMode NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionUseSafeMode API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @constant SCNSceneSourceLoadingOptionAssetDirectoryURLs
@@ -86,7 +86,7 @@
  This is recommended if you want to construct your scene source from a data object, not from an URL,
  and need to load resources whose paths are not absolute.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionAssetDirectoryURLs NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionAssetDirectoryURLs API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @constant SCNSceneSourceLoadingOptionOverrideAssetURLs
@@ -95,7 +95,7 @@
  You can force SceneKit to only search for extern resources within the directories specified by the SCNSceneSourceAssetDirectoryURLsKey key.
  This can be useful to load a file and its resources from a specific bundle for instance.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionOverrideAssetURLs NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionOverrideAssetURLs API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @constant SCNSceneSourceLoadingOptionStrictConformance
@@ -104,7 +104,7 @@
 			 enable additional features and make the rendering as close as possible to the original intent. If you pass YES,
              SceneKit will instead only consider features which are part of the file format specification.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionStrictConformance NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionStrictConformance API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @constant SCNSceneSourceLoadingOptionConvertUnitsToMeters
@@ -113,7 +113,7 @@
      For better physics simulation it is recommended to use 1 unit equals to 1 meter.
      This option has no effect if the asset is already compressed by Xcode (use the compression options instead).
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionConvertUnitsToMeters NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionConvertUnitsToMeters API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @constant SCNSceneSourceLoadingOptionConvertToYUp
@@ -121,32 +121,32 @@
  @discussion Use this with a boolean value encapsulated in a NSNumber. The default value is NO.
  This option has no effect if the asset is already compressed by Xcode (use the compression options instead).
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionConvertToYUp NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionConvertToYUp API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @constant SCNSceneSourceLoadingOptionAnimationImportPolicy
  @abstract Pass one of the value below to specify what to do with loaded animations.
  @discussion See below for the description of each individual key. Defaults to SCNSceneSourceAnimationImportPolicyPlayRepeatedly. On 10.9 and before the behavior is SCNSceneSourceAnimationImportPolicyPlayUsingSceneTimeBase. For compatibility reason if the application was built on 10.9 or before the default behavior is SCNSceneSourceAnimationImportPolicyPlayUsingSceneTimeBase.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionAnimationImportPolicy NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionAnimationImportPolicy API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @constant SCNSceneSourceLoadingOptionPreserveOriginalTopology
  @abstract Pass YES to make SceneKit preserve the original topology instead of triangulating at load time.
  This can be useful to get better results when subdividing a geometry. Defaults to NO.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionPreserveOriginalTopology NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionPreserveOriginalTopology API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 FOUNDATION_EXTERN NSString * const SCNSceneSourceCreateNormalsIfAbsentKey;                          // Please use SCNSceneSourceLoadingOption.createNormalsIfAbsent instead.
-FOUNDATION_EXTERN NSString * const SCNSceneSourceCheckConsistencyKey;                               // Please use SCNSceneSourceLoadingOption.createNormalsIfAbsent instead.
+FOUNDATION_EXTERN NSString * const SCNSceneSourceCheckConsistencyKey;                               // Please use SCNSceneSourceLoadingOption.checkConsistency instead.
 FOUNDATION_EXTERN NSString * const SCNSceneSourceFlattenSceneKey;                                   // Please use SCNSceneSourceLoadingOption.flattenScene instead.
 FOUNDATION_EXTERN NSString * const SCNSceneSourceUseSafeModeKey;                                    // Please use SCNSceneSourceLoadingOption.useSafeMode instead.
 FOUNDATION_EXTERN NSString * const SCNSceneSourceAssetDirectoryURLsKey;                             // Please use SCNSceneSourceLoadingOption.assetDirectoryURLs instead.
 FOUNDATION_EXTERN NSString * const SCNSceneSourceOverrideAssetURLsKey;                              // Please use SCNSceneSourceLoadingOption.overrideAssetURLs instead.
 FOUNDATION_EXTERN NSString * const SCNSceneSourceStrictConformanceKey;                              // Please use SCNSceneSourceLoadingOption.strictConformance instead.
-FOUNDATION_EXTERN NSString * const SCNSceneSourceConvertUnitsToMetersKey NS_AVAILABLE(10_10, NA);   // Please use SCNSceneSourceLoadingOption.convertUnitsToMeters instead.
-FOUNDATION_EXTERN NSString * const SCNSceneSourceConvertToYUpKey NS_AVAILABLE(10_10, NA);           // Please use SCNSceneSourceLoadingOption.convertUnitsToMeters instead.
-FOUNDATION_EXTERN NSString * const SCNSceneSourceAnimationImportPolicyKey NS_AVAILABLE(10_10, 8_0); // Please use SCNSceneSourceLoadingOption.animationImportPolicy instead.
+FOUNDATION_EXTERN NSString * const SCNSceneSourceConvertUnitsToMetersKey API_AVAILABLE(macosx(10.10), ios(NA));   // Please use SCNSceneSourceLoadingOption.convertUnitsToMeters instead.
+FOUNDATION_EXTERN NSString * const SCNSceneSourceConvertToYUpKey API_AVAILABLE(macosx(10.10), ios(NA));           // Please use SCNSceneSourceLoadingOption.convertToYUp instead.
+FOUNDATION_EXTERN NSString * const SCNSceneSourceAnimationImportPolicyKey API_AVAILABLE(macosx(10.10)); // Please use SCNSceneSourceLoadingOption.animationImportPolicy instead.
 
 
 /* Values for SCNSceneSourceLoadingOptionAnimationImportPolicy */
@@ -160,25 +160,25 @@
  @constant SCNSceneSourceAnimationImportPolicyPlay
  @abstract Add animations to the scene and play them once (repeatCount set to 1).
  */
-FOUNDATION_EXTERN SCNSceneSourceAnimationImportPolicy const SCNSceneSourceAnimationImportPolicyPlay NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNSceneSourceAnimationImportPolicy const SCNSceneSourceAnimationImportPolicyPlay API_AVAILABLE(macosx(10.10));
 
 /*!
  @constant SCNSceneSourceAnimationImportPolicyPlayRepeatedly
  @abstract Add animations to the scene and play them repeatedly (repeatCount set to infinity).
  */
-FOUNDATION_EXTERN SCNSceneSourceAnimationImportPolicy const SCNSceneSourceAnimationImportPolicyPlayRepeatedly NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNSceneSourceAnimationImportPolicy const SCNSceneSourceAnimationImportPolicyPlayRepeatedly API_AVAILABLE(macosx(10.10));
 
 /*!
  @constant SCNSceneSourceAnimationImportPolicyDoNotPlay
  @abstract Only keep animations in the SCNSceneSource and don't add to the animatable elements of the scene.
  */
-FOUNDATION_EXTERN SCNSceneSourceAnimationImportPolicy const SCNSceneSourceAnimationImportPolicyDoNotPlay NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNSceneSourceAnimationImportPolicy const SCNSceneSourceAnimationImportPolicyDoNotPlay API_AVAILABLE(macosx(10.10));
 
 /*!
  @constant SCNSceneSourceAnimationImportPolicyPlayUsingSceneTimeBase
  @abstract Add animations to the scene and play them using the SCNView/SCNRenderer's scene time (usesSceneTimeBase set to YES)
  */
-FOUNDATION_EXTERN SCNSceneSourceAnimationImportPolicy const SCNSceneSourceAnimationImportPolicyPlayUsingSceneTimeBase NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNSceneSourceAnimationImportPolicy const SCNSceneSourceAnimationImportPolicyPlayUsingSceneTimeBase API_AVAILABLE(macosx(10.10));
 
 
 /*!
@@ -251,7 +251,6 @@
  After creating a SCNSceneSource object for the appropriate source, you can obtain scenes using SCNSceneSource methods.
  */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNSceneSource : NSObject 
 
 /*!
@@ -353,7 +352,7 @@
  @param predicate The block to apply to entries in the library. The block takes three arguments: "entry" is an entry in the library, "identifier" is the ID of this entry and "stop" is a reference to a Boolean value. The block can set the value to YES to stop further processing of the library. The stop argument is an out-only argument. You should only ever set this Boolean to YES within the Block. The Block returns a Boolean value that indicates whether "entry" passed the test.
  @discussion The entry is an instance of one of following classes: SCNMaterial, SCNScene, SCNGeometry, SCNNode, CAAnimation, SCNLight, SCNCamera, SCNSkinner, SCNMorpher, NSImage.
  */
-- (NSArray<id> *)entriesPassingTest:(__attribute__((noescape)) BOOL (^)(id entry, NSString *identifier, BOOL *stop))predicate NS_AVAILABLE(10_9, 8_0);
+- (NSArray<id> *)entriesPassingTest:(NS_NOESCAPE BOOL (^)(id entry, NSString *identifier, BOOL *stop))predicate API_AVAILABLE(macosx(10.9));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNShadable.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNShadable.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNShadable.h	2016-05-31 04:56:13.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNShadable.h	2016-06-26 09:42:49.000000000 +0200
@@ -32,7 +32,7 @@
     SCNBufferFrequencyPerFrame    = 0,
     SCNBufferFrequencyPerNode     = 1,
     SCNBufferFrequencyPerShadable = 2 // SCNMaterial or SCNGeometry
-} NS_ENUM_AVAILABLE(10_11, 9_0);
+} API_AVAILABLE(macosx(10.11), ios(9.0));
 
 @protocol SCNBufferStream <NSObject>
 - (void)writeBytes:(void *)bytes length:(NSUInteger)length;
@@ -56,7 +56,7 @@
  @param renderedNode The node currently being rendered.
  @param renderer The renderer that is currently rendering the scene.
  */
-typedef void (^SCNBindingBlock)(unsigned int programID, unsigned int location,  SCNNode * _Nullable renderedNode, SCNRenderer *renderer);
+typedef void (^SCNBindingBlock)(unsigned int programID, unsigned int location, SCNNode * _Nullable renderedNode, SCNRenderer *renderer);
 
 
 /*!
@@ -80,7 +80,7 @@
  @param block The block to call to bind the specified symbol.
  @discussion This method can only be used with OpenGL and OpenGLES based programs.
  */
-- (void)handleBindingOfSymbol:(NSString *)symbol usingBlock:(nullable SCNBindingBlock)block NS_AVAILABLE(10_9, 8_0) __WATCHOS_PROHIBITED;
+- (void)handleBindingOfSymbol:(NSString *)symbol usingBlock:(nullable SCNBindingBlock)block API_AVAILABLE(macosx(10.9)) __WATCHOS_PROHIBITED;
 
 /*!
  @method handleUnbindingOfSymbol:usingBlock:
@@ -89,7 +89,7 @@
  @param block The block to call to unbind the specified symbol.
  @discussion This method can only be used with OpenGL and OpenGLES based programs.
  */
-- (void)handleUnbindingOfSymbol:(NSString *)symbol usingBlock:(nullable SCNBindingBlock)block NS_AVAILABLE(10_9, 8_0) __WATCHOS_PROHIBITED;
+- (void)handleUnbindingOfSymbol:(NSString *)symbol usingBlock:(nullable SCNBindingBlock)block API_AVAILABLE(macosx(10.9)) __WATCHOS_PROHIBITED;
 
 /*!
  @property shaderModifiers
@@ -155,7 +155,7 @@
  
  SceneKit declares the following built-in uniforms:
  float u_time;                               // The current time, in seconds
- vec2  u_inverseResolution;                 // 1./screen size (available on iOS 9 and OS X 10.11)
+ vec2  u_inverseResolution;                  // 1./screen size (available since iOS 9 and macOS 10.11)
  -------------------------------------------------------------------------------------
  mat4  u_modelTransform                      // See SCNModelTransform
  mat4  u_viewTransform                       // See SCNViewTransform
@@ -179,9 +179,9 @@
  4. fragment
  See below for a detailed explanation of these entry points and the context they provide.
  
- Shader modifiers can be written in GLSL or Metal. Metal shaders won't run on iOS8 and OS X 10.10 or below.
+ Shader modifiers can be written in GLSL or Metal. Metal shaders won't run on iOS 8 and macOS 10.10 or below.
  */
-@property(nonatomic, copy, nullable) NSDictionary<SCNShaderModifierEntryPoint, NSString *> *shaderModifiers NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic, copy, nullable) NSDictionary<SCNShaderModifierEntryPoint, NSString *> *shaderModifiers API_AVAILABLE(macosx(10.9));
 
 @end
 
@@ -196,7 +196,7 @@
  @class SCNProgram
  @abstract A SCNProgram lets you specify custom shaders to use when rendering materials.
  */
-NS_CLASS_AVAILABLE(10_8, 8_0) __WATCHOS_PROHIBITED
+__WATCHOS_PROHIBITED
 @interface SCNProgram : NSObject <NSCopying, NSSecureCoding>
 
 /*!
@@ -223,14 +223,14 @@
  @abstract Determines the receiver's vertex function name.
  @discussion The name of the vertex function (for Metal programs).
  */
-@property(nonatomic, copy, nullable) NSString *vertexFunctionName NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, copy, nullable) NSString *vertexFunctionName API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @property fragmentFunctionName
  @abstract Determines the receiver's fragment function name.
  @discussion The name of the fragment function (for Metal programs).
  */
-@property(nonatomic, copy, nullable) NSString *fragmentFunctionName NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, copy, nullable) NSString *fragmentFunctionName API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @method handleBindingOfBufferNamed:frequency:usingBlock:
@@ -240,14 +240,14 @@
  @param block The block that binds the buffer.
  @discussion This method can only be used with Metal based programs.
  */
-- (void)handleBindingOfBufferNamed:(NSString *)name frequency:(SCNBufferFrequency)frequency usingBlock:(SCNBufferBindingBlock)block NS_AVAILABLE(10_11, 9_0);
+- (void)handleBindingOfBufferNamed:(NSString *)name frequency:(SCNBufferFrequency)frequency usingBlock:(SCNBufferBindingBlock)block API_AVAILABLE(macosx(10.11), ios(9.0));
 
 
 /*!
  @property opaque
  @abstract Determines the receiver's fragment are opaque or not. Defaults to YES.
  */
-@property(nonatomic, getter=isOpaque) BOOL opaque NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic, getter=isOpaque) BOOL opaque API_AVAILABLE(macosx(10.10));
 
 /*!
  @method setSemantic:forSymbol:options:
@@ -277,7 +277,7 @@
  @abstract Specifies the metal library to use to locate the function names specified above. 
  @discussion If set to nil the default library is used. Defaults to nil.
  */
-@property(nonatomic, retain, nullable) id <MTLLibrary> library NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, retain, nullable) id <MTLLibrary> library API_AVAILABLE(macosx(10.11), ios(9.0));
 
 @end
 
@@ -304,7 +304,7 @@
  @param program The queried program.
  @discussion This is deprecated. Use SCNProgram's opaque property instead.
  */
-- (BOOL)programIsOpaque:(SCNProgram *)program NS_DEPRECATED(10_8, 10_10, NA, NA);
+- (BOOL)programIsOpaque:(SCNProgram *)program API_DEPRECATED("Use SCNProgram.opaque instead", macosx(10.8, 10.10)) API_UNAVAILABLE(ios, watchos, tvos);
 
 @end
 
@@ -342,7 +342,7 @@
  uniform float Amplitude = 0.1
  _geometry.position.xyz += _geometry.normal * (Amplitude*_geometry.position.y*_geometry.position.x) * sin(u_time);
  */
-FOUNDATION_EXTERN SCNShaderModifierEntryPoint const SCNShaderModifierEntryPointGeometry NS_AVAILABLE(10_9, 8_0);
+FOUNDATION_EXTERN SCNShaderModifierEntryPoint const SCNShaderModifierEntryPointGeometry API_AVAILABLE(macosx(10.9));
 
 /*!
  @constant SCNShaderModifierEntryPointSurface
@@ -355,6 +355,7 @@
  |    vec3 view;                // Direction from the point on the surface toward the camera (V)
  |    vec3 position;            // Position of the fragment
  |    vec3 normal;              // Normal of the fragment (N)
+ |    vec3 geometryNormal;      // Geometric normal of the fragment (normal map is ignored)
  |    vec3 tangent;             // Tangent of the fragment
  |    vec3 bitangent;           // Bitangent of the fragment
  |    vec4 ambient;             // Ambient property of the fragment
@@ -398,7 +399,7 @@
  f1 = f1 * f1 * 2.0 * (3. * 2. * f1);
  _surface.diffuse = mix(vec4(1.0), vec4(0.0), f1);
  */
-FOUNDATION_EXTERN SCNShaderModifierEntryPoint const SCNShaderModifierEntryPointSurface NS_AVAILABLE(10_9, 8_0);
+FOUNDATION_EXTERN SCNShaderModifierEntryPoint const SCNShaderModifierEntryPointSurface API_AVAILABLE(macosx(10.9));
 
 /*!
  @constant SCNShaderModifierEntryPointLightingModel
@@ -439,7 +440,7 @@
  dotProduct = max(0.0, pow(max(0.0, dot(_surface.normal, halfVector)), _surface.shininess));
  _lightingContribution.specular += (dotProduct * _light.intensity.rgb);
  */
-FOUNDATION_EXTERN SCNShaderModifierEntryPoint const SCNShaderModifierEntryPointLightingModel NS_AVAILABLE(10_9, 8_0);
+FOUNDATION_EXTERN SCNShaderModifierEntryPoint const SCNShaderModifierEntryPointLightingModel API_AVAILABLE(macosx(10.9));
 
 /*!
  @constant SCNShaderModifierEntryPointFragment
@@ -464,6 +465,6 @@
  
  _output.color.rgb = vec3(1.0) - _output.color.rgb;
  */
-FOUNDATION_EXTERN SCNShaderModifierEntryPoint const SCNShaderModifierEntryPointFragment NS_AVAILABLE(10_9, 8_0);
+FOUNDATION_EXTERN SCNShaderModifierEntryPoint const SCNShaderModifierEntryPointFragment API_AVAILABLE(macosx(10.9));
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSkinner.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSkinner.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSkinner.h	2016-05-31 05:16:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSkinner.h	2016-06-26 08:35:21.000000000 +0200
@@ -16,7 +16,7 @@
  @class SCNSkinner
  @abstract SCNSkinner controls the deformation of skinned geometries */
 
-NS_CLASS_AVAILABLE(10_9, 8_0)
+API_AVAILABLE(macosx(10.9))
 @interface SCNSkinner : NSObject <NSSecureCoding>
 
 /*!
@@ -35,7 +35,7 @@
  @param boneWeights A buffer of weights. This contains the weights of every influence of every vertex. The number of influence per vertex is controlled by the number of component in the geometry source.
  @param boneIndices A buffer of bone indexes. This buffer contains the corresponding index in the bones array for every weight in the weights buffer.
  */
-+ (instancetype)skinnerWithBaseGeometry:(nullable SCNGeometry *)baseGeometry bones:(NSArray<SCNNode *> *)bones boneInverseBindTransforms:(nullable NSArray<NSValue *> *)boneInverseBindTransforms boneWeights:(SCNGeometrySource *)boneWeights boneIndices:(SCNGeometrySource *)boneIndices NS_AVAILABLE(10_10, 8_0);
++ (instancetype)skinnerWithBaseGeometry:(nullable SCNGeometry *)baseGeometry bones:(NSArray<SCNNode *> *)bones boneInverseBindTransforms:(nullable NSArray<NSValue *> *)boneInverseBindTransforms boneWeights:(SCNGeometrySource *)boneWeights boneIndices:(SCNGeometrySource *)boneIndices API_AVAILABLE(macosx(10.10));
 
 /*!
  @property baseGeometry
@@ -45,38 +45,38 @@
  Access this property if you want a whole new geometry (which will necessarily be shared among the skinner instances), with
  different sources, for instance.
  */
-@property(retain, nonatomic, nullable) SCNGeometry *baseGeometry NS_AVAILABLE(10_9, 8_0);
+@property(retain, nonatomic, nullable) SCNGeometry *baseGeometry API_AVAILABLE(macosx(10.9));
 
 /*!
  @property baseGeometryBindTransform
  @abstract Specifies the transform of the baseGeometry at the time when the mesh was bound to a skeleton. This transforms the baseGeometry from object space to a space on which the skinning then applies.
  */
-@property(nonatomic) SCNMatrix4 baseGeometryBindTransform NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) SCNMatrix4 baseGeometryBindTransform API_AVAILABLE(macosx(10.10));
 
 /*!
  @property boneInverseBindTransforms
  @abstract The inverse of the bone’s bind-space transformation matrix at the time the bind shape was bound to this bone.
  @discussion boneInverseBindTransforms is an array of SCNMatrix4 wrapped into instances of NSValue.
  */
-@property(readonly, nonatomic, nullable) NSArray<NSValue *> *boneInverseBindTransforms NS_AVAILABLE(10_10, 8_0);
+@property(readonly, nonatomic, nullable) NSArray<NSValue *> *boneInverseBindTransforms API_AVAILABLE(macosx(10.10));
 
 /*!
  @property bones
  @abstract The bones of the skinner.
  */
-@property(readonly, nonatomic) NSArray<SCNNode *> *bones NS_AVAILABLE(10_10, 8_0);
+@property(readonly, nonatomic) NSArray<SCNNode *> *bones API_AVAILABLE(macosx(10.10));
 
 /*!
  @property boneWeights
  @abstract The bone weights of the receiver.
  */
-@property(readonly, nonatomic) SCNGeometrySource *boneWeights NS_AVAILABLE(10_10, 8_0);
+@property(readonly, nonatomic) SCNGeometrySource *boneWeights API_AVAILABLE(macosx(10.10));
 
 /*!
  @property boneIndices
  @abstract The bone indices of the receiver.
  */
-@property(readonly, nonatomic) SCNGeometrySource *boneIndices NS_AVAILABLE(10_10, 8_0);
+@property(readonly, nonatomic) SCNGeometrySource *boneIndices API_AVAILABLE(macosx(10.10));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNTechnique.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNTechnique.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNTechnique.h	2016-05-31 04:56:13.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNTechnique.h	2016-06-26 09:42:49.000000000 +0200
@@ -14,7 +14,7 @@
  @abstract SCNTechnique represents a rendering process that may require multiple passes.
  @discussion A technique is generally initialized from a Property List file. It can be set to any object that conforms to the SCNTechniqueSupport protocol.
  */
-NS_CLASS_AVAILABLE(10_10, 8_0)
+API_AVAILABLE(macosx(10.10))
 @interface SCNTechnique : NSObject <SCNAnimatable, NSCopying, NSSecureCoding>
 
 /*!
@@ -254,12 +254,12 @@
  vec4          | SCNVector4
  mat4, mat44   | SCNMatrix4
  
- On OS X 10.11 or later and iOS 9 or later you can also use the object subscripting syntax to set values to uniforms.
+ On macOS 10.11 or later and iOS 9 or later you can also use the object subscripting syntax to set values to uniforms.
  For example:
  myTechnique[@"myAmplitude"] = aValue;
  */
-- (nullable id)objectForKeyedSubscript:(id)key NS_AVAILABLE(10_11, 9_0);
-- (void)setObject:(nullable id)obj forKeyedSubscript:(id <NSCopying>)key NS_AVAILABLE(10_11, 9_0);
+- (nullable id)objectForKeyedSubscript:(id)key API_AVAILABLE(macosx(10.11), ios(9.0));
+- (void)setObject:(nullable id)obj forKeyedSubscript:(id <NSCopying>)key API_AVAILABLE(macosx(10.11), ios(9.0));
 
 @end
 
@@ -275,7 +275,7 @@
  @property technique
  @abstract Specifies the technique of the receiver. Defaults to nil.
  */
-@property(nonatomic, copy, nullable) SCNTechnique *technique NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic, copy, nullable) SCNTechnique *technique API_AVAILABLE(macosx(10.10));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNTransaction.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNTransaction.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNTransaction.h	2016-05-31 05:16:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNTransaction.h	2016-06-26 08:35:21.000000000 +0200
@@ -14,7 +14,6 @@
  * operations into atomic updates. Every
  * modification to the scene graph requires a transaction to be part of. */
 
-NS_CLASS_AVAILABLE(10_8, 8_0)
 @interface SCNTransaction : NSObject
 
 /* Begin a new transaction for the current thread; nests. */
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNView.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNView.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNView.h	2016-05-31 05:16:41.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNView.h	2016-06-26 08:35:21.000000000 +0200
@@ -21,23 +21,23 @@
  @constant SCNViewOptionPreferredRenderingAPI Specifies the preferred rendering API to be used by the renderer.
  @discussion Pass it as the key in the options dictionary given to initWithFrame:options:. The value is a NSNumber wrapping a SCNRenderingAPI. You can also select the preferred rendering API directly from the SCNView inspector in InterfaceBuilder.
  */
-FOUNDATION_EXTERN SCNViewOption const SCNViewOptionPreferredRenderingAPI NS_AVAILABLE(10_12, 10_0) __WATCHOS_UNAVAILABLE;
+FOUNDATION_EXTERN SCNViewOption const SCNViewOptionPreferredRenderingAPI API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)) __WATCHOS_UNAVAILABLE;
 
 /*!
  @constant SCNViewOptionPreferredDevice Specifies the preferred metal device to be used by the renderer.
  @discussion The value is directly a id <MTLDevice>.
  */
-FOUNDATION_EXTERN SCNViewOption const SCNViewOptionPreferredDevice NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNViewOption const SCNViewOptionPreferredDevice API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
 /*!
  @constant SCNViewOptionPreferLowPowerDevice Specifies if the renderer should prefer a low power metal device.
  @discussion The value is a NSNumber wrapping a BOOL. Defaults to NO.
  */
-FOUNDATION_EXTERN SCNViewOption const SCNViewOptionPreferLowPowerDevice NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNViewOption const SCNViewOptionPreferLowPowerDevice API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
-FOUNDATION_EXTERN NSString * const SCNPreferredRenderingAPIKey NS_AVAILABLE(10_11, 9_0) __WATCHOS_UNAVAILABLE; // Please use SCNViewOption.preferredRenderingAPI instead.
-FOUNDATION_EXTERN NSString * const SCNPreferredDeviceKey NS_AVAILABLE(10_11, 9_0);                             // Please use SCNViewOption.preferredDevice instead.
-FOUNDATION_EXTERN NSString * const SCNPreferLowPowerDeviceKey NS_AVAILABLE(10_11, 9_0);                        // Please use SCNViewOption.preferLowPowerDevice instead.
+FOUNDATION_EXTERN NSString * const SCNPreferredRenderingAPIKey API_AVAILABLE(macosx(10.11), ios(9.0)) __WATCHOS_UNAVAILABLE; // Please use SCNViewOption.preferredRenderingAPI instead.
+FOUNDATION_EXTERN NSString * const SCNPreferredDeviceKey API_AVAILABLE(macosx(10.11), ios(9.0));                             // Please use SCNViewOption.preferredDevice instead.
+FOUNDATION_EXTERN NSString * const SCNPreferLowPowerDeviceKey API_AVAILABLE(macosx(10.11), ios(9.0));                        // Please use SCNViewOption.preferLowPowerDevice instead.
 
 
 /*!
@@ -74,7 +74,7 @@
  @abstract Draws the contents of the view and returns them as a new image object
  @discussion This method is thread-safe and may be called at any time.
  */
-- (UIImage *)snapshot NS_AVAILABLE(10_10, 8_0);
+- (UIImage *)snapshot API_AVAILABLE(macosx(10.10));
 
 /*! 
  @functiongroup Actions
@@ -108,7 +108,7 @@
  @discussion When your application sets its preferred frame rate, the view chooses a frame rate as close to that as possible based on the capabilities of the screen the view is displayed on. The actual frame rate chosen is usually a factor of the maximum refresh rate of the screen to provide a consistent frame rate. For example, if the maximum refresh rate of the screen is 60 frames per second, that is also the highest frame rate the view sets as the actual frame rate. However, if you ask for a lower frame rate, it might choose 30, 20, 15 or some other factor to be the actual frame rate. Your application should choose a frame rate that it can consistently maintain.
              The default value is 0 which means the display link will fire at the native cadence of the display hardware.
  */
-@property(nonatomic) NSInteger preferredFramesPerSecond NS_AVAILABLE(10_12, 8_0);
+@property(nonatomic) NSInteger preferredFramesPerSecond API_AVAILABLE(macosx(10.12));
 
 /*!
  @property eaglContext
@@ -119,9 +119,9 @@
 
 /*!
  @property antialiasingMode
- @abstract Defaults to SCNAntialiasingModeMultisampling4X on OSX and SCNAntialiasingModeNone on iOS.
+ @abstract Defaults to SCNAntialiasingModeMultisampling4X on macOS and SCNAntialiasingModeNone on iOS.
  */
-@property(nonatomic) SCNAntialiasingMode antialiasingMode NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic) SCNAntialiasingMode antialiasingMode API_AVAILABLE(macosx(10.10));
 
 
 @end
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKitTypes.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKitTypes.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKitTypes.h	2016-05-31 04:56:02.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKitTypes.h	2016-06-26 09:21:12.000000000 +0200
@@ -30,10 +30,10 @@
 } SCNVector4;
 
 /* The null vector: [0 0 0]. */
-FOUNDATION_EXTERN const SCNVector3 SCNVector3Zero NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN const SCNVector3 SCNVector3Zero API_AVAILABLE(macosx(10.10));
 
 /* The null vector: [0 0 0 0]. */
-FOUNDATION_EXTERN const SCNVector4 SCNVector4Zero NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN const SCNVector4 SCNVector4Zero API_AVAILABLE(macosx(10.10));
 
 /* Returns true if 'a' is exactly equal to 'b'. */
 FOUNDATION_EXTERN bool SCNVector3EqualToVector3 (SCNVector3 a, SCNVector3 b);
@@ -69,13 +69,13 @@
 } SCNMatrix4;
 
 /* The identity matrix: [1 0 0 0; 0 1 0 0; 0 0 1 0; 0 0 0 1]. */
-FOUNDATION_EXTERN const SCNMatrix4 SCNMatrix4Identity NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN const SCNMatrix4 SCNMatrix4Identity API_AVAILABLE(macosx(10.10));
 
 /* Returns true if 'm' is the identity matrix. */
-FOUNDATION_EXTERN bool SCNMatrix4IsIdentity(SCNMatrix4 m) NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN bool SCNMatrix4IsIdentity(SCNMatrix4 m) API_AVAILABLE(macosx(10.10));
 
 /* Returns true if 'a' is exactly equal to 'b'. */
-FOUNDATION_EXTERN bool SCNMatrix4EqualToMatrix4(SCNMatrix4 a, SCNMatrix4 b) NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN bool SCNMatrix4EqualToMatrix4(SCNMatrix4 a, SCNMatrix4 b) API_AVAILABLE(macosx(10.10));
 
 /* Returns a transform that translates by '(tx, ty, tz)':
  * m' =  [1 0 0 0; 0 1 0 0; 0 0 1 0; tx ty tz 1]. */
@@ -98,7 +98,7 @@
 }
 
 /* Returns a matrix that rotates by 'angle' radians about the vector '(x, y, z)'. */
-FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4MakeRotation(float angle, float x, float y, float z) NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4MakeRotation(float angle, float x, float y, float z) API_AVAILABLE(macosx(10.10));
 
 /* Translate 'm' by '(tx, ty, tz)' and return the result:
  * m' = translate(tx, ty, tz) * m. */
@@ -111,17 +111,17 @@
 
 /* Scale 'm' by '(sx, sy, sz)' and return the result:
  * m' = scale(sx, sy, sz) * m. */
-FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4Scale(SCNMatrix4 m, float sx, float sy, float sz) NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4Scale(SCNMatrix4 m, float sx, float sy, float sz) API_AVAILABLE(macosx(10.10));
 
 /* Rotate 'm' by 'angle' radians about the vector '(x, y, z)' and return the result:
  * m' = rotation(angle, x, y, z) * m. */
-FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4Rotate(SCNMatrix4 m, float angle, float x, float y, float z) NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4Rotate(SCNMatrix4 m, float angle, float x, float y, float z) API_AVAILABLE(macosx(10.10));
 
 /* Invert 'm' and return the result. */
-FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4Invert(SCNMatrix4 m) NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4Invert(SCNMatrix4 m) API_AVAILABLE(macosx(10.10));
 
 /* Concatenate 'b' to 'a' and return the result: m' = a * b. */
-FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4Mult(SCNMatrix4 a, SCNMatrix4 b) NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4Mult(SCNMatrix4 a, SCNMatrix4 b) API_AVAILABLE(macosx(10.10));
 
 
 #pragma mark - GLKit Bridge
@@ -146,8 +146,8 @@
     return v;
 }
 
-FOUNDATION_EXTERN GLKMatrix4 SCNMatrix4ToGLKMatrix4(SCNMatrix4 mat) NS_AVAILABLE(10_10, 8_0);
-FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4FromGLKMatrix4(GLKMatrix4 mat) NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN GLKMatrix4 SCNMatrix4ToGLKMatrix4(SCNMatrix4 mat) API_AVAILABLE(macosx(10.10));
+FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4FromGLKMatrix4(GLKMatrix4 mat) API_AVAILABLE(macosx(10.10));
 
 
 #pragma mark - SIMD Bridge
@@ -202,11 +202,11 @@
 
 + (NSValue *)valueWithSCNVector3:(SCNVector3)v;
 + (NSValue *)valueWithSCNVector4:(SCNVector4)v;
-+ (NSValue *)valueWithSCNMatrix4:(SCNMatrix4)v NS_AVAILABLE(10_10, 8_0);
++ (NSValue *)valueWithSCNMatrix4:(SCNMatrix4)v API_AVAILABLE(macosx(10.10));
 
 @property(nonatomic, readonly) SCNVector3 SCNVector3Value;
 @property(nonatomic, readonly) SCNVector4 SCNVector4Value;
-@property(nonatomic, readonly) SCNMatrix4 SCNMatrix4Value NS_AVAILABLE(10_10, 8_0);
+@property(nonatomic, readonly) SCNMatrix4 SCNMatrix4Value API_AVAILABLE(macosx(10.10));
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/scn_metal /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/scn_metal
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/scn_metal	2016-05-31 05:16:49.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/scn_metal	2016-06-26 08:35:21.000000000 +0200
@@ -34,7 +34,7 @@
     float       sinTime;
     float       cosTime;
     float       random01;
-    // new in OSX 10.12 / iOS 10.0
+    // new in macOS 10.12 and iOS 10
     float       environmentIntensity;
     float4x4    inverseProjectionTransform;
     float4x4    inverseViewProjectionTransform;

```