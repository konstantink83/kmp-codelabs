Summary: Create an application based on moko-template
<br>ID: giphy-app-1
<br>Categories: multiplatform
<br>Environments: moko-template
<br>Status: published
<br>Feedback Link: https://github.com/icerockdev/kmp-codelabs/issues
<br>Analytics Account: UA-81805223-5
<br>Author: Aleksey Mikhailov <am@icerock.dev>

# GiphyApp #1 - Create an application based on moko-template
## Intro
Duration: 5

In this lesson we will cover the development of a small application for iOS and Android using [Kotlin Multiplatform](https://kotlinlang.org/docs/reference/multiplatform.html) based on [moko-template](https://github.com/icerockdev/moko-template).

### Tools
We will need: 
- Android Studio 3.4.0+ (**do not use version 3.5.1 because it has a [bug, breaking MPP project](https://youtrack.jetbrains.com/issue/KT-34143)**);
- Xcode 10.3+;
- Xcode Command Line Tools (`xcode-select --install`);
- [CocoaPods](https://cocoapods.org/) (`sudo gem install cocoapods`);
- [JDK](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) - necessary to launch `gradle` from `Xcode build phase`.

### The Result
As a result of the `GiphyApp` lessons, you will get an application to view gif files using [GIPHY API](https://developers.giphy.com/docs/api). 
The UI of this application will be completely native, and the player of gif files will use native libraries [glide](https://github.com/bumptech/glide) for Android and [SwiftyGif](https://github.com/kirualex/SwiftyGif) for iOS.

|android app|ios app|
|---|---|
|![giphy-android-app](assets/giphy-android-app.webp)|![giphy-ios-app](assets/giphy-ios-app.webp)|

Final code is in the [github](https://github.com/Alex009/giphy-mobile) repository.

## Create the project based on the moko-template
Duration: 5

For the project creation we will use a project template from [moko-template](https://github.com/icerockdev/moko-template). 

Benefits
: The project template already has preconfigured builds of iOS and Android applications with a shared library and you will save time on integration of the shared library with the iOS project on iOS, and on configuration of Kotlin Multiplatform modules and dependencies (use [mobile-multiplatform-gradle-plugin](https://github.com/icerockdev/mobile-multiplatform-gradle-plugin) to simplify this configuraion). The project template includes several sample features as well. 

### Use this template
To use this template you have to go to [GitHub moko-template](https://github.com/icerockdev/moko-template) and press a green button `Use this template`. As a result, you will have created a new repository from the last commit of the  `master` branch of the `moko-template` project.

Next, clone this rep:  `git clone <git url of repo>`.

## Test build
Duration: 5

To be sure that the starting state is correct, we will run both applications. To do this: 
- on Android: open the root repository directory in Android Studio, wait till `Gradle Sync` has finished, and run `android-app` as a regular application. 
- on iOS: install project's CocoaPods (in directory `ios-app` run a command `pod install`, and after this open `ios-app/ios-app.xcworkspace` in Xcode and press `Run` to run the application. 

Benefits
: Building the Kotlin/Native portion will take time (the build starts automatically on doing `pod install` as well as at compilation of the iOS project). 

## Setting up app identifiers 
Duration: 10

You can set appllication identifiers like you do in a regular Android or iOS application: 

### Change Appliсation Id
Android - in file `android-app/build.gradle.kts` change:
```kotlin
android {
    ...

    defaultConfig {
        ...
        
        applicationId = "dev.icerock.codelab.giphy"
        ...
    }
}
```
iOS - you have to set `Bundle Identifier` in the project's setting in Xcode like on the screenshot below:  
![Xcode bundle identifier](assets/giphy-1-1.png)

### Change the application name
Android - in file `android-app/src/main/res/values/strings.xml` change:
```xml
<resources>
    <string name="app_name">Giphy App</string>
    ...
</resources>
```
iOS - you have to set `Display name` in the project's setting in Xcode like on the screenshot below:  
![Xcode display name](assets/giphy-1-2.png)

### Change the app icon
You can download the icon resources [here](assets/giphy-1-icons.zip).  

To change the Android icons you have to move the content of the `android` directory of this archive to the `android-app/src/main/res` directory. After this, you need to set this icon in `android-app/src/main/AndroidManifest.xml`:

```xml
<manifest>
    <application
        ...
        android:icon="@mipmap/ic_launcher">
        ...
    </application>
</manifest>
```
To change the icons for iOS, you have to replace the `ios-app/src/Assets.xcassets/AppIcon.appiconset` directory with the corresponding version from the archive. 

### Change launch screen 
iOS has a launch screen, and to replace it you have to modify the `ios-app/src/Resources/LaunchScreen.storyboard` file. For example, let's just change the text like on the screenshot: 

![change launch screen](assets/giphy-1-3.png)

## Next steps 
Duration: 3

The next lesson [GiphyApp #2](https://codelabs.kmp.icerock.dev/codelabs/giphy-app-2) will teach you to create a Gif list. 
