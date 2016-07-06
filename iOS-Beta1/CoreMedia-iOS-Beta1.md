#CoreMedia.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMBase.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMBase.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMBase.h	2016-03-02 05:50:24.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMBase.h	2016-05-28 06:19:48.000000000 +0200
@@ -14,6 +14,16 @@
 #include <Availability.h>
 #include <AvailabilityMacros.h>
 
+// Pre-10.12, weak import
+#ifndef __AVAILABILITY_INTERNAL__MAC_10_12
+#define __AVAILABILITY_INTERNAL__MAC_10_12 __AVAILABILITY_INTERNAL_WEAK_IMPORT
+#endif
+
+// Pre- iOS 10.0, weak import
+#ifndef __AVAILABILITY_INTERNAL__IPHONE_10_0
+#define __AVAILABILITY_INTERNAL__IPHONE_10_0 __AVAILABILITY_INTERNAL_WEAK_IMPORT
+#endif
+
 // Pre-10.11.3, weak import
 #ifndef __AVAILABILITY_INTERNAL__MAC_10_11_3
 #define __AVAILABILITY_INTERNAL__MAC_10_11_3 __AVAILABILITY_INTERNAL_WEAK_IMPORT
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMBlockBuffer.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMBlockBuffer.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMBlockBuffer.h	2015-10-03 00:33:56.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMBlockBuffer.h	2016-05-26 02:09:24.000000000 +0200
@@ -48,7 +48,7 @@
 				from the CFAllocator provided for CMBlockBuffer construction.
 	@constant	kCMBlockBufferBlockAllocationFailedErr Returned when the allocator provided to allocate a memory block
 				(as distinct from CMBlockBuffer structures) fails.
-	@constant	kCMBlockBufferBadCustomBlockSourceErr The custom block source�s Allocate() routine was NULL when an allocation was attempted.
+	@constant	kCMBlockBufferBadCustomBlockSourceErr The custom block source’s Allocate() routine was NULL when an allocation was attempted.
 	@constant	kCMBlockBufferBadOffsetParameterErr The offset provided to an API is out of the range of the relevent CMBlockBuffer.
 	@constant	kCMBlockBufferBadLengthParameterErr The length provided to an API is out of the range of the relevent CMBlockBuffer,
 				or is not allowed to be zero.
@@ -536,7 +536,7 @@
 	@param	theBuffer		CMBlockBuffer to examine. Must not be NULL
 	@param	offset			Offset within the buffer's offset range.
 	@param	length			Desired number of bytes to access at offset. If zero, the number of bytes available at offset
-							(dataLength � offset), contiguous or not, is used.
+							(dataLength – offset), contiguous or not, is used.
 							
 	@result	Returns true if the specified range is contiguous within the CMBlockBuffer, false otherwise. Also returns false if the
 			CMBlockBuffer is NULL or empty.
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMBufferQueue.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMBufferQueue.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMBufferQueue.h	2016-02-26 05:39:31.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMBufferQueue.h	2016-05-28 06:38:48.000000000 +0200
@@ -464,7 +464,7 @@
 
 /*!
 	@function	CMBufferQueueGetFirstPresentationTimeStamp
-	@abstract	Gets the decode timestamp of the first buffer in a CMBufferQueue.
+	@abstract	Gets the presentation timestamp of the first buffer in a CMBufferQueue.
 	@discussion	This API is is a faster alternative to GetMinPresentationTimeStamp,
 				but only works if you know your queue is sorted by presentation
 				timestamp. If the getPresentationTimeStamp callback is NULL,
@@ -614,7 +614,7 @@
 															Must be numeric (ie. not invalid, indefinite, or infinite),
 															except for certain trigger conditions which ignore it
 															(eg, kCMBufferQueueTrigger_WhenMinPresentationTimeStampChanges). */
-	CMBufferQueueTriggerToken CM_NULLABLE * CM_NONNULL triggerTokenOut )	/*! @param triggerTokenOut
+	CMBufferQueueTriggerToken CM_NULLABLE * CM_NULLABLE triggerTokenOut )	/*! @param triggerTokenOut
 															Address where created trigger token will be written.
 															Can be NULL, if client has no need to explicitly test
 															or remove the trigger. Cannot be NULL if triggerCallback
@@ -644,7 +644,7 @@
 																				Must be a valid condition for an integer threshold. */
 	CMItemCount triggerThreshold,											/*! @param triggerThreshold
 																				The integer value to compare against when evaluating the trigger. */
-	CMBufferQueueTriggerToken CM_NULLABLE * CM_NONNULL triggerTokenOut )	/*! @param triggerTokenOut
+	CMBufferQueueTriggerToken CM_NULLABLE * CM_NULLABLE triggerTokenOut )	/*! @param triggerTokenOut
 																				Address where created trigger token will be written.
 																				Can be NULL, if client has no need to explicitly test
 																				or remove the trigger. Cannot be NULL if triggerCallback
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMFormatDescription.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMFormatDescription.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMFormatDescription.h	2016-03-02 05:50:27.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMFormatDescription.h	2016-05-28 06:38:48.000000000 +0200
@@ -87,7 +87,7 @@
 	kCMMediaType_ClosedCaption		= 'clcp',
 	kCMMediaType_Subtitle			= 'sbtl',
 	kCMMediaType_TimeCode			= 'tmcd',
-	kCMMediaType_Metadata			= 'meta'
+	kCMMediaType_Metadata			= 'meta',
 };
 
 /*! 
@@ -658,6 +658,7 @@
 #define kCMFormatDescriptionKey_CleanApertureVerticalOffset		kCVImageBufferCleanApertureVerticalOffsetKey	// CFNumber
 
 // These additional keys are used to record the precise numerator and denominator in cases where the number is not an integer.
+// NOTE: Some modules only read the float-valued keys, so if you set any of the ...Rational keys, you should also set the corresponding floating-point keys.
 CM_EXPORT const CFStringRef kCMFormatDescriptionKey_CleanApertureWidthRational									// CFArray of 2 CFNumbers: numerator, denominator
 							__OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0);
 CM_EXPORT const CFStringRef kCMFormatDescriptionKey_CleanApertureHeightRational									// CFArray of 2 CFNumbers: numerator, denominator
@@ -715,6 +716,8 @@
 #define kCMFormatDescriptionTransferFunction_UseGamma			kCVImageBufferTransferFunction_UseGamma			// CFString
 CM_EXPORT const CFStringRef kCMFormatDescriptionTransferFunction_ITU_R_2020										// same as kCVImageBufferTransferFunction_ITU_R_2020
 							__OSX_AVAILABLE_STARTING(__MAC_10_11,__IPHONE_9_0);
+CM_EXPORT const CFStringRef kCMFormatDescriptionTransferFunction_SMPTE_ST_428_1									// same as kCVImageBufferTransferFunction_SMPTE_ST_428_1
+							__OSX_AVAILABLE_STARTING(__MAC_10_12,__IPHONE_10_0);
 
 CM_EXPORT const CFStringRef kCMFormatDescriptionExtension_GammaLevel __OSX_AVAILABLE_STARTING(__MAC_10_11,__IPHONE_9_0);
 #define kCMFormatDescriptionExtension_GammaLevel				kCVImageBufferGammaLevelKey						// CFNumber describing the gamma level, used in absence of (or ignorance of) kCMFormatDescriptionExtension_TransferFunction
@@ -963,12 +966,12 @@
 CGRect CMVideoFormatDescriptionGetCleanAperture( 
 		CMVideoFormatDescriptionRef CM_NONNULL videoDesc,		/*! @param videoDesc
 																	FormatDescription being interrogated. */
-		Boolean originIsAtTopLeft )								/*! @param�originIsAtTopLeft
+		Boolean originIsAtTopLeft )								/*! @param originIsAtTopLeft
 																	Pass true if the CGRect will be used in an environment
 																	where (0,0) is at the top-left corner of an enclosing rectangle
 																	and y coordinates increase as you go down.
-																	Pass false if the CGRect will be used in�an environment 
-																	where (0,0) is at the bottom-left corner of an enclosing rectangle�
+																	Pass false if the CGRect will be used in an environment 
+																	where (0,0) is at the bottom-left corner of an enclosing rectangle 
 																	and y coordinates increase as you go up. */
 							__OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0);
 
@@ -1138,7 +1141,7 @@
 #endif
 {
     kCMTextFormatType_QTText           = 'text',
-    kCMTextFormatType_3GText           = 'tx3g'
+    kCMTextFormatType_3GText           = 'tx3g',
 };
 
 /*!
@@ -1301,14 +1304,14 @@
 OSStatus CMTextFormatDescriptionGetDefaultTextBox(
 	CMFormatDescriptionRef CM_NONNULL desc,		/*! @param desc
 													FormatDescription being interrogated. */
-	Boolean originIsAtTopLeft,					/*! @param�originIsAtTopLeft
+	Boolean originIsAtTopLeft,					/*! @param originIsAtTopLeft
 													Pass true if the CGRect will be used in an environment
 													where (0,0) is at the top-left corner of an enclosing rectangle
 													and y coordinates increase as you go down.
-													Pass false if the CGRect will be used in�an environment
+													Pass false if the CGRect will be used in an environment
 													where (0,0) is at the bottom-left corner of an enclosing rectangle
 													and y coordinates increase as you go up. */
-	CGFloat heightOfTextTrack,					/*! @param�heightOfTextTrack
+	CGFloat heightOfTextTrack,					/*! @param heightOfTextTrack
 													If originIsAtTopLeft is false, pass the height of the enclosing text track or destination.
 													This value will be used to properly compute the default text box for the given origin.
 													Ignored if originIsAtTopLeft is true. */
@@ -1550,6 +1553,8 @@
 							__OSX_AVAILABLE_STARTING(__MAC_10_10,__IPHONE_8_0);
 	CM_EXPORT const CFStringRef kCMMetadataFormatDescriptionKey_StructuralDependency	// CFDictionary
 							__OSX_AVAILABLE_STARTING(__MAC_10_11,__IPHONE_9_0);
+	CM_EXPORT const CFStringRef kCMMetadataFormatDescriptionKey_SetupData	// CFData
+							__OSX_AVAILABLE_STARTING(__MAC_10_11,__IPHONE_9_0);
 
 CM_EXPORT const CFStringRef kCMMetadataFormatDescription_StructuralDependencyKey_DependencyIsInvalidFlag	// CFBoolean
 							__OSX_AVAILABLE_STARTING(__MAC_10_11,__IPHONE_9_0);
@@ -1562,6 +1567,8 @@
 							__OSX_AVAILABLE_STARTING(__MAC_10_10,__IPHONE_8_0);
 CM_EXPORT const CFStringRef kCMMetadataFormatDescriptionMetadataSpecificationKey_StructuralDependency	// CFDictionary
 							__OSX_AVAILABLE_STARTING(__MAC_10_11,__IPHONE_9_0);
+CM_EXPORT const CFStringRef kCMMetadataFormatDescriptionMetadataSpecificationKey_SetupData				// CFData
+							__OSX_AVAILABLE_STARTING(__MAC_10_11,__IPHONE_9_0);
 
 CM_ASSUME_NONNULL_END
 CF_IMPLICIT_BRIDGING_DISABLED
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMTime.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMTime.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMTime.h	2015-10-03 00:33:57.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CoreMedia.framework/Headers/CMTime.h	2016-05-28 06:17:14.000000000 +0200
@@ -3,7 +3,7 @@
 	
 	Framework:  CoreMedia
  
-    Copyright 2005-2015 Apple Inc. All rights reserved.
+    Copyright 2005-2016 Apple Inc. All rights reserved.
  
 */
 
@@ -217,7 +217,7 @@
 /*!
 	@function	CMTimeMakeWithSeconds
 	@abstract	Make a CMTime from a Float64 number of seconds, and a preferred timescale.
-	@discussion	The epoch of the result will be zero.  If preferredTimeScale is <= 0, the result
+	@discussion	The epoch of the result will be zero.  If preferredTimescale is <= 0, the result
 				will be an invalid CMTime.  If the preferred timescale will cause an overflow, the
 				timescale will be halved repeatedly until the overflow goes away, or the timescale
 				is 1.  If it still overflows at that point, the result will be +/- infinity.  The
@@ -228,7 +228,7 @@
 CM_EXPORT 
 CMTime CMTimeMakeWithSeconds(
 				Float64 seconds,
-				int32_t preferredTimeScale)
+				int32_t preferredTimescale)
 							__OSX_AVAILABLE_STARTING(__MAC_10_7,__IPHONE_4_0);
 
 /*!

```