#MetalKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKModel.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKModel.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKModel.h	2015-10-03 01:52:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKModel.h	2016-05-11 18:30:16.000000000 +0200
@@ -61,7 +61,7 @@
  @discussion Memory backing these buffer are Metal buffers.  Model I/O will load index and vertex data from from a model asset directly in to the Metal buffer.
  */
 NS_CLASS_AVAILABLE(10_11, 9_0)
-@interface MTKMeshBuffer : NSObject <MDLMeshBuffer>
+@interface MTKMeshBuffer : NSObject <MDLMeshBuffer, MDLNamed>
 
 /*!
  @method init
@@ -169,7 +169,7 @@
  @abstract Name from the original MDLSubmesh object.
  @discussion Although not directly used by this object, the application may use this to identify the submesh in the renderer/scene/world.
  */
-@property (nonatomic, nonnull) NSString *name;
+@property (nonatomic, copy, nonnull) NSString *name;
 
 @end
 
@@ -241,9 +241,9 @@
 /*!
  @property name
  @abstract Name of the mesh copies from the originating Model I/O mesh.
- @discussion Can be used by the app to identiry the mesh in its scene/world/renderer etc.
+ @discussion Can be used by the app to identify the mesh in its scene/world/renderer etc.
  */
-@property (nonatomic, nonnull) NSString *name;
+@property (nonatomic, copy, nonnull) NSString *name;
 
 @end
 
@@ -261,6 +261,13 @@
 MTK_EXTERN MDLVertexDescriptor* __nonnull MTKModelIOVertexDescriptorFromMetal(MTLVertexDescriptor* __nonnull metalDescriptor);
 
 /*!
+ @function MTKModelIOVertexDescriptorFromMetalWithError
+ @abstract Partially converts a Metal vertex descriptor to a Model I/O vertex descriptor
+ @discussion This method can only set vertex format, offset, bufferIndex, and stride information in the produced Model I/O vertex descriptor.  It does not add any semantic information such at attributes names.  Names must be set in the returned Model I/O vertex descriptor before it can be applied to a a Model I/O mesh. If error is nonnull, and the conversion cannot be made, it will be set.
+ */
+MTK_EXTERN MDLVertexDescriptor* __nonnull MTKModelIOVertexDescriptorFromMetalWithError(MTLVertexDescriptor* __nonnull metalDescriptor, NSError * __nullable * __nullable error);
+
+/*!
  @function MTKMetalVertexDescriptorFromModelIO
  @abstract Partially converts a Model I/O vertex descriptor to a Metal vertex descriptor
  @discussion This method can only set vertex format, offset, bufferIndex, and stride information in the produced Metal vertex descriptor. It simply copies attributes 1 for 1. Thus attributes in the given Model I/O vertex descriptor must be arranged in the correct order for the resulting descriptor to properly map mesh data to vertex shader inputs.  Layout stepFunction and stepRates for the resulting MTLVertexDescriptor must also be set by application.
@@ -268,6 +275,13 @@
 MTK_EXTERN MTLVertexDescriptor* __nonnull MTKMetalVertexDescriptorFromModelIO(MDLVertexDescriptor* __nonnull modelIODescriptor);
 
 /*!
+ @function MTKMetalVertexDescriptorFromModelIOWithError
+ @abstract Partially converts a Model I/O vertex descriptor to a Metal vertex descriptor
+ @discussion This method can only set vertex format, offset, bufferIndex, and stride information in the produced Metal vertex descriptor. It simply copies attributes 1 for 1. Thus attributes in the given Model I/O vertex descriptor must be arranged in the correct order for the resulting descriptor to properly map mesh data to vertex shader inputs.  Layout stepFunction and stepRates for the resulting MTLVertexDescriptor must also be set by application.  If error is nonnull, and the conversion cannot be made, it will be set.
+ */
+MTK_EXTERN MTLVertexDescriptor* __nonnull MTKMetalVertexDescriptorFromModelIOWithError(MDLVertexDescriptor* __nonnull modelIODescriptor, NSError * __nullable * __nullable error);
+
+/*!
  @function MTKModelIOVertexFormatFromMetal
  @abstract Converts a Metal vertex format to a Model I/O vertex format
  @return A Model I/O vertexformat correspoinding to the given Metal vertex format.  Returns MDLVertexFormatInvalid if no matching Model I/O vertex format exists.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h	2015-10-03 01:52:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKTextureLoader.h	2016-05-18 05:03:45.000000000 +0200
@@ -12,6 +12,7 @@
 
 @protocol MTLDevice;
 @protocol MTLTexture;
+@class MDLTexture;
 
 /*!
  @group MTKTextureLoaderErrors
@@ -26,7 +27,6 @@
  */
 MTK_EXTERN NSString * __nonnull const MTKTextureLoaderErrorKey NS_AVAILABLE(10_11, 9_0);
 
-
 /*!
  @group MTKTextureLoaderOptions
  */
@@ -34,11 +34,18 @@
 /*!
  @constant MTKTextureLoaderOptionAllocateMipmaps
  @abstract Identifier to be used in an options NSDictionary with a boolean NSNumber specifying whether to allocate memory for mipmaps when creating the texture
- @discussion If the boolean value specified with this string is true, the resulting Metal texture will have been created with mipmaps whose contents are undefined. It is the responsibility of the caller to fill out the contents of the mipmap data. However, if the file being loaded contains data for mipmaps (such as in a PVR or KTX file) this option does need to be specified. In those cases the mipmap memory will be allocated and the image data loaded.
+ @discussion If the boolean value specified with this string is true, the resulting Metal texture will have been created with mipmaps whose contents are undefined. It is the responsibility of the caller to fill out the contents of the mipmap data unless MTLTextureLoaderOptionGenerateMipmaps is specified. If the file being loaded contains data for mipmaps (such as in a PVR or KTX file) this option does not need to be specified. In those cases the mipmap memory will be allocated and the image data loaded.
  */
 MTK_EXTERN NSString * __nonnull const MTKTextureLoaderOptionAllocateMipmaps NS_AVAILABLE(10_11, 9_0);
 
 /*!
+ @constant MTKTextureLoaderOptionGenerateMipmaps
+ @abstract Identifier to be used in an options NSDictionary with a boolean NSNumber specifying whether to generate mipmaps when creating the texture
+ @discussion If the boolean value specified with this string is true, the resulting Metal texture will be created with mipmaps. If the file being loaded contains data for mipmaps (such as in a PVR or KTX file), specifying this option will overwrite the existing mipmap data in the loaded texture. This option can only be used if the pixel format of the texture is color filterable and color renderable. This option implies MTKTextureLoaderOptionAllocateMipmaps. Specifying this option will cause the MTKTextureLoader to submit work to the GPU on behalf of the caller.
+ */
+MTK_EXTERN NSString * __nonnull const MTKTextureLoaderOptionGenerateMipmaps NS_AVAILABLE(10_12, 10_0);
+
+/*!
  @constant MTKTextureLoaderOptionSRGB
  @abstract Identifier to be used in an options NSDictionary with a boolean NSNumber specifying whether to create the texture with an sRGB (gamma corrected) pixel format
  @discussion If the boolean value specified with this string is true, the texture will be created with an sRGB pixel format regardless of whether the image file specifies that the data has already been gamma corrected. Likewise, if false, the texture will be created with a non-sRGB pixel format regardless of whether the image file specifies that the data has been gamma corrected. To use the sRGB information specified in the file, do not specify this in the options dictionary.
@@ -59,8 +66,59 @@
  */
 MTK_EXTERN NSString * __nonnull const MTKTextureLoaderOptionTextureCPUCacheMode NS_AVAILABLE(10_11, 9_0);
 
+/*!
+ @constant MTKTextureLoaderOptionTextureStorageMode
+ @abstract Identifier to be used with an NSNumber specifying the MTLStorageMode
+ @discussion The resulting Metal texture will be created with the MTLStorageMode indicated by the NSNumber associated with this string. If this option is omitted, the texture will be created with the default storage mode for Metal textures: MTLStorageModeShared on iOS, and MTLStorageModeManaged on OS X. Specifying this option with MTLTextureStorageModePrivate cause the MTKTextureLoader to submit work to the GPU on behalf of the caller.
+ */
+MTK_EXTERN NSString * __nonnull const MTKTextureLoaderOptionTextureStorageMode NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ * @constant MTKTextureLoaderOptionCubeLayout
+ * @abstract Identifier to be used in an options NSDictionary with an MTKTextureLoaderCubeLayout NSString specifying whether to create a cubemap from a 2D image
+ * @discussion The NSString value specified with this string must be one option of MTKTextureLoaderCubeLayout. If this option is omitted, the texture loader will not create cubemaps from 2D textures. This option cannot be used with PVR files, KTX files, or MDLTextures, which support cube textures directly.
+ */
+MTK_EXTERN NSString * __nonnull const MTKTextureLoaderOptionCubeLayout NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ * @constant MTKTextureLoaderCubeLayoutVertical
+ * @abstract Identifier specifying that the texture loader will create a cube texture from six faces arranged vertically within a single 2D image
+ * @discussion A texture cube will be created from six faces arranged vertically within a single 2D image. The image height must be six times the image width, with faces arranged in the following order from top to bottom: +X, -X, +Y, -Y, +Z, -Z.
+ */
+MTK_EXTERN NSString * __nonnull const MTKTextureLoaderCubeLayoutVertical NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ * @constant MTKTextureLoaderOptionOrigin
+ * @abstract Identifier to be used in an options NSDictionary with an MTKTextureLoaderOrigin NSString specifying whether to flip textures vertically
+ * @discussion The NSString value specified with this string must be one option of MTKTextureLoaderOrigin. If this option is omitted, the texture loader will not flip loaded textures. This option cannot be used with block-compressed texture formats, and can only be used with 2D, 2D array, and cube map textures. Each mipmap level and slice of a texture will be flipped.
+ */
+MTK_EXTERN NSString * __nonnull const MTKTextureLoaderOptionOrigin NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @constant MTKTextureLoaderOriginTopLeft
+ @abstract Identifier specifying that the texture loader should flip textures whose origin is in the bottom-left corner
+ @discussion The texture will be flipped vertically if metadata in the file being loaded indicates that the source data starts with the bottom-left corner of the texture.
+ */
+MTK_EXTERN NSString * __nonnull const MTKTextureLoaderOriginTopLeft NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @constant MTKTextureLoaderOriginBottomLeft
+ @abstract Identifier specifying that the texture loader should flip textures whose origin is in the top-left corner
+ @discussion The texture will be flipped vertically if metadata in the file being loaded indicates that the source data starts with the top-left corner of the texture.
+ */
+MTK_EXTERN NSString * __nonnull const MTKTextureLoaderOriginBottomLeft NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @constant MTKTextureLoaderOriginFlippedVertically
+ @abstract Identifier specifying that the texture loader should always flip textures
+ @discussion The texture will be flipped vertically regardless of any metadata in the file indicating the placement of the origin in the source data
+ */
+MTK_EXTERN NSString * __nonnull const MTKTextureLoaderOriginFlippedVertically NS_AVAILABLE(10_12, 10_0);
+
 typedef void (^MTKTextureLoaderCallback) (id <MTLTexture> __nullable texture, NSError * __nullable error);
 
+typedef void (^MTKTextureLoaderArrayCallback) (NSArray<id <MTLTexture>> * __nonnull textures, NSError * __nullable error);
+
 /*!
  @class MTKTextureLoader
  @abstract Load Metal textures from files with the device specified at initialization
@@ -91,10 +149,68 @@
  @param completionHandler Block called when the texture has been loaded and fully initialized
  */
 - (void)newTextureWithContentsOfURL:(nonnull NSURL *)URL
-                            options:(nullable NSDictionary <NSString *, NSNumber *> *)options
+                            options:(nullable NSDictionary <NSString *, NSObject *> *)options
                   completionHandler:(nonnull MTKTextureLoaderCallback)completionHandler;
 
 /*!
+ @method newTextureWithName:scaleFactor:bundle:options:completionHandler:
+ @abstract Asynchronously create a Metal texture and load image data from a given texture asset name
+ @param names An array of texture asset names
+ @param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the 
+                    value retrieved from -[UIView contentScale] or  -[NSWindow backingScaleFactor].
+ @param bundle Resource bundle in which the asset is located.  Main bundle used if nil.
+ @param options Dictonary of MTKTextureLoaderOptions. This method cannot be used with the 
+                following options:
+                    MTKTextureLoaderOptionGenerateMipmaps
+                    MTKTextureLoaderOptionSRGB
+                    MTKTextureLoaderOptionCubeFromVerticalTexture
+                    MTKTextureLoaderOptionOrigin
+ @param completionHandler Block called when texture has been loaded and fully initialized
+ @discussion
+ */
+- (void)newTextureWithName:(nonnull NSString *)name
+               scaleFactor:(CGFloat)scaleFactor
+                    bundle:(nullable NSBundle *)bundle
+                   options:(nullable NSDictionary <NSString *, NSObject *> *)options
+         completionHandler:(nonnull MTKTextureLoaderCallback)completionHandler;
+
+/*!
+ @method newTexturesWithContentsOfURLs:options:completionHandler:
+ @abstract Asynchronously create an array of Metal textures and load image data from the files at URLs
+ @param URLs Locations of image files from which to create the textures
+ @param options Dictonary of MTKTextureLoaderOptions, which will be used for every texture loaded
+ @param completionHandler Block called when all of the textures have been loaded and fully initialized. The array of MTLTextures will be the same length and in the same order as the requested array of paths. If an error occurs while loading a texture, the corresponding array index will contain NSNull. The NSError will be null if all of the textures are loaded successfully, or will correspond to one of the textures which failed to load.
+ */
+- (void)newTexturesWithContentsOfURLs:(nonnull NSArray<NSURL *> *)URLs
+                              options:(nullable NSDictionary <NSString *, NSObject *> *)options
+                    completionHandler:(nonnull MTKTextureLoaderArrayCallback)completionHandler NS_AVAILABLE(10_12, 10_0);
+
+/*!
+ @method newTexturesWithNames:scaleFactor:bundle:options:completionHandler:
+ @abstract Asynchronously create Metal textures and load image data from a given texture asset names
+ @param names An array of texture asset names
+ @param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
+                    value retrieved from -[UIView contentScale] or  -[NSWindow backingScaleFactor].
+ @param bundle Resource bundle in which the assets are located
+ @param options Dictonary of MTKTextureLoaderOptions. This method cannot be used with the
+                following options:
+                    MTKTextureLoaderOptionGenerateMipmaps
+                    MTKTextureLoaderOptionSRGB
+                    MTKTextureLoaderOptionCubeFromVerticalTexture
+                    MTKTextureLoaderOptionOrigin
+ @param completionHandler Block called when all of the textures have been loaded and fully
+                          initialized. The NSError will be null if all of the textures are loaded
+                          successfully, or will correspond to one of the textures which failed to
+                          load.
+
+ */
+- (void)newTexturesWithNames:(nonnull NSArray<NSString *> *)names
+                 scaleFactor:(CGFloat)scaleFactor
+                      bundle:(nullable NSBundle *)bundle
+                     options:(nullable NSDictionary <NSString *, NSObject *> *)options
+           completionHandler:(nonnull MTKTextureLoaderArrayCallback)completionHandler;
+
+/*!
  @method newTextureWithData:options:completionHandler:
  @abstract Asynchronously create a Metal texture and load image data from the NSData object provided
  @param data NSData object containing image file data from which to create the texture
@@ -102,7 +218,7 @@
  @param completionHandler Block called when texture has been loaded and fully initialized
  */
 - (void)newTextureWithData:(nonnull NSData *)data
-                   options:(nullable NSDictionary <NSString *, NSNumber *> *)options
+                   options:(nullable NSDictionary <NSString *, NSObject *> *)options
          completionHandler:(nonnull MTKTextureLoaderCallback)completionHandler;
 
 /*!
@@ -113,10 +229,21 @@
  @param completionHandler Block called when texture has been loaded and fully initialized
  */
 - (void)newTextureWithCGImage:(nonnull CGImageRef)cgImage
-                      options:(nullable NSDictionary <NSString *, NSNumber *> *)options
+                      options:(nullable NSDictionary <NSString *, NSObject *> *)options
             completionHandler:(nonnull MTKTextureLoaderCallback)completionHandler;
 
 /*!
+ @method newTextureWithMDLTexture:options:completionHandler:
+ @abstract Asynchronously create a Metal texture and load image data from the given MDLTexture
+ @param texture MDLTexture containing image data from which to create the texture
+ @param options Dictonary of MTKTextureLoaderOptions
+ @param completionHandler Block called when texture has been loaded and fully initialized
+ */
+- (void)newTextureWithMDLTexture:(nonnull MDLTexture *)texture
+                         options:(nullable NSDictionary <NSString *, NSObject *> *)options
+               completionHandler:(nonnull MTKTextureLoaderCallback)completionHandler;
+
+/*!
  @method newTextureWithContentsOfURL:options:error:
  @abstract Synchronously create a Metal texture and load image data from the file at URL
  @return The Metal texture. nil if an error occured
@@ -125,10 +252,22 @@
  @param error Pointer to an autoreleased NSError object which will be set if an error occurred
  */
 - (nullable id <MTLTexture>)newTextureWithContentsOfURL:(nonnull NSURL *)URL
-                                                options:(nullable NSDictionary <NSString *, NSNumber *> *)options
+                                                options:(nullable NSDictionary <NSString *, NSObject *> *)options
                                                   error:(NSError *__nullable *__nullable)error;
 
 /*!
+ @method newTexturesWithContentsOfURLs:options:completionHandler:
+ @abstract Synchronously create an array of Metal textures and load image data from the files at URLs
+ @return An array of MTLTextures of the same length and in the same order as the requested array of paths. If an error occurs while loading a texture, the corresponding array index will contain NSNull.
+ @param URLs Locations of image files from which to create the textures
+ @param options Dictonary of MTKTextureLoaderOptions, which will be used for every texture loaded
+ @param error Pointer to an autoreleased NSError object which will be set if an error occurred. Will be null if all of the textures are loaded successfully, or will correspond to one of the textures which failed to load.
+ */
+- (NSArray <id <MTLTexture>> * __nonnull)newTexturesWithContentsOfURLs:(nonnull NSArray <NSURL *> *)URLs
+                                                               options:(nullable NSDictionary <NSString *, NSObject *> *)options
+                                                                 error:(NSError *__nullable *__nullable)error;
+
+/*!
  @method newTextureWithData:options:error:
  @abstract Synchronously create a Metal texture and load image data from the NSData object provided
  @return The Metal texture. nil if an error occured
@@ -137,7 +276,7 @@
  @param error Pointer to an autoreleased NSError object which will be set if an error occurred
  */
 - (nullable id <MTLTexture>)newTextureWithData:(nonnull NSData *)data
-                                       options:(nullable NSDictionary <NSString *, NSNumber *> *)options
+                                       options:(nullable NSDictionary <NSString *, NSObject *> *)options
                                          error:(NSError *__nullable *__nullable)error;
 
 /*!
@@ -149,7 +288,47 @@
  @param error Pointer to an autoreleased NSError object which will be set if an error occurred
  */
 - (nullable id <MTLTexture>)newTextureWithCGImage:(nonnull CGImageRef)cgImage
-                                          options:(nullable NSDictionary <NSString *, NSNumber *> *)options
+                                          options:(nullable NSDictionary <NSString *, NSObject *> *)options
                                             error:(NSError *__nullable *__nullable)error;
 
+/*!
+ @method newTextureWithMDLTexture:options:error:
+ @abstract Synchronously create a Metal texture and load image data from the given MDLTexture
+ @return The Metal texture. nil if an error occured
+ @param texture MDLTexture containing image data from which to create the texture
+ @param options Dictonary of MTKTextureLoaderOptions
+ @param error Pointer to an autoreleased NSError object which will be set if an error occurred
+ */
+- (nullable id <MTLTexture>)newTextureWithMDLTexture:(nonnull MDLTexture *)texture
+                                             options:(nullable NSDictionary <NSString *, NSObject *> *)options
+                                               error:(NSError *__nullable *__nullable)error;
+
+/*!
+ @method newTextursWithName:bundle:options:error:
+ @abstract Synchronously create a Metal texture with texture data from a given texture asset name
+ @return The Metal texture. nil if an error occured
+ @param names An array of texture asset names
+ @param scaleFactor scale factor of the texture to retrieve from the asset catalog.  Typically the
+                    value retrieved from -[UIView contentScale] or  -[NSWindow backingScaleFactor].
+ @param bundle Resource bundle in which the asset is located
+ @param options Dictonary of MTKTextureLoaderOptions. This method cannot be used with the
+                following options:
+                    MTKTextureLoaderOptionGenerateMipmaps
+                    MTKTextureLoaderOptionSRGB
+                    MTKTextureLoaderOptionCubeFromVerticalTexture
+                    MTKTextureLoaderOptionOrigins
+ @param error Pointer to an autoreleased NSError object which will be set if an error occurred
+ @discussion This method cannot be used with the following options:
+                 MTKTextureLoaderOptionGenerateMipmaps
+                 MTKTextureLoaderOptionSRGB
+                 MTKTextureLoaderOptionCubeFromVerticalTexture
+                 MTKTextureLoaderOptionOrigin 
+ */
+- (nullable id <MTLTexture>)newTextureWithName:(nonnull NSString *)name
+                                   scaleFactor:(CGFloat)scaleFactor
+                                        bundle:(nullable NSBundle *)bundle
+                                       options:(nullable NSDictionary <NSString *, NSObject *> *)options
+                                         error:(NSError *__nullable *__nullable)error;
+
+
 @end
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKView.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKView.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKView.h	2015-10-03 01:52:06.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKView.h	2016-05-16 05:34:06.000000000 +0200
@@ -21,7 +21,7 @@
  @abstract View for rendering metal content
  */
 NS_CLASS_AVAILABLE(10_11, 9_0)
-@interface MTKView : UIView <NSCoding>
+@interface MTKView : UIView <NSCoding,CALayerDelegate>
 
 /*!
  @method initWithFrame:device
@@ -74,7 +74,7 @@
 
 /*!
  @property colorPixelFormat
- @abstract The pixelFormat for the drawable's texture
+ @abstract The pixelFormat for the drawable's texture.  This is an alias to colorPixelFormats[drawableAttachmentIndex]
  */
 @property (nonatomic) MTLPixelFormat colorPixelFormat;
 
@@ -122,7 +122,7 @@
 /*!
  @property multisampleColorTexture
  @abstract A multisample color texture that will be resolved into the currentDrawable's texture
- @discussion The view will generate the multisample color buffer using the specified colorPixelFormat.  This will be nil if sampleCount is less than or equal to 1.
+ @discussion The view will generate the multisample color buffer using the specified colorPixelFormat.  This will be nil if sampleCount is less than or equal to 1.  This is an alias to multisampleColorTextures[drawableAttachmentIndex]
  */
 @property (nonatomic, readonly, nullable) id <MTLTexture> multisampleColorTexture;
 

```