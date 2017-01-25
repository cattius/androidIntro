An Introduction to Android Development
======================================

Why Android?
-----------

Based on the Linux kernel, Android is an open-source operating system which is currently developed by Google, and is designed for touchscreen devices such as smartphones and tablets. Specialised versions of Android have also been developed for cars, smartwatches, digital cameras, games consoles, and TVs. Android is currently overwhelmingly dominant amongst mobile operating systems, with an astounding market share of 86.8% as of Q3 2016. Now running on over a billion smartphones (not to mention tablets), the former underdog OS has become too popular for developers to ignore. It also has numerous advantages over iOS for developers, including no requirement to develop on a Mac (Android Studio is compatible with Windows, Mac, and Linux), reduced developer fees (a $25 one-time payment for the Play Store vs. $99 annually for the Apple App Store), and a shorter app approval process.

A key challenge faced by Android developers is compatibility - with Android you are developing for a much wider range of devices than for iOS, each with different hardware, often running a proprietary software layer from their manufacturer in addition to the main OS, and often running outdated versions of Android. A key decision to make when you begin development is what the minimum API level (OS version) you will support is - this will affect what Android features you can use. Fortunately, there are many options for resolving these compatibility issues, for example the Android Support Library, a collection of libraries which help provide the functionality of newer APIs on older Android releases. 

Android Components
------------------
There are four different fundamental app components: activities, services, broadcast receivers, and content providers. Each component has a lifecycle during which it is created, changes state (possibly many times), and is then destroyed. Each state has an associated method, for example onCreate(), onStart(), and onResume(), and the code within this method will run each time the component enters that state. Each app component must be declared in your app’s AndroidManifest.xml file.

* An Activity is a single screen or user ‘activity’ within your app’s user interface. For example, a weather app might have an activity for the forecast, another activity for the radar map, a search activity for finding forecasts in new locations, and a settings activity. An activity is often full-screen, but you can also layer activities using floating windows or embedding. Fragments are used to subdivide an Activity to further modularise the code.
* Broadcast receivers handle communication between your app and the OS/other apps, for example the OS might send a broadcast with a low battery alert, or a messaging app might send a new message broadcast (even though the user is currently using a different app).
* Services handle an app’s background processes – for example, a music player app should continue playing music even when the user switches to a different app.
* Activities, broadcast receivers and services are all activated by asynchronous message objects called Intents. Intents request actions from other components, binding components together at runtime. For example, you can start an activity by passing an Intent to startActivity(), or start a broadcast by passing an Intent to sendBroadcast().
* Content providers are different – they are activated by requests from a ContentResolver rather than by Intents. They manage stored app data that you might want to share with other apps. For example, the Android OS provides a content provider for the user’s contact data that other apps can query, so that they can read from and write to the contacts if they have the proper permissions to.

Going into more depth on Android components is beyond the scope of this tutorial, but the Android developer guide has detailed documentation.

Get Started
------------
Most Android app development is done in Java, although there are alternatives such as writing critical sections of an app in C/C++ for performance gains, or creating an app in HTML, CSS, and Javascript as if it were a website and then using tools to package it for Android. This tutorial will assume you’re familiar with Java. If not, there are many great resources available online, such as Programming by Doing (aimed at those new to programming) or TutorialsPoint’s guides. 

For this tutorial, we’ll be developing in Android Studio. Based on IntelliJ, this IDE is carefully tailored for Android development, integrating many useful frameworks and tools such as the Android SDK, Gradle (for build automation), a WYSIWYG layout editor, an emulator for testing your app on virtual Android devices, and the Android Device Monitor for viewing system logs while your app is running. Android is one of the development contexts where using an IDE is undoubtedly worthwhile - even simple apps involve a myriad of files and dependencies which would be very time-consuming to manage manually.

First, you’ll need to install Android Studio. After going through the setup wizard, click Start a new Android Studio project. You’ll need to give your new app a name and provide a company domain. The domain is to follow Java package naming conventions, but if you don’t own a domain, don’t worry - you just need to make sure the package name is unique, so you could use your name or a nickname, for example. Select Phone and Tablet as the form factor your app will run on, and choose the minimum SDK your app will support - the example code provided supports API 15.

Finally, select a Google Maps activity to add. This will create an activity for us in our app with some sample code already provided so that we can get our app up and running very quickly.

Project Structure
-----------------
You might be surprised by how many project files the creation wizard has made for you! XML files contain your app’s layouts and settings, and AndroidManifest.xml is the most important of these, providing essential information about your app to the OS. Gradle is a build system which compiles, builds, and tests your code (using the unit tests you provide), packaging all your app’s files into a .apk file, i.e. an app which can be installed on Android devices. Its script files can be modified to change how it carries this out. The res folder contains non-code resources such as XML layouts for each activity, UI strings, and images. The java folder contains your source code, separated by package name. 

Marking the Map
---------------
Take a look at MapsActivity.java (this is the default – if you renamed your activity during the setup wizard, it’ll have the name you gave it). The code Android Studio has provided for you will display a full-screen map. The code in onCreate() sets it up, and then onMapReady() makes changes to the map once it’s ready. By default, it adds a marker at the latitude and longitude of Sydney, Australia, and then moves the camera to centre the map there. 

Let’s try adding a new marker. You can find the latitude and longitude of any address here – try your home or work address, perhaps. In this example, I’ve added a marker at the University of Bristol, and focused the map there instead of on Sydney, although the Sydney marker is still on the map. 

To get data from Google Maps you need developer credentials - a Google Maps API key. Open google_maps_api.xml (in res > values) and copy the link provided in the comment into your browser to go to the Google API Console. Follow the instructions to create a new project and an Android-restricted API key for the project, then add the key into the file where it says YOUR_KEY_HERE:

Running the app
---------------
Next, go to Tools > Android > SDK Manager within the IDE, and make sure you have the latest Android SDK platform (the example code uses 7.1.1 Nougat, SDK level 25), Android SDK Tools, Android SDK Platform-Tools, Android SDK Build-Tools, the Support Repository, and Google Play Services installed.

If you have an Android device, you can run your app on it. First, connect it to your computer by USB (on Windows you may need to install a USB driver). Enable USB debugging by going to Settings > Developer Options on your device, or on Android 4.2 and newer, going to Settings > About phone, tapping Build Number the magic seven times, then going back to the previous screen to see Developer Options. Yes, it’s bizarre! 

If you don’t have an Android device, you can run it in the Android Emulator. First, create a new Virtual Device in Android Studio by going to Tools > Android > AVD Manager. Click Create Virtual Device and pick a phone hardware platform, such as the Nexus 6. Pick a system image which uses the latest Android API level, making sure you use a version which says (with Google APIs).

Whether you’re using an actual device or the Emulator, click Run   in Android Studio and select your (virtual) device as the deployment target. Android Studio will compile and build your app, install it on your device/in the emulator and then open it automatically. Be patient – it might take a while the first time.

Congratulations – you’ve created your first app!

Note: if you get an error saying you must update Google Play services but the update button doesn’t work, try downgrading the version of Google Play services in your build.gradle to 9.6.0, or try running the app on a physical device rather than on the emulator. This seems to be a recurring problem with the emulator.
The full code is available in this repo if you want to look at it.

Explore further
---------------
Explore the Google Maps Android API documentation to see how you could take the project further – there’s a huge range of things you can do with Google Maps. An interesting next challenge would be to mark the user’s current location on the map; this common task for any map-based app is surprisingly complex, due to both the way permissions now work in Android, and the latency and uncertainty involved when querying location providers. Developing a solution will introduce you to these additional core aspects of Android development. Take a look at the guide here to get started.

And of course, there’s many more APIs and Android features to explore than just maps! The Android Developer site is a veritable gold mine of information and tips for all aspects of development, from UI design and accessibility through to publishing on the Play Store.

