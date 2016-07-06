#SpriteKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SK3DNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SK3DNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SK3DNode.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SK3DNode.h	2016-05-28 06:30:01.000000000 +0200
@@ -5,7 +5,7 @@
  3D Nodes are used to display 3D content in a SKScene.
  
  
- @copyright 2011 Apple, Inc. All rights reserve.
+ @copyright 2011 Apple, Inc. All rights reserved.
  
  */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKAction.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKAction.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKAction.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKAction.h	2016-05-28 06:41:02.000000000 +0200
@@ -149,6 +149,11 @@
 + (SKAction *)scaleXTo:(CGFloat)scale duration:(NSTimeInterval)sec;
 + (SKAction *)scaleYTo:(CGFloat)scale duration:(NSTimeInterval)sec;
 
+/**
+ Adjust the sprite's xScale & yScale to achieve the desired size (in parent's coordinate space)
+ */
++ (SKAction *)scaleToSize:(CGSize)size duration:(NSTimeInterval)sec NS_AVAILABLE(10_12, 10_0);
+
 /** Creates an action that runs a collection of actions sequentially
  @param sequence An array of SKAction objects
  
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKAttribute.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKAttribute.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKAttribute.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKAttribute.h	2016-05-28 06:30:01.000000000 +0200
@@ -0,0 +1,61 @@
+/**
+ @header
+ 
+ SKAttributes can be used to provide a per-node value to be
+ used with SKShaders.
+ 
+ @copyright 2015 Apple, Inc. All rights reserved.
+ 
+ */
+
+#import <SpriteKit/SpriteKitBase.h>
+#import <simd/simd.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+typedef NS_ENUM(NSInteger, SKAttributeType) {
+    SKAttributeTypeNone                 =    0,
+    
+    SKAttributeTypeFloat                =    1,
+    SKAttributeTypeVectorFloat2         =    2,
+    SKAttributeTypeVectorFloat3         =    3,
+    SKAttributeTypeVectorFloat4         =    4,
+    
+    SKAttributeTypeHalfFloat            =    5,
+    SKAttributeTypeVectorHalfFloat2     =    6,
+    SKAttributeTypeVectorHalfFloat3     =    7,
+    SKAttributeTypeVectorHalfFloat4     =    8,
+    
+} NS_ENUM_AVAILABLE(10_11, 9_0);
+
+NS_CLASS_AVAILABLE(10_11, 9_0)
+SK_EXPORT @interface SKAttribute : NSObject <NSCoding>
+
++ (instancetype)attributeWithName:(NSString*)name type:(SKAttributeType)type;
+- (instancetype)initWithName:(NSString*)name type:(SKAttributeType)type NS_DESIGNATED_INITIALIZER;
+
+@property (readonly, nonatomic) NSString *name;
+@property (readonly, nonatomic) SKAttributeType type;
+
+@end
+
+
+
+NS_CLASS_AVAILABLE(10_11, 9_0)
+SK_EXPORT @interface SKAttributeValue : NSObject <NSCoding>
+
++ (instancetype)valueWithFloat:(float)value;
++ (instancetype)valueWithVectorFloat2:(vector_float2)value;
++ (instancetype)valueWithVectorFloat3:(vector_float3)value;
++ (instancetype)valueWithVectorFloat4:(vector_float4)value;
+
+- (instancetype)init NS_DESIGNATED_INITIALIZER;
+
+@property (nonatomic) float floatValue;
+@property (nonatomic) vector_float2 vectorFloat2Value;
+@property (nonatomic) vector_float3 vectorFloat3Value;
+@property (nonatomic) vector_float4 vectorFloat4Value;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKAudioNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKAudioNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKAudioNode.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKAudioNode.h	2016-05-28 06:30:01.000000000 +0200
@@ -3,12 +3,14 @@
  
  Node that holds an AVAudioEngine sound graph, including from a single sound source or URL.
  
- @copyright 2015 Apple, Inc. All rights reserve.
+ @copyright 2015 Apple, Inc. All rights reserved.
  
  */
 
 #import <SpriteKit/SpriteKit.h>
 
+#if __has_include(<AVFoundation/AVAudioEngine.h>)
+
 @class AVAudioNode;
 
 NS_ASSUME_NONNULL_BEGIN
@@ -85,3 +87,5 @@
 @end
 
 NS_ASSUME_NONNULL_END
+
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKCameraNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKCameraNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKCameraNode.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKCameraNode.h	2016-05-28 06:30:01.000000000 +0200
@@ -3,7 +3,7 @@
  
  Node that controls camera movement, zoom and rotation.
  
- @copyright 2015 Apple, Inc. All rights reserve.
+ @copyright 2015 Apple, Inc. All rights reserved.
  
  */
 
@@ -45,4 +45,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKCropNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKCropNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKCropNode.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKCropNode.h	2016-05-28 06:30:01.000000000 +0200
@@ -5,7 +5,7 @@
  Node that can crop its children's contents with a mask
  
  
- @copyright 2011 Apple, Inc. All rights reserve.
+ @copyright 2011 Apple, Inc. All rights reserved.
  
  */
 
@@ -28,4 +28,4 @@
 
 @end
 
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKEffectNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKEffectNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKEffectNode.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKEffectNode.h	2016-05-28 06:30:01.000000000 +0200
@@ -5,26 +5,33 @@
  Node that can apply an effect to its children
  
  
- @copyright 2011 Apple, Inc. All rights reserve.
+ @copyright 2011 Apple, Inc. All rights reserved.
  
  */
 
+#if __has_include(<CoreImage/CIFilter.h>)
+@class CIFilter;
+#endif
+
 #import <SpriteKit/SKNode.h>
 #import <SpriteKit/SpriteKitBase.h>
 #import <SpriteKit/SKShader.h>
+#import <SpriteKit/SKWarpGeometry.h>
 
 NS_ASSUME_NONNULL_BEGIN
 /**
  A SpriteKit node that applies frame buffer effects to the rendered results of its child nodes. This is done continuously on live content and is not a simple snapshot of the rendered result at one instant of time.
  */
-SK_EXPORT @interface SKEffectNode : SKNode
+SK_EXPORT @interface SKEffectNode : SKNode <SKWarpable>
 
+#if __has_include(<CoreImage/CIFilter.h>)
 /**
  A CIFilter to be used as an effect
  
  Any CIFilter that requires only a single "inputImage" and produces an "outputImage" is allowed. The filter is applied to all children of the SKEffectNode. If the filter is nil, the children of this node is flattened before being drawn as long as the SKEffectNode is enabled.
  */
 @property (nonatomic, retain, nullable) CIFilter *filter;
+#endif
 
 /* Controls whether the filter's "inputCenter" (if it exists) should automatically be set to the center of the effect area. Defaults to YES. */
 @property (nonatomic) BOOL shouldCenterFilter;
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKEmitterNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKEmitterNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKEmitterNode.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKEmitterNode.h	2016-05-28 06:40:54.000000000 +0200
@@ -5,7 +5,7 @@
  Particle Emitter Node
  
  
- @copyright 2011 Apple, Inc. All rights reserve.
+ @copyright 2011 Apple, Inc. All rights reserved.
  
  */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKNode.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKNode.h	2016-05-27 06:51:24.000000000 +0200
@@ -5,7 +5,7 @@
  Nodes are the base scene graph nodes used in the SpriteKit scene graph.
  
  
- @copyright 2011 Apple, Inc. All rights reserve.
+ @copyright 2011 Apple, Inc. All rights reserved.
  
  */
 
@@ -13,7 +13,9 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
-@class SKView, SKAction, SKScene, SKTexture, SKPhysicsBody, SKFieldNode, SKReachConstraints, SKConstraint, GKPolygonObstacle;
+@class SKAction, SKScene, SKTexture, SKPhysicsBody, SKFieldNode;
+@class SKReachConstraints, SKConstraint, SKAttributeValue, SKWarpGeometry;
+@protocol UIFocusItem;
 
 /**
  Blend modes that the SKNode uses to compose with the framebuffer to produce blended colors.
@@ -34,7 +36,11 @@
  All nodes have one and exactly one parent unless they are the root node of a graph tree. Leaf nodes have no children and contain some sort of sharable data that guarantee the DAG condition.
  */
 #if TARGET_OS_IPHONE
-SK_EXPORT @interface SKNode : UIResponder <NSCopying, NSCoding>
+#if SKVIEW_AVAILABLE
+SK_EXPORT @interface SKNode : UIResponder <NSCopying, NSCoding, UIFocusItem>
+#else
+SK_EXPORT @interface SKNode : NSObject <NSCopying, NSCoding>
+#endif
 #else
 SK_EXPORT @interface SKNode : NSResponder <NSCopying, NSCoding>
 #endif
@@ -157,6 +163,15 @@
 @property (nonatomic, copy, nullable) NSArray<SKConstraint*> *constraints;
 
 /**
+ Optional dictionary of SKAttributeValues
+ Attributes can be used with custom SKShaders.
+ */
+@property (nonatomic, nonnull, copy) NSDictionary<NSString *, SKAttributeValue *> *attributeValues;
+
+- (nullable SKAttributeValue*)valueForAttributeNamed:(nonnull NSString *)key;
+- (void)setValue:(SKAttributeValue*)value forAttributeNamed:(nonnull NSString *)key;
+
+/**
  Sets both the x & y scale
  
  @param scale the uniform scale to set.
@@ -178,7 +193,7 @@
 - (void)removeAllChildren;
 
 - (void)removeFromParent;
-- (void)moveToParent:(SKNode *)parent;
+- (void)moveToParent:(SKNode *)parent NS_AVAILABLE(10_11, 9_0);
 
 - (nullable SKNode *)childNodeWithName:(NSString *)name;
 
@@ -232,15 +247,6 @@
 
 - (BOOL)isEqualToNode:(SKNode *)node;
 
-/* Returns an array of GKPolygonObstacles from a group of SKSpriteNode's textures in scene space. For use with GPObstacleGraph in GameplayKit */
-+ (NSArray<GKPolygonObstacle*> *)obstaclesFromSpriteTextures:(NSArray<SKNode*>*)sprites accuracy:(float)accuracy;
-
-/* Returns an array of GKPolygonObstacles from a group of SKNode's transformed bounds in scene space. For use with GPObstacleGraph in GameplayKit */
-+ (NSArray<GKPolygonObstacle*> *)obstaclesFromNodeBounds:(NSArray<SKNode*>*)nodes;
-
-/* Returns an array of GKPolygonObstacles from a group of SKNode's physics bodies in scene space. For use with GPObstacleGraph in GameplayKit */
-+ (NSArray<GKPolygonObstacle*> *)obstaclesFromNodePhysicsBodies:(NSArray<SKNode*>*)nodes;
-
 @end
 
 
@@ -248,17 +254,17 @@
  Provided for easy transformation of UITouches coordinates to SKNode coordinates should you choose to handle touch events natively.
  */
 #if TARGET_OS_IPHONE
+#if __has_include(<UIKit/UITouch.h>)
 //Allow conversion of UITouch coordinates to scene-space
 @interface UITouch (SKNodeTouches)
 - (CGPoint)locationInNode:(SKNode *)node;
 - (CGPoint)previousLocationInNode:(SKNode *)node;
 @end
+#endif
 #else
 @interface NSEvent (SKNodeEvent)
 - (CGPoint)locationInNode:(SKNode *)node;
 @end
 #endif
 
-
-
-NS_ASSUME_NONNULL_END
\ No newline at end of file
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKScene.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKScene.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKScene.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKScene.h	2016-05-27 06:51:24.000000000 +0200
@@ -9,7 +9,11 @@
 #import <SpriteKit/SKEffectNode.h>
 #import <SpriteKit/SpriteKitBase.h>
 
-@class SKView, SKPhysicsWorld, AVAudioEngine;
+#if SKVIEW_AVAILABLE
+@class SKView;
+#endif
+
+@class SKPhysicsWorld, AVAudioEngine;
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -38,11 +42,8 @@
 SK_EXPORT @interface SKScene : SKEffectNode
 
 /**
- Called once when the scene is created, do your one-time setup here.
- 
  A scene is infinitely large, but it has a viewport that is the frame through which you present the content of the scene.
  The passed in size defines the size of this viewport that you use to present the scene.
- To display different portions of your scene, move the contents relative to the viewport. One way to do that is to create a SKNode to function as a viewport transformation. That node should have all visible conents parented under it.
  
  @param size a size in points that signifies the viewport into the scene that defines your framing of the scene.
  */
@@ -50,6 +51,10 @@
 
 + (instancetype)sceneWithSize:(CGSize)size;
 
+/* This is called once after the scene has been initialized or decoded,
+ this is the recommended place to perform one-time setup */
+- (void)sceneDidLoad NS_AVAILABLE(10_12, 10_0);
+
 @property (nonatomic) CGSize size;
 
 /**
@@ -71,14 +76,16 @@
 /**
  The audio engine that the listener and the scene's audio nodes use to process their sound through.
  */
+#if __has_include(<AVFoundation/AVAudioEngine.h>)
 @property (nonatomic, retain, readonly) AVAudioEngine *audioEngine NS_AVAILABLE(10_11, 9_0);
+#endif
 
 /**
  Background color, defaults to gray
  */
 @property (nonatomic, retain) SKColor *backgroundColor;
 
-@property (nonatomic, assign, nullable) id<SKSceneDelegate> delegate NS_AVAILABLE(10_10, 8_0);
+@property (nonatomic, weak, nullable) id<SKSceneDelegate> delegate NS_AVAILABLE(10_10, 8_0);
 
 /**
  Used to choose the origin of the scene's coordinate system
@@ -90,14 +97,17 @@
  */
 @property (nonatomic, readonly) SKPhysicsWorld *physicsWorld;
 
-- (CGPoint)convertPointFromView:(CGPoint)point;
-- (CGPoint)convertPointToView:(CGPoint)point;
 
+#if SKVIEW_AVAILABLE
 /**
  The SKView this scene is currently presented in, or nil if it is not being presented.
  */
 @property (nonatomic, weak, readonly, nullable) SKView *view;
 
+- (CGPoint)convertPointFromView:(CGPoint)point;
+- (CGPoint)convertPointToView:(CGPoint)point;
+#endif
+
 /**
  Override this to perform per-frame game logic. Called exactly once per frame before any actions are evaluated and any physics are simulated.
  
@@ -127,8 +137,11 @@
  */
 - (void)didFinishUpdate NS_AVAILABLE(10_10, 8_0);
 
+#if SKVIEW_AVAILABLE
 - (void)didMoveToView:(SKView *)view;
 - (void)willMoveFromView:(SKView *)view;
+#endif
+
 - (void)didChangeSize:(CGSize)oldSize;
 
 @end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKShader.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKShader.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKShader.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKShader.h	2016-05-28 06:30:01.000000000 +0200
@@ -8,7 +8,7 @@
  */
 
 #import <SpriteKit/SpriteKitBase.h>
-#import <SpriteKit/SKUniform.h>
+@class SKUniform, SKAttribute;
 
 NS_ASSUME_NONNULL_BEGIN
 
@@ -87,6 +87,8 @@
 - (nullable SKUniform *)uniformNamed:(NSString *)name;
 - (void)removeUniformNamed:(NSString *)name;
 
+@property (nonatomic, copy, nonnull) NSArray<SKAttribute*> *attributes NS_AVAILABLE(10_11, 9_0);
+
 @end
 
 NS_ASSUME_NONNULL_END
\ No newline at end of file
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKSpriteNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKSpriteNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKSpriteNode.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKSpriteNode.h	2016-05-28 06:41:02.000000000 +0200
@@ -16,6 +16,7 @@
 
 #import <SpriteKit/SKNode.h>
 #import <SpriteKit/SKShader.h>
+#import <SpriteKit/SKWarpGeometry.h>
 #import <SpriteKit/SpriteKitBase.h>
 
 NS_ASSUME_NONNULL_BEGIN
@@ -29,7 +30,7 @@
  See <a href="http://en.wikipedia.org/wiki/Sprite_(computer_graphics)">wiki</a> for a definition of a Sprite.
  
  */
-SK_EXPORT @interface SKSpriteNode : SKNode
+SK_EXPORT @interface SKSpriteNode : SKNode <SKWarpable>
 
 /**
  Create a sprite with an SKTexture and the specified size.
@@ -161,6 +162,11 @@
  */
 @property (nonatomic) CGSize size;
 
+/**
+ Adjust the sprite's xScale & yScale to achieve the desired size (in parent's coordinate space)
+ */
+- (void)scaleToSize:(CGSize)size NS_AVAILABLE(10_12, 10_0);
+
 @property (nonatomic, retain, nullable) SKShader *shader NS_AVAILABLE(10_10, 8_0);
 
 @end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTexture.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTexture.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTexture.h	2015-10-24 03:11:36.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTexture.h	2016-05-28 06:41:02.000000000 +0200
@@ -8,7 +8,9 @@
 #import <Foundation/Foundation.h>
 #import <SpriteKit/SpriteKitBase.h>
 
+#if __has_include(<CoreImage/CIFilter.h>)
 @class CIFilter;
+#endif
 
 typedef NS_ENUM(NSInteger, SKTextureFilteringMode) {
     SKTextureFilteringNearest,
@@ -91,12 +93,15 @@
  */
 + (instancetype)textureWithData:(NSData *)pixelData size:(CGSize)size rowLength:(unsigned int)rowLength alignment:(unsigned int)alignment;
 
+
+#if __has_include(<CoreImage/CIFilter.h>)
 /**
  Create new texture by applying a CIFilter to an existing one. Any CIFilter that requires only a single "inputImage" and produces an "outputImage" is allowed.
  
  @param filter the CI filter to apply in the copy.
  */
 - (instancetype)textureByApplyingCIFilter:(CIFilter *)filter;
+#endif
 
 
 /**
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTileDefinition.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTileDefinition.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTileDefinition.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTileDefinition.h	2016-05-27 03:54:53.000000000 +0200
@@ -0,0 +1,155 @@
+//
+//  SKTileDefinition.h
+//
+//  Copyright © 2015 Apple Inc. All rights reserved.
+//
+
+#import <SpriteKit/SKNode.h>
+#import <SpriteKit/SpriteKitBase.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/**
+ Adjust the rotation of the tile definition image, in 90 degree increments.
+ */
+typedef NS_ENUM(NSUInteger, SKTileDefinitionRotation) {
+    SKTileDefinitionRotation0 = 0,
+    SKTileDefinitionRotation90,
+    SKTileDefinitionRotation180,
+    SKTileDefinitionRotation270
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
+/**
+ A tile definition contains the information needed to represent a single type of tile within a tile map.
+ */
+SK_EXPORT NS_AVAILABLE(10_12, 10_0) @interface SKTileDefinition : NSObject <NSCopying, NSCoding>
+
+/**
+ Create a tile definition with an SKTexture, and set its size to the SKTexture's width/height.
+ @param texture the texture to reference for size and content
+ */
++ (instancetype)tileDefinitionWithTexture:(SKTexture *)texture;
+
+/**
+ Create a tile definition with an SKTexture and the specified size.
+ @param texture the texture to reference for content
+ @param size the size of the tile in points
+ */
++ (instancetype)tileDefinitionWithTexture:(SKTexture *)texture size:(CGSize)size;
+
+/**
+ Create a tile definition with an SKTexture and the specified size.
+ @param texture the texture to reference for content
+ @param normalTexture the normal texture to use for generating normals for lighting
+ @param size the size of the tile in points
+ */
++ (instancetype)tileDefinitionWithTexture:(SKTexture *)texture normalTexture:(SKTexture *)normalTexture size:(CGSize)size;
+
+/**
+ Create an animated tile definition with an array of SKTextures, the specified size, and the length of time each texture should be displayed for in the animation.
+ @param textures the textures to reference for animated content
+ @param size the size of the tile in points
+ @param timePerFrame the duration, in seconds, that each texture in the textures array is displayed before switching to the next texture in the sequence
+ */
++ (instancetype)tileDefinitionWithTextures:(NSArray<SKTexture *> *)textures size:(CGSize)size timePerFrame:(CGFloat)timePerFrame;
+
+/**
+ Create an animated tile definition with an array of SKTextures, the specified size, and the length of time each texture should be displayed for in the animation.
+ @param textures the textures to reference for animated content
+ @param normalTextures the normal textures to use for generating normals for lighting
+ @param size the size of the tile in points
+ @param timePerFrame the duration, in seconds, that each texture in the textures array is displayed before switching to the next texture in the sequence
+ */
++ (instancetype)tileDefinitionWithTextures:(NSArray<SKTexture *> *)textures normalTextures:(NSArray<SKTexture *> *)normalTextures size:(CGSize)size timePerFrame:(CGFloat)timePerFrame;
+
+/**
+ Initilize a tile definition with an SKTexture, and set its size to the SKTexture's width/height.
+ @param texture the texture to reference for size and content
+ */
+- (instancetype)initWithTexture:(SKTexture *)texture;
+
+/**
+ Initilize a tile definition with an SKTexture and the specified size.
+ @param texture the texture to reference for content
+ @param size the size of the tile in points
+ */
+- (instancetype)initWithTexture:(SKTexture *)texture size:(CGSize)size;
+
+/**
+ Initilize a tile definition with an SKTexture and the specified size.
+ @param texture the texture to reference for content
+ @param normalTexture the normal texture to use for generating normals for lighting
+ @param size the size of the tile in points
+ */
+- (instancetype)initWithTexture:(SKTexture *)texture normalTexture:(SKTexture *)normalTexture size:(CGSize)size;
+
+/**
+ Initilize an animated tile definition with an array of SKTextures, the specified size, and the length of time each texture should be displayed for in the animation.
+ @param textures the textures to reference for animated content
+ @param size the size of the tile in points
+ @param timePerFrame the duration, in seconds, that each texture in the textures array is displayed before switching to the next texture in the sequence
+ */
+- (instancetype)initWithTextures:(NSArray<SKTexture *>*)textures size:(CGSize)size timePerFrame:(CGFloat)timePerFrame;
+
+/**
+ Initilize an animated tile definition with an array of SKTextures, the specified size, and the length of time each texture should be displayed for in the animation.
+ @param textures the textures to reference for animated content
+ @param normalTextures the normal textures to use for generating normals for lighting
+ @param size the size of the tile in points
+ @param timePerFrame the duration, in seconds, that each texture in the textures array is displayed before switching to the next texture in the sequence
+ */
+- (instancetype)initWithTextures:(NSArray<SKTexture *>*)textures normalTextures:(NSArray<SKTexture *> *)normalTextures size:(CGSize)size timePerFrame:(CGFloat)timePerFrame;
+
+/**
+ The textures used to draw the tile. Non-animated tiles use only one texture. When more than one texture is present, the tile will swap through them in sequence, showing each for the duration specified in the timePerFrame property. After displaying the last texture in the array, the sequence is repeated from the first texture.
+ */
+@property (nonatomic, copy) NSArray<SKTexture *> *textures;
+
+/**
+ The textures to use for generating normals that lights use to light this tile. These will only be used if the tile is lit by at least one light. Each normal texture corresponds to a texture in the textures property.
+ */
+@property (nonatomic, copy) NSArray<SKTexture *> *normalTextures;
+
+/**
+ An optional dictionary that can be used to store your own data for each tile definition. Defaults to nil.
+ */
+@property (nonatomic, retain, nullable) NSMutableDictionary *userData;
+
+/**
+ Client-assignable name for the tile definition. Defaults to nil.
+ */
+@property (nonatomic, copy, nullable) NSString *name;
+
+/**
+ The size of the tile in points.
+ */
+@property (nonatomic) CGSize size;
+
+/**
+ The duration, in seconds, that each texture in the textures array is displayed before switching to the next texture in the sequence. Only used when there is more than one texture available.
+ */
+@property (nonatomic) CGFloat timePerFrame;
+
+/**
+ This value is used to determine how likely this tile definition is to be chosen for placement when a SKTileGroupRule has mulitple tile definitions assigned to it. A higher value relative to the other definitions assigned to the rule make it more likely for this definition to be selected; lower values make it less likely. Defaults to 1. When set to 0, the definition will never be chosen as long as there is at least one other definition with a placementWeight above 0.
+ */
+@property (nonatomic) NSUInteger placementWeight;
+
+/**
+ The rotation of the tile definition's images can be set in 90 degree increments. Defaults to SKTileDefinitionRotation0.
+ */
+@property (nonatomic) SKTileDefinitionRotation rotation;
+
+/**
+ When set to YES, the tile definition's images will be flipped vertically (i.e., the top of the image becomes the bottom). Defaults to NO.
+ */
+@property (nonatomic) BOOL flipVertically;
+
+/**
+ When set to YES, the tile definition's images will be flipped horizontally (i.e., the left of the image becomes the right). Defaults to NO.
+ */
+@property (nonatomic) BOOL flipHorizontally;
+
+@end
+
+NS_ASSUME_NONNULL_END
\ No newline at end of file
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTileMapNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTileMapNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTileMapNode.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTileMapNode.h	2016-05-28 06:41:02.000000000 +0200
@@ -0,0 +1,199 @@
+//
+//  SKTileMapNode.h
+//
+//  Copyright © 2015 Apple Inc. All rights reserved.
+//
+
+#import <SpriteKit/SKNode.h>
+#import <SpriteKit/SKShader.h>
+#import <SpriteKit/SpriteKitBase.h>
+
+#import <SpriteKit/SKTileSet.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/**
+ A SpriteKit node used to render a 2D array of textured sprites. Uses SKTileSet to determine what textures it can use to render. Separate tile map nodes can be layered on top of one another to achieve various effects, such as parallax scrolling.
+ */
+SK_EXPORT NS_AVAILABLE(10_12, 10_0) @interface SKTileMapNode : SKNode <NSCopying, NSCoding>
+
+/**
+ Create a tile map node with the specified tile set and dimensions. The tiles of the map will be empty, equivalent to the nil tile definition/group.
+ @param tileSet the tile set that is used to render the tiles
+ @param columns the number of columns in the map that can hold tiles
+ @param rows the number of rows in the map that can hold tiles
+ @param tileSize the size of each tile in points
+ */
++ (instancetype)tileMapNodeWithTileSet:(SKTileSet *)tileSet columns:(NSUInteger)columns rows:(NSUInteger)rows tileSize:(CGSize)tileSize;
+
+/**
+ Create a tile map node with the specified tile set and dimensions, and fill it with the specified tile group.
+ @param tileSet the tile set that is used to render the tiles
+ @param columns the number of columns in the map that can hold tiles
+ @param rows the number of rows in the map that can hold tiles
+ @param tileSize the size of each tile in points
+ @param tileGroup the tile group we wish to fill the tile map with
+ */
++ (instancetype)tileMapNodeWithTileSet:(SKTileSet *)tileSet columns:(NSUInteger)columns rows:(NSUInteger)rows tileSize:(CGSize)tileSize fillWithTileGroup:(SKTileGroup *)tileGroup;
+
+/**
+ Create a tile map node with the specified tile set and dimensions, and fill it with a specific layout of tile groups that belong to the provided tile set. The tileGroupLayout array should match the dimensions of the tile map (i.e., the number of elements should be equal to columns * rows). Index 0 of the array maps to column 0, row 0 of the tile map. Index 1 is column 1, row 0, and so on, wrapping around to the next row once the index passes the number of columns in the tile map. If the array has fewer elements than the number of tiles in the map, the remaining tiles are initialized with the nil tile group. If the array has more elements than the number of tiles in the map, the extra tile groups are ignored.
+ @param tileSet the tile set that is used to render the tiles
+ @param columns the number of columns in the map that can hold tiles
+ @param rows the number of rows in the map that can hold tiles
+ @param tileSize the size of each tile in points
+ @param tileGroupLayout an array of tile groups that we want to use to fill the tile map
+ */
++ (instancetype)tileMapNodeWithTileSet:(SKTileSet *)tileSet columns:(NSUInteger)columns rows:(NSUInteger)rows tileSize:(CGSize)tileSize tileGroupLayout:(NSArray<SKTileGroup *> *)tileGroupLayout;
+
+/**
+ Initialize a tile map node with the specified tile set and dimensions. The tiles of the map will be empty, equivalent to the nil tile definition/group.
+ @param tileSet the tile set that is used to render the tiles
+ @param columns the number of columns in the map that can hold tiles
+ @param rows the number of rows in the map that can hold tiles
+ @param tileSize the size of each tile in points
+ */
+- (instancetype)initWithTileSet:(SKTileSet *)tileSet columns:(NSUInteger)columns rows:(NSUInteger)rows tileSize:(CGSize)tileSize;
+
+/**
+ Initialize a tile map node with the specified tile set and dimensions, and fill it with the specified tile group.
+ @param tileSet the tile set that is used to render the tiles
+ @param columns the number of columns in the map that can hold tiles
+ @param rows the number of rows in the map that can hold tiles
+ @param tileSize the size of each tile in points
+ @param tileGroup the tile group we wish to fill the tile map with
+ */
+- (instancetype)initWithTileSet:(SKTileSet *)tileSet columns:(NSUInteger)columns rows:(NSUInteger)rows tileSize:(CGSize)tileSize fillWithTileGroup:(SKTileGroup *)tileGroup;
+
+/**
+ Initialize a tile map node with the specified tile set and dimensions, and fill it with a specific layout of tile groups that belong to the provided tile set. The tileGroupLayout array should match the dimensions of the tile map (i.e., the number of elements should be equal to columns * rows). Index 0 of the array maps to column 0, row 0 of the tile map. Index 1 is column 1, row 0, and so on, wrapping around to the next row once the index passes the number of columns in the tile map. If the array has fewer elements than the number of tiles in the map, the remaining tiles are initialized with the nil tile group. If the array has more elements than the number of tiles in the map, the extra tile groups are ignored.
+ @param tileSet the tile set that is used to render the tiles
+ @param columns the number of columns in the map that can hold tiles
+ @param rows the number of rows in the map that can hold tiles
+ @param tileSize the size of each tile in points
+ @param tileGroupLayout an array of tile groups that we want to use to fill the tile map
+ */
+- (instancetype)initWithTileSet:(SKTileSet *)tileSet columns:(NSUInteger)columns rows:(NSUInteger)rows tileSize:(CGSize)tileSize tileGroupLayout:(NSArray<SKTileGroup *> *)tileGroupLayout;
+
+/**
+ The number of columns in the tile map.
+ */
+@property (nonatomic) NSUInteger numberOfColumns;
+
+/**
+ The number of rows in the tile map.
+ */
+@property (nonatomic) NSUInteger numberOfRows;
+
+/**
+ The size of each tile in the map.
+ */
+@property (nonatomic) CGSize tileSize;
+
+/**
+ The size of the tile map. This is dependent on the tileSize, the number of columns and rows in the map, and the tile set type.
+ */
+@property (nonatomic, readonly) CGSize mapSize;
+
+/**
+ The tile set being used by this tile map.
+ */
+@property (nonatomic) SKTileSet *tileSet;
+
+/**
+ Controls the blending between the texture and the tile map color. The valid interval of values is from 0.0 up to and including 1.0. A value above or below that interval is clamped to the minimum (0.0) if below or the maximum (1.0) if above.
+ */
+@property (nonatomic) CGFloat colorBlendFactor;
+
+/**
+ Base color for the tile map (If no texture is present, the color still is drawn).
+ */
+@property (nonatomic, retain) SKColor *color;
+
+/**
+ Sets the blend mode to use when composing the tile map with the final framebuffer.
+ @see SKNode.SKBlendMode
+ */
+@property (nonatomic) SKBlendMode blendMode;
+
+/**
+ Used to choose the location in the tile map that maps to its 'position' in the parent's coordinate space. The valid interval for each input is from 0.0 up to and including 1.0.
+ */
+@property (nonatomic) CGPoint anchorPoint;
+
+/**
+ A property that determines whether the tile map is rendered using a custom shader.
+ */
+@property (nonatomic, retain, nullable) SKShader *shader;
+
+/**
+ Bitmask to indicate being lit by a set of lights using overlapping lighting categories.
+
+ A light whose category is set to a value that masks to non-zero using this mask will
+ apply light to this sprite.
+
+ When used together with a normal texture, complex lighting effects can be used.
+ */
+@property (nonatomic) uint32_t lightingBitMask;
+
+@property (nonatomic) BOOL enableAutomapping;
+
+/**
+ Fill the entire tile map with the provided tile group.
+ @param tileGroup the tile group that will be used to fill the map
+ */
+- (void)fillWithTileGroup:(nullable SKTileGroup *)tileGroup;
+
+/**
+ Look up the tile definition at the specified tile index.
+ @param column the column index of the tile
+ @param row the row index of the tile
+ */
+- (nullable SKTileDefinition *)tileDefinitionAtColumn:(NSUInteger)column row:(NSUInteger)row;
+
+/**
+ Look up the tile group at the specified tile index.
+ @param column the column index of the tile
+ @param row the row index of the tile
+ */
+- (nullable SKTileGroup *)tileGroupAtColumn:(NSUInteger)column row:(NSUInteger)row;
+
+/**
+ Set the tile group at the specified tile index. When automapping is enabled, the appropriate tile definitions will automatically be selected and placed, possibly modifying neighboring tiles. When automapping is disabled, it will simply place the default center tile definition for the group, and will not modify any of the neihboring tiles.
+ @param tileGroup the tile group we want to place in the map
+ @param column the column index of the tile
+ @param row the row index of the tile
+ */
+- (void)setTileGroup:(nullable SKTileGroup *)tileGroup forColumn:(NSUInteger)column row:(NSUInteger)row;
+
+/**
+ Set the tile group and tile defintion at the specified tile index. When automapping is enabled, it will attempt to resolve the surrounding tiles to allow the specified tile definition to be placed. When automapping is disabled, it will simply place the tile definition and not modify any of the neighboring tiles.
+ @param tileGroup the tile group we want to place in the map
+ @param tileDefinition the tile definition we want to place in the map
+ @param column the column index of the tile
+ @param row the row index of the tile
+ */
+- (void)setTileGroup:(SKTileGroup *)tileGroup andTileDefinition:(SKTileDefinition *)tileDefinition forColumn:(NSUInteger)column row:(NSUInteger)row;
+
+/**
+ Returns the column index of the tile that lies under the specified position. Returns NSUIntegerMax if the position does not fall within the tile map.
+ @param position the position we want to check against the tile map
+ */
+- (NSUInteger)tileColumnIndexFromPosition:(CGPoint)position;
+
+/**
+ Returns the row index of the tile that lies under the specified position. Returns NSUIntegerMax if the position does not fall within the tile map.
+ @param position the position we want to check against the tile map
+ */
+- (NSUInteger)tileRowIndexFromPosition:(CGPoint)position;
+
+/**
+ Returns the position of the center of the tile at the specified column and row.
+ @param column the column index of the tile
+ @param row the row index of the tile
+ */
+- (CGPoint)centerOfTileAtColumn:(NSUInteger)column row:(NSUInteger)row;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTileSet.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTileSet.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTileSet.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTileSet.h	2016-05-28 06:40:54.000000000 +0200
@@ -0,0 +1,251 @@
+//
+//  SKTileSet.h
+//
+//  Copyright © 2015 Apple Inc. All rights reserved.
+//
+
+#import <SpriteKit/SKTileDefinition.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+/**
+ The tile set type is used to describe how the tiles will be arranged in a tile map.
+ 
+ @enum SKTileSetTypeGrid Specifies that the tiles will be axis-alligned rectangles that are placed in rows and columns at right angles to one another. This is the default type.
+ @enum SKTileSetTypeIsometric Specifies that the tiles will be rectangles that are rotated and scaled to give the appearance of 3/4 perspective.
+ @enum SKTileSetTypeHexagonalFlat Specifies that the tiles will be flat bottomed hexagons.
+ @enum SKTileSetTypeHexagonalPointy Specifies that the tiles will be "pointy" bottomed hexagons.
+*/
+typedef NS_ENUM(NSUInteger, SKTileSetType) {
+    SKTileSetTypeGrid,
+    SKTileSetTypeIsometric,
+    SKTileSetTypeHexagonalFlat,
+    SKTileSetTypeHexagonalPointy,
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
+/**
+ The adjacency mask is used to specify which neighboring tiles need to be filled in for a rule to go into effect.
+ */
+typedef NS_OPTIONS(NSUInteger, SKTileAdjacencyMask) {
+    
+    SKTileAdjacencyUp         = 1 << 0, // The above neighboring tile
+    SKTileAdjacencyUpperRight = 1 << 1, // The neighboring tile to the upper right
+    SKTileAdjacencyRight      = 1 << 2, // The neighboring tile to the right
+    SKTileAdjacencyLowerRight = 1 << 3, // The neighboring tile to the lower right
+    SKTileAdjacencyDown       = 1 << 4, // The below neighboring tile
+    SKTileAdjacencyLowerLeft  = 1 << 5, // The neighboring tile to the lower left
+    SKTileAdjacencyLeft       = 1 << 6, // The neighboring tile to the left
+    SKTileAdjacencyUpperLeft  = 1 << 7, // The neighboring tile to the upper left
+    
+    SKTileAdjacencyAll = SKTileAdjacencyUp | SKTileAdjacencyUpperRight | SKTileAdjacencyRight | SKTileAdjacencyLowerRight | SKTileAdjacencyDown | SKTileAdjacencyLowerLeft | SKTileAdjacencyLeft | SKTileAdjacencyUpperLeft,
+    
+    SKTileHexFlatAdjacencyUp         = 1 << 0,
+    SKTileHexFlatAdjacencyUpperRight = 1 << 1,
+    SKTileHexFlatAdjacencyLowerRight = 1 << 2,
+    SKTileHexFlatAdjacencyDown       = 1 << 3,
+    SKTileHexFlatAdjacencyLowerLeft  = 1 << 4,
+    SKTileHexFlatAdjacencyUpperLeft  = 1 << 5,
+    
+    SKTileHexFlatAdjacencyAll = SKTileHexFlatAdjacencyUp | SKTileHexFlatAdjacencyUpperRight | SKTileHexFlatAdjacencyLowerRight | SKTileHexFlatAdjacencyDown | SKTileHexFlatAdjacencyLowerLeft | SKTileHexFlatAdjacencyUpperLeft,
+    
+    SKTileHexPointyAdjacencyUpperLeft  = 1 << 0,
+    SKTileHexPointyAdjacencyUpperRight = 1 << 1,
+    SKTileHexPointyAdjacencyRight      = 1 << 2,
+    SKTileHexPointyAdjacencyLowerRight = 1 << 3,
+    SKTileHexPointyAdjacencyLowerLeft  = 1 << 4,
+    SKTileHexPointyAdjacencyLeft       = 1 << 5,
+    
+    SKTileHexPointyAdjacencyAdd = SKTileHexPointyAdjacencyUpperLeft | SKTileHexPointyAdjacencyUpperRight | SKTileHexPointyAdjacencyRight | SKTileHexPointyAdjacencyLowerRight | SKTileHexPointyAdjacencyLowerLeft | SKTileHexPointyAdjacencyLeft,
+    
+    // The enumerators below are pre-defined values for common tile configurations
+    
+    // Pre-defined values for an upwards-facing edge tile.
+    SKTileAdjacencyUpEdge = SKTileAdjacencyRight | SKTileAdjacencyLowerRight | SKTileAdjacencyDown | SKTileAdjacencyLowerLeft | SKTileAdjacencyLeft,
+    
+    // Pre-defined values for an upper right-facing edge tile.
+    SKTileAdjacencyUpperRightEdge = SKTileAdjacencyDown | SKTileAdjacencyLowerLeft | SKTileAdjacencyLeft,
+    
+    // Pre-defined values for a right-facing edge tile.
+    SKTileAdjacencyRightEdge = SKTileAdjacencyDown | SKTileAdjacencyLowerLeft | SKTileAdjacencyLeft | SKTileAdjacencyUpperLeft | SKTileAdjacencyUp,
+    
+    // Pre-defined values for a lower right-facing edge tile.
+    SKTileAdjacencyLowerRightEdge = SKTileAdjacencyLeft | SKTileAdjacencyUpperLeft | SKTileAdjacencyUp,
+    
+    // Pre-defined values for a downwards-facing edge tile.
+    SKTileAdjacencyDownEdge = SKTileAdjacencyUp | SKTileAdjacencyUpperRight | SKTileAdjacencyRight | SKTileAdjacencyLeft | SKTileAdjacencyUpperLeft,
+    
+    // Pre-defined values for a lower left-facing edge tile.
+    SKTileAdjacencyLowerLeftEdge = SKTileAdjacencyUp | SKTileAdjacencyUpperRight | SKTileAdjacencyRight,
+    
+    // Pre-defined values for a left-facing edge tile.
+    SKTileAdjacencyLeftEdge = SKTileAdjacencyUp | SKTileAdjacencyUpperRight | SKTileAdjacencyRight | SKTileAdjacencyLowerRight | SKTileAdjacencyDown,
+    
+    // Pre-defined values for a upper left-facing edge tile.
+    SKTileAdjacencyUpperLeftEdge = SKTileAdjacencyRight | SKTileAdjacencyLowerRight | SKTileAdjacencyDown,
+    
+    // Pre-defined values for an upper right-facing corner tile.
+    SKTileAdjacencyUpperRightCorner = SKTileAdjacencyUp | SKTileAdjacencyUpperRight | SKTileAdjacencyRight | SKTileAdjacencyLowerRight | SKTileAdjacencyDown | SKTileAdjacencyLeft | SKTileAdjacencyUpperLeft,
+    
+    // Pre-defined values for a lower right-facing corner tile.
+    SKTileAdjacencyLowerRightCorner = SKTileAdjacencyUp | SKTileAdjacencyUpperRight | SKTileAdjacencyRight | SKTileAdjacencyLowerRight | SKTileAdjacencyDown | SKTileAdjacencyLowerLeft | SKTileAdjacencyLeft,
+    
+    // Pre-defined values for a lower left-facing corner tile.
+    SKTileAdjacencyLowerLeftCorner = SKTileAdjacencyUp | SKTileAdjacencyRight | SKTileAdjacencyLowerRight | SKTileAdjacencyDown | SKTileAdjacencyLowerLeft | SKTileAdjacencyLeft | SKTileAdjacencyUpperLeft,
+    
+    // Pre-defined values for an upper left-facing corner tile.
+    SKTileAdjacencyUpperLeftCorner = SKTileAdjacencyUp | SKTileAdjacencyUpperRight | SKTileAdjacencyRight | SKTileAdjacencyDown | SKTileAdjacencyLowerLeft | SKTileAdjacencyLeft | SKTileAdjacencyUpperLeft,
+} NS_ENUM_AVAILABLE(10_12, 10_0);
+
+@class SKTileGroup, SKTileGroupRule;
+
+/**
+ A tile set contains all of the tile definitions that are available for use in a tile map. In addition, it also contains tile groups, which define collections of related tile definitions and the rules that govern their placement.
+ */
+SK_EXPORT NS_AVAILABLE(10_12, 10_0) @interface SKTileSet : NSObject <NSCopying, NSCoding>
+
+/**
+ Create a tile set with the specified tile groups.
+ @param tileGroups the tile groups that will be available for use with this set
+ */
++ (instancetype)tileSetWithTileGroups:(NSArray<SKTileGroup *> *)tileGroups;
+
+/**
+ Create a tile set with the specified tile groups and tile set type.
+ @param tileGroups the tile groups that will be available for use with this set
+ @param tileSetType the type of tile set this will be
+ */
++ (instancetype)tileSetWithTileGroups:(NSArray<SKTileGroup *> *)tileGroups tileSetType:(SKTileSetType)tileSetType;
+
+/**
+ Initilize a tile set with the specified tile groups.
+ @param tileGroups the tile groups that will be available for use with this set
+ */
+- (instancetype)initWithTileGroups:(NSArray<SKTileGroup *> *)tileGroups;
+
+/**
+ Initilize a tile set with the specified tile groups and tile set type.
+ @param tileGroups the tile groups that will be available for use with this set
+ @param tileSetType the type of tile set this will be
+ */
+- (instancetype)initWithTileGroups:(NSArray<SKTileGroup *> *)tileGroups tileSetType:(SKTileSetType)tileSetType;
+
+/**
+ Gets the tile set with the specified name from the SpriteKit resource bundle. Returns nil if a tile set with a matching name cannot be found.
+ @param name the name of the tile set to search for
+ */
++ (nullable instancetype)tileSetNamed:(NSString *)name;
+
+/**
+ Creates a tile set from the specified tile set file. Returns nil if the URL doesn't point to a valid tile set file.
+ @param name the URL of the tile set file
+ */
++ (nullable instancetype)tileSetFromURL:(NSURL *)url;
+
+/**
+ The tile groups that this set provides for use.
+ */
+@property (nonatomic, copy) NSArray<SKTileGroup *> *tileGroups;
+
+/**
+ Client-assignable name for the tile set. Defaults to nil.
+ */
+@property (nonatomic, copy, nullable) NSString *name;
+
+/**
+ The tile set type specifies how the tiles in the set will be arranged when placed in a tile map. Defaults to SKTileSetTypeGrid.
+ */
+@property (nonatomic) SKTileSetType type;
+
+@property (nonatomic, nullable) SKTileGroup *defaultTileGroup;
+
+/**
+ The default tile size is the value an SKTileMapNode will use for it's tiles when the tile set is assigned to it.
+ */
+@property (nonatomic) CGSize defaultTileSize;
+
+@end
+
+/**
+ A tile group encapsulates a collection of related tile definitions that are designed to be pieced together within a tile map. How those tiles are pieced together is governed by the set of rules. When a tile group is placed in a tile map, the map evaluates the rules to determine which tiles should be placed to achieve the desired outcome.
+ */
+SK_EXPORT NS_AVAILABLE(10_12, 10_0) @interface SKTileGroup : NSObject <NSCopying, NSCoding>
+
+/**
+ Create a simple tile group for a single tile definition. This creates and initializes the SKTileGroupRule necessary to place the provided tile definition in a tile map.
+ @param the tile definition we wish to place in a tile map
+ */
++ (instancetype)tileGroupWithTileDefinition:(SKTileDefinition *)tileDefinition;
+
+/**
+ Create a tile group with the specified rules.
+ @param rules the rules the group will use to determine tile placement
+ */
++ (instancetype)tileGroupWithRules:(NSArray<SKTileGroupRule *> *)rules;
+
+/**
+ Create an empty tile group. Placing this in a tile map will erase the existing tile at that location.
+ */
++ (instancetype)emptyTileGroup;
+
+/**
+ Initilize a simple tile group for a single tile definition. This creates and initializes the SKTileGroupRule necessary to place the provided tile definition in a tile map.
+ @param the tile definition we wish to place in a tile map
+ */
+- (instancetype)initWithTileDefinition:(SKTileDefinition *)tileDefinition;
+
+/**
+ Initilize a tile group with the specified rules.
+ @param rules the rules the group will use to determine tile placement
+ */
+- (instancetype)initWithRules:(NSArray<SKTileGroupRule *> *)rules;
+
+/**
+ The rules that govern which tiles are placed when this group is used, and where in the map they'll be placed.
+ */
+@property (nonatomic, copy) NSArray<SKTileGroupRule *> *rules;
+
+/**
+ Client-assignable name for the tile group. Defaults to nil.
+ */
+@property (nonatomic, copy, nullable) NSString *name;
+
+@end
+
+/**
+ A tile group rule defines how a certain type of tile should be placed on the map. These tiles are like puzzle pieces, and the rules define how they should be pieced together. This is accomplished by defining which neighboring spaces need to be filled with tiles that belong to the same group, and which tiles are required to be empty. The required pattern of neighboring tiles is defined using the SKTileAdjacencyMask.
+ */
+SK_EXPORT NS_AVAILABLE(10_12, 10_0) @interface SKTileGroupRule : NSObject <NSCopying, NSCoding>
+
+/**
+ Create a tile group rule with the specified adjacency and tile definitions.
+ @param adjacency the adjacency requirements for this rule; use the mask that covers the adjacent spaces that must be filled with tiles belonging to the same group; tiles not masked out must be empty
+ @param tileDefinitions the tile definitions used for this rule
+ */
++ (instancetype)tileGroupRuleWithAdjacency:(SKTileAdjacencyMask)adjacency tileDefinitions:(NSArray<SKTileDefinition*>*)tileDefinitions;
+
+/**
+ Initilize a tile group rule with the specified adjacency and tile definitions.
+ @param adjacency the adjacency requirements for this rule; use the mask that covers the adjacent spaces that must be filled with tiles belonging to the same group; tiles not masked out must be empty
+ @param tileDefinitions the tile definitions used for this rule
+ */
+- (instancetype)initWithAdjacency:(SKTileAdjacencyMask)adjacency tileDefinitions:(NSArray<SKTileDefinition *> *)tileDefinitions;
+
+/**
+ The adjacency mask used by this rule. Set this to the mask that covers the adjacent spaces that must be filled with tiles belonging to the same group for this rule met.
+ */
+@property (nonatomic) SKTileAdjacencyMask adjacency;
+
+
+/**
+ The tile definitions used by this rule. If the rule is evaluated and its conditions are met, one of the tile definitions within this array will be randomly selected for placement within the tile map. Each tile definitions' placement weight is taken into consideration to determine how likely each is to be selected; tile definitions with higher placement weights will be selected more frequently than those with lower placement weights.
+ */
+@property (nonatomic, copy) NSArray<SKTileDefinition *> *tileDefinitions;
+
+/**
+ Client-assignable name for the tile group rule. Defaults to nil.
+ */
+@property (nonatomic, copy, nullable) NSString *name;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTransition.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTransition.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTransition.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKTransition.h	2016-05-28 06:30:01.000000000 +0200
@@ -9,7 +9,9 @@
 
 NS_ASSUME_NONNULL_BEGIN
 
+#if __has_include(<CoreImage/CIFilter.h>)
 @class CIFilter;
+#endif
 
 typedef NS_ENUM(NSInteger, SKTransitionDirection) {
     SKTransitionDirectionUp,
@@ -43,9 +45,11 @@
 
 + (SKTransition *)doorwayWithDuration:(NSTimeInterval)sec;
 
+#if __has_include(<CoreImage/CIFilter.h>)
 /* Create a transition with a CIFilter. The filter must be a transition filter which requires only two images (inputImage, inputTargetImage) and generates a single image (outputImage). SpriteKit sets the inputImage, inputTargetImage, and inputTime properties when rendering, all others must be setup beforehand. */
 
 + (SKTransition *)transitionWithCIFilter:(CIFilter*)filter duration:(NSTimeInterval)sec;
+#endif
 
 /**
  Pause the incoming Scene during the transition, defaults to YES.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKUniform.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKUniform.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKUniform.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKUniform.h	2016-05-28 06:41:02.000000000 +0200
@@ -9,7 +9,11 @@
 
 #import <SpriteKit/SpriteKitBase.h>
 #import <SpriteKit/SKTexture.h>
+#import <simd/simd.h>
+
+#if __has_include(<GLKit/GLKMath.h>)
 #import <GLKit/GLKMath.h>
+#endif
 
 typedef NS_ENUM(NSInteger, SKUniformType) {
     SKUniformTypeNone               =    0,
@@ -42,7 +46,7 @@
  @param name the name of the shader uniform.
  @param texture the texture data associated with this uniform.
  */
-+ (instancetype)uniformWithName:(NSString *)name texture:(SKTexture*)texture;
++ (instancetype)uniformWithName:(NSString *)name texture:(nullable SKTexture*)texture;
 
 /**
  Create a shader uniform with a given name, and a float value
@@ -58,7 +62,7 @@
  @param name the name of the shader uniform.
  @param value the float vector2 value associated with this uniform.
  */
-+ (instancetype)uniformWithName:(NSString *)name floatVector2:(GLKVector2)value;
++ (instancetype)uniformWithName:(NSString *)name vectorFloat2:(vector_float2)value NS_AVAILABLE(10_12, 10_0);
 
 /**
  Create a shader uniform with a given name, and a float vector3 value
@@ -66,7 +70,7 @@
  @param name the name of the shader uniform.
  @param value the float vector3 value associated with this uniform.
  */
-+ (instancetype)uniformWithName:(NSString *)name floatVector3:(GLKVector3)value;
++ (instancetype)uniformWithName:(NSString *)name vectorFloat3:(vector_float3)value NS_AVAILABLE(10_12, 10_0);
 
 /**
  Create a shader uniform with a given name, and a float vector4 value
@@ -74,7 +78,7 @@
  @param name the name of the shader uniform.
  @param value the float vector4 value associated with this uniform.
  */
-+ (instancetype)uniformWithName:(NSString *)name floatVector4:(GLKVector4)value;
++ (instancetype)uniformWithName:(NSString *)name vectorFloat4:(vector_float4)value NS_AVAILABLE(10_12, 10_0);
 
 /**
  Create a shader uniform with a given name, and a 2x2 matrix value
@@ -82,7 +86,7 @@
  @param name the name of the shader uniform.
  @param value the 2x2 matrix value associated with this uniform.
  */
-+ (instancetype)uniformWithName:(NSString *)name floatMatrix2:(GLKMatrix2)value;
++ (instancetype)uniformWithName:(NSString *)name matrixFloat2x2:(matrix_float2x2)value NS_AVAILABLE(10_12, 10_0);
 
 /**
  Create a shader uniform with a given name, and a 3x3 matrix value
@@ -90,7 +94,7 @@
  @param name the name of the shader uniform.
  @param value the 3x3 matrix value associated with this uniform.
  */
-+ (instancetype)uniformWithName:(NSString *)name floatMatrix3:(GLKMatrix3)value;
++ (instancetype)uniformWithName:(NSString *)name matrixFloat3x3:(matrix_float3x3)value NS_AVAILABLE(10_12, 10_0);
 
 /**
  Create a shader uniform with a given name, and a 4x4 matrix value
@@ -98,7 +102,7 @@
  @param name the name of the shader uniform.
  @param value the 4x4 matrix value associated with this uniform.
  */
-+ (instancetype)uniformWithName:(NSString *)name floatMatrix4:(GLKMatrix4)value;
++ (instancetype)uniformWithName:(NSString *)name matrixFloat4x4:(matrix_float4x4)value NS_AVAILABLE(10_12, 10_0);
 
 /* The name by which this uniform will be referenced in a shader */
 @property (nonatomic, readonly) NSString *name;
@@ -109,35 +113,47 @@
 /* Access to the texture data associated with the current uniform */
 @property (nonatomic, retain, nullable) SKTexture *textureValue;
 
-/* Access to the float value associated with the current uniform */
-@property float floatValue;
-/* Access to the float vector 2 value associated with the current uniform */
-@property GLKVector2 floatVector2Value;
-/* Access to the float vector 3 value associated with the current uniform */
-@property GLKVector3 floatVector3Value;
-/* Access to the float vector 4 value associated with the current uniform */
-@property GLKVector4 floatVector4Value;
-
-/* Access to the 2x2 matrix value associated with the current uniform */
-@property GLKMatrix2 floatMatrix2Value;
-/* Access to the 3x3 matrix value associated with the current uniform */
-@property GLKMatrix3 floatMatrix3Value;
-/* Access to the 4x4 matrix value associated with the current uniform */
-@property GLKMatrix4 floatMatrix4Value;
-
+/* Access to the value associated with the uniform */
+@property (nonatomic) float floatValue;
+@property (nonatomic) vector_float2 vectorFloat2Value NS_AVAILABLE(10_12, 10_0);
+@property (nonatomic) vector_float3 vectorFloat3Value NS_AVAILABLE(10_12, 10_0);
+@property (nonatomic) vector_float4 vectorFloat4Value NS_AVAILABLE(10_12, 10_0);
+@property (nonatomic) matrix_float2x2 matrixFloat2x2Value NS_AVAILABLE(10_12, 10_0);
+@property (nonatomic) matrix_float3x3 matrixFloat3x3Value NS_AVAILABLE(10_12, 10_0);
+@property (nonatomic) matrix_float4x4 matrixFloat4x4Value NS_AVAILABLE(10_12, 10_0);
 
 - (instancetype)initWithName:(NSString *)name;
-
 - (instancetype)initWithName:(NSString *)name texture:(nullable SKTexture*)texture;
-
 - (instancetype)initWithName:(NSString *)name float:(float)value;
-- (instancetype)initWithName:(NSString *)name floatVector2:(GLKVector2)value;
-- (instancetype)initWithName:(NSString *)name floatVector3:(GLKVector3)value;
-- (instancetype)initWithName:(NSString *)name floatVector4:(GLKVector4)value;
-
-- (instancetype)initWithName:(NSString *)name floatMatrix2:(GLKMatrix2)value;
-- (instancetype)initWithName:(NSString *)name floatMatrix3:(GLKMatrix3)value;
-- (instancetype)initWithName:(NSString *)name floatMatrix4:(GLKMatrix4)value;
+- (instancetype)initWithName:(NSString *)name vectorFloat2:(vector_float2)value NS_AVAILABLE(10_12, 10_0);
+- (instancetype)initWithName:(NSString *)name vectorFloat3:(vector_float3)value NS_AVAILABLE(10_12, 10_0);
+- (instancetype)initWithName:(NSString *)name vectorFloat4:(vector_float4)value NS_AVAILABLE(10_12, 10_0);
+- (instancetype)initWithName:(NSString *)name matrixFloat2x2:(matrix_float2x2)value NS_AVAILABLE(10_12, 10_0);
+- (instancetype)initWithName:(NSString *)name matrixFloat3x3:(matrix_float3x3)value NS_AVAILABLE(10_12, 10_0);
+- (instancetype)initWithName:(NSString *)name matrixFloat4x4:(matrix_float4x4)value NS_AVAILABLE(10_12, 10_0);
+
+#if __has_include(<GLKit/GLKMath.h>)
+@property GLKVector2 floatVector2Value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
+@property GLKVector3 floatVector3Value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
+@property GLKVector4 floatVector4Value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
+@property GLKMatrix2 floatMatrix2Value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
+@property GLKMatrix3 floatMatrix3Value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
+@property GLKMatrix4 floatMatrix4Value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
+
++ (instancetype)uniformWithName:(NSString *)name floatVector2:(GLKVector2)value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
++ (instancetype)uniformWithName:(NSString *)name floatVector3:(GLKVector3)value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
++ (instancetype)uniformWithName:(NSString *)name floatVector4:(GLKVector4)value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
++ (instancetype)uniformWithName:(NSString *)name floatMatrix2:(GLKMatrix2)value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
++ (instancetype)uniformWithName:(NSString *)name floatMatrix3:(GLKMatrix3)value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
++ (instancetype)uniformWithName:(NSString *)name floatMatrix4:(GLKMatrix4)value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
+
+- (instancetype)initWithName:(NSString *)name floatVector2:(GLKVector2)value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
+- (instancetype)initWithName:(NSString *)name floatVector3:(GLKVector3)value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
+- (instancetype)initWithName:(NSString *)name floatVector4:(GLKVector4)value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
+- (instancetype)initWithName:(NSString *)name floatMatrix2:(GLKMatrix2)value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
+- (instancetype)initWithName:(NSString *)name floatMatrix3:(GLKMatrix3)value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
+- (instancetype)initWithName:(NSString *)name floatMatrix4:(GLKMatrix4)value NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
+#endif
 
 @end
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVersion.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVersion.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVersion.h	2016-02-20 01:21:16.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVersion.h	2016-05-28 06:30:01.000000000 +0200
@@ -1 +1 @@
-#define SK_VERSION 17096008
+#define SK_VERSION 18064201
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVideoNode.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVideoNode.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVideoNode.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKVideoNode.h	2016-05-28 06:30:01.000000000 +0200
@@ -5,11 +5,14 @@
  Node that can play a video file
  
  
- @copyright 2011 Apple, Inc. All rights reserve.
+ @copyright 2011 Apple, Inc. All rights reserved.
  
  */
 
+#if __has_include(<AVFoundation/AVPlayer.h>)
 @class AVPlayer;
+#endif
+
 
 #import <SpriteKit/SKSpriteNode.h>
 #import <SpriteKit/SpriteKitBase.h>
@@ -21,26 +24,30 @@
 /**
  Create a video node from an AVPlayer. You can use the AVPlayer to control playback.
  */
+#if __has_include(<AVFoundation/AVPlayer.h>)
 + (SKVideoNode *)videoNodeWithAVPlayer:(AVPlayer*)player;
+#endif
 
 /**
  Create a video node from a file.
  */
-+ (SKVideoNode *)videoNodeWithVideoFileNamed:(NSString *)videoFile NS_DEPRECATED(10_8, 10_10, 7_0, 8_0);
-+ (SKVideoNode *)videoNodeWithFileNamed:(NSString *)videoFile NS_AVAILABLE(10_10, 8_0);
++ (SKVideoNode *)videoNodeWithVideoFileNamed:(NSString *)videoFile NS_DEPRECATED(10_8, 10_11, 7_0, 9_0);
++ (SKVideoNode *)videoNodeWithFileNamed:(NSString *)videoFile NS_AVAILABLE(10_11, 9_0);
 
 /**
  Create a video node from a URL.
  */
-+ (SKVideoNode *)videoNodeWithVideoURL:(NSURL *)videoURL NS_DEPRECATED(10_8, 10_10, 7_0, 8_0);
-+ (SKVideoNode *)videoNodeWithURL:(NSURL *)videoURL NS_AVAILABLE(10_10, 8_0);
++ (SKVideoNode *)videoNodeWithVideoURL:(NSURL *)videoURL NS_DEPRECATED(10_8, 10_11, 7_0, 9_0);
++ (SKVideoNode *)videoNodeWithURL:(NSURL *)videoURL NS_AVAILABLE(10_11, 9_0);
 
 /**
  Designated Initializer.
  
  Initialize a video node from an AVPlayer. You can use the AVPlayer to control playback.
  */
+#if __has_include(<AVFoundation/AVPlayer.h>)
 - (instancetype)initWithAVPlayer:(AVPlayer*)player NS_DESIGNATED_INITIALIZER;
+#endif
 
 /**
  Initialize a video node from a file.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKView.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKView.h	2016-05-28 06:41:02.000000000 +0200
@@ -5,9 +5,15 @@
 //  Copyright (c) 2011 Apple Inc. All rights reserved.
 //
 
+
 #import <SpriteKit/SpriteKitBase.h>
 
+
+/* SKView is not available on WatchOS, please see WKInterfaceSpriteKit */
+#if SKVIEW_AVAILABLE
+
 @class SKScene, SKTransition, SKTexture, SKNode;
+@protocol SKViewDelegate;
 
 /**
  The view to present your SKScene nodes in.
@@ -69,10 +75,30 @@
  */
 @property (nonatomic) BOOL ignoresSiblingOrder;
 
+
 @property (nonatomic) BOOL shouldCullNonVisibleNodes NS_AVAILABLE(10_10, 8_0);
 
-/* Number of hardware vsyncs between callbacks, same behaviour as CADisplayLink. Defaults to 1 (render every vsync) */
-@property (nonatomic) NSInteger frameInterval;
+
+/* Defines the desired rate for this SKView to it's content. 
+ Actual rate maybe be limited by hardware or other software. */
+@property (nonatomic) NSInteger preferredFramesPerSecond NS_AVAILABLE(10_12, 10_0);
+
+
+/**
+ Optional view delegate, see SKViewDelegate.
+ */
+@property (nonatomic, weak, nullable) NSObject<SKViewDelegate> *delegate NS_AVAILABLE(10_12, 10_0);
+
+
+/* Deprecated, please use preferredFramesPerSecond.
+ Number of frames to skip between renders, defaults to 1 (render every frame)
+ Actual requested rate will be preferredFramesPerSecond / frameInterval.  */
+@property (nonatomic) NSInteger frameInterval NS_DEPRECATED(10_8, 10_12, 7_0, 10_0);
+
+/* Deprecated, please use preferredFramesPerSecond. */
+/* FIXME: remove from public headers once all clinets adopt preferredFramesPerSecond. */
+@property(nonatomic) float preferredFrameRate NS_DEPRECATED(10_12, 10_12, 10_0, 10_0);
+
 
 /**
  Present an SKScene in the view, replacing the current scene.
@@ -129,4 +155,20 @@
 
 @end
 
+
+
+SK_EXPORT NS_AVAILABLE(10_12, 10_0) @protocol SKViewDelegate <NSObject>
+@optional
+/**
+ Allows the client to dynamically control the render rate.
+ 
+ return YES to initiate an update and render for the target time.
+ return NO to skip update and render for this target time.
+ */
+- (BOOL)view:(SKView *)view shouldRenderAtTime:(NSTimeInterval)time;
+@end
+
+
 NS_ASSUME_NONNULL_END
+
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKWarpGeometry.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKWarpGeometry.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKWarpGeometry.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SKWarpGeometry.h	2016-05-27 06:51:24.000000000 +0200
@@ -0,0 +1,132 @@
+
+/**
+ SKWarpGeometry.h
+ 
+ Nodes that conform to the SKWarpable protocol can be warped and animated by defining distortions via a SKWarpGeometry objects.
+
+  @copyright 2016 Apple, Inc. All rights reserved.
+ */
+
+#import <SpriteKit/SpriteKitBase.h>
+#import <SpriteKit/SKAction.h>
+#import <simd/simd.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class SKTexture, SKShader, SKWarpGeometry, SKWarpGeometryGrid;
+
+
+SK_EXPORT NS_AVAILABLE(10_12, 10_0) @protocol SKWarpable <NSObject>
+
+/* Warp geometry used to define the distortion */
+@property (nonatomic, nullable) SKWarpGeometry *warpGeometry;
+
+/* maximum number of subdivision iterations used to generate the final vertices */
+@property (nonatomic) NSInteger subdivisionLevels;
+
+@end
+
+
+
+
+/* Base class for future expansion */
+SK_EXPORT NS_AVAILABLE(10_12, 10_0) @interface SKWarpGeometry : NSObject <NSCopying, NSCoding>
+@end
+
+SK_EXPORT NS_AVAILABLE(10_12, 10_0) @interface SKWarpGeometryGrid : SKWarpGeometry <NSCoding>
+
+- (nullable instancetype)initWithCoder:(NSCoder *)aDecoder NS_DESIGNATED_INITIALIZER;
+
+/* 1x1 grid with no distortion */
++ (instancetype)grid;
+
+/* grid of the specified dimensions and no distortion */
++ (instancetype)gridWithColumns:(NSInteger)cols
+                           rows:(NSInteger)rows;
+
+/*
+ Create a grid of the specified dimensions, source and dest positions.
+ 
+ Grid dimensions (cols and rows) refer to the number of faces in each dimension. The
+ number of vertices required for a given dimension is equal to (cols + 1) * (rows + 1).
+ 
+ SourcePositions are normalized (0.0 - 1.0) coordinates to determine the source content.
+ 
+ DestPositions are normalized (0.0 - 1.0) positional coordinates with respect to
+ the node's native size. Values outside the (0.0-1.0) range are perfectly valid and
+ correspond to positions outside of the native undistorted bounds.
+ 
+ Source and dest positions are provided in row-major order staring from the top-left.
+ For example the indices for a 2x2 grid would be as follows:
+ 
+ [0]---[1]---[2]
+  |     |     |
+ [3]---[4]---[5]
+  |     |     |
+ [6]---[7]---[8]
+ 
+ */
+
++ (instancetype)gridWithColumns:(NSInteger)cols
+                           rows:(NSInteger)rows
+                sourcePositions:(nullable const vector_float2 *)sourcePositions
+                  destPositions:(nullable const vector_float2 *)destPositions;
+
+/* init with the specified dimensions, source and dest positions. */
+- (instancetype)initWithColumns:(NSInteger)cols
+                           rows:(NSInteger)rows
+                sourcePositions:(nullable const vector_float2 *)sourcePositions
+                  destPositions:(nullable const vector_float2 *)destPositions NS_DESIGNATED_INITIALIZER;
+
+/* the number of columns in this grid */
+@property (nonatomic, readonly) NSInteger numberOfColumns;
+
+/* the number of rows in this grid */
+@property (nonatomic, readonly) NSInteger numberOfRows;
+
+
+/* the total number of (sourcePosition + destPosition) pairs that define this grid.
+ For a given dimension this is equal to (numberOfColumns + 1) * (numberOfRows + 1). */
+@property (nonatomic, readonly) NSInteger vertexCount;
+
+- (vector_float2)sourcePositionAtIndex:(NSInteger)index;
+- (vector_float2)destPositionAtIndex:(NSInteger)index;
+
+- (instancetype)gridByReplacingSourcePositions:(const vector_float2 *)sourcePositions;
+- (instancetype)gridByReplacingDestPositions:(const vector_float2 *)destPositions;
+
+@end
+
+
+
+
+@interface SKAction (SKWarpable)
+
+/* Animate from the node's current warpGeometry to a new one over the specified duration.
+ 
+ If the numberOfColumns and numberOfRows match, a smooth interpolation will be performed
+ from the node current warp.
+ */
++ (nullable SKAction *)warpTo:(SKWarpGeometry *)warp
+                     duration:(NSTimeInterval)duration NS_AVAILABLE(10_12, 10_0);
+
+/* Animate through an array of warps
+ 
+ The numberOfColumns and numberOfRows must match for all warps.
+ Times are specified in seconds and must be increasing values.
+ */
++ (nullable SKAction *)animateWithWarps:(NSArray<SKWarpGeometry *> *)warps
+                                  times:(NSArray<NSNumber *> *)times NS_AVAILABLE(10_12, 10_0);
+
+/* Animate through an array of warps
+ 
+ The numberOfColumns and numberOfRows must match for all warps.
+ Times are specified in seconds and must be increasing values.
+ Optionally restore the original node's warpGeometry from before the action.
+ */
++ (nullable SKAction *)animateWithWarps:(NSArray<SKWarpGeometry *> *)warps
+                                  times:(NSArray<NSNumber *> *)times
+                                restore:(BOOL)restore NS_AVAILABLE(10_12, 10_0);
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SpriteKit.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SpriteKit.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SpriteKit.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SpriteKit.h	2016-05-28 06:30:01.000000000 +0200
@@ -23,7 +23,14 @@
 #import <SpriteKit/SKRegion.h>
 #import <SpriteKit/SKView.h>
 #import <SpriteKit/SKTransition.h>
+#import <SpriteKit/SKShader.h>
+#import <SpriteKit/SKUniform.h>
+#import <SpriteKit/SKAttribute.h>
+#import <SpriteKit/SKWarpGeometry.h>
 
+#import <SpriteKit/SKTileDefinition.h>
+#import <SpriteKit/SKTileSet.h>
+#import <SpriteKit/SKTileMapNode.h>
 
 #import <SpriteKit/SKTexture.h>
 #import <SpriteKit/SKMutableTexture.h>
@@ -37,3 +44,7 @@
 #import <SpriteKit/SKPhysicsBody.h>
 #import <SpriteKit/SKPhysicsJoint.h>
 #import <SpriteKit/SKPhysicsWorld.h>
+
+#if !TARGET_OS_IPHONE
+#import <SpriteKit/SKNode+NSAccessibility.h>
+#endif
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SpriteKitBase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SpriteKitBase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SpriteKitBase.h	2015-10-03 01:54:13.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/SpriteKit.framework/Headers/SpriteKitBase.h	2016-05-28 06:30:01.000000000 +0200
@@ -9,7 +9,6 @@
 #import <TargetConditionals.h>
 #import <CoreGraphics/CGGeometry.h>
 #import <Foundation/Foundation.h>
-#import <QuartzCore/QuartzCore.h>
 
 #import <SpriteKit/SKVersion.h>
 
@@ -19,12 +18,20 @@
 #import <AppKit/AppKit.h>
 #endif
 
+
+#if TARGET_OS_IPHONE && !__has_include(<UIKit/UIView.h>)
+#define SKVIEW_AVAILABLE 0
+#else
+#define SKVIEW_AVAILABLE 1
+#endif
+
 #ifdef __cplusplus
 #define SK_EXPORT extern "C" __attribute__((visibility ("default")))
 #else
 #define SK_EXPORT extern __attribute__((visibility ("default")))
 #endif
 #define SK_AVAILABLE __OSX_AVAILABLE_STARTING
+#define SK_WEAK_LINK __attribute__((weak_import))
 
 #if TARGET_OS_IPHONE
 #define SKColor UIColor

```