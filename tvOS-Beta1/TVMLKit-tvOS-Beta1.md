#TVMLKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVInterfaceFactory.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVInterfaceFactory.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVInterfaceFactory.h	2016-03-03 06:21:35.000000000 +0100
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVInterfaceFactory.h	2016-06-01 05:22:04.000000000 +0200
@@ -43,6 +43,12 @@
  */
 - (nullable UIImage *)imageForResource:(NSString *)resourceName NS_AVAILABLE_IOS(9_2);
 
+/*
+ @description Return a collection view cell class given an element contained in a list, shelf or grid. A common cell class is used for all elements
+ 		that share the same name in a collection, hence this method is only called once per a unique element name. Return nil for default handling.
+ */
+- (nullable Class)collectionViewCellClassForElement:(TVViewElement *)element NS_AVAILABLE_IOS(10_0);
+
 @end
 
 /*!
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVViewElement.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVViewElement.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVViewElement.h	2015-10-09 07:07:44.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVViewElement.h	2016-06-01 05:22:17.000000000 +0200
@@ -37,7 +37,13 @@
     /*!
      @brief Signifies that the node itself and its subtree is modified.
      */
-    TVElementUpdateTypeSelf
+    TVElementUpdateTypeSelf,
+    
+    /*!
+     @brief Signifies that style property on view elements could have changed as
+            a result of reevaluating media queries.
+     */
+    TVElementUpdateTypeStyles NS_AVAILABLE_IOS(10_0),
 } NS_ENUM_AVAILABLE_IOS(9_0);
 
 /*!
@@ -78,7 +84,7 @@
 // Value for "autoHighlight" attribute, defines the inital focused element.
 @property (nonatomic, readonly, nullable) NSString *autoHighlightIdentifier;
 // Value for "disabled" attribute
-@property (nonatomic, getter = isDisabled) BOOL disabled;
+@property (nonatomic, readonly, getter = isDisabled) BOOL disabled;
 // Defines the update type after a DOM re-parse. Initial state is TVElementUpdateTypeNone.
 @property (nonatomic, readonly) TVElementUpdateType updateType;
 
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVViewElementStyle.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVViewElementStyle.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVViewElementStyle.h	2015-10-09 07:07:44.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/AppleTVOS.platform/Developer/SDKs/AppleTVOS.sdk/System/Library/Frameworks/TVMLKit.framework/Headers/TVViewElementStyle.h	2016-06-01 05:22:04.000000000 +0200
@@ -61,6 +61,7 @@
 @property (nonatomic, readonly, nullable) NSString *fontWeight;
 @property (nonatomic, readonly) CGFloat height;
 @property (nonatomic, readonly) UIEdgeInsets margin;
+@property (nonatomic, readonly) UIEdgeInsets focusMargin NS_AVAILABLE_IOS(10_0);
 @property (nonatomic, readonly) CGFloat maxHeight;
 @property (nonatomic, readonly) CGFloat maxWidth;
 @property (nonatomic, readonly) CGFloat minHeight;

```