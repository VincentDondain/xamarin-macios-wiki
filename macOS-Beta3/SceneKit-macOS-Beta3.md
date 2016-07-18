#SceneKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBoundingVolume.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBoundingVolume.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBoundingVolume.h	2016-06-26 09:09:03.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNBoundingVolume.h	2016-07-09 12:22:09.000000000 +0200
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
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNGeometry.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNGeometry.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNGeometry.h	2016-06-26 09:21:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNGeometry.h	2016-07-10 13:07:45.000000000 +0200
@@ -31,7 +31,7 @@
 #endif
 
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNGeometrySourceSemantic NS_EXTENSIBLE_STRING_ENUM;
+typedef NSString * SCNGeometrySourceSemantic NS_EXTENSIBLE_STRING_ENUM NS_SWIFT_NAME(SCNGeometrySource.Semantic);
 #else
 typedef NSString * SCNGeometrySourceSemantic;
 #endif
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNHitTest.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNHitTest.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNHitTest.h	2016-06-26 09:42:49.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNHitTest.h	2016-07-10 12:43:42.000000000 +0200
@@ -18,24 +18,24 @@
 typedef NSString * SCNHitTestOption;
 #endif
 
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionFirstFoundOnly    API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // If set to YES, returns the first object found. This object is not necessarily the nearest. Defaults to NO.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionSortResults       API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Determines whether the results should be sorted. If set to YES sorts nearest objects first. Defaults to YES.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionClipToZRange      API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // If set to YES ignores the objects clipped by the zNear/zFar range of the current point of view. Defaults to YES.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionBackFaceCulling   API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // If set to YES ignores the faces not facing to the camera. Defaults to YES.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionBoundingBoxOnly   API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // If set to YES only tests the bounding boxes of the 3D objects. Defaults to NO.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionIgnoreChildNodes  API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Determines whether the child nodes are ignored. Defaults to NO.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionRootNode          API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Specifies the root node to use for the hit test. Defaults to the root node of the scene.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionIgnoreHiddenNodes API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Determines whether hidden nodes should be ignored. Defaults to YES.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionCategoryBitMask   API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Determines the node categories to test. Defaults to all bits set.
-
-FOUNDATION_EXTERN NSString * const SCNHitTestFirstFoundOnlyKey;                                // Please use SCNHitTestOption.firstFoundOnly instead.
-FOUNDATION_EXTERN NSString * const SCNHitTestSortResultsKey;                                   // Please use SCNHitTestOption.sortResults instead.
-FOUNDATION_EXTERN NSString * const SCNHitTestClipToZRangeKey;                                  // Please use SCNHitTestOption.clipToZRange instead.
-FOUNDATION_EXTERN NSString * const SCNHitTestBackFaceCullingKey;                               // Please use SCNHitTestOption.backFaceCulling instead.
-FOUNDATION_EXTERN NSString * const SCNHitTestBoundingBoxOnlyKey;                               // Please use SCNHitTestOption.boundingBoxOnly instead.
-FOUNDATION_EXTERN NSString * const SCNHitTestIgnoreChildNodesKey;                              // Please use SCNHitTestOption.ignoreChildNodes instead.
-FOUNDATION_EXTERN NSString * const SCNHitTestRootNodeKey;                                      // Please use SCNHitTestOption.rootNode instead.
-FOUNDATION_EXTERN NSString * const SCNHitTestIgnoreHiddenNodesKey API_AVAILABLE(macosx(10.9)); // Please use SCNHitTestOption.ignoreHiddenNodes instead.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestFirstFoundOnlyKey     NS_SWIFT_NAME(firstFoundOnly);                                // If set to YES, returns the first object found. This object is not necessarily the nearest. Defaults to NO.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestSortResultsKey        NS_SWIFT_NAME(sortResults);                                   // Determines whether the results should be sorted. If set to YES sorts nearest objects first. Defaults to YES.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestClipToZRangeKey       NS_SWIFT_NAME(clipToZRange);                                  // If set to YES ignores the objects clipped by the zNear/zFar range of the current point of view. Defaults to YES.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestBackFaceCullingKey    NS_SWIFT_NAME(backFaceCulling);                               // If set to YES ignores the faces not facing to the camera. Defaults to YES.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestBoundingBoxOnlyKey    NS_SWIFT_NAME(boundingBoxOnly);                               // If set to YES only tests the bounding boxes of the 3D objects. Defaults to NO.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestIgnoreChildNodesKey   NS_SWIFT_NAME(ignoreChildNodes);                              // Determines whether the child nodes are ignored. Defaults to NO.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestRootNodeKey           NS_SWIFT_NAME(rootNode);                                      // Specifies the root node to use for the hit test. Defaults to the root node of the scene.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestIgnoreHiddenNodesKey  NS_SWIFT_NAME(ignoreHiddenNodes) API_AVAILABLE(macosx(10.9)); // Determines whether hidden nodes should be ignored. Defaults to YES.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionCategoryBitMask API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));          // Determines the node categories to test. Defaults to all bits set.
+
+#define SCNHitTestOptionFirstFoundOnly    SCNHitTestFirstFoundOnlyKey
+#define SCNHitTestOptionSortResults       SCNHitTestSortResultsKey
+#define SCNHitTestOptionClipToZRange      SCNHitTestClipToZRangeKey
+#define SCNHitTestOptionBackFaceCulling   SCNHitTestBackFaceCullingKey
+#define SCNHitTestOptionBoundingBoxOnly   SCNHitTestBoundingBoxOnlyKey
+#define SCNHitTestOptionIgnoreChildNodes  SCNHitTestIgnoreChildNodesKey
+#define SCNHitTestOptionRootNode          SCNHitTestRootNodeKey
+#define SCNHitTestOptionIgnoreHiddenNodes SCNHitTestIgnoreHiddenNodesKey
 
 /*! @class SCNHitTestResult
  @abstract Results returned by the hit-test methods.
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLight.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLight.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLight.h	2016-06-26 09:09:03.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLight.h	2016-07-09 12:22:09.000000000 +0200
@@ -18,7 +18,7 @@
  */
 
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNLightType NS_STRING_ENUM;
+typedef NSString * SCNLightType NS_STRING_ENUM NS_SWIFT_NAME(SCNLight.LightType);
 #else
 typedef NSString * SCNLightType;
 #endif
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterial.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterial.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterial.h	2016-06-26 09:09:03.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterial.h	2016-07-09 12:22:09.000000000 +0200
@@ -79,7 +79,7 @@
  */
 
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNLightingModel NS_STRING_ENUM;
+typedef NSString * SCNLightingModel NS_STRING_ENUM NS_SWIFT_NAME(SCNMaterial.LightingModel);
 #else
 typedef NSString * SCNLightingModel;
 #endif
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNNode.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNNode.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNNode.h	2016-06-26 08:35:21.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNNode.h	2016-07-10 12:41:28.000000000 +0200
@@ -24,19 +24,6 @@
 @class SCNRenderer;
 @protocol SCNNodeRendererDelegate;
 
-#if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNTransformSemantic NS_STRING_ENUM;
-#else
-typedef NSString * SCNTransformSemantic;
-#endif
-
-FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticModel API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
-FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticView API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
-FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticProjection API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
-FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticNormal API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
-FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticModelView API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
-FOUNDATION_EXTERN SCNTransformSemantic const SCNTransformSemanticModelViewProjection API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
-
 /*! @group Rendering arguments
     @discussion These keys are used for the 'semantic' argument of -[SCNProgram setSemantic:forSymbol:options:]
                 Transforms are SCNMatrix4 wrapped in NSValues.
@@ -480,7 +467,7 @@
  @param renderer The scene renderer to render into.
  @param arguments A dictionary whose values are SCNMatrix4 matrices wrapped in NSValue objects.
  */
-- (void)renderNode:(SCNNode *)node renderer:(SCNRenderer *)renderer arguments:(NSDictionary<SCNTransformSemantic, id> *)arguments;
+- (void)renderNode:(SCNNode *)node renderer:(SCNRenderer *)renderer arguments:(NSDictionary<NSString *, id> *)arguments;
 
 @end
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParticleSystem.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParticleSystem.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParticleSystem.h	2016-06-26 09:09:03.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParticleSystem.h	2016-07-09 12:22:10.000000000 +0200
@@ -14,7 +14,7 @@
 @class SCNGeometry;
 
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNParticleProperty NS_STRING_ENUM;
+typedef NSString * SCNParticleProperty NS_STRING_ENUM NS_SWIFT_NAME(SCNParticleSystem.ParticleProperty);
 #else
 typedef NSString * SCNParticleProperty;
 #endif
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsShape.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsShape.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsShape.h	2016-06-26 09:09:04.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsShape.h	2016-07-09 12:22:10.000000000 +0200
@@ -12,23 +12,23 @@
 @class SCNNode;
 
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNPhysicsShapeOption NS_STRING_ENUM;
+typedef NSString * SCNPhysicsShapeOption NS_STRING_ENUM NS_SWIFT_NAME(SCNPhysicsShape.Option);
 #else
 typedef NSString * SCNPhysicsShapeOption;
 #endif
 
-FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionType API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));            // Type of the physics shape. Default is SCNPhysicsShapeTypeConvexHull. See below for the list of shape types.
-FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionKeepAsCompound API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));  // A boolean to decide if a hierarchy is kept as a compound of shapes or flattened as one single volume. Default is true.
-FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionScale API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));           // Local scaling of the physics shape (as an SCNVector3 wrapped in a NSValue)
-FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionCollisionMargin API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Collision margin of the physics shape (as an NSNumber)
-
-FOUNDATION_EXTERN NSString * const SCNPhysicsShapeTypeKey API_AVAILABLE(macosx(10.10));           // Please use SCNPhysicsShapeOption.type instead.
-FOUNDATION_EXTERN NSString * const SCNPhysicsShapeKeepAsCompoundKey API_AVAILABLE(macosx(10.10)); // Please use SCNPhysicsShapeOption.keepAsCompound instead.
-FOUNDATION_EXTERN NSString * const SCNPhysicsShapeScaleKey API_AVAILABLE(macosx(10.10));          // Please use SCNPhysicsShapeOption.scale instead.
+FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeTypeKey               NS_SWIFT_NAME(type)           API_AVAILABLE(macosx(10.10)); // Type of the physics shape. Default is SCNPhysicsShapeTypeConvexHull. See below for the list of shape types.
+FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeKeepAsCompoundKey     NS_SWIFT_NAME(keepAsCompound) API_AVAILABLE(macosx(10.10)); // A boolean to decide if a hierarchy is kept as a compound of shapes or flattened as one single volume. Default is true.
+FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeScaleKey              NS_SWIFT_NAME(scale)          API_AVAILABLE(macosx(10.10)); // Local scaling of the physics shape (as an SCNVector3 wrapped in a NSValue)
+FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionCollisionMargin API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));        // Collision margin of the physics shape (as an NSNumber)
+
+#define SCNPhysicsShapeOptionType           SCNPhysicsShapeTypeKey
+#define SCNPhysicsShapeOptionKeepAsCompound SCNPhysicsShapeKeepAsCompoundKey
+#define SCNPhysicsShapeOptionScale          SCNPhysicsShapeScaleKey
 
 // Values for SCNPhysicsShapeOptionType
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNPhysicsShapeType NS_STRING_ENUM;
+typedef NSString * SCNPhysicsShapeType NS_STRING_ENUM NS_SWIFT_NAME(SCNPhysicsShape.ShapeType);
 #else
 typedef NSString * SCNPhysicsShapeType;
 #endif
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsWorld.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsWorld.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsWorld.h	2016-06-26 08:35:21.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsWorld.h	2016-07-10 12:41:28.000000000 +0200
@@ -17,22 +17,22 @@
 
 // Keys for ray, contact and sweep tests
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNPhysicsTestOption NS_STRING_ENUM;
+typedef NSString * SCNPhysicsTestOption NS_STRING_ENUM NS_SWIFT_NAME(SCNPhysicsWorld.TestOption);
 #else
 typedef NSString * SCNPhysicsTestOption;
 #endif
 
-FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestOptionCollisionBitMask API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Allows to filter the objects tested by rayTest, contactTest and convexSweep. Default is SCNPhysicsCollisionCategoryAll
-FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestOptionSearchMode API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));       // Specifies how to perform the ray/contact/sweep test. Values are defined below. If not defined, then defaults to SCNPhysicsTestSearchModeAny
-FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestOptionBackfaceCulling API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));  // Specifies whether the back faces should be ignored or not. Defaults to YES.
-
-FOUNDATION_EXTERN NSString * const SCNPhysicsTestCollisionBitMaskKey API_AVAILABLE(macosx(10.10)); // Please use SCNPhysicsTestOption.collisionBitMask instead.
-FOUNDATION_EXTERN NSString * const SCNPhysicsTestSearchModeKey API_AVAILABLE(macosx(10.10));       // Please use SCNPhysicsTestOption.searchMode instead.
-FOUNDATION_EXTERN NSString * const SCNPhysicsTestBackfaceCullingKey API_AVAILABLE(macosx(10.10));  // Please use SCNPhysicsTestOption.backfaceCulling instead.
+FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestCollisionBitMaskKey NS_SWIFT_NAME(collisionBitMask) API_AVAILABLE(macosx(10.10)); // Allows to filter the objects tested by rayTest, contactTest and convexSweep. Default is SCNPhysicsCollisionCategoryAll
+FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestSearchModeKey       NS_SWIFT_NAME(searchMode) API_AVAILABLE(macosx(10.10));       // Specifies how to perform the ray/contact/sweep test. Values are defined below. If not defined, then defaults to SCNPhysicsTestSearchModeAny
+FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestBackfaceCullingKey  NS_SWIFT_NAME(backfaceCulling) API_AVAILABLE(macosx(10.10));  // Specifies whether the back faces should be ignored or not. Defaults to YES.
+
+#define SCNPhysicsTestOptionCollisionBitMask SCNPhysicsTestCollisionBitMaskKey
+#define SCNPhysicsTestOptionSearchMode       SCNPhysicsTestSearchModeKey
+#define SCNPhysicsTestOptionBackfaceCulling  SCNPhysicsTestBackfaceCullingKey
 
 // Values for SCNPhysicsTestSearchModeKey
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNPhysicsTestSearchMode NS_STRING_ENUM;
+typedef NSString * SCNPhysicsTestSearchMode NS_STRING_ENUM NS_SWIFT_NAME(SCNPhysicsWorld.TestSearchMode);
 #else
 typedef NSString * SCNPhysicsTestSearchMode;
 #endif
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNScene.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNScene.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNScene.h	2016-06-26 09:09:03.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNScene.h	2016-07-09 12:22:09.000000000 +0200
@@ -38,20 +38,20 @@
     @abstract These keys can be used with the -[SCNScene attributeForKey:] method.
  */
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNSceneAttribute NS_STRING_ENUM;
+typedef NSString * SCNSceneAttribute NS_STRING_ENUM NS_SWIFT_NAME(SCNScene.Attribute);
 #else
 typedef NSString * SCNSceneAttribute;
 #endif
 
-FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneAttributeStartTime API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // A floating point value, encapsulated in a NSNumber, containing the start time of the scene.
-FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneAttributeEndTime API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));   // A floating point value, encapsulated in a NSNumber, containing the end time of the scene.
-FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneAttributeFrameRate API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // A floating point value, encapsulated in a NSNumber, containing the framerate of the scene.
-FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneAttributeUpAxis API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));    // A vector3 value, encapsulated in a NSValue, containing the up axis of the scene. This is just for information, setting the up axis as no effect.
-
-FOUNDATION_EXTERN NSString * const SCNSceneStartTimeAttributeKey;                       // Please use SCNSceneAttribute.startTime instead.
-FOUNDATION_EXTERN NSString * const SCNSceneEndTimeAttributeKey;                         // Please use SCNSceneAttribute.endTime instead.
-FOUNDATION_EXTERN NSString * const SCNSceneFrameRateAttributeKey;                       // Please use SCNSceneAttribute.frameRate instead.
-FOUNDATION_EXTERN NSString * const SCNSceneUpAxisAttributeKey API_AVAILABLE(macosx(10.10)); // Please use SCNSceneAttribute.upAxis instead.
+FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneStartTimeAttributeKey NS_SWIFT_NAME(startTime);                           // A floating point value, encapsulated in a NSNumber, containing the start time of the scene.
+FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneEndTimeAttributeKey   NS_SWIFT_NAME(endTime);                             // A floating point value, encapsulated in a NSNumber, containing the end time of the scene.
+FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneFrameRateAttributeKey NS_SWIFT_NAME(frameRate);                           // A floating point value, encapsulated in a NSNumber, containing the framerate of the scene.
+FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneUpAxisAttributeKey    NS_SWIFT_NAME(upAxis) API_AVAILABLE(macosx(10.10)); // A vector3 value, encapsulated in a NSValue, containing the up axis of the scene. This is just for information, setting the up axis as no effect.
+
+#define SCNSceneAttributeStartTime SCNSceneStartTimeAttributeKey
+#define SCNSceneAttributeEndTime   SCNSceneEndTimeAttributeKey
+#define SCNSceneAttributeFrameRate SCNSceneFrameRateAttributeKey
+#define SCNSceneAttributeUpAxis    SCNSceneUpAxisAttributeKey
 
 /*!
  @class SCNScene
@@ -158,7 +158,7 @@
              Starting macOS 10.11 exporting supports .dae, .scn as well as file all formats supported by Model I/O.
              Starting iOS 10 exporting supports .scn as well as all file formats supported by Model I/O.
  */
-- (BOOL)writeToURL:(NSURL *)url options:(nullable NSDictionary<NSString *, id> *)options delegate:(nullable id <SCNSceneExportDelegate>)delegate progressHandler:(nullable SCNSceneExportProgressHandler)progressHandler API_AVAILABLE(macosx(10.9), ios(10.0), tvos(10.0));
+- (BOOL)writeToURL:(NSURL *)url options:(nullable NSDictionary<NSString *, id> *)options delegate:(nullable id <SCNSceneExportDelegate>)delegate progressHandler:(nullable SCNSceneExportProgressHandler)progressHandler API_AVAILABLE(macosx(10.9), ios(10.0), tvos(10.0)) API_UNAVAILABLE(watchos);
 
 #pragma mark - Fog
 
@@ -201,6 +201,7 @@
 
 @end
 
+API_AVAILABLE(macosx(10.9), ios(10.0), tvos(10.0)) API_UNAVAILABLE(watchos)
 @protocol SCNSceneExportDelegate <NSObject>
 @optional
 /*!
@@ -211,7 +212,7 @@
  @param originalImageURL The original url for the image. May be nil if the image was not previously loaded from a url.
  @return The delegate must returns the url of the image that was exported or nil if it didn't export any image. If the returned value is nil, the image will be exported to a default destination in a default format.
  */
-- (nullable NSURL *)writeImage:(NSImage *)image withSceneDocumentURL:(NSURL *)documentURL originalImageURL:(nullable NSURL *)originalImageURL API_AVAILABLE(macosx(10.9), ios(NA));
+- (nullable NSURL *)writeImage:(NSImage *)image withSceneDocumentURL:(NSURL *)documentURL originalImageURL:(nullable NSURL *)originalImageURL API_AVAILABLE(macosx(10.9), ios(10.0), tvos(10.0)) API_UNAVAILABLE(watchos);
 
 @end
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneSource.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneSource.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneSource.h	2016-06-26 09:21:12.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneSource.h	2016-07-10 13:07:45.000000000 +0200
@@ -36,19 +36,19 @@
 
 /*! @group Scene loading options */
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNSceneSourceLoadingOption NS_STRING_ENUM;
+typedef NSString * SCNSceneSourceLoadingOption NS_STRING_ENUM NS_SWIFT_NAME(SCNSceneSource.LoadingOption);
 #else
 typedef NSString * SCNSceneSourceLoadingOption;
 #endif
 
-/*! @constant SCNSceneSourceLoadingOptionCreateNormalsIfAbsent
+/*! @constant SCNSceneSourceCreateNormalsIfAbsentKey
 	@abstract Enable to try to guess acceptable normals for the vertices if none are given in the file
     @discussion Use this with a boolean value encapsulated in a NSNumber. The default value is NO.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionCreateNormalsIfAbsent API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceCreateNormalsIfAbsentKey NS_SWIFT_NAME(createNormalsIfAbsent);
 
 /*!
- @constant SCNSceneSourceLoadingOptionCheckConsistency
+ @constant SCNSceneSourceCheckConsistencyKey
  @abstract Pass YES in order to perform the document validation. 
  @discussion This option can be set in the options dictionary of the SCNScene and SCNSceneSource loading methods.
  The value for this option should be a boolean NSNumber. If its boolean value is YES (the default is NO),
@@ -56,79 +56,79 @@
  If the document doesn't pass the consistency check it is then not loaded and an error is returned.
  This is slower, but for security reasons it should be set to YES if you are not sure the files you load are valid and have not been tampered with. 
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionCheckConsistency API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceCheckConsistencyKey NS_SWIFT_NAME(checkConsistency);
 
 /*!
- @constant SCNSceneSourceLoadingOptionFlattenScene
+ @constant SCNSceneSourceFlattenSceneKey
  @abstract Pass YES to flatten the scene graph when possible.
  @discussion This option can be set in the options dictionary of the SCNScene and SCNSceneSource loading methods.
  The value for this option should be a boolean NSNumber. If its boolean value is YES (the default is NO),
  SceneKit will attempt to reduce the scene graph by merging the geometries.
  This option is suitable to preview a 3D scene efficiently and when manipulating the scene graph is not needed.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionFlattenScene API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceFlattenSceneKey NS_SWIFT_NAME(flattenScene);
 
 /*!
- @constant SCNSceneSourceLoadingOptionUseSafeMode
+ @constant SCNSceneSourceUseSafeModeKey
  @abstract Pass YES in order to enable the safe mode.
  @discussion This option can be set in the options dictionary of the SCNScene and SCNSceneSource loading methods.
  The value for this option should be a boolean NSNumber. If its boolean value is YES (the default is NO),
  SceneKit will forbid network accesses, prevent the loading of resources from arbitrary directories, and will not execute
  any code present in the loaded files.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionUseSafeMode API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceUseSafeModeKey NS_SWIFT_NAME(useSafeMode);
 
 /*!
- @constant SCNSceneSourceLoadingOptionAssetDirectoryURLs
+ @constant SCNSceneSourceAssetDirectoryURLsKey
  @abstract Pass an array of directory URLs where SceneKit should look for resources
  @discussion By default, SceneKit will look for the external resources it cannot find in the parent directory of the imported file.
  You can add additional directories by setting an array of URLs for this key when calling sceneWithOptions:error:.
  This is recommended if you want to construct your scene source from a data object, not from an URL,
  and need to load resources whose paths are not absolute.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionAssetDirectoryURLs API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceAssetDirectoryURLsKey NS_SWIFT_NAME(assetDirectoryURLs);
 
 /*!
- @constant SCNSceneSourceLoadingOptionOverrideAssetURLs
+ @constant SCNSceneSourceOverrideAssetURLsKey
  @abstract Pass YES in order to override assets URLs with the directory URLs passed via SCNSceneSourceAssetDirectoryURLsKey.
  @discussion By default, SceneKit will look for the external resources using the paths/urls as described in the imported file.
  You can force SceneKit to only search for extern resources within the directories specified by the SCNSceneSourceAssetDirectoryURLsKey key.
  This can be useful to load a file and its resources from a specific bundle for instance.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionOverrideAssetURLs API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceOverrideAssetURLsKey NS_SWIFT_NAME(overrideAssetURLs);
 
 /*!
- @constant SCNSceneSourceLoadingOptionStrictConformance
+ @constant SCNSceneSourceStrictConformanceKey
  @abstract Pass YES to interpret the 3D format of the file in a strict way.
  @discussion This option defaults to NO. In this case SceneKit will try to read any additional metadata present in the file to
 			 enable additional features and make the rendering as close as possible to the original intent. If you pass YES,
              SceneKit will instead only consider features which are part of the file format specification.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionStrictConformance API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceStrictConformanceKey NS_SWIFT_NAME(strictConformance);
 
 /*!
- @constant SCNSceneSourceLoadingOptionConvertUnitsToMeters
+ @constant SCNSceneSourceConvertUnitsToMetersKey
  @abstract Pass the units you want the scene to be converted to (in meter).
  @discussion Use this with a floating value encapsulated in a NSNumber. The default value is nil which means no conversion done. Passing a non-zero value will convert the scene coordinates so that 1 unit corresponds to N meters. For example pass 0.01 for 1 unit == 1 centimeter, pass 0.3048 for 1 unit == 1 foot...
      For better physics simulation it is recommended to use 1 unit equals to 1 meter.
      This option has no effect if the asset is already compressed by Xcode (use the compression options instead).
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionConvertUnitsToMeters API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceConvertUnitsToMetersKey NS_SWIFT_NAME(convertUnitsToMeters) API_AVAILABLE(macosx(10.10)) API_UNAVAILABLE(ios, tvos, watchos);
 
 /*!
- @constant SCNSceneSourceLoadingOptionConvertToYUp
+ @constant SCNSceneSourceConvertToYUpKey
  @abstract Pass YES if a scene should be converted to Y up if it currently has a different up axis.
  @discussion Use this with a boolean value encapsulated in a NSNumber. The default value is NO.
  This option has no effect if the asset is already compressed by Xcode (use the compression options instead).
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionConvertToYUp API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceConvertToYUpKey NS_SWIFT_NAME(convertToYUp) API_AVAILABLE(macosx(10.10)) API_UNAVAILABLE(ios, tvos, watchos);
 
 /*!
- @constant SCNSceneSourceLoadingOptionAnimationImportPolicy
+ @constant SCNSceneSourceAnimationImportPolicyKey
  @abstract Pass one of the value below to specify what to do with loaded animations.
  @discussion See below for the description of each individual key. Defaults to SCNSceneSourceAnimationImportPolicyPlayRepeatedly. On 10.9 and before the behavior is SCNSceneSourceAnimationImportPolicyPlayUsingSceneTimeBase. For compatibility reason if the application was built on 10.9 or before the default behavior is SCNSceneSourceAnimationImportPolicyPlayUsingSceneTimeBase.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionAnimationImportPolicy API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceAnimationImportPolicyKey NS_SWIFT_NAME(animationImportPolicy) API_AVAILABLE(macosx(10.10));
 
 /*!
  @constant SCNSceneSourceLoadingOptionPreserveOriginalTopology
@@ -137,21 +137,20 @@
  */
 FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceLoadingOptionPreserveOriginalTopology API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
 
-FOUNDATION_EXTERN NSString * const SCNSceneSourceCreateNormalsIfAbsentKey;                          // Please use SCNSceneSourceLoadingOption.createNormalsIfAbsent instead.
-FOUNDATION_EXTERN NSString * const SCNSceneSourceCheckConsistencyKey;                               // Please use SCNSceneSourceLoadingOption.checkConsistency instead.
-FOUNDATION_EXTERN NSString * const SCNSceneSourceFlattenSceneKey;                                   // Please use SCNSceneSourceLoadingOption.flattenScene instead.
-FOUNDATION_EXTERN NSString * const SCNSceneSourceUseSafeModeKey;                                    // Please use SCNSceneSourceLoadingOption.useSafeMode instead.
-FOUNDATION_EXTERN NSString * const SCNSceneSourceAssetDirectoryURLsKey;                             // Please use SCNSceneSourceLoadingOption.assetDirectoryURLs instead.
-FOUNDATION_EXTERN NSString * const SCNSceneSourceOverrideAssetURLsKey;                              // Please use SCNSceneSourceLoadingOption.overrideAssetURLs instead.
-FOUNDATION_EXTERN NSString * const SCNSceneSourceStrictConformanceKey;                              // Please use SCNSceneSourceLoadingOption.strictConformance instead.
-FOUNDATION_EXTERN NSString * const SCNSceneSourceConvertUnitsToMetersKey API_AVAILABLE(macosx(10.10), ios(NA));   // Please use SCNSceneSourceLoadingOption.convertUnitsToMeters instead.
-FOUNDATION_EXTERN NSString * const SCNSceneSourceConvertToYUpKey API_AVAILABLE(macosx(10.10), ios(NA));           // Please use SCNSceneSourceLoadingOption.convertToYUp instead.
-FOUNDATION_EXTERN NSString * const SCNSceneSourceAnimationImportPolicyKey API_AVAILABLE(macosx(10.10)); // Please use SCNSceneSourceLoadingOption.animationImportPolicy instead.
-
+#define SCNSceneSourceLoadingOptionCreateNormalsIfAbsent    SCNSceneSourceCreateNormalsIfAbsentKey
+#define SCNSceneSourceLoadingOptionCheckConsistency         SCNSceneSourceCheckConsistencyKey
+#define SCNSceneSourceLoadingOptionFlattenScene             SCNSceneSourceFlattenSceneKey
+#define SCNSceneSourceLoadingOptionUseSafeMode              SCNSceneSourceUseSafeModeKey
+#define SCNSceneSourceLoadingOptionAssetDirectoryURLs       SCNSceneSourceAssetDirectoryURLsKey
+#define SCNSceneSourceLoadingOptionOverrideAssetURLs        SCNSceneSourceOverrideAssetURLsKey
+#define SCNSceneSourceLoadingOptionStrictConformance        SCNSceneSourceStrictConformanceKey
+#define SCNSceneSourceLoadingOptionConvertUnitsToMeters     SCNSceneSourceConvertUnitsToMetersKey
+#define SCNSceneSourceLoadingOptionConvertToYUp             SCNSceneSourceConvertToYUpKey
+#define SCNSceneSourceLoadingOptionAnimationImportPolicy    SCNSceneSourceAnimationImportPolicyKey
 
 /* Values for SCNSceneSourceLoadingOptionAnimationImportPolicy */
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNSceneSourceAnimationImportPolicy NS_STRING_ENUM;
+typedef NSString * SCNSceneSourceAnimationImportPolicy NS_STRING_ENUM NS_SWIFT_NAME(SCNSceneSource.AnimationImportPolicy);
 #else
 typedef NSString * SCNSceneSourceAnimationImportPolicy;
 #endif
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNShadable.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNShadable.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNShadable.h	2016-06-26 09:09:04.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNShadable.h	2016-07-09 12:22:10.000000000 +0200
@@ -221,19 +221,19 @@
  @property tessellationControlShader
  @abstract Determines the receiver's tessellation control shader. Tessellation shaders require OpenGL Core Profile.
  */
-@property(nonatomic, copy, nullable) NSString *tessellationControlShader API_AVAILABLE(macosx(10.10), ios(NA));
+@property(nonatomic, copy, nullable) NSString *tessellationControlShader API_AVAILABLE(macosx(10.10)) API_UNAVAILABLE(ios, tvos, watchos);
 
 /*!
  @property tessellationEvaluationShader
  @abstract Determines the receiver's tessellation evaluation shader. Tessellation shaders require OpenGL Core Profile.
  */
-@property(nonatomic, copy, nullable) NSString *tessellationEvaluationShader API_AVAILABLE(macosx(10.10), ios(NA));
+@property(nonatomic, copy, nullable) NSString *tessellationEvaluationShader API_AVAILABLE(macosx(10.10)) API_UNAVAILABLE(ios, tvos, watchos);
 
 /*!
  @property geometryShader
  @abstract Determines the receiver's geometry shader. Geometry shaders require OpenGL Core Profile.
  */
-@property(nonatomic, copy, nullable) NSString *geometryShader API_AVAILABLE(macosx(10.10), ios(NA));
+@property(nonatomic, copy, nullable) NSString *geometryShader API_AVAILABLE(macosx(10.10)) API_UNAVAILABLE(ios, tvos, watchos);
 
 /*!
  @property vertexFunctionName
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNView.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNView.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNView.h	2016-06-26 09:09:03.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNView.h	2016-07-09 12:22:09.000000000 +0200
@@ -12,7 +12,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNViewOption NS_STRING_ENUM;
+typedef NSString * SCNViewOption NS_STRING_ENUM NS_SWIFT_NAME(SCNView.Option);
 #else
 typedef NSString * SCNViewOption;
 #endif
@@ -21,24 +21,23 @@
  @constant SCNViewOptionPreferredRenderingAPI Specifies the preferred rendering API to be used by the renderer.
  @discussion Pass it as the key in the options dictionary given to initWithFrame:options:. The value is a NSNumber wrapping a SCNRenderingAPI. You can also select the preferred rendering API directly from the SCNView inspector in InterfaceBuilder.
  */
-FOUNDATION_EXTERN SCNViewOption const SCNViewOptionPreferredRenderingAPI API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)) __WATCHOS_UNAVAILABLE;
+FOUNDATION_EXTERN SCNViewOption const SCNPreferredRenderingAPIKey NS_SWIFT_NAME(preferredRenderingAPI) API_AVAILABLE(macosx(10.11), ios(9.0)) __WATCHOS_UNAVAILABLE;
 
 /*!
  @constant SCNViewOptionPreferredDevice Specifies the preferred metal device to be used by the renderer.
  @discussion The value is directly a id <MTLDevice>.
  */
-FOUNDATION_EXTERN SCNViewOption const SCNViewOptionPreferredDevice API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
+FOUNDATION_EXTERN SCNViewOption const SCNPreferredDeviceKey NS_SWIFT_NAME(preferredDevice) API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @constant SCNViewOptionPreferLowPowerDevice Specifies if the renderer should prefer a low power metal device.
  @discussion The value is a NSNumber wrapping a BOOL. Defaults to NO.
  */
-FOUNDATION_EXTERN SCNViewOption const SCNViewOptionPreferLowPowerDevice API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));
-
-FOUNDATION_EXTERN NSString * const SCNPreferredRenderingAPIKey API_AVAILABLE(macosx(10.11), ios(9.0)) __WATCHOS_UNAVAILABLE; // Please use SCNViewOption.preferredRenderingAPI instead.
-FOUNDATION_EXTERN NSString * const SCNPreferredDeviceKey API_AVAILABLE(macosx(10.11), ios(9.0));                             // Please use SCNViewOption.preferredDevice instead.
-FOUNDATION_EXTERN NSString * const SCNPreferLowPowerDeviceKey API_AVAILABLE(macosx(10.11), ios(9.0));                        // Please use SCNViewOption.preferLowPowerDevice instead.
+FOUNDATION_EXTERN SCNViewOption const SCNPreferLowPowerDeviceKey NS_SWIFT_NAME(preferLowPowerDevice) API_AVAILABLE(macosx(10.11), ios(9.0));
 
+#define SCNViewOptionPreferredRenderingAPI SCNPreferredRenderingAPIKey
+#define SCNViewOptionPreferredDevice       SCNPreferredDeviceKey
+#define SCNViewOptionPreferLowPowerDevice  SCNPreferLowPowerDeviceKey
 
 /*!
  @class SCNView
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKitTypes.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKitTypes.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKitTypes.h	2016-06-26 09:09:03.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKitTypes.h	2016-07-09 12:22:09.000000000 +0200
@@ -4,7 +4,10 @@
 //  Copyright (c) 2012-2016 Apple Inc. All rights reserved.
 //
 
+#import <Foundation/Foundation.h>
+#import <CoreGraphics/CoreGraphics.h>
 #import <simd/simd.h>
+
 #import <QuartzCore/QuartzCore.h>
 #import <GLKit/GLKMathTypes.h>
 

```