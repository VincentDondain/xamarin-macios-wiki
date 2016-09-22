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

- The latest features and API requires Xcode 8 and the bundled iOS, tvOS and watchOS SDKs;
- Apple Xcode 8 requires a Mac running OSX 10.11.5 (El Capitan) or newer;

What's New
==========

This release is built upon our [open sourced SDK](https://github.com/xamarin/xamarin-macios),
using the `master` branch, and include some additional IDE integratin tools.

### It's now possible to specify how many parallel AOT processes mtouch can launch by using the `-j #` argument to mtouch (in the project's iOS Build options). The default is the number of processors on the machine, but builds on high-end machines may profit from increasing this value.

### Known Issues


### API diff

This is a live document so there's no static list to link to. However our [Jenkins bots](https://jenkins.mono-project.com/job/xamarin-macios-pr-builder/) produce this information for every commit that is being built. Pick on based on `master` and look for the **API diff** link on the left column.
