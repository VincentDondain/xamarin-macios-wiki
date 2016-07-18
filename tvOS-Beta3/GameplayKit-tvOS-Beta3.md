#GameplayKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKDecisionTree.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKDecisionTree.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKDecisionTree.h	2016-06-26 08:25:18.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKDecisionTree.h	2016-07-09 03:59:16.000000000 +0200
@@ -95,7 +95,7 @@
  * @param answers The dictionary of attributes (keys) and their answers (values)
  * @return The attribute found by traversing the tree given the provided answers
  */
-- (id <NSObject>)findActionForAnswers:(NSDictionary <id <NSObject>, id <NSObject>>*)answers;
+- (nullable id <NSObject>)findActionForAnswers:(NSDictionary <id <NSObject>, id <NSObject>>*)answers;
 
 @end
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKEntity.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKEntity.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKEntity.h	2016-06-26 08:25:18.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKEntity.h	2016-07-09 03:59:16.000000000 +0200
@@ -63,14 +63,21 @@
  * Removes the component of the indicates class from this entity
  * @param componentClass the class of the component you want to remove
  */
+#if (defined(SWIFT_SDK_OVERLAY_GAMEPLAYKIT_EPOCH) && SWIFT_SDK_OVERLAY_GAMEPLAYKIT_EPOCH >= 1)
+- (void)removeComponentForClass:(Class)componentClass NS_REFINED_FOR_SWIFT;
+#else
 - (void)removeComponentForClass:(Class)componentClass;
+#endif
 
 /**
  * Gets the component of the indicated class.  Returns nil if entity does not have this component
  * @param componentClass the class of the component you want to get
  */
+#if (defined(SWIFT_SDK_OVERLAY_GAMEPLAYKIT_EPOCH) && SWIFT_SDK_OVERLAY_GAMEPLAYKIT_EPOCH >= 1)
+- (nullable GKComponent *)componentForClass:(Class)componentClass NS_REFINED_FOR_SWIFT;
+#else
  - (nullable GKComponent *)componentForClass:(Class)componentClass NS_SWIFT_UNAVAILABLE("Exposed in Swift as componentForClass<ComponentType: GKComponent>(componentClass: ComponentType.Type) -> ComponentType?");
-
+#endif
 
 @end
 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKObstacle.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKObstacle.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKObstacle.h	2016-06-26 08:25:18.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKObstacle.h	2016-07-09 03:59:16.000000000 +0200
@@ -56,8 +56,13 @@
  * @param points array of points in counter-clockwise order that are the vertices of a convex polygon
  * @param numPoints the number of points in the array
  */
+#if (defined(SWIFT_SDK_OVERLAY_GAMEPLAYKIT_EPOCH) && SWIFT_SDK_OVERLAY_GAMEPLAYKIT_EPOCH >= 1)
++ (instancetype)obstacleWithPoints:(vector_float2 *)points count:(size_t)numPoints NS_REFINED_FOR_SWIFT;
+- (instancetype)initWithPoints:(vector_float2 *)points count:(size_t)numPoints NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
+#else
 + (instancetype)obstacleWithPoints:(vector_float2 *)points count:(size_t)numPoints;
-- (instancetype)initWithPoints:(vector_float2 *)points count:(size_t)numPoints NS_DESIGNATED_INITIALIZER;;
+- (instancetype)initWithPoints:(vector_float2 *)points count:(size_t)numPoints NS_DESIGNATED_INITIALIZER;
+#endif
 
 /**
  * Returns the vertex at the indicated index
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKPath.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKPath.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKPath.h	2016-06-26 08:25:18.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKPath.h	2016-07-09 03:59:16.000000000 +0200
@@ -37,10 +37,17 @@
  * @param radius radius of the path to create
  * @param cyclical is the path a cycle that loops back on itself?
  */
+#if (defined(SWIFT_SDK_OVERLAY_GAMEPLAYKIT_EPOCH) && SWIFT_SDK_OVERLAY_GAMEPLAYKIT_EPOCH >= 1)
++ (instancetype)pathWithPoints:(vector_float2 *)points count:(size_t)count radius:(float)radius cyclical:(BOOL)cyclical NS_REFINED_FOR_SWIFT;
+- (instancetype)initWithPoints:(vector_float2 *)points count:(size_t)count radius:(float)radius cyclical:(BOOL)cyclical NS_REFINED_FOR_SWIFT;
++ (instancetype)pathWithFloat3Points:(vector_float3 *)points count:(size_t)count radius:(float)radius cyclical:(BOOL)cyclical NS_AVAILABLE(10_12, 10_0) NS_REFINED_FOR_SWIFT;
+- (instancetype)initWithFloat3Points:(vector_float3 *)points count:(size_t)count radius:(float)radius cyclical:(BOOL)cyclical NS_AVAILABLE(10_12, 10_0) NS_REFINED_FOR_SWIFT;
+#else
 + (instancetype)pathWithPoints:(vector_float2 *)points count:(size_t)count radius:(float)radius cyclical:(BOOL)cyclical;
 - (instancetype)initWithPoints:(vector_float2 *)points count:(size_t)count radius:(float)radius cyclical:(BOOL)cyclical;
 + (instancetype)pathWithFloat3Points:(vector_float3 *)points count:(size_t)count radius:(float)radius cyclical:(BOOL)cyclical NS_AVAILABLE(10_12, 10_0);
 - (instancetype)initWithFloat3Points:(vector_float3 *)points count:(size_t)count radius:(float)radius cyclical:(BOOL)cyclical NS_AVAILABLE(10_12, 10_0);
+#endif
 
 /**
  * Creates a path from an array of graph nodes (often a result of pathfinding)
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKVersion.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKVersion.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKVersion.h	2016-06-26 08:25:18.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/GameplayKit.framework/Headers/GKVersion.h	2016-07-09 03:59:16.000000000 +0200
@@ -1 +1 @@
-#define GK_VERSION 63000000
+#define GK_VERSION 64000000

```