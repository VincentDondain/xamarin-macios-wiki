#VideoToolbox.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTCompressionSession.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTCompressionSession.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTCompressionSession.h	2015-08-23 03:53:47.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTCompressionSession.h	2016-05-28 06:19:32.000000000 +0200
@@ -126,6 +126,7 @@
 		it will be necessary to copy image data.)
 	@param	compressedDataAllocator
 		An allocator for the compressed data.  Pass NULL to use the default allocator.
+ 		Note: on MacOS 10.12 and later, using a compressedDataAllocator may trigger an extra buffer copy.
 	@param	outputCallback
 		The callback to be called with compressed frames.
 		This function may be called asynchronously, on a different thread from the one that calls VTCompressionSessionEncodeFrame.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTErrors.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTErrors.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTErrors.h	2015-08-23 03:53:47.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTErrors.h	2016-05-26 02:10:10.000000000 +0200
@@ -25,7 +25,7 @@
 #else
 enum
 #endif // COREMEDIA_USE_DERIVED_ENUMS_FOR_CONSTANTS
-	{
+{
 	kVTPropertyNotSupportedErr				= -12900,
 	kVTPropertyReadOnlyErr					= -12901,
 	kVTParameterErr							= -12902,
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTPixelTransferProperties.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTPixelTransferProperties.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTPixelTransferProperties.h	2015-08-23 03:53:47.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTPixelTransferProperties.h	2016-05-28 06:19:32.000000000 +0200
@@ -17,8 +17,18 @@
 #include <CoreFoundation/CoreFoundation.h>
 
 #ifndef VT_SUPPORT_COLORSYNC_PIXEL_TRANSFER
-#define VT_SUPPORT_COLORSYNC_PIXEL_TRANSFER ( TARGET_OS_MAC && ! TARGET_OS_IPHONE && ( MAC_OS_X_VERSION_MIN_REQUIRED >= 1080 ) )
-#endif // VT_SUPPORT_COLORSYNC_PIXEL_TRANSFER
+#if TARGET_OS_TV
+#define VT_SUPPORT_COLORSYNC_PIXEL_TRANSFER (__TV_OS_VERSION_MIN_REQUIRED >= 93000)
+#elif TARGET_OS_WATCH
+#define VT_SUPPORT_COLORSYNC_PIXEL_TRANSFER 0
+#elif TARGET_OS_IPHONE
+#define VT_SUPPORT_COLORSYNC_PIXEL_TRANSFER (__IPHONE_OS_VERSION_MIN_REQUIRED >= 93000)
+#elif TARGET_OS_MAC
+#define VT_SUPPORT_COLORSYNC_PIXEL_TRANSFER (__MAC_OS_X_VERSION_MIN_REQUIRED >= 1080)
+#else
+#define VT_SUPPORT_COLORSYNC_PIXEL_TRANSFER 0
+#endif
+#endif
 
 #if defined(__cplusplus)
 extern "C"
@@ -135,8 +145,6 @@
 
 // Properties for color information
 
-#if VT_SUPPORT_COLORSYNC_PIXEL_TRANSFER
-
 /*!
 	@constant	kVTPixelTransferPropertyKey_DestinationColorPrimaries
 	@abstract
@@ -158,7 +166,7 @@
 		the destination.
 */
 VT_EXPORT const CFStringRef kVTPixelTransferPropertyKey_DestinationTransferFunction __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_9_0); // Read/write, CFString (see kCMFormatDescriptionExtension_TransferFunction), Optional
-
+	
 /*!
 	@constant	kVTPixelTransferPropertyKey_DestinationICCProfile
 	@abstract
@@ -169,8 +177,6 @@
 		the destination.
 */
 VT_EXPORT const CFStringRef kVTPixelTransferPropertyKey_DestinationICCProfile __OSX_AVAILABLE_STARTING(__MAC_10_8,__IPHONE_9_0); // Read/write, CFData (see kCMFormatDescriptionExtension_ICCProfile), Optional
-
-#endif // VT_SUPPORT_COLORSYNC_PIXEL_TRANSFER
     
 /*!
 	@constant	kVTPixelTransferPropertyKey_DestinationYCbCrMatrix
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTProfessionalVideoWorkflow.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTProfessionalVideoWorkflow.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTProfessionalVideoWorkflow.h	2015-08-23 03:53:47.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VTProfessionalVideoWorkflow.h	2016-05-26 02:10:10.000000000 +0200
@@ -3,7 +3,7 @@
  
 	Framework:  VideoToolbox
  
-	Copyright � 2013-2014 Apple Inc. All rights reserved.
+	Copyright © 2013-2014 Apple Inc. All rights reserved.
  
 */
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VideoToolbox.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VideoToolbox.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VideoToolbox.h	2015-08-23 03:53:47.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/VideoToolbox.framework/Headers/VideoToolbox.h	2016-05-26 02:10:08.000000000 +0200
@@ -13,8 +13,8 @@
 #include <VideoToolbox/VTMultiPassStorage.h>
 #include <VideoToolbox/VTVideoEncoderList.h>
 #include <VideoToolbox/VTUtilities.h>
-#if !TARGET_OS_IPHONE
 #include <VideoToolbox/VTPixelTransferProperties.h>
+#if !TARGET_OS_IPHONE
 #include <VideoToolbox/VTPixelTransferSession.h>
 #include <VideoToolbox/VTProfessionalVideoWorkflow.h>
 #endif // !TARGET_OS_IPHONE

```