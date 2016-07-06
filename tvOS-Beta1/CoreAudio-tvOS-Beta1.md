#CoreAudio.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/CoreAudioTypes.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/CoreAudioTypes.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/CoreAudioTypes.h	2015-09-30 22:20:44.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/CoreAudio.framework/Headers/CoreAudioTypes.h	2016-05-27 06:51:23.000000000 +0200
@@ -177,12 +177,11 @@
     UInt32      mNumberBuffers;
     AudioBuffer mBuffers[1]; // this is a variable length array of mNumberBuffers elements
     
-#if defined(__cplusplus) && CA_STRICT
+#if defined(__cplusplus) && defined(CA_STRICT) && CA_STRICT
 public:
     AudioBufferList() {}
 private:
-    //  Copying and assigning a variable length struct is problematic so turn their use into a
-    //  compile time error for eacy spotting.
+    //  Copying and assigning a variable length struct is problematic; generate a compile error.
     AudioBufferList(const AudioBufferList&);
     AudioBufferList&    operator=(const AudioBufferList&);
 #endif
@@ -1309,7 +1308,7 @@
     AudioChannelLayout() {}
 private:
     //  Copying and assigning a variable length struct is problematic so turn their use into a
-    //  compile time error for eacy spotting.
+    //  compile time error for easy spotting.
     AudioChannelLayout(const AudioChannelLayout&);
     AudioChannelLayout&         operator=(const AudioChannelLayout&);
 #endif

```