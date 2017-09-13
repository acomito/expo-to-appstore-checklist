UNDER CONSTRUCTION



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
