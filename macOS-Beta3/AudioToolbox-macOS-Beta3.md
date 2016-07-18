#AudioToolbox.framework

``` diff
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AudioQueue.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AudioQueue.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AudioQueue.h	2016-06-26 06:32:17.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioToolbox.framework/Headers/AudioQueue.h	2016-07-09 08:26:35.000000000 +0200
@@ -952,8 +952,8 @@
                                     AudioQueueBufferRef __nullable * __nonnull outBuffer)              __OSX_AVAILABLE_STARTING(__MAC_10_5,__IPHONE_2_0);
 
 /*!
-    @function   AudioQueueAllocateBuffer
-    @abstract   Asks an audio queue to allocate a buffer.
+    @function   AudioQueueAllocateBufferWithPacketDescriptions
+    @abstract   Asks an audio queue to allocate a buffer with space for packet descriptions.
     @discussion
         Once allocated, the pointer to the buffer and the buffer's size are fixed and cannot be
         changed. The mAudioDataByteSize field in the audio queue buffer structure,

```