#SceneKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNGeometry.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNGeometry.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNGeometry.h	2016-07-23 01:48:33.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNGeometry.h	2016-08-05 08:59:47.000000000 +0200
@@ -31,7 +31,7 @@
 #endif
 
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNGeometrySourceSemantic NS_EXTENSIBLE_STRING_ENUM NS_SWIFT_NAME(SCNGeometrySource.Semantic);
+typedef NSString * SCNGeometrySourceSemantic NS_EXTENSIBLE_STRING_ENUM;
 #else
 typedef NSString * SCNGeometrySourceSemantic;
 #endif
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNHitTest.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNHitTest.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNHitTest.h	2016-07-23 00:54:58.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNHitTest.h	2016-08-05 08:21:07.000000000 +0200
@@ -18,15 +18,15 @@
 typedef NSString * SCNHitTestOption;
 #endif
 
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestFirstFoundOnlyKey     NS_SWIFT_NAME(firstFoundOnly);                                // If set to YES, returns the first object found. This object is not necessarily the nearest. Defaults to NO.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestSortResultsKey        NS_SWIFT_NAME(sortResults);                                   // Determines whether the results should be sorted. If set to YES sorts nearest objects first. Defaults to YES.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestClipToZRangeKey       NS_SWIFT_NAME(clipToZRange);                                  // If set to YES ignores the objects clipped by the zNear/zFar range of the current point of view. Defaults to YES.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestBackFaceCullingKey    NS_SWIFT_NAME(backFaceCulling);                               // If set to YES ignores the faces not facing to the camera. Defaults to YES.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestBoundingBoxOnlyKey    NS_SWIFT_NAME(boundingBoxOnly);                               // If set to YES only tests the bounding boxes of the 3D objects. Defaults to NO.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestIgnoreChildNodesKey   NS_SWIFT_NAME(ignoreChildNodes);                              // Determines whether the child nodes are ignored. Defaults to NO.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestRootNodeKey           NS_SWIFT_NAME(rootNode);                                      // Specifies the root node to use for the hit test. Defaults to the root node of the scene.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestIgnoreHiddenNodesKey  NS_SWIFT_NAME(ignoreHiddenNodes) API_AVAILABLE(macosx(10.9)); // Determines whether hidden nodes should be ignored. Defaults to YES.
-FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionCategoryBitMask API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));          // Determines the node categories to test. Defaults to all bits set.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestFirstFoundOnlyKey;                                                         // If set to YES, returns the first object found. This object is not necessarily the nearest. Defaults to NO.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestSortResultsKey;                                                            // Determines whether the results should be sorted. If set to YES sorts nearest objects first. Defaults to YES.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestClipToZRangeKey;                                                           // If set to YES ignores the objects clipped by the zNear/zFar range of the current point of view. Defaults to YES.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestBackFaceCullingKey;                                                        // If set to YES ignores the faces not facing to the camera. Defaults to YES.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestBoundingBoxOnlyKey;                                                        // If set to YES only tests the bounding boxes of the 3D objects. Defaults to NO.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestIgnoreChildNodesKey;                                                       // Determines whether the child nodes are ignored. Defaults to NO.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestRootNodeKey;                                                               // Specifies the root node to use for the hit test. Defaults to the root node of the scene.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestIgnoreHiddenNodesKey  API_AVAILABLE(macosx(10.9));                         // Determines whether hidden nodes should be ignored. Defaults to YES.
+FOUNDATION_EXTERN SCNHitTestOption const SCNHitTestOptionCategoryBitMask API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Determines the node categories to test. Defaults to all bits set.
 
 #define SCNHitTestOptionFirstFoundOnly    SCNHitTestFirstFoundOnlyKey
 #define SCNHitTestOptionSortResults       SCNHitTestSortResultsKey
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLight.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLight.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLight.h	2016-07-23 01:30:59.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNLight.h	2016-08-05 09:19:26.000000000 +0200
@@ -18,7 +18,7 @@
  */
 
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNLightType NS_STRING_ENUM NS_SWIFT_NAME(SCNLight.LightType);
+typedef NSString * SCNLightType NS_STRING_ENUM;
 #else
 typedef NSString * SCNLightType;
 #endif
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterial.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterial.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterial.h	2016-07-23 01:15:30.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNMaterial.h	2016-08-05 08:49:49.000000000 +0200
@@ -79,7 +79,7 @@
  */
 
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNLightingModel NS_STRING_ENUM NS_SWIFT_NAME(SCNMaterial.LightingModel);
+typedef NSString * SCNLightingModel NS_STRING_ENUM;
 #else
 typedef NSString * SCNLightingModel;
 #endif
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParticleSystem.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParticleSystem.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParticleSystem.h	2016-07-23 00:54:59.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNParticleSystem.h	2016-08-05 08:59:47.000000000 +0200
@@ -14,7 +14,7 @@
 @class SCNGeometry;
 
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNParticleProperty NS_STRING_ENUM NS_SWIFT_NAME(SCNParticleSystem.ParticleProperty);
+typedef NSString * SCNParticleProperty NS_STRING_ENUM;
 #else
 typedef NSString * SCNParticleProperty;
 #endif
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsShape.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsShape.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsShape.h	2016-07-23 00:24:48.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsShape.h	2016-08-05 09:19:31.000000000 +0200
@@ -12,15 +12,15 @@
 @class SCNNode;
 
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNPhysicsShapeOption NS_STRING_ENUM NS_SWIFT_NAME(SCNPhysicsShape.Option);
+typedef NSString * SCNPhysicsShapeOption NS_STRING_ENUM;
 #else
 typedef NSString * SCNPhysicsShapeOption;
 #endif
 
-FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeTypeKey               NS_SWIFT_NAME(type)           API_AVAILABLE(macosx(10.10)); // Type of the physics shape. Default is SCNPhysicsShapeTypeConvexHull. See below for the list of shape types.
-FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeKeepAsCompoundKey     NS_SWIFT_NAME(keepAsCompound) API_AVAILABLE(macosx(10.10)); // A boolean to decide if a hierarchy is kept as a compound of shapes or flattened as one single volume. Default is true.
-FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeScaleKey              NS_SWIFT_NAME(scale)          API_AVAILABLE(macosx(10.10)); // Local scaling of the physics shape (as an SCNVector3 wrapped in a NSValue)
-FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionCollisionMargin API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0));        // Collision margin of the physics shape (as an NSNumber)
+FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeTypeKey               API_AVAILABLE(macosx(10.10));                        // Type of the physics shape. Default is SCNPhysicsShapeTypeConvexHull. See below for the list of shape types.
+FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeKeepAsCompoundKey     API_AVAILABLE(macosx(10.10));                        // A boolean to decide if a hierarchy is kept as a compound of shapes or flattened as one single volume. Default is true.
+FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeScaleKey              API_AVAILABLE(macosx(10.10));                        // Local scaling of the physics shape (as an SCNVector3 wrapped in a NSValue)
+FOUNDATION_EXTERN SCNPhysicsShapeOption const SCNPhysicsShapeOptionCollisionMargin API_AVAILABLE(macosx(10.12), ios(10.0), tvos(10.0)); // Collision margin of the physics shape (as an NSNumber)
 
 #define SCNPhysicsShapeOptionType           SCNPhysicsShapeTypeKey
 #define SCNPhysicsShapeOptionKeepAsCompound SCNPhysicsShapeKeepAsCompoundKey
@@ -28,7 +28,7 @@
 
 // Values for SCNPhysicsShapeOptionType
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNPhysicsShapeType NS_STRING_ENUM NS_SWIFT_NAME(SCNPhysicsShape.ShapeType);
+typedef NSString * SCNPhysicsShapeType NS_STRING_ENUM;
 #else
 typedef NSString * SCNPhysicsShapeType;
 #endif
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsWorld.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsWorld.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsWorld.h	2016-07-23 01:48:33.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNPhysicsWorld.h	2016-08-05 09:19:31.000000000 +0200
@@ -17,14 +17,14 @@
 
 // Keys for ray, contact and sweep tests
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNPhysicsTestOption NS_STRING_ENUM NS_SWIFT_NAME(SCNPhysicsWorld.TestOption);
+typedef NSString * SCNPhysicsTestOption NS_STRING_ENUM;
 #else
 typedef NSString * SCNPhysicsTestOption;
 #endif
 
-FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestCollisionBitMaskKey NS_SWIFT_NAME(collisionBitMask) API_AVAILABLE(macosx(10.10)); // Allows to filter the objects tested by rayTest, contactTest and convexSweep. Default is SCNPhysicsCollisionCategoryAll
-FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestSearchModeKey       NS_SWIFT_NAME(searchMode) API_AVAILABLE(macosx(10.10));       // Specifies how to perform the ray/contact/sweep test. Values are defined below. If not defined, then defaults to SCNPhysicsTestSearchModeAny
-FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestBackfaceCullingKey  NS_SWIFT_NAME(backfaceCulling) API_AVAILABLE(macosx(10.10));  // Specifies whether the back faces should be ignored or not. Defaults to YES.
+FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestCollisionBitMaskKey API_AVAILABLE(macosx(10.10)); // Allows to filter the objects tested by rayTest, contactTest and convexSweep. Default is SCNPhysicsCollisionCategoryAll
+FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestSearchModeKey       API_AVAILABLE(macosx(10.10)); // Specifies how to perform the ray/contact/sweep test. Values are defined below. If not defined, then defaults to SCNPhysicsTestSearchModeAny
+FOUNDATION_EXTERN SCNPhysicsTestOption const SCNPhysicsTestBackfaceCullingKey  API_AVAILABLE(macosx(10.10)); // Specifies whether the back faces should be ignored or not. Defaults to YES.
 
 #define SCNPhysicsTestOptionCollisionBitMask SCNPhysicsTestCollisionBitMaskKey
 #define SCNPhysicsTestOptionSearchMode       SCNPhysicsTestSearchModeKey
@@ -32,14 +32,14 @@
 
 // Values for SCNPhysicsTestSearchModeKey
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNPhysicsTestSearchMode NS_STRING_ENUM NS_SWIFT_NAME(SCNPhysicsWorld.TestSearchMode);
+typedef NSString * SCNPhysicsTestSearchMode NS_STRING_ENUM;
 #else
 typedef NSString * SCNPhysicsTestSearchMode;
 #endif
 
-FOUNDATION_EXTERN SCNPhysicsTestSearchMode const SCNPhysicsTestSearchModeAny API_AVAILABLE(macosx(10.10));     // Returns the first contact found.
+FOUNDATION_EXTERN SCNPhysicsTestSearchMode const SCNPhysicsTestSearchModeAny     API_AVAILABLE(macosx(10.10)); // Returns the first contact found.
 FOUNDATION_EXTERN SCNPhysicsTestSearchMode const SCNPhysicsTestSearchModeClosest API_AVAILABLE(macosx(10.10)); // Returns the nearest contact found only.
-FOUNDATION_EXTERN SCNPhysicsTestSearchMode const SCNPhysicsTestSearchModeAll API_AVAILABLE(macosx(10.10));     // All contacts are returned.
+FOUNDATION_EXTERN SCNPhysicsTestSearchMode const SCNPhysicsTestSearchModeAll     API_AVAILABLE(macosx(10.10)); // All contacts are returned.
 
 /*!
  @protocol SCNPhysicsContactDelegate
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNScene.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNScene.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNScene.h	2016-07-23 00:54:59.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNScene.h	2016-08-05 09:19:26.000000000 +0200
@@ -38,15 +38,15 @@
     @abstract These keys can be used with the -[SCNScene attributeForKey:] method.
  */
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNSceneAttribute NS_STRING_ENUM NS_SWIFT_NAME(SCNScene.Attribute);
+typedef NSString * SCNSceneAttribute NS_STRING_ENUM;
 #else
 typedef NSString * SCNSceneAttribute;
 #endif
 
-FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneStartTimeAttributeKey NS_SWIFT_NAME(startTime);                           // A floating point value, encapsulated in a NSNumber, containing the start time of the scene.
-FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneEndTimeAttributeKey   NS_SWIFT_NAME(endTime);                             // A floating point value, encapsulated in a NSNumber, containing the end time of the scene.
-FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneFrameRateAttributeKey NS_SWIFT_NAME(frameRate);                           // A floating point value, encapsulated in a NSNumber, containing the framerate of the scene.
-FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneUpAxisAttributeKey    NS_SWIFT_NAME(upAxis) API_AVAILABLE(macosx(10.10)); // A vector3 value, encapsulated in a NSValue, containing the up axis of the scene. This is just for information, setting the up axis as no effect.
+FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneStartTimeAttributeKey;                           // A floating point value, encapsulated in a NSNumber, containing the start time of the scene.
+FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneEndTimeAttributeKey;                             // A floating point value, encapsulated in a NSNumber, containing the end time of the scene.
+FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneFrameRateAttributeKey;                           // A floating point value, encapsulated in a NSNumber, containing the framerate of the scene.
+FOUNDATION_EXTERN SCNSceneAttribute const SCNSceneUpAxisAttributeKey API_AVAILABLE(macosx(10.10)); // A vector3 value, encapsulated in a NSValue, containing the up axis of the scene. This is just for information, setting the up axis as no effect.
 
 #define SCNSceneAttributeStartTime SCNSceneStartTimeAttributeKey
 #define SCNSceneAttributeEndTime   SCNSceneEndTimeAttributeKey
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneSource.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneSource.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneSource.h	2016-07-23 01:48:33.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNSceneSource.h	2016-08-05 08:22:33.000000000 +0200
@@ -36,7 +36,7 @@
 
 /*! @group Scene loading options */
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNSceneSourceLoadingOption NS_STRING_ENUM NS_SWIFT_NAME(SCNSceneSource.LoadingOption);
+typedef NSString * SCNSceneSourceLoadingOption NS_STRING_ENUM;
 #else
 typedef NSString * SCNSceneSourceLoadingOption;
 #endif
@@ -45,7 +45,7 @@
 	@abstract Enable to try to guess acceptable normals for the vertices if none are given in the file
     @discussion Use this with a boolean value encapsulated in a NSNumber. The default value is NO.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceCreateNormalsIfAbsentKey NS_SWIFT_NAME(createNormalsIfAbsent);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceCreateNormalsIfAbsentKey;
 
 /*!
  @constant SCNSceneSourceCheckConsistencyKey
@@ -56,7 +56,7 @@
  If the document doesn't pass the consistency check it is then not loaded and an error is returned.
  This is slower, but for security reasons it should be set to YES if you are not sure the files you load are valid and have not been tampered with. 
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceCheckConsistencyKey NS_SWIFT_NAME(checkConsistency);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceCheckConsistencyKey;
 
 /*!
  @constant SCNSceneSourceFlattenSceneKey
@@ -66,7 +66,7 @@
  SceneKit will attempt to reduce the scene graph by merging the geometries.
  This option is suitable to preview a 3D scene efficiently and when manipulating the scene graph is not needed.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceFlattenSceneKey NS_SWIFT_NAME(flattenScene);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceFlattenSceneKey;
 
 /*!
  @constant SCNSceneSourceUseSafeModeKey
@@ -76,7 +76,7 @@
  SceneKit will forbid network accesses, prevent the loading of resources from arbitrary directories, and will not execute
  any code present in the loaded files.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceUseSafeModeKey NS_SWIFT_NAME(useSafeMode);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceUseSafeModeKey;
 
 /*!
  @constant SCNSceneSourceAssetDirectoryURLsKey
@@ -86,7 +86,7 @@
  This is recommended if you want to construct your scene source from a data object, not from an URL,
  and need to load resources whose paths are not absolute.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceAssetDirectoryURLsKey NS_SWIFT_NAME(assetDirectoryURLs);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceAssetDirectoryURLsKey;
 
 /*!
  @constant SCNSceneSourceOverrideAssetURLsKey
@@ -95,7 +95,7 @@
  You can force SceneKit to only search for extern resources within the directories specified by the SCNSceneSourceAssetDirectoryURLsKey key.
  This can be useful to load a file and its resources from a specific bundle for instance.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceOverrideAssetURLsKey NS_SWIFT_NAME(overrideAssetURLs);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceOverrideAssetURLsKey;
 
 /*!
  @constant SCNSceneSourceStrictConformanceKey
@@ -104,7 +104,7 @@
 			 enable additional features and make the rendering as close as possible to the original intent. If you pass YES,
              SceneKit will instead only consider features which are part of the file format specification.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceStrictConformanceKey NS_SWIFT_NAME(strictConformance);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceStrictConformanceKey;
 
 /*!
  @constant SCNSceneSourceConvertUnitsToMetersKey
@@ -113,7 +113,7 @@
      For better physics simulation it is recommended to use 1 unit equals to 1 meter.
      This option has no effect if the asset is already compressed by Xcode (use the compression options instead).
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceConvertUnitsToMetersKey NS_SWIFT_NAME(convertUnitsToMeters) API_AVAILABLE(macosx(10.10)) API_UNAVAILABLE(ios, tvos, watchos);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceConvertUnitsToMetersKey API_AVAILABLE(macosx(10.10)) API_UNAVAILABLE(ios, tvos, watchos);
 
 /*!
  @constant SCNSceneSourceConvertToYUpKey
@@ -121,14 +121,14 @@
  @discussion Use this with a boolean value encapsulated in a NSNumber. The default value is NO.
  This option has no effect if the asset is already compressed by Xcode (use the compression options instead).
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceConvertToYUpKey NS_SWIFT_NAME(convertToYUp) API_AVAILABLE(macosx(10.10)) API_UNAVAILABLE(ios, tvos, watchos);
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceConvertToYUpKey API_AVAILABLE(macosx(10.10)) API_UNAVAILABLE(ios, tvos, watchos);
 
 /*!
  @constant SCNSceneSourceAnimationImportPolicyKey
  @abstract Pass one of the value below to specify what to do with loaded animations.
  @discussion See below for the description of each individual key. Defaults to SCNSceneSourceAnimationImportPolicyPlayRepeatedly. On 10.9 and before the behavior is SCNSceneSourceAnimationImportPolicyPlayUsingSceneTimeBase. For compatibility reason if the application was built on 10.9 or before the default behavior is SCNSceneSourceAnimationImportPolicyPlayUsingSceneTimeBase.
  */
-FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceAnimationImportPolicyKey NS_SWIFT_NAME(animationImportPolicy) API_AVAILABLE(macosx(10.10));
+FOUNDATION_EXTERN SCNSceneSourceLoadingOption const SCNSceneSourceAnimationImportPolicyKey API_AVAILABLE(macosx(10.10));
 
 /*!
  @constant SCNSceneSourceLoadingOptionPreserveOriginalTopology
@@ -150,7 +150,7 @@
 
 /* Values for SCNSceneSourceLoadingOptionAnimationImportPolicy */
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNSceneSourceAnimationImportPolicy NS_STRING_ENUM NS_SWIFT_NAME(SCNSceneSource.AnimationImportPolicy);
+typedef NSString * SCNSceneSourceAnimationImportPolicy NS_STRING_ENUM;
 #else
 typedef NSString * SCNSceneSourceAnimationImportPolicy;
 #endif
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNView.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNView.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNView.h	2016-07-23 00:54:59.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SCNView.h	2016-08-05 09:19:31.000000000 +0200
@@ -12,7 +12,7 @@
 NS_ASSUME_NONNULL_BEGIN
 
 #if defined(SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH) && SWIFT_SDK_OVERLAY2_SCENEKIT_EPOCH >= 3
-typedef NSString * SCNViewOption NS_STRING_ENUM NS_SWIFT_NAME(SCNView.Option);
+typedef NSString * SCNViewOption NS_STRING_ENUM;
 #else
 typedef NSString * SCNViewOption;
 #endif
@@ -21,19 +21,19 @@
  @constant SCNViewOptionPreferredRenderingAPI Specifies the preferred rendering API to be used by the renderer.
  @discussion Pass it as the key in the options dictionary given to initWithFrame:options:. The value is a NSNumber wrapping a SCNRenderingAPI. You can also select the preferred rendering API directly from the SCNView inspector in InterfaceBuilder.
  */
-FOUNDATION_EXTERN SCNViewOption const SCNPreferredRenderingAPIKey NS_SWIFT_NAME(preferredRenderingAPI) API_AVAILABLE(macosx(10.11), ios(9.0)) __WATCHOS_UNAVAILABLE;
+FOUNDATION_EXTERN SCNViewOption const SCNPreferredRenderingAPIKey API_AVAILABLE(macosx(10.11), ios(9.0)) __WATCHOS_UNAVAILABLE;
 
 /*!
  @constant SCNViewOptionPreferredDevice Specifies the preferred metal device to be used by the renderer.
  @discussion The value is directly a id <MTLDevice>.
  */
-FOUNDATION_EXTERN SCNViewOption const SCNPreferredDeviceKey NS_SWIFT_NAME(preferredDevice) API_AVAILABLE(macosx(10.11), ios(9.0));
+FOUNDATION_EXTERN SCNViewOption const SCNPreferredDeviceKey API_AVAILABLE(macosx(10.11), ios(9.0));
 
 /*!
  @constant SCNViewOptionPreferLowPowerDevice Specifies if the renderer should prefer a low power metal device.
  @discussion The value is a NSNumber wrapping a BOOL. Defaults to NO.
  */
-FOUNDATION_EXTERN SCNViewOption const SCNPreferLowPowerDeviceKey NS_SWIFT_NAME(preferLowPowerDevice) API_AVAILABLE(macosx(10.11), ios(9.0));
+FOUNDATION_EXTERN SCNViewOption const SCNPreferLowPowerDeviceKey API_AVAILABLE(macosx(10.11), ios(9.0));
 
 #define SCNViewOptionPreferredRenderingAPI SCNPreferredRenderingAPIKey
 #define SCNViewOptionPreferredDevice       SCNPreferredDeviceKey
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKitTypes.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKitTypes.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKitTypes.h	2016-07-23 01:15:30.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SceneKit.framework/Headers/SceneKitTypes.h	2016-08-05 08:59:47.000000000 +0200
@@ -180,7 +180,7 @@
 }
 
 NS_INLINE SCNVector4 SCNVector4FromFloat4(vector_float4 v) {
-    SCNVector4 vec = {v.x, v.y, v.z, v.z } ;
+    SCNVector4 vec = {v.x, v.y, v.z, v.w } ;
     return vec;
 }
 

```