# AMGSoundManager

[![CI Status](http://img.shields.io/travis/Albert M/AMGSoundManager.svg?style=flat)](https://travis-ci.org/Albert M/AMGSoundManager)
[![Version](https://img.shields.io/cocoapods/v/AMGSoundManager.svg?style=flat)](http://cocoapods.org/pods/AMGSoundManager)
[![License](https://img.shields.io/cocoapods/l/AMGSoundManager.svg?style=flat)](http://cocoapods.org/pods/AMGSoundManager)
[![Platform](https://img.shields.io/cocoapods/p/AMGSoundManager.svg?style=flat)](http://cocoapods.org/pods/AMGSoundManager)

## Usage

To run the example project, clone the repo, and run `pod install` from the Example directory first.

## Requirements

AMGSoundManager requires ios 6.0 and above.

## Installation

AMGSoundManager is available through [CocoaPods](http://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod "AMGSoundManager"
```

## How it works

AMGSoundManager works as a sigleton instance that manages all audios that are playing across differents screens.

To create the singleton just write:

```
[AMGSoundManager sharedManager]
```

To play an audio, AMGSoundManager provides multiple options:

```
-(BOOL)playAudioAtPath:(NSString *)audioPath;
-(BOOL)playAudioAtPath:(NSString *)audioPath withName:(NSString *)name;
-(BOOL)playAudioAtPath:(NSString *)audioPath withName:(NSString *)name inLine:(NSString *)line;
-(BOOL)playAudioAtPath:(NSString *)audioPath withName:(NSString *)name inLine:(NSString *)line withVolum:(float)volum;
-(BOOL)playAudioAtPath:(NSString *)audioPath withName:(NSString *)name inLine:(NSString *)line withVolum:(float)volum andRepeatCount:(int)repeatCount;
```

As you can see, you can simply play an audio with just it's path. But also you can specify a name, line, volume and repeat count. 
If repeat count is -1, the audio makes a loop.

The name is used to identify a single sound (or a group of sounds with the same file, or whatever you want) and the line is normally used to identify a kind of sounds such as sfx, voices, background sounds, etc. But it's up to you what name and line you want to put in every sound.

Then, you can stop the audios with the following methods:

```
-(void)stopAllAudios;
-(void)stopAllAudiosForLine:(NSString *)line;
-(void)stopAllAudiosWithoutLine;
-(void)stopAudioWithName:(NSString *)name;
-(void)stopAudioWithPath:(NSString *)path;
```

Also, if you want to check if an audio is currently playing you can wirte:

```
-(BOOL)isAudioPlayingInLine:(NSString *)line;
-(BOOL)isAudioPlayingInLine:(NSString *)line withName:(NSString *)name;
```

You can also pause and resume an audio:

```
-(void)pauseAudiosInLine:(NSString *)line;
-(void)resumeAudiosInLine:(NSString *)line;
```

And the most awesome feature: you can change the volume of any audio currently playing!

```
-(void)setVolume:(float)volum forLine:(NSString*)line;
```

AMGSoundManager also implements a delegate to notify when an audio has finished or has given some kind of error.
With this, you can make a sequence of audios.

```
-(void)audioDidFinish:(NSString *)name inLine:(NSString *)line;
-(void)audioErrorOcurred:(NSString *)name inLine:(NSString *)line;
```

## Examples

Run a background sound:

```
if(![[AMGSoundManager sharedManager] isAudioPlayingInLine:@"background"]){
    [[AMGSoundManager sharedManager] playAudioAtPath:[[NSBundle mainBundle] pathForResource:@"background_music" ofType:@"mp3"]
                                            withName:@"ambient"
                                              inLine:@"background"
                                           withVolum:0.3
                                      andRepeatCount:-1];
}
```

To stop all audios in a line:

```
[[AMGSoundManager sharedManager] stopAllAudiosForLine:@"background"];
```

To change the volume of an audio in live:

```
[[AMGSoundManager sharedManager] setVolume:2.0 forLine:@"background"];
```

## License

AMGSoundManager is available under the MIT license. See the LICENSE file for more info.
