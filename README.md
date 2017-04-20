# expo-to-appstore-checklist


## Decide on a iOS config
This is set in the exp.json file.

```
  "ios": {
    "bundleIdentifier": "identifier",
    "buildNumber": "1.0.0",
  }
```

## Define a Scheme
The scheme is used for things like deep-linking. It is defined in your exp.json file.

```
  "scheme": "myrnapp"
```

## Gather Icons for Expo

These icons will be used in expo and are added to your exp.json file:
* 48x48 png grayscale with transparency (push notifications)
* 512x512 png file with transparency (home screen and within the Exponent app)

## Configure Splash/Loading Screen

```
  "loading": {
    "icon": "./assets/pathToFile.png", // Must be a .png.
    "backgroundColor": "#34495e",
  }
```

## Gather Icons for App Store

## Gather Sceenshots for  App Store

Screenshots. You can generate these using the Simulator and Command+S to take a screenshot. You must use Window > Scale > 100% (Command+1)
* REQUIRED one iPad Pro screenshot.
* REQUIRED one iPhone 7 Plus screenshot.
* These are the highest resolutions for iPad and iPhone.

