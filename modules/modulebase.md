---
description: Parameters that all modules use.
---

# ModuleBase

Updated for version 3.38.

## ModuleBase

### XML Structure

```markup
<ModuleName file name post_init_clbk ...>
    ...
</ModuleName>
```

#### `<ModuleName file name post_init_clbk ...>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| ModuleName | Meta | The registered key or class name of the module |
| name | String | \[OPTIONAL\] unique name which is used as the key when it is being placed in the mod's table. Only really required if you wish to have a different name than the Modules `type_name` or you have multiple of the same module |
| init\_clbk | String | Path/name to the function which is called when the init function is called \(after the config has loaded of course\) |
| post\_init | String | Path/name to the function which is called when the PostInit function is called |
| file | String | String file path to an individual file which will be used as the module configuration |
| file\_type | String | Type of file to load if using `file`. Defaults to `custom_xml`. Can be `custom_xml`, `generic_xml`, `json` and `binary`. |

### Head variables

| Variable | Type | Description |
| :--- | :--- | :--- |


type\_name\|String\|The name of the module. This is used when the module is registered with `BeardLib:RegisterModule` Example: "Weapon"\| required\_params\|Table\|Required parameters for the module to have. For example ItemModuleBase has "id" as a required parameter\| \|auto\_load\|Boolean\|Should the :Load\(\) function be automatically called? This is set to true in this class but not in ItemModuleBase \(doesn't use it actually\) and not in some select few modules\| \_loose\|Boolean\|Decides if the module can be used a few times in the same mod. True by default for ItemModuleBase\|

### Functions

| Function | Description |
| :--- | :--- |
| init\(ModCore mod, Table config\) | Initializes the module  `core_mod` The mod table.   `config` A table which contains the module configuration |
| Load\(\) | Loads the module. This is called after the mod has been initialized and is ready to load the modules' code. **Note**: Not all modules use this function to load. |
| PostInit | A function called after all modules of the mod were loaded. This is useful when you need a little late point to load the module |
| Log\(String str, ...\) | A log function. The parameters act like string.format |

Err\(String str, ...\)\|Logs an error message to the console \(\[ERROR\] + message\). The parameters are like in string.format. The errors get logged and shown in errors dialog if developer mode is active\| Warn\(String str, ...\)\|Logs a warning message to the console \(\[WARN\] + message\). The parameters are like in string.format\| \|LogErr\(...\)\|Same as `Err` but never adds the error to the errors dialog\| \|GetPath\(String directory, String prev\_dir\)\|A simple function used by some modules to join paths. if prev\_dir is null it will use ModPath instead.

## ItemModuleBase

_Inherits ModuleBase_

The class is used to load "item" type modules, such as weapons. Also when you need to add something to the tweak\_data as it doesn't fully load if you try to call it from Load\(\) or PostInit\(\).

### XML Structure

Like ModuleBase but adds the following:

| Parameter | Type | Description |
| :--- | :--- | :--- |
| register\_hook | String | Path/name to the function which is called before calling RegisterHook |
| post\_register\_hook | String | Path/name to the function which is called after calling RgisterHook |

### Head variables

| Variable | Type | Description |
| :--- | :--- | :--- |
| clean\_table | Table | Set of rules for cleaning the table. See `DoCleanTable` for usage |

### Functions

| Function | Description |
| :--- | :--- |
| DoRegisterHook | Called by the framework's RegisterHooks function. Calls `register_hook_clbks` value \(if exists\) and then calls RegisterHook to load the module |
| RegisterHook | Loads the module. In most modules of this type we are adding hooks to bunch of tweakdata classes to add our stuff |
| DoCleanTable\(Table config\) | Cleans the configuration of the module depending on the `clean_table` variable. Doesn't do anything if the variable is empty. Usage:   `MyModule.clean_table = {{param = "tbl", action = "remove_metas"}}` There are many ways to use it. But each table inside it has to have a param and action.   `param` is the location that the cleaning should take place in. It will be processed by BeardLib.Utils:StringToTable so you can write things like param.x.y.z.   `action` can be either of these: |

