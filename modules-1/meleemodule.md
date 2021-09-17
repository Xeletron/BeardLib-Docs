# Melee

Updated for version 3.38.

## Module Definition

The module is inherited from [ItemModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase#ItemModuleBase). So base parameters can be found there.

This modules let's you add melee weapons.

### Module name

The name of the module you use as the meta of the module definition is 'Melee' or 'MeleeModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<Melee id global_value unit third_unit .../>
```

#### `<Melee ...>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String | The ID of the melee weapon |
| based\_on | String | An ID of an existing melee you want to base your melee on. Defaults to `kebar`. Full list here [https://modworkshop.net/wiki.php?action=view&id=7\#Melee](https://modworkshop.net/wiki.php?action=view&id=7#Melee) |
| global\_value | String | For packs of mods, a global id assigned to all. A nice way to label your mods. You'll still have to create the global value through [GlobalValueModule](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/GlobalValueModule) |
| unit | String | Optional path to the first person unit Defaults to units/mods/weapons/wpn_mel_`id`/wpn_mel_`id` |
| third\_unit | String | Optional path to the third person unit. Mostly not needed with 3.38 and above |
| name\_id | String | Localization ID for the title \(Defaults to bm_melee_ + `id`\) |
| unlock\_level | Integer | Have a level in which the melee will become available \(1 to 100\) |
| type | String | Optional type of the melee. Defaults to based on melee's one |
| stats | Table | Optional table that holds stats of the melee weapon.`min_damage` Minimum damage of the melee. The in-game damage is the value \* 10. So 30 damage is 3. This damage logic applies to many damage values in the game`max_damage`Maximum damage of the melee`min_damage_effect`A number that gets multiplied by `min_damage` and the result of it is the minimum knockdown value.`max_damage_effect`A number that gets multiplied by `max_damage` and the result of it is the maximum knockdown value.`charge_time` Seconds to charge the melee fully.`range` Range of the melee weapon`concealment` Concealment of the melee. |
| sounds | Table | Optional table of sounds. There are 5 keys and each has a value for the sound. |
| align\_objects | Table | Optional table that is used to align the melee in specific hands or in both. Most melee weapons place it on "a\_weapon\_right". To place it on both you need both sides. "a\_weapon\_left" and "a\_weapon\_right". This is mostly not important if you based on already does that for you. |
| anim\_global\_param | String | Optional animation group for the melee |
| melee\_repeat\_expire\_t | Number | Number of seconds to retract the melee back when swinging/hitting with it |
| expire\_t | Number | Time it takes until the melee weapon is put away after using it |
| repeat\_expire\_t | Number | Time it takes to attack again \(without putting away the melee weapon\) |
| melee\_damage\_delay | Number | Time it takes until the melee deals damage after using it |

#### `<vr locked><offsets>...</offsets></vr>`

_Optional settings for VR_

| Parameter | Type | Description |
| :--- | :--- | :--- |
| locked | Boolean | Lock the melee from being used in VR. This may be because it doesn't support it well |
| offsets | Table | A table of offsets for the melee in VR. Should look like this: `<offsets position="0 0 0" rotation="Rotation(0,0,0)"/>` or `<offsets><left position="0 0 0" rotation="Rotation(0,0,0)"/> <right position="0 0 0" rotation="Rotation(0,0,0)"/></offsets>` To have specific offsets for hands |
| offsets\_npc | Table | Same thing as `offsets` just for npc variants of the melee |

And any other tweakdata value. There are more that are not listed here yet.

#### The icon

The icon will be stored in guis/textures/pd2/blackmarket/icons/melee\_weapons \(unless you use texture\_bundle\_folder\) and will be named `id`.texture then add it using [AddFiles](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/AddFiles).   
Yep, pretty long path. Thanks Overkill.

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<Melee id="captains_shield" based_on="briefcase" global_value="captains_shield"/>
```

This will add the melee `captains_shield`, which is based on the briefcase. You will still need to localize the title and description of the material. In this case `bm_melee_captains_shield` and `bm_msk_troll_dallas_desc` will need to be localized using [LocalizationModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/LocalizationModule). And add unit, object, material\_config, textures and icon through [AddFiles](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/AddFiles)

#### Template

Download template [here](https://minhaskamal.github.io/DownGit/#/home?url=https://github.com/ModWorkshop/BeardLib-Templates/tree/master/Melee-Template)

