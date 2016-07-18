#SpriteKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKNode.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKNode.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKNode.h	2016-06-26 08:40:20.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKNode.h	2016-07-10 08:24:21.000000000 +0200
@@ -169,7 +169,7 @@
 @property (nonatomic, nonnull, copy) NSDictionary<NSString *, SKAttributeValue *> *attributeValues;
 
 - (nullable SKAttributeValue*)valueForAttributeNamed:(nonnull NSString *)key;
-- (void)setValue:(SKAttributeValue*)value forAttributeNamed:(nonnull NSString *)key;
+- (void)setValue:(SKAttributeValue*)value forAttributeNamed:(nonnull NSString *)key NS_SWIFT_NAME(setValue(_:forAttribute:));
 
 /**
  Sets both the x & y scale
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVersion.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVersion.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVersion.h	2016-06-26 08:23:52.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVersion.h	2016-07-10 07:53:10.000000000 +0200
@@ -1 +1 @@
-#define SK_VERSION 18082000
+#define SK_VERSION 18088002
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKWarpGeometry.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKWarpGeometry.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKWarpGeometry.h	2016-06-26 08:28:50.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKWarpGeometry.h	2016-07-10 08:24:21.000000000 +0200
@@ -66,7 +66,18 @@
  [6]---[7]---[8]
  
  */
+#if (defined(SWIFT_SDK_OVERLAY_SPRITEKIT_EPOCH) && SWIFT_SDK_OVERLAY_SPRITEKIT_EPOCH >= 1)
++ (instancetype)gridWithColumns:(NSInteger)cols
+                           rows:(NSInteger)rows
+                sourcePositions:(nullable const vector_float2 *)sourcePositions
+                  destPositions:(nullable const vector_float2 *)destPositions NS_REFINED_FOR_SWIFT;
 
+/* init with the specified dimensions, source and dest positions. */
+- (instancetype)initWithColumns:(NSInteger)cols
+                           rows:(NSInteger)rows
+                sourcePositions:(nullable const vector_float2 *)sourcePositions
+                  destPositions:(nullable const vector_float2 *)destPositions NS_DESIGNATED_INITIALIZER NS_REFINED_FOR_SWIFT;
+#else
 + (instancetype)gridWithColumns:(NSInteger)cols
                            rows:(NSInteger)rows
                 sourcePositions:(nullable const vector_float2 *)sourcePositions
@@ -77,6 +88,7 @@
                            rows:(NSInteger)rows
                 sourcePositions:(nullable const vector_float2 *)sourcePositions
                   destPositions:(nullable const vector_float2 *)destPositions NS_DESIGNATED_INITIALIZER;
+#endif
 
 /* the number of columns in this grid */
 @property (nonatomic, readonly) NSInteger numberOfColumns;
@@ -92,9 +104,13 @@
 - (vector_float2)sourcePositionAtIndex:(NSInteger)index;
 - (vector_float2)destPositionAtIndex:(NSInteger)index;
 
+#if (defined(SWIFT_SDK_OVERLAY_SPRITEKIT_EPOCH) && SWIFT_SDK_OVERLAY_SPRITEKIT_EPOCH >= 1)
+- (instancetype)gridByReplacingSourcePositions:(const vector_float2 *)sourcePositions NS_REFINED_FOR_SWIFT;
+- (instancetype)gridByReplacingDestPositions:(const vector_float2 *)destPositions NS_REFINED_FOR_SWIFT;
+#else
 - (instancetype)gridByReplacingSourcePositions:(const vector_float2 *)sourcePositions;
 - (instancetype)gridByReplacingDestPositions:(const vector_float2 *)destPositions;
-
+#endif
 @end
 
 

```