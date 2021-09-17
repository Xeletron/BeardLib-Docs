# Keybind

Updated for version 3.38.

## Module Definition

The module is inherited from [ModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase). So base parameters can be found there.

The module uses almost the same parameters of the BLT json keybinds [https://payday-2-blt-docs.readthedocs.io/en/latest/mods/definition/\#json-keybinds](https://payday-2-blt-docs.readthedocs.io/en/latest/mods/definition/#json-keybinds)

### Module name

The name of the module you use as the meta of the module definition is 'Keybind' or 'KeybindModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<Keybind id name description localized run_in_game run_in_menu script_path/>
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id/keybind\_id | String | a string id for the keybind\[make sure its unique as possible\] |
| name | String | string of the title/id that will show up as the title in the keybinds menu |
| description | String | string of the description/id that will show up as the description in the keybinds menu |
| localized | Boolean | Determines if the menu should use the name and description as localization keys\[DEFAULT: true\] |
| run\_in\_game | Boolean | Determines if the keybind can be used in game \[DEFAULT: true\] |
| run\_in\_menu | Boolean | Determines if the keybind can be used in menu \[DEFAULT: true\] |
| script\_path | String | path to the script that the keybind will be running \[ModPath + script\_path\] |

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<Keybind keybind_id="mykeybind" name="My keybind" description="Runs a script!" localized="false" script_path="Script.lua"/>
```

This will add a keybind to mod keybinds menu similar to BLT's Json ones. when the key that the keybind is set to is pressed, this will run the script in 'script\_path'.

