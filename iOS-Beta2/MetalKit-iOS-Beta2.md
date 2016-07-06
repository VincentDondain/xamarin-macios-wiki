#MetalKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h	2016-05-18 05:03:45.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h	2016-06-25 02:25:02.000000000 +0200
@@ -14,6 +14,17 @@
 @protocol MTLTexture;
 @class MDLTexture;
 
+
+/*!
+ @enum MTKDisplayGamut
+ @abstract DisplayGamut assocated with a version of a texture from a texture set.
+ */
+typedef NS_ENUM(NSUInteger, MTKDisplayGamut)
+{
+    MTKDisplayGamutSRGB = 0,
+    MTKDisplayGamutDisplayP3 = 1,
+};
+
 /*!
  @group MTKTextureLoaderErrors
  */
@@ -174,6 +186,34 @@
                    options:(nullable NSDictionary <NSString *, NSObject *> *)options
          completionHandler:(nonnull MTKTextureLoaderCallback)completionHandler;
 
+
+#if TARGET_OS_MAC
+/*!
+ @method newTextureWithName:scaleFactor:bundle:options:completionHandler:
+ @abstract Asynchronously create a Metal texture and load image data from a given texture asset name
+ @param names An array of texture asset names
+ @param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
+                    value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor].
+ @param displayGamut Gamut of the display which the version of the texture you're requesting is
+                     associated with
+ @param bundle Resource bundle in which the asset is located.  Main bundle used if nil.
+ @param options Dictonary of MTKTextureLoaderOptions. This method cannot be used with the
+ following options:
+                    MTKTextureLoaderOptionGenerateMipmaps
+                    MTKTextureLoaderOptionSRGB
+                    MTKTextureLoaderOptionCubeFromVerticalTexture
+                    MTKTextureLoaderOptionOrigin
+ @param completionHandler Block called when texture has been loaded and fully initialized
+ @discussion Uses texture data from version of the texture from the texture set in the asset catalog
+             which mathces the device's traits
+ */
+- (void)newTextureWithName:(nonnull NSString *)name
+               scaleFactor:(CGFloat)scaleFactor
+              displayGamut:(MTKDisplayGamut)displayGamut
+                    bundle:(nullable NSBundle *)bundle
+                   options:(nullable NSDictionary <NSString *, NSObject *> *)options
+         completionHandler:(nonnull MTKTextureLoaderCallback)completionHandler;
+#endif // TARGET_OS_MAC
 /*!
  @method newTexturesWithContentsOfURLs:options:completionHandler:
  @abstract Asynchronously create an array of Metal textures and load image data from the files at URLs
@@ -190,7 +230,7 @@
  @abstract Asynchronously create Metal textures and load image data from a given texture asset names
  @param names An array of texture asset names
  @param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
-                    value retrieved from -[UIView contentScale] or  -[NSWindow backingScaleFactor].
+                    value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor].
  @param bundle Resource bundle in which the assets are located
  @param options Dictonary of MTKTextureLoaderOptions. This method cannot be used with the
                 following options:
@@ -210,6 +250,36 @@
                      options:(nullable NSDictionary <NSString *, NSObject *> *)options
            completionHandler:(nonnull MTKTextureLoaderArrayCallback)completionHandler;
 
+#if TARGET_OS_MAC
+/*!
+@method newTexturesWithNames:scaleFactor:bundle:options:completionHandler:
+@abstract Asynchronously create Metal textures and load image data from a given texture asset names
+@param names An array of texture asset names
+@param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
+                   value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor]
+@param displayGamut Gamut of the display which the version of the texture you're requesting is
+                    associated with .
+@param bundle Resource bundle in which the assets are located
+@param options Dictonary of MTKTextureLoaderOptions. This method cannot be used with the
+       following options:
+          MTKTextureLoaderOptionGenerateMipmaps
+          MTKTextureLoaderOptionSRGB
+          MTKTextureLoaderOptionCubeFromVerticalTexture
+          MTKTextureLoaderOptionOrigin
+@param completionHandler Block called when all of the textures have been loaded and fully
+                         initialized. The NSError will be null if all of the textures are loaded
+                         successfully, or will correspond to one of the textures which failed to
+                         load.
+
+*/
+- (void)newTexturesWithNames:(nonnull NSArray<NSString *> *)names
+                 scaleFactor:(CGFloat)scaleFactor
+                displayGamut:(MTKDisplayGamut)displayGamut
+                      bundle:(nullable NSBundle *)bundle
+                     options:(nullable NSDictionary <NSString *, NSObject *> *)options
+           completionHandler:(nonnull MTKTextureLoaderArrayCallback)completionHandler;
+#endif // TARGET_OS_MAC
+
 /*!
  @method newTextureWithData:options:completionHandler:
  @abstract Asynchronously create a Metal texture and load image data from the NSData object provided
@@ -330,5 +395,30 @@
                                        options:(nullable NSDictionary <NSString *, NSObject *> *)options
                                          error:(NSError *__nullable *__nullable)error;
 
+#if TARGET_OS_MAC
+/*!
+ @method newTextursWithName:bundle:options:error:
+ @abstract Synchronously create a Metal texture with texture data from a given texture asset name
+ @return The Metal texture. nil if an error occured
+ @param names An array of texture asset names
+ @param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
+                     value retrieved from -[UIView contentScale] or -[NSWindow backingScaleFactor].
+ @param bundle Resource bundle in which the asset is located
+ @param options Dictonary of MTKTextureLoaderOptions. This method cannot be used with the
+                following options:
+                    MTKTextureLoaderOptionGenerateMipmaps
+                     MTKTextureLoaderOptionSRGB
+                     MTKTextureLoaderOptionCubeFromVerticalTexture
+                    MTKTextureLoaderOptionOrigins
+ @param error Pointer to an autoreleased NSError object which will be set if an error occurred
+ */
+- (nullable id <MTLTexture>)newTextureWithName:(nonnull NSString *)name
+                                   scaleFactor:(CGFloat)scaleFactor
+                                  displayGamut:(MTKDisplayGamut)displayGamut
+                                        bundle:(nullable NSBundle *)bundle
+                                       options:(nullable NSDictionary <NSString *, NSObject *> *)options
+                                         error:(NSError *__nullable *__nullable)error;
+#endif // TARGET_OS_MAC
+
 
 @end

```