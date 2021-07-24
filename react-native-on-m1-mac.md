# Setting up a new React Native App

`npx react-native init MyApp`

### 1. Exclude `arm64` from Xcode project

- Open `ios/MyApp.xcworkspace` with Xcode

- Go to `Build Settings` and under `Excluded Architectures` add `arm64` for both `Debug` and `Release`

### 2. Exclude `arm64` from Podfile

- Open `ios/Podfile` with a text editor and add this after `react_native_post_install(installer)`:
```
installer.pods_project.build_configurations.each do |config| config.build_settings["EXCLUDED_ARCHS[sdk=iphonesimulator*]"] =  "arm64"
end
```
3. Reinstall pods so that they're refreshed

Reinstall pods with `cd ios && pod deintegrate && pod install && cd ..`

4. Run

`npx react-native run-ios`

PS: if necessary clean up dev env with `rm -rf ~/Library/Developer/Xcode/DerivedData/`
