# Options

## Module Definition

The module is inherited from [ModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase). So base parameters can be found there.

### Module name

The name of the module you use as the meta of the module definition is 'Options' or 'OptionModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<Options save_file loaded_callback auto_build_menu auto_load>
    <options name node_name title_id desc_id build_items>
        <merge_data ...> ... </merge_data>
        <option name type value_changed converter enabled_callback default_value disabled title_id desc_id hidden>
            <merge_data ...> ... </merge_data>
        </option>
        <option type="multichoice" values_tbl save_value ...> ...
            <values> <value_node value/> ... </values>
        </option>
        <option type="number" min max step show_value ...> ... </option>
        <option type="bool" ...> ... </option>
        <option type="colour" alpha scale_factor step min max ...> ... </option>
        <option type="vector" scale_factor step min max ...> ... </option>
        <option_group build_menu ...> ... </option_group>
        <option_set not_pre_generated items_tbl populate_items ...>
            <items> </items>
            <item_parameters ...> ... </item_parameters>
        </option_set>
    </options>
</Options>
```

#### `<Options save_file loaded_callback auto_build_menu auto_load>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| save\_file | String | Filename of the save file, relative to the SavePath. \[DEFAULT: 'ModName\_Options.txt'\] |
| loaded\_callback | String | Function path/name of a function which should be called when the Options are loaded. |
| auto\_build\_menu | Boolean | Determines if the menu should be automatically built. \[DEFAULT: True\] |
| auto\_load | Boolean | Determines if the options should be automatically loaded. \[DEFAULT: True\] |

#### `<options name node_name title_id desc_id build_items>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| name | String | The base name of the options group. Only required if it is an option\_set or option\_group. |
| node\_name | String | The name of the node that holds the options. |
| title\_id | String | The localization id of the title of the button for this options node |
| desc\_id | String | The localization id of the description of the button for this options node |
| build\_items | Boolean | Determines if the items in the menu should be created |

#### `<merge_data ...> ... </merge_data>`

_Any additional parameters which should be included in the item/node definition_

#### `<option name type value_changed converter enabled_callback default_value disabled title_id desc_id hidden>`

_Every value type uses these parameters_

| Parameter | Type | Description |
| :--- | :--- | :--- |
| name | String | The name of option \[REQUIRED\] |
| type | String | The option type. Options are `multichoice`, `number`, `bool`, `colour`, `color`, `vector`, `rotation` and `table` |
| value\_changed | String | Function path/name which is called once the value of the option has been changed. This is given the parameters 'name' and 'value' of the option. |
| converter | String | Function path/name which is called to convert the value of option once GetValue param \#2 is given 'true' |
| enabled\_callback | String | Function path/name which should return a bool that determines if the option is enabled |
| default\_value | Any | The default value of the option |
| disabled | Boolean | Determines if the option is disabled |
| title\_id | String | Localization id of the title of the option. \[DEFAULT: ModNameOptionNameTitleID\] |
| desc\_id | String | Localization id of the description of the option. \[DEFAULT: ModNameOptionNameDescID\] |
| hidden | Boolean | Determines if the option is hidden in the menu |

#### `<option type="multichoice" values_tbl save_value ...> ...`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| values\_tbl | String | Path/Name of a table that holds all the values for the multichoice option \(BeardLib reads the string and finds the object with the name/path\) Example: `self.MyValues` or `MyGlobalClass.MyValues` |
| save\_value | Boolean | Determines if the value of the option should be saved or the index. This is useful if you have a variable amount of values which may have ones inserted in the middle or the end and the value should be retained. |

#### `<values> <value_node value/> ... </values>`

_This allows you to define the multichoice items in the xml._ value\_node automatically assigns the index depending on its location inside `<values>`

#### `<option type="number" min max step show_value ...> ... </option>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| min | Number | The minimum value of the option in the menu |
| max | Number | The maximum value of the option in the menu |
| step | Number | The step value of the option in the menu |
| show\_value | Boolean | Determines if the value should be shown on the option in the menu |

#### `<option type="colour" alpha scale_factor step min max ...> ... </option>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| alpha | Boolean | Determines if there should be an option for the alpha of the colour in the menu. |
| scale\_factor | Number | What the values of the colour are scaled up to. E.g. 255 so that it is more intuitive for the user. |
| step | Number | The step of the options for the colour |
| min | Number | The minimum value of the options for the colour |
| max | Number | The maximum value of the options for the colour |

#### `<option type="vector" scale_factor step min max ...> ... </option>`

_`scale_factor`, `step`, `min`, `max`_ Same as in the colour option.

#### `<option type="table"/>`

The table option type is used to save tables into the options config, the menu will not create anything for this item, mostly this item is the same as the others just that default\_value is a table like seen in here:

```markup
<option name="Something" type="table">
    <default_value/>
</option>
```

#### `<option_group build_menu ...> ... </option_group>`

_Same parameters as defined in the main `options` docs. The `option_group` can hold sub\_menus in the form of option\_groups or option\_sets and sub options. The `option_group` is used for grouping of similar options, this will create a sub menu in the parent node for the options._

| Parameter | Type | Description |
| :--- | :--- | :--- |
| build\_menu | Boolean | Determines if this sub menu should be built in the options menu |

#### `<option_set not_pre_generated items_tbl populate_items ...>`

_The option set is used to create a collection of options which have similar parameters. This is used in PD:TH Hud to create the options for Heist Specific colour grading, as it generates the set of options based on the values from the tweak\_data._

| Parameter | Type | Description |  |  |
| :--- | :--- | :--- | :--- | :--- |
| not\_pre\_generated | Boolean | Determines if the options are pre\_generated. This should be used if you are saving options which are not fixed and you just want to store values. This is used in  the BeardLib-Editor to save the prefabs for the map editor. |  |  |
| items\_tbl | String | Path/Name of a table which contains data for the items which are part of the option\_set. It should be setup like a table of sub tables which contains the item parameters for an option, these will overwrite any of the \`item\_parameters |  | that were defined. |
| populate\_items | String | Path/name of a function which returns a table for the items. See: above detail. |  |  |

#### `<items> </items>`

_This can be used to define the items for the option set. See: 'items\_tbl' definition above._

#### `<item_parameters ...> ... </item_parameters>`

_Item parameters as defined in the docs for the 'option' node._

### Example

See: [Mod Template](https://github.com/Luffyyy/BeardLib-Templates/blob/master/BLT%20Mod%20template/main.xml)

## Functions

| Function | Description |
| :--- | :--- |
| SetValue\(String name, Any value\) | Sets value of option `name` \(can be a path to it example ui/hud/color1\) to `value` |
| GetValue\(String name\) | Returns the value of the option `name` |
| GetOption\(String name\) | Return the option `name`. The table pretty much has the same data as defined in the XML but also has "value" |
| ResetToDefaultValues\(String path, Boolean shallow, Boolean no\) | Resets the options. `path` is the path to the option group that should be reset \(leave as an empty string to reset all\), `shallow` determines if the reset should only happen in the current table and not in the sub options too, `no_save` determines if after resetting the options the function shouldn't save the changes |
| Save\(\) | Saves the options |

There are more functions but as they are mostly used in the class itself they are not defined here.

