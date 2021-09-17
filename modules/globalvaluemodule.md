# Global Value \(Tagging weapons/etc\)

Updated for version 3.38.

## Module Definition

The module is inherited from [ModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase). So base parameters can be found there.

Let's you make a global value. A global value is a great way to label your custom weapons, melee etc. You'll see a lot of times weapons saying "This is an X weapon!" This is basically it. Almost all custom item modules have a parameter named `global_value` which you set to the ID of this module that you create.

### Module name

The name of the module you use as the meta of the module definition is 'GlobalValue' or 'GlobalValueModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<GlobalValue id overwrite name_id desc_id color is_category/>
```

#### `<GlobalValue ...>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String | The ID of the global value |
| color | Color | The color of the global value |
| overwrite | Boolean | Skips the ID check if the global value already exists and overwrites it |
| name\_id | String | String ID of the title \[Default: bm_global\_value_`id`\] |
| desc\_id | String | String ID of the description \[Default: menu_l\_global\_value_`id`\] |
| is\_category | Boolean | Makes the global value a category |

And any value that is used in the LootDropTweakData.global\_values

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<GlobalValue id="beard" color="Color('ffffff')"/>
```

This will add a DLC named beard. You will need to localize name\_id and desc\_id \([LocalizationModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/LocalizationModule)\)

