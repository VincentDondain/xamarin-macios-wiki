#InputMethodKit.framework

``` diff
diff -ruN /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/InputMethodKit.framework/Headers/IMKCandidates.h /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/InputMethodKit.framework/Headers/IMKCandidates.h
--- /Applications/Xcode73.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.11.sdk/System/Library/Frameworks/InputMethodKit.framework/Headers/IMKCandidates.h	2015-08-26 06:42:33.000000000 +0200
+++ /Applications/Xcode8-beta1.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.12.sdk/System/Library/Frameworks/InputMethodKit.framework/Headers/IMKCandidates.h	2016-05-27 02:24:57.000000000 +0200
@@ -13,8 +13,8 @@
  @enum		IMKCandidatePanelType
  @abstract   Lists the basic candidate panel types that are supplied by the InputMethodKit.
  @constant	kIMKSingleColumnScrollingCandidatePanel creates a window with a 1 column X 9 row grid.  If there are more than 9 rows this will display a scroll bar.
- @constant  kIMKScrollingGridCandidatePanel a grid with 5 columns is used to display.  If necessary a scroll bar will be displayed
- @constant	kIMKSingleRowSteppingCandidatePanel a 9 column x 1 row grid is displayed.  If there are more thand 9 candidates a stepper controller will be displayed.
+ @constant  kIMKScrollingGridCandidatePanel a grid with 5 columns is used to display.  If necessary, a scroll bar will be displayed.
+ @constant	kIMKSingleRowSteppingCandidatePanel a 9 column x 1 row grid is displayed.  If there are more than 9 candidates, a stepper controller will be displayed.
  */
 enum {
 	kIMKSingleColumnScrollingCandidatePanel		=	1,
@@ -34,7 +34,7 @@
 /*!
  @enum		IMKCandidatesLocationHint
  @abstract   Provides a hint where to place the candidates display.
- @discussion The IMKCandidatePanelType will use the hint to place the candidate display being sure that the display is always fully visible.
+ @discussion The IMKCandidatePanelType will use the hint to place the candidate display, being sure that the display is always fully visible.
  @constant   kIMKLocateCandidatesAboveHint	Place the candidates above the start of the current text selection.
  @constant	kIMKLocateCandidatesBelowHint	Place the candidates below the start of the current text selection.
  @constant	kIMKLocateCandidatesLeftHint	Place the candidates to the left of the current text selection.
@@ -60,7 +60,7 @@
  @const		IMKCandidatesSendServerKeyEventFirst
  @abstract	Control when key events are sent to a candidate window.
  
- @discussion	Value is a NSNumber with a boolean value of NO (keyevents are sent to the candidate window first) or YES (keyevents are sent to the IMKInputController first). Note this is only applicable when a candidate window is displayed.  The default behavior is to send the key event to the candidate window first.  Then if it is not processed there to send it on to the input controller.
+ @discussion	Value is a NSNumber with a boolean value of NO (key events are sent to the candidate window first) or YES (key events are sent to the IMKInputController first). Note that this is only applicable when a candidate window is displayed.  The default behavior is to send the key event to the candidate window first, and if it is not processed there, to send it on to the input controller.
  */
 extern const NSString*	IMKCandidatesSendServerKeyEventFirst;
 
@@ -71,15 +71,15 @@
 
 @interface IMKCandidates : NSResponder {
 @protected
-	IMKCandidatesPrivate			*_private;
-	
+	IMKCandidatesPrivate *_private;
 }
 
 /*!
  @method     
  @abstract   Default initializer for the class.
- @discussion When an input method allocates an IMKCandidate object is should initialize that object by calling this method passing the IMKServer that will manage the candiates and the initial panel type.
+ @discussion When an input method allocates an IMKCandidate object it should initialize that object by calling this method passing the IMKServer that will manage the candidates and the initial panel type.
  */
+
 -(id)initWithServer:(IMKServer*)server panelType:(IMKCandidatePanelType)panelType;
 
 - (id)initWithServer:(IMKServer*)server panelType:(IMKCandidatePanelType)panelType styleType:(IMKStyleType)style;
@@ -98,21 +98,21 @@
 
 /*!
  @method     
- @abstract   If a candidate window type has been provided show the candidate window. The caller provides a location hint that is used to position the window.
+ @abstract   If a candidate window type has been provided, show the candidate window. The caller provides a location hint that is used to position the window.
  
- Input method's call this method when it is appropriate during text conversion to display a list of candidates.  
+ Input methods call this method when it is appropriate, during text conversion, to display a list of candidates.
  */
 - (void)show:(IMKCandidatesLocationHint)locationHint;
 
 /*!
  @method     
- @abstract   If the candidate window is visible hide it.
+ @abstract   If the candidate window is visible, hide it.
  */
 - (void)hide;
 
 /*!
  @method     
- @abstract   Utility method returns YES if a candidate display is visble.
+ @abstract   Utility method returns YES if a candidate display is visible.
  */
 - (BOOL)isVisible;
 
@@ -120,7 +120,7 @@
 /*!
  @method     
  @abstract   Call this method to update the candidates displayed in the candidate window.
- @discussion Calling this method will result in a call being made to the IMKInputController's candidates method. Note that the candidate list will be updated, but the window's visible state will not change.  That is to say if the window is hidden it will remain hidden and vice versa.
+ @discussion Calling this method will result in a call being made to the IMKInputController's candidates method. Note that the candidate list will be updated, but the window's visible state will not change; that is to say, if the window is hidden it will remain hidden, and vice versa.
  */
 -(void)updateCandidates;
 
@@ -137,7 +137,7 @@
 /*!
  @method     
  @abstract   Returns the current selection.
- @discussion Call this to get the string that the user has selected.  Will return nil if no selection or window is not visible.  
+ @discussion Call this to get the string that the user has selected. Will return nil if no selection or window is not visible.
  */
 -(NSAttributedString*)selectedCandidateString;
 
@@ -151,15 +151,15 @@
 /*!
  @method     
  @abstract   Set the selection keys for the candidates.
- @discussion Selection keys are an array of NSNumbers where each NSNumber is a virtual key codes that the controller will map to characters that are displayed either across the top of the candidates, if the candidates are laid out horizontally, or along the left edge of the candidates if they are aligned vertically.  
+ @discussion Selection keys are an array of NSNumbers where each NSNumber is a virtual key code that the controller will map to characters that are displayed either across the top of the candidates, if the candidates are laid out horizontally, or along the left edge of the candidates, if they are aligned vertically.
  
  The number of selection keys determines how many candidates are displayed per page.  For example, if you
- passed an array of 4 key codes then 4 candidates are displayed per page.  If you passed 11 key codes then 11 candidates would be displayed.
+ passed an array of 4 key codes, then 4 candidates are displayed per page.  If you passed 11 key codes, then 11 candidates would be displayed.
  
  By default the key codes are mapped using the keyboard layout whose source id is com.apple.keylayout.US.  The default layout can be replaced by calling
  setSelectionKeysKeylayout (see below).
  
- The default selection keys are the digits 1 through 9 or in terms of key codes: 18-21,23,22, 26, 28, 25.
+ The default selection keys are the digits 1 through 9, or in terms of key codes: 18-21,23,22, 26, 28, 25.
  */
 -(void)setSelectionKeys:(NSArray*)keyCodes;
 
@@ -167,7 +167,7 @@
  @method     
  @abstract   Returns an NSArray of NSNumbers where each NSNumber is a virtual key code.
  
- The NSArray is an autorelease object. Do not release unless it is first retained.
+ The NSArray is an autoreleased object. Do not release unless it is first retained.
  */
 -(NSArray*)selectionKeys;
 
@@ -181,7 +181,7 @@
  @method     
  @abstract   Returns the key layout that is used to map virtual key codes for the selection keys.  By default this is the key layout whose source id is com.apple.keylayout.US.
  
- This is an autorelease object.  Retain it if you need to keep it.
+ This is an autoreleased object.  Retain it if you need to keep it.
  */
 -(TISInputSourceRef)selectionKeysKeylayout;
 
@@ -197,7 +197,7 @@
  
  NSBackgroundColorDocumentAttribute (value = NSColor).  Set the background color that is drawn behind the candidate text.
  
- IMKCandidatesSendServerKeyEventFirst (value = NSNumber).  NO (default) gives the candidate window first chance at key events.  YES causes events to first be routed to the current IMKInputController.  In that case, if the event is not handled it will then be sent to the candidate window.
+ IMKCandidatesSendServerKeyEventFirst (value = NSNumber).  NO (default) gives the candidate window first chance at key events.  YES causes events to first be routed to the current IMKInputController.  In that case, if the event is not handled, it will then be sent to the candidate window.
  */
 -(void)setAttributes:(NSDictionary*)attributes;
 
@@ -211,7 +211,7 @@
 /*!
  @method     
  @abstract   Setting the dismissesAutomatically flag determines what happens to displayed candidates when the return key or enter key is typed.  
- @discussion By default if a return or enter key is typed the candidates are dismissed and a candidateSelected: message is sent to the input controller.  However if  setDismissesAutomatically is passed a NO flag  the candidate display will not be dismissed when a return or enter key is typed.  The input controller will still be sent the candidatesSelected: message, but, as stated, the candidates display will not be dismissed.  
+ @discussion By default, if a return or enter key is typed, the candidates are dismissed and a candidateSelected: message is sent to the input controller.  However  if setDismissesAutomatically is passed a NO flag  the candidate display will not be dismissed when a return or enter key is typed.  The input controller will still be sent the candidatesSelected: message, but, as stated, the candidates display will not be dismissed.
  
  Setting this flag to NO lets an input method process text input while keeping a dynamically changing candidates display in view throughout the text input process.
  
@@ -300,7 +300,7 @@
 /*!
  @method
  @abstract	Map a candidateString to an identifier.
- @discussion Beginning with MacOS 10.7 candidates strings are mapped internally to an unique identifier of type NSInteger.  Using identifiers to identify a particular candidate is the first stage of enabling data types other than NSString and NSAttributedString for containing the contents of a candidate.
+ @discussion Beginning with MacOS 10.7, candidate strings are mapped internally to an unique identifier of type NSInteger.  Using identifiers to identify a particular candidate is the first stage of enabling data types other than NSString and NSAttributedString for containing the contents of a candidate.
  */
 -(NSInteger)candidateStringIdentifier:(id)candidateString AVAILABLE_MAC_OS_X_VERSION_10_7_AND_LATER;
 
@@ -314,7 +314,7 @@
 /*!
  @method
  @abstract	 Returns the candidate identifier for a given line in the candidate window display.
- @discussion Maps the lineNumber to a candidate identifier.  Line number 0 corresponds to the candidate in the cell currently in the first (top for vertical) line of the candidate window.  This is convienient for input methods that support selecting a candidate by a number key. Line Number values depend on the column arrangement of your candidate.  If you are displaying a single column candidate window than lines that have been scrolled out of view will have negative values.  For other a single row grid line numbers will correspond to the cell's position in the row (i.e. the first cell will be 0, the second 1, etc).  Finally for a grid the line numbers correspond to the grid row.  If the line number is invalid NSNotFound is returned.
+ @discussion Maps the lineNumber to a candidate identifier.  Line number 0 corresponds to the candidate in the cell currently in the first (top for vertical) line of the candidate window.  This is convienient for input methods that support selecting a candidate by a number key. Line Number values depend on the column arrangement of your candidate.  If you are displaying a single column candidate window, lines that have been scrolled out of view will have negative values.  For a single row grid line, numbers will correspond to the cell's position in the row (i.e. the first cell will be 0, the second 1, etc).  Finally, for a grid, the line numbers correspond to the grid row.  If the line number is invalid, NSNotFound is returned.
  @param lineNumber a number representing a cells position in the candidate window.
  */
 -(NSInteger)candidateIdentifierAtLineNumber:(NSInteger)lineNumber AVAILABLE_MAC_OS_X_VERSION_10_7_AND_LATER;
@@ -324,7 +324,7 @@
  @abstract	Returns the line number for a given CandidateID.
  @result  The line number.  NSNotFound if the candidateID is invalid.
  @param  candidateIdentifier - A valid identifier for a candidate.
- @discussion If the cell that contains the candidate is at the top line of the candidate window the return value will be 0.
+ @discussion If the cell that contains the candidate is at the top line of the candidate window, the return value will be 0.
  */
 -(NSInteger)lineNumberForCandidateWithIdentifier:(NSInteger)candidateIdentifier AVAILABLE_MAC_OS_X_VERSION_10_7_AND_LATER;
 

```