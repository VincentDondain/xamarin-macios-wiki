#AudioVideoBridging.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioVideoBridging.framework/Headers/AVB17221ACMPMessage.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioVideoBridging.framework/Headers/AVB17221ACMPMessage.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioVideoBridging.framework/Headers/AVB17221ACMPMessage.h	2016-05-20 08:23:23.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioVideoBridging.framework/Headers/AVB17221ACMPMessage.h	2016-06-26 09:10:49.000000000 +0200
@@ -126,6 +126,22 @@
  */
 @property (copy, nullable) AVBMACAddress *sourceMAC;
 
+/*!
+	@method		errorForStatusCode:
+	@abstract	This method returns an NSError filled out with an appropriate description for the passed in status code.
+	@result		An NSError instance within the AVBErrorDomain with the status code and an appropriate description.
+				Will return nil if status code is success or in progress.
+ */
++ (nullable NSError *)errorForStatusCode:(AVB17221ACMPStatusCode)statusCode;
+
+/*!
+	@method		errorForStatusCode
+	@abstract	This method returns an NSError filled out with an appropriate description for the message's status code.
+	@result		An NSError instance within the AVBErrorDomain with the status code and an appropriate description.
+				Will return nil if status code is success or in progress.
+ */
+- (nullable NSError *)errorForStatusCode;
+
 @end
 
 NS_ASSUME_NONNULL_END
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioVideoBridging.framework/Headers/AVB17221AECPMessage.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioVideoBridging.framework/Headers/AVB17221AECPMessage.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioVideoBridging.framework/Headers/AVB17221AECPMessage.h	2016-05-04 00:21:22.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/AudioVideoBridging.framework/Headers/AVB17221AECPMessage.h	2016-06-26 09:10:49.000000000 +0200
@@ -75,6 +75,21 @@
  */
 @property (copy) AVBMACAddress *sourceMAC;
 
+/*!
+	@method		errorForStatusCode:
+	@abstract	This method returns an NSError filled out with an appropriate description for the passed in status code.
+	@result		An NSError instance within the AVBErrorDomain with the status code and an appropriate description.
+				Will return nil if status code is success or in progress.
+ */
++ (nullable NSError *)errorForStatusCode:(AVB17221AECPStatusCode)statusCode;
+
+/*!
+	@method		errorForStatusCode
+	@abstract	This method returns an NSError filled out with an appropriate description for the message's status code.
+	@result		An NSError instance within the AVBErrorDomain with the status code and an appropriate description.
+				Will return nil if status code is success or in progress.
+ */
+- (nullable NSError *)errorForStatusCode;
 
 @end
 

```