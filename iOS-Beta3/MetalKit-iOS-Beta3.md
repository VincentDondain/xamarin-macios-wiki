#MetalKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h	2016-06-25 02:25:02.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h	2016-07-10 07:49:54.000000000 +0200
@@ -6,7 +6,6 @@
  */
 
 #import <MetalKit/MTKDefines.h>
-
 #import <Foundation/Foundation.h>
 #import <CoreGraphics/CoreGraphics.h>
 
@@ -14,17 +13,6 @@
 @protocol MTLTexture;
 @class MDLTexture;
 
-
-/*!
- @enum MTKDisplayGamut
- @abstract DisplayGamut assocated with a version of a texture from a texture set.
- */
-typedef NS_ENUM(NSUInteger, MTKDisplayGamut)
-{
-    MTKDisplayGamutSRGB = 0,
-    MTKDisplayGamutDisplayP3 = 1,
-};
-
 /*!
  @group MTKTextureLoaderErrors
  */
@@ -128,7 +116,7 @@
 
 typedef void (^MTKTextureLoaderCallback) (id <MTLTexture> __nullable texture, NSError * __nullable error);
 
-typedef void (^MTKTextureLoaderArrayCallback) (NSArray<id <MTLTexture>> * __nonnull textures, NSError * __nullable error);
+typedef void (^MTKTextureLoaderArrayCallback) (NSArray<id <MTLTexture>> * __nonnull textures, NSError * __nullable error) NS_AVAILABLE(10_12, 10_0);
 
 /*!
  @class MTKTextureLoader
@@ -165,55 +153,66 @@
 
 /*!
  @method newTextureWithName:scaleFactor:bundle:options:completionHandler:
- @abstract Asynchronously create a Metal texture and load image data from a given texture asset name
+ @abstract Asynchronously create a Metal texture and load image data from a given texture or image 
+           asset name
  @param names An array of texture asset names
  @param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the 
                     value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor].
  @param bundle Resource bundle in which the asset is located.  Main bundle used if nil.
- @param options Dictonary of MTKTextureLoaderOptions. This method cannot be used with the 
-                following options:
+ @param options Dictonary of MTKTextureLoaderOptions. The following options are ignormed when used
+                to load a texture asset but can be used when creating a texture from an image asset:
                     MTKTextureLoaderOptionGenerateMipmaps
                     MTKTextureLoaderOptionSRGB
                     MTKTextureLoaderOptionCubeFromVerticalTexture
                     MTKTextureLoaderOptionOrigin
  @param completionHandler Block called when texture has been loaded and fully initialized
  @discussion Uses texture data from version of the texture from the texture set in the asset catalog
-             which mathces the device's traits
+             which mathces the device's traits.
+             This method attempts to load a texture asset with thw name iven.  If a texture asset
+             with the name given does not exist, it will attempt to create a texture from a an
+             image asset with the name give if it can.
  */
 - (void)newTextureWithName:(nonnull NSString *)name
                scaleFactor:(CGFloat)scaleFactor
                     bundle:(nullable NSBundle *)bundle
                    options:(nullable NSDictionary <NSString *, NSObject *> *)options
-         completionHandler:(nonnull MTKTextureLoaderCallback)completionHandler;
-
+         completionHandler:(nonnull MTKTextureLoaderCallback)completionHandler NS_AVAILABLE(10_12, 10_0);
 
-#if TARGET_OS_MAC
 /*!
- @method newTextureWithName:scaleFactor:bundle:options:completionHandler:
- @abstract Asynchronously create a Metal texture and load image data from a given texture asset name
+ @method newTextureWithName:scaleFactor:displayGamut:bundle:options:completionHandler:
+ @abstract Asynchronously create a Metal texture and load image data from a given texture or image 
+           asset name
  @param names An array of texture asset names
  @param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
                     value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor].
- @param displayGamut Gamut of the display which the version of the texture you're requesting is
-                     associated with
+ @param displayGamut ColorSpace for the version of the texture you would like built.  This corresponds
+                     to the "Gamut" trait in xcode's asset catalog.  The app would usually
+                     obtain this by getting the colorSpace property of the NSScrean object
+                     the view is rendering on.  ( metalView.window.screen.colorSpace.CGColorSpace )
  @param bundle Resource bundle in which the asset is located.  Main bundle used if nil.
- @param options Dictonary of MTKTextureLoaderOptions. This method cannot be used with the
- following options:
+ @param options Dictonary of MTKTextureLoaderOptions. The following options are ignormed when used
+                to load a texture asset but can be used when creating a texture from an image asset:
                     MTKTextureLoaderOptionGenerateMipmaps
                     MTKTextureLoaderOptionSRGB
                     MTKTextureLoaderOptionCubeFromVerticalTexture
                     MTKTextureLoaderOptionOrigin
  @param completionHandler Block called when texture has been loaded and fully initialized
  @discussion Uses texture data from version of the texture from the texture set in the asset catalog
-             which mathces the device's traits
+             which mathces the device's traits.
+             This method attempts to load a texture asset with the name given.  If a texture asset
+             with the name given does not exist, it will attempt to create a texture from a an
+             image asset with the name give if it can.
+             This method can be used on macOS to choose between sRGB and P3 versions of a texture
+             asset depending on the gamut of the display rendered to.
  */
 - (void)newTextureWithName:(nonnull NSString *)name
                scaleFactor:(CGFloat)scaleFactor
-              displayGamut:(MTKDisplayGamut)displayGamut
+              displayGamut:(nullable CGColorSpaceRef)displayGamut
                     bundle:(nullable NSBundle *)bundle
                    options:(nullable NSDictionary <NSString *, NSObject *> *)options
-         completionHandler:(nonnull MTKTextureLoaderCallback)completionHandler;
-#endif // TARGET_OS_MAC
+         completionHandler:(nonnull MTKTextureLoaderCallback)completionHandler NS_AVAILABLE_MAC(10_12);
+
+
 /*!
  @method newTexturesWithContentsOfURLs:options:completionHandler:
  @abstract Asynchronously create an array of Metal textures and load image data from the files at URLs
@@ -227,13 +226,14 @@
 
 /*!
  @method newTexturesWithNames:scaleFactor:bundle:options:completionHandler:
- @abstract Asynchronously create Metal textures and load image data from a given texture asset names
+ @abstract Asynchronously create Metal textures and load image data from a given texture or image
+           asset names
  @param names An array of texture asset names
  @param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
                     value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor].
  @param bundle Resource bundle in which the assets are located
- @param options Dictonary of MTKTextureLoaderOptions. This method cannot be used with the
-                following options:
+ @param options Dictonary of MTKTextureLoaderOptions. The following options are ignormed when used
+                to load a texture asset but can be used when creating a texture from an image asset
                     MTKTextureLoaderOptionGenerateMipmaps
                     MTKTextureLoaderOptionSRGB
                     MTKTextureLoaderOptionCubeFromVerticalTexture
@@ -242,43 +242,54 @@
                           initialized. The NSError will be null if all of the textures are loaded
                           successfully, or will correspond to one of the textures which failed to
                           load.
-
+ @discussion Uses texture data from version of the texture from the texture set in the asset catalog
+             which mathces the device's traits.
+             This method attempts to load a texture asset with each name iven.  If a texture asset
+             with the name given does not exist, it will attempt to create a texture from a an
+             image asset with the name give if it can.
  */
 - (void)newTexturesWithNames:(nonnull NSArray<NSString *> *)names
                  scaleFactor:(CGFloat)scaleFactor
                       bundle:(nullable NSBundle *)bundle
                      options:(nullable NSDictionary <NSString *, NSObject *> *)options
-           completionHandler:(nonnull MTKTextureLoaderArrayCallback)completionHandler;
+           completionHandler:(nonnull MTKTextureLoaderArrayCallback)completionHandler NS_AVAILABLE(10_12, 10_0);
 
-#if TARGET_OS_MAC
 /*!
-@method newTexturesWithNames:scaleFactor:bundle:options:completionHandler:
-@abstract Asynchronously create Metal textures and load image data from a given texture asset names
+@method newTexturesWithNames:scaleFactor:displayGamut:bundle:options:completionHandler:
+@abstract Asynchronously create Metal textures and load image data from given texture or image
+          asset names
 @param names An array of texture asset names
 @param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
                    value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor]
-@param displayGamut Gamut of the display which the version of the texture you're requesting is
-                    associated with .
+@param displayGamut ColorSpace for the version of the texture you would like built.  This corresponds
+                    to the "Gamut" trait in xcode's asset catalog.  The app would usually
+                    obtain this by getting the colorSpace property of the NSScrean object
+                    the view is rendering on. ( metalView.window.screen.colorSpace.CGColorSpace )
 @param bundle Resource bundle in which the assets are located
-@param options Dictonary of MTKTextureLoaderOptions. This method cannot be used with the
-       following options:
-          MTKTextureLoaderOptionGenerateMipmaps
-          MTKTextureLoaderOptionSRGB
-          MTKTextureLoaderOptionCubeFromVerticalTexture
-          MTKTextureLoaderOptionOrigin
+@param options Dictonary of MTKTextureLoaderOptions. The following options are ignormed when used
+               to load a texture asset but can be used when creating a texture from an image asset
+                   MTKTextureLoaderOptionGenerateMipmaps
+                   MTKTextureLoaderOptionSRGB
+                   MTKTextureLoaderOptionCubeFromVerticalTexture
+                   MTKTextureLoaderOptionOrigin
 @param completionHandler Block called when all of the textures have been loaded and fully
-                         initialized. The NSError will be null if all of the textures are loaded
+                         initialized. The NSError will be nif if all of the textures are loaded
                          successfully, or will correspond to one of the textures which failed to
                          load.
-
+@discussion Uses texture data from version of the texture from the texture sets in the asset catalog
+            which mathces the device's traits.
+            This method attempts to load a texture asset with each name given.  If a texture asset
+            with the name given does not exist, it will attempt to create a texture from a an
+            image asset with the name give if it can.
+            This method can be used on macOS to choose between sRGB and P3 versions of a texture
+            asset depending on the gamut of the display rendered to
 */
 - (void)newTexturesWithNames:(nonnull NSArray<NSString *> *)names
                  scaleFactor:(CGFloat)scaleFactor
-                displayGamut:(MTKDisplayGamut)displayGamut
+                displayGamut:(nullable CGColorSpaceRef)displayGamut
                       bundle:(nullable NSBundle *)bundle
                      options:(nullable NSDictionary <NSString *, NSObject *> *)options
-           completionHandler:(nonnull MTKTextureLoaderArrayCallback)completionHandler;
-#endif // TARGET_OS_MAC
+           completionHandler:(nonnull MTKTextureLoaderArrayCallback)completionHandler NS_AVAILABLE_MAC(10_12);
 
 /*!
  @method newTextureWithData:options:completionHandler:
@@ -311,7 +322,7 @@
  */
 - (void)newTextureWithMDLTexture:(nonnull MDLTexture *)texture
                          options:(nullable NSDictionary <NSString *, NSObject *> *)options
-               completionHandler:(nonnull MTKTextureLoaderCallback)completionHandler;
+               completionHandler:(nonnull MTKTextureLoaderCallback)completionHandler NS_AVAILABLE(10_12, 10_0);
 
 /*!
  @method newTextureWithContentsOfURL:options:error:
@@ -335,7 +346,7 @@
  */
 - (NSArray <id <MTLTexture>> * __nonnull)newTexturesWithContentsOfURLs:(nonnull NSArray <NSURL *> *)URLs
                                                                options:(nullable NSDictionary <NSString *, NSObject *> *)options
-                                                                 error:(NSError *__nullable *__nullable)error;
+                                                                 error:(NSError *__nullable *__nullable)error NS_AVAILABLE(10_12, 10_0);
 
 /*!
  @method newTextureWithData:options:error:
@@ -371,54 +382,67 @@
  */
 - (nullable id <MTLTexture>)newTextureWithMDLTexture:(nonnull MDLTexture *)texture
                                              options:(nullable NSDictionary <NSString *, NSObject *> *)options
-                                               error:(NSError *__nullable *__nullable)error;
+                                               error:(NSError *__nullable *__nullable)error NS_AVAILABLE(10_12, 10_0);
 
 /*!
- @method newTextursWithName:bundle:options:error:
- @abstract Synchronously create a Metal texture with texture data from a given texture asset name
+ @method newTextursWithName:sca;eFactpr:bundle:options:error:
+ @abstract Synchronously create a Metal texture with texture data from a given texture or image 
+           asset name
  @return The Metal texture. nil if an error occured
  @param names An array of texture asset names
  @param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
                     value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor].
  @param bundle Resource bundle in which the asset is located
- @param options Dictonary of MTKTextureLoaderOptions. This method cannot be used with the
-                following options:
+ @param options Dictonary of MTKTextureLoaderOptions. The following options are ignormed when used
+                to load a texture asset but can be used when creating a texture from an image asset
                     MTKTextureLoaderOptionGenerateMipmaps
                     MTKTextureLoaderOptionSRGB
                     MTKTextureLoaderOptionCubeFromVerticalTexture
                     MTKTextureLoaderOptionOrigins
- @param error Pointer to an autoreleased NSError object which will be set if an error occurred
- */
+ @discussion Uses texture data from version of the texture from the texture set in the asset catalog
+             which mathces the device's traits.
+             This method attempts to load a texture asset with the name given.  If a texture asset
+             with the name given does not exist, it will attempt to create a texture from a an
+             image asset with the name give if it can.
+  */
 - (nullable id <MTLTexture>)newTextureWithName:(nonnull NSString *)name
                                    scaleFactor:(CGFloat)scaleFactor
                                         bundle:(nullable NSBundle *)bundle
                                        options:(nullable NSDictionary <NSString *, NSObject *> *)options
-                                         error:(NSError *__nullable *__nullable)error;
+                                         error:(NSError *__nullable *__nullable)error NS_AVAILABLE(10_12, 10_0);
 
-#if TARGET_OS_MAC
 /*!
- @method newTextursWithName:bundle:options:error:
- @abstract Synchronously create a Metal texture with texture data from a given texture asset name
+ @method newTextursWithName:sca;eFactpr:displayGamut:bundle:options:error:
+ @abstract Synchronously create a Metal texture with texture data from a given texture or image
+           asset name
  @return The Metal texture. nil if an error occured
  @param names An array of texture asset names
  @param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
                      value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor].
+ @param displayGamut ColorSpace for the version of the texture you would like built.  This corresponds
+                     to the "Gamut" trait in xcode's asset catalog.  The app would usually
+                     obtain this by getting the colorSpace property of the NSScrean object
+                     the view is rendering on. ( metalView.window.screen.colorSpace.CGColorSpace )
  @param bundle Resource bundle in which the asset is located
- @param options Dictonary of MTKTextureLoaderOptions. This method cannot be used with the
-                following options:
+ @param options Dictonary of MTKTextureLoaderOptions. The following options are ignormed when used
+                to load a texture asset but can be used when creating a texture from an image asset
                     MTKTextureLoaderOptionGenerateMipmaps
-                     MTKTextureLoaderOptionSRGB
-                     MTKTextureLoaderOptionCubeFromVerticalTexture
-                    MTKTextureLoaderOptionOrigins
- @param error Pointer to an autoreleased NSError object which will be set if an error occurred
+                    MTKTextureLoaderOptionSRGB
+                    MTKTextureLoaderOptionCubeFromVerticalTexture
+                    MTKTextureLoaderOptionOrigin
+ @discussion Uses texture data from version of the texture from the texture set in the asset catalog
+             which mathces the device's traits.
+             This method attempts to load a texture asset with the name given.  If a texture asset
+             with the name given does not exist, it will attempt to create a texture from a an
+             image asset with the name give if it can.
+             This method can be used on macOS to choose between sRGB and P3 versions of a texture
+             asset depending on the gamut of the display rendered to.
  */
 - (nullable id <MTLTexture>)newTextureWithName:(nonnull NSString *)name
                                    scaleFactor:(CGFloat)scaleFactor
-                                  displayGamut:(MTKDisplayGamut)displayGamut
+                                  displayGamut:(nullable CGColorSpaceRef)displayGamut
                                         bundle:(nullable NSBundle *)bundle
                                        options:(nullable NSDictionary <NSString *, NSObject *> *)options
-                                         error:(NSError *__nullable *__nullable)error;
-#endif // TARGET_OS_MAC
-
+                                         error:(NSError *__nullable *__nullable)error NS_AVAILABLE_MAC(10_12);
 
 @end
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKView.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKView.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKView.h	2016-06-25 02:25:02.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKView.h	2016-07-10 10:03:35.000000000 +0200
@@ -74,7 +74,7 @@
 
 /*!
  @property colorPixelFormat
- @abstract The pixelFormat for the drawable's texture.  This is an alias to colorPixelFormats[drawableAttachmentIndex]
+ @abstract The pixelFormat for the drawable's texture.
  */
 @property (nonatomic) MTLPixelFormat colorPixelFormat;
 
@@ -122,7 +122,7 @@
 /*!
  @property multisampleColorTexture
  @abstract A multisample color texture that will be resolved into the currentDrawable's texture
- @discussion The view will generate the multisample color buffer using the specified colorPixelFormat.  This will be nil if sampleCount is less than or equal to 1.  This is an alias to multisampleColorTextures[drawableAttachmentIndex]
+ @discussion The view will generate the multisample color buffer using the specified colorPixelFormat.  This will be nil if sampleCount is less than or equal to 1.
  */
 @property (nonatomic, readonly, nullable) id <MTLTexture> multisampleColorTexture;
 
@@ -176,6 +176,13 @@
 @property (nonatomic, getter=isPaused) BOOL paused;
 
 /*!
+ @property colorspace
+ @abstract The colorspace of the rendered frames. '
+ @discussion If nil, no colormatching occurs.  If non-nil, the rendered content will be colormatched to the colorspace of the context containing this layer (typically the display's colorspace).  This property aliases the olorspace property or the view's CAMetalLayer
+ */
+@property (nonatomic, nullable) CGColorSpaceRef colorspace NS_AVAILABLE_MAC(10_12);
+
+/*!
  @method draw
  @abstract Manually ask the view to draw new contents. This causes the view to call either the drawInMTKView (delegate) or drawRect (subclass) method.
  @discussion Manually ask the view to draw new contents. This causes the view to call either the drawInMTKView (delegate) or drawRect (subclass) method. This should be used when the view's paused proprety is set to true and enableSetNeedsDisplay is set to false.

```