#MetalKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h
--- /Applications/Xcode8-beta4.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h	2016-07-23 01:33:25.000000000 +0200
+++ /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h	2016-08-03 06:00:08.000000000 +0200
@@ -4,11 +4,13 @@
  @abstract MetalKit helper functionality for loading a Metal texture from image file data
  @copyright Copyright © 2015 Apple, Inc. All rights reserved.
  */
-
+#import <TargetConditionals.h>
 #import <MetalKit/MTKDefines.h>
 #import <Foundation/Foundation.h>
 #import <CoreGraphics/CoreGraphics.h>
 
+
+
 @protocol MTLDevice;
 @protocol MTLTexture;
 @class MDLTexture;
@@ -178,40 +180,6 @@
                    options:(nullable NSDictionary <NSString *, NSObject *> *)options
          completionHandler:(nonnull MTKTextureLoaderCallback)completionHandler NS_AVAILABLE(10_12, 10_0);
 
-/*!
- @method newTextureWithName:scaleFactor:displayGamut:bundle:options:completionHandler:
- @abstract Asynchronously create a Metal texture and load image data from a given texture or image 
-           asset name
- @param names An array of texture asset names
- @param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
-                    value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor].
- @param displayGamut ColorSpace for the version of the texture you would like built.  This corresponds
-                     to the "Gamut" trait in xcode's asset catalog.  The app would usually
-                     obtain this by getting the colorSpace property of the NSScrean object
-                     the view is rendering on.  ( metalView.window.screen.colorSpace.CGColorSpace )
- @param bundle Resource bundle in which the asset is located.  Main bundle used if nil.
- @param options Dictonary of MTKTextureLoaderOptions. The following options are ignormed when used
-                to load a texture asset but can be used when creating a texture from an image asset:
-                    MTKTextureLoaderOptionGenerateMipmaps
-                    MTKTextureLoaderOptionSRGB
-                    MTKTextureLoaderOptionCubeFromVerticalTexture
-                    MTKTextureLoaderOptionOrigin
- @param completionHandler Block called when texture has been loaded and fully initialized
- @discussion Uses texture data from version of the texture from the texture set in the asset catalog
-             which mathces the device's traits.
-             This method attempts to load a texture asset with the name given.  If a texture asset
-             with the name given does not exist, it will attempt to create a texture from a an
-             image asset with the name give if it can.
-             This method can be used on macOS to choose between sRGB and P3 versions of a texture
-             asset depending on the gamut of the display rendered to.
- */
-- (void)newTextureWithName:(nonnull NSString *)name
-               scaleFactor:(CGFloat)scaleFactor
-              displayGamut:(nullable CGColorSpaceRef)displayGamut
-                    bundle:(nullable NSBundle *)bundle
-                   options:(nullable NSDictionary <NSString *, NSObject *> *)options
-         completionHandler:(nonnull MTKTextureLoaderCallback)completionHandler NS_AVAILABLE_MAC(10_12);
-
 
 /*!
  @method newTexturesWithContentsOfURLs:options:completionHandler:
@@ -254,42 +222,6 @@
                      options:(nullable NSDictionary <NSString *, NSObject *> *)options
            completionHandler:(nonnull MTKTextureLoaderArrayCallback)completionHandler NS_AVAILABLE(10_12, 10_0);
 
-/*!
-@method newTexturesWithNames:scaleFactor:displayGamut:bundle:options:completionHandler:
-@abstract Asynchronously create Metal textures and load image data from given texture or image
-          asset names
-@param names An array of texture asset names
-@param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
-                   value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor]
-@param displayGamut ColorSpace for the version of the texture you would like built.  This corresponds
-                    to the "Gamut" trait in xcode's asset catalog.  The app would usually
-                    obtain this by getting the colorSpace property of the NSScrean object
-                    the view is rendering on. ( metalView.window.screen.colorSpace.CGColorSpace )
-@param bundle Resource bundle in which the assets are located
-@param options Dictonary of MTKTextureLoaderOptions. The following options are ignormed when used
-               to load a texture asset but can be used when creating a texture from an image asset
-                   MTKTextureLoaderOptionGenerateMipmaps
-                   MTKTextureLoaderOptionSRGB
-                   MTKTextureLoaderOptionCubeFromVerticalTexture
-                   MTKTextureLoaderOptionOrigin
-@param completionHandler Block called when all of the textures have been loaded and fully
-                         initialized. The NSError will be nif if all of the textures are loaded
-                         successfully, or will correspond to one of the textures which failed to
-                         load.
-@discussion Uses texture data from version of the texture from the texture sets in the asset catalog
-            which mathces the device's traits.
-            This method attempts to load a texture asset with each name given.  If a texture asset
-            with the name given does not exist, it will attempt to create a texture from a an
-            image asset with the name give if it can.
-            This method can be used on macOS to choose between sRGB and P3 versions of a texture
-            asset depending on the gamut of the display rendered to
-*/
-- (void)newTexturesWithNames:(nonnull NSArray<NSString *> *)names
-                 scaleFactor:(CGFloat)scaleFactor
-                displayGamut:(nullable CGColorSpaceRef)displayGamut
-                      bundle:(nullable NSBundle *)bundle
-                     options:(nullable NSDictionary <NSString *, NSObject *> *)options
-           completionHandler:(nonnull MTKTextureLoaderArrayCallback)completionHandler NS_AVAILABLE_MAC(10_12);
 
 /*!
  @method newTextureWithData:options:completionHandler:
@@ -411,38 +343,5 @@
                                        options:(nullable NSDictionary <NSString *, NSObject *> *)options
                                          error:(NSError *__nullable *__nullable)error NS_AVAILABLE(10_12, 10_0);
 
-/*!
- @method newTextursWithName:sca;eFactpr:displayGamut:bundle:options:error:
- @abstract Synchronously create a Metal texture with texture data from a given texture or image
-           asset name
- @return The Metal texture. nil if an error occured
- @param names An array of texture asset names
- @param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
-                     value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor].
- @param displayGamut ColorSpace for the version of the texture you would like built.  This corresponds
-                     to the "Gamut" trait in xcode's asset catalog.  The app would usually
-                     obtain this by getting the colorSpace property of the NSScrean object
-                     the view is rendering on. ( metalView.window.screen.colorSpace.CGColorSpace )
- @param bundle Resource bundle in which the asset is located
- @param options Dictonary of MTKTextureLoaderOptions. The following options are ignormed when used
-                to load a texture asset but can be used when creating a texture from an image asset
-                    MTKTextureLoaderOptionGenerateMipmaps
-                    MTKTextureLoaderOptionSRGB
-                    MTKTextureLoaderOptionCubeFromVerticalTexture
-                    MTKTextureLoaderOptionOrigin
- @discussion Uses texture data from version of the texture from the texture set in the asset catalog
-             which mathces the device's traits.
-             This method attempts to load a texture asset with the name given.  If a texture asset
-             with the name given does not exist, it will attempt to create a texture from a an
-             image asset with the name give if it can.
-             This method can be used on macOS to choose between sRGB and P3 versions of a texture
-             asset depending on the gamut of the display rendered to.
- */
-- (nullable id <MTLTexture>)newTextureWithName:(nonnull NSString *)name
-                                   scaleFactor:(CGFloat)scaleFactor
-                                  displayGamut:(nullable CGColorSpaceRef)displayGamut
-                                        bundle:(nullable NSBundle *)bundle
-                                       options:(nullable NSDictionary <NSString *, NSObject *> *)options
-                                         error:(NSError *__nullable *__nullable)error NS_AVAILABLE_MAC(10_12);
 
 @end

```