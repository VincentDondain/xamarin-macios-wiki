The **xamarin-macios** wiki is where we keep our documents (release notes, Xcode diff, etc) about **Xamarin.iOS & Xamarin.Mac**.

### Release Notes

Here we keep the initial drafts for release notes based on our main work (on master) or in special branch, e.g. `xcode8` tracks the API and tooling changes to support iOS 10, tvOS 10, watchOS 3 and macOS 10.12.

* [Xamarin.iOS 9.11 (master / C9)](https://github.com/xamarin/xamarin-macios/wiki/xamarin.ios_9.11)
* [Xamarin.iOS 9.99 (xcode8)](https://github.com/xamarin/xamarin-macios/wiki/xamarin.ios_9.99)

Found a typo, an undocumented new feature or a missing bug fix reference ? just create a PR and we'll merge it after review.


### Continuous Builds

You can now download Xamarin.iOS and Xamarin.Mac packages directly from our build bots. They are provided **as-is** and **no** QA or other validations were done on those builds (e.g. builds that failed internal tests are also published)

* [master](https://jenkins.mono-project.com/view/Xamarin.MaciOS/job/xamarin-macios-builds-master/) : our latest bits;
* [cycle8](https://jenkins.mono-project.com/view/Xamarin.MaciOS/job/xamarin-macios-builds-cycle8/) : our next branch being stabilized (in alpha now);
* [xcode8](https://jenkins.mono-project.com/view/Xamarin.MaciOS/job/xamarin-macios-builds-xcode8/) : our support for Xcode8 and the latest SDK (based on cycle8 branch);


### Bindings

To start contributing to the bindings effort, please take a look at the [Bindings](https://github.com/xamarin/xamarin-macios/wiki/Bindings) document.