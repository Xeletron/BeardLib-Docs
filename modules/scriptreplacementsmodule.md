# Script Mods \(Replace script data\)

Updated for version 3.38.

## Module Definition

The module is inherited from [ModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase). So base parameters can be found there.

### Module name

The name of the module you use as the meta of the module definition is 'ScriptMods' or 'ScriptReplacementsModule' if `_force_search` is set to true in the module definition.

### XML Structure

There are two ways of modding scriptdata:

#### File

```markup
<ScriptMods directory>
    <mod file type target_path target_type .../>
</ScriptMods>
```

#### Direct

```markup
<ScriptMods directory>
    <mod target_path target_type ...>
        <tbl>
        </tbl>
    </mod>
</ScriptMods>
```

#### `<ScriptMods directory>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| directory | String | string directory/path relative to the mods directory which contains all the script data mods being referenced. \[OPTIONAL\] |

#### `<mod file type target_path target_type, ...>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| file | String | string which is the filename of the script data file relative to the Mod directory and the directory defined in the main node if it was specified. |
| type | String | The script data type of the file you are using for replacement/mod. E.g. custom\_xml, generic\_xml, binary etc |
| tbl | Table | Instead of `file` and `type`, write scriptdata mod directly. |
| target\_path | String | The path of the script data file you are modifying |
| target\_type | String | The extension/type of the script data file you are modifying |

#### Options / Additional parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| use\_clbk | String | Path/name to callback that would be called before scriptdata mod gets applied, if the callback returns true, the scriptdata mod will be applied. Can be "self.UseFunc" or "ClassClbk\(class, 'UseFunc'\)" |
| merge\_mode | String | How should the scriptdata mode be applied, the modes are:`replace` Replaces the scriptdata entirely, default.`merge` Merges with the scriptdata.`script_merge` A dynamic merge with the script, allows you to remove specific parts of the scriptdata, merge with specific parts or replace specifc parts. Read about script\_merge [here](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/table#other) and see examples [here](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/table#script_merge-examples). You can see removal of a part in the example below |

### Examples

In both examples is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

#### File

For this example your script mod would be like this: `mods/MyMod/scriptdata/start_menu.xml`. If you are using this module in a BLT mod.

```markup
<ScriptMods directory="scriptdata">
    <mod file="start_menu.xml" type="custom_xml" target_path="gamedata/menus/start_menu" target_type="menu"/>
<ScriptMods/>
```

#### Direct

```markup
<ScriptMods>
    <mod target_file="units/payday2/characters/ragdoll" target_type="sequence_manager" merge_mode="script_merge">
        <tbl>
            <table search="unit">
                <table mode="remove" search="sequence;name='\'freeze_ragdoll\''"/>
            </table>
        </tbl>
    </mod>
</ScriptMods>
```

