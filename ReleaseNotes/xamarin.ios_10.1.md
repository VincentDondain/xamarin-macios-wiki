id:23e82b9c-09e5-428f-9aab-196687fb6ebd
title:Xamarin.iOS
version:9.11.0
releasedate:2016-07-14

<div class="note">
	<b>Cycle 9 Daily Builds</b>
	This version of Xamarin.iOS will likely ship after the release of Xcode 8 and Xamarin.iOS 10.
	Some fixes might be backported into `cycle8` and released long before other parts of `master` becomes public.
</div>

Requirements
============

- The latest features and API requires Xcode 7.3 and the bundled iOS, tvOS and watchOS SDKs;
- Apple Xcode 7.3 requires a Mac running OSX 10.11.3 (El Capitan) or newer;

What's New
==========

This release is built upon our [open sourced SDK](https://github.com/xamarin/xamarin-macios),
using the `master` branch, and include some additional IDE integratin tools.


### Known Issues

* **Issue:** This does not include Xcode8 related work. See our `xcode8` branch and releases for previews. Once Xcode8 and it's SDK becomes stable the `xcode8` branch will be merged into `master`;


### API diff

This is a live document so there's no static list to link to. However our [Jenkins bots](https://jenkins.mono-project.com/job/xamarin-macios-pr-builder/) produce this information for every commit that is being built. Pick on based on `master` and look for the **API diff** link on the left column.