## PersistentStreamPlayer

Example usage:

```
PersistentStreamPlayer *remoteAudioPlayer = [[PersistentStreamPlayer alloc] initWithRemoteURL:myHTTPURL
                                                                                     localURL:myFileURL];
remoteAudioPlayer.delegate = self;
[remoteAudioPlayer play];
```

Features:

* streaming of audio file, starting playback as soon as first data is available
* **also** saves streamed data to a file URL as soon as the buffer completes
* exposes `timeBuffered`, helpful for displaying buffer progress bars in the UI
* handles re-starting the audio file after the buffer stream stalls (e.g. slow network)
* simple `play`, `pause` and `destroy` methods (`destroy` clears all memory resources)
* does not keep audio file data in memory, so that it supports large files that don't fit in RAM

The `PersistentStreamPlayerDelegate` protocol has some helpful event indicators

```
/* called when the data is saved to localURL */
- (void)persistentStreamPlayerDidPersistAsset:(PersistentStreamPlayer *)player;

/* called when the audio file completed */
- (void)persistentStreamPlayerDidFinishPlaying:(PersistentStreamPlayer *)player;

/* called when the play head reaches the buffer head */
- (void)persistentStreamPlayerStreamingDidStall:(PersistentStreamPlayer *)player;

/* called as soon as the asset loads with a duration, helpful for showing a duration clock */
- (void)persistentStreamPlayerDidLoadAsset:(PersistentStreamPlayer *)player;

/* on failure to load asset */
- (void)persistentStreamPlayerDidFailToLoadAsset:(PersistentStreamPlayer *)player;
```