# Weapon

Updated for version 3.38. Thanks Pawcio for pretty much all of this info. This info here is mostly based of his template.

This page is missing some information.

You should read [this](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/ScriptData#things-to-know) to understand some things about the XML files in BeardLib.

## Module Definition

The module is inherited from [ItemModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase#ItemModuleBase). So base parameters can be found there.

This modules let's you add weapons.

### Module name

The name of the module you use as the meta of the module definition is 'WeaponMod' or 'WeaponModModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<Weapon>
    <weapon id ...>
        <stats damage spread spread_moving recoil concealment/>
        ...
    </weapon>
    <factory id ...>
        <adds/>
        <override/>
        <default_blueprint>
            <value_node value/>
        </default_blueprint>
        <uses_parts>
            <value_node value/>
        </uses_parts>
    </factory>
    ...
    <stance/>
</Weapon>
```

Many values are optional if their based on weapon already defines them and you don't wish to change them.

#### `<weapon id ...>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String | Unique ID of weapon |
| name\_id | String | Optional localization ID for the name of the gun. Defaults to bm_w_`id`. You'll need to localize it using [LocalizationModule](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/LocalizationModule) |
| desc\_id | String | Optional localization ID for the description of the gun. Defaults to bm_w_`id`\_desc |
| unlock\_level | Number | Required reputation level to unlock |
| based\_on | String | ID of weapon base that the custom weapon will be based on |
| weapon\_hold | String | Optional parameter that is only needed if custom weapon is using incorrect hold animation - In most cases ID is same as used in based\_on |
| global\_value | String | For packs of mods, a global id assigned to all. A nice way to label your mods. You'll still have to create the global value through [GlobalValueModule](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/GlobalValueModule) |
| texture\_bundle\_folder | String | Folder to contain the icon. The path will be guis/dlcs/`texture_bundle_folder`/textures/pd2/mods/icons/weapons/`id`. Defaults to "mods" |
| animations | Table | A table of animation group used by custom weapon:  |
| CLIP\_AMMO\_MAX | Number | Rounds in magazine/etc |
| NR\_CLIPS\_MAX | Number | How many magazines/etc that weapon can have. Note: Both CLIP\_AMMO\_MAX and NR\_CLIPS\_MAX are used to calculate total ammo of weapon in this case: 30 \* 5 = 150 total ammo |
| ammo\_pickup | Number | Optional index used for ammo pickup that defines how min and max values for ammo pickup are calculated. The indices:As we said, this is optional and you can pretty much use the based on's AMMO\_PICKUP. |
| AMMO\_PICKUP | Table | Optional value if you want to set the AMMO\_PICKUP manually without using premade indices. The table needs to have 2 values in the 1st index the low number and in 2nd the high |

muzzleflash\|String\|Optional in-game path to muzzle flash effect\| muzzleflash\_silenced\|String\|Optional in-game path to muzzle flash effect when suppressor is attached\| shell\_ejection\|String\|Optional in-game path to effect used for ejecting cases\| categories\|Table\|Optional ategories that weapons will be present this also has effect on player weapon skills. This can be `assault_rifle`, `smg`, `shotgun`, `pistol`, `lmg`, `snp`, `grande_launcher`, `revolver`, `akimbo`, `saw`, `flamethrower`, `bow`, `crossbow`. Akimbos use both their original category and `akimbo`, and rpgs use `grenade_launcher`. This is optional of course if the based on weapon already defined them. \|stats\|Table\|Unique stats of custom weapon. Available stats parameters and values: \|use\_data\|Table\|Has a value named `selection_index` Inventory slot of weapon: 1 - Secondary 2 - Primary\| fire\_mode\_data\|Table\|Has a value named `fire_rate` Fire rate value: Fire rate in 60 / RPM = Value. Example 60 / 800 RPM = 0.075\| \|stats\_modifiers\|Table\|Has a value named `damage` Modifier that will multiply damage by value. Note: This modifier also applies to attachments. \|sounds\|Table\| \|animations\|Table\|Has a value named `reload_name_id` ID of reload animation\|

And any other value from WeaponTweakData. There are more that are not listed here yet

#### `<factory id ...>`

Holds more data for the weapon.

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String | Unique factory ID of weapon. Defaults to wpn_fps_`id` of `<weapon>` |
| unit | String | Optional path to weapon base unit. Leave empty to use the based on's unit |
| stock\_adapter | String | Optional parameter only needed if weapon will be using AR-15 Stocks. ID = Attachment that use "stock\_adapter" type and will be added to connect weapon model with AR-15 stock models. |
| animations | Table | Some weapons bases use own animations table if custom weapon is missing animations check if chosen base has animations table in the weaponfactorytweakdata script. |
| optional\_types | Table | Types used by weapon \(Currently it's not used by the game but must be defined\). Each value is a string in a value\_node. Types are found [here](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/WeaponModModule#weaponmod-) |
| adds | Table | Adds additional attachments to specific attachment - like rails for sights or gadgets. Contains tables that have their meta as weapon mod ids and inside of these tables are the parts you want to add when using that part |
| override | Table | Allows to override data of attachments used by weapon. Contains tables that have their meta as weapon mod ids and the values of the table contains any data of a weapon mod you wish to change like `unit`, `a_obj`,etc |
| default\_blueprint | Table | List of attachments IDs \(all in a value\_node\) the weapon has by default. Any changes to this list require to sell old gun and repurchase it |
| uses\_parts | Table | IDs of the parts that the gun uses. You must also include the default\_blueprint parts! |
| skip\_thq\_parts | Boolean | Used only for NPC bows |

\*These are all of the values for factory

#### `<stance/>`

Data for the "stance" of the weapon or basically where the guns is on the screen or how much rotated it is. There's one for standing \(standard\), aiming \(steelsight\), crouching\(crouched\), and bipod. The module will inherit the stance of the based on weapon regardless. Example of modifying the stance:

```markup
<stance>
    <standard position="10 10 -5" rotation="Rotation(0, 0, 0)"/>
    <crouched rotation="Rotation(0, 0, 0)"/>
    <shoulders rotation="Rotation(0.1, 0, 0)"/>
</stance>
```

You can get the values for position \(vector3\) and rotation \(Rotation\) using a mod called [PVM](https://modworkshop.net/mydownloads.php?action=view_down&did=17618) Using that mod you can pretty much change the stance to your liking.

#### The icon

The icon will be stored in guis/dlcs/mods/textures/pd2/blackmarket/icons/weapons and will be named `id`.texture then add it using [AddFiles](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/AddFiles).

#### Template

Since this template is more complex and requires other modules \(other than the usual AddFiles, Localization\) You pretty much should depend on the template. Download template [here](https://minhaskamal.github.io/DownGit/#/home?url=https://github.com/ModWorkshop/BeardLib-Templates/tree/master/Weapon-Template)

