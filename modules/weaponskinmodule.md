# Weapon Skin

Updated for version 3.38.

This page is missing some information, such as explaining what is skin\_folder and how to load the skins themselves.

## Module Definition

The module is inherited from [ItemModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase#ItemModuleBase). So base parameters can be found there.

### Module Name

The name of the module you use as the meta of the module definition is 'WeaponSkin' or 'WeaponSkinModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<WeaponSkin id weapon_id name desc rarity skin_folder locked unique_name>
    <skin_attachments>
        <value_node value="weapon_mod_id"/>
    </skin_attachments>
</WeaponSkin>
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String | The id of your skin, which will be added in the tweak data table. It must be unique and not used by another skin |
| weapon\_id | String | The weapon id that the skin will be attached to. For a full list check here: [https://modworkshop.net/wiki.php?action=view&id=7](https://modworkshop.net/wiki.php?action=view&id=7) |
| weapon\_ids | Table | Like weapon\_id but allows to set multiple weapons |
| name | String | The string id that the skin will use as a name |
| desc | String | \(Optional\) If used, it will show a description below the skin name in the inventory |
| rarity | String | The skin rarity. Can be one of the following : `common`, `uncommon`, `rare`, `epic`, `legendary` |
| locked | Boolean | \(Optional\) If set to true, it will act like the old legendary skins and won't allow the weapon modification if the skin is applied |
| unique\_name | String | \(Optional\) If set to true, it will make the current weapon name the same as the skin name in the player's inventory. They cannot modify it afterwards |
| texture\_bundle\_folder | String | \(Optional\) The folder that contains the textures |

skin\_folder\|String\|...\| \|skin\_attachments\|Table\|The attachments that should be added to the weapon if the skin is applied\|

And any value that appears in the tweak\_data should merge

For Idstrings you need to write them like `param="@ID0d8ea9bdcebaaf64@".` Sadly there's no way to write it using a raw string. Use Bundle Modder to get the hashes.

#### Skin Attachments

Another optional option, you can setup attachments for your skin, working the same as most of rare/epic/legendary skins in the game.

| Parameter | Type | Description |
| :--- | :--- | :--- |
| weapon\_mod\_id | String | The weapon mod id that will be automatically added when the player use your skin |

**Note** You must include the 'base' parts as well, otherwise, the weapon will have no body or barrel. For a list of attachments, check the tweak data tables or here: [https://modworkshop.net/wiki.php?action=view&id=2](https://modworkshop.net/wiki.php?action=view&id=2) and [https://modworkshop.net/wiki.php?action=view&id=3](https://modworkshop.net/wiki.php?action=view&id=3)

### Examples

These examples are what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<WeaponSkin id="colt_infinite_red" weapon_id="new_raging_bull" name="bm_wskn_infinite_red" rarity="uncommon" skin_folder="InfiniteRed" />
```

```markup
<WeaponSkin id="colt_infinite_red" weapon_id="new_raging_bull" name="bm_wskn_infinite_red" rarity="uncommon" skin_folder="InfiniteRed">
    <skin_attachments>
        <value_node value="wpn_fps_pis_rage_g_ergo" />
        <value_node value="wpn_fps_pis_rage_b_long" />
        <value_node value="wpn_fps_pis_rage_body_smooth" />
    </skin_attachments>
</WeaponSkin>
```

This will add a uncommon skin named "bm\_wskn\_infinite\_red" to the weapon "new\_raging\_bull".

