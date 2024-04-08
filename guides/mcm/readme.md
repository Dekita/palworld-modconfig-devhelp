

# Mod Config JSON structure
How to add your own mods configuration options into the [Palworld Mod Config Menu](https://www.nexusmods.com/palworld/mods/577) interface by dekitarpg@gmail.com. 

# General information
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

Simply paste this json into a file named "MyAwesomeModsConfig.modconfig.json", add it to the palworlds installs Content/Paks/LogicMods folder, and launch the game. It should now be displaying within the interface. 

:exclamation: For LUA mods, place the .modconfig.json file in your Win64/Mods/ModName folder, next to the Scripts folder and any enabled.txt file that may be there. This is where the Mod Config Menu will search for your lua mod config file. 

# Breaking down the structure
Essentially, the json object structure consists of "Key: Value" pairs, where the "Key" is used as the name of the configurable option within the user interface, and the "Value" is an object detailing how the user interface is allowed to manipulate this property. 

For the purpose of this guide, these will be referred to as "Key Names" and "Value Objects".

Each "Value Object" MUST contain at least a "type", "init", and "live" properties. This is the bare minimum required by the system in order to properly control the value as desired within the interface. The ONLY EXCEPTION to this, is the "object" type of "Value Object", which does not have an "init" or "live" properties.

- "type" - defines the type of overall value that this property should store. 
- "init" - defines the initial value for the configuration property. (used whena user presses 'reset' in the ui)
- "live" - stores the live value for this configuration property, potentially modified by the user/the ui.

All "Value Objects" can also optionally include the following properties;

- "name" - the name shown in the interface for the option, if you want to display a different name than the key. 
- "desc" - defines the description shown within the interface info window when the user hovers over this option.
- "reqs" - an array of strings that pair with the "key name" for a "boolean" option type. will only show option when all boolean options specified within the "reqs" property are 'true'.
- "flag" - currently only accepts "when-server-only". This will show an additional [when-server-only] text within the user interface, so that users will know this setting will apply when their game (or the game the mod with its configuration is applied to) is acting as the server. 

Finally, some "Value Objects" support additional properties, such as integer and float "type" supporting options for min and max. A full list of all supported "Value Object" structures is detailed below;

# Value Object Structure Types

## boolean
A standard primative boolean type, can be on or off. (true or false)

Example JSON: 
```json
{
    "My Custom Boolean": {
        "type": "boolean",
        "desc": "awesome description",
        "flag": "when-server-only",
        "init": true,
        "live": true
    }
}
```

## integer
A standard integer number. Allows the user to select a value from a predefined range. (default 0-100)
Allows for an "opts" property, which is an object containing optional "min", "max" and "step" properties, which determine the minimum slider value, the maximum, and the 'step' (amount moved per slider 'tick') respectively.  

Example JSON: 
```json
{
    "My Custom Integer": {
        "type": "integer",
        "desc": "some description..",
        "flag": "when-server-only",
        "opts": { "min": 69, "max": 420, "step": 2 },
        "init": 69,
        "live": 69
    }
}
```

## float
A standard floating point number. Works same as integer, but doesnt round. (default 0.0-1.0) 

Example JSON: 
```json
{
    "My Custom Floater": {
        "type": "float",
        "desc": "some description..",
        "flag": "when-server-only",
        "opts": { "min": 0.25, "max": 0.75, "step": 0.05 },
        "init": 0.5,
        "live": 0.5
    }
}
```

## string
A regular string type. Allows the user to edit the text. 

Example JSON: 
```json
{
    "My Custom String": {
        "type": "string",
        "desc": "some description..",
        "flag": "when-server-only",
        "init": "im the initial text",
        "live": "im live"
    }
}
```

## option
Stores a string as the live value, but allows a selection of predefined options to the user. Intended as an alternative to "string" type, when the user should not be allowed to enter text. "opts" should be an array of the available string options the user can select from. 

Example JSON: 
```json
{
    "My Custom Option": {
        "type": "option",
        "desc": "some description.",
        "opts": ["Option 1","Option 2", "Option 3"],
        "init": "Option 2",
        "live": "Option 2"
    }
}
```


## color
Stores an rgba object as the live value that allows the user to select a custom color. Intended to do exactly that, and offer devvevlopers the ability to provide customizable color options.

Example JSON: 
```json
{
    "My Custom Color": {
        "type": "color",
        "desc": "The text color used for the custom server button",
        "init": { "r": 0.623961, "g": 0.879623, "b": 0.955974, "a": 1 },
        "live": { "r": 0.623961, "g": 0.879623, "b": 0.955974, "a": 1 }
    }
}
```

## keybind
Stores an object with key, bShift, bCtrl, bAlt, and bCmd properties which relates to an unreal engine key chord struct. This option allows for the developer to provide customizable keybind options to users. 

Example JSON: 
```json
{
    "My Custom Keybind": {
        "type": "keybind",
        "desc": "This is an example keybind",
        "init": {"key": "F6","bShift": false,"bCtrl": false,"bAlt": false,"bCmd": false},
        "live": {"key": "F6","bShift": false,"bCtrl": false,"bAlt": false,"bCmd": false}
    }
}
```



## object
Allows further nesting of other "Value Objects".. Intended for use as a categorization header to seperate various options into more managable segments within the ui. Helpful for mods that feature a lot of various configurables. 

Only supports the "type" and a "data" properties, where "data" is an object containing "Key Name: Value Object" pairs. (similar to the root object within the json file). However, other properties you define should be preserved. This is helpful if you wish to add a "desc" field for your own notes (may also be implemted in the ui in future updates) 

Example JSON: 
```json
{
    "My Custom Object": {
        "type": "object",
        "data": {
            "Object Option 1": {
                "type": "boolean",
                "init": true,
                "live": true
            },
            "Object Option 2": {
                "type": "float",
                "init": 0.5,
                "live": 0.5
            }
        }
    }
}
```

## header
A basic header type. Added in v1.2 to stop developers from using empty object types as headers to split options. Headers also only support "type" and "desc" properties.
```json
{
    "My Custom Header": {
        "type": "header",
        "desc": "This is a header, it's just for looks."
    }
}
```

## test
A simple boolean flag that can be set in the root level object. Will cause the 'save' button to save to a `testconfig.json` file rather than `modconfig.json`.
```json
{
    "test": true
}
```

## meta
Another root level option that allows the mod developer to add basic information into the config menu. This includes setting the mod version information, as well as links to the mod on nexus and curseforge!

"game" should be set to `true` if you want to allow for your mod to be configurable while in game. This is a feature intended for v1.3. You should only set this if you have setup callbacks / event bindings for `OnResetModConfig` and `OnSavedModConfig`. This tells the MCM that your mod is ready to be re-configured while in game.

"vers" should be set to the current mod version release.

"auth" should state the name of the mod author.

"desc" should describe the general purpose of the mod.

"link" is an object containing 3 optional properties; "nexus-mod-id", "curse-slug", and "donate". "nexus-mod-id" should be exactly that - the mod id for your mod on nexus mods. "curse-slug" is the url slug path for your mod on curseforge. "donate" allows for either patreon, paypal, ko-fi, or boosty links to be set.  
```json
{
    "meta": {
        "game": false, 
        "vers": "2.0", 
        "auth": "DekitaRPG", 
        "desc": "some description",
        "link": {
            "nexus-mod-id": "577",
            "curse-slug": "miscellaneous/mod-config-menu",
            "donate": "https://www.patreon.com/DekitaRPG"
        }
    }
}
```

# Complete JSON Example 
```json
{
    "test": true,
    "meta": {
        "game": false, 
        "vers": "1.0", 
        "auth": "DekitaRPG", 
        "desc": "This is an example for custom mod configuration structure",
        "link": {
            "nexus-mod-id": "577",
            "curse-slug": "miscellaneous/mod-config-menu",
            "donate": "https://www.patreon.com/DekitaRPG"
        }
    },
    "My First Boolean Option": {
        "type": "boolean",
        "init": true,
        "live": true
    },
    "My First Floater Option": {
        "type": "float",
        "init": 0.5,
        "live": 0.5
    },
    "My Custom Boolean": {
        "type": "boolean",
        "desc": "awesome description",
        "flag": "when-server-only",
        "init": true,
        "live": true
    },
    "My Custom Header": {
        "type": "header",
        "desc": "This is a header, it's just for looks."
    },
    "My Custom Integer": {
        "type": "integer",
        "desc": "some description..",
        "flag": "when-server-only",
        "opts": { "min": 69, "max": 420, "step": 2 },
        "init": 69,
        "live": 69
    },
    "My Custom Floater": {
        "type": "float",
        "desc": "some description..",
        "flag": "when-server-only",
        "opts": { "min": 0.25, "max": 0.75, "step": 0.05 },
        "init": 0.5,
        "live": 0.5
    },
    "My Custom String": {
        "type": "string",
        "desc": "some description..",
        "flag": "when-server-only",
        "init": "im the initial text",
        "live": "im live"
    },
    "My Custom Option": {
        "type": "option",
        "desc": "some description.",
        "opts": ["Option 1","Option 2", "Option 3"],
        "init": "Option 2",
        "live": "Option 2"
    },
    "My Custom Color": {
        "type": "color",
        "name": "I'm some custom name shown",
        "reqs": ["My Custom Boolean"],
        "desc": "The text color used for the custom server button",
        "init": { "r": 0.623961, "g": 0.879623, "b": 0.955974, "a": 1 },
        "live": { "r": 0.623961, "g": 0.879623, "b": 0.955974, "a": 1 }
    },
    "My Custom Keybind": {
        "type": "keybind",
        "desc": "This is an example keybind",
        "reqs": ["My Custom Boolean"],
        "init": {"key": "F6","bShift": false,"bCtrl": false,"bAlt": false,"bCmd": false},
        "live": {"key": "F6","bShift": false,"bCtrl": false,"bAlt": false,"bCmd": false}
    }, 
    "My Custom Object": {
        "type": "object",
        "data": {
            "Object Option 1": {
                "type": "boolean",
                "init": true,
                "live": true
            },
            "Object Option 2": {
                "type": "boolean",
                "init": true,
                "live": true
            }
        }
    }
}
```


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

At which point, you simply pull the value pin from the final "Get Field" node, and convert it to your desired data type for processing the confgiruation; integer, float, boolean, or string! 


## For LUA Mods 
- coming soon (once i figure out how)

# Extra
- feel free to request additional information be added. 
- join [my discord server](https://discord.gg/DCXh2TUF2u) if you need some additional guidance in getting things setup for your own mod. 
