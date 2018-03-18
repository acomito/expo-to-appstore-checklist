# Expo-to-App-Store Checklist


## NOTE: I WANT TO IMPROVE THIS. PULL REQUESTS WELCOME!


## PREQUESISITES

* To have your app show up under an organization name (e.g. "Trump Apps"), and not your personal name (e.g. "Donald Trump"), be sure to setup an organization account with apple rather than an individual account. You will need a DUNS number, so heads up.
* If you already have an account, you can switch your account to a organization account, but you'll have to reach out to apple. Good luck.
* you need an apple username and apple password. --> Or signup [here](https://developer.apple.com/register)
* you need your apple teamID --> [get it here under the membership tab in the developer section](https://developer.apple.com/account/#/membership)
* for expo < 46.0.5, you need to turn off 2-factor authentication.  --> see [this issue](https://github.com/expo/expo/issues/160) and [see this](https://security.stackexchange.com/questions/41939/two-step-vs-two-factor-authentication-is-there-a-difference). For expo >= 46.0.5 you can try the --local-auth flag (currently in beta): `exp build:ios --local-auth`.  --> see [this comment](https://github.com/expo/expo/issues/160#issuecomment-348375652)
* decide on a bundleIdentifier.  --> see [this stackoverflow question](http://stackoverflow.com/questions/11347470/what-does-bundle-identifier-mean-in-the-ios-project)
* Make sure you've setup reasonable permissions dialogue text: https://docs.expo.io/versions/latest/guides/app-stores.html#system-permissions-dialogs-on-ios

### Gather Icons for App Store

note: The png for the app-icon MUST NOT contain alpha channels or transparencies

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

Screenshots. You can generate these using the Simulator and Command+S to take a screenshot. You must use Window > Scale > 100% (Command+1) https://stackoverflow.com/questions/7092613/take-screenshots-in-the-ios-simulator

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

### Configure Splash Screen

https://docs.expo.io/versions/latest/guides/splash-screens.html

```
"splash": {
  "image": "./assets/splash.png"
}
```
Note, the previous loading screen API is essentially depricated [(source)](https://docs.expo.io/versions/latest/guides/splash-screens.html#migrating-from-the).


# STEP 1

### Go to project directory and publish

* go into your app directory
* go into the exp.json file of your project, then add a slug like "myslug" (The  full slug will be automatically generated, so just put the very last word of the slug such as "myslug" which will be output as exp.host/@notbrent/myslug:)
```
  "slug": "rnplay"
```
* make sure your terminal is in the root directory of your app directory, then run `exp start` (or publish via expo GUI)
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

### Scheme vs. Slug?
They seem like virtually the same thing. What are the differences?


# STEP 4


* build your app by doing this command from teh project root: `exp build:ios`

```
We need your Apple ID/password to manage certificates and provisioning profiles from your Apple Developer account.
? What's your Apple ID?
```

Put in your credentials for your apple developer account. [Make sure 2factor auth is turend off](https://github.com/expo/expo/issues/160)

```
? Do you already have a distribution certificate you'd like us to use,
or do you want us to manage your certificates for you? true
```

hit 1 to let Expo handle our certificates

```
? Do you already have a push notification certificate you'd like us to use,
or do you want us to manage your push certificates for you? true
```

hit 1 to let Expo handle our certificates

Then it will start to build your ipa file

when it is done, you'll see this message and the packager/process will exit/end:

```
[exp] Building...
[exp] Build successfully started, it may take a few minutes to complete. Run "exp build:status" to monitor it.
```
* check on the status with: ```exp build:status```


### Waiting for IPA file to download...

* run `exp build:status` to check on status. keep doing this until eventually it will return the URL
* copy paste that URL into your browser, it should automatically download the ipa file
* this file is what you will upload to the apple store


# STEP 5

### General TODOs before doing iTunes Connect stuff

Decide on:

- app description, 
- keywords, 
- title, 
- and categories

see: https://developer.apple.com/app-store/product-page/

For an example of the pros at work, take a look at instagram or offerup and how they've setup their app store page. Note the title is not always the vanilla app title, and they add additional artwork beyond screenshots.


# STEP 6

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

### General App Information section

* App Icon > Choose File > Your 1024x1024px icon from prerequisite section. MAKE SURE YOU UPLOAD JPG NOT PNG FOR THIS ICON
* Click edit next to "Rating". Fill out questionnaire. Be careful, it's easier to get approved if you don't select "Made For Kids". Click Done.
* Copyright (your business name) required.
* Address information is required.

* now, if you have not yet, download Apple's [Application Loader 3.0](https://itunesconnect.apple.com/apploader/ApplicationLoader_3.0.dmg)
* if you have problems with it, you may need to download xcode, then open xcode, the go to Xcode > developer settings > applications > application loader (this will be application loader 3.6). See: https://forums.developer.apple.com/thread/64041
* either way, 3.6 or 3.0, you will go through the wizard and upload your IPA file.
* after downloading apploader or xcode, open app loader and sign in with your apple username and password
* choose "deliver app" from the options then click "next"
* a file picker will open, find you ipa file that you built earlier (via your terminal, in my case the ipa is no in my downloads)

Is your app designed to use cryptography or does it contain or incorporate cryptography? (Select Yes even if your app is only utilizing the encryption available in iOS or macOS.)

Once you select, yes, another question pops up like: 

"Does your app meet any of the following:
(a) Qualifies for one or more exemptions provided under category 5 part 2
(b) Use of encryption is limited to encryption within the operating system (iOS or macOS)
(c) Only makes call(s) over HTTPS
(d) App is made available only in the U.S. and/or Canada"

All my apps are typically a "Yes" here (I'm sure 89% are), but you should maybe take a minute to assess your specific app.

"Does your app contain, display, or access third-party content?"

- I typically answer yes for most of my apps. I think in this sense they mean social networks (where people other than yourself post content). 

Note: When submitting to the iTunes Store, you’ll be asked whether your app uses the advertising identifier (IDFA). Because Expo depends on Segment Analytics, the answer is yes, and you’ll need to check a couple boxes on the Apple submission form. See Segment’s Guide for which specific boxes to fill in.

https://segment.com/docs/sources/mobile/ios/quickstart/#step-5-submitting-to-the-app-store

Last I checked, you will mark:



Congratulations! You have submitted your app for review. Drink two beers.

App is now "Waiting For Review".
The next stages are:
- "Preparing for Review"
- "Going in Review"
- "Accepted" or "Rejected"

You will receive an email for your app's approval, but it is good to check it yourself in iTunes Connect.


## FURTHER READING

- Wondering how to handle dev vs staging vs production? See [this](https://docs.expo.io/versions/latest/guides/release-channels.html)
- Looking to get some kind of circleCI build process going? see [this recent post](https://blog.expo.io/new-automation-features-in-expo-cli-7a901afcc1bc) from the expo blog.
- Wondering about how OTA updates work with your expo app? See [this](https://docs.expo.io/versions/latest/guides/offline-support.html)
- Interested in HARD MODE? Checkout [this blog post](https://blog.expo.io/automating-standalone-expo-app-builds-and-deployments-with-fastlane-exp-and-exptool-9b2f5ad0a2cd) for setting up FastLane with expo.

## SOURCES

- https://docs.expo.io/versions/latest/guides/building-standalone-apps.html
- https://github.com/alex-wap/app-store


## TODO

* add directions about adding bundleIdentifer in dev console before going to itunes connect
* make a not about SKU
* Finish fastlane steps
