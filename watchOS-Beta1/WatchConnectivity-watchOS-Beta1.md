#WatchConnectivity.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/WatchConnectivity.framework/Headers/WCSession.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/WatchConnectivity.framework/Headers/WCSession.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/WatchConnectivity.framework/Headers/WCSession.h	2016-02-25 03:39:07.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/WatchOS.platform/Developer/SDKs/WatchOS.sdk/System/Library/Frameworks/WatchConnectivity.framework/Headers/WCSession.h	2016-05-18 06:55:50.000000000 +0200
@@ -48,6 +48,9 @@
 /** The state of the current session */
 @property (nonatomic, readonly) WCSessionActivationState activationState __IOS_AVAILABLE(9.3) __WATCHOS_AVAILABLE(2.2);
 
+/** Whether or not there is more content for the session to deliver */
+@property (nonatomic, readonly) BOOL hasContentPending __IOS_AVAILABLE(10.0) __WATCHOS_AVAILABLE(3.0);
+
 /** ------------------------- iOS App State For Watch ---------------------------
  *  State information that applies to Watch and is only available to the iOS app.
  *  This information includes device state, counterpart app state, and iOS app
@@ -63,6 +66,9 @@
 /** Check if the user has the Watch app's complication enabled */
 @property (nonatomic, readonly, getter=isComplicationEnabled) BOOL complicationEnabled __WATCHOS_UNAVAILABLE;
 
+/** The number of calls remaining to transferCurrentComplicationUserInfo: before the system starts transferring the complicationUserInfo as regular userInfos. If this is 0, the complicationUserInfo will be transferred as regular userInfos. Count will be 0 whenever the complication is not enabled */
+@property (nonatomic, readonly) NSUInteger remainingComplicationUserInfoTransfers __IOS_AVAILABLE(10.0) __WATCHOS_UNAVAILABLE;
+
 /** Use this directory to persist any data specific to the selected Watch. The location of the URL will change when the selected Watch changes. This directory will be deleted upon next launch if the watch app is uninstalled for the selected Watch, or that Watch is unpaired. If the watch app is not installed for the selected Watch the value will be nil. */
 @property (nonatomic, readonly, nullable) NSURL *watchDirectoryURL __WATCHOS_UNAVAILABLE;
 
@@ -129,8 +135,6 @@
  */
 @protocol WCSessionDelegate <NSObject>
 
-@optional
-
 /** Called when the session has completed activation. If session state is WCSessionActivationStateNotActivated there will be an error with more details. */
 - (void)session:(WCSession *)session activationDidCompleteWithState:(WCSessionActivationState)activationState error:(nullable NSError *)error __IOS_AVAILABLE(9.3) __WATCHOS_AVAILABLE(2.2);
 
@@ -142,6 +146,8 @@
 /** Called when all delegate callbacks for the previously selected watch has occurred. The session can be re-activated for the now selected watch using activateSession. */
 - (void)sessionDidDeactivate:(WCSession *)session __IOS_AVAILABLE(9.3) __WATCHOS_UNAVAILABLE;
 
+@optional
+
 /** Called when any of the Watch state properties change. */
 - (void)sessionWatchStateDidChange:(WCSession *)session __WATCHOS_UNAVAILABLE;
 

```