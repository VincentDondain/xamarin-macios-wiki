<div class="note">
	<b>Classic Profile Deprecation:</b>
	The complete removal of classic support is scheduled for next fall with the release of Xamarin.iOS 10.0 and
	this preview of our iOS 10 support does **not** ship with `monotouch.dll`.
	Xamarin.iOS 9.10 (cycle 8) will be the last version to ship support for `monotouch.dll` this summer.
</div>

Requirements
============

- The latest features and API requires Xcode 8.0 beta 1 and the bundled iOS, tvOS and watchOS SDKs;
- Apple Xcode 8.0 requires a Mac running OSX 10.11.5 (El Capitan) or newer;

What's New
==========

This release is built upon our [open sourced SDK](https://github.com/xamarin/xamarin-macios),
using the `xcode8` branch, and include some additional IDE integratin tools.

This release is based on our **cycle 8** work, which will become XI 9.10 this summer.
It includes Mono 4.6 which continues to adopt more code from 
Microsoft's open sourced .NET code (reference source) to improve the conformance,
speed and memory usage of our base class libraries (BCL).

### New Frameworks

The following new frameworks were added in iOS 10:

* CallKit (available, beta 2)
* Intents (available, beta 2)
* IntentsUI (available, beta 2)
* Message (available, beta 2)
* Speech (available, beta 2)
* UserNotification (available, beta 2)
* UserNotificationUI (available, beta 2)
* VideoSubscriberAccount (available, beta 1)

The following new frameworks were added in tvOS 10:

* ExternalAccessory (blocked) radar #27266975
* HomeKit (enabled, unaudited)
* MultipeerConnectivity (enabled, unaudited)
* Photos (enabled, unaudited)
* ReplayKit (enabled, unaudited)
* UserNotificationUI (enabled, unaudited)
* VideoSubscriberAccount (enabled, unaudited)

The following new frameworks were added in watchOS 3:

* AVFoundation (not yet enabled)
* CloudKit (enabled, unaudited)
* CoreAudio (not yet enabled)
* GameKit (in progress)
* SceneKit (not yet enabled)
* SpriteKit (not yet enabled)
* UserNotificationUI (enabled, unaudited)

Note: New frameworks for tvOS and watchOS are new to the platform, but already exists (or were just added) in iOS.


### New Bindings

Beside the new frameworks there are also many updates to the existing ones. You can track the [progress of our bindings](https://github.com/xamarin/xamarin-macios/wiki/Bindings) from the wiki.

In general we start iOS SDK and when a new beta gets out then we update existing bindings to match the latest changes, then we go back to bind other frameworks. Next we'll work on tvOS and watchOS SDK.

Starting with iOS means we're including most new, shared API with tvOS, watchOS and macOS. The later generally do not require a lot of changes when iOS bindings are over (mostly auditing the API).


### Known Issues

* **Issue:** our watchOS 3.x support has the same limitations our watchOS 2.x support has on the current XI 9.9 preview. The same mono code and tooling is shared with **cycle8** and **xcode8** branches;


### API diff

This is a live document so there's no static list to link to. However our [Jenkins bots](https://jenkins.mono-project.com/job/xamarin-macios-pr-builder/) produce this information for every commit that is being built. Pick on based on `xcode8` and look for the **API diff** link on the left column.
