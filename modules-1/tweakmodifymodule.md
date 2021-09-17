# Tweak Modify

Updated for version 3.38.

## Module Definition

The module is inherited from [ItemModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase#ItemModuleBase). So base parameters can be found there.

This modules let's you change tweakdata through XML. The module uses [TweakDataHelper](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/TweakDataHelper) to inject to the tweakdata.

### Module name

The name of the module you use as the meta of the module definition is 'TweakModify' or 'TweakModifyModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<TweakModify overwrite normalize>
    <tweak path data overwrite normalize/>
</TweakModify>
```

#### `<tweak path data overwrite/>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| path | String | Path to the data in tweak\_data that you wish to "modify/overwrite". For example: narrative/jobs \(tweak\_data.narrative.jobs\) or "dlc" \(tweak\_data.dlc\) |
| data | Any | The data that should merge with it/overwrite it. This can be a table, string, number etc |
| overwrite | Boolean | Determines if the data should be overwritten. Non table values are always overwritten. |
| normalize | Boolean | Determines if the data should be "normalized". This let's us write values like Color and Rotation which normally not supported \(The game will read it as a string\) |

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<TweakModify>
    <tweak path="screen_colors/button_stage_2" data="Color(0.5, 0.3, 0.6)" normalize="true"/>
</TweakModify>
```

This changes one of the button colors in many areas of the game \(Modifies tweak\_data.screen\_colors.button\_stage\_2\)

