# Skin Json Format Explained:
```json 
{
    "gend": The gender of the player as a string, either "F" or "M", Can be left empty to allow skin for any gender (only for armor)
    "head": {"hair": false}, // 'hair' Boolean based on if skin includes hair on the mesh + hair material. only applies to head equip
    "cond": An array of condition objects (future implementation),
    "item": An array of item id's, that this skin is allowed to be used with,
    "icon": Game relative 'soft reference' path for the icon to show within the interface,
    "mesh": Game relative 'soft reference' path for the mesh to use for this skin, weapon, armor, equip, etc,
    "mats": An array of game relative 'soft reference' paths, for each material the mesh expects.. Order should match the mesh's expectencies.
}
```


# Known Issues / Limitations

## Weapons


## body Armors
Armor materials dont seem to show unless they are bundled and set with a skeletal mesh that also uses them.
I was thinking maybe something to do with the fact that all default game armor materials seem to be instances of `MI_PalLit_CharacterBodyBase`, which is an instance of `MI_PalLit`, which is an instance of `M_PalLit` (which is where that trail ends thankfully..). So perhaps that chain of inheritance is required or something? Maybe the M_PalLit material sets some property thats unique to armor materials? Not entirely sure why this is - if you know, please let me!

## Head Equip
Head Equipment skins have to use the same socket on the skeleton! eg, `Socket_HairAttach_Ear_L`, `Socket_HairAttach_HeadEquip_front`, `Socket_HairAttach_SmallHat`. These cannot be mixed and matched.. eg: you cannot make a hat replace the mesh for an earing accessory!



[!] More coming soon <3

