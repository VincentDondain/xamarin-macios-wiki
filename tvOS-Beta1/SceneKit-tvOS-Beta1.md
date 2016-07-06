#SceneKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/ModelIO.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/ModelIO.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/ModelIO.h	2015-09-30 23:36:44.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/ModelIO.h	2016-05-31 05:16:49.000000000 +0200
@@ -1,7 +1,7 @@
 //
 //  ModelIO.h
 //
-//  Copyright (c) 2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2015-2016 Apple Inc. All rights reserved.
 //
 
 #import <ModelIO/ModelIO.h>
@@ -19,6 +19,7 @@
 
 @interface MDLAsset (SCNModelIO)
 + (instancetype)assetWithSCNScene:(SCNScene *)scnScene NS_AVAILABLE(10_11, 9_0);
++ (instancetype)assetWithSCNScene:(SCNScene *)scnScene bufferAllocator:(nullable id <MDLMeshBufferAllocator>)bufferAllocator NS_AVAILABLE(10_12, 10_0);
 @end
 
 @interface SCNNode (SCNModelIO)
@@ -27,6 +28,7 @@
 
 @interface MDLObject (SCNModelIO)
 + (instancetype)objectWithSCNNode:(SCNNode *)scnNode NS_AVAILABLE(10_11, 9_0);
++ (instancetype)objectWithSCNNode:(SCNNode *)scnNode bufferAllocator:(nullable id <MDLMeshBufferAllocator>)bufferAllocator NS_AVAILABLE(10_12, 10_0);
 @end
 
 @interface SCNGeometry (SCNModelIO)
@@ -35,6 +37,7 @@
 
 @interface MDLMesh (SCNModelIO)
 + (instancetype)meshWithSCNGeometry:(SCNGeometry *)scnGeometry NS_AVAILABLE(10_11, 9_0);
++ (instancetype)meshWithSCNGeometry:(SCNGeometry *)scnGeometry bufferAllocator:(nullable id <MDLMeshBufferAllocator>)bufferAllocator NS_AVAILABLE(10_12, 10_0);
 @end
 
 @interface SCNGeometryElement (SCNModelIO)
@@ -43,6 +46,7 @@
 
 @interface MDLSubmesh (SCNModelIO)
 + (instancetype)submeshWithSCNGeometryElement:(SCNGeometryElement *)scnGeometryElement NS_AVAILABLE(10_11, 9_0);
++ (instancetype)submeshWithSCNGeometryElement:(SCNGeometryElement *)scnGeometryElement bufferAllocator:(nullable id <MDLMeshBufferAllocator>)bufferAllocator NS_AVAILABLE(10_12, 10_0);
 @end
 
 @interface SCNMaterial (SCNModelIO)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNAnimation.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNAnimation.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNAnimation.h	2015-09-30 23:36:44.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNAnimation.h	2016-05-31 04:56:13.000000000 +0200
@@ -1,7 +1,7 @@
 //
 //  SCNAnimation.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <QuartzCore/QuartzCore.h>
@@ -104,6 +104,14 @@
  */
 - (void)removeAnimationForKey:(NSString *)key fadeOutDuration:(CGFloat)duration NS_AVAILABLE(10_10, 8_0);
 
+/*!
+ @method setSpeed:forAnimationKey:
+ @abstract Update the animation speed of the animation with the given identifier.
+ @param speed The new speed of the animation.
+ @param key The identifier for the animation to update.
+ */
+- (void)setSpeed:(CGFloat)speed forAnimationKey:(NSString *)key NS_AVAILABLE(10_12, 10_0);
+
 @end
 
 /*!
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNAudioSource.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNAudioSource.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNAudioSource.h	2015-09-30 23:36:44.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNAudioSource.h	2016-05-22 05:48:21.000000000 +0200
@@ -1,10 +1,10 @@
 //
 //  SCNAudioSource.h
 //
-//  Copyright (c) 2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2015-2016 Apple Inc. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
+#import <SceneKit/SCNNode.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBase.h	2015-09-30 23:36:44.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBase.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,15 +0,0 @@
-//
-//  SCNBase.h
-//
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
-//
-
-/*! @header SCNBase
-    @abstract Various defines used throughout SceneKit
- */
-
-#define SCN_EXTERN FOUNDATION_EXTERN
-
-#ifndef __has_feature      // Optional.
-#define __has_feature(x) 0 // Compatibility with non-clang compilers.
-#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBoundingVolume.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBoundingVolume.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBoundingVolume.h	2015-09-30 23:36:44.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBoundingVolume.h	2016-05-31 05:16:49.000000000 +0200
@@ -1,9 +1,11 @@
 //
 //  SCNBoundingVolume.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
+#import <SceneKit/SceneKitTypes.h>
+
 /*!
  @protocol SCNBoundingVolume
  @abstract The SCNBoundingVolume protocol is implemented by objects which can compute their bounding boxes.
@@ -24,14 +26,6 @@
 - (BOOL)getBoundingBoxMin:(nullable SCNVector3 *)min max:(nullable SCNVector3 *)max;
 
 /*!
- @method getBoundingSphereCenter:radius:
- @abstract Fill the center vector with the center of the bounding sphere and store the radius of the bounding sphere in 'radius'.
- @param center A pointer to a SCNVector3 to store the center of the bounding sphere into.
- @param radius A pointer to a CGFloat to store the radius of the bounding sphere into.
- */
-- (BOOL)getBoundingSphereCenter:(nullable SCNVector3 *)center radius:(nullable CGFloat *)radius;
-
-/*!
  @method setBoundingBoxMin:max:
  @abstract Override the receiver bounding box with the min and max vectors provided.
  @param min A pointer to a SCNVector3 representing the min vertex of the desired bounding box.
@@ -40,6 +34,14 @@
  */
 - (void)setBoundingBoxMin:(nullable SCNVector3 *)min max:(nullable SCNVector3 *)max NS_AVAILABLE(10_9, 8_0);
 
+/*!
+ @method getBoundingSphereCenter:radius:
+ @abstract Fill the center vector with the center of the bounding sphere and store the radius of the bounding sphere in 'radius'.
+ @param center A pointer to a SCNVector3 to store the center of the bounding sphere into.
+ @param radius A pointer to a CGFloat to store the radius of the bounding sphere into.
+ */
+- (BOOL)getBoundingSphereCenter:(nullable SCNVector3 *)center radius:(nullable CGFloat *)radius;
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNCamera.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNCamera.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNCamera.h	2015-09-30 23:36:44.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNCamera.h	2016-05-31 04:56:13.000000000 +0200
@@ -1,10 +1,10 @@
 //
 //  SCNCamera.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
+#import <SceneKit/SceneKitTypes.h>
 #import <SceneKit/SCNAnimation.h>
 #import <SceneKit/SCNTechnique.h>
 
@@ -80,11 +80,10 @@
 @property(nonatomic) double orthographicScale NS_AVAILABLE(10_9, 8_0);
 
 /*!
- @method projectionTransform
+ @property projectionTransform
  @abstract Determines the projection transform used by the camera to project the world onscreen. 
  */
-- (SCNMatrix4)projectionTransform;
-- (void)setProjectionTransform:(SCNMatrix4)projectionTransform NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic) SCNMatrix4 projectionTransform;
 
 /*!
  @functiongroup Depth of field
@@ -118,6 +117,130 @@
 @property(nonatomic) CGFloat aperture NS_AVAILABLE(10_9, 8_0);
 
 /*!
+ @property motionBlurIntensity
+ @abstract Determines the intensity of the motion blur. Animatable. Defaults to 0.
+ @discussion An intensity of zero means no motion blur. The intensity should not exceeed 1.
+ */
+@property(nonatomic) CGFloat motionBlurIntensity NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @functiongroup High Dynamic Range
+ */
+/*!
+ @property wantsHDR
+ @abstract Determines if the receiver has a high dynamic range. Defaults to NO.
+ */
+@property(nonatomic) BOOL wantsHDR NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property exposureOffset
+ @abstract Determines the logarithimc exposure biasing, in EV. Defaults to 0.
+ */
+@property(nonatomic) CGFloat exposureOffset NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property averageGray
+ @abstract Determines the average gray level desired in the final image. Defaults to 0.18.
+ */
+@property(nonatomic) CGFloat averageGray NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property whitePoint
+ @abstract Determines the smallest luminance level that will be mapped to white in the final image. Defaults to 1.
+ */
+@property(nonatomic) CGFloat whitePoint NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property wantsExposureAdaptation
+ @abstract Determines if the receiver should simulate an eye and continuously adjust to luminance. Defaults to YES.
+ */
+@property(nonatomic) BOOL wantsExposureAdaptation NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property exposureAdaptationBrighteningSpeedFactor
+ @abstract Determines the exposure adaptation speed when going from bright areas to dark areas. Defaults to 0.4.
+ */
+@property(nonatomic) CGFloat exposureAdaptationBrighteningSpeedFactor NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property exposureAdaptationBrighteningSpeedFactor
+ @abstract Determines the exposure adaptation speed whien going from dark areas to bright areas. Defaults to 0.6.
+ */
+@property(nonatomic) CGFloat exposureAdaptationDarkeningSpeedFactor NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property minimumExposure
+ @abstract Determines the minimum exposure offset of the adaptation, in EV. Defaults to -15.
+ */
+@property(nonatomic) CGFloat minimumExposure NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property maximumExposure
+ @abstract Determines the maximum exposure offset of the adaptation, in EV. Defaults to -15.
+ */
+@property(nonatomic) CGFloat maximumExposure NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property bloomThreshold
+ @abstract Determines the luminance threshold for the bloom effect. Animatable. Defaults to 1.
+ */
+@property(nonatomic) CGFloat bloomThreshold NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property bloomIntensity
+ @abstract Determines the intensity of the bloom effect. Animatable. Defaults to 0 (no effect).
+ */
+@property(nonatomic) CGFloat bloomIntensity NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property bloomBlurRadius
+ @abstract Determines the radius of the bloom effect in pixels. Animatable. Defaults to 4.
+ */
+@property(nonatomic) CGFloat bloomBlurRadius NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property vignettingPower
+ @abstract Controls the shape of the vignetting effect. Defaults to 0 (no effect).
+ */
+@property(nonatomic) CGFloat vignettingPower NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property vignettingIntensity
+ @abstract Controls the intensity of the vignetting effect. Defaults to 0 (no effect).
+ */
+@property(nonatomic) CGFloat vignettingIntensity NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property colorFringeStrength
+ @abstract Controls the strength of the color shift effect. Defaults to 0 (no effect).
+ */
+@property(nonatomic) CGFloat colorFringeStrength NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property colorFringeIntensity
+ @abstract Controls the intensity of the color shift effect. Defaults to 1.
+ */
+@property(nonatomic) CGFloat colorFringeIntensity NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property saturation
+ @abstract Controls the overall saturation of the scene. Defaults to 1 (no effect).
+ */
+@property(nonatomic) CGFloat saturation NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property contrast
+ @abstract Controls the overall contrast of the scene. Defaults to 0 (no effect).
+ */
+@property(nonatomic) CGFloat contrast NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property colorGrading
+ @abstract Specifies a lookup texture to apply color grading. The contents must a 2D image representing `n` slices of a unit color cube texture, arranged in an horizontal row of `n` images. For instance, a color cube of dimension 16x16x16 should be provided as an image of size 256x16.
+ */
+@property(nonatomic, readonly) SCNMaterialProperty *colorGrading NS_AVAILABLE(10_12, 10_0);
+
+/*!
  @property categoryBitMask
  @abstract Determines the node categories that are visible from the receiver. Defaults to all bits set.
  */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNConstraint.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNConstraint.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNConstraint.h	2015-09-30 23:36:44.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNConstraint.h	2016-05-31 04:56:13.000000000 +0200
@@ -1,11 +1,16 @@
 //
 //  SCNConstraint.h
 //
-//  Copyright (c) 2013-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2013-2016 Apple Inc. All rights reserved.
 //
 
+#import <SceneKit/SceneKitTypes.h>
+#import <SceneKit/SCNAnimation.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
+@class SCNNode;
+
 /*!
  @class SCNConstraint
  @abstract A SCNConstraint is an abstract class that represents a single constraint that can be applied to a node.
@@ -35,13 +40,15 @@
  @abstract Creates and returns a SCNLookAtConstraint object with the specified target.
  @param target The target node to look at.
  */
-+ (instancetype)lookAtConstraintWithTarget:(SCNNode *)target;
++ (instancetype)lookAtConstraintWithTarget:(nullable SCNNode *)target;
 
 /*!
  @property target
  @abstract Defines the target node to look at.
  */
-@property(nonatomic, readonly) SCNNode *target;
+@property(nonatomic, retain, nullable) SCNNode *target;
+- (nullable SCNNode *)target;
+- (void)setTarget:(nullable SCNNode *)target NS_AVAILABLE(10_12, 10_0);
 
 /*!
  @property gimbalLockEnabled
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNGeometry.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNGeometry.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNGeometry.h	2015-09-30 23:36:44.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNGeometry.h	2016-05-31 05:16:41.000000000 +0200
@@ -1,10 +1,9 @@
 //
 //  SCNGeometry.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
 #import <SceneKit/SceneKitTypes.h>
 #import <SceneKit/SCNAnimation.h>
 #import <SceneKit/SCNBoundingVolume.h>
@@ -18,20 +17,34 @@
 @protocol MTLBuffer;
 
 typedef NS_ENUM(NSInteger, SCNGeometryPrimitiveType) {
-	SCNGeometryPrimitiveTypeTriangles     = 0,
-	SCNGeometryPrimitiveTypeTriangleStrip = 1,
-	SCNGeometryPrimitiveTypeLine          = 2,
-	SCNGeometryPrimitiveTypePoint         = 3
+	SCNGeometryPrimitiveTypeTriangles                              = 0,
+	SCNGeometryPrimitiveTypeTriangleStrip                          = 1,
+	SCNGeometryPrimitiveTypeLine                                   = 2,
+	SCNGeometryPrimitiveTypePoint                                  = 3,
+#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 2
+    SCNGeometryPrimitiveTypePolygon NS_ENUM_AVAILABLE(10_12, 10_0) = 4
+#endif
 };
 
-SCN_EXTERN NSString * const SCNGeometrySourceSemanticVertex;
-SCN_EXTERN NSString * const SCNGeometrySourceSemanticNormal;
-SCN_EXTERN NSString * const SCNGeometrySourceSemanticColor;
-SCN_EXTERN NSString * const SCNGeometrySourceSemanticTexcoord;
-SCN_EXTERN NSString * const SCNGeometrySourceSemanticVertexCrease NS_AVAILABLE(10_10, 8_0);
-SCN_EXTERN NSString * const SCNGeometrySourceSemanticEdgeCrease NS_AVAILABLE(10_10, 8_0);
-SCN_EXTERN NSString * const SCNGeometrySourceSemanticBoneWeights NS_AVAILABLE(10_10, 8_0);
-SCN_EXTERN NSString * const SCNGeometrySourceSemanticBoneIndices NS_AVAILABLE(10_10, 8_0);
+#if !(defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 2)
+#define SCNGeometryPrimitiveTypePolygon (SCNGeometryPrimitiveType)4
+#endif
+
+#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
+typedef NSString * SCNGeometrySourceSemantic NS_EXTENSIBLE_STRING_ENUM;
+#else
+typedef NSString * SCNGeometrySourceSemantic;
+#endif
+
+FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticVertex;
+FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticNormal;
+FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticColor;
+FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticTexcoord;
+FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticTangent NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticVertexCrease NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticEdgeCrease NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticBoneWeights NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNGeometrySourceSemantic const SCNGeometrySourceSemanticBoneIndices NS_AVAILABLE(10_10, 8_0);
 
 /*!
  @class SCNGeometry
@@ -105,7 +118,7 @@
  @param elements An array of geometry elements. The sort order in the array determines the mapping between materials and geometry elements.
  @discussion A geometry is made of geometry sources (at least vertices) and at least one geometry element. Multiple sources for texture coordinates are accepted. In that case the mappingChannel is implicitly set based on the order of the texture sources, starting at index 0.
 */
-+ (instancetype)geometryWithSources:(NSArray<SCNGeometrySource *> *)sources elements:(NSArray<SCNGeometryElement *> *)elements;
++ (instancetype)geometryWithSources:(NSArray<SCNGeometrySource *> *)sources elements:(nullable NSArray<SCNGeometryElement *> *)elements;
 
 /*!
  @property geometrySources
@@ -119,7 +132,7 @@
  @param semantic The semantic of the geometry sources that should be retrieved.
  @discussion Returns nil if no geometry source is found for the given semantic. May return more than one source, typically for multiple texture coordinate sources.
  */
-- (NSArray<SCNGeometrySource *> *)geometrySourcesForSemantic:(NSString *)semantic;
+- (NSArray<SCNGeometrySource *> *)geometrySourcesForSemantic:(SCNGeometrySourceSemantic)semantic;
 
 /*!
  @property geometryElements
@@ -190,7 +203,7 @@
  @param offset The offset from the beginning of the data. In bytes.
  @param stride The number of bytes from a vector to the next one in the data.
  */
-+ (instancetype)geometrySourceWithData:(NSData *)data semantic:(NSString *)semantic vectorCount:(NSInteger)vectorCount floatComponents:(BOOL)floatComponents componentsPerVector:(NSInteger)componentsPerVector bytesPerComponent:(NSInteger)bytesPerComponent dataOffset:(NSInteger)offset dataStride:(NSInteger)stride;
++ (instancetype)geometrySourceWithData:(NSData *)data semantic:(SCNGeometrySourceSemantic)semantic vectorCount:(NSInteger)vectorCount floatComponents:(BOOL)floatComponents componentsPerVector:(NSInteger)componentsPerVector bytesPerComponent:(NSInteger)bytesPerComponent dataOffset:(NSInteger)offset dataStride:(NSInteger)stride;
 
 /*!
  @method geometrySourceWithVertices:count:
@@ -251,7 +264,7 @@
  }
  
  */
-+ (instancetype)geometrySourceWithBuffer:(id <MTLBuffer>)mtlBuffer vertexFormat:(MTLVertexFormat)vertexFormat semantic:(NSString *)semantic vertexCount:(NSInteger)vertexCount dataOffset:(NSInteger)offset dataStride:(NSInteger)stride NS_AVAILABLE(10_11, 9_0);
++ (instancetype)geometrySourceWithBuffer:(id <MTLBuffer>)mtlBuffer vertexFormat:(MTLVertexFormat)vertexFormat semantic:(SCNGeometrySourceSemantic)semantic vertexCount:(NSInteger)vertexCount dataOffset:(NSInteger)offset dataStride:(NSInteger)stride NS_AVAILABLE(10_11, 9_0);
 #endif
 
 /*! 
@@ -264,7 +277,7 @@
  @property semantic
  @abstract The semantic of the geometry source
  */
-@property(nonatomic, readonly) NSString *semantic;
+@property(nonatomic, readonly) SCNGeometrySourceSemantic semantic;
 
 /*! 
  @property vectorCount
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNHitTest.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNHitTest.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNHitTest.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNHitTest.h	2016-05-22 05:48:21.000000000 +0200
@@ -0,0 +1,83 @@
+//
+//  SCNHitTest.h
+//
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
+//
+
+#import <SceneKit/SceneKitTypes.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class SCNNode;
+
+/*! @group Hit-test options */
+
+#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
+typedef NSString * SCNHitTestOption NS_STRING_ENUM;
+#else
+typedef NSString * SCNHitTestOption;
+#endif
+
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionFirstFoundOnly    NS_AVAILABLE(10_12, 10_0); // If set to YES, returns the first object found. This object is not necessarily the nearest. Defaults to NO.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionSortResults       NS_AVAILABLE(10_12, 10_0); // Determines whether the results should be sorted. If set to YES sorts nearest objects first. Defaults to YES.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionClipToZRange      NS_AVAILABLE(10_12, 10_0); // If set to YES ignores the objects clipped by the zNear/zFar range of the current point of view. Defaults to YES.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionBackFaceCulling   NS_AVAILABLE(10_12, 10_0); // If set to YES ignores the faces not facing to the camera. Defaults to YES.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionBoundingBoxOnly   NS_AVAILABLE(10_12, 10_0); // If set to YES only tests the bounding boxes of the 3D objects. Defaults to NO.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionIgnoreChildNodes  NS_AVAILABLE(10_12, 10_0); // Determines whether the child nodes are ignored. Defaults to NO.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionRootNode          NS_AVAILABLE(10_12, 10_0); // Specifies the root node to use for the hit test. Defaults to the root node of the scene.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionIgnoreHiddenNodes NS_AVAILABLE(10_12, 10_0); // Determines whether hidden nodes should be ignored. Defaults to YES.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionCategoryBitMask   NS_AVAILABLE(10_12, 10_0); // Determines the node categories to test. Defaults to all bits set.
+
+FOUNDATION_EXTERN NSString * const SCNHitTestFirstFoundOnlyKey;                            // Please use SCNHitTestOption.firstFoundOnly instead.
+FOUNDATION_EXTERN NSString * const SCNHitTestSortResultsKey;                               // Please use SCNHitTestOption.sortResults instead.
+FOUNDATION_EXTERN NSString * const SCNHitTestClipToZRangeKey;                              // Please use SCNHitTestOption.clipToZRange instead.
+FOUNDATION_EXTERN NSString * const SCNHitTestBackFaceCullingKey;                           // Please use SCNHitTestOption.backFaceCulling instead.
+FOUNDATION_EXTERN NSString * const SCNHitTestBoundingBoxOnlyKey;                           // Please use SCNHitTestOption.boundingBoxOnly instead.
+FOUNDATION_EXTERN NSString * const SCNHitTestIgnoreChildNodesKey;                          // Please use SCNHitTestOption.ignoreChildNodes instead.
+FOUNDATION_EXTERN NSString * const SCNHitTestRootNodeKey;                                  // Please use SCNHitTestOption.rootNode instead.
+FOUNDATION_EXTERN NSString * const SCNHitTestIgnoreHiddenNodesKey NS_AVAILABLE(10_9, 8_0); // Please use SCNHitTestOption.ignoreHiddenNodes instead.
+
+/*! @class SCNHitTestResult
+ @abstract Results returned by the hit-test methods.
+ */
+
+NS_CLASS_AVAILABLE(10_8, 8_0)
+@interface SCNHitTestResult : NSObject
+
+/*! The node hit. */
+@property(nonatomic, readonly) SCNNode *node;
+
+/*! Index of the geometry hit. */
+@property(nonatomic, readonly) NSInteger geometryIndex;
+
+/*! Index of the face hit. */
+@property(nonatomic, readonly) NSInteger faceIndex;
+
+/*! Intersection point in the node local coordinate system. */
+@property(nonatomic, readonly) SCNVector3 localCoordinates;
+
+/*! Intersection point in the world coordinate system. */
+@property(nonatomic, readonly) SCNVector3 worldCoordinates;
+
+/*! Intersection normal in the node local coordinate system. */
+@property(nonatomic, readonly) SCNVector3 localNormal;
+
+/*! Intersection normal in the world coordinate system. */
+@property(nonatomic, readonly) SCNVector3 worldNormal;
+
+/*! World transform of the node intersected. */
+@property(nonatomic, readonly) SCNMatrix4 modelTransform;
+
+/*! The bone node hit. Only available if the node hit has a SCNSkinner attached. */
+@property(nonatomic, readonly) SCNNode *boneNode NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @method textureCoordinatesWithMappingChannel:
+ @abstract Returns the texture coordinates at the point of intersection, for a given mapping channel.
+ @param channel The texture coordinates source index of the geometry to use. The channel must exists on the geometry otherwise {0,0} will be returned.
+ */
+- (CGPoint)textureCoordinatesWithMappingChannel:(NSInteger)channel;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNJavascript.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNJavascript.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNJavascript.h	2015-09-30 23:36:44.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNJavascript.h	2016-05-31 05:16:49.000000000 +0200
@@ -1,15 +1,14 @@
 //
 //  SCNJavascript.h
 //
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
-#import <JavaScriptCore/JavaScriptCore.h>
 
-NS_ASSUME_NONNULL_BEGIN
+@class JSContext;
 
-#if JSC_OBJC_API_ENABLED
+NS_ASSUME_NONNULL_BEGIN
 
 /*
  @function SCNExportJavaScriptModule
@@ -53,8 +52,6 @@
  aNode.transform = {m11:1, m12:0, m13:0 ... m44:1};
  */
 
-SCN_EXTERN void SCNExportJavaScriptModule(JSContext *context) NS_AVAILABLE(10_10, 8_0);
-
-#endif
+FOUNDATION_EXTERN void SCNExportJavaScriptModule(JSContext *context) NS_AVAILABLE(10_10, 8_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLevelOfDetail.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLevelOfDetail.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLevelOfDetail.h	2015-09-30 23:36:44.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLevelOfDetail.h	2016-05-31 05:16:49.000000000 +0200
@@ -1,7 +1,7 @@
 //
 //  SCNLevelOfDetail.h
 //
-//  Copyright (c) 2013-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2013-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLight.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLight.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLight.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLight.h	2016-05-31 04:56:02.000000000 +0200
@@ -1,7 +1,7 @@
 //
 //  SCNLight.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
@@ -10,20 +10,25 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class SCNMaterialProperty;
+
 /*!
  @group Light Types
  @abstract Describes the various light types available.
  */
 
-/*! @constant SCNLightTypeAmbient Ambient light */
-SCN_EXTERN NSString * const SCNLightTypeAmbient;
-/*! @constant SCNLightTypeOmni Omnidirectional light */
-SCN_EXTERN NSString * const SCNLightTypeOmni;
-/*! @constant SCNLightTypeDirectional Directional light */
-SCN_EXTERN NSString * const SCNLightTypeDirectional;
-/*! @constant SCNLightTypeSpot Spot light */
-SCN_EXTERN NSString * const SCNLightTypeSpot;
-
+#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
+typedef NSString * SCNLightType NS_STRING_ENUM;
+#else
+typedef NSString * SCNLightType;
+#endif
+
+FOUNDATION_EXTERN SCNLightType const SCNLightTypeAmbient;                         // Ambient light
+FOUNDATION_EXTERN SCNLightType const SCNLightTypeOmni;                            // Omnidirectional light
+FOUNDATION_EXTERN SCNLightType const SCNLightTypeDirectional;                     // Directional light
+FOUNDATION_EXTERN SCNLightType const SCNLightTypeSpot;                            // Spot light
+FOUNDATION_EXTERN SCNLightType const SCNLightTypeIES NS_AVAILABLE(10_12, 10_0);   // IES light
+FOUNDATION_EXTERN SCNLightType const SCNLightTypeProbe NS_AVAILABLE(10_12, 10_0); // Light probe
 
 /*! @enum SCNShadowMode
  @abstract The different modes available to compute shadows.
@@ -54,18 +59,32 @@
 /*! 
  @property type
  @abstract Specifies the receiver's type.
- @discussion A light type can be one of the "Light Types" constants. Defaults to SCNLightTypeOmni on iOS 8 and later, and on OSX 10.10 and later (otherwise defaults to SCNLightTypeAmbient).
+ @discussion Defaults to SCNLightTypeOmni on iOS 8 and later, and on OSX 10.10 and later (otherwise defaults to SCNLightTypeAmbient).
  */
-@property(nonatomic, copy) NSString *type;
+@property(nonatomic, copy) SCNLightType type;
 
 /*! 
  @property color
  @abstract Specifies the receiver's color (NSColor or CGColorRef). Animatable. Defaults to white.
- @discussion The initial value is a NSColor.
+ @discussion The initial value is a NSColor. The renderer multiplies the light's color is by the color derived from the light's temperature.
  */
 @property(nonatomic, retain) id color;
 
 /*!
+ @property temperature
+ @abstract Specifies the receiver's temperature.
+ @discussion This specifies the temperature of the light in Kelvin. The renderer multiplies the light's color by the color derived from the light's temperature. Defaults to 6500 (pure white). Animatable.
+ */
+@property(nonatomic) CGFloat temperature NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property intensity
+ @abstract Specifies the receiver's intensity.
+ @discussion This intensity is used to modulate the light color. When used with a physically-based material, this corresponds to the luminous flux of the light, expressed in lumens (lm). Defaults to 1000. Animatable.
+ */
+@property(nonatomic) CGFloat intensity NS_AVAILABLE(10_12, 10_0);
+
+/*!
  @property name
  @abstract Determines the name of the receiver.
  */
@@ -83,7 +102,8 @@
 
 /*! 
  @property shadowColor
- @abstract Specifies the color (CGColorRef or NSColor) of the shadow casted by the receiver. Default is 50% transparent black. Animatable.
+ @abstract Specifies the color (CGColorRef or NSColor) of the shadow casted by the receiver. Defaults to black. Animatable.
+ @discussion on iOS9 / OS X 10.11 or earlier, this defaults to black 50% transparent.
  */
 @property(nonatomic, retain) id shadowColor;
 
@@ -102,7 +122,9 @@
 
 /*!
  @property shadowSampleCount
- @abstract Specifies the number of sample per fragment to compute the shadow map. Defaults to 1.
+ @abstract Specifies the number of sample per fragment to compute the shadow map. Defaults to 0.
+ @discussion on OS X 10.11 or lower, the shadowSampleCount defaults to 16. On iOS 9.0 or lower it defaults to 1.0.
+ On OS X 10.12, iOS 10.0 and greater, when the shadowSampleCount is set to 0, a default sample count is chosen depending on the platform.
  */
 @property(nonatomic) NSUInteger shadowSampleCount NS_AVAILABLE(10_10, 8_0);
 
@@ -187,6 +209,12 @@
 @property(nonatomic, readonly, nullable) SCNMaterialProperty *gobo NS_AVAILABLE(10_9, 8_0);
 
 /*!
+ @property IESProfileURL
+ @abstract Specifies the IES file from which the shape, direction, and intensity of illumination is determined. Defaults to nil.
+ */
+@property(nonatomic, retain, nullable) NSURL *IESProfileURL NS_AVAILABLE(10_12, 10_0);
+
+/*!
  @property categoryBitMask
  @abstract Determines the node categories that will be lit by the receiver. Defaults to all bit set.
  */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterial.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterial.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterial.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterial.h	2016-05-22 05:48:21.000000000 +0200
@@ -1,7 +1,7 @@
 //
 //  SCNMaterial.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
@@ -78,19 +78,29 @@
      <diffuse> — The 'diffuse' property of the SCNMaterial instance
  */
 
-SCN_EXTERN NSString * const SCNLightingModelPhong;
-SCN_EXTERN NSString * const SCNLightingModelBlinn;
-SCN_EXTERN NSString * const SCNLightingModelLambert;
-SCN_EXTERN NSString * const SCNLightingModelConstant;
+#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
+typedef NSString * SCNLightingModel NS_STRING_ENUM;
+#else
+typedef NSString * SCNLightingModel;
+#endif
+
+FOUNDATION_EXTERN SCNLightingModel const SCNLightingModelPhong;
+FOUNDATION_EXTERN SCNLightingModel const SCNLightingModelBlinn;
+FOUNDATION_EXTERN SCNLightingModel const SCNLightingModelLambert;
+FOUNDATION_EXTERN SCNLightingModel const SCNLightingModelConstant;
+FOUNDATION_EXTERN SCNLightingModel const SCNLightingModelPhysicallyBased NS_AVAILABLE(10_12, 10_0);
 
 typedef NS_ENUM(NSInteger, SCNCullMode) {
-	SCNCullBack  = 0,
-	SCNCullFront = 1,
+	SCNCullModeBack  = 0,
+	SCNCullModeFront = 1
 };
 
+#define SCNCullBack  SCNCullModeBack
+#define SCNCullFront SCNCullModeFront
+
 typedef NS_ENUM(NSInteger, SCNTransparencyMode) {
 	SCNTransparencyModeAOne    = 0, 
-	SCNTransparencyModeRGBZero = 1, 
+	SCNTransparencyModeRGBZero = 1
 };
 
 /*! 
@@ -187,13 +197,25 @@
  @property ambientOcclusion
  @abstract The ambientOcclusion property specifies the ambient occlusion of the surface. The ambient occlusion is multiplied with the ambient light, then the result is added to the lighting contribution. This property has no visual impact on scenes that have no ambient light. When an ambient occlusion map is set, the ambient property is ignored.
  */
-@property(nonatomic, readonly) SCNMaterialProperty *ambientOcclusion NS_ENUM_AVAILABLE(10_11, 9_0);
+@property(nonatomic, readonly) SCNMaterialProperty *ambientOcclusion NS_AVAILABLE(10_11, 9_0);
 
 /*!
  @property selfIllumination
  @abstract The selfIllumination property specifies a texture or a color that is added to the lighting contribution of the surface. When a selfIllumination is set, the emission property is ignored.
  */
-@property(nonatomic, readonly) SCNMaterialProperty *selfIllumination NS_ENUM_AVAILABLE(10_11, 9_0);
+@property(nonatomic, readonly) SCNMaterialProperty *selfIllumination NS_AVAILABLE(10_11, 9_0);
+
+/*!
+ @property metalness
+ @abstract The metalness property specifies how metallic the material's surface appears. Lower values (darker colors) cause the material to appear more like a dielectric surface. Higher values (brighter colors) cause the surface to appear more metallic. This property is only used when 'lightingModelName' is 'SCNLightingModelPhysicallyBased'.
+ */
+@property(nonatomic, readonly) SCNMaterialProperty *metalness NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property roughness
+ @abstract The roughness property specifies the apparent smoothness of the surface. Lower values (darker colors) cause the material to appear shiny, with well-defined specular highlights. Higher values (brighter colors) cause specular highlights to spread out and the diffuse property of the material to become more retroreflective. This property is only used when 'lightingModelName' is 'SCNLightingModelPhysicallyBased'.
+ */
+@property(nonatomic, readonly) SCNMaterialProperty *roughness NS_AVAILABLE(10_12, 10_0);
 
 /*! 
  @property shininess
@@ -208,11 +230,11 @@
  */
 @property(nonatomic) CGFloat transparency;
 
-/*! 
+/*!
  @property lightingModelName
  @abstract Determines the receiver's lighting model. See above for the list of lighting models. Defaults to SCNLightingModelBlinn.
  */
-@property(nonatomic, copy) NSString *lightingModelName;
+@property(nonatomic, copy) SCNLightingModel lightingModelName;
 
 /*! 
  @property litPerPixel
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterialProperty.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterialProperty.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterialProperty.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterialProperty.h	2016-05-22 05:48:16.000000000 +0200
@@ -1,10 +1,11 @@
 //
 //  SCNMaterialProperty.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
+#import <SceneKit/SceneKitTypes.h>
+#import <SceneKit/SCNAnimation.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -12,20 +13,20 @@
     @abstract Filtering modes
 */
 typedef NS_ENUM(NSInteger, SCNFilterMode) {
-    SCNFilterModeNone    NS_ENUM_AVAILABLE(10_9, 8_0) = 0,
-    SCNFilterModeNearest NS_ENUM_AVAILABLE(10_9, 8_0) = 1,
-    SCNFilterModeLinear  NS_ENUM_AVAILABLE(10_9, 8_0) = 2
-};
+    SCNFilterModeNone    = 0,
+    SCNFilterModeNearest = 1,
+    SCNFilterModeLinear  = 2
+} NS_ENUM_AVAILABLE(10_9, 8_0);
 
 /*! @enum SCNWrapeMode
  @abstract Wrap modes
  */
 typedef NS_ENUM(NSInteger, SCNWrapMode) {
-    SCNWrapModeClamp NS_ENUM_AVAILABLE(10_9, 8_0) = 1,
-    SCNWrapModeRepeat NS_ENUM_AVAILABLE(10_9, 8_0) = 2,
-    SCNWrapModeClampToBorder NS_ENUM_AVAILABLE(10_9, 9_0) = 3,
-    SCNWrapModeMirror NS_ENUM_AVAILABLE(10_9, 8_0) = 4,
-};
+    SCNWrapModeClamp         = 1,
+    SCNWrapModeRepeat        = 2,
+    SCNWrapModeClampToBorder = 3,
+    SCNWrapModeMirror        = 4
+} NS_ENUM_AVAILABLE(10_9, 8_0);
 
 /*! @class SCNMaterialProperty
     @abstract The contents of a SCNMaterial slot
@@ -43,9 +44,15 @@
 
 /*! 
  @property contents
- @abstract Specifies the receiver's contents. This can be a color (NSColor/UIColor), an image (NSImage/CGImageRef), a layer (CALayer), a path (NSString or NSURL), a SpriteKit scene (SKScene) or a texture (SKTexture, id<MTLTexture> or GLKTextureInfo). Animatable when set to a color.
- @discussion CGColorRef and CGImageRef can also be set. An array (NSArray) of 6 images is allowed for cube maps, only for reflective property. This array must contain images of the exact same dimensions, in the following order, in a left-handed coordinate system : +X, -X, +Y, -Y, +Z, -Z or if you prefer Right, Left, Top, Bottom, Front, Back. 
-     Setting the contents to an instance of SKTexture will automatically update the wrapS, wrapT, contentsTransform, minification, magnification and mip filters according to the SKTexture settings.
+ @abstract Specifies the receiver's contents. This can be a color (NSColor, UIColor, CGColorRef), an image (NSImage, UIImage, CGImageRef), a layer (CALayer), a path (NSString or NSURL), a SpriteKit scene (SKScene) or a texture (SKTexture, id<MTLTexture> or GLKTextureInfo). Animatable when set to a color.
+ @discussion Setting the contents to an instance of SKTexture will automatically update the wrapS, wrapT, contentsTransform, minification, magnification and mip filters according to the SKTexture settings.
+             When a cube map is expected (e.g. SCNMaterial.reflective, SCNScene.background, SCNScene.lightingEnvironment) you can use
+               1. A horizontal strip image  where `6 * image.height ==     image.width`
+               2. A vertical strip image    where `    image.height == 6 * image.width`
+               3. A horizontal cross image  where `4 * image.height == 3 * image.width`
+               4. A vertical cross image    where `3 * image.height == 4 * image.width`
+               5. A lat/long image          where `    image.height == 2 * image.width`
+               6. A NSArray of 6 images. This array must contain images of the exact same dimensions, in the following order, in a left-handed coordinate system: +X, -X, +Y, -Y, +Z, -Z (or Right, Left, Top, Bottom, Front, Back).
  */
 @property(nonatomic, retain, nullable) id contents;
 
@@ -74,7 +81,7 @@
 /*! 
  @property mipFilter
  @abstract Specifies the mipmap filter to use during minification.
- @discussion Defaults to SCNFilterModeNone.
+ @discussion Defaults to SCNFilterModeNone on OS X 10.11 and iOS 9 or earlier, SCNFilterModeNearest starting in OS X 10.12 and iOS 10.
  */
 @property(nonatomic) SCNFilterMode mipFilter;
 
@@ -101,7 +108,7 @@
  @abstract Determines the receiver's border color (CGColorRef or UIColor). Animatable.
  @discussion The border color is ignored on iOS and is always considered as clear color (0,0,0,0) when the texture has an alpha channel and opaque back (0,0,0,1) otherwise.
  */
-@property(nonatomic, retain, nullable) id borderColor;
+@property(nonatomic, retain, nullable) id borderColor NS_DEPRECATED(10_7, 10_12, 8_0, 10_0) __WATCHOS_UNAVAILABLE;
 
 /*! 
  @property mappingChannel
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMorpher.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMorpher.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMorpher.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMorpher.h	2016-05-31 05:16:49.000000000 +0200
@@ -1,7 +1,7 @@
 //
 //  SCNMorpher.h
 //
-//  Copyright (c) 2013-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2013-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
@@ -9,14 +9,16 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class SCNGeometry;
+
 /*!
  @class SCNMorpher
  @abstract SCNMorpher controls the deformation of morphed geometries
  */
 
 typedef NS_ENUM(NSInteger, SCNMorpherCalculationMode) {
-    SCNMorpherCalculationModeNormalized, // (1 - w0 - w1 - ...) * BaseMesh + w0 * Target0 + w1 * Target1 + ...
-    SCNMorpherCalculationModeAdditive    // BaseMesh + w0 * Target0 + w1 * Target1 + ...
+    SCNMorpherCalculationModeNormalized = 0, // (1 - w0 - w1 - ...) * BaseMesh + w0 * Target0 + w1 * Target1 + ...
+    SCNMorpherCalculationModeAdditive   = 1  // BaseMesh + w0 * Target0 + w1 * Target1 + ...
 };
 
 NS_CLASS_AVAILABLE(10_9, 8_0)
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNNode.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNNode.h	2016-05-31 05:16:41.000000000 +0200
@@ -1,17 +1,16 @@
 //
 //  SCNNode.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
-#import <QuartzCore/QuartzCore.h>
 #import <SceneKit/SCNAnimation.h>
 #import <SceneKit/SCNBoundingVolume.h>
 #import <SceneKit/SCNAction.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class CIFilter;
 @class SCNLight;
 @class SCNCamera;
 @class SCNGeometry;
@@ -21,20 +20,43 @@
 @class SCNPhysicsBody;
 @class SCNPhysicsField;
 @class SCNPhysicsBody;
-
+@class SCNHitTestResult;
+@class SCNRenderer;
 @protocol SCNNodeRendererDelegate;
 
+#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
+typedef NSString * SCNTransformSemantic NS_STRING_ENUM;
+#else
+typedef NSString * SCNTransformSemantic;
+#endif
+
+FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticModel NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticView NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticProjection NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticNormal NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticModelView NS_AVAILABLE(10_12, 10_0);
+FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticModelViewProjection NS_AVAILABLE(10_12, 10_0);
+
 /*! @group Rendering arguments
-    @discussion These keys are used in the 'arguments' dictionary of renderNode:renderer:arguments:
-				and in the 'semantic' argument of -[SCNProgram setSemantic:forSymbol:options:].
+    @discussion These keys are used for the 'semantic' argument of -[SCNProgram setSemantic:forSymbol:options:]
                 Transforms are SCNMatrix4 wrapped in NSValues.
  */
-SCN_EXTERN NSString * const SCNModelTransform;
-SCN_EXTERN NSString * const SCNViewTransform;
-SCN_EXTERN NSString * const SCNProjectionTransform;
-SCN_EXTERN NSString * const SCNNormalTransform;
-SCN_EXTERN NSString * const SCNModelViewTransform;
-SCN_EXTERN NSString * const SCNModelViewProjectionTransform;
+FOUNDATION_EXTERN NSString * const SCNModelTransform;
+FOUNDATION_EXTERN NSString * const SCNViewTransform;
+FOUNDATION_EXTERN NSString * const SCNProjectionTransform;
+FOUNDATION_EXTERN NSString * const SCNNormalTransform;
+FOUNDATION_EXTERN NSString * const SCNModelViewTransform;
+FOUNDATION_EXTERN NSString * const SCNModelViewProjectionTransform;
+
+/*! @enum SCNMovabilityHint
+ @abstract The available modes of movability.
+ @discussion Movable nodes are not captured when computing light probes. Fixed nodes are not lit by probes.
+ Also Movable nodes are not blurred by the motion blur.
+ */
+typedef NS_ENUM(NSInteger, SCNMovabilityHint) {
+    SCNMovabilityHintFixed,
+    SCNMovabilityHintMovable,
+} NS_ENUM_AVAILABLE(10_12, 10_0);
 
 /*!
  @class SCNNode
@@ -125,7 +147,7 @@
 
 
 
-#pragma mark - Modifying the Node's Transform
+#pragma mark - Modifying the Node′s Transform
 
 /*! 
  @property transform
@@ -156,7 +178,14 @@
 /*!
  @property eulerAngles
  @abstract Determines the receiver's euler angles. Animatable.
- @dicussion Specify the intrinsic euler angles (in radians). It represents a sequence of 3 rotations about the x, y, and z axis with the following order: z, y, x (or roll, yaw, pitch).
+ @dicussion The order of components in this vector matches the axes of rotation:
+               1. Pitch (the x component) is the rotation about the node's x-axis (in radians)
+               2. Yaw   (the y component) is the rotation about the node's y-axis (in radians)
+               3. Roll  (the z component) is the rotation about the node's z-axis (in radians)
+            SceneKit applies these rotations in the reverse order of the components:
+               1. first roll
+               2. then yaw
+               3. then pitch
  */
 @property(nonatomic) SCNVector3 eulerAngles NS_AVAILABLE(10_10, 8_0);
 
@@ -181,7 +210,7 @@
 
 
 
-#pragma mark - Modifying the Node's Visibility
+#pragma mark - Modifying the Node′s Visibility
 
 /*! 
  @property hidden
@@ -208,6 +237,12 @@
  */
 @property(nonatomic) BOOL castsShadow NS_AVAILABLE(10_10, 8_0);
 
+/*!
+ @property movabilityHint
+ @abstract Give hints oregarding the movability of the receiver. See enum above for details. Defaults to SCNMovabilityHintFixed.
+ */
+@property (nonatomic) SCNMovabilityHint movabilityHint NS_AVAILABLE(10_12, 10_0);
+
 
 #pragma mark - Managing the Node Hierarchy
 
@@ -272,15 +307,23 @@
  @discussion The search is recursive and uses a pre-order tree traversal.
  @param predicate The block to apply to child nodes of the receiver. The block takes two arguments: "child" is a child node and "stop" is a reference to a Boolean value. The block can set the value to YES to stop further processing of the node hierarchy. The stop argument is an out-only argument. You should only ever set this Boolean to YES within the Block. The Block returns a Boolean value that indicates whether "child" passed the test.
  */
-- (NSArray<SCNNode *> *)childNodesPassingTest:(BOOL (^)(SCNNode *child, BOOL *stop))predicate;
+- (NSArray<SCNNode *> *)childNodesPassingTest:(__attribute__((noescape)) BOOL (^)(SCNNode *child, BOOL *stop))predicate;
 
 /*!
  @method enumerateChildNodesUsingBlock:
- @abstract Executes a given block using each child node under the receiver.
+ @abstract Executes a given block on each child node under the receiver.
  @discussion The search is recursive and uses a pre-order tree traversal.
  @param block The block to apply to child nodes of the receiver. The block takes two arguments: "child" is a child node and "stop" is a reference to a Boolean value. The block can set the value to YES to stop further processing of the node hierarchy. The stop argument is an out-only argument. You should only ever set this Boolean to YES within the Block.
  */
-- (void)enumerateChildNodesUsingBlock:(void (^)(SCNNode *child, BOOL *stop))block NS_AVAILABLE(10_10, 8_0);
+- (void)enumerateChildNodesUsingBlock:(__attribute__((noescape)) void (^)(SCNNode *child, BOOL *stop))block NS_AVAILABLE(10_10, 8_0);
+
+/*!
+ @method enumerateHierarchyUsingBlock:
+ @abstract Executes a given block on the receiver and its child nodes.
+ @discussion The search is recursive and uses a pre-order tree traversal.
+ @param block The block to apply to the receiver and its child nodes. The block takes two arguments: "node" is a node in the hierarchy of the receiver (including the receiver) and "stop" is a reference to a Boolean value. The block can set the value to YES to stop further processing of the node hierarchy. The stop argument is an out-only argument. You should only ever set this Boolean to YES within the Block.
+ */
+- (void)enumerateHierarchyUsingBlock:(__attribute__((noescape)) void (^)(SCNNode *node, BOOL *stop))block NS_AVAILABLE(10_12, 10_0);
 
 
 #pragma mark - Converting Between Node Coordinate Systems
@@ -318,7 +361,7 @@
 - (SCNMatrix4)convertTransform:(SCNMatrix4)transform fromNode:(nullable SCNNode *)node NS_AVAILABLE(10_9, 8_0);
 
 
-#pragma mark - Managing the SCNNode's physics body
+#pragma mark - Managing the SCNNode′s physics body
 
 /*!
  @property physicsBody
@@ -328,7 +371,7 @@
 @property(nonatomic, retain, nullable) SCNPhysicsBody *physicsBody NS_AVAILABLE(10_10, 8_0);
 
 
-#pragma mark - Managing the Node's Physics Field
+#pragma mark - Managing the Node′s Physics Field
 
 /*!
  @property physicsField
@@ -338,7 +381,7 @@
 @property(nonatomic, retain, nullable) SCNPhysicsField *physicsField NS_AVAILABLE(10_10, 8_0);
 
 
-#pragma mark - Managing the Node's Constraints
+#pragma mark - Managing the Node′s Constraints
 
 /*!
  @property constraints
@@ -348,16 +391,14 @@
 @property(copy, nullable) NSArray<SCNConstraint *> *constraints NS_AVAILABLE(10_9, 8_0);
 
 
-
-#pragma mark - Accessing the Node's Filters
+#pragma mark - Accessing the Node′s Filters
 
 /*!
  @property filters
  @abstract An array of Core Image filters that are applied to the rendering of the receiver and its child nodes. Animatable.
  @discussion Defaults to nil. Filter properties should be modified by calling setValue:forKeyPath: on each node that the filter is attached to. If the inputs of the filter are modified directly after the filter is attached to a node, the behavior is undefined.
  */
-@property(nonatomic, copy, nullable) NSArray<CIFilter *> *filters NS_AVAILABLE(10_9, 8_0);
-
+@property(nonatomic, copy, nullable) NSArray<CIFilter *> *filters NS_AVAILABLE(10_9, 8_0) __WATCHOS_PROHIBITED;
 
 
 #pragma mark - Accessing the Presentation Node
@@ -412,7 +453,10 @@
 /*!
  @property categoryBitMask
  @abstract Defines what logical 'categories' the receiver belongs too. Defaults to 1.
- @discussion Categories can be used to exclude nodes from the influence of a given light (see SCNLight's categoryBitMask). It can also be used to include/exclude nodes from render passes (see SCNTechnique.h).
+ @discussion Categories can be used to
+                1. exclude nodes from the influence of a given light (see SCNLight.categoryBitMask)
+                2. include/exclude nodes from render passes (see SCNTechnique.h)
+                3. specify which nodes to use when hit-testing (see SCNHitTestOptionCategoryBitMask)
  */
 @property(nonatomic) NSUInteger categoryBitMask NS_AVAILABLE(10_10, 8_0);
 
@@ -435,9 +479,9 @@
              Only drawing calls and the means to achieve them are supposed to be performed during the renderer delegate callback, any changes in the model (nodes, geometry...) would involve unexpected results.
  @param node The node to render.
  @param renderer The scene renderer to render into.
- @param arguments A dictionary that can have any of the entries described at the beginning of this file.
+ @param arguments A dictionary whose values are SCNMatrix4 matrices wrapped in NSValue objects.
  */
-- (void)renderNode:(SCNNode *)node renderer:(SCNRenderer *)renderer arguments:(NSDictionary<NSString *, NSValue *> *)arguments;
+- (void)renderNode:(SCNNode *)node renderer:(SCNRenderer *)renderer arguments:(NSDictionary<SCNTransformSemantic, id> *)arguments;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParametricGeometry.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParametricGeometry.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParametricGeometry.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParametricGeometry.h	2016-05-31 05:16:41.000000000 +0200
@@ -1,13 +1,15 @@
 //
 //  SCNParametricGeometry.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
+#import <SceneKit/SCNGeometry.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class UIFont;
+@class UIBezierPath;
 @class SCNGeometry;
 
 /*!
@@ -544,9 +546,31 @@
 @property(nonatomic) CGFloat reflectionFalloffEnd;
 
 /*!
+ @property reflectionCategoryBitMask
+ @abstract Determines the node categories to reflect. Defaults to all bits set.
+ */
+@property(nonatomic) NSUInteger reflectionCategoryBitMask NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @property width
+ @abstract The floor extent along the X axis. Animatable.
+ @discussion If the value is equal to 0, the floor is infinite on the X axis. The default value is 0.
+ */
+@property(nonatomic) CGFloat width;
+
+/*!
+ @property height
+ @abstract The floor extent along the Y axis. Animatable.
+ @discussion If the value is equal to 0, the floor is infinite on the Y axis. The default value is 0.
+ */
+@property(nonatomic) CGFloat height;
+
+
+/*!
  @property reflectionResolutionScaleFactor
  @abstract Specifies the resolution scale factor of the buffer used to render the reflection.
  @discussion Defaults to 0.5.
+#endif
 */
 @property(nonatomic) CGFloat reflectionResolutionScaleFactor NS_AVAILABLE(10_10, 8_0);
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParticleSystem.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParticleSystem.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParticleSystem.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParticleSystem.h	2016-05-22 05:48:21.000000000 +0200
@@ -1,35 +1,43 @@
 //
 //  SCNParticleSystem.h
 //
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
+#import <SceneKit/SceneKitTypes.h>
+#import <SceneKit/SCNNode.h>
+#import <SceneKit/SCNScene.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class UIColor;
 @class SCNGeometry;
 
-// Particle Properties Name
-SCN_EXTERN NSString * const SCNParticlePropertyPosition NS_AVAILABLE(10_10, 8_0);        // float3 : {x,y,z}     controller animation type : {NSValue(SCNVector3)}
-SCN_EXTERN NSString * const SCNParticlePropertyAngle NS_AVAILABLE(10_10, 8_0);           // float                controller animation type : {NSNumber}
-SCN_EXTERN NSString * const SCNParticlePropertyRotationAxis NS_AVAILABLE(10_10, 8_0);    // float3 : {x,y,z}     controller animation type : {NSValue(SCNVector3)}
-SCN_EXTERN NSString * const SCNParticlePropertyVelocity NS_AVAILABLE(10_10, 8_0);        // float3 : {x,y,z}     controller animation type : {NSValue(SCNVector3)}
-SCN_EXTERN NSString * const SCNParticlePropertyAngularVelocity NS_AVAILABLE(10_10, 8_0); // float                controller animation type : {NSNumber}
-SCN_EXTERN NSString * const SCNParticlePropertyLife NS_AVAILABLE(10_10, 8_0);            // float                not controllable
-SCN_EXTERN NSString * const SCNParticlePropertyColor NS_AVAILABLE(10_10, 8_0);           // float4 : {r,g,b,a}   controller animation type : {UIColor}
-SCN_EXTERN NSString * const SCNParticlePropertyOpacity NS_AVAILABLE(10_10, 8_0);         // float                controller animation type : {NSNumber}
-SCN_EXTERN NSString * const SCNParticlePropertySize NS_AVAILABLE(10_10, 8_0);            // float                controller animation type : {NSNumber}
-SCN_EXTERN NSString * const SCNParticlePropertyFrame NS_AVAILABLE(10_10, 8_0);           // float                controller animation type : {NSNumber}
-SCN_EXTERN NSString * const SCNParticlePropertyFrameRate NS_AVAILABLE(10_10, 8_0);       // float                controller animation type : {NSNumber}
-SCN_EXTERN NSString * const SCNParticlePropertyBounce NS_AVAILABLE(10_10, 8_0);          // float                controller animation type : {NSNumber}
-SCN_EXTERN NSString * const SCNParticlePropertyCharge NS_AVAILABLE(10_10, 8_0);          // float                controller animation type : {NSNumber}
-SCN_EXTERN NSString * const SCNParticlePropertyFriction NS_AVAILABLE(10_10, 8_0);        // float                controller animation type : {NSNumber}
+#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
+typedef NSString * SCNParticleProperty NS_STRING_ENUM;
+#else
+typedef NSString * SCNParticleProperty;
+#endif
+
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyPosition NS_AVAILABLE(10_10, 8_0);        // float3 : {x,y,z}     controller animation type : {NSValue(SCNVector3)}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyAngle NS_AVAILABLE(10_10, 8_0);           // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyRotationAxis NS_AVAILABLE(10_10, 8_0);    // float3 : {x,y,z}     controller animation type : {NSValue(SCNVector3)}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyVelocity NS_AVAILABLE(10_10, 8_0);        // float3 : {x,y,z}     controller animation type : {NSValue(SCNVector3)}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyAngularVelocity NS_AVAILABLE(10_10, 8_0); // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyLife NS_AVAILABLE(10_10, 8_0);            // float                not controllable
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyColor NS_AVAILABLE(10_10, 8_0);           // float4 : {r,g,b,a}   controller animation type : {UIColor}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyOpacity NS_AVAILABLE(10_10, 8_0);         // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertySize NS_AVAILABLE(10_10, 8_0);            // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyFrame NS_AVAILABLE(10_10, 8_0);           // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyFrameRate NS_AVAILABLE(10_10, 8_0);       // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyBounce NS_AVAILABLE(10_10, 8_0);          // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyCharge NS_AVAILABLE(10_10, 8_0);          // float                controller animation type : {NSNumber}
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyFriction NS_AVAILABLE(10_10, 8_0);        // float                controller animation type : {NSNumber}
 
 // These two properties are only available when handling the events of type SCNParticleEventCollision.
 // They are read-only values.
-SCN_EXTERN NSString * const SCNParticlePropertyContactPoint NS_AVAILABLE(10_10, 8_0);    // float3               not controllable
-SCN_EXTERN NSString * const SCNParticlePropertyContactNormal NS_AVAILABLE(10_10, 8_0);   // float3               not controllable
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyContactPoint NS_AVAILABLE(10_10, 8_0);    // float3               not controllable
+FOUNDATION_EXTERN SCNParticleProperty const SCNParticlePropertyContactNormal NS_AVAILABLE(10_10, 8_0);   // float3               not controllable
 
 /*!
  @typedef SCNParticleEventBlock
@@ -52,7 +60,7 @@
      }
  }];
 */
-typedef void (^SCNParticleEventBlock)(void * __nonnull * __nonnull data, size_t * __nonnull dataStride, uint32_t * __nullable indices, NSInteger count);
+typedef void (^SCNParticleEventBlock)(void * _Nonnull * _Nonnull data, size_t * _Nonnull dataStride, uint32_t * _Nullable indices, NSInteger count);
 
 /*!
  @typedef SCNParticleModifierBlock
@@ -74,7 +82,7 @@
      }
  }];
 */
-typedef void (^SCNParticleModifierBlock)(void * __nonnull * __nonnull data, size_t * __nonnull dataStride, NSInteger start, NSInteger end, float deltaTime);
+typedef void (^SCNParticleModifierBlock)(void * _Nonnull * _Nonnull data, size_t * _Nonnull dataStride, NSInteger start, NSInteger end, float deltaTime);
 
 // Particle Sorting Mode
 typedef NS_ENUM(NSInteger, SCNParticleSortingMode) {
@@ -174,7 +182,7 @@
 @property(nonatomic, weak, nullable) SCNNode *inputOrigin;
 
 // Specifies which property to use as input for the input mode "SCNParticleInputModeOverOtherProperty".
-@property(nonatomic, copy, nullable) NSString *inputProperty;
+@property(nonatomic, copy, nullable) SCNParticleProperty inputProperty;
 
 @end
 
@@ -389,19 +397,18 @@
 @property(nonatomic) CGFloat fresnelExponent;
 
 // Property controllers.
-// The keys for this directionary are listed in the "Particle Properties Name" section.
-@property(nonatomic, copy, nullable) NSDictionary<NSString *, SCNParticlePropertyController *> *propertyControllers;
+@property(nonatomic, copy, nullable) NSDictionary<SCNParticleProperty, SCNParticlePropertyController *> *propertyControllers;
 
 // Remove all the already-emitted particles and restart the simulation.
 - (void)reset;
 
 // Events handling
 // "block" will be invoked for particles that trigger the specified event, with the data and dataStride that corresponds to "properties". The block should only update the particle properties reference by the "indices" passed as argument in the block.
-- (void)handleEvent:(SCNParticleEvent)event forProperties:(NSArray<NSString *> *)properties withBlock:(SCNParticleEventBlock)block;
+- (void)handleEvent:(SCNParticleEvent)event forProperties:(NSArray<SCNParticleProperty> *)properties withBlock:(SCNParticleEventBlock)block;
 
 // Modifications handling
 // "block" will be invoked at every simulation step at the specified stage. The data and dataStride passed to the block will corresponds to the specified "properties".
-- (void)addModifierForProperties:(NSArray<NSString *> *)properties atStage:(SCNParticleModifierStage)stage withBlock:(SCNParticleModifierBlock)block;
+- (void)addModifierForProperties:(NSArray<SCNParticleProperty> *)properties atStage:(SCNParticleModifierStage)stage withBlock:(SCNParticleModifierBlock)block;
 - (void)removeModifiersOfStage:(SCNParticleModifierStage)stage;
 - (void)removeAllModifiers;
 
@@ -430,7 +437,7 @@
 // Add a particle system at the given location.
 - (void)addParticleSystem:(SCNParticleSystem *)system withTransform:(SCNMatrix4)transform NS_AVAILABLE(10_10, 8_0);
 
-// Remove all particle systems of the receiver.
+// Remove all particle systems in the scene.
 - (void)removeAllParticleSystems NS_AVAILABLE(10_10, 8_0);
 
 // Remove the specified particle system from the receiver.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsBehavior.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsBehavior.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsBehavior.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsBehavior.h	2016-05-31 05:16:49.000000000 +0200
@@ -1,11 +1,16 @@
 //
 //  SCNPhysicsBehavior.h
 //
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
+#import <SceneKit/SceneKitTypes.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
+@class SCNNode;
+@class SCNPhysicsBody;
+
 /*!
  @class SCNPhysicsBehavior
  @abstract SCNPhysicsBehavior is an abstract class that represents a behavior in the physics world.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsBody.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsBody.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsBody.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsBody.h	2016-05-24 23:53:11.000000000 +0200
@@ -1,9 +1,11 @@
 //
 //  SCNPhysicsBody.h
 //
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
+#import <SceneKit/SceneKitTypes.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 @class SCNPhysicsShape;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsContact.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsContact.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsContact.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsContact.h	2016-05-31 05:16:49.000000000 +0200
@@ -1,11 +1,15 @@
 //
 //  SCNPhysicsContact.h
 //
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
+#import <SceneKit/SceneKitTypes.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
+@class SCNNode;
+
 /*!
  @class SCNPhysicsContact
  @abstract SCNPhysicsContact contains information about a physics contact.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsField.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsField.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsField.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsField.h	2016-05-31 04:56:02.000000000 +0200
@@ -1,9 +1,11 @@
 //
 //  SCNPhysicsField.h
 //
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
+#import <SceneKit/SceneKitTypes.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 @class SCNNode;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsShape.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsShape.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsShape.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsShape.h	2016-05-31 05:16:49.000000000 +0200
@@ -1,28 +1,41 @@
 //
 //  SCNPhysicsShape.h
 //
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
+#import <Foundation/Foundation.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 @class SCNGeometry;
 @class SCNNode;
 
-//Type of the physics shape. Default is SCNPhysicsShapeTypeConvexHull.
-//See below for the list of shape types.
-SCN_EXTERN NSString * const SCNPhysicsShapeTypeKey NS_AVAILABLE(10_10, 8_0);
-
-//The possible values for the key SCNPhysicsShapeGeometryTypeKey
-SCN_EXTERN NSString * const SCNPhysicsShapeTypeBoundingBox NS_AVAILABLE(10_10, 8_0);
-SCN_EXTERN NSString * const SCNPhysicsShapeTypeConvexHull NS_AVAILABLE(10_10, 8_0);
-SCN_EXTERN NSString * const SCNPhysicsShapeTypeConcavePolyhedron NS_AVAILABLE(10_10, 8_0);
-
-//A boolean to decide if a hierarchy is kept as a compound of shapes or flattened as one single volume. Default is true.
-SCN_EXTERN NSString * const SCNPhysicsShapeKeepAsCompoundKey NS_AVAILABLE(10_10, 8_0);
-
-//Local scaling of the physics shape (as an SCNVector3 wrapped in a NSValue)
-SCN_EXTERN NSString * const SCNPhysicsShapeScaleKey NS_AVAILABLE(10_10, 8_0);
+#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
+typedef NSString * SCNPhysicsShapeOption NS_STRING_ENUM;
+#else
+typedef NSString * SCNPhysicsShapeOption;
+#endif
+
+FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionType NS_AVAILABLE(10_12, 10_0);            // Type of the physics shape. Default is SCNPhysicsShapeTypeConvexHull. See below for the list of shape types.
+FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionKeepAsCompound NS_AVAILABLE(10_12, 10_0);  // A boolean to decide if a hierarchy is kept as a compound of shapes or flattened as one single volume. Default is true.
+FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionScale NS_AVAILABLE(10_12, 10_0);           // Local scaling of the physics shape (as an SCNVector3 wrapped in a NSValue)
+FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionCollisionMargin NS_AVAILABLE(10_12, 10_0); // Collision margin of the physics shape (as an NSNumber)
+
+FOUNDATION_EXTERN NSString * const SCNPhysicsShapeTypeKey NS_AVAILABLE(10_10, 8_0);           // Please use SCNPhysicsShapeOption.type instead.
+FOUNDATION_EXTERN NSString * const SCNPhysicsShapeKeepAsCompoundKey NS_AVAILABLE(10_10, 8_0); // Please use SCNPhysicsShapeOption.keepAsCompound instead.
+FOUNDATION_EXTERN NSString * const SCNPhysicsShapeScaleKey NS_AVAILABLE(10_10, 8_0);          // Please use SCNPhysicsShapeOption.scale instead.
+
+// Values for SCNPhysicsShapeOptionType
+#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
+typedef NSString * SCNPhysicsShapeType NS_STRING_ENUM;
+#else
+typedef NSString * SCNPhysicsShapeType;
+#endif
+
+FOUNDATION_EXTERN SCNPhysicsShapeType const SCNPhysicsShapeTypeBoundingBox NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNPhysicsShapeType const SCNPhysicsShapeTypeConvexHull NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNPhysicsShapeType const SCNPhysicsShapeTypeConcavePolyhedron NS_AVAILABLE(10_10, 8_0);
 
 /*!
  @class SCNPhysicsShape
@@ -32,16 +45,16 @@
 @interface SCNPhysicsShape : NSObject <NSCopying, NSSecureCoding>
 
 //Creates an instance of a physics shape based on a geometry. see above for the possible options.
-+ (instancetype)shapeWithGeometry:(SCNGeometry *)geometry options:(nullable NSDictionary<NSString *, id> *)options;
++ (instancetype)shapeWithGeometry:(SCNGeometry *)geometry options:(nullable NSDictionary<SCNPhysicsShapeOption, id> *)options;
 
 //Creates an instance of a physics shape based on a node hierachy. The hierarchy must contain geometries at some point to create a valid shape. see above for the possible options.
-+ (instancetype)shapeWithNode:(SCNNode *)node options:(nullable NSDictionary<NSString *, id> *)options;
++ (instancetype)shapeWithNode:(SCNNode *)node options:(nullable NSDictionary<SCNPhysicsShapeOption, id> *)options;
 
 //Creates an instance of a physics shape based on several sub shapes, associated with transforms. The transforms are to be passed as an array of NSValue wrapping SCNMatrix4
 + (instancetype)shapeWithShapes:(NSArray<SCNPhysicsShape *> *)shapes transforms:(nullable NSArray<NSValue *> *)transforms;
 
 // Returns the options requested at init time
-@property(readonly, nonatomic, nullable) NSDictionary<NSString *, id> *options NS_AVAILABLE(10_11, 9_0);
+@property(readonly, nonatomic, nullable) NSDictionary<SCNPhysicsShapeOption, id> *options NS_AVAILABLE(10_11, 9_0);
 
 // Returns the object from which this physics shape was created. It can be an SCNGeometry*, an SCNNode* or in NSArray* of subshapes.
 @property(readonly, nonatomic) id sourceObject NS_AVAILABLE(10_11, 9_0);
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsWorld.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsWorld.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsWorld.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsWorld.h	2016-05-22 05:48:21.000000000 +0200
@@ -1,23 +1,45 @@
 //
 //  SCNPhysicsWorld.h
 //
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
+#import <SceneKit/SceneKitTypes.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
+@class SCNPhysicsBody;
+@class SCNPhysicsShape;
+@class SCNPhysicsWorld;
 @class SCNPhysicsContact;
 @class SCNPhysicsBehavior;
+@class SCNHitTestResult;
 
-//Keys for ray, contact and sweep tests
-SCN_EXTERN NSString * const SCNPhysicsTestCollisionBitMaskKey NS_AVAILABLE(10_10, 8_0); //Allows to filter the objects tested by rayTest, contactTest and convexSweep. Default is SCNPhysicsCollisionCategoryAll
-SCN_EXTERN NSString * const SCNPhysicsTestSearchModeKey NS_AVAILABLE(10_10, 8_0);       //Specifies how to perform the ray/contact/sweep test. Values are defined below. If not defined, then defaults to SCNPhysicsTestSearchModeAny
-SCN_EXTERN NSString * const SCNPhysicsTestBackfaceCullingKey NS_AVAILABLE(10_10, 8_0);  //Specifies whether the back faces should be ignored or not. Defaults to YES.
-
-//Values for SCNPhysicsTestSearchModeKey
-SCN_EXTERN NSString * const SCNPhysicsTestSearchModeAny NS_AVAILABLE(10_10, 8_0);       //Returns the first contact found.
-SCN_EXTERN NSString * const SCNPhysicsTestSearchModeClosest NS_AVAILABLE(10_10, 8_0);   //Returns the nearest contact found only.
-SCN_EXTERN NSString * const SCNPhysicsTestSearchModeAll NS_AVAILABLE(10_10, 8_0);       //All contacts are returned.
+// Keys for ray, contact and sweep tests
+#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
+typedef NSString * SCNPhysicsTestOption NS_STRING_ENUM;
+#else
+typedef NSString * SCNPhysicsTestOption;
+#endif
+
+FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestOptionCollisionBitMask NS_AVAILABLE(10_12, 10_0); // Allows to filter the objects tested by rayTest, contactTest and convexSweep. Default is SCNPhysicsCollisionCategoryAll
+FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestOptionSearchMode NS_AVAILABLE(10_12, 10_0);       // Specifies how to perform the ray/contact/sweep test. Values are defined below. If not defined, then defaults to SCNPhysicsTestSearchModeAny
+FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestOptionBackfaceCulling NS_AVAILABLE(10_12, 10_0);  // Specifies whether the back faces should be ignored or not. Defaults to YES.
+
+FOUNDATION_EXTERN NSString * const SCNPhysicsTestCollisionBitMaskKey NS_AVAILABLE(10_10, 8_0); // Please use SCNPhysicsTestOption.collisionBitMask instead.
+FOUNDATION_EXTERN NSString * const SCNPhysicsTestSearchModeKey NS_AVAILABLE(10_10, 8_0);       // Please use SCNPhysicsTestOption.searchMode instead.
+FOUNDATION_EXTERN NSString * const SCNPhysicsTestBackfaceCullingKey NS_AVAILABLE(10_10, 8_0);  // Please use SCNPhysicsTestOption.backfaceCulling instead.
+
+// Values for SCNPhysicsTestSearchModeKey
+#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
+typedef NSString * SCNPhysicsTestSearchMode NS_STRING_ENUM;
+#else
+typedef NSString * SCNPhysicsTestSearchMode;
+#endif
+
+FOUNDATION_EXTERN SCNPhysicsTestSearchMode const SCNPhysicsTestSearchModeAny NS_AVAILABLE(10_10, 8_0);     // Returns the first contact found.
+FOUNDATION_EXTERN SCNPhysicsTestSearchMode const SCNPhysicsTestSearchModeClosest NS_AVAILABLE(10_10, 8_0); // Returns the nearest contact found only.
+FOUNDATION_EXTERN SCNPhysicsTestSearchMode const SCNPhysicsTestSearchModeAll NS_AVAILABLE(10_10, 8_0);     // All contacts are returned.
 
 /*!
  @protocol SCNPhysicsContactDelegate
@@ -59,12 +81,12 @@
 @property(nonatomic, readonly) NSArray<SCNPhysicsBehavior *> *allBehaviors;
 
 //Performs a ray test on the physics bodies and their physics shapes.
-- (NSArray<SCNHitTestResult *> *)rayTestWithSegmentFromPoint:(SCNVector3)origin toPoint:(SCNVector3)dest options:(nullable NSDictionary<NSString *, id> *)options;
+- (NSArray<SCNHitTestResult *> *)rayTestWithSegmentFromPoint:(SCNVector3)origin toPoint:(SCNVector3)dest options:(nullable NSDictionary<SCNPhysicsTestOption, id> *)options;
 
 //The methods below perform contact tests.
-- (NSArray<SCNPhysicsContact *> *)contactTestBetweenBody:(SCNPhysicsBody *)bodyA andBody:(SCNPhysicsBody *)bodyB options:(nullable NSDictionary<NSString *, id> *)options;
-- (NSArray<SCNPhysicsContact *> *)contactTestWithBody:(SCNPhysicsBody *)body options:(nullable NSDictionary<NSString *, id> *)options;
-- (NSArray<SCNPhysicsContact *> *)convexSweepTestWithShape:(SCNPhysicsShape *)shape fromTransform:(SCNMatrix4)from toTransform:(SCNMatrix4)to options:(nullable NSDictionary<NSString *, id> *)options;
+- (NSArray<SCNPhysicsContact *> *)contactTestBetweenBody:(SCNPhysicsBody *)bodyA andBody:(SCNPhysicsBody *)bodyB options:(nullable NSDictionary<SCNPhysicsTestOption, id> *)options;
+- (NSArray<SCNPhysicsContact *> *)contactTestWithBody:(SCNPhysicsBody *)body options:(nullable NSDictionary<SCNPhysicsTestOption, id> *)options;
+- (NSArray<SCNPhysicsContact *> *)convexSweepTestWithShape:(SCNPhysicsShape *)shape fromTransform:(SCNMatrix4)from toTransform:(SCNMatrix4)to options:(nullable NSDictionary<SCNPhysicsTestOption, id> *)options;
 
 //Force the physics engine to re-evaluate collisions.
 //This needs to be called if kinematic are moved and the contacts are wanted before the next simulation step.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNReferenceNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNReferenceNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNReferenceNode.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNReferenceNode.h	2016-05-31 05:16:49.000000000 +0200
@@ -1,9 +1,11 @@
 //
 //  SCNReferenceNode.h
 //
-//  Copyright (c) 2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2015-2016 Apple Inc. All rights reserved.
 //
 
+#import <SceneKit/SCNNode.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
 /*! @enum SCNReferenceLoadingPolicy
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNRenderer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNRenderer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNRenderer.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNRenderer.h	2016-05-31 05:16:49.000000000 +0200
@@ -1,7 +1,7 @@
 //
 //  SCNRenderer.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <SceneKit/SCNSceneRenderer.h>
@@ -9,6 +9,7 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class UIImage;
 @protocol MTLDevice;
 @protocol MTLCommandQueue;
 @protocol MTLRenderCommandEncoder;
@@ -17,7 +18,7 @@
 /*! @class SCNRenderer
 	@abstract SCNRenderer lets you use the SceneKit renderer in an OpenGL context or Metal render pass descriptor of your own.
  */
-NS_CLASS_AVAILABLE(10_8, 8_0)
+NS_CLASS_AVAILABLE(10_8, 8_0) __WATCHOS_PROHIBITED
 @interface SCNRenderer : NSObject <SCNSceneRenderer, SCNTechniqueSupport>
 
 /*! 
@@ -26,7 +27,7 @@
  @param context The context to render into.
  @param options An optional dictionary for future extensions.
  */
-+ (instancetype)rendererWithContext:(EAGLContext *)context options:(nullable NSDictionary *)options;
++ (instancetype)rendererWithContext:(nullable EAGLContext *)context options:(nullable NSDictionary *)options;
 
 /*!
  @method rendererWithDevice:options:
@@ -50,6 +51,12 @@
 - (void)renderAtTime:(CFTimeInterval)time NS_AVAILABLE(10_10, 8_0);
 
 /*!
+ @method snapshotAtTime:withSize:antialiasingMode:
+ @abstract renders the receiver's scene at the specified time (system time) into an image.
+ */
+- (UIImage *)snapshotAtTime:(CFTimeInterval)time withSize:(CGSize)size antialiasingMode:(SCNAntialiasingMode)antialiasingMode NS_AVAILABLE(10_12, 10_0);
+
+/*!
  @method renderAtTime:viewport:commandBuffer:passDescriptor:
  @abstract renders the receiver's scene at the specified time (system time) viewport, metal command buffer and pass descriptor.
  @discussion Use this method to render using Metal.
@@ -67,7 +74,7 @@
  @abstract renders the receiver's scene at the current system time.
  @discussion This method only work if the receiver was allocated with an OpenGL context and it is deprecated (use renderAtIme: instead). Use renderAtTime:withEncoder:pass:commandQueue: to render with Metal.
  */
-- (void)render NS_DEPRECATED(10_8, 10_11, 8_0, 9_0);
+- (void)render NS_DEPRECATED(10_8, 10_11, 8_0, 9_0) __WATCHOS_UNAVAILABLE;
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNScene.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNScene.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNScene.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNScene.h	2016-05-22 05:48:21.000000000 +0200
@@ -1,11 +1,12 @@
 //
 //  SCNScene.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
 #import <SceneKit/SCNAnimation.h>
+#import <SceneKit/SCNSceneSource.h>
 #import <SceneKit/SCNMaterialProperty.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -21,7 +22,7 @@
  @param error Will contain information about the failure if any.
  @param stop Set *stop to YES if you want to abort the operation.
  */
-typedef void (^SCNSceneExportProgressHandler)(float totalProgress, NSError * __nullable error, BOOL *stop);
+typedef void (^SCNSceneExportProgressHandler)(float totalProgress, NSError * _Nullable error, BOOL *stop);
 
 
 /*! @group Scene writing options */
@@ -30,21 +31,27 @@
  @abstract Specifies the final destination (as a NSURL) of the scene being exported.
  @discussion The destination URL is required if the scene is exported to a temporary directory and then moved to a final destination. This enables the exported document to get correct relative paths to referenced images.
  */
-SCN_EXTERN NSString * const SCNSceneExportDestinationURL NS_AVAILABLE(10_9, 8_0);
+FOUNDATION_EXTERN NSString * const SCNSceneExportDestinationURL NS_AVAILABLE(10_9, 8_0);
 
 
 /*! @group Scene attributes
     @abstract These keys can be used with the -[SCNScene attributeForKey:] method.
  */
-
-/*! A floating point value, encapsulated in a NSNumber, containing the start time of the scene. */
-SCN_EXTERN NSString * const SCNSceneStartTimeAttributeKey;
-/*! A floating point value, encapsulated in a NSNumber, containing the end time of the scene. */
-SCN_EXTERN NSString * const SCNSceneEndTimeAttributeKey;
-/*! A floating point value, encapsulated in a NSNumber, containing the framerate of the scene. */
-SCN_EXTERN NSString * const SCNSceneFrameRateAttributeKey;
-/*! A vector3 value, encapsulated in a NSValue, containing the up axis of the scene. This is just for information, setting the up axis as no effect */
-SCN_EXTERN NSString * const SCNSceneUpAxisAttributeKey NS_AVAILABLE(10_10, 8_0);
+#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
+typedef NSString * SCNSceneAttribute NS_STRING_ENUM;
+#else
+typedef NSString * SCNSceneAttribute;
+#endif
+
+FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneAttributeStartTime NS_AVAILABLE(10_12, 10_0); // A floating point value, encapsulated in a NSNumber, containing the start time of the scene.
+FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneAttributeEndTime NS_AVAILABLE(10_12, 10_0);   // A floating point value, encapsulated in a NSNumber, containing the end time of the scene.
+FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneAttributeFrameRate NS_AVAILABLE(10_12, 10_0); // A floating point value, encapsulated in a NSNumber, containing the framerate of the scene.
+FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneAttributeUpAxis NS_AVAILABLE(10_12, 10_0);    // A vector3 value, encapsulated in a NSValue, containing the up axis of the scene. This is just for information, setting the up axis as no effect.
+
+FOUNDATION_EXTERN NSString * const SCNSceneStartTimeAttributeKey;                       // Please use SCNSceneAttribute.startTime instead.
+FOUNDATION_EXTERN NSString * const SCNSceneEndTimeAttributeKey;                         // Please use SCNSceneAttribute.endTime instead.
+FOUNDATION_EXTERN NSString * const SCNSceneFrameRateAttributeKey;                       // Please use SCNSceneAttribute.frameRate instead.
+FOUNDATION_EXTERN NSString * const SCNSceneUpAxisAttributeKey NS_AVAILABLE(10_10, 8_0); // Please use SCNSceneAttribute.upAxis instead.
 
 /*!
  @class SCNScene
@@ -92,10 +99,19 @@
 /*!
  @property background
  @abstract Specifies the background of the receiver.
- @discussion The background is rendered before the rest of the scene. The background can be rendered as a skybox by setting a NSArray of six images to its contents (see SCNMaterialProperty.h). Setting a color will have no effect (use SCNView's backgroundColor instead).
+ @discussion The background is rendered before the rest of the scene.
+             The background can be rendered as a skybox by setting a cube map as described in SCNMaterialProperty.h
+             Colors are supported starting OS X 10.12 and iOS 10.0. Prior to that you can use SCNView.backgroundColor.
  */
 @property(nonatomic, readonly) SCNMaterialProperty *background NS_AVAILABLE(10_9, 8_0);
 
+/*!
+ @property lightingEnvironment
+ @abstract Specifies the receiver's environment for image-based lighting (IBL).
+ @discussion The environment should be a cube map as described in SCNMaterialProperty.h
+ */
+@property(nonatomic, readonly) SCNMaterialProperty *lightingEnvironment NS_AVAILABLE(10_12, 10_0);
+
 
 #pragma mark - Loading
 
@@ -115,7 +131,7 @@
  @param options An options dictionary. The relevant keys are documented in the SCNSceneSource class.
  @discussion This method initializes with no options and does not check for errors. The resulting object is not cached.
  */
-+ (nullable instancetype)sceneNamed:(NSString *)name inDirectory:(nullable NSString *)directory options:(nullable NSDictionary<NSString *, id> *)options NS_AVAILABLE(10_10, 8_0);
++ (nullable instancetype)sceneNamed:(NSString *)name inDirectory:(nullable NSString *)directory options:(nullable NSDictionary<SCNSceneSourceLoadingOption, id> *)options NS_AVAILABLE(10_10, 8_0);
 
 /*!
  @method sceneWithURL:options:error:
@@ -126,8 +142,24 @@
  @discussion This method is here for convenience. It is equivalent to initializing a SCNSceneSource with the specified
  url and options, and asking it for its scene with the same options.
  */
-+ (nullable instancetype)sceneWithURL:(NSURL *)url options:(nullable NSDictionary<NSString *, id> *)options error:(NSError **)error;
++ (nullable instancetype)sceneWithURL:(NSURL *)url options:(nullable NSDictionary<SCNSceneSourceLoadingOption, id> *)options error:(NSError **)error;
 
+#pragma mark - Writing
+
+/*!
+ @method writeToURL:options:delegate:progressHandler:
+ @abstract write the scene to the specified url.
+ @param url the destination url to write the scene to.
+ @param options A dictionary of options. The valid keys are described in the "Scene writing options" section.
+ @param delegate an optional delegate to manage external references such as images.
+ @param progressHandler an optional block to handle the progress of the operation.
+ @return Returns YES if the operation succeeded, NO otherwise. Errors checking can be done via the "error"
+ parameter of the 'progressHandler'.
+ @discussion OS X 10.10 and lower only supports exporting to .dae files.
+             Starting OS X 10.11 exporting supports .dae, .scn as well as file all formats supported by Model I/O.
+             Starting iOS 10.0 exporting supports .scn as well as all file formats supported by Model I/O.
+ */
+- (BOOL)writeToURL:(NSURL *)url options:(nullable NSDictionary<NSString *, id> *)options delegate:(nullable id <SCNSceneExportDelegate>)delegate progressHandler:(nullable SCNSceneExportProgressHandler)progressHandler NS_AVAILABLE(10_9, 10_0);
 
 #pragma mark - Fog
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneRenderer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneRenderer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneRenderer.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneRenderer.h	2016-05-31 04:56:02.000000000 +0200
@@ -1,40 +1,34 @@
 //
 //  SCNSceneRenderer.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
+#import <SceneKit/SceneKitTypes.h>
+#import <SceneKit/SCNHitTest.h>
+
 NS_ASSUME_NONNULL_BEGIN
 
-@class SCNScene;
 @class SCNNode;
+@class SCNScene;
+@protocol SCNSceneRendererDelegate;
 @class SKScene;
 @class SKTransition;
-@protocol SCNSceneRendererDelegate;
+@class MTLRenderPassDescriptor;
 @protocol MTLRenderCommandEncoder;
 @protocol MTLCommandBuffer;
-@class MTLRenderPassDescriptor;
 @class AVAudioEngine;
 @class AVAudioEnvironmentNode;
 
-/*! @group Hit test options */
-
-/*! If set to YES, returns the first object found. This object is not necessarily the nearest. Defaults to NO. */
-SCN_EXTERN NSString * const SCNHitTestFirstFoundOnlyKey;
-/*! Determines whether the results should be sorted. If set to YES sorts nearest objects first. Defaults to YES. */
-SCN_EXTERN NSString * const SCNHitTestSortResultsKey;
-/*! If set to YES ignores the objects clipped by the zNear/zFar range of the current point of view. Defaults to YES. */
-SCN_EXTERN NSString * const SCNHitTestClipToZRangeKey;
-/*! If set to YES ignores the faces not facing to the camera. Defaults to YES. */
-SCN_EXTERN NSString * const SCNHitTestBackFaceCullingKey;
-/*!  If set to YES only tests the bounding boxes of the 3D objects. Defaults to NO. */
-SCN_EXTERN NSString * const SCNHitTestBoundingBoxOnlyKey;
-/*! Determines whether the child nodes are ignored. Defaults to NO. */
-SCN_EXTERN NSString * const SCNHitTestIgnoreChildNodesKey;
-/*! Specifies the root node to use for the hit test. Defaults to the root node of the scene. */
-SCN_EXTERN NSString * const SCNHitTestRootNodeKey;
-/*! Determines whether hidden nodes should be ignored. Defaults to YES. */
-SCN_EXTERN NSString * const SCNHitTestIgnoreHiddenNodesKey NS_AVAILABLE(10_9, 8_0);
+/*!
+ @enum SCNAntialiasingMode
+ @abstract antialiasing modes for scene renderers
+ */
+typedef NS_ENUM(NSUInteger, SCNAntialiasingMode) {
+    SCNAntialiasingModeNone,
+    SCNAntialiasingModeMultisampling2X,
+    SCNAntialiasingModeMultisampling4X
+} NS_ENUM_AVAILABLE(10_10, 8_0);
 
 /*!
  @enum SCNRenderingAPI
@@ -62,47 +56,6 @@
 } NS_ENUM_AVAILABLE(10_11, 9_0);
 
 
-/*! @class SCNHitTestResult
-    @abstract Results returned by the hit test methods.
- */
-
-NS_CLASS_AVAILABLE(10_8, 8_0)
-@interface SCNHitTestResult : NSObject
-
-/*! The node hit. */
-@property(nonatomic, readonly) SCNNode *node;
-
-/*! Index of the geometry hit. */
-@property(nonatomic, readonly) NSInteger geometryIndex;
-
-/*! Index of the face hit. */
-@property(nonatomic, readonly) NSInteger faceIndex;
-
-/*! Intersection point in the node local coordinate system. */
-@property(nonatomic, readonly) SCNVector3 localCoordinates;
-
-/*! Intersection point in the world coordinate system. */
-@property(nonatomic, readonly) SCNVector3 worldCoordinates;
-
-/*! Intersection normal in the node local coordinate system. */
-@property(nonatomic, readonly) SCNVector3 localNormal;
-
-/*! Intersection normal in the world coordinate system. */
-@property(nonatomic, readonly) SCNVector3 worldNormal;
-
-/*! World transform of the node intersected. */
-@property(nonatomic, readonly) SCNMatrix4 modelTransform;
-
-/*! 
- @method textureCoordinatesWithMappingChannel:
- @abstract Returns the texture coordinates at the point of intersection, for a given mapping channel.
- @param channel The texture coordinates source index of the geometry to use. The channel must exists on the geometry otherwise {0,0} will be returned.
- */
-- (CGPoint)textureCoordinatesWithMappingChannel:(NSInteger)channel;
-
-@end
-
-
 
 /*! @protocol SCNSceneRenderer
     @abstract Protocol adopted by the various renderers (SCNView, SCNLayer, SCNRenderer)
@@ -145,7 +98,7 @@
  @param point A point in the coordinate system of the receiver.
  @param options Optional parameters (see the "Hit test options" group for the available options).
  */
-- (NSArray<SCNHitTestResult *> *)hitTest:(CGPoint)point options:(nullable NSDictionary<NSString *, id> *)options;
+- (NSArray<SCNHitTestResult *> *)hitTest:(CGPoint)point options:(nullable NSDictionary<SCNHitTestOption, id> *)options;
 
 /*!
  @method isNodeInsideFrustum:withPointOfView:
@@ -221,7 +174,7 @@
  @param block This block will be called repeatedly while the object is prepared. Return YES if you want the operation to abort.
  @discussion Returns YES if the object was prepared successfully, NO if it was canceled. This method may be triggered from a secondary thread. This method is observable using NSProgress.
  */
-- (BOOL)prepareObject:(id)object shouldAbortBlock:(nullable BOOL (^)())block NS_AVAILABLE(10_9, 8_0);
+- (BOOL)prepareObject:(id)object shouldAbortBlock:(nullable __attribute__((noescape)) BOOL (^)())block NS_AVAILABLE(10_9, 8_0);
 
 /*!
  @method prepareObjects:withCompletionHandler:
@@ -315,7 +268,7 @@
  @property audioEnvironmentNode
  @abstract Contains the instance of audio environment node used by the scene to spacialize sounds.
  */
-@property(nonatomic, readonly) AVAudioEnvironmentNode *audioEnvironmentNode NS_AVAILABLE(10_11, 9_0);
+@property(nonatomic, readonly) AVAudioEnvironmentNode *audioEnvironmentNode NS_AVAILABLE(10_11, 9_0) __WATCHOS_PROHIBITED;
 
 /*!
  @property audioListener
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneSource.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneSource.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneSource.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneSource.h	2016-05-22 05:48:16.000000000 +0200
@@ -1,7 +1,7 @@
 //
 //  SCNSceneSource.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
@@ -12,38 +12,43 @@
 
 /*! @group Scene source properties */
 /*! File contributors. The values are dictionaries populated with keys documented in the "Contributor dictionary keys" group. */
-SCN_EXTERN NSString * const SCNSceneSourceAssetContributorsKey;
+FOUNDATION_EXTERN NSString * const SCNSceneSourceAssetContributorsKey;
 /*! When the file was created. The value is a NSDate instance. */
-SCN_EXTERN NSString * const SCNSceneSourceAssetCreatedDateKey;
+FOUNDATION_EXTERN NSString * const SCNSceneSourceAssetCreatedDateKey;
 /*! When the file was last modified. The value is a NSDate instance. */
-SCN_EXTERN NSString * const SCNSceneSourceAssetModifiedDateKey;
+FOUNDATION_EXTERN NSString * const SCNSceneSourceAssetModifiedDateKey;
 /*! The up axis of the file. If the file is oriented Y-up, for example, then this is the string \@"0.0 1.0 0.0" */
-SCN_EXTERN NSString * const SCNSceneSourceAssetUpAxisKey;
+FOUNDATION_EXTERN NSString * const SCNSceneSourceAssetUpAxisKey;
 /*! The unit used in the file. The value is a dictionary populated with keys documented in the "Unit dictionary keys" group. */
-SCN_EXTERN NSString * const SCNSceneSourceAssetUnitKey;
+FOUNDATION_EXTERN NSString * const SCNSceneSourceAssetUnitKey;
 
 /*! @group Contributor dictionary keys */
 /*! Authoring tool used to create the file. The corresponding value is an NSString. */
-SCN_EXTERN NSString * const SCNSceneSourceAssetAuthoringToolKey;
+FOUNDATION_EXTERN NSString * const SCNSceneSourceAssetAuthoringToolKey;
 /*! The file's author. The corresponding value is an NSString. */
-SCN_EXTERN NSString * const SCNSceneSourceAssetAuthorKey;
+FOUNDATION_EXTERN NSString * const SCNSceneSourceAssetAuthorKey;
 
 /*! @group Unit dictionary keys */
 /*! The name (NSString) of the unit */
-SCN_EXTERN NSString * const SCNSceneSourceAssetUnitNameKey;
+FOUNDATION_EXTERN NSString * const SCNSceneSourceAssetUnitNameKey;
 /*! A NSNumber encapsulating a floating-point value indicating how many meters the unit is. For example, if the name is \@"centimeter", then this will be 0.01. */
-SCN_EXTERN NSString * const SCNSceneSourceAssetUnitMeterKey;
+FOUNDATION_EXTERN NSString * const SCNSceneSourceAssetUnitMeterKey;
 
 /*! @group Scene loading options */
+#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
+typedef NSString * SCNSceneSourceLoadingOption NS_STRING_ENUM;
+#else
+typedef NSString * SCNSceneSourceLoadingOption;
+#endif
 
-/*! @constant SCNSceneSourceCreateNormalsIfAbsentKey
+/*! @constant SCNSceneSourceLoadingOptionCreateNormalsIfAbsent
 	@abstract Enable to try to guess acceptable normals for the vertices if none are given in the file
     @discussion Use this with a boolean value encapsulated in a NSNumber. The default value is NO.
  */
-SCN_EXTERN NSString * const SCNSceneSourceCreateNormalsIfAbsentKey;
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionCreateNormalsIfAbsent NS_AVAILABLE(10_12, 10_0);
 
 /*!
- @constant SCNSceneSourceCheckConsistencyKey
+ @constant SCNSceneSourceLoadingOptionCheckConsistency
  @abstract Pass YES in order to perform the document validation. 
  @discussion This option can be set in the options dictionary of the SCNScene and SCNSceneSource loading methods.
  The value for this option should be a boolean NSNumber. If its boolean value is YES (the default is NO),
@@ -51,101 +56,130 @@
  If the document doesn't pass the consistency check it is then not loaded and an error is returned.
  This is slower, but for security reasons it should be set to YES if you are not sure the files you load are valid and have not been tampered with. 
  */
-SCN_EXTERN NSString * const SCNSceneSourceCheckConsistencyKey;
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionCheckConsistency NS_AVAILABLE(10_12, 10_0);
 
 /*!
- @constant SCNSceneSourceFlattenSceneKey
+ @constant SCNSceneSourceLoadingOptionFlattenScene
  @abstract Pass YES to flatten the scene graph when possible.
  @discussion This option can be set in the options dictionary of the SCNScene and SCNSceneSource loading methods.
  The value for this option should be a boolean NSNumber. If its boolean value is YES (the default is NO),
  SceneKit will attempt to reduce the scene graph by merging the geometries.
  This option is suitable to preview a 3D scene efficiently and when manipulating the scene graph is not needed.
  */
-SCN_EXTERN NSString * const SCNSceneSourceFlattenSceneKey;
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionFlattenScene NS_AVAILABLE(10_12, 10_0);
 
 /*!
- @constant SCNSceneSourceUseSafeModeKey
+ @constant SCNSceneSourceLoadingOptionUseSafeMode
  @abstract Pass YES in order to enable the safe mode.
  @discussion This option can be set in the options dictionary of the SCNScene and SCNSceneSource loading methods.
  The value for this option should be a boolean NSNumber. If its boolean value is YES (the default is NO),
  SceneKit will forbid network accesses, prevent the loading of resources from arbitrary directories, and will not execute
  any code present in the loaded files.
  */
-SCN_EXTERN NSString * const SCNSceneSourceUseSafeModeKey;
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionUseSafeMode NS_AVAILABLE(10_12, 10_0);
 
 /*!
- @constant SCNSceneSourceAssetDirectoryURLsKey
+ @constant SCNSceneSourceLoadingOptionAssetDirectoryURLs
  @abstract Pass an array of directory URLs where SceneKit should look for resources
  @discussion By default, SceneKit will look for the external resources it cannot find in the parent directory of the imported file.
  You can add additional directories by setting an array of URLs for this key when calling sceneWithOptions:error:.
  This is recommended if you want to construct your scene source from a data object, not from an URL,
  and need to load resources whose paths are not absolute.
  */
-SCN_EXTERN NSString * const SCNSceneSourceAssetDirectoryURLsKey;
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionAssetDirectoryURLs NS_AVAILABLE(10_12, 10_0);
 
 /*!
- @constant SCNSceneSourceOverrideAssetURLsKey
+ @constant SCNSceneSourceLoadingOptionOverrideAssetURLs
  @abstract Pass YES in order to override assets URLs with the directory URLs passed via SCNSceneSourceAssetDirectoryURLsKey.
  @discussion By default, SceneKit will look for the external resources using the paths/urls as described in the imported file.
  You can force SceneKit to only search for extern resources within the directories specified by the SCNSceneSourceAssetDirectoryURLsKey key.
  This can be useful to load a file and its resources from a specific bundle for instance.
  */
-SCN_EXTERN NSString * const SCNSceneSourceOverrideAssetURLsKey;
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionOverrideAssetURLs NS_AVAILABLE(10_12, 10_0);
 
 /*!
- @constant SCNSceneSourceStrictConformanceKey
+ @constant SCNSceneSourceLoadingOptionStrictConformance
  @abstract Pass YES to interpret the 3D format of the file in a strict way.
  @discussion This option defaults to NO. In this case SceneKit will try to read any additional metadata present in the file to
 			 enable additional features and make the rendering as close as possible to the original intent. If you pass YES,
              SceneKit will instead only consider features which are part of the file format specification.
  */
-SCN_EXTERN NSString * const SCNSceneSourceStrictConformanceKey;
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionStrictConformance NS_AVAILABLE(10_12, 10_0);
 
 /*!
- @constant SCNSceneSourceConvertUnitsToMetersKey
+ @constant SCNSceneSourceLoadingOptionConvertUnitsToMeters
  @abstract Pass the units you want the scene to be converted to (in meter).
  @discussion Use this with a floating value encapsulated in a NSNumber. The default value is nil which means no conversion done. Passing a non-zero value will convert the scene coordinates so that 1 unit corresponds to N meters. For example pass 0.01 for 1 unit == 1 centimeter, pass 0.3048 for 1 unit == 1 foot...
      For better physics simulation it is recommended to use 1 unit equals to 1 meter.
      This option has no effect if the asset is already compressed by Xcode (use the compression options instead).
  */
-SCN_EXTERN NSString * const SCNSceneSourceConvertUnitsToMetersKey NS_AVAILABLE(10_10, NA);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionConvertUnitsToMeters NS_AVAILABLE(10_12, 10_0);
 
 /*!
- @constant SCNSceneSourceConvertToYUpKey
+ @constant SCNSceneSourceLoadingOptionConvertToYUp
  @abstract Pass YES if a scene should be converted to Y up if it currently has a different up axis.
  @discussion Use this with a boolean value encapsulated in a NSNumber. The default value is NO.
  This option has no effect if the asset is already compressed by Xcode (use the compression options instead).
  */
-SCN_EXTERN NSString * const SCNSceneSourceConvertToYUpKey NS_AVAILABLE(10_10, NA);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionConvertToYUp NS_AVAILABLE(10_12, 10_0);
 
 /*!
- @constant SCNSceneSourceAnimationImportPolicyKey
+ @constant SCNSceneSourceLoadingOptionAnimationImportPolicy
  @abstract Pass one of the value below to specify what to do with loaded animations.
  @discussion See below for the description of each individual key. Defaults to SCNSceneSourceAnimationImportPolicyPlayRepeatedly. On 10.9 and before the behavior is SCNSceneSourceAnimationImportPolicyPlayUsingSceneTimeBase. For compatibility reason if the application was built on 10.9 or before the default behavior is SCNSceneSourceAnimationImportPolicyPlayUsingSceneTimeBase.
  */
-SCN_EXTERN NSString * const SCNSceneSourceAnimationImportPolicyKey NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionAnimationImportPolicy NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @constant SCNSceneSourceLoadingOptionPreserveOriginalTopology
+ @abstract Pass YES to make SceneKit preserve the original topology instead of triangulating at load time.
+ This can be useful to get better results when subdividing a geometry. Defaults to NO.
+ */
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionPreserveOriginalTopology NS_AVAILABLE(10_12, 10_0);
+
+FOUNDATION_EXTERN NSString * const SCNSceneSourceCreateNormalsIfAbsentKey;                          // Please use SCNSceneSourceLoadingOption.createNormalsIfAbsent instead.
+FOUNDATION_EXTERN NSString * const SCNSceneSourceCheckConsistencyKey;                               // Please use SCNSceneSourceLoadingOption.createNormalsIfAbsent instead.
+FOUNDATION_EXTERN NSString * const SCNSceneSourceFlattenSceneKey;                                   // Please use SCNSceneSourceLoadingOption.flattenScene instead.
+FOUNDATION_EXTERN NSString * const SCNSceneSourceUseSafeModeKey;                                    // Please use SCNSceneSourceLoadingOption.useSafeMode instead.
+FOUNDATION_EXTERN NSString * const SCNSceneSourceAssetDirectoryURLsKey;                             // Please use SCNSceneSourceLoadingOption.assetDirectoryURLs instead.
+FOUNDATION_EXTERN NSString * const SCNSceneSourceOverrideAssetURLsKey;                              // Please use SCNSceneSourceLoadingOption.overrideAssetURLs instead.
+FOUNDATION_EXTERN NSString * const SCNSceneSourceStrictConformanceKey;                              // Please use SCNSceneSourceLoadingOption.strictConformance instead.
+FOUNDATION_EXTERN NSString * const SCNSceneSourceConvertUnitsToMetersKey NS_AVAILABLE(10_10, NA);   // Please use SCNSceneSourceLoadingOption.convertUnitsToMeters instead.
+FOUNDATION_EXTERN NSString * const SCNSceneSourceConvertToYUpKey NS_AVAILABLE(10_10, NA);           // Please use SCNSceneSourceLoadingOption.convertUnitsToMeters instead.
+FOUNDATION_EXTERN NSString * const SCNSceneSourceAnimationImportPolicyKey NS_AVAILABLE(10_10, 8_0); // Please use SCNSceneSourceLoadingOption.animationImportPolicy instead.
+
+
+/* Values for SCNSceneSourceLoadingOptionAnimationImportPolicy */
+#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
+typedef NSString * SCNSceneSourceAnimationImportPolicy NS_STRING_ENUM;
+#else
+typedef NSString * SCNSceneSourceAnimationImportPolicy;
+#endif
 
-/* values for SCNSceneSourceAnimationImportPolicyKey */
 /*!
  @constant SCNSceneSourceAnimationImportPolicyPlay
  @abstract Add animations to the scene and play them once (repeatCount set to 1).
  */
-SCN_EXTERN NSString * const SCNSceneSourceAnimationImportPolicyPlay NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNSceneSourceAnimationImportPolicy const SCNSceneSourceAnimationImportPolicyPlay NS_AVAILABLE(10_10, 8_0);
+
 /*!
  @constant SCNSceneSourceAnimationImportPolicyPlayRepeatedly
  @abstract Add animations to the scene and play them repeatedly (repeatCount set to infinity).
  */
-SCN_EXTERN NSString * const SCNSceneSourceAnimationImportPolicyPlayRepeatedly NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNSceneSourceAnimationImportPolicy const SCNSceneSourceAnimationImportPolicyPlayRepeatedly NS_AVAILABLE(10_10, 8_0);
+
 /*!
  @constant SCNSceneSourceAnimationImportPolicyDoNotPlay
  @abstract Only keep animations in the SCNSceneSource and don't add to the animatable elements of the scene.
  */
-SCN_EXTERN NSString * const SCNSceneSourceAnimationImportPolicyDoNotPlay NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNSceneSourceAnimationImportPolicy const SCNSceneSourceAnimationImportPolicyDoNotPlay NS_AVAILABLE(10_10, 8_0);
+
 /*!
  @constant SCNSceneSourceAnimationImportPolicyPlayUsingSceneTimeBase
  @abstract Add animations to the scene and play them using the SCNView/SCNRenderer's scene time (usesSceneTimeBase set to YES)
  */
-SCN_EXTERN NSString * const SCNSceneSourceAnimationImportPolicyPlayUsingSceneTimeBase NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNSceneSourceAnimationImportPolicy const SCNSceneSourceAnimationImportPolicyPlayUsingSceneTimeBase NS_AVAILABLE(10_10, 8_0);
+
 
 /*!
  @constant SCNDetailedErrorsKey
@@ -156,7 +190,7 @@
              in their user info dictionary using the other keys (SCNConsistency*) defined in this file.
  */
 
-SCN_EXTERN NSString * const SCNDetailedErrorsKey;
+FOUNDATION_EXTERN NSString * const SCNDetailedErrorsKey;
 
 /*!
  @constant SCNConsistencyElementIDErrorKey
@@ -164,21 +198,21 @@
  @discussion When the element does not have an ID, the ID of the closest parent element which has one is returned.
  */
 
-SCN_EXTERN NSString * const SCNConsistencyElementIDErrorKey;
+FOUNDATION_EXTERN NSString * const SCNConsistencyElementIDErrorKey;
 
 /*!
  @constant SCNConsistencyElementTypeErrorKey
  @abstract For XML-based formats, the tag name of the element where the error occurred.
  */
 
-SCN_EXTERN NSString * const SCNConsistencyElementTypeErrorKey;
+FOUNDATION_EXTERN NSString * const SCNConsistencyElementTypeErrorKey;
 
 /*!
  @constant SCNConsistencyLineNumberErrorKey
  @abstract For text-based formats, the line number where an error occurred.
  */
 
-SCN_EXTERN NSString * const SCNConsistencyLineNumberErrorKey;
+FOUNDATION_EXTERN NSString * const SCNConsistencyLineNumberErrorKey;
 
 /*!
  @enum SCNConsistencyErrorCode
@@ -208,7 +242,7 @@
 	SCNSceneSourceStatusComplete   = 16
 };
 
-typedef void (^SCNSceneSourceStatusHandler)(float totalProgress, SCNSceneSourceStatus status, NSError * __nullable error, BOOL *stop);
+typedef void (^SCNSceneSourceStatusHandler)(float totalProgress, SCNSceneSourceStatus status, NSError * _Nullable error, BOOL *stop);
 
 
 /*!
@@ -226,7 +260,7 @@
  @param url The URL to read scenes from.
  @param options An optional dictionary for future extensions. 
  */
-+ (nullable instancetype)sceneSourceWithURL:(NSURL *)url options:(nullable NSDictionary<NSString *, id> *)options;
++ (nullable instancetype)sceneSourceWithURL:(NSURL *)url options:(nullable NSDictionary<SCNSceneSourceLoadingOption, id> *)options;
 
 /*!
  @method sceneSourceWithData:options:
@@ -234,7 +268,7 @@
  @param data The scene data.
  @param options An optional dictionary for future extensions. 
  */
-+ (nullable instancetype)sceneSourceWithData:(NSData *)data options:(nullable NSDictionary<NSString *, id> *)options;
++ (nullable instancetype)sceneSourceWithData:(NSData *)data options:(nullable NSDictionary<SCNSceneSourceLoadingOption, id> *)options;
 
 /*!
  @method initWithURL:options:
@@ -242,7 +276,7 @@
  @param url The URL to read scenes from.
  @param options An optional dictionary for future extensions. 
  */
-- (nullable instancetype)initWithURL:(NSURL *)url options:(nullable NSDictionary<NSString *, id> *)options;
+- (nullable instancetype)initWithURL:(NSURL *)url options:(nullable NSDictionary<SCNSceneSourceLoadingOption, id> *)options;
 
 /*!
  @method initWithData:options:
@@ -250,7 +284,7 @@
  @param data The data to read scenes from.
  @param options An optional dictionary for future extensions. 
  */
-- (nullable instancetype)initWithData:(NSData *)data options:(nullable NSDictionary<NSString *, id> *)options;
+- (nullable instancetype)initWithData:(NSData *)data options:(nullable NSDictionary<SCNSceneSourceLoadingOption, id> *)options;
 
 /*!
  @property url
@@ -274,7 +308,7 @@
 					  - If status == SCNSceneStatusError, then error will contain more information about the failure, and the method will return nil after having called the block. Otherwise error will be nil.
 					  - Set *stop to YES if you want the source to abort the loading operation.
  */
-- (nullable SCNScene *)sceneWithOptions:(nullable NSDictionary<NSString *, id> *)options statusHandler:(nullable SCNSceneSourceStatusHandler)statusHandler;
+- (nullable SCNScene *)sceneWithOptions:(nullable NSDictionary<SCNSceneSourceLoadingOption, id> *)options statusHandler:(nullable SCNSceneSourceStatusHandler)statusHandler;
 
 /*!
  @method sceneWithOptions:error:
@@ -284,7 +318,7 @@
  @discussion This simpler version is equivalent to providing a block to sceneWithOptions:statusHandler: and checking the "error"
  parameter of the block if the status is SCNSceneStatusError.
  */
-- (nullable SCNScene *)sceneWithOptions:(nullable NSDictionary<NSString *, id> *)options error:(NSError **)error;
+- (nullable SCNScene *)sceneWithOptions:(nullable NSDictionary<SCNSceneSourceLoadingOption, id> *)options error:(NSError **)error;
 
 /*!
  @method propertyForKey:
@@ -319,7 +353,7 @@
  @param predicate The block to apply to entries in the library. The block takes three arguments: "entry" is an entry in the library, "identifier" is the ID of this entry and "stop" is a reference to a Boolean value. The block can set the value to YES to stop further processing of the library. The stop argument is an out-only argument. You should only ever set this Boolean to YES within the Block. The Block returns a Boolean value that indicates whether "entry" passed the test.
  @discussion The entry is an instance of one of following classes: SCNMaterial, SCNScene, SCNGeometry, SCNNode, CAAnimation, SCNLight, SCNCamera, SCNSkinner, SCNMorpher, NSImage.
  */
-- (NSArray<id> *)entriesPassingTest:(BOOL (^)(id entry, NSString *identifier, BOOL *stop))predicate NS_AVAILABLE(10_9, 8_0);
+- (NSArray<id> *)entriesPassingTest:(__attribute__((noescape)) BOOL (^)(id entry, NSString *identifier, BOOL *stop))predicate NS_AVAILABLE(10_9, 8_0);
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNShadable.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNShadable.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNShadable.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNShadable.h	2016-05-31 04:56:13.000000000 +0200
@@ -1,7 +1,7 @@
 //
 //  SCNShadable.h
 //
-//  Copyright (c) 2013-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2013-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
@@ -16,7 +16,11 @@
 @protocol SCNProgramDelegate;
 @protocol SCNShadable;
 
-
+#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
+typedef NSString * SCNShaderModifierEntryPoint NS_STRING_ENUM;
+#else
+typedef NSString * SCNShaderModifierEntryPoint;
+#endif
 
 /*! @enum SCNBufferFrequency
  @abstract The frequency at which the custom program input should be updated.
@@ -52,7 +56,7 @@
  @param renderedNode The node currently being rendered.
  @param renderer The renderer that is currently rendering the scene.
  */
-typedef void (^SCNBindingBlock)(unsigned int programID, unsigned int location, SCNNode *renderedNode, SCNRenderer *renderer);
+typedef void (^SCNBindingBlock)(unsigned int programID, unsigned int location,  SCNNode * _Nullable renderedNode, SCNRenderer *renderer);
 
 
 /*!
@@ -67,7 +71,7 @@
  @abstract Specifies a custom program used to render the receiver.
  @discussion When a program is set, it overrides all the rendering parameters such as material settings and shaderModifiers.
  */
-@property(nonatomic, retain, nullable) SCNProgram *program;
+@property(nonatomic, retain, nullable) SCNProgram *program __WATCHOS_PROHIBITED;
 
 /*!
  @method handleBindingOfSymbol:usingBlock:
@@ -76,7 +80,7 @@
  @param block The block to call to bind the specified symbol.
  @discussion This method can only be used with OpenGL and OpenGLES based programs.
  */
-- (void)handleBindingOfSymbol:(NSString *)symbol usingBlock:(nullable SCNBindingBlock)block NS_AVAILABLE(10_9, 8_0);
+- (void)handleBindingOfSymbol:(NSString *)symbol usingBlock:(nullable SCNBindingBlock)block NS_AVAILABLE(10_9, 8_0) __WATCHOS_PROHIBITED;
 
 /*!
  @method handleUnbindingOfSymbol:usingBlock:
@@ -85,7 +89,7 @@
  @param block The block to call to unbind the specified symbol.
  @discussion This method can only be used with OpenGL and OpenGLES based programs.
  */
-- (void)handleUnbindingOfSymbol:(NSString *)symbol usingBlock:(nullable SCNBindingBlock)block NS_AVAILABLE(10_9, 8_0);
+- (void)handleUnbindingOfSymbol:(NSString *)symbol usingBlock:(nullable SCNBindingBlock)block NS_AVAILABLE(10_9, 8_0) __WATCHOS_PROHIBITED;
 
 /*!
  @property shaderModifiers
@@ -177,7 +181,7 @@
  
  Shader modifiers can be written in GLSL or Metal. Metal shaders won't run on iOS8 and OS X 10.10 or below.
  */
-@property(nonatomic, copy, nullable) NSDictionary<NSString *, NSString *> *shaderModifiers NS_AVAILABLE(10_9, 8_0);
+@property(nonatomic, copy, nullable) NSDictionary<SCNShaderModifierEntryPoint, NSString *> *shaderModifiers NS_AVAILABLE(10_9, 8_0);
 
 @end
 
@@ -186,13 +190,13 @@
  @group Semantic options
  @abstract Valid keys for the option parameter of setSemantic:forSymbol:options:
  */
-SCN_EXTERN NSString * const SCNProgramMappingChannelKey;  /* This key is optional and may be used in association with the SCNGeometrySourceSemanticTexcoord semantic. It allows to associate a mapping channel from the geometry to a symbol from the program source code. The mapping channel allows to plug programs that work with multiple texture coordinates. The associated value must be a NSNumber(integer) greater than zero. */
+FOUNDATION_EXTERN NSString * const SCNProgramMappingChannelKey __WATCHOS_PROHIBITED; /* This key is optional and may be used in association with the SCNGeometrySourceSemanticTexcoord semantic. It allows to associate a mapping channel from the geometry to a symbol from the program source code. The mapping channel allows to plug programs that work with multiple texture coordinates. The associated value must be a NSNumber(integer) greater than zero. */
 
 /*!
  @class SCNProgram
  @abstract A SCNProgram lets you specify custom shaders to use when rendering materials.
  */
-NS_CLASS_AVAILABLE(10_8, 8_0)
+NS_CLASS_AVAILABLE(10_8, 8_0) __WATCHOS_PROHIBITED
 @interface SCNProgram : NSObject <NSCopying, NSSecureCoding>
 
 /*!
@@ -281,6 +285,7 @@
  @protocol SCNProgramDelegate
  @abstract The SCNProgramDelegate protocol declares the methods that an instance of SCNProgram invokes to delegate the binding of parameters.
  */
+__WATCHOS_PROHIBITED
 @protocol SCNProgramDelegate <NSObject>
 
 @optional
@@ -307,6 +312,7 @@
  @group Shader Modifier Entry Point
  @abstract Entry points designing the insertion point of the shader code snippet of a shader modifiers dictionary.
  */
+
 /*!
  @constant SCNShaderModifierEntryPointGeometry
  @abstract This is the entry point to operate on the geometry vertices, for example deforming them.
@@ -336,7 +342,7 @@
  uniform float Amplitude = 0.1
  _geometry.position.xyz += _geometry.normal * (Amplitude*_geometry.position.y*_geometry.position.x) * sin(u_time);
  */
-SCN_EXTERN NSString * const SCNShaderModifierEntryPointGeometry NS_AVAILABLE(10_9, 8_0);
+FOUNDATION_EXTERN SCNShaderModifierEntryPoint const SCNShaderModifierEntryPointGeometry NS_AVAILABLE(10_9, 8_0);
 
 /*!
  @constant SCNShaderModifierEntryPointSurface
@@ -364,8 +370,12 @@
  |    vec4 transparent;         // Transparent property of the fragment
  |    vec2 transparentTexcoord; // Transparent texture coordinates
  |    vec4 reflective;          // Reflective property of the fragment
- |    float shininess;          // Shininess property of the fragment.
- |    float fresnel;            // Fresnel property of the fragment.
+ |    float metalness;          // Metalness property of the fragment
+ |    vec2 metalnessTexcoord;   // Metalness texture coordinates
+ |    float roughness;          // Roughness property of the fragment
+ |    vec2 roughnessTexcoord;   // Metalness texture coordinates
+ |    float shininess;          // Shininess property of the fragment
+ |    float fresnel;            // Fresnel property of the fragment
  | } _surface;
  |
  | Access: ReadWrite
@@ -388,7 +398,7 @@
  f1 = f1 * f1 * 2.0 * (3. * 2. * f1);
  _surface.diffuse = mix(vec4(1.0), vec4(0.0), f1);
  */
-SCN_EXTERN NSString * const SCNShaderModifierEntryPointSurface NS_AVAILABLE(10_9, 8_0);
+FOUNDATION_EXTERN SCNShaderModifierEntryPoint const SCNShaderModifierEntryPointSurface NS_AVAILABLE(10_9, 8_0);
 
 /*!
  @constant SCNShaderModifierEntryPointLightingModel
@@ -429,7 +439,7 @@
  dotProduct = max(0.0, pow(max(0.0, dot(_surface.normal, halfVector)), _surface.shininess));
  _lightingContribution.specular += (dotProduct * _light.intensity.rgb);
  */
-SCN_EXTERN NSString * const SCNShaderModifierEntryPointLightingModel NS_AVAILABLE(10_9, 8_0);
+FOUNDATION_EXTERN SCNShaderModifierEntryPoint const SCNShaderModifierEntryPointLightingModel NS_AVAILABLE(10_9, 8_0);
 
 /*!
  @constant SCNShaderModifierEntryPointFragment
@@ -454,6 +464,6 @@
  
  _output.color.rgb = vec3(1.0) - _output.color.rgb;
  */
-SCN_EXTERN NSString * const SCNShaderModifierEntryPointFragment NS_AVAILABLE(10_9, 8_0);
+FOUNDATION_EXTERN SCNShaderModifierEntryPoint const SCNShaderModifierEntryPointFragment NS_AVAILABLE(10_9, 8_0);
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSkinner.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSkinner.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSkinner.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSkinner.h	2016-05-31 05:16:49.000000000 +0200
@@ -1,13 +1,17 @@
 //
 //  SCNSkinner.h
 //
-//  Copyright (c) 2013-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2013-2016 Apple Inc. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
+#import <SceneKit/SceneKitTypes.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class SCNNode;
+@class SCNGeometry;
+@class SCNGeometrySource;
+
 /*!
  @class SCNSkinner
  @abstract SCNSkinner controls the deformation of skinned geometries */
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNTechnique.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNTechnique.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNTechnique.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNTechnique.h	2016-05-31 04:56:13.000000000 +0200
@@ -1,10 +1,10 @@
 //
 //  SCNTechnique.h
 //
-//  Copyright (c) 2014-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2014-2016 Apple Inc. All rights reserved.
 //
 
-#import <Foundation/Foundation.h>
+#import <SceneKit/SCNShadable.h>
 #import <SceneKit/SCNAnimation.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -112,7 +112,7 @@
 <color states>
  A dictionary with the following optional keys:
  "clear" a boolean specifying whether the color target should be cleared or not
- "clearColor" a string specifying the clear color as 4 float (red, green, blue, alpha), or the string "sceneBackground" to clear with the scene background color.
+ "clearColor" a string specifying the clear color as 4 float ("red green blue alpha"), or the string "sceneBackground" to clear with the scene background color.
  
 <depth states>
  A dictionary with the following optional keys:
@@ -182,20 +182,30 @@
 <symbol description>
  A dictionary with the following optional keys and their possible associated values:
  
- semantic: vertex, normal, color, texcoord, time, modelViewProjectionTransform, modelViewTransform, modelTransform, viewTransform, projectionTransform, normalTransform, modelViewProjectionInverseTransform, modelViewInverseTransform, modelInverseTransform, viewInverseTransform, projectionInverseTransform, normalInverseTransform
+ semantic: vertex, normal, color, texcoord, tangent, time, modelViewProjectionTransform, modelViewTransform, modelTransform, viewTransform, projectionTransform, normalTransform, modelViewProjectionInverseTransform, modelViewInverseTransform, modelInverseTransform, viewInverseTransform, projectionInverseTransform, normalInverseTransform
  
  type: float, vec2, vec3, vec4, mat4, int, ivec2, ivec3, ivec4, mat3, sampler2D, none. Every types can also be an array of the given type by adding [N] where N is the number of elements in the array.
  
  image: name of an image located in the application bundle. (only valid when type is sampler2D)
  
  if a semantic is set, no type is required.
+ Note that with Metal shaders you should not provide any semantic. Instead simply declare a struct in you shader and add the members you need named as specified in SceneKit/scn_metal.
+ 
+ For example for a per-node semantic:
+ 
+ struct MyStruct
+ {
+ float4x4 modelTransform;
+ float4x4 modelViewProjectionTransform;
+ };
+ then in your function add an argument that must be named “scn_node” to get the members automatically filed with node semantics (see the documentation in scn_metal).
  
 <target description>
  A dictionary with the following optional keys and their possible associated values:
  
  type: a string specifying the type of the render target. It can be one of the following: color, depth, stencil
  format: a string specifying the format of the render target. It can be:
- - for color targets: rgba32f, r8, r16, rgba(default)
+ - for color targets: rgba32f, r8, r16f, rg16, rgba(default)
  - for depth targets: depth24, depth24stencil8
  - for stencil targets: depth24stencil8
  scaleFactor: a float value (encapsulated in a NSNumber) that controls the size of the render target. default to 1, which means 1x the size of the main viewport.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNTransaction.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNTransaction.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNTransaction.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNTransaction.h	2016-05-31 05:16:49.000000000 +0200
@@ -1,13 +1,15 @@
 //
 //  SCNTransaction.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <Foundation/Foundation.h>
 
 NS_ASSUME_NONNULL_BEGIN
 
+@class CAMediaTimingFunction;
+
 /* Transactions are SceneKit's mechanism for batching multiple scene graph
  * operations into atomic updates. Every
  * modification to the scene graph requires a transaction to be part of. */
@@ -31,30 +33,24 @@
 
 /* Accessors for the "animationDuration" per-thread transaction
  * property. Defines the default duration of animations. Defaults to 1/4s for explicit transactions, 0s for implicit transactions. */
-+ (CFTimeInterval)animationDuration;
-+ (void)setAnimationDuration:(CFTimeInterval)duration;
+@property(class, nonatomic) CFTimeInterval animationDuration;
 
 /* Accessors for the "animationTimingFunction" per-thread transaction
  * property. The default value is nil, when set to a non-nil value any
  * animations added to scene graph will have this value set as their
  * "timingFunction" property. */
-+ (nullable CAMediaTimingFunction *)animationTimingFunction;
-+ (void)setAnimationTimingFunction:(nullable CAMediaTimingFunction *)animationTimingFunction;
+@property(class, nonatomic, copy, nullable) CAMediaTimingFunction *animationTimingFunction __WATCHOS_PROHIBITED;
 
 /* Accessors for the "disableActions" per-thread transaction property.
  * Defines whether or not the implicit animations are performed. 
  * Defaults to NO, i.e. implicit animations enabled. */
-+ (BOOL)disableActions;
-+ (void)setDisableActions:(BOOL)flag;
+@property(class, nonatomic) BOOL disableActions;
 
 /* Accessors for the "completionBlock" per-thread transaction property.
  * Once set to a non-nil value the block is guaranteed to be called (on
  * the main thread) as soon as all animations subsequently added by
  * this transaction group have completed (or been removed). */
-#if __BLOCKS__
-+ (nullable void (^)(void))completionBlock;
-+ (void)setCompletionBlock:(nullable void (^)(void))block;
-#endif
+@property(class, nonatomic, copy, nullable) void (^completionBlock)(void);
 
 /* Associate arbitrary keyed-data with the current transaction (i.e.
  * with the current thread).
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNView.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNView.h	2016-05-31 05:16:41.000000000 +0200
@@ -1,7 +1,7 @@
 //
 //  SCNView.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
 #import <UIKit/UIKit.h>
@@ -11,41 +11,42 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-/*! 
- @enum SCNAntialiasingMode
- @abstract antialiasing modes for SCNView
- */
-typedef NS_ENUM(NSUInteger, SCNAntialiasingMode) {
-    SCNAntialiasingModeNone,
-    SCNAntialiasingModeMultisampling2X,
-    SCNAntialiasingModeMultisampling4X
-} NS_ENUM_AVAILABLE(10_10, 8_0);
+#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
+typedef NSString * SCNViewOption NS_STRING_ENUM;
+#else
+typedef NSString * SCNViewOption;
+#endif
 
-/*! @group View initialization options
- @constant SCNPreferredRenderingAPIKey Specifies the preferred rendering API to be used by the renderer.
+/*!
+ @constant SCNViewOptionPreferredRenderingAPI Specifies the preferred rendering API to be used by the renderer.
  @discussion Pass it as the key in the options dictionary given to initWithFrame:options:. The value is a NSNumber wrapping a SCNRenderingAPI. You can also select the preferred rendering API directly from the SCNView inspector in InterfaceBuilder.
  */
-SCN_EXTERN NSString * const SCNPreferredRenderingAPIKey NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXTERN SCNViewOption const SCNViewOptionPreferredRenderingAPI NS_AVAILABLE(10_12, 10_0) __WATCHOS_UNAVAILABLE;
 
 /*!
- @constant SCNPreferredDeviceKey Specifies the preferred metal device to be used by the renderer.
+ @constant SCNViewOptionPreferredDevice Specifies the preferred metal device to be used by the renderer.
  @discussion The value is directly a id <MTLDevice>.
  */
-SCN_EXTERN NSString * const SCNPreferredDeviceKey NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXTERN SCNViewOption const SCNViewOptionPreferredDevice NS_AVAILABLE(10_12, 10_0);
 
 /*!
- @constant SCNPreferLowPowerDeviceKey Specifies if the renderer should prefer a low power metal device.
+ @constant SCNViewOptionPreferLowPowerDevice Specifies if the renderer should prefer a low power metal device.
  @discussion The value is a NSNumber wrapping a BOOL. Defaults to NO.
  */
-SCN_EXTERN NSString * const SCNPreferLowPowerDeviceKey NS_AVAILABLE(10_11, 9_0);
+FOUNDATION_EXTERN SCNViewOption const SCNViewOptionPreferLowPowerDevice NS_AVAILABLE(10_12, 10_0);
+
+FOUNDATION_EXTERN NSString * const SCNPreferredRenderingAPIKey NS_AVAILABLE(10_11, 9_0) __WATCHOS_UNAVAILABLE; // Please use SCNViewOption.preferredRenderingAPI instead.
+FOUNDATION_EXTERN NSString * const SCNPreferredDeviceKey NS_AVAILABLE(10_11, 9_0);                             // Please use SCNViewOption.preferredDevice instead.
+FOUNDATION_EXTERN NSString * const SCNPreferLowPowerDeviceKey NS_AVAILABLE(10_11, 9_0);                        // Please use SCNViewOption.preferLowPowerDevice instead.
+
 
 /*!
  @class SCNView
  @abstract A SCNView is a subclass of NSView that can display a SCNScene
  */
+__WATCHOS_PROHIBITED
 @interface SCNView : UIView <SCNSceneRenderer, SCNTechniqueSupport>
 
-
 /*! 
  @method initWithFrame:options:
  @abstract Initializes and returns a newly allocated SCNView object with a specified frame rectangle.
@@ -60,19 +61,11 @@
  */
 @property(nonatomic, retain, nullable) SCNScene *scene;
 
-
 /*! 
  @property allowsCameraControl
  @abstract A Boolean value that determines whether the user can manipulate the point of view used to render the scene. 
  @discussion  When set to YES, the user can manipulate the current point of view with the mouse or the trackpad. The scene graph and existing cameras won't be modified by this action. The default value of this property is NO.
      Note that the primary purpose of this property is to aid in debugging your application. You may want to implement you own camera controller suitable for your application.
-     The built-in camera controller let you:
-       - pan with 1 finger to rotate the camera around the scene.
-       - pan with 2 fingers to translate the camera on its local X,Y plan.
-       - pan with 3 fingers vertically to move the the camera forward/backward.
-       - double tap to switch to the next camera in the scene.
-       - rotate with two fingers to roll the camera (rotation on the Z axis).
-       - pinch to zoom-in / zoom-out (change the fov of the camera).
  */
 @property(nonatomic) BOOL allowsCameraControl;
 
@@ -113,9 +106,9 @@
  @property preferredFramesPerSecond
  @abstract The rate you want the view to redraw its contents.
  @discussion When your application sets its preferred frame rate, the view chooses a frame rate as close to that as possible based on the capabilities of the screen the view is displayed on. The actual frame rate chosen is usually a factor of the maximum refresh rate of the screen to provide a consistent frame rate. For example, if the maximum refresh rate of the screen is 60 frames per second, that is also the highest frame rate the view sets as the actual frame rate. However, if you ask for a lower frame rate, it might choose 30, 20, 15 or some other factor to be the actual frame rate. Your application should choose a frame rate that it can consistently maintain.
- The default value is 60 frames per second.
+             The default value is 0 which means the display link will fire at the native cadence of the display hardware.
  */
-@property(nonatomic) NSInteger preferredFramesPerSecond;
+@property(nonatomic) NSInteger preferredFramesPerSecond NS_AVAILABLE(10_12, 8_0);
 
 /*!
  @property eaglContext
@@ -124,7 +117,6 @@
  */
 @property(nonatomic, retain, nullable) EAGLContext *eaglContext;
 
-
 /*!
  @property antialiasingMode
  @abstract Defaults to SCNAntialiasingModeMultisampling4X on OSX and SCNAntialiasingModeNone on iOS.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKit.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKit.h	2016-05-31 05:16:49.000000000 +0200
@@ -1,7 +1,7 @@
 //
 //  SceneKit.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
 /*! @framework SceneKit
@@ -9,9 +9,6 @@
     @discussion SceneKit lets you easily load, manipulate, and render 3D scenes.
  */
 
-//base
-#import <SceneKit/SCNBase.h>
-
 //types
 #import <SceneKit/SceneKitTypes.h>
 
@@ -50,10 +47,7 @@
 #import <SceneKit/SCNTechnique.h>
 #import <SceneKit/SCNReferenceNode.h>
 #import <SceneKit/SCNAudioSource.h>
-
-//bridges
-#import <SceneKit/SceneKit_simd.h>
+#import <SceneKit/SCNHitTest.h>
 
 //scripting
 #import <SceneKit/SCNJavascript.h>
-
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKitTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKitTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKitTypes.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKitTypes.h	2016-05-31 04:56:02.000000000 +0200
@@ -1,23 +1,26 @@
 //
 //  SceneKitTypes.h
 //
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
+//  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
+#import <simd/simd.h>
 #import <QuartzCore/QuartzCore.h>
 #import <GLKit/GLKMathTypes.h>
 
-
 /*! @header SceneKitTypes
  @abstract Various types and utility functions used throughout SceneKit
  */
 
-#define SCN_ENABLE_METAL (!TARGET_IPHONE_SIMULATOR)
+#define SCN_ENABLE_METAL (!TARGET_OS_SIMULATOR)
 
 #if SCN_ENABLE_METAL
 #import <Metal/Metal.h>
 #endif
 
+
+#pragma mark - Vectors
+
 typedef struct SCNVector3 {
     float x, y, z;
 } SCNVector3;
@@ -26,45 +29,66 @@
     float x, y, z, w;
 } SCNVector4;
 
-typedef struct SCNMatrix4 {
-    float m11, m12, m13, m14;
-    float m21, m22, m23, m24;
-    float m31, m32, m33, m34;
-    float m41, m42, m43, m44;
-} SCNMatrix4;
-
-typedef SCNVector4 SCNQuaternion;
+/* The null vector: [0 0 0]. */
+FOUNDATION_EXTERN const SCNVector3 SCNVector3Zero NS_AVAILABLE(10_10, 8_0);
 
-SCN_EXTERN const SCNMatrix4 SCNMatrix4Identity NS_AVAILABLE(10_10, 8_0);
-SCN_EXTERN const SCNVector3 SCNVector3Zero NS_AVAILABLE(10_10, 8_0);
-SCN_EXTERN const SCNVector4 SCNVector4Zero NS_AVAILABLE(10_10, 8_0);
+/* The null vector: [0 0 0 0]. */
+FOUNDATION_EXTERN const SCNVector4 SCNVector4Zero NS_AVAILABLE(10_10, 8_0);
 
-/*! Returns true if 'a' is exactly equal to 'b'. */
-SCN_EXTERN bool SCNVector3EqualToVector3 (SCNVector3 a, SCNVector3 b);
+/* Returns true if 'a' is exactly equal to 'b'. */
+FOUNDATION_EXTERN bool SCNVector3EqualToVector3 (SCNVector3 a, SCNVector3 b);
 
-/*! Returns true if 'a' is exactly equal to 'b'. */
-SCN_EXTERN bool SCNVector4EqualToVector4 (SCNVector4 a, SCNVector4 b);
+/* Returns true if 'a' is exactly equal to 'b'. */
+FOUNDATION_EXTERN bool SCNVector4EqualToVector4 (SCNVector4 a, SCNVector4 b);
 
-/*! Returns an initialized SCNVector3 */
+/* Returns an initialized SCNVector3 */
 NS_INLINE SCNVector3 SCNVector3Make(float x, float y, float z) {
     SCNVector3 v = {x, y, z};
     return v;
 }
 
-/*! Returns an initialized SCNVector4 */
+/* Returns an initialized SCNVector4 */
 NS_INLINE SCNVector4 SCNVector4Make(float x, float y, float z, float w) {
     SCNVector4 v = {x, y, z, w};
     return v;
 }
 
-NS_INLINE SCNMatrix4 SCNMatrix4MakeTranslation(float x, float y, float z) {
+
+#pragma mark - Quaternions
+
+typedef SCNVector4 SCNQuaternion;
+
+
+#pragma mark - Matrices
+
+typedef struct SCNMatrix4 {
+    float m11, m12, m13, m14;
+    float m21, m22, m23, m24;
+    float m31, m32, m33, m34;
+    float m41, m42, m43, m44;
+} SCNMatrix4;
+
+/* The identity matrix: [1 0 0 0; 0 1 0 0; 0 0 1 0; 0 0 0 1]. */
+FOUNDATION_EXTERN const SCNMatrix4 SCNMatrix4Identity NS_AVAILABLE(10_10, 8_0);
+
+/* Returns true if 'm' is the identity matrix. */
+FOUNDATION_EXTERN bool SCNMatrix4IsIdentity(SCNMatrix4 m) NS_AVAILABLE(10_10, 8_0);
+
+/* Returns true if 'a' is exactly equal to 'b'. */
+FOUNDATION_EXTERN bool SCNMatrix4EqualToMatrix4(SCNMatrix4 a, SCNMatrix4 b) NS_AVAILABLE(10_10, 8_0);
+
+/* Returns a transform that translates by '(tx, ty, tz)':
+ * m' =  [1 0 0 0; 0 1 0 0; 0 0 1 0; tx ty tz 1]. */
+NS_INLINE SCNMatrix4 SCNMatrix4MakeTranslation(float tx, float ty, float tz) {
     SCNMatrix4 m = SCNMatrix4Identity;
-    m.m41 = x;
-    m.m42 = y;
-    m.m43 = z;
+    m.m41 = tx;
+    m.m42 = ty;
+    m.m43 = tz;
     return m;
 }
 
+/* Returns a transform that scales by '(sx, sy, sz)':
+ * m' = [sx 0 0 0; 0 sy 0 0; 0 0 sz 0; 0 0 0 1]. */
 NS_INLINE SCNMatrix4 SCNMatrix4MakeScale(float sx, float sy, float sz) {
     SCNMatrix4 m = SCNMatrix4Identity;
     m.m11 = sx;
@@ -73,23 +97,35 @@
     return m;
 }
 
-NS_INLINE SCNMatrix4 SCNMatrix4Translate(SCNMatrix4 mat, float x, float y, float z) {
-    mat.m41 += x;
-    mat.m42 += y;
-    mat.m43 += z;
-    return mat;
+/* Returns a matrix that rotates by 'angle' radians about the vector '(x, y, z)'. */
+FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4MakeRotation(float angle, float x, float y, float z) NS_AVAILABLE(10_10, 8_0);
+
+/* Translate 'm' by '(tx, ty, tz)' and return the result:
+ * m' = translate(tx, ty, tz) * m. */
+NS_INLINE SCNMatrix4 SCNMatrix4Translate(SCNMatrix4 m, float tx, float ty, float tz) {
+    m.m41 += tx;
+    m.m42 += ty;
+    m.m43 += tz;
+    return m;
 }
 
-SCN_EXTERN SCNMatrix4 SCNMatrix4MakeRotation(float angle, float x, float y, float z) NS_AVAILABLE(10_10, 8_0);
-SCN_EXTERN SCNMatrix4 SCNMatrix4Scale(SCNMatrix4 mat, float x, float y, float z) NS_AVAILABLE(10_10, 8_0);
-SCN_EXTERN SCNMatrix4 SCNMatrix4Rotate(SCNMatrix4 mat, float angle, float x, float y, float z) NS_AVAILABLE(10_10, 8_0);
-
-SCN_EXTERN SCNMatrix4 SCNMatrix4Invert(SCNMatrix4 mat) NS_AVAILABLE(10_10, 8_0);
-SCN_EXTERN SCNMatrix4 SCNMatrix4Mult(SCNMatrix4 matA, SCNMatrix4 matB) NS_AVAILABLE(10_10, 8_0);
-SCN_EXTERN bool       SCNMatrix4IsIdentity(SCNMatrix4 mat) NS_AVAILABLE(10_10, 8_0);
-SCN_EXTERN bool       SCNMatrix4EqualToMatrix4(SCNMatrix4 matA, SCNMatrix4 matB) NS_AVAILABLE(10_10, 8_0);
+/* Scale 'm' by '(sx, sy, sz)' and return the result:
+ * m' = scale(sx, sy, sz) * m. */
+FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4Scale(SCNMatrix4 m, float sx, float sy, float sz) NS_AVAILABLE(10_10, 8_0);
+
+/* Rotate 'm' by 'angle' radians about the vector '(x, y, z)' and return the result:
+ * m' = rotation(angle, x, y, z) * m. */
+FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4Rotate(SCNMatrix4 m, float angle, float x, float y, float z) NS_AVAILABLE(10_10, 8_0);
+
+/* Invert 'm' and return the result. */
+FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4Invert(SCNMatrix4 m) NS_AVAILABLE(10_10, 8_0);
+
+/* Concatenate 'b' to 'a' and return the result: m' = a * b. */
+FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4Mult(SCNMatrix4 a, SCNMatrix4 b) NS_AVAILABLE(10_10, 8_0);
+
+
+#pragma mark - GLKit Bridge
 
-/* GLKit bridge */
 NS_INLINE SCNVector3 SCNVector3FromGLKVector3(GLKVector3 vector) {
     SCNVector3 v = (SCNVector3){vector.v[0], vector.v[1], vector.v[2]};
     return v;
@@ -110,11 +146,49 @@
     return v;
 }
 
-SCN_EXTERN GLKMatrix4 SCNMatrix4ToGLKMatrix4(SCNMatrix4 mat) NS_AVAILABLE(10_10, 8_0);
-SCN_EXTERN SCNMatrix4 SCNMatrix4FromGLKMatrix4(GLKMatrix4 mat) NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN GLKMatrix4 SCNMatrix4ToGLKMatrix4(SCNMatrix4 mat) NS_AVAILABLE(10_10, 8_0);
+FOUNDATION_EXTERN SCNMatrix4 SCNMatrix4FromGLKMatrix4(GLKMatrix4 mat) NS_AVAILABLE(10_10, 8_0);
+
+
+#pragma mark - SIMD Bridge
     
-//SIMD bridge
-#import <SceneKit/SceneKit_simd.h>
+NS_INLINE vector_float3 SCNVector3ToFloat3(SCNVector3 v) {
+    vector_float3 vec = {(float)v.x, (float)v.y, (float)v.z};
+    return vec;
+}
+
+NS_INLINE vector_float4 SCNVector4ToFloat4(SCNVector4 v) {
+    vector_float4 vec = {(float)v.x, (float)v.y, (float)v.z, (float)v.w};
+    return vec;
+}
+
+NS_INLINE matrix_float4x4 SCNMatrix4ToMat4(SCNMatrix4 m) {
+    matrix_float4x4 mat;
+    mat.columns[0] = (vector_float4){(float)m.m11, (float)m.m12, (float)m.m13, (float)m.m14};
+    mat.columns[1] = (vector_float4){(float)m.m21, (float)m.m22, (float)m.m23, (float)m.m24};
+    mat.columns[2] = (vector_float4){(float)m.m31, (float)m.m32, (float)m.m33, (float)m.m34};
+    mat.columns[3] = (vector_float4){(float)m.m41, (float)m.m42, (float)m.m43, (float)m.m44};
+    return mat;
+}
+
+NS_INLINE SCNVector3 SCNVector3FromFloat3(vector_float3 v) {
+    SCNVector3 vec = {v.x, v.y, v.z } ;
+    return vec;
+}
+
+NS_INLINE SCNVector4 SCNVector4FromFloat4(vector_float4 v) {
+    SCNVector4 vec = {v.x, v.y, v.z, v.z } ;
+    return vec;
+}
+
+NS_INLINE SCNMatrix4 SCNMatrix4FromMat4(matrix_float4x4 m) {
+    SCNMatrix4 mat;
+    memcpy(&mat, &m, sizeof(mat));
+    return mat;
+}
+
+
+#pragma mark - NSValue Additions
     
 #ifdef __OBJC__
     
@@ -136,8 +210,11 @@
 
 @end
 
+
+#pragma mark - Errors
+
 //domain for errors from SceneKit API.
-SCN_EXTERN NSString * const SCNErrorDomain;
+FOUNDATION_EXTERN NSString * const SCNErrorDomain;
 
 // NSError codes in SCNErrorDomain.
 enum {
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKit_simd.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKit_simd.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKit_simd.h	2015-09-30 23:36:45.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKit_simd.h	1970-01-01 01:00:00.000000000 +0100
@@ -1,51 +0,0 @@
-//
-//  SceneKit_simd.h
-//
-//  Copyright (c) 2012-2015 Apple Inc. All rights reserved.
-//
-
-#import <simd/simd.h>
-
-/*! @header SceneKit_simd.h
-    @abstract Bridge with the SIMD math library
- */
-
-/* vector_ext bridge */
-NS_INLINE vector_float3 SCNVector3ToFloat3(SCNVector3 v) {
-    vector_float3 vec = {(float)v.x, (float)v.y, (float)v.z};
-    return vec;
-}
-
-NS_INLINE vector_float4 SCNVector4ToFloat4(SCNVector4 v) {
-    vector_float4 vec = {(float)v.x, (float)v.y, (float)v.z, (float)v.w};
-    return vec;
-}
-
-NS_INLINE matrix_float4x4 SCNMatrix4ToMat4(SCNMatrix4 m) {
-    matrix_float4x4 mat;
-    mat.columns[0] = (vector_float4){(float)m.m11, (float)m.m12, (float)m.m13, (float)m.m14};
-    mat.columns[1] = (vector_float4){(float)m.m21, (float)m.m22, (float)m.m23, (float)m.m24};
-    mat.columns[2] = (vector_float4){(float)m.m31, (float)m.m32, (float)m.m33, (float)m.m34};
-    mat.columns[3] = (vector_float4){(float)m.m41, (float)m.m42, (float)m.m43, (float)m.m44};
-    return mat;
-}
-    
-NS_INLINE SCNVector3 SCNVector3FromFloat3(vector_float3 v) {
-    SCNVector3 vec = {v.x, v.y, v.z } ;
-    return vec;
-}
-
-NS_INLINE SCNVector4 SCNVector4FromFloat4(vector_float4 v) {
-    SCNVector4 vec = {v.x, v.y, v.z, v.z } ;
-    return vec;
-}
-
-NS_INLINE SCNMatrix4 SCNMatrix4FromMat4(matrix_float4x4 m) {
-    SCNMatrix4 mat;
-    mat.m11 = m.columns[0].x; mat.m12 = m.columns[0].y; mat.m13 = m.columns[0].z; mat.m14 = m.columns[0].w;
-    mat.m21 = m.columns[1].x; mat.m22 = m.columns[1].y; mat.m23 = m.columns[1].z; mat.m24 = m.columns[1].w;
-    mat.m31 = m.columns[2].x; mat.m32 = m.columns[2].y; mat.m33 = m.columns[2].z; mat.m34 = m.columns[2].w;
-    mat.m41 = m.columns[3].x; mat.m42 = m.columns[3].y; mat.m43 = m.columns[3].z; mat.m44 = m.columns[3].w;
-    return mat;
-}
-
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/scn_metal /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/scn_metal
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/scn_metal	2015-09-30 23:36:03.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/scn_metal	2016-05-31 05:16:49.000000000 +0200
@@ -11,7 +11,11 @@
     SCNVertexSemanticTexcoord0,
     SCNVertexSemanticTexcoord1,
     SCNVertexSemanticTexcoord2,
-    SCNVertexSemanticTexcoord3
+    SCNVertexSemanticTexcoord3,
+    SCNVertexSemanticTexcoord4,
+    SCNVertexSemanticTexcoord5,
+    SCNVertexSemanticTexcoord6,
+    SCNVertexSemanticTexcoord7
 };
 
 // This structure hold all the informations that are constant through a render pass
@@ -30,6 +34,10 @@
     float       sinTime;
     float       cosTime;
     float       random01;
+    // new in OSX 10.12 / iOS 10.0
+    float       environmentIntensity;
+    float4x4    inverseProjectionTransform;
+    float4x4    inverseViewProjectionTransform;
 };
 
 // In custom shaders or in shader modifiers, you also have access to node relative information.

```