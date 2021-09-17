# Crime Spree Mission

Updated for version 3.38.

## Module Definition

The module is inherited from [ModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase). So base parameters can be found there.

This module is used to add your level to the crime spree pool

### Module name

The name of the module you use as the meta of the module definition is 'CrimeSpreeMission' or 'CrimeSpreeMissionModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<CrimeSpreeMission id icon level type add>
</CrimeSpreeMission>
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String | Id for the crimespree mission |
| icon | String | A preview texture for the level |
| level | String | The id of the level that is going to be in this crimespree mission |
| type | String | The type of the level, short, medium or long\(if I'm not wrong short is stealth\) |
| add | Number | How much points to add to the crimespree score \[Default: 7\] |
| icon\_rect | Table | A table for the rectangle shape of the image\(x,y,w,h\). This can be used if your picture is inside a sprite texture, usage example: |

```markup
<CrimeSpreeMission id="crimespree_custom" icon="guis/path/to/loaded/texture" level="some_custom_level" type="medium">
    <icon_rect>
        <value_node value="250"/>
        <value_node value="0"/>
        <value_node value="250"/>
        <value_node value="250"/>
    </icon_rect>
</CrimeSpreeMission>
```

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<CrimeSpreeMission id="crimespree_custom" icon="guis/path/to/loaded/texture" level="some_custom_level" type="medium">
```

### Functions

| Function | Description |
| :--- | :--- |
| AddMissionDataToTweak\(crimespree\_tweak\_data, tweak\_data\) | The function that injects the crimespree mission to the crimespree tweak data. Called by the hook created in RegisterHook or from the function RegisterHook itself |

