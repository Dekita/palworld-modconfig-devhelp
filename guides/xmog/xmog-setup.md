# Skin Json Format Explained:
Note, example data below taken from `~mods/xMOG/DefaultArmors/DefaultHeadEquip005.skin.json`.


>[!WARNING]  
>If replacing the mesh for the item being reskinned, you MUST ensure that the mesh resides within a unique filepath in your unreal engine project/pak file contents. This path is also recommended to be as short as possible. I personally suggest creating a "SkinMods" folder within your unreal engine project's Content Folder, and then creating a personal subfolder within SkinMods for each of your skin mod paks.. eg: Content/SkinMods/MyDopeSkinMod/MeshAndMaterialFilesForTheModGoHERE



## gend [armor only]
Allows item to be restricted (wont be shown within the ui at all) based on the players gender.
Should be set to the gender of the player as a string, either "F" or "M", Can be left empty (null or completely undefined) to allow skin for any gender.


Example JSON: 
```json
{
    "gend": "F"
}
```

## head [head-equip only]
An object containing various confirable properties for the head when this skinis enabled. The 'hair' boolean should identify if the skin includes hair on the mesh + hair material. 

Example JSON: 
```json
{
    "head": {"hair": false}
}
```

## cond
An array of condition objects (detailed setup coming soon),

Example JSON: 
```json
{
    "cond": ﻿[
        {"type": "level", "req": 5},
        {"type": "paldex", "req": "PalID", "min": 1},
        {"type": "weight", "req": 500.0},
        {"type": "bosskill", "req": "BossID"},
        {"type": "bosskills", "req": 5},
        {"type": "ft-point", "req": "FastTravelPointID"},
    ]
}
```

## item
An array of item id's, that this skin is allowed to be used with,

Example JSON: 
```json
{
    "item": ["Head005", "Head005_2", "Head005_3", "Head005_4", "Head005_5"]
}
```

## icon
Game relative 'soft reference' path for the icon to show within the interface,

Example JSON: 
```json
{
    "icon": "/Game/Others/InventoryItemIcon/Texture/T_itemicon_Armor_Head005.T_itemicon_Armor_Head005"
}
```


## mesh
Game relative 'soft reference' path for the mesh to use for this skin, weapon, armor, equip, etc,

Example JSON: 
```json
{
    "mesh": "/Game/Pal/Model/Character/Player/HeadEquip/HeadEquip005/SK_HeadEquip005.SK_HeadEquip005"
}
```


## mats
An array of game relative 'soft reference' paths, for each material the mesh expects.. Order should match the mesh's expectencies.

Example JSON: 
```json
{
    "mats": [
        "/Game/Pal/Model/Character/Player/HeadEquip/HeadEquip005/MI_HeadEquip005_Hair.MI_HeadEquip005_Hair",
        "/Game/Pal/Model/Character/Player/HeadEquip/HeadEquip005/MI_HeadEquip005.MI_HeadEquip005"
    ]
}
```


## opts
An object, similar to the configuration structure used for [Mod Config Menu](../mcm/mcm-structure.md), but for controlling material instance parameters on the skin. Not all MCM data object types are valid, but boolean, float, and color are! (other options will be shown, but wont affect material parameters)

>[!WARNING]
>This is an advanced feature. Do not try to use this for your skin mod until you have validated basic functionality. 

Example JSON: 
```json
{
    "DiffuseTintColor": {
        "mats": [0],
        "type": "color",
        "init": {"r": 1,"g": 1,"b": 1,"a": 1}
    },
    "FresnelStrength": {
        "mats": [1],
        "type": "float",
        "opts": {"min": 0,"max": 9.9, "step": 0.1},
        "init": 2.5
    }
}
```

With the above example, this would create ui elements within the xMOG interface that control the material instance parameters of the same name. eg, DiffuseTintColor should be a valid parameter for the material instance. assuming it is, then when the value is changed and saved, the material's parameter will be updated. 

The "mats" property is exclusive to skin.json "opts" and is not found within MCM config structure. "mats" should be an array of integers to tell the system which materials this property is allowed to control (in case you wish for some property to control more than one materials params)

- "float" type properties should be used for controlling 'Scalar Parameters'
- "color" type properties should be used for controlling 'Vector Parameters'
- "boolean" type properties should be used for controlling 'Scalar Parameters' (but will set it to either 0.0 or 1.0)

Static Switch parameters cannot be dynamically controlled, hence: static. But...

<img src="https://raw.githubusercontent.com/dekita/palworld-modconfig-devhelp/main/images/scalar-switch.png" style="margin-top: 28px;">


# Complete Examples 
- [Complete Example: Armor](/guides/xmog/xmog-example-armor.json)
- [Complete Example: Weapon](/guides/xmog/xmog-example-weapon.json)


# Known Issues / Limitations

## Armors
- Armors MUST use Material Instances!
- Armor materials dont seem to show unless they are bundled and set with a skeletal mesh that also uses them. I was thinking maybe something to do with the fact that all default game armor materials seem to be instances of `MI_PalLit_CharacterBodyBase`, which is an instance of `MI_PalLit`, which is an instance of `M_PalLit` (which is where that trail ends thankfully..). So perhaps that chain of inheritance is required or something? Maybe the M_PalLit material sets some property thats unique to armor materials? Not entirely sure why this is - if you know, please let me!


## Armors [Head]
- Head Equipment skins have to use the same socket on the skeleton! eg, `Socket_HairAttach_Ear_L`, `Socket_HairAttach_HeadEquip_front`, `Socket_HairAttach_SmallHat`. These cannot be mixed and matched.. eg: you cannot make a hat replace the mesh for an earing accessory!


## Weapons
- Can use Materials/Material Instances



>[!WARNING]  
>More information coming soon <3
