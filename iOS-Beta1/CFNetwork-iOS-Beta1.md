#CFNetwork.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CFNetwork.framework/Headers/CFHost.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CFNetwork.framework/Headers/CFHost.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CFNetwork.framework/Headers/CFHost.h	2015-10-02 23:29:26.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CFNetwork.framework/Headers/CFHost.h	2016-05-19 07:47:30.000000000 +0200
@@ -137,7 +137,7 @@
    * debugging purposes. This is used by the CFCopyDescription()
    * function.
    */
-  CFAllocatorCopyDescriptionCallBack  copyDescription;
+  CFAllocatorCopyDescriptionCallBack  __nullable copyDescription;
 };
 typedef struct CFHostClientContext	  CFHostClientContext;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CFNetwork.framework/Headers/CFNetServices.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CFNetwork.framework/Headers/CFNetServices.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CFNetwork.framework/Headers/CFNetServices.h	2015-10-02 23:29:26.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/CFNetwork.framework/Headers/CFNetServices.h	2016-05-19 07:44:41.000000000 +0200
@@ -311,7 +311,7 @@
  *	  Client's info reference which was passed into the client
  *	  context.
  */
-typedef CALLBACK_API_C( void , CFNetServiceMonitorClientCallBack )(CFNetServiceMonitorRef theMonitor, CFNetServiceRef theService, CFNetServiceMonitorType typeInfo, CFDataRef rdata, CFStreamError * __nullable error, void * __nullable info);
+typedef CALLBACK_API_C( void , CFNetServiceMonitorClientCallBack )(CFNetServiceMonitorRef theMonitor, CFNetServiceRef __nullable theService, CFNetServiceMonitorType typeInfo, CFDataRef __nullable rdata, CFStreamError * __nullable error, void * __nullable info);
 
 /*
  *  CFNetServiceBrowserClientCallBack
@@ -341,7 +341,7 @@
  *	  Client's info reference which was passed into the client
  *	  context.
  */
-typedef CALLBACK_API_C( void , CFNetServiceBrowserClientCallBack )(CFNetServiceBrowserRef browser, CFOptionFlags flags, CFTypeRef domainOrService, CFStreamError * __nullable error, void * __nullable info);
+typedef CALLBACK_API_C( void , CFNetServiceBrowserClientCallBack )(CFNetServiceBrowserRef browser, CFOptionFlags flags, CFTypeRef __nullable domainOrService, CFStreamError * __nullable error, void * __nullable info);
 
 /*
  *  CFNetServiceGetTypeID()

```