# Package Manager

Updated for version 4.0.

To understand how some functions work here read about [AddFilesModule](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/AddFilesModule)

## BeardLibPackageManager class

Used to be called CustomPackageManager.

Access it using BeardLib.Managers.Package

### Variables

| Function | Description |
| :--- | :--- |
| custom\_packages | A table containing custom packages. Each table has a key being the the Idstring key of the ID and table value containing `dir` for directory, `config` for the package data, and `id` for raw ID |
| unload\_on\_restart | A table containing packages to unload after a restart. Each value in it just containing the config of the package to unload |
| EXT\_CONVERT | A table with keys of file names that should be converted into their in-game counterparts. Example, dds is "texture" "bik" is "movie" etc |
| UNIT\_SHORTCUTS | The table that holds the unit shortcuts. Each key being the meta of the shortcut and the value containing a table with data of what should be loaded. Inside each table you have types of files that should be loaded. Writing just {} will load by default unit, object, and model. Writing any type like "type=true" will load that type. If you need to load multiple files of the same type you write "type={"\_thq"}" with the values inside being suffixes to the path |
| TEXTURE\_SHORTCUTS | Like `UNIT_SHORTCUTS` this holds shortcuts but shortcuts only for textures. Each table of a meta key holds suffixes. Example: "df\_nm\_cc = {"\_df", "\_nm", "\_df\_cc"}" loads path\_df.texture, path\_nm.texture, and path\_df\_cc.texture |

### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| RegisterPackage\(String id, String directory, Table config\) | Boolean | Registers a package to be loaded using `PackageManager:load` or `BeardLib.Managers.Package:Load`. `id` is the ID \(think of the "path" for normal package\), `directory` the directory for the assets. Usually ModPath + "/assets" or "/Assets" the files inside the game will have the path _after_ the defined directory, `config` is the package config. Almost identical to [AddFilesModule](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/AddFilesModule). And yes, this means that the config uses \_meta values to know what file type is each table. It is recommended to use [PackageModule](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/PackageModule) to add custom packages |
| LoadPackage\(String id\) | Boolean | Loads a custom package. `id` is the id of the package |
| UnloadPackage\(String id\) | Boolean | Unloads a custom package |
| PackageLoaded\(String id\) | Boolean | Returns a boolean determining if the package is loaded |
| HasPackage\(String id\) | Boolean | Returns a boolean if the custom package was registered |

#### Other

| Function | Description |
| :--- | :--- |
| LoadPackageConfig\(String directory, Table config, Boolean temp\) | The function that goes through `config` and loads all files defined there. Pretty much to understand how it works you need to understand how AddFilesModule works. `directory` is the directory of the assets and `temp` will unload the files on restart |
| AddFileWithCheck\(Idstring ext, Idstring path, String file\) | Adds a file but checks if the file exists first. Calls `self:Err` if the file was not found \(In AddFilesModule it will call the error on the module class not BeardLib in general\) That error shows up in developer mode's errors dialog |
| Err\(...\) | Calls [BeardLib:Err](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/BeardLib-Class#usable-functions) |
| UnloadPackageConfig\(Table config\) | Called by `:UnloadPackage` and unloads the files of `config` |
| Unload\(\) | Unloads packages that unload on restart. Called by a PostHook in `Setup:unload_packages` |

