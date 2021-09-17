# BeardLib Class

Updated for version 4.0.

## BeardLib class

Contains a few useful functions.

### Variables

| Parameter | Type | Description |
| :--- | :--- | :--- |
| Name | String | The name of mod which of course is "BeardLib" |
| ModPath | String | Path to BeardLib's folder. Generally mods/BeardLib |
| Frameworks | Table | A table holding all frameworks of BeardLib |
| Managers | Table | A table holding all managers of BeardLib |
| Menus | Table | A table holding the menus of BeardLib \(mods manager and achievements\) |
| MusicMods | Table | A table holding music mods |
| Modules | Table | holds all modules of BeardLib |

### Functions

The BeardLib class inherits most of the functions found in [ModCore](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/ModCore#functions)

#### Usable functions

| Function | Description |
| :--- | :--- |
| AddUpdater\(String id, Function clbk, Boolean paused\) | Adds an updater which is called after the update function is called. `id` being the ID of your updater, `clbk` is the function/callback, and `paused` determines if the updater should run when paused |
| RemoveUpdater\(String id\) | Removes updater with id `id` |
| CallOnNextUpdate\(Function func, Boolean only\_unpaused, Boolean only\_paused\) | Adds a function to be called in the next update. After it's called once it won't be called again unless you run this again. `only_unpaused` determines if the function should only run in unpaused state and `only_paused` is the opposite of it. If both `only_paused` and `only_unpaused` are not defined the function will run in both |
| RegisterModule\(String key, Table module\) | Registers a module with `key` which is the type\_name of the module and `module` is the class/table of it. Unlike frameworks you must define this one if you create a module not using [MoudlesModule](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/ModulesModule). |
| GetPath\(\) | Returns the path of BeardLib. Should always be "mods/BeardLib" |
| RegisterFramework\(String name, Table clss\) | Adds a framework class to the framweworks list \(Called automatically even if you create a custom framework\). Though, in extreme cases you may need to use it |
| RegisterManager\(String name, Table clss\) | Registers a manager class for BeardLib |
| RegisterMenu\(String name, Table clss\) | Registers a menu class for BeardLib. For example, the mods menu |
| RegisterClass\(String name, Any obj, Number typ\) | Registers a class. `name` is the key of the class, `obj` is the class itself, and `typ` is one of the values of BeardLib.Constants.ClassTypes. Generally used internally and is verbose. |
| ModError\(ModCore mod, String str, ...\) | Called usually by [ModCore](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/ModCore#functions) itself. This error is a little different than the regular Err function in that this will show a message to the user. |

#### Core functions

These functions are automatically called by BeardLib. Therefore, there's no point in calling them. Some are more BeardLib specific.

| Function | Description |
| :--- | :--- |
| Init\(\) | The initialization function of BeardLib |
| LoadClasses\(Table config, String prev\_dir\) | Loads the classes that BeardLib uses. `config` is used have grouped classes inside the Classes table alongside `prev_dir`. |
| LoadModules\(String dir\) | Loads BeardLib's modules by getting all files in /Modules/ or dir. `dir` is used to load subfolders in the modules folder |
| LoadLocalization\(\) | Loads the localization files from /Localization adds them to a LocalizationModule afterwards |
| Update\(Number t, Number dt\) | The update function for BeardLib |
| PausedUpdate\(Number t, Number dt\) | The update function that runs when the game is paused for BeardLib |
| RegisterTweak\(\) | Adds the mod global value and mod DLC to the tweakdata |
| MigrateModSettings\(\) | Migrates mod settings of BeardLib versions before 4.0 to the 4.0 format. The change involves moving DisabledMods and IgnoredUpdates to the ModSettings table which will hold configurations for mods. |
| ShowErrorsDialog\(\) | Gets automatically called by BeardLib when entering main menu and there are mod errors to show. Can be turned off by an option |
| DevLog\(String str, ...\) | Used by BeardLib for debugging. Generally does nothin without editing the function |

#### Return functions

| Function | Return Type | Description |
| :--- | :--- | :--- |
| ManagerClass\(String name, Any inherit\) | class\(\) | Makes a new manager class. With `name` used to Register it and `inherit` if you wish to inherit a previous class's functions & variables |
| MenuClass\(String name, Any inherit\) | class\(\) | Same as ManagerClass just for menus |
| ModuleClass\(String name, Any inherit\) | class\(\) | Same as ManagerClass just for modules |
| FrameworkClass\(String name, Any inherit\) | class\(\) | Same as ManagerClass just for frameworks |

