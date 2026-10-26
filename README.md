# Vasu Novel Reader

An Android WebView reader for web-novel sites with a built-in **Reader Mode**
overlay, native text-to-speech, page translation and a fully themeable
reading experience.

Package: `com.vasudev.novelreader` · versionName `1.0`

## Features

- **Reader Mode (Shadow DOM)** – the main article text is extracted from any
  novel/blog page and rendered in the app's own overlay, isolated inside a
  Shadow DOM so a website's CSS can never break it (and vice versa).
- **Text to speech** through the phone's own TTS engine – paragraph by
  paragraph, with paragraph highlighting and auto-advance to the next chapter.
- **Background playback** – a foreground service plus an inaudible keep-alive
  oscillator so Chromium never freezes the hidden page.
- **Translation** of the current chapter (Hindi, English, Bengali, Tamil,
  Telugu, Marathi) with a read-aloud option. No API key required.
- **Chapter navigation** – previous / next chapter, a chapter/URL jump box and
  a local history of visited pages.
- **Appearance** – theme mode, reader themes (white/sepia/gray/dark/AMOLED),
  six font families, font size, line height, paragraph spacing, margins,
  bionic reading, custom CSS.
- **Ad blocking** (off by default), offline audio capture, sleep timer, focus
  sessions, gestures, volume-key controls and reading insights.
- **Settings file** export/import, so settings can be moved between devices or
  pushed from a companion settings app.

## Project layout

```
AndroidManifest.xml
com/vasudev/novelreader/     app + WebView + TTS bridge + Reader Mode
com/vasudev/settingsui/      the settings panel (tabs, cards, themes)
res/                         icons, strings, theme
```

## Building

The project is plain Java with no Gradle wrapper and no AndroidX, so it builds
with the standard Android command line tools:

1. Install JDK 17, Android build-tools 35 and platform 35.
2. Compile resources with `aapt2 compile` + `aapt2 link`
   (`--min-sdk-version 24 --target-sdk-version 34 --version-name 1.0`).
3. Compile the Java sources with `javac` (`-source 1.8 -target 1.8`,
   bootclasspath = `android.jar` + `core-lambda-stubs.jar`).
4. Convert to dex with `d8 --release --min-api 24`, add `classes.dex` to the
   APK, `zipalign -f 4`, then sign with **your own** keystore.

> **Signing:** this repository deliberately contains **no keystore and no
> passwords**. Create your own keystore with `keytool` and keep it private.
> Never commit a keystore, a `.jks`, or a signing password.

## Notes

- Reader Mode only takes over real reading pages. Homepages, about, login and
  policy pages are left exactly as the website renders them.
- TTS uses the phone's installed engines – no cloud service, no API key.
- Translation uses free public endpoints; no credentials are stored anywhere.

## License

MIT – see [LICENSE](LICENSE).
