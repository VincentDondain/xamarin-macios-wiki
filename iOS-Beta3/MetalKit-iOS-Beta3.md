#MetalKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKView.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKView.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKView.h	2016-06-25 02:25:02.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MetalKit.framework/Headers/MTKView.h	2016-07-10 10:03:35.000000000 +0200
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