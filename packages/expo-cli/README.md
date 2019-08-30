# expo-cli-direct

![npm](https://img.shields.io/npm/dw/expo-cli-direct?style=plastic) [![npm version](https://badge.fury.io/js/expo-cli-direct.svg)](https://badge.fury.io/js/expo-cli-direct) ![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)



#### expo-cli-direct is a a modded package from official expo-cli. You can use some expo features without using the expo-cli. Call directly inside your Node.js project, from your React app, or wherever you want.



#### Getting started 
Using Yarn :
```
$ yarn add expo-cli-direct
```
or NPM :
```
$ npm install expo-cli-direct
```
Then, import to your project: 
```js
const expoAccount = require("expo-cli-direct/build/accounts");
const expoPublish = require("expo-cli-direct/build/commands/publish");
const expoBuilder = require("expo-cli-direct/build/commands/build/index")
const expoFetcher = require("expo-cli-direct/build/commands/fetch/index')
;
```
## API

## `expoAccount`
### `login({usernameLogin:<username> , passwordLogin:<password>})`
#### `usernameLogin` (string, required)

The Expo username you want to login.

#### `password` (string, required)

The Expo password you want to login

## `expoPublish`
### `requirePublish(projectPath, options)`
<br>

## `expoBuilder`
### `requestAndroidBuild(projectPath, options)`

### `requestIOSBuild(projectPath, options)`
<br>

### `projectPath` (string, required for `expoBuilder, expoPublish`) 

The Expo project path (initialised by expo-cli or somewhere). `app.json` must be exist. 



### `options` (object, optional, default: `{}`)
By passing `options` to some functions from `expoBuilder`, `expoPublish`, Expo will parse some informations from this object. 

This is an example of `options`: 
```js
const options = {
  wait: true,
  releaseChannel: "default",
  clearCredentials: false,
  type: "simulator"
  appleId: "demo@gmail.com",
  appleIdPassword: "demo123",
  distP12Path: "/home/demo.p12",
  pushP8Path: "/home/demo_apns_key.p8",
  pushId: "AbE9Vx",
  provisioningProfilePath: "/home/demo.mobileprovision",
  p12password: "99Ab3DOvDL=="
};

```
#### `wait` (boolean, optional, default: false)
`wait` let Expo know if Expo continues to run some "heavy" commands such as build, wait. If `wait` is `true`, expoBuilder will run all async functions inside, print all log via console, until the build is completed. `false` let Expo mark the build as completed after it received a "queued" signal.

#### `releaseChannel` (string, required)
Every Expo project need a `releaseChannel`. Use release channels in Expo to send out different versions of your application to your users by giving them a URL or configuring your standalone app. You should use release channels if:
- You have an app in production and need a testing environment.
- You have multiple versions of your app. 

#### `clearCredentials` (boolean, optional, default: false)
*Please read this carefully or go to [Building Standalone App](https://docs.expo.io/versions/v34.0.0/distribution/building-standalone-apps/) for more informations. If you don't know what are you doing, remove this from `options` or make it `false`.*

> Google requires all Android apps to be digitally signed with a certificate before they are installed on a device or updated. Usually a private key and its public certificate are stored in a keystore. In the past, APKs uploaded to the store were required to be signed with the app signing certificate (certificate that will be attached to the app in store), and if the keystore was lost there was no way to recover or reset it. If you opt in to App Signing by Google Play you need to upload an APK signed with an upload certificate, and Google Play will strip that signature and replace it with one generated using the app signing certificate. Both the upload keystore and keystore with the app signing key are essentially the same mechanism, but if your upload keystore is lost or compromised, you can contact the Google Play support team to reset the key.
From the build process's perspective, there is no difference whether an app is signed with an upload certificate or an app signing certificate. Either way, expo build:android will generate an APK signed with the keystore currently assigned to your application. If you want to generate an upload keystore manually, you can do that the same way you created your original keystore.
See [here](https://developer.android.com/studio/publish/app-signing) to find more information about this process.

#### `type` (string, required, default: `simulator` for Android, `archive` for iOS)
`type` dedicate what type of building that Expo should do. There are two build types: `simulator` or `archive`. Request a build with `simulator` mean Expo will perform a build that return a `.apk` file for Android build or `.tar.gz` file for iOS. `archive` let Expo know it's the time to build a `.ipa` file. You will need to your Apple ID account, and passed the two-factor verification to perform this request.

#### `appleId` (string, required, default: undefined)
`appleId` is your Apple ID. Make sure your account is a developer account.

#### `appleIdPassword (string, required, default: undefined)
`appleIdPassword` is your Apple password.

#### distP12Path (string, optional, default: undefined)

### More API and features coming soon. 


## Development

`expo-cli-direct` uses [Lerna.js](https://lerna.js.org/) for fast developing.
Make a change in your file and instantanously see your updates!

### Packages

- `expo-cli`: Expo CLI is the command line interface for developing, building and sharing Expo apps.
- `@expo/dev-tools`: the web-based graphical user interface included in Expo CLI for quickly viewing logs, connecting testing devices, deploying updates and more.
- `xdl`: the Expo development library is a dependency of both the CLI and Dev Tools user interfaces, doing all the heavy lifting behind the scenes.
- `@expo/schemer`: a library for validating [Expo configuration files](https://docs.expo.io/versions/latest/workflow/configuration).
- `@expo/json-file`: a library for reading and writing JSON files.
- `@expo/osascript`: a library for working with `osascript` which runs AppleScript code on macOS.
- `@expo/traveling-fastlane-darwin`/`@expo/traveling-fastlane-linux`: JavaScript wrappers for managing iOS certs, based on [Fastlane](https://fastlane.tools), which is a Ruby based app automation tool.
- 
#### Clone the repository

Open your favorite Terminal and run these commands.


```sh
git clone https://github.com/hyperion0201/expo-direct.git
cd expo-direct
yarn run bootstrap  (Installs dependencies, links and builds packages.)
yarn start (start watching and automatically re-building packages when there are new changes.)
```
#### Publishing a release

To publish a new release, run this command (you must have two-factor authentication enabled for npm):

```
node ./scripts/publish.js
```

The command will bump the versions of all packages with changes since the previous release and publish them in the correct order. For each changed package, it will ask, if the changes require a new _major_ version (breaking changes), _minor_ version (new backwards compatible functionality) or just a _patch_ version (backwards compatible bug fixes).



Original source code from [Expo](http://expo.io/).

License
----
[Expo](http://expo.io/)


