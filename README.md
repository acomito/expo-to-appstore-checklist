# Expo-to-App-Store Checklist

TODO


* add directions about adding bundleIdentifer in dev console before going to itunes connect
* make a not about SKU
* Finish fastlane steps


## PREQUESISITES

* you need your apple teamID --> [get it here](https://developer.apple.com/account/#/membership)
* you need your apple username and apple password.
* you need to turn off 2-factor authentication.  --> see [this issue](https://github.com/expo/expo/issues/160)
* decide on a bundleIdentifier.  --> see [this stackoverflow question](http://stackoverflow.com/questions/11347470/what-does-bundle-identifier-mean-in-the-ios-project)

### Gather Icons for App Store

#### iPhone
* 180px × 180px (60pt × 60pt @3x)
* 120px × 120px (60pt × 60pt @2x)
* 120px × 120px (40pt × 40pt @3x)
* 80px × 80px (40pt × 40pt @2x)
* 87px × 87px (29pt × 29pt @3x)
* 58px × 58px (29pt × 29pt @2x)
* 60px × 60px (20pt × 20pt @3x)
* 40px × 40px (20pt × 20pt @2x)
#### iPad Pro
* 167px × 167px (83.5pt × 83.5pt @2x)
* 80px × 80px (40pt × 40pt @2x)
#### iPad, iPad mini
* 152px × 152px (76pt × 76pt @2x)
* 40px × 40px (20pt × 20pt @2x)
#### App Store
* 1024px × 1024px

some more thoughts from stackoverflow: http://stackoverflow.com/questions/34329715/how-to-add-icons-to-react-native-app

WARNING, do not have duplicate icons (exact same size, but different name). DOUBLE CHECK ACTUAL SIZE OF ICONS AND DELETE DUPLICATES
Maybe use https://itunes.apple.com/us/app/prepo/id476533227?mt=12

### Gather Sceenshots for  App Store

Screenshots. You can generate these using the Simulator and Command+S to take a screenshot. You must use Window > Scale > 100% (Command+1)

* REQUIRED one iPad Pro screenshot.
* REQUIRED one iPhone 7 Plus screenshot.
* These are the highest resolutions for iPad and iPhone.

### Gather Icons for Expo

These icons will be used in expo and are added to your exp.json file:

* 48x48 png grayscale with transparency (push notifications)
* 512x512 png file with transparency (home screen and within the Exponent app)

The 48X48 should be used for push notifications, setup like so:

```
  "notification": {
    "icon": "./assets/pathToFile.png", // Must be a .png.
  }
```
and the 512x512 is on a top-level json property called icon:

```
 "icon": "./assets/pathToFile.png", // Must be a .png.
```

### Configure Splash/Loading Screen

```
  "loading": {
    "icon": "./assets/pathToFile.png", // Must be a .png.
    "backgroundColor": "#34495e",
  }
```



# STEP 1

### Go to project directory and publish

* go into your app directory
* go into the exp.json file of your project, then add a slug like "myslug" (The  full slug will be automatically generated, so just put the very last word of the slug such as "myslug" which will be output as exp.host/@notbrent/myslug:)
```
  "slug": "rnplay"
```
* make sure your terminal is in the root directory of your app directory, then run `exp start`
* that will show a QR code, etc. and you'll see "[exp] Dependency graph loaded.". This means you're done, hit ctrl + C to stop packager


# STEP 2

### Decide on a iOS config
This is set in the exp.json file.

```
  "ios": {
    "bundleIdentifier": "identifier",
    "buildNumber": "1.0.0",
  }
```

# STEP 3

### Define a Scheme
The scheme is used for things like deep-linking. It is defined in your exp.json file.

```
  "scheme": "myrnapp"
```


# STEP 4





* build your app by doing this command from teh project root: ```exp build:status```
```
We need your Apple ID/password to manage certificates and provisioning profiles from your Apple Developer account.
? What's your Apple ID?
```

```
? Do you already have a distribution certificate you'd like us to use,
or do you want us to manage your certificates for you? true
```

hit 1 for yes

```
? Do you already have a push notification certificate you'd like us to use,
or do you want us to manage your push certificates for you? true
```

hit 1 for yes

Then it will start to build your ipa file

when it is done, you'll see this message and the packager/process will exit/end:

```
[exp] Building...
[exp] Build successfully started, it may take a few minutes to complete. Run "exp build:status" to monitor it.
```


### Waiting for IPA file to download...

* run `exp build:status` to check on status. keep doing this until eventually it will return the URL


### Test it on fastlane's pilot [SECTION UNDER CONSTRUCTION, MOVE TO NEXT]:

https://github.com/fastlane/fastlane/tree/master/pilot

* download fastlane first (if you have not)
* go into your project directory and run `fastlane init`
* it will ask if this is an iOS project, say yes
* it will say it could not automatically detect the file, plrease provide a path: provide it ``
* it will ask for your appleID/credientials-- provide them.
* now you have a fastfile folder in your project
* make changes to your file like the following:

```
fastlane_version "1.68.0"

default_platform :ios

platform :ios do

  desc "Submit a new Beta Build to Apple TestFlight"
  desc "This will also make sure the profile is up to date"
  lane :beta do
    match(type: "appstore")

    gym(
      scheme: "AwesomeProject",
      project: './ios/AwesomeProject.xcodeproj'
    )

    pilot

  end
end
```


> match(type: "appstore") will make sure you’ve got the latest version of the certificates/provisioning profiles and keep them > in sync.
> 
> gym(...) will build and sign your application.
> 
> pilot will upload the result to TestFlight.
> 
> That’s all we need from Fastlane. Have a look at the Fastlane Docs for more actions and information.

above directions are via [this blog](https://dbanck.svbtle.com/deploying-a-react-native-app-with-fastlane)
maybe more up-to-date: https://medium.com/react-native-training/fastlane-for-react-native-ios-android-app-devops-8ca85bee614e
code signing: https://codesigning.guide/

* If the gods are on your side, you should now have fastlane setup 
* go into the directory that holds your ipa file
* run `fastlane pilot upload`
* then invite a tester with `fastlane pilot add email@invite.com`


Note: When submitting to the iTunes Store, you’ll be asked whether your app uses the advertising identifier (IDFA). Because Expo depends on Segment Analytics, the answer is yes, and you’ll need to check a couple boxes on the Apple submission form. See Segment’s Guide for which specific boxes to fill in.


### General TODOs

Decide on app description, keywords, title and categories:

https://developer.apple.com/app-store/product-page/

### iTunes Connect

* Go to iTunes Connect.
* Go to My Apps.
* Click the plus button to create a "New iOS App".
* Select iOS Checkbox.
* Name field for your New App is permanent after submission. Pick what you want carefully.
* Select English for "Primary Language".
* Select your Bundle ID.
* SKU is a unique ID (you pick it). e.g. NameOfApp0.1
* Click Create


### iOS App 1.0 Prepare for Submission

* Choose File > Your iPhone screenshot from the prerequisite section.
* Click iPad button above screenshot preview.
* Choose File > Your iPad screenshot from the prerequisite section.
* Click Save (top right)
* Description is required.
* Keywords are required.
* Support URL is required (your website or github).
* Ignore "Build" for now and scroll down to "General App Information".


BASED ON: https://github.com/alex-wap/app-store
