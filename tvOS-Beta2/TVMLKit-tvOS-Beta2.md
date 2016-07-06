#TVMLKit.framework

``` diff
diff -ruN /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVViewElement.h /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVViewElement.h
--- /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVViewElement.h	2016-06-01 05:22:17.000000000 +0200
+++ /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVViewElement.h	2016-06-26 09:18:12.000000000 +0200
@@ -84,7 +84,7 @@
 // Value for "autoHighlight" attribute, defines the inital focused element.
 @property (nonatomic, readonly, nullable) NSString *autoHighlightIdentifier;
 // Value for "disabled" attribute
-@property (nonatomic, readonly, getter = isDisabled) BOOL disabled;
+@property (nonatomic, getter = isDisabled) BOOL disabled;
 // Defines the update type after a DOM re-parse. Initial state is TVElementUpdateTypeNone.
 @property (nonatomic, readonly) TVElementUpdateType updateType;
 

```