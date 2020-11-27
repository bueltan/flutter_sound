# SoundPlayerUI

## Overview

The SoundPlayerUI provides a Playback widget styled after the HTML 5 audio player.![](https://raw.githubusercontent.com/bsutton/sounds/master/images/SoundPlayerUI.png)

Detailed SoundPlayerUI API documentation can be found on [pub.dev](https://pub.dev/documentation/sounds/latest/sounds/sounds-library.html).

The player displays a loading indicator and allows the user to pause/resume/skip via the progress bar.

You can also pause/resume the player via an api call to SoundPlayerUI's state using a GlobalKey.

The SoundPlayerUI widget allows you to playback audio from multiple sources:

* File
* Asset
* URL
* Buffer

## MediaFormat

When using the `SoundPlayerUI` you MUST pass a `Track` that has been initialised with a supported `MediaFormat`.

The Widget needs to obtain the duration of the audio that it is play and that can only be done if we know the `MediaFormat` of the Widget.

If you pass a `Track` that wasn't constructed with a `MediaFormat` then a `MediaFormatException` will be thrown.

The `MediaFormat` must also be natively supported by the OS. See [MediaFormat](mediaformat.md) for additional details on checking for a supported format.

### Example:

```dart
Track track;

/// global key so we can pause/resume the player via the api.
var playerStateKey = GlobalKey<SoundPlayerUIState>();

void initState()
{
   track = Track.fromAsset('assets/rock.mp3', mediaFormat: Mp3MediaFormat());
}

Widget build(BuildContext build)
{
    var player = SoundPlayerUI.fromTrack(track, key: playerStateKey);
    return
        Column(child: [
            player,
            RaisedButton("Pause", onPressed: () => playerState.currentState.pause()),
            RaisedButton("Resume", onPressed: () => playerState.currentState.resume())
        ]);
}
```

`Sounds` uses [Track](track.md) as the primary method of handing around audio data.

You can also dynamically load a `Track` when the user clicks the 'Play' button on the `SoundPlayerUI` widget. This allows you to delay the decision on what Track is going to be played until the user clicks the 'Play' button.

```dart
Track track;


void initState()
{
   track = Track.fromAsset('assets/rock.mp3', mediaFormat: Mp3MediaFormat());
}

Widget build(BuildContext build)
{
    return SoundPlayerUI.fromLoader((context) => loadTrack());
}

Future<Track> loadTrack()
{
    Track track;
    track = Track.fromAsset('assets/rock.mp3', mediaFormat: Mp3MediaFormat());

    track.title = "Asset playback.";
    track.artist = "By sounds";
}
```

# Flutter Sound UI Widgets API

The modules offered for the Flutter Sound UI Widgets are :

- [UI Player](#uiplayer)
- [UI Recorder](#uirecorder)
- [UI Controller](#uicontroller)

*(This documentation is just a start. It must be completely rewriten)*

## How to use
First import the modules
``` import 'flutter_sound.dart```

Then reference to one of the flutter sound UI widgets in your widget tree:

- [UI Player](../ui_player/ui_player-library.html)
- [UI Recorder](../ui_recorder/ui_recorder-library.html)
- [UI Controller](../ui_controller/ui_controller-library.html)

--------------------------------------------------------------------------------

## `UI Player`

To use add FOREGROUND_SERVICE permission.

### Android

Add this line to your AndroidManifest.xml
```
<uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
```

### Style of the `SoundPlayerUI` widget

The two constructors of the `SoundPlayerUI` widget have 6 optional parameters for allowing the App to tune the UI presentation:

- Color backgroundColor = Colors.grey,
- Color iconColor = Colors.black,
- Color disabledIconColor = Colors.blueGrey,
- TextStyle textStyle = null,
- TextStyle titleStyle = null,
- SliderThemeData sliderThemeData = null,

*...working on documentation.*

--------------------------------------------------------------------------

## `UI Recorder`

*...working on documentation.*

--------------------------------------------------------------------------

## `UI Controller`

*...working on documentation.*

