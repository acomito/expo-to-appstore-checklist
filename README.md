# Expo-to-App-Store Checklist


### Decide on a iOS config
This is set in the exp.json file.

```
  "ios": {
    "bundleIdentifier": "identifier",
    "buildNumber": "1.0.0",
  }
```

### Define a Scheme
The scheme is used for things like deep-linking. It is defined in your exp.json file.

```
  "scheme": "myrnapp"
```

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


### Gather Sceenshots for  App Store

Screenshots. You can generate these using the Simulator and Command+S to take a screenshot. You must use Window > Scale > 100% (Command+1)
* REQUIRED one iPad Pro screenshot.
* REQUIRED one iPhone 7 Plus screenshot.
* These are the highest resolutions for iPad and iPhone.

