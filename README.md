ForgeAudio
==========

Allows users of trigger.io Forge to play audio files with Javascript.

Installing:

1.  Follow the instructions on trigger.io to enable plugins for your account.  Instructions are found on their website at http://docs.trigger.io/en/v1.4/modules/native/index.html.

2.  From TriggerToolkit, add a new plugin, called "audio".

3.  Replace the "plugin" folder with the "plugin" folder in this project.

4.  Add the plugin to your config.json file

Usage:
The plugin includes methods for playing sound effects (like a click sound) and background music.  Just call the methods using the example Javascript below inside your Forge HTML app.

These methods come as-is without any guarantees!  They at least work with mp3 and aif formats, and possibly others.

I also have the plugin source if you are interested, just send me an email (it's nothing special).

Use the plugin in combination with forge.file.url and forge.prefs for faster playback.

Example:
<pre>
    
    var id = "audio/bg.mp3";
    var url = "http://your_domain.com/" + id;

    forge.prefs.get(id, function(file) {
        if (!file) {
            // store sound and play after stored
            forge.file.cacheURL(url, function(returned_file) {
                // save data in forge prefs for next time
                forge.prefs.set(id, returned_file);
                // and play sound
                forge.internal.call('audio.play_bg', {
                    url : url
                });
            });
        } else {
            // got file from storage
            forge.file.URL(file, 
                function(url) {
                    forge.internal.call('audio.play_bg', {
                        url : url
                    },
                );
            });
        }
    });    
</pre>

*Sound Effects*

**audio.play_sound**

Plays a sound effect one time.

Example:
forge.internal.call(
    'audio.play_sound', 
    { url : "http://path_to_sound.mp3" }
);

**audio.stop_sound**

Stops a sound effect

Example:
forge.internal.call(
    'audio.stop_sound', 
    {}
);

**audio.set_sound_volume**

Adjusts the volume of the sound effects.  The volume passed should be between 0.0 and 1.0.

Example:
forge.internal.call(
    'audio.set_sound_volume', 
    {
        volume : 0.5
    }
);

*Background Music*

**audio.play_bg**

Plays a background music file in an infinite loop.

Example:
forge.internal.call(
    'audio.play_bg', 
    { url : "http://path_to_sound.mp3" }
);

**audio.stop_bg**

Stops the background music.

Example:
forge.internal.call('audio.stop_bg', {});

**audio.set_bg_volume**

Adjusts the volume of the background music.  The volume passed should be between 0.0 and 1.0.

Example:
forge.internal.call(
    'audio.set_bg_volume', 
    {
        volume : 0.5
    }
);

