# expo-music-info-2
New version of expo-music-info library. Compatible with Expo !

Expo-compatible React Native audio metadata extractor.

Pure JavaScript.
Supports ID3v2.3.0 and ID3v2.4.0 tags (no flags).

## Getting started
```
expo install expo-music-info-2
```
Or
```
npm i --save expo-music-info-2
```
Or
```
yarn add expo-music-info-2
```
## Usage
Use this module to retrieve audio metadata from file URI.

```
MusicInfo.getMusicInfoAsync(fileUri, options);
```

Example:
```
import {MusicInfo} from 'expo-music-info-2';


const readMP3Tags = async (uri: string) => {
  try {
    let metadata = await MusicInfo.getMusicInfoAsync(uri, {
      title: true,
      artist: true,
      album: true,
      genre: true,
      picture: true,
    });
return metadata
  } catch (error) {
    console.error("Error fetching MP3 files:", error as Error);
  }
};

###use readMP3Tags() anywhere
```

Result:
```
MusicInfo {
  "title": "Far from love",
  "album": "Missquerada",
  "artist": "Missquerada",
  "picture": Object {
    "description": "",
    "pictureData": "data:image/jpeg;base64,/9j/4AAQSkZJRgABAgEASABIAAD...
  }
}
```
If the specified audio file has incorrect/unsupported ID3 tag format, the resulting object will be null.

## Options
Specify the information you are interested in. If the audio file's metadata doesn't include specified info, it will have null value in the resulting object.

| Option  | Type    | Default | Description                                        |
|---------|---------|---------|----------------------------------------------------|
| title   | boolean | true    | Whether to include ```TIT2``` tag frame text data. |
| artist  | boolean | true    | Whether to include ```TPE1``` tag frame text data. |
| album   | boolean | true    | Whether to include ```TALB``` tag frame text data. |
| genre   | boolean | false   | Whether to include ```TCON``` tag frame text data. |
| picture | boolean | false   | Whether to include ```APIC``` tag frame data - cover picture's text description and Base64-encoded image binary data. |
