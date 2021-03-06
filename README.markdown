# Welcome to Diceshaker.

This repository contains various versions of Diceshaker. Each is as fully functional as it can be; each is meant to be an exercise in mobile UI design and a nifty testbed for mobile OS tech.

## iPhone version

The iPhone version of Diceshaker is built by the "Multiverse" ∞labs build infrastructure. This infrastructure is common and not replicated between projects. In the future, it will be a Git submodule, but for now you must clone it yourself; in both cases, you must set up your Xcode preferences or specify the path manually as a build setting for Diceshaker to build.

That is, you MUST first check out the repository at [http://github.com/millenomi/infinitelabs-build-tools](http://github.com/millenomi/infinitelabs-build-tools)
and set your system up to find these files during the build as the `INFINITELABS_TOOLS` source tree.

To build Diceshaker without errors:

 - from the command line, you may use the experimental Unified Build scripts in the Tools distribution to build the project. For example, if you have checked out the repository in `/Projects/Diceshaker` and the tools in `/Projects/InfiniteLabsTools`, the following will build Diceshaker correctly for testing:

		/Projects/InfiniteLabsTools/Unified/Build /Projects/Diceshaker --debug
	
	The Unified Build Tools switches are in flux, but currently you can use the following:
	
	* Build styles: `--debug`, `--iphone-ad-hoc`, `--iphone-app-store`; also `--release` (which is short for `--iphone-ad-hoc --iphone-app-store`). You can combine these in a single build. Also, `--all` will build all available styles (which is the default).
	* Build options: `--iphone-development-identity CERTIFICATE_NAME`, `--iphone-distribution-identity CERTIFICATE_NAME`; `--iphone-ad-hoc-profile UUID`, `--iphone-app-store-profile UUID` (where `UUID` is the identifier attached to the provisioning profile — if you install the profile via Xcode or the [iPhone Configuration Utility](http://support.apple.com/downloads/iPhone_Configuration_Utility_1_1_for_Mac_OS_X), the profile's installed copy will be renamed to its UUID); `--fast`, which performs a build without cleaning the built products first.

 - from the command line, set the `INFINITELABS_TOOLS` build setting to the full path to the Tools directory you checked out. For example, if you have checked out the repository in `/Projects/Diceshaker` and the tools in `/Projects/InfiniteLabsTools`, the following will build Diceshaker correctly:

		cd /Projects/Diceshaker
		xcodebuild -configuration Debug -sdk iphonesimulator2.2 clean build INFINITELABS_TOOLS=/Projects/InfiniteLabsTools
	
 - from the Xcode IDE, choose Xcode > Preferences from the menu, select the Source Trees section, then add a new source tree called `INFINITELABS_TOOLS` that points to the checked out Tools repository's root. For example, if you have checked out the repository in `/Projects/InfiniteLabsTools`, use that as the path.

The project references an iPhone development and distribution certificate that you won't have. Make sure you modify these settings in the project before you build this app for the device. (Future commits will make it easier to specify this information without "polluting" the pbxproj file with private settings.)

## Android version

The Android version of Diceshaker is developed with Eclipse and can be built with Ant. Building with Ant is as simple as:

	export ANDROID_SDK="/path/to/android/sdk"
	ant
	
in the Android directory. The Ant build file already knows of the dependencies it has to build (which reside in the Java5 directory). Note that you must have the ANDROID_SDK environment variable set to the path to the Android SDK root, or most targets won't work.

Eclipse, on the other hand, does not. To work with Eclipse:

 * Create a new Java project. Rather than creating the project in the workspace, select the Java5 folder as the root for this project.

 * Create a new Android project. Rather than creating etc., select the Android folder as the root.

 * Right- (or ctrl-, on the Mac) click on the Android project, choose Properties, then Java Build Path. Select the Projects tab, and add the Java project to the list. This lets Eclipse know of the dependency between projects.

This usually works.
