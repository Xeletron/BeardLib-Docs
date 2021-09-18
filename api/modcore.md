# ModCore

Updated for version 3.38.

## Config/XML parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| name | String | Optional name of the mod to be used for logging. Defaults to the folder name of the mod |
| author | String | Optional name of the author of the mod. Will show up in the mods list |
| global\_key | String | Optional global key for the mod class. If it doesn't exist already it will create the global |
| priority | Number | A number that determines the priority of the mod. Similarly to BLT's priority, the higher it is the earlier the mod will load |
| min\_lib\_ver | Float | Minimum version of BeardLib that the mod can load in. If your mod uses a new feature that can cause issues/crashes in older versions, use this! |
| core\_class | String | Path to the core class. If no class will be returned it will use ModCore as the class. If you have set a global key you can use that global key to add functions to your ModCore class. See in functions for the currently available functions |
| load\_first | Table | A table of strings of which modules to load first |
| no\_disabled\_updates | Boolean | Determines if the mod should not be updatable when disabled by an error |
| notify\_about\_version | Boolean | Determines if BeardLib should notify the user if they are running an older version of BeardLib that does not work with the mod. Defaults to true |
| post\_init | String | Path/name of the function that should be called after ModCore's `PostInit` function. If you're using core\_class read about the `Init` function instead! |
| ignored\_modules | Table | A table of modules that should be ignored. Highly specific use cases where you want to postpone the initialization of some modules |
| post\_hook | String | Optional value that lets you initialize your BeardLib mod through a post hook script |
| pre\_hook | String | Like `post_hook` but a pre hook script instead |

All of these values are available through self.\_config after the mod gets initialized. Feel free to include your own values in the XML.

## Functions

| Function | Description |
| :--- | :--- |
| init\(String config\_path, Boolean load\_modules\) | The init function of the class. If the mod isn't disabled it will load the config file `config_path` The path to the xml config for the mod`load_modules` Determines if modules should be automatically loaded on instantiation of ModCore |
| PostInit\(\) | Post init of the mod. In this stage many modules get fully loaded. |
| InitModules\(\) | Initializes all the modules that have been defined by the mod. Calling this is only necessary when `load_modules` passed to init/new is false |
| LoadConfigFile\(String path\) | Loads the config file and sets a few variables based on it. `module_tbl` is the config of the module |
| AddModule\(Table module\_tbl\) | Initializes a module and adds it to self.\_modules. This was separated from `InitModules()` so we could make the XMLModule work. Potentially this can be used to load any module in runtime |
| Log\(String str, ...\) | A log function. The parameters act like string.format |
| Err\(String str, ...\) | Logs an error message to the console \(\[ERROR\] + message\). The parameters are like in string.format. The errors get logged and shown in errors dialog if developer mode is active |
| LogErr\(...\) | Same as `Err` but never adds the error to the errors dialog |
| Warn\(String str, ...\) | Logs a warning message to the console \(\[WARN\] + message\). The parameters are like in string.format |
| RegisterHook\(String source\_file, String file, Boolean pre\) | Registers a script hook. |
| ForceDisable\(\) | Disables the mod. Make sure to call this before the mod gets fully initialized. **This only disables the mod for the current lua state** |

### Get functions

| Function | Return type | Description |
| :--- | :--- | :--- |
| GetRealFilePath\(String path, Table lookup\_tbl\) | String | Returns a version of the passed string `path` with patterns such as '$variable$' being corrected to the value of the variable with that key in the `lookup_tbl` `lookup_tbl` The table to use as a lookup for found variables, defaults to the ModCore table |
| StringToValue\(String str\) | Any | Converts `str` to a value. Example: self.AFunctionMyClassHas \(previously named StringToTable but was renamed because it can get anything\) |
| StringToCallback\(String str\) | Function | Converts `str` to a callback. For example: self.MyCallback self is ModCore but can be any class you want |
| GetPath\(\) | String | Returns self.ModPath, the path of your mod \(where main.xml resides\) |
| Enabled\(\) | Boolean | Returns a boolean determining if the mod is enabled |
| Disabled\(\) | Boolean | Returns a boolean determining if the mod is disabled |
| GetName\(\) | String | Returns self.Name, the name of the mod |
| Config\(\) | Table | Returns self.\_config, the config \(ie, xml\) of the mod |
| Priority\(\) | Number | Returns self.Priority, the priority of the mod |
| IsBLTMod\(\) | Boolean | Returns true if the mod is a BLT mod \(that uses BeardLib\) |
| Modules\(\) | Table | Returns a table with all loaded modules |
| GetModule\(String type\_name\) | Any module | Return the first module with the type name `type_name`. Think of the type name as the meta name you put in your main.xml like "AddFiles" |
| GetModuleIndex\(ModuleBase m\) | Number | Return the index of module `m` |
| GetModules\(String type\_name\) | Table | Returns a table of every module with type name `type_name`. Useful when the module can be added a few times in the mod \(for example, weapons, update module, any module with \_loose set to true\) |

### `core_class` functions

Functions to be used by `core_class` functions. Just create the functions in the class inside core\_class.

| Function | Description |
| :--- | :--- |
| Init\(\) | The function where you should write the initiailzation code for your mod. This is called after the modules get post initialized |
| PreInit\(\) | A function called earlier than `Init` this is before the modules get post initialized |
| PreInitModules\(\) | The earliest point. Before modules are even initialized. Use this function to check for errors before the mod fully loads using `ModError`. |

### Additional tips for core\_class

* If you need an update function you can add one using BeardLib:AddUpdater\(String id, Function clbk, Boolean paused\) and remove it using RemoveUpdater\(String id\).
* Automatic icon You can have BeardLib automatically load the mod icon and set it for you. Just create an icon.png in the root of your mod.

## Template

Download template here: [https://github.com/Luffyyy/BeardLib-Templates/tree/master/BLT-Template](https://github.com/Luffyyy/BeardLib-Templates/tree/master/BLT-Template)

beep

