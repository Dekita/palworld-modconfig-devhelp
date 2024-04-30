# v1.7 Changelog:
- Mod now automatically creates ~mods folder if it doesnt already exist.
- Made certain ui elements more modular (for use within XMOG Reskin System + other future mods)

# v1.6 Changelog:
- Added NOT: prefix support for 'value objects' reqs. eg: (NOT:MyCustomBooleanOption)
- Added MOD: prefix support for 'value objects' reqs. eg: (MOD:PakMods:DekFF7RSkins_P) (PakMods | PAK, LogicMods | LOGIC, LuaMods | LUA)
- Added additional helper functions for logic mods;
- BPFL Helper: `DekCheckModFileExists` (allows checking for existense of mods)
- BPFL Helper: `DekUnregisterHook` (allows unregistering a registered hook)
- BPFL Helper: `DekRegisterHook` (allows registering hooks similar to lua mods)

# v1.5 Changelog:
- Fix for meta.game flag not responding properly
- Added `AfterClickSavedButton` and `AfterUpdatedConfig` functions to easily hook into from lua
- Added `SetupModConfigBindings` as a bp helper function to easily set event callbacks for `AfterClickSavedButton` and `AfterUpdatedConfig`
- Added sound fx when click buttons etc
- Improved Option Selection Highilight

# v1.4 Changelog:
- Fix for 'string' option type's default empty string text.
- Slight positioning fix for [More Mods] button.
- Added support for 'name' property on "value objects".
- Mod Config Menu can now be opened while in game! (Shift +F6 - Beta feature, see below)
- Added 'reqs' property to make an option only show when some other boolean option is true.
- Added 'hidden' flag for config option to not be shown within config menu (for secret dev config for w.e reason)
- Added 'color' option type for mod developers.
- Added support for boosty donation links.
- Fixed incorrect version display on scene open.
- Added 'keybind' option type for mod developers.
- Minor visual enhancements..

# v1.3 Changelog:
- proper vortex installation support (TY Vortex Extension Team <3)
- fixed scrolling issue (now autoscrolls to top of config options list on click mod name)
- fixed issue with multiline descriptions for configuration options altering the ui position
- added event delegates for `OnResetModConfig` and `OnSavedModConfig` (args: String (mod name), JSON (data))
- added 'header' type for mod developers (to stop them using empty object types as headers)
- added 'meta' data section to modconfig for devs to use
- added mod banner and buttons (for dev to add url links)
- other minor improvements

# v1.2 is now live:
- Fixed issue with "string" type (text input) config options.
- Fixed scaling issue for ultrawide monnitors
- Fixed issue for not showing files (when they are all actually in their correct place) without running game as admin
- Added LUA mod dir scanning for modconfig files - Auto identifies gamepass/steam game version via available WinGDK folder.
- RENAMED the LUA `DekDirectoryScanner` mod portion of this system to `DekModConfigMenu` for consistency in naming.

I feel like there was another thing but i cannot remember...

# v1.1: 
- Disabled Vortex Installation
- Improved general mod structure






Still no vortex installation support - working on it!

More fixes and enhancements coming soon including;
- proper vortex installation
- event delgates (for hooking into when a button is pressed in the ui)
- potential reloading of config during gameplay (maybe...)
- keybind selection options (for mods that have keybinds)

If you are upgrading from v1.1 or earlier, make sure to delete the `DekDirectoryScanner` mod from the Win64/WinGDK folders as those files were completely changed and renamed to DekModConfigMenu for consistency as mentioned above. The latest update will not even try to use their functions. 

NOTE: only mods that have enabled 'game' and have properly bound and react accordingly to the relevant events (`OnResetModConfig` and `OnSavedModConfig`) will be configurable 'on-the-fly' while in game. (Shift+F6 - Beta feature, has to be implimented fully into each individual mod).. Mods that do not support editing in game will be visible while in game, but cannot be altered. 

