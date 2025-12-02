This is to demonstrate a versioning error.

Steps to replicate:

1. Clone repo
2. Install dependencies (`npm install`)
3. Run prebuild (`npm run prebuild:tv`)

You'll then see this error:
```
⚠️  Something went wrong running `pod install` in the `ios` directory.
Command `pod install` failed.
└─ Cause: CocoaPods could not find compatible versions for pod "openiap":
  In Podfile:
    ExpoIap (from `../node_modules/expo-iap/ios`) was resolved to 3.1.36, which depends on
      openiap (~> 1.2.39)

Specs satisfying the `openiap (~> 1.2.39)` dependency were found, but they required a higher minimum deployment target.

pod install --repo-update --ansi exited with non-zero code: 1
```

I get this error when I try to `npm run ios:device` (when I remove the lines in app.json setting tvos versions--when I have the tvos versions set in the app.json, I get a giant error output):

```
❌  (node_modules/expo-iap/ios/ExpoIapHelper.swift:3:8)

  1 | import ExpoModulesCore
  2 | import Foundation
> 3 | import OpenIAP
    |        ^ compiling for tvOS 15.1, but module 'OpenIAP' has a minimum deployment target of tvOS 16.0: /Users/christopher/Library/Developer/Xcode/D
erivedData/MyTVProject-gpmesbimsfidlocknpgixgtdohcn/Build/Products/Debug-appletvos/openiap/OpenIAP.swiftmodule/arm64-apple-tvos.swiftmodule
  4 | 
  5 | /// Exception wrapper for PurchaseError that preserves OpenIAP error codes
  6 | /// This ensures consistent error format between try-catch and onPurchaseError callback
```

Probably relevant files:

- package.json
- app.json
- ios/Podfile (generated - `platform :tvos, podfile_properties['ios.deploymentTarget'] || '15.1'`):
