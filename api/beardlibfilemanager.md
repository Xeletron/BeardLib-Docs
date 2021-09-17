# File Manager

Updated for version 4.0.

## BeardLibFileManager class

_Used to be called FileManager_

Access it via BeardLib.Managers.File

### Functions

| Function | Description |
| :--- | :--- |
| AddFile\(String/Idstring ext, String/Idstring path, String file\) | Adds a file to the game. Works in Linux. \(Thanks Znix!\) `ext` is the extension inside the game \(See type [here](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/AddFilesModule#does-not-need-loadtrue)\) `path` is the path **inside** the game and `file` is the path to the file including extension.  You should use this function if you are planning on adding files through lua as BeardLib also adds its to a list so some functions like `PackageManager:has` will return true. |
| AddFileWithCheck\(String/Idstring ext, String/Idstring path, String file\) | Same as `AddFile` but checks if file exists before adding. Logs a message if it doesn't exist |
| RemoveFile\(String/Idstring ext, String/Idstring path\) | Removes a file from the game `ext` and `path` same as in `AddFile` |
| ScriptReplaceFile\(String/Idstring ext, String/Idstring path, String file, Table options\) | Adds a scriptdata modification to the list. If your mod has a BeardLib config file you may want to use the [module](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/ScriptReplacementsModule)  `ext` being the scriptdata extension \(sequence\_manager, environment, world, mission, continent, etc\), `path` is the path to the scriptdata you want to modify \(or add\), `file` is the path to the modification/scriptdata. `options` is a table containing some parameters which are:  `use_clbk` a callback that is called before doing the process to check if to proceed with the process. You may be interested in using if you want to have an option before merging |
| ScriptReplaceFile\(String/Idstring ext, String/Idstring path, Table tbl, Table options\) | Like `ScriptReplaceFile` but instead of a file doing the modification it uses a table with the data. `tbl` being the modification data/scriptdata. Since it doesn't load anything it doesn't need `type` in options. |
| Has\(String/Idstring ext, String/Idstring path\) | A function to check if file `path` with extension `ext` exists in Beardlib. Called in `PackageManager:has` |
| HasScriptMod\(String/Idstring ext, String/Idstring path\) | A function to check if a scriptdata modification/addition exists in BeardLib. Called in `PackageManager:has` and `DB:has` |
| LoadAsset\(String/Idstring ext, String/Idstring path, String file\_path\) | Loads a file into the game fully. `ext` is the extension of the file \(in the game\), `path` is the path in the game, and `file_path` is the full path of the file \(normally this is not required but it's useful so you can see if the file loaded through DevLog\)  Some files need this \(Some like units are loaded automatically before spawning, see list [here](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/AddFilesModule#types)\). Remember that adding a file to the game isn't the same as loading in diesel. Diesel is weird a little so some files need that extra push to be fully loaded and usable |
| UnloadAsset\(String/Idstring ext, String/Idstring path, String file\_path\) | Unloads file with extension `ext` and path `path`. `file_path` is not required but recommended |
| Process\(Idstring ids\_ext, Idstring ids\_path, Idstring name\_mt\) | A core function called automatically after `PackageManager:script_data`. No need to call it |
| Update\(Number t, Number dt\) | Update function for the class. Called automatically by BeardLib |

