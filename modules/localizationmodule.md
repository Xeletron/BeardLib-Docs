# Localization

Updated for version 4.0.

## Module Definition

The module is inherited from [BasicModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/BasicModuleBase). So base parameters can be found there.

### Module name

The name of the module you use as the meta of the module definition is 'Localization' or 'LocalizationModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<Localization directory default>
    <loc language file/>
</Localization>
```

#### `<Localization directory default>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| directory | String | Sirectory/path relative to the mods directory which contains all of the localization files you are referencing. \[OPTIONAL\] |
| default | String | File name which is the default localization file if the game's language does not have an appropriate localization file in your xml definition |

#### `<loc language file/>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| localization | String | The meta. Can be either `localization` or `loc` |
| file | String | File name of the localization file relative to the ModPath \(And `directory` if specified\). The file can be a json file or a YAML file \(extension must end with .yaml to use YAML\) |
| language | String | Representation of the language that this localization file is for. Languages that are supported in the game already. Or were added through modding like Korean |

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<Localization directory="Lang" default="english.txt">
    <loc file="english.txt" language="english"/>
    <loc file="russian.txt" language="russian"/>
</Classes>
```

For this example your class like this: `mods/MyMod/Lang/english.txt` and `mods/MyMod/Lang/russian.txt`. If you are using this module in a BLT mod.

Or if you only have English in your mod:

```markup
<Localization directory="Lang" default="english.txt"/>
```

### Functions

| Function | Description |
| :--- | :--- |
| LoadLocalization\(\) | The function loads the localization files. The function is called from the `Load()` function either from the function itself \(If localization manager is available\) or from the `LocalizationManagerPostInit` hook. |

