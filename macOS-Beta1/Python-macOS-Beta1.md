#Python.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Python.framework/Headers/pymactoolbox.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Python.framework/Headers/pymactoolbox.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/Python.framework/Headers/pymactoolbox.h	2015-08-23 05:37:54.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/Python.framework/Headers/pymactoolbox.h	2016-05-11 19:30:36.000000000 +0200
@@ -9,10 +9,6 @@
 
 #include <Carbon/Carbon.h>
 
-#ifndef __LP64__
-#include <QuickTime/QuickTime.h>
-#endif /* !__LP64__ */
-
 /*
 ** Helper routines for error codes and such.
 */
@@ -155,22 +151,6 @@
 extern int GWorldObj_Convert(PyObject *, GWorldPtr *);
 #endif /* !__LP64__ */
 
-/* Qt exports */
-#ifndef __LP64__
-extern PyObject *TrackObj_New(Track);
-extern int TrackObj_Convert(PyObject *, Track *);
-extern PyObject *MovieObj_New(Movie);
-extern int MovieObj_Convert(PyObject *, Movie *);
-extern PyObject *MovieCtlObj_New(MovieController);
-extern int MovieCtlObj_Convert(PyObject *, MovieController *);
-extern PyObject *TimeBaseObj_New(TimeBase);
-extern int TimeBaseObj_Convert(PyObject *, TimeBase *);
-extern PyObject *UserDataObj_New(UserData);
-extern int UserDataObj_Convert(PyObject *, UserData *);
-extern PyObject *MediaObj_New(Media);
-extern int MediaObj_Convert(PyObject *, Media *);
-#endif /* !__LP64__ */
-
 /* Res exports */
 extern PyObject *ResObj_New(Handle);
 extern int ResObj_Convert(PyObject *, Handle *);

```