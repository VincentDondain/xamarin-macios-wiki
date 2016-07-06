#MultipeerConnectivity.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MultipeerConnectivity.framework/Headers/MCNearbyServiceAdvertiser.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MultipeerConnectivity.framework/Headers/MCNearbyServiceAdvertiser.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MultipeerConnectivity.framework/Headers/MCNearbyServiceAdvertiser.h	2015-10-03 02:22:27.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/MultipeerConnectivity.framework/Headers/MCNearbyServiceAdvertiser.h	2016-05-25 05:40:17.000000000 +0200
@@ -73,7 +73,7 @@
 - (void)            advertiser:(MCNearbyServiceAdvertiser *)advertiser
   didReceiveInvitationFromPeer:(MCPeerID *)peerID
                    withContext:(nullable NSData *)context
-             invitationHandler:(void (^)(BOOL accept, MCSession *session))invitationHandler;
+             invitationHandler:(void (^)(BOOL accept, MCSession * __nullable session))invitationHandler;
 
 @optional
 // Advertising did not start due to an error.

```