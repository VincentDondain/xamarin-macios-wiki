#CFNetwork.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CFNetwork.framework/Headers/CFSocketStream.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CFNetwork.framework/Headers/CFSocketStream.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CFNetwork.framework/Headers/CFSocketStream.h	2016-05-19 08:07:18.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CFNetwork.framework/Headers/CFSocketStream.h	2016-06-28 08:09:20.000000000 +0200
@@ -173,6 +173,7 @@
 CFN_EXPORT const CFStringRef kCFStreamNetworkServiceTypeVideo      CF_AVAILABLE(10_7, 5_0);   // interactive video
 CFN_EXPORT const CFStringRef kCFStreamNetworkServiceTypeVoice      CF_AVAILABLE(10_7, 5_0);   // interactive voice data
 CFN_EXPORT const CFStringRef kCFStreamNetworkServiceTypeBackground CF_AVAILABLE(10_7, 5_0);   // background
+CFN_EXPORT const CFStringRef kCFStreamNetworkServiceTypeCallSignaling	   CF_AVAILABLE(10_12, 10_0); //Call Signaling
 
 /* deprecated network service type: */
 CFN_EXPORT const CFStringRef kCFStreamNetworkServiceTypeVoIP       CF_DEPRECATED(10_7, 10_11, 4_0, 9_0, "use PushKit for VoIP control purposes");   // voice over IP control - this service type is deprecated in favor of using PushKit for VoIP control

```