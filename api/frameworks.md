# Frameworks

Updated for version 4.0.

Frameworks in BeardLib are a major part in BeardLib's mod loading, this is what loads the mods and gives them a place to stay in.

There are 3 frameworks in BeardLib: FrameworkBase, AddFramework and MapFramework.

Each framework gets added to this table: BeardLib.Frameworks. Each framework key is the type\_name of the framework so: BeardLib.Frameworks.Base, BeardLib.Frameworks.Add, and BeardLib.Frameworks.Map. These are the classes you'd want to call to use functions such as `GetModByName`.

## FrameworkBase

The base framework, all other frameworks inherit this framework. By itself, the framework loads any main.xml it finds inside **BLT** mods.

Access with `BeardLib.Frameworks.Base`

### Variables

| Parameter | Type | Description |
| :--- | :--- | :--- |
| \_directory | String | The directory of the mods that the framework should load. In this case it's set to "mods/" |
| \_mod\_core | Class | The class that the mod of this framework should initialize in. All frameworks use [ModCore](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/ModCore) |
| main\_file\_name | String | The main file that the framework should load. All frameworks use "main.xml" |
| auto\_init\_module | Boolean | Automatically initialize the modules in this framework? |
| \_ignore\_folders | Table | A table of folders that the framework should ignore. The values inside are folder = true |
| \_ignore\_detection\_errors | Boolean | Determines if the framework should not log about folders it could not find a main.xml in the directory of the framework. Defaults to true \(Except map framework\) |
| menu\_color | Color | The default color of mods that are inside this framework \(Shown in the BeardLib mods manager\) |

### Functions

| Function | Description |
| :--- | :--- |
| init\(\) | The init function. Registers the framework to BeardLib using BeardLib:RegisterFramework and sets up stuff. Creates a hook that runs every time require is called and in that hook CheckModQueue is called |
| CheckModQueue\(Booolean post, String file\) | Called a few times to check for mods that are waiting to load through a post or pre hook |
| Load\(\) | Called after init finished the setup process |
| FindMods | Searches for mods to load. Loads each mod using `LoadMod` |
| SortMods | Sorts the mods based on priority |
| InitMods | Calls PreInitModules on mods to start loading the modules. Mods with `post_hook` or `pre_hook` will load be added to self.\_waiting\_to\_load |
| RegisterHooks\(\) | Called automatically by a BeardLib hook for each framework from some point in tweakdata. This calls `DoRegisterHook` for modules and some modules use this point to add hooks for tweakdata |
| log\(s, ...\) | A log function. Parameters act like string.format |
| DevLog\(s, ...\) | Same as log but only logs when BeardLib has developer mode on \(mods folder needs to have mod.txt file and you need to turn on the option in BeardLib options\) |
| LoadMod\(String folder\_name, String directory, String main\_file\) | Instantiates a mod.  |
| AddMod\(String dir, ModCore mod\) | Adds the mod to the mod lists |
| RemoveMod\(String dir\) | Removes the mod from the mod lists |

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| GetModByDir\(String dir\) | ModCore | Returns a mod based on a directory. For example mods/Holo will return HoloUI if exists |
| GetModByName\(String name\) | ModCore | Returns a mod based on a name. For example Sora HUD Reborn will return the Sora's HUD mod |

## AddFramework

The framework for mod overrides mods and add.xml.

Access with `BeardLib.Frameworks.Add`

### Variables

| Parameter | Type | Description |
| :--- | :--- | :--- |
| add\_configs | Table | The table that holds all add.xml configs. Each config is stored in a mod path key. |

Inherits BaseFramework and does the following things:

* Allows loading a file named "add.xml" which is a quick and dirty way of loading AddFiles by modifying the `FindMods` function to pickup these files.
* Sets `_directory` to assets/mod\_overrides

## MapFramework

The framework for custom maps basically your "Maps" folder.

Access with `BeardLib.Frameworks.Map`

Inherits BaseFramework and does the following things: Sets `_directory` to "Maps" Sets `_ignored_folders` to {"backups", "prefabs"} to ignore the default editor folders\|

## Modules of interest

* [ContactModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ContactModule)
* [LevelModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/LevelModule)
* [NarrativeModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/NarrativeModule)
* [LocalizationModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/LocalizationModule)

### Functions

| Function | Description |
| :--- | :--- |
| AddCustomContact\(\) | A function called from a modified `RegisterHooks` to create a default contact for custom maps |

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| GetMapByJobId\(String job\_id\) | ModCore | Searches for a mod that has a narrative/job with id `job_id` and returns it |

