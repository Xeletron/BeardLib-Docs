# Level

## Module Definition

The module is inherited from [ModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase). So base parameters can be found there.

### Module name

The name of the module you use as the meta of the module definition is 'level' or 'LevelModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<level id name_id briefing_id briefing_dialog ai_group_type intro_event outro_event music cube ghost_bonus max_bags team_ai_off>
    <include directory>
        <file file type/>
    </include>
    <add ...>
        ...
    </add>
    <script_data_mods ...>
        ...
    </script_data_mods>
    <hooks ...>
        ...
    </hooks>
    <packages>
        <value_node value/>
    </packages>
    <assets>
        <asset name exclude/>
        <NewAsset ...>
            ...
        </NewAsset>
    </assets>
    <merge_data ... >
        ...
    </merge_data>
</contact>
```

#### `<level id name_id briefing_id briefing_dialog ai_group_type intro_event outro_event music cube ghost_bonus max_bags team_ai_off>`

* `id` string id of the level \[REQUIRED\]. This is used as the key for when it is added to the tweak\_data
* `name_id` The localization id of the title of the level. Defaults to heist\_ID\_name
* `briefing_id` The localization id of the briefing of the level, this is used as the description when you are in the pre-heist lobby
* `briefing_dialog` The sound id of the VO of the briefing\_id
* `ai_group_type` The type of enemies, such as 'default', 'america' or 'russia'
* `intro_event` String ID or table of ids of intro dialog events
* `outro_event` String ID or table of ids of outro dialog events
* `team_ai_off` bool that determines if team ai should be disabled on the heist

#### `<include directory>`

* `directory` The directory relative to the mod path which contains the level files to be included

#### `<add ...> ...`

[AddFilesModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/AddFilesModule) which is used when the level is being played. i.e. to have assets which are designed for your level.

#### `<script_data_mods ...> ...`

[ScriptReplacementsModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ScriptReplacementsModule) which is used when the level is being played. i.e. to have script data which should only be used when the level is being played.

#### `<hooks ...> ...`

[HooksModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/HooksModule) which is used when the level is being played. i.e. to have lua modifications that are used when the level is being played.

#### `<custom_packages>`

Table of packages that should be loaded when playing the level. Packages are the bundle files you see in your assets folder, these contain packages of assets for certain purposes \(like levels\). When including a new package to be loaded you would do `<value_node value="package/name"/>`. This 'value\_node' is how you create a table of values in custom\_xml.

#### `<asset name exclude/>`

* `name` The name if of the asset that you are referencing
* `exclude` bool that determines if your level should be excluded from this asset or included. i.e if exclude is missing or false your level will use this asset, otherwise your level will be included in the 'excluded\_stages'

#### `<NewAsset ...> ...`

* `NewAsset` The key/id of the asset you want to created
* `...` parameters/sub tables that are included in your asset definition.

  NOTE: This may be moved to it's own module if necessary.

#### `<file file type/>`

* `file` The path of the file that should be included for the level. Relative to the mod path and \(if specified\) the directory in the include definition
* `type` The type of script data that the file's data is in. Such as custom\_xml, generic\_xml, binary etc

#### `<merge_data ... > ...`

* `...` Any data which is not in the main level node definition, but you wish to be included in the tweak data definition

### Example

See [MapFramework](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/MapFramework)

## Functions

### LevelModule:RegisterHook\(\)

This registers the Hooks which will add the level to the game. This will be automatically called if the module is being used under the MapFramework. Otherwise it must be manually called, best would be `lib/tweak_data/enveffecttweakdata` as it is the last tweak\_data class to be defined before they are all instantiated.

