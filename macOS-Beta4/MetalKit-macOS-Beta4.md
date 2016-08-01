#MetalKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h
--- /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h	2016-07-10 07:49:54.000000000 +0200
+++ /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h	2016-07-23 22:13:37.000000000 +0200
@@ -4,11 +4,14 @@
  @abstract MetalKit helper functionality for loading a Metal texture from image file data
  @copyright Copyright © 2015 Apple, Inc. All rights reserved.
  */
-
+#import <TargetConditionals.h>
 #import <MetalKit/MTKDefines.h>
 #import <Foundation/Foundation.h>
 #import <CoreGraphics/CoreGraphics.h>
 
+#import <AppKit/NSGraphics.h>
+
+
 @protocol MTLDevice;
 @protocol MTLTexture;
 @class MDLTexture;
@@ -183,12 +186,11 @@
  @abstract Asynchronously create a Metal texture and load image data from a given texture or image 
            asset name
  @param names An array of texture asset names
- @param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
-                    value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor].
- @param displayGamut ColorSpace for the version of the texture you would like built.  This corresponds
-                     to the "Gamut" trait in xcode's asset catalog.  The app would usually
-                     obtain this by getting the colorSpace property of the NSScrean object
-                     the view is rendering on.  ( metalView.window.screen.colorSpace.CGColorSpace )
+ @param scaleFactor Scale factor of the texture to retrieve from the asset catalog.  Typically the
+                    value retrieved from -[NSWindow backingScaleFactor].
+ @param displayGamut Version of the texture based upon the "Gamut" trait in Xcode.  You'd typically
+                     check -[NSWindow canRepresentDisplayGamut:] with the widest NSDisplayGamut value
+                     and pass that value here if it returns YES.
  @param bundle Resource bundle in which the asset is located.  Main bundle used if nil.
  @param options Dictonary of MTKTextureLoaderOptions. The following options are ignormed when used
                 to load a texture asset but can be used when creating a texture from an image asset:
@@ -207,7 +209,7 @@
  */
 - (void)newTextureWithName:(nonnull NSString *)name
                scaleFactor:(CGFloat)scaleFactor
-              displayGamut:(nullable CGColorSpaceRef)displayGamut
+              displayGamut:(NSDisplayGamut)displayGamut
                     bundle:(nullable NSBundle *)bundle
                    options:(nullable NSDictionary <NSString *, NSObject *> *)options
          completionHandler:(nonnull MTKTextureLoaderCallback)completionHandler NS_AVAILABLE_MAC(10_12);
@@ -259,13 +261,11 @@
 @abstract Asynchronously create Metal textures and load image data from given texture or image
           asset names
 @param names An array of texture asset names
-@param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
+@param scaleFactor Scale factor of the texture to retrieve from the asset catalog.  Typically the
                    value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor]
-@param displayGamut ColorSpace for the version of the texture you would like built.  This corresponds
-                    to the "Gamut" trait in xcode's asset catalog.  The app would usually
-                    obtain this by getting the colorSpace property of the NSScrean object
-                    the view is rendering on. ( metalView.window.screen.colorSpace.CGColorSpace )
-@param bundle Resource bundle in which the assets are located
+@param displayGamut Version of the texture based upon the "Gamut" trait in Xcode.  You'd typically
+                    check -[NSWindow canRepresentDisplayGamut:] with the widest NSDisplayGamut value
+                    and pass that value here if it returns YES.@param bundle Resource bundle in which the assets are located
 @param options Dictonary of MTKTextureLoaderOptions. The following options are ignormed when used
                to load a texture asset but can be used when creating a texture from an image asset
                    MTKTextureLoaderOptionGenerateMipmaps
@@ -417,12 +417,11 @@
            asset name
  @return The Metal texture. nil if an error occured
  @param names An array of texture asset names
- @param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
-                     value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor].
- @param displayGamut ColorSpace for the version of the texture you would like built.  This corresponds
-                     to the "Gamut" trait in xcode's asset catalog.  The app would usually
-                     obtain this by getting the colorSpace property of the NSScrean object
-                     the view is rendering on. ( metalView.window.screen.colorSpace.CGColorSpace )
+ @param scaleFactor Scale factor of the texture to retrieve from the asset catalog.  Typically the
+                    value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor].
+ @param displayGamut Version of the texture based upon the "Gamut" trait in Xcode.  You'd typically
+                     check -[NSWindow canRepresentDisplayGamut:] with the widest NSDisplayGamut value
+                     and pass that value here if it returns YES.@param bundle Resource bundle in which the assets are located
  @param bundle Resource bundle in which the asset is located
  @param options Dictonary of MTKTextureLoaderOptions. The following options are ignormed when used
                 to load a texture asset but can be used when creating a texture from an image asset

```