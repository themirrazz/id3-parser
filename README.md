# ID3Parser
This is an open-source library that parses metadata from audio data. It's built from the ground up and runs entirely in JavaScript. No dependencies. No borrowed code. And no WebAssembly, either.

## How was it made?
I used [Hexed.it](https://hexed.it/) to look some audio files I had lying around on an old iPod. From there, it was a matter of figuring out how to get it to work.

## How do I use it?
It's very easy. First off, the only functions you need to really use is the ones that parse the metadata. They're always formatted as `ID3Parse.ParseXYZ()`, where XYZ is the file extension or metadata format in all caps. You can either pass an ArrayBuffer, a Uint8Array, or a string (use `ID3Parse.BufferToString(...)` on an ArrayBuffer or Uint8Array to prevent unicode issues.)

Here's a small example.
```js
const response = await fetch('https://media.example.com/never-gonna-give-you-up.mp3');
const buffer = await response.arrayBuffer();
const metadata = await ID3Parse.ParseMP3(buffer);
console.log(`${metadata.title} by ${metadata.artist}`) // Expected output: "Never Gonna Give You Up by Rick Astley"
```

## File Formats
Currently, the following file formats are supported:
* M4A, especially iTunes-compatible ones
* MP3 with ID3v2 Tags (ID3v1 is not support as of right now)

## Known Issues.
* Non-Latin scripts (e.g. Chinese characters, Japanese kana, and Hangul) don't show up correctly. This is due to it reading the binary as raw ASCII.
* Some files may not conform to however this library expects to read it. This can cause missing metadata, or extra unwanted characters inside of metadata.
* The library seems to work best on files where the metadata was either edited or created with iTunes.
