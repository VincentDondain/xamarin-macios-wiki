#IntentsUI.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/INImage+IntentsUI.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/INImage+IntentsUI.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/INImage+IntentsUI.h	2016-06-26 09:17:38.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/INImage+IntentsUI.h	2016-07-11 07:35:18.000000000 +0200
@@ -14,12 +14,12 @@
 
 @interface INImage (IntentsUI)
 
-+ (instancetype)imageWithCGImage:(CGImageRef)imageRef;
-+ (instancetype)imageWithUIImage:(UIImage *)image;
++ (instancetype)imageWithCGImage:(CGImageRef)imageRef API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
++ (instancetype)imageWithUIImage:(UIImage *)image API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 /*!
  @abstract Returns the image size at which the image for an INIntentResponse will be displayed
  */
-+ (CGSize)imageSizeForIntentResponse:(INIntentResponse *)response;
++ (CGSize)imageSizeForIntentResponse:(INIntentResponse *)response API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 @end
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/INUIHostedViewControlling.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/INUIHostedViewControlling.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/INUIHostedViewControlling.h	2016-06-26 09:17:38.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/IntentsUI.framework/Headers/INUIHostedViewControlling.h	2016-07-11 07:35:18.000000000 +0200
@@ -12,7 +12,7 @@
 typedef NS_ENUM(NSUInteger, INUIHostedViewContext) {
     INUIHostedViewContextSiriSnippet,
     INUIHostedViewContextMapsCard,
-};
+} API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 @protocol INUIHostedViewControlling <NSObject>
 
@@ -32,7 +32,7 @@
 
 @interface NSExtensionContext (INUIHostedViewControlling)
 
-@property (nonatomic, assign, readonly) CGSize hostedViewMinimumAllowedSize;
-@property (nonatomic, assign, readonly) CGSize hostedViewMaximumAllowedSize;
+@property (nonatomic, assign, readonly) CGSize hostedViewMinimumAllowedSize API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
+@property (nonatomic, assign, readonly) CGSize hostedViewMaximumAllowedSize API_AVAILABLE(ios(10.0)) API_UNAVAILABLE(macosx);
 
 @end

```