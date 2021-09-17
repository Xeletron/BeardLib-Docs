# XML

Updated for version 3.38.

## Module Definition

The module is inherited from [ModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase). So base parameters can be found there.

This module is great for organizing your mod into parts. If you always hated putting everything in the same XML but didn't want to use the `file` parameter this makes it easy to organize many modules into separated files.

### Module name

The name of the module you use as the meta of the module definition is 'XML' or 'XMLModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<XML path file_type>
    <load_first/>
</XML>
```

#### `<XML path file_type>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| path | String | The path to the XML file that should be loaded |
| load\_first | Table | An optional list of modules that should load first |
| file\_type | String | The type of file that should load \[Default: custom\_xml\] can be custom\_xml, generic\_xml an json. |

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<XML path="Extra.xml"/>
```

This will load the file Extra.xml and read the modules that are inside of it.

