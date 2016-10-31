#SpriteKit.framework

``` diff
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKEffectNode.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKEffectNode.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKEffectNode.h	2016-09-24 03:51:23.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKEffectNode.h	2016-10-23 09:41:23.000000000 +0200
@@ -58,6 +58,15 @@
 
 @property (nonatomic, retain, nullable) SKShader *shader;
 
+/**
+ Optional dictionary of SKAttributeValues
+ Attributes can be used with custom SKShaders.
+ */
+@property (nonatomic, nonnull, copy) NSDictionary<NSString *, SKAttributeValue *> *attributeValues;
+
+- (nullable SKAttributeValue*)valueForAttributeNamed:(nonnull NSString *)key;
+- (void)setValue:(SKAttributeValue*)value forAttributeNamed:(nonnull NSString *)key NS_SWIFT_NAME(setValue(_:forAttribute:));
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKEmitterNode.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKEmitterNode.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKEmitterNode.h	2016-09-24 03:34:49.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKEmitterNode.h	2016-10-23 10:15:44.000000000 +0200
@@ -202,7 +202,7 @@
 @property (nonatomic, retain, nullable) SKKeyframeSequence *particleAlphaSequence;
 
 /**
- The rate at which to modify the alpha for each particle. Defaults to 1.0.
+ Specifies an action executed by new particles.
  */
 @property (nonatomic, copy, nullable) SKAction *particleAction;
 
@@ -219,6 +219,14 @@
 
 @property (nonatomic, retain, nullable) SKShader *shader;
 
+/**
+ Optional dictionary of SKAttributeValues
+ Attributes can be used with custom SKShaders.
+ */
+@property (nonatomic, nonnull, copy) NSDictionary<NSString *, SKAttributeValue *> *attributeValues;
+
+- (nullable SKAttributeValue*)valueForAttributeNamed:(nonnull NSString *)key;
+- (void)setValue:(SKAttributeValue*)value forAttributeNamed:(nonnull NSString *)key NS_SWIFT_NAME(setValue(_:forAttribute:));
 
 /**
  The starting z-position for each particle. Defaults to 0.0.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKNode.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKNode.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKNode.h	2016-09-24 03:34:49.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKNode.h	2016-10-23 10:36:23.000000000 +0200
@@ -163,15 +163,6 @@
 @property (nonatomic, copy, nullable) NSArray<SKConstraint*> *constraints;
 
 /**
- Optional dictionary of SKAttributeValues
- Attributes can be used with custom SKShaders.
- */
-@property (nonatomic, nonnull, copy) NSDictionary<NSString *, SKAttributeValue *> *attributeValues;
-
-- (nullable SKAttributeValue*)valueForAttributeNamed:(nonnull NSString *)key;
-- (void)setValue:(SKAttributeValue*)value forAttributeNamed:(nonnull NSString *)key NS_SWIFT_NAME(setValue(_:forAttribute:));
-
-/**
  Sets both the x & y scale
  
  @param scale the uniform scale to set.
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKShapeNode.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKShapeNode.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKShapeNode.h	2016-05-04 00:21:22.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKShapeNode.h	2016-10-23 10:15:44.000000000 +0200
@@ -127,6 +127,15 @@
 /* An optional SKShader used for the Shape's Stroke. */
 @property (nonatomic, retain, nullable) SKShader *strokeShader NS_AVAILABLE(10_10, 8_0);
 
+/**
+ Optional dictionary of SKAttributeValues
+ Attributes can be used with custom SKShaders.
+ */
+@property (nonatomic, nonnull, copy) NSDictionary<NSString *, SKAttributeValue *> *attributeValues;
+
+- (nullable SKAttributeValue*)valueForAttributeNamed:(nonnull NSString *)key;
+- (void)setValue:(SKAttributeValue*)value forAttributeNamed:(nonnull NSString *)key NS_SWIFT_NAME(setValue(_:forAttribute:));
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKSpriteNode.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKSpriteNode.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKSpriteNode.h	2016-07-31 03:16:20.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKSpriteNode.h	2016-10-23 09:16:41.000000000 +0200
@@ -169,6 +169,15 @@
 
 @property (nonatomic, retain, nullable) SKShader *shader NS_AVAILABLE(10_10, 8_0);
 
+/**
+ Optional dictionary of SKAttributeValues
+ Attributes can be used with custom SKShaders.
+ */
+@property (nonatomic, nonnull, copy) NSDictionary<NSString *, SKAttributeValue *> *attributeValues;
+
+- (nullable SKAttributeValue*)valueForAttributeNamed:(nonnull NSString *)key;
+- (void)setValue:(SKAttributeValue*)value forAttributeNamed:(nonnull NSString *)key NS_SWIFT_NAME(setValue(_:forAttribute:));
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTileMapNode.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTileMapNode.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTileMapNode.h	2016-09-24 03:34:49.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTileMapNode.h	2016-10-23 10:36:23.000000000 +0200
@@ -127,6 +127,15 @@
 @property (nonatomic, retain, nullable) SKShader *shader;
 
 /**
+ Optional dictionary of SKAttributeValues
+ Attributes can be used with custom SKShaders.
+ */
+@property (nonatomic, nonnull, copy) NSDictionary<NSString *, SKAttributeValue *> *attributeValues;
+
+- (nullable SKAttributeValue*)valueForAttributeNamed:(nonnull NSString *)key;
+- (void)setValue:(SKAttributeValue*)value forAttributeNamed:(nonnull NSString *)key NS_SWIFT_NAME(setValue(_:forAttribute:));
+
+/**
  Bitmask to indicate being lit by a set of lights using overlapping lighting categories.
 
  A light whose category is set to a value that masks to non-zero using this mask will
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVersion.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVersion.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVersion.h	2016-09-24 03:51:23.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVersion.h	2016-10-23 09:41:24.000000000 +0200
@@ -1 +1 @@
-#define SK_VERSION 18095000
+#define SK_VERSION 18108000
diff -ruN /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVideoNode.h /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVideoNode.h
--- /Applications/Xcode81.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVideoNode.h	2016-09-24 03:51:23.000000000 +0200
+++ /Applications/Xcode82-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVideoNode.h	2016-10-23 09:41:23.000000000 +0200
@@ -9,7 +9,6 @@
  
  */
 
-#if __has_include(<AVFoundation/AVPlayer.h>)
 @class AVPlayer;
 
 
@@ -74,5 +73,3 @@
 @end
 
 NS_ASSUME_NONNULL_END
-
-#endif

```