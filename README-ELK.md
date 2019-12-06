# JuicySFPlugin

Modified for headless plugin build for [Elk Audio OS](https://elk.audio).

The original plugin is using the GUI to load a soundfont file. As a quick workaround, this one checks the environment variable
```
JUICY_SOUNDFONT_PATH
```

to load a given Soundfont file.

## Build Instructions

The VST2 SDK needs to be available and configured in Projucer.

1. Open `juicysfplugin.jucer` with the Projucer.
3. Navigate to the folder `Builds/LinuxMakefile/`.
4. Set up the cross-compilation toolchain with:  

   ```bash
   $ source /path/to/elk-sika64-sdk/environment-setup-aarch64-elk-linux
   ```

5. (optional) Add flags for more aggressive optimizations than the default ones from the toolchain with:  

   ```bash
   $ export CXXFLAGS="-O3 -pipe -ffast-math -felimnate-unused-debug-types"
   ```

6. Finally cross compile the plugin using:  

   ```bash
   $ AR=aarch64-elk-linux-gcc-ar make CONFIG=Release CFLAGS="-DJUCE_HEADLESS_PLUGIN_CLIENT=1" V=1 TARGET_ARCH="-march=armv8-a -mtune=cortex-a72"
   ```

## Additional notes

* Make sure to use our [JUCE fork](https://github.com/elk-audio/JUCE)
* For further compilation help. Look at our [documentation](https://github.com/elk-audio/elk-docs/blob/master/documents/building_plugins_for_elk.md).

