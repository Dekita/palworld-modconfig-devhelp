

# Mod Config JSON structure
How to add your own mods configuration options into the [Palworld Mod Config Menu](https://www.nexusmods.com/palworld/mods/577) interface by dekitarpg@gmail.com. 

# Basic Configuration Setup
In order for your modconfig.json file to be compatible with the mod config menu, it MUST be an object containing a valid json structure formatted in the way the system expects. 

The following structure details the most basic configurable options - a simple boolean and float (from 0.0-1.0). This is all the json you would need to add the "My Custom Boolean" and "My Custom Floater" options into the mod config menu interface. 

```json
{
    "My First Boolean Option": {
        "type": "boolean",
        "init": true,
        "live": true
    },
    "My First Floater Option": {
        "type": "float",
        "init": 0.5,
        "live": 0.5
    }
}
```

Simply paste this json into a file named "MyAwesomeModsConfig.modconfig.json", add it to the palworld installs Content/Paks/LogicMods folder, and launch the game. It should now be displaying within the MCM interface. 

:exclamation: For LUA mods, place the .modconfig.json file in your Win64/Mods/ModName folder, next to the Scripts folder and any enabled.txt file that may be there. This is where the Mod Config Menu will search for your lua mod's config file. 

## Additional Links: 
- [Full Structure Guide](/guides/mcm/mcm-structure.md)
- [Complete Example](/guides/mcm/mcm-example.md)


# How to read the configuration within your mod? 

## For Blueprint Logic Mods
Use the following nodes within your ue blueprint (assumes you are using Palworld Modding Kit ue project)
- "Get Project Content Directory"
- "Append"  - append `Paks/LogicMods/MyAwesomeModName.modconfig.json` to the content directory
- "LoadJsonFromFile" - make filepath struct and connect to the result from "Append"
- Drag from the Json result gained in "LoadJsonFromFile" and use "Get Field" once to get the desired "Value Object" using its "Key Name". 
- Drag from the json result gained in "Get Field" once to get "live" value of the configuration option.

The result should look something similar to this: 
<img src="https://raw.githubusercontent.com/dekita/palworld-modconfig-devhelp/main/images/getjson-bp-example.png" style="margin-top: 28px;">

At which point, you simply pull the value pin from the final "Get Field" node, and convert it to your desired data type for processing the configuration; integer, float, boolean, or string! 


## For LUA Mods 
You can include a lua library, such as [json.lua](https://github.com/rxi/json.lua), within your lua mod files to parse and handle your mods json configuration file. :)


# Extra
- feel free to request additional information be added. 
- join [my discord server](https://discord.gg/DCXh2TUF2u) if you need some additional guidance in getting things setup for your own mod. 
