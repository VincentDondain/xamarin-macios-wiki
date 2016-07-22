#WatchKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceSCNScene.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceSCNScene.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceSCNScene.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceSCNScene.h	2016-06-03 05:34:20.000000000 +0200
@@ -0,0 +1,47 @@
+//
+//  WKInterfaceSCNScene.h
+//  WatchKit
+//
+//  Copyright (c) 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <WatchKit/WKDefines.h>
+#import <WatchKit/WKInterfaceObject.h>
+#import <SceneKit/SceneKit.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKInterfaceSCNScene : WKInterfaceObject <SCNSceneRenderer>
+
+/*!
+ @property scene
+ @abstract Specifies the scene of the receiver
+ */
+@property(nonatomic, retain, nullable) SCNScene *scene;
+
+/*!
+ @property snapshot
+ @abstract Draws the contents of the view and returns them as a new image object
+ @discussion This method is thread-safe and may be called at any time.
+ */
+- (UIImage *)snapshot;
+
+/*!
+ @property preferredFramesPerSecond
+ @abstract The rate you want the view to redraw its contents.
+ @discussion When your application sets its preferred frame rate, the view chooses a frame rate as close to that as possible based on the capabilities of the screen the view is displayed on. The actual frame rate chosen is usually a factor of the maximum refresh rate of the screen to provide a consistent frame rate. For example, if the maximum refresh rate of the screen is 60 frames per second, that is also the highest frame rate the view sets as the actual frame rate. However, if you ask for a lower frame rate, it might choose 30, 20, 15 or some other factor to be the actual frame rate. Your application should choose a frame rate that it can consistently maintain.
+ The default value is 0 which means the display link will fire at the native cadence of the display hardware.
+ */
+@property(nonatomic) NSInteger preferredFramesPerSecond;
+
+/*!
+ @property antialiasingMode
+ @abstract Defaults to SCNAntialiasingModeNone.
+ */
+@property(nonatomic) SCNAntialiasingMode antialiasingMode;
+
+@end
+
+NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceSKScene.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceSKScene.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceSKScene.h	1970-01-01 01:00:00.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/WatchKit.framework/Headers/WKInterfaceSKScene.h	2016-06-03 05:34:20.000000000 +0200
@@ -0,0 +1,67 @@
+//
+//  WKInterfaceSKScene.h
+//  WatchKit
+//
+//  Copyright © 2016 Apple Inc. All rights reserved.
+//
+
+#import <Foundation/Foundation.h>
+#import <WatchKit/WKDefines.h>
+#import <WatchKit/WKInterfaceObject.h>
+
+NS_ASSUME_NONNULL_BEGIN
+
+@class SKScene, SKTransition, SKTexture, SKNode;
+
+WK_AVAILABLE_WATCHOS_ONLY(3.0)
+@interface WKInterfaceSKScene : WKInterfaceObject
+
+/**
+ Pause the entire interface
+ */
+@property (nonatomic, getter = isPaused) BOOL paused;
+
+/* Defines the desired rate for interface to render it's content.
+ Actual rate maybe be limited by hardware or other software. */
+@property (nonatomic) NSInteger preferredFramesPerSecond NS_AVAILABLE(10_12, 10_0);
+
+/**
+ Present an SKScene in the interface, replacing the current scene.
+ 
+ @param scene the scene to present.
+ */
+- (void)presentScene:(nullable SKScene *)scene;
+
+/**
+ Present an SKScene in the interface, replacing the current scene.
+ 
+ If there is currently a scene being presented in the interface, the transition is used to swap between them.
+ 
+ @param scene the scene to present.
+ @param transition the transition to use when presenting the scene.
+ */
+- (void)presentScene:(SKScene *)scene transition:(SKTransition *)transition;
+
+/**
+ The currently presented scene, otherwise nil. If in a transition, the 'incoming' scene is returned.
+ */
+@property (nonatomic, readonly, nullable) SKScene *scene;
+
+/**
+ Create an SKTexture containing a snapshot of how it would have been rendered in this interface.
+ The texture is tightly cropped to the size of the node.
+ @param node the node subtree to render to the texture.
+ */
+- (nullable SKTexture *)textureFromNode:(SKNode *)node;
+
+/**
+ Create an SKTexture containing a snapshot of how it would have been rendered in this interface.
+ The texture is cropped to the specified rectangle
+ @param node the node subtree to render to the texture.
+ @param crop the rectangle to crop to
+ */
+- (nullable SKTexture *)textureFromNode:(SKNode *)node crop:(CGRect)crop;
+
+@end
+
+NS_ASSUME_NONNULL_END
```