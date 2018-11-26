***NOTE: this project is now archived & unmaintained, and here for informational purposes only***

# rnfb-test-project
repo for testing https://github.com/invertase/react-native-firebase/issues/917

**iOS testing only**

# Environment
This repo was generated under the following environment

* macOS High Sierra 10.13.3
* react-native cli 2.0.1
* react 16.3.0-rc.0 (default installed by react-native init)
* react-native-firebase 3.3.1 (default)
* yarn 1.5.1
* cocoapods 1.3.1
* node 8.10.0 (via NVM)
* nvm 0.33.6
* Xcode 9.2 (9C40b)

# Branches
Each branch represents the addition of a new component

## master
A virgin react-native project created with `react-native init`

### build status
* `react-native run-ios` - successful
* Xcode (IDE) 'debug' build of `RNFBTestProject/ios/RNFBTestProject.xcodeproj` - successful

## rnfb-core
*branched from master*
1. React Native Firebase added per [https://rnfirebase.io/docs/v3.3.x/installation/initial-setup]
  * `yarn add react-native-firebase`
  * `react-native link react-native-firebase`
  * add dummy `GoogleService-Info.plist`
  * add `Firebase.h` import to `AppDelegate.m`
  * add `[FIRApp configure];`
  * `pod init` in '/ios'
  * add `pod 'Firebase/Core'` to Podfile
  * uncomment `platform :ios, '9.0'` at top of Podfile
  * `pod install`
    * **results in error `[!] The target `RNFBTestProject-tvOSTests` is declared twice.`**
    * remove all targets for '...tvOS...' from Podfile
    * `pod install`
  * `pod update`
    * pod output `Analyzing dependencies\
Downloading dependencies\
Using Firebase (4.11.0)\
Using FirebaseAnalytics (4.1.0)\
Using FirebaseCore (4.0.18)\
Using FirebaseInstanceID (2.0.10)\
Using GoogleToolboxForMac (2.1.3)\
Using nanopb (0.3.8)\
Generating Pods project\
Integrating client project\
Sending stats\
Pod installation complete! There is 1 dependency from the Podfile and 6 total pods installed.`

### build status
**NOTE: substitute a real GoogleService-Info.plist file in order to launch**
* `react-native run-ios` - successful
* Xcode (IDE) 'debug' build of `/RNFBTestProject/ios/RNFBTestProject.xcworkspace` - successful

## rnfb-firestore
*branched from rnfb-core*
1. React Native Firebase 'Firestore' module added per [https://rnfirebase.io/docs/v3.3.x/firestore/ios]
  * add `pod 'Firebase/Firestore'` to Podfile
  * `pod update`
  * close and reopen Xcode workspace, run a clean

### build status
**NOTE: substitute a real GoogleService-Info.plist file in order to launch**
* `react-native run-ios` - successful
* Xcode (IDE) 'debug' build of `/RNFBTestProject/ios/RNFBTestProject.xcworkspace` - successful

**To my surprise, this worked fine. The addition of the Firestore pod did NOT pull in the 'React' pod dependency**

## rn-vector-icons
*branched from rnfb-firestore*

**NOTE: I noticed a common dependency of 'react-native-vector-icons' between my production stuff and @scottarivale's Podfile. This branch adds that dependency, which results in changes to the Podfile via the `react-native link` step**
1. Add react-native-vector-icons package per [https://github.com/oblador/react-native-vector-icons]
  * `yarn add react-native-vector-icons`
  * `react-native link`
    * output: `Scanning folders for symlinks in /Users/michaeljarecki/rnative/RNFBTestProject/node_modules (22ms)  
rnpm-install info Platform 'ios' module react-native-firebase is already linked   
rnpm-install info Platform 'android' module react-native-firebase is already linked   
rnpm-install info Linking react-native-vector-icons ios dependency   
rnpm-install info Platform 'ios' module react-native-vector-icons has been successfully linked   
rnpm-install info Linking react-native-vector-icons android dependency   
rnpm-install info Platform 'android' module react-native-vector-icons has been successfully linked   
rnpm-install info Linking assets to ios project   
rnpm-install WARN ERRGROUP Group 'Resources' does not exist in your Xcode project. We have created it automatically for you.  
rnpm-install info Linking assets to android project   
rnpm-install info Assets have been successfully linked to your project`
  * `pod install` **React pod is downloaded**

### build status
**NOTE: substitute a real GoogleService-Info.plist file in order to launch**
* `react-native run-ios` - **failure**
* Xcode (IDE) 'debug' build of `/RNFBTestProject/ios/RNFBTestProject.xcworkspace` - **failure**
