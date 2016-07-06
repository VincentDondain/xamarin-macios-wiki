#AVFoundation.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h	2016-05-25 07:22:12.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAsset.h	2016-06-27 06:16:12.000000000 +0200
@@ -3,7 +3,7 @@
 
 	Framework:  AVFoundation
  
-	Copyright 2010-2015 Apple Inc. All rights reserved.
+	Copyright 2010-2016 Apple Inc. All rights reserved.
 
 */
 
@@ -324,7 +324,10 @@
 
 @interface AVAsset (AVAssetProtectedContent)
 
-/* Indicates whether or not the asset has protected content.
+/*!
+  @property		hasProtectedContent
+  @abstract		Indicates whether or not the asset has protected content.
+  @discussion	Assets containing protected content may not be playable without successful authorization, even if the value of the "playable" property is YES.  See the properties in the AVAssetUsability category for details on how such an asset may be used.  On OS X, clients can use the interfaces in AVPlayerItemProtectedContentAdditions.h to request authorization to play the asset.
 */
 @property (nonatomic, readonly) BOOL hasProtectedContent NS_AVAILABLE(10_7, 4_2);
 
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetWriterInput.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetWriterInput.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetWriterInput.h	2016-05-04 00:21:25.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVAssetWriterInput.h	2016-06-27 06:04:30.000000000 +0200
@@ -256,7 +256,14 @@
  
  @discussion
 	The timing information in the sample buffer, considered relative to the time passed to -[AVAssetWriter startSessionAtSourceTime:], will be used to determine the timing of those samples in the output file.
- 
+
+	For track types other than audio tracks, to determine the duration of all samples in the output file other than the very last sample that's appended, the difference between the sample buffer's output DTS and the following sample buffer's output DTS will be used. The duration of the last sample is determined as follows:
+	1. If a marker sample buffer with kCMSampleBufferAttachmentKey_EndsPreviousSampleDuration is appended following the last media-bearing sample, the difference between the output DTS of the marker sample buffer and the output DTS of the last media-bearing sample will be used.
+	2. If the marker sample buffer is not provided and if the output duration of the last media-bearing sample is valid, it will be used.
+	3. if the output duration of the last media-bearing sample is not valid, the duration of the second-to-last sample will be used.
+
+	For audio tracks, the properties of each appended sample buffer are used to determine corresponding output durations.
+
 	The receiver will retain the CMSampleBuffer until it is done with it, and then release it.  Do not modify a CMSampleBuffer or its contents after you have passed it to this method.
  
 	If the sample buffer contains audio data and the AVAssetWriterInput was intialized with an outputSettings dictionary then the format must be linear PCM. If the outputSettings dictionary was nil then audio data can be provided in a compressed format, and it will be passed through to the output without any re-compression. Note that advanced formats like AAC will have encoder delay present in their bitstreams. This data is inserted by the encoder and is necessary for proper decoding, but it is not meant to be played back. Clients who provide compressed audio bitstreams must use kCMSampleBufferAttachmentKey_TrimDurationAtStart to mark the encoder delay (generally restricted to the first sample buffer). Packetization can cause there to be extra audio frames in the last packet which are not meant to be played back. These remainder frames should be marked with kCMSampleBufferAttachmentKey_TrimDurationAtEnd. CMSampleBuffers obtained from AVAssetReader will already have the necessary trim attachments. Please see http://developer.apple.com/mac/library/technotes/tn2009/tn2258.html for more information about encoder delay. When attaching trims make sure that the output PTS of the sample buffer is what you expect. For example if you called -[AVAssetWriter startSessionAtSourceTime:kCMTimeZero] and you want your audio to start at time zero in the output file then make sure that the output PTS of the first non-fully trimmed audio sample buffer is kCMTimeZero.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMovieTrack.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMovieTrack.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMovieTrack.h	2016-05-26 02:32:47.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVMovieTrack.h	2016-06-27 04:08:21.000000000 +0200
@@ -367,7 +367,7 @@
                     Note regarding sample timing: in a track's media, the first sample's decode timestamp must always be zero.
                     For an audio track, each sample buffer's duration is used as the sample decode duration.
                     For other track types, difference between a sample's decode timestamp and the following 
-                    sample's decode timestamps is used as the first sample's decode duration, so as to preserve the relative timing.
+                    sample's decode timestamp is used as the first sample's decode duration, so as to preserve the relative timing.
                     
                     Note that this method does not modify the track's sourceTimeMappings but only appends sample references and sample data to the track's media.  
                     To make the new samples appear in the track's timeline, invoke -insertMediaTimeRange:intoTimeRange:.
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItem.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItem.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItem.h	2016-05-25 04:39:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVPlayerItem.h	2016-06-27 06:16:16.000000000 +0200
@@ -957,6 +957,14 @@
 @property (nonatomic, readonly) double indicatedBitrate;
 
 /*!
+ @property		indicatedAverageBitrate
+ @abstract		Average throughput required to play the stream, as advertised by the server. Measured in bits per second.
+ @discussion	Value is negative if unknown. Corresponds to "sc-indicated-avg-bitrate".
+ This property is not observable.
+ */
+@property (nonatomic, readonly) double indicatedAverageBitrate NS_AVAILABLE(10_12, 10_0);
+
+/*!
  @property		averageVideoBitrate
  @abstract		The average bitrate of video track if it is unmuxed. Average bitrate of combined content if muxed. Measured in bits per second.
  @discussion	Value is negative if unknown. Corresponds to "c-avg-video-bitrate".
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoComposition.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoComposition.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoComposition.h	2016-05-25 04:40:26.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AVFoundation.framework/Headers/AVVideoComposition.h	2016-06-27 04:08:29.000000000 +0200
@@ -97,17 +97,11 @@
  @discussion
     Collectively the properties colorPrimaries, colorYCbCrMatrix, and colorTransferFunction define the color space that the rendered frames will be tagged with. For custom video compositing these properties are also used to specify the required color space of the source frames.
 
-    Examples of common color spaces:
-	
-        TODO: SD
-        TODO: HD
-        TODO: HD-P3
+    For examples of common color spaces see AVVideoSettings.h.
 
     How to preserve the color space of the source frames:
  
         Decide which color space to be preserved by examining the source asset's video tracks. Copy the source track's primaries, matrix and transfer function into the video composition's colorPrimaries, colorYCbCrMatrix and colorTransferFunction respectively.
-		
-        TODO: <rdar://problem/25496972> sample code showing how to inspect the source asset track's primaries etc and setup a video composition to preserve them. Ideally we'll show the narrow-HD case and the wide-P3 case.
 
         - When using custom video compositing
 			Setting these properties will cause source frames to be converted into the specified color space and tagged as such. New frames allocated using -[AVVideoCompositionRenderContext newPixelBuffer] will also be tagged correctly.
@@ -266,17 +260,11 @@
  @discussion
     Collectively the properties colorPrimaries, colorYCbCrMatrix, and colorTransferFunction define the color space that the rendered frames will be tagged with. For custom video compositing these properties are also used to specify the required color space of the source frames.
 
-    Examples of common color spaces:
-	
-        TODO: SD
-        TODO: HD
-        TODO: HD-P3
+    For examples of common color spaces see AVVideoSettings.h.
 
     How to preserve the color space of the source frames:
  
         Decide which color space to be preserved by examining the source asset's video tracks. Copy the source track's primaries, matrix and transfer function into the video composition's colorPrimaries, colorYCbCrMatrix and colorTransferFunction respectively.
-		
-        TODO: <rdar://problem/25496972> sample code showing how to inspect the source asset track's primaries etc and setup a video composition to preserve them. Ideally we'll show the narrow-HD case and the wide-P3 case.
 
         - When using custom video compositing
 			Setting these properties will cause source frames to be converted into the specified color space and tagged as such. New frames allocated using -[AVVideoCompositionRenderContext newPixelBuffer] will also be tagged correctly.

```