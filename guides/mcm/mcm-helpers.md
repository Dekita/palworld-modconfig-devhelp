# Mod Config Menu Helpers

## Event Bindings Setup Guide
You can hook into the `AfterClickSavedButton` and `AfterUpdatedConfig` functions easily from lua, but for blueprint mods, you can create an event or function in your blueprint named `SetupModConfigBindings` that accepts three string parameters. One for a unique identifier that should match your xxxyyz.modconfig.json filename, eg: xxxyyz. The remaining two parameters define the callback function names for saved/updated events respectively. 

It should look somewhat similar to the image below;

<img src="https://raw.githubusercontent.com/dekita/palworld-modconfig-devhelp/main/images/setup-bindings-example.png" style="margin-top: 28px;">



## Check mod file existence:
Create a function within your blueprint named `DekCheckModFileExists` that takes two string arguments, one for the directory to check, and another for the mod's pak file name, or if it is an lua mod, its mod folder name. The function should have a single return value boolean that will be true if the file has been found.

It should look like the image below;

<img src="https://raw.githubusercontent.com/dekita/palworld-modconfig-devhelp/main/images/check-required-mod.png" style="margin-top: 28px;">

