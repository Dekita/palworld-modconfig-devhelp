# Skin Json Format Explained:
Note, example data below taken from `~mods/xMOG/DefaultArmors/DefaultHeadEquip005.skin.json`.


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
An array of condition objects (future implementation),

Example JSON: 
```json
{
    "cond": "F"
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


# Known Issues / Limitations

## Weapons


## body Armors
Armor materials dont seem to show unless they are bundled and set with a skeletal mesh that also uses them.
I was thinking maybe something to do with the fact that all default game armor materials seem to be instances of `MI_PalLit_CharacterBodyBase`, which is an instance of `MI_PalLit`, which is an instance of `M_PalLit` (which is where that trail ends thankfully..). So perhaps that chain of inheritance is required or something? Maybe the M_PalLit material sets some property thats unique to armor materials? Not entirely sure why this is - if you know, please let me!

## Head Equip
Head Equipment skins have to use the same socket on the skeleton! eg, `Socket_HairAttach_Ear_L`, `Socket_HairAttach_HeadEquip_front`, `Socket_HairAttach_SmallHat`. These cannot be mixed and matched.. eg: you cannot make a hat replace the mesh for an earing accessory!



[!] More coming soon <3

