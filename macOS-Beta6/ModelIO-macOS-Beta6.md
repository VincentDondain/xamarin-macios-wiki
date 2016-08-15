#ModelIO.framework

``` diff
diff -ruN /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLAsset.h /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLAsset.h
--- /Applications/Xcode8-beta5.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLAsset.h	2016-08-13 19:40:35.000000000 +0200
+++ /Applications/Xcode8-beta6.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/ModelIO.framework/Headers/MDLAsset.h	2016-08-03 04:17:27.000000000 +0200
@@ -87,6 +87,7 @@
  @abstract Initialize an empty MDLAsset with a buffer allocator to be used during
            other operations.
  */
+- (instancetype)initWithBufferAllocator:(nullable id<MDLMeshBufferAllocator>)bufferAllocator;
 
 /*! 
  @method initWithURL:vertexDescriptor:bufferAllocator:preserveTopology:error:

```