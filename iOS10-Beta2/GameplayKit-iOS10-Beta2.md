#GameplayKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKAgent.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKAgent.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKAgent.h	2016-05-18 05:10:29.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKAgent.h	2016-06-26 08:25:18.000000000 +0200
@@ -143,6 +143,11 @@
  */
 @property (nonatomic, readonly) vector_float3 velocity;
 
+/**
+ * Should this vehicle operate in a right-handed coordinate system? NO means it will be left-handed
+ */
+@property (nonatomic) BOOL rightHanded;
+
 
 /**
  * The 3x3 rotation matrix that defines the orientation of this agent in 3D space
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGraphNode.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGraphNode.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGraphNode.h	2016-05-25 04:45:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKGraphNode.h	2016-06-26 09:33:12.000000000 +0200
@@ -78,7 +78,7 @@
 /**
  * GKGraphNode coupled with a 3D position
  */
-GK_BASE_AVAILABILITY @interface GKGraphNode3D : GKGraphNode
+GK_BASE_AVAILABILITY_2 @interface GKGraphNode3D : GKGraphNode
 
 @property (nonatomic) vector_float3 position;
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKNoise.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKNoise.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKNoise.h	2016-05-18 05:10:29.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKNoise.h	2016-06-26 08:25:18.000000000 +0200
@@ -84,6 +84,15 @@
 + (instancetype)noiseWithComponentNoises:(NSArray<GKNoise *> *)noises selectionNoise:(GKNoise *)selectionNoise componentBoundaries:(NSArray<NSNumber *> *)componentBoundaries boundaryBlendDistances:(NSArray<NSNumber *> *)blendDistances;
 
 /**
+ * The noise value at the specified sample index of the 2D plane.
+ *
+ * @param position Sample index of the extracted 2D plane at which to query the value
+ *
+ * @return The noise map value at the specified position.
+ */
+- (float)valueAtPosition:(vector_float2)position;
+
+/**
  * Takes the absoltue value of all noise positions.
  */
 - (void)applyAbsoluteValue;
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKOctree.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKOctree.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKOctree.h	2016-05-25 04:45:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKOctree.h	2016-06-26 09:33:12.000000000 +0200
@@ -8,6 +8,8 @@
 #import <GameplayKit/GameplayKitBase.h>
 #import <GameplayKit/GKPrimitives.h>
 
+NS_ASSUME_NONNULL_BEGIN
+
 /**
  * The individual node(s) that make up a GKOctree.
  * Used as a hint for faster removal via [GKOctree removeData:WithNode:]
@@ -93,3 +95,5 @@
 -(BOOL)removeElement:(ElementType)element withNode:(GKOctreeNode*)node;
 
 @end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKQuadtree.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKQuadtree.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKQuadtree.h	2016-05-25 04:45:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKQuadtree.h	2016-06-26 09:33:12.000000000 +0200
@@ -8,6 +8,8 @@
 #import <GameplayKit/GameplayKitBase.h>
 #import <GameplayKit/GKPrimitives.h>
 
+NS_ASSUME_NONNULL_BEGIN
+
 /**
  * The individual node(s) that make up a GKQuadtree.
  * Used as a hint for faster removal via [GKQuadtree removeData:WithNode:]
@@ -93,3 +95,5 @@
 -(BOOL)removeElement:(ElementType)data withNode:(GKQuadtreeNode*)node;
 
 @end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKRTree.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKRTree.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKRTree.h	2016-05-25 04:45:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKRTree.h	2016-06-26 09:33:12.000000000 +0200
@@ -8,6 +8,8 @@
 #import <GameplayKit/GameplayKitBase.h>
 #import <GameplayKit/GKPrimitives.h>
 
+NS_ASSUME_NONNULL_BEGIN
+
 /** Used to adjust the way in which RTree nodes are split when they grow too large.
  
  @enum GKRTreeSplitStrategyHalve Specifies that nodes should be split in half based on insert order.
@@ -74,3 +76,5 @@
 -(NSArray<ElementType>*)elementsInBoundingRectMin:(vector_float2)rectMin rectMax:(vector_float2)rectMax;
 
 @end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKScene.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKScene.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKScene.h	2016-05-25 04:45:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKScene.h	2016-06-26 09:33:12.000000000 +0200
@@ -45,7 +45,7 @@
 /**
  The navigational graphs of this scene.
  */
-@property (nonatomic, readonly) NSArray<GKGraph *> *graphs;
+@property (nonatomic, readonly) NSDictionary<NSString*, GKGraph *> *graphs;
 
 /**
  Adds an entity to the scene's list of entities.
@@ -66,14 +66,14 @@
  
  @param graph the graph to add.
  */
-- (void)addGraph:(GKGraph *)graph;
+- (void)addGraph:(GKGraph *)graph name:(NSString*)name;
 
 /**
  Removes a graph from the scene's list of graphs.
  
- @param graph the graph to remove.
+ @param name the name of the corresponding graph as added via addGraph:
  */
-- (void)removeGraph:(GKGraph *)graph;
+- (void)removeGraph:(NSString*)name;
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKVersion.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKVersion.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKVersion.h	2016-05-25 04:45:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKVersion.h	2016-06-26 09:33:12.000000000 +0200
@@ -1 +1 @@
-#define GK_VERSION 60000000
+#define GK_VERSION 63000000

```