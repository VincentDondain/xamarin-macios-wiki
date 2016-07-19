#Foundation.framework

``` 
diff -ruN /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSString.h /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSString.h
--- /Applications/Xcode8-beta2.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSString.h	2016-06-27 06:06:56.000000000 +0200
+++ /Applications/Xcode8-beta3.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/System/Library/Frameworks/Foundation.framework/Headers/NSString.h	2016-07-13 05:50:31.000000000 +0200
@@ -101,12 +101,12 @@
 
 #pragma mark *** String comparison and equality ***
 
-/* In the compare: methods, the range argument specifies the subrange, rather than the whole, of the receiver to use in the comparison. The range is not applied to the search string.  For example, [@"AB" compare:@"ABC" options:0 range:NSMakeRange(0,1)] compares "A" to "ABC", not "A" to "A", and will return NSOrderedAscending.
+/* In the compare: methods, the range argument specifies the subrange, rather than the whole, of the receiver to use in the comparison. The range is not applied to the search string.  For example, [@"AB" compare:@"ABC" options:0 range:NSMakeRange(0,1)] compares "A" to "ABC", not "A" to "A", and will return NSOrderedAscending. It is an error to specify a range that is outside of the receiver's bounds, and an exception may be raised.
 */
 - (NSComparisonResult)compare:(NSString *)string;
 - (NSComparisonResult)compare:(NSString *)string options:(NSStringCompareOptions)mask;
-- (NSComparisonResult)compare:(NSString *)string options:(NSStringCompareOptions)mask range:(NSRange)compareRange;
-- (NSComparisonResult)compare:(NSString *)string options:(NSStringCompareOptions)mask range:(NSRange)compareRange locale:(nullable id)locale; // locale arg used to be a dictionary pre-Leopard. We now accept NSLocale. Assumes the current locale if non-nil and non-NSLocale. nil continues to mean canonical compare, which doesn't depend on user's locale choice.
+- (NSComparisonResult)compare:(NSString *)string options:(NSStringCompareOptions)mask range:(NSRange)rangeOfReceiverToCompare;
+- (NSComparisonResult)compare:(NSString *)string options:(NSStringCompareOptions)mask range:(NSRange)rangeOfReceiverToCompare locale:(nullable id)locale; // locale arg used to be a dictionary pre-Leopard. We now accept NSLocale. Assumes the current locale if non-nil and non-NSLocale. nil continues to mean canonical compare, which doesn't depend on user's locale choice.
 - (NSComparisonResult)caseInsensitiveCompare:(NSString *)string;
 - (NSComparisonResult)localizedCompare:(NSString *)string;
 - (NSComparisonResult)localizedCaseInsensitiveCompare:(NSString *)string;
@@ -140,17 +140,21 @@
 /* These methods perform string search, looking for the searchString within the receiver string.  These return length==0 if the target string is not found. So, to check for containment: ([str rangeOfString:@"target"].length > 0).  Note that the length of the range returned by these methods might be different than the length of the target string, due composed characters and such.
  
 Note that the first three methods do not take locale arguments, and perform the search in a non-locale aware fashion, which is not appropriate for user-level searching. To do user-level string searching, use the last method, specifying locale:[NSLocale currentLocale], or better yet, use localizedStandardRangeOfString: or localizedStandardContainsString:.
+ 
+The range argument specifies the subrange, rather than the whole, of the receiver to use in the search.  It is an error to specify a range that is outside of the receiver's bounds, and an exception may be raised.
 */
 - (NSRange)rangeOfString:(NSString *)searchString;
 - (NSRange)rangeOfString:(NSString *)searchString options:(NSStringCompareOptions)mask;
-- (NSRange)rangeOfString:(NSString *)searchString options:(NSStringCompareOptions)mask range:(NSRange)searchRange;
-- (NSRange)rangeOfString:(NSString *)searchString options:(NSStringCompareOptions)mask range:(NSRange)searchRange locale:(nullable NSLocale *)locale NS_AVAILABLE(10_5, 2_0);
+- (NSRange)rangeOfString:(NSString *)searchString options:(NSStringCompareOptions)mask range:(NSRange)rangeOfReceiverToSearch;
+- (NSRange)rangeOfString:(NSString *)searchString options:(NSStringCompareOptions)mask range:(NSRange)rangeOfReceiverToSearch locale:(nullable NSLocale *)locale NS_AVAILABLE(10_5, 2_0);
 
 /* These return the range of the first character from the set in the string, not the range of a sequence of characters. 
+ 
+The range argument specifies the subrange, rather than the whole, of the receiver to use in the search.  It is an error to specify a range that is outside of the receiver's bounds, and an exception may be raised.
 */
 - (NSRange)rangeOfCharacterFromSet:(NSCharacterSet *)searchSet;
 - (NSRange)rangeOfCharacterFromSet:(NSCharacterSet *)searchSet options:(NSStringCompareOptions)mask;
-- (NSRange)rangeOfCharacterFromSet:(NSCharacterSet *)searchSet options:(NSStringCompareOptions)mask range:(NSRange)searchRange;
+- (NSRange)rangeOfCharacterFromSet:(NSCharacterSet *)searchSet options:(NSStringCompareOptions)mask range:(NSRange)rangeOfReceiverToSearch;
 
 - (NSRange)rangeOfComposedCharacterSequenceAtIndex:(NSUInteger)index;
 - (NSRange)rangeOfComposedCharacterSequencesForRange:(NSRange)range NS_AVAILABLE(10_5, 2_0);

```