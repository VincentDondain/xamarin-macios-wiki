#ModelIO.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLAsset.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLAsset.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLAsset.h	2016-05-16 07:44:17.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLAsset.h	2016-06-26 08:24:46.000000000 +0200
@@ -117,7 +115,7 @@
  @abstract Export an asset to the specified URL.
  @return YES is returned if exporting proceeded successfully,
  */
-- (BOOL)exportAssetToURL:(NSURL *)URL;
+- (BOOL)exportAssetToURL:(NSURL *)URL NS_SWIFT_UNAVAILABLE("Use exportAssetToURL:error");
 
 /*!
  @method exportAssetToURL:error:
@@ -247,6 +245,15 @@
  */
 - (MDLObject *)objectAtIndex:(NSUInteger)index;
 
+/*!
+ @property masters
+ @abstract Master objects that can be instanced into the asset's object hierarchy
+ 
+ @see MDLObjectContainerComponent
+ */
+@property (nonatomic, retain) id<MDLObjectContainerComponent> masters;
+
+
 @end
 
 @protocol MDLLightProbeIrradianceDataSource <NSObject>
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLLight.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLLight.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLLight.h	2016-05-18 04:40:09.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLLight.h	2016-06-26 09:18:51.000000000 +0200
@@ -36,11 +36,14 @@
 
 /** A utility function that returns the irradiance from the light at a given point.
     @discussion point is world space
+    @property colorSpace name, as defined in CGColorSpace.h. Default is 
+              kCGColorSpaceSRGB
   */
 - (CGColorRef)irradianceAtPoint:(vector_float3)point;
 - (CGColorRef)irradianceAtPoint:(vector_float3)point colorSpace:(CGColorSpaceRef)colorSpace;
 
 @property (nonatomic, readwrite) MDLLightType lightType;
+@property (nonatomic, copy, readwrite) NSString *colorSpace;
 
 @end
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMesh.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMesh.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMesh.h	2016-05-16 07:44:17.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLMesh.h	2016-06-26 08:32:34.000000000 +0200
@@ -18,16 +18,18 @@
  @class MDLVertexAttributeData
  @abstract convenience object to quickly access vertex attribute data
  @discussion created by MDLMesh's vertexAttributeData selector
+             Setting values on this object has no effect on the
+             underlying objects.
  */
 
 NS_CLASS_AVAILABLE(10_11, 9_0)
 MDL_EXPORT
 @interface MDLVertexAttributeData : NSObject
 
-@property (nonatomic, retain, readonly) MDLMeshBufferMap *map;
-@property (nonatomic, readonly) void *dataStart;
-@property (nonatomic, readonly) NSUInteger stride;
-@property (nonatomic, readonly) MDLVertexFormat format;
+@property (nonatomic, retain) MDLMeshBufferMap *map;
+@property (nonatomic) void *dataStart;
+@property (nonatomic) NSUInteger stride;
+@property (nonatomic) MDLVertexFormat format;
 
 @end
 
@@ -195,6 +195,29 @@
                      stride:(NSInteger)stride;
 
 /*!
+ @method addAttributeWithName:format:type:data:stride:time
+ @abstract Create a new vertex attribute including an associated buffer with
+           a copy of the supplied data, and update the vertex descriptor accordingly
+ @param name The name the attribute can be found by
+ @param format Format of the data, such as MDLVertexFormatFloat3
+ @param type The usage of the attribute, such as MDLVertexAttributePosition
+ @param data Object containing the data to be used in the new vertex buffer
+ @param stride The increment in bytes from the start of one data entry to
+        the next.
+ @param time The time the attribute is to be invoked at.
+ @discussion Adding an attribute, such as position data, at multiple times will
+             result in attributes being created for each of those times.
+             Attributes corresponding to multiple times can be retrieved from
+             the vertex descriptor.
+ */
+-(void)addAttributeWithName:(NSString *)name
+                     format:(MDLVertexFormat)format
+                       type:(NSString *)type
+                       data:(NSData *)data
+                     stride:(NSInteger)stride
+                       time:(NSTimeInterval)time;
+
+/*!
  @method addNormalsWithAttributeNamed:creaseThreshold:
  @abstract Calculate and add vertex normal data
  @param attributeName Name of vertex normal attribute.  If nil, vertex normals
@@ -216,7 +239,7 @@
  @method addTangentBasisForTextureCoordinateAttributeNamed:tangentAttributeNamed:bitangentAttributeNamed
  @abstract Create tangent basis data
  @param textureCoordinateAttributeName texture coordinates to use in calculations
- @param tangentAttributeName Name of vertex tangent attribute.
+ @param tangentAttributeNamed Name of vertex tangent attribute.
  @param bitangentAttributeNamed Name of vertex bitangent attribute.
  @discussion Uses the attribute named MDLVertexAttributePosition and
              textureCoordinateAttributeName to calculate tangent and bitangent
@@ -224,7 +247,7 @@
              the new attributes if necessary.
  */
 - (void)addTangentBasisForTextureCoordinateAttributeNamed:(NSString*)textureCoordinateAttributeName
-                                    tangentAttributeNamed:(NSString *)tangentAttributeName
+                                    tangentAttributeNamed:(NSString *)tangentAttributeNamed
                                   bitangentAttributeNamed:(nullable NSString *)bitangentAttributeName;
 
 /*!
@@ -241,8 +264,8 @@
              tangent by B = (N x T) * T.w
  */
 - (void)addTangentBasisForTextureCoordinateAttributeNamed:(NSString*)textureCoordinateAttributeName
-                                     normalAttributeNamed:(NSString*)normalAttributeName
-                                    tangentAttributeNamed:(NSString *)tangentAttributeName;
+                                     normalAttributeNamed:(NSString*)normalAttributeNamed
+                                    tangentAttributeNamed:(NSString *)tangentAttributeNamed;
 
 /*!
  @method addTextureCoordinatesForAttributeNamed:textureCoordinateAttributeName
@@ -496,7 +500,7 @@
                                 allocator:(nullable id<MDLMeshBufferAllocator>)allocator;
 
 /*!
- @method newSubdividedMesh:subdivisionLevels:allocator:
+ @method initMeshBySubdividingMesh:submeshIndex:subdivisionLevels:allocator
  @abstract Factory method that generates a subdivided mesh from a source mesh
  @param mesh Mesh from which to generate a subdivided mesh
  @param submeshIndex Index of submesh in Mesh's submesh array from which to
@@ -555,20 +559,6 @@
 
 @end
 
-/*!
- @interface MDLAnimationRig
- @abstract Animation control rig for use when vertex attributes of joint indices
-           and weights exist.
- */
-
-@interface MDLMesh (MDLAnimationRig)
-
-@property (readonly, nonatomic) NSUInteger controlNodeCount;
-- (MDLObject *) controlNodeForIndex:(NSUInteger)index;
-- (matrix_float4x4) inverseBasePoseForIndex:(NSUInteger)index;
-
-@end
-
 
 @interface MDLMesh (MDLLightBaking)
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLObject.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLObject.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLObject.h	2016-05-16 08:40:26.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLObject.h	2016-06-26 08:32:34.000000000 +0200
@@ -46,6 +46,21 @@
 @property (nonatomic, weak, nullable) MDLObject* parent;
 
 /*!
+ @property instance
+ @abstract Instance object
+ @discussion nil, unless this object refers to master data to be instanced. The
+             master data object can be any MDLObject that does not have a parent.
+             If an MDLAsset has been created from a data file, any master objects
+             parsed from that file will be found in the masters property.
+             A typical use of a master and instance might be to have one master
+             chair MDLObject, and instance six chairs around a table. The
+             transform of each chair would be found on the parent MDLObject, but
+             the various items making up the chair would be found in the master
+             object.
+ */
+@property (nonatomic, nullable, retain) MDLObject* instance;
+
+/*!
  @property path
  @abstract a string representing a path to the object
  @discussion a path is of the form /path/to/object where the path is formed by
@@ -57,14 +72,14 @@
 @property (nonatomic, readonly) NSString* path;
 
 /*!
+ @abstract Return the object at the specified path, or nil if none exists there
+ */
+- (MDLObject*)objectAtPath:(NSString*)path;
+
+/*!
  @property transform
  @abstract Short hand property for the MDLTransformComponent.
- @discussion 
- 
- The default value is nil
-
- Getter is equivalent to "-[componentConformingToProtocol:@protocol(MDLTransformComponent)]"
- Setter is equivalent to "-[setComponent:forProtocol:@protocol(MDLTransformComponent)]"
+ @discussion The default value is nil
  
  @see MDLTransformComponent
  */
@@ -73,17 +88,21 @@
 /*!
  @property children
  @abstract Short hand property for the MDLObjectContainerComponent.
- @discussion
-  The default value is nil
- 
- Getter is equivalent to "-[componentConformingToProtocol:@protocol(MDLObjectContainerComponent)]"
- Setter is equivalent to "-[setComponent:forProtocol:@protocol(MDLObjectContainerComponent)]"
+ @discussion The default value is nil
  
  @see MDLObjectContainerComponent
  */
 @property (nonatomic, retain) id<MDLObjectContainerComponent> children;
 
 /*!
+ @property hidden
+ @abstract Visibility of the node
+ @discussion default is NO
+ */
+
+@property (nonatomic) BOOL hidden;
+
+/*!
  @method addChild:
  @abstract Short hand for adding a child to the current container component and 
            setting the parent to this object.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTexture.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTexture.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTexture.h	2016-05-16 05:38:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTexture.h	2016-06-26 08:21:25.000000000 +0200
@@ -99,7 +99,8 @@
     orientation and demosaiced in all other instances.
  */
 + (nullable instancetype)textureCubeWithImagesNamed:(NSArray<NSString *> *)names;
-+ (nullable instancetype)textureCubeWithImagesNamed:(NSArray<NSString *> *)names bundle:(nullable NSBundle*)bundleOrNil;
++ (nullable instancetype)textureCubeWithImagesNamed:(NSArray<NSString *> *)names
+                                             bundle:(nullable NSBundle*)bundleOrNil;
 
 + (instancetype)irradianceTextureCubeWithTexture:(MDLTexture*)texture
                                             name:(nullable NSString*)name
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTypes.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTypes.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTypes.h	2016-05-16 08:40:26.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLTypes.h	2016-06-26 09:39:44.000000000 +0200
@@ -28,9 +28,6 @@
 /* Universal Scene Description file format, file extension USDA or USDB, UTI com.pixar.universal-scene-description */
 MDL_EXPORT NSString * __nonnull const kUTTypeUniversalSceneDescription NS_AVAILABLE(10_12, 10_0);
 
-/* MDLTexture can export OpenEXR files. The correct file format extension is EXR, and
-   the UTI is com.ilm.openexr-image */
-
 NS_ASSUME_NONNULL_BEGIN
 typedef NS_ENUM(NSUInteger, MDLIndexBitDepth)
 {
@@ -49,12 +46,7 @@
     MDLGeometryTypeTriangles,
     MDLGeometryTypeTriangleStrips,
     MDLGeometryTypeQuads,
-    MDLGeometryTypeVariableTopology,
-    MDLGeometryKindPoints = 0,        // Legacy enumerations
-    MDLGeometryKindLines,
-    MDLGeometryKindTriangles,
-    MDLGeometryKindTriangleStrips,
-    MDLGeometryKindQuads
+    MDLGeometryTypeVariableTopology
 };
 
 typedef NS_ENUM(NSInteger, MDLProbePlacement) {
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVertexDescriptor.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVertexDescriptor.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVertexDescriptor.h	2016-05-16 05:38:40.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLVertexDescriptor.h	2016-06-26 09:39:44.000000000 +0200
@@ -171,6 +171,8 @@
 MDL_EXPORT
 @interface MDLVertexBufferLayout : NSObject <NSCopying>
 
+- (instancetype) initWithStride:(NSUInteger) stride;
+
 /*!
  @property stride
  @abstract stride in bytes of each vertex element of in the buffer
@@ -228,6 +230,13 @@
 @property (nonatomic, readwrite) NSUInteger bufferIndex;
 
 /*!
+ @property time
+ @abstract the time the attribute is intended for.
+ @discussion morph targets would store their times here
+ */
+@property (nonatomic, readwrite) NSTimeInterval time;
+
+/*!
  @property initializationValue
  @abstract Value to initialize the attribute to in the vertex buffer if no values
  @discussion This values of this vector will be set in attribute in the vertex

```