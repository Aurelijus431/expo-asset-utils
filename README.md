[![NPM](https://nodei.co/npm/expo-asset-utils.png)](https://nodei.co/npm/expo-asset-utils/)

---

# expo-asset-utils

Utilities for converting files into Expo Assets.
**Uses:**

* Caching remote files
* Parsing `asset-library://` files from ios `CameraRoll`
* Parsing local files from Android's file system
* Preparing assets to be rendered in GL 😁

### Installation

```bash
yarn add expo-asset-utils
```

### Usage

Import the library into your JavaScript file:

```bash
import AssetUtils from 'expo-asset-utils';
```

## Functions

##### resolveAsync

Given a reference to some asset, this will return a promise that resolves to an Expo.Asset.

* Expo asset: `Expo.Asset.fromModule(require('./image.png'))`
* static resource: `require('./image.png')`
* remote image: `'https://upload.wikimedia.org/wikipedia/en/1/17/Batman-BenAffleck.jpg'`
* local file: `'file:///var/image.png'`
* asset library file: `'asset-library:///var/image.png'`
* React Native Image source: `{uri: 'https://upload.wikimedia.org/wikipedia/en/1/17/Batman-BenAffleck.jpg'}`

| Property      |                       Type                        | Description                                      |
| ------------- | :-----------------------------------------------: | ------------------------------------------------ |
| fileReference | `Expo.Asset`, `number`, `string`, `{uri: string}` | This will resolve into a downloaded `Expo.Asset` |

##### fromUriAsync

Given a file URI `string`, this will return an `Expo.Asset` that hasn't been downloaded yet.

| Property  |   Type    | Description                                                            |
| --------- | :-------: | ---------------------------------------------------------------------- |
| remoteUri | `string`  | This remote URI will be downloaded and it's file info will be gathered |
| fileName  | `?string` | This will be assigned to the `Expo.Asset.name`                         |

##### fileInfoAsync

Given a file URI `string`, this will cache the file and collect the `MD5` hash

| Property |   Type    | Description                                                                                                |
| -------- | :-------: | ---------------------------------------------------------------------------------------------------------- |
| uri      | `string`  | This URI (local, remote, asset library) will be cached and it's `MD5` hash will be retrieved               |
| name     | `?string` | This will be assigned to the `Expo.Asset.name`, if not provided the last component of the uri will be used |

### Example

```js
import AssetUtils from 'expo-asset-utils';

const remoteImage = 'https://upload.wikimedia.org/wikipedia/en/1/17/Batman-BenAffleck.jpg';
const asset = await AssetUtil.resolveAsync(remoteImage);
const { localUri, width, height } = asset;
```

### TODO

* Parse remote data format (json containing `uri`)
