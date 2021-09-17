# FileIO

Updated for version 3.38

## FileIO

FileIO is an utility class that is meant to bring all file functions into one known class instead of io, SystemFS, and file. It also brings some more useful functions.

Remember that this class is called using a colon not a period.

**At the moment, not all functions are supported in Linux.** An asterisk will be written near functions to indicate that they don't support Linux. Also, make sure you're using the latest SuperBLT version as it may add support for some functions.

### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| Open\(String path, String flag\) | File | Opens a file. Pretty much the same as io.open [https://www.lua.org/manual/5.1/manual.html\#pdf-io.open](https://www.lua.org/manual/5.1/manual.html#pdf-io.open) |
| WriteTo\(String path, Any data, String flags\) | Boolean | Opens a file in `path` and writes into `data` into it. The flag defaults to `w`. You may need to change to wb for binary files. Returns true if the file opened successfully and closes the file automatically |
| ReadFrom\(String path, String flags, String method\) | String | Opens a file in `path` and reads its content using `method` which defaults to "\*all" |
| ReadConfig\(String path, Table tbl\) | Table | Opens a custom XML file in `path`. If `tbl` is present it will run through the strings in the config and try to convert them into values. For example, if `tbl` has the value x=1 and in the config we have the string y="$x" it will convert that to 1 |
| ConvertScriptData\(String/Binary data, String typ, Boolean clean\) | Table | Converts `data` to a readable table. `typ` is the type of the data. Either custom\_xml, generic\_xml, binary, or json. `clean` cleans the returned table. This is mostly for specific cases with reading custom XMLs as they are prone to repeat values when not needed. |
| ConvertToScriptData\(Table data, String typ, Boolean clean\) | String/Binary | Converts table `data` into one of the types \(same as in `ConvertScriptData`\). Clean does the same as in the other function too |
| ReadScriptData\(String path, String typ, Boolean clean\) | Table | Same as `ConvertScriptData` but opens a file in `path` and converts its data. |
| WriteScriptData\(String path, Table data, String typ, Boolean clean\) | Boolean | Opens a file in `path` and writes the return of `ConvertToScriptData` to the file. After `path` the parameters are the same as in `ConvertToScriptData`. Returns the same as `WriteTo` |
| Exists\(String path\) | Boolean | Returns a boolean indicating if the file or directory in `path` exists |
| \*CanWriteTo\(String path\) | Boolean | Returns true if path is writable. At the moment, returns true in Linux regardless |
| GetFiles\(String path\) | Table | Returns a table of files in `path` |
| GetFolders\(String path\) | Table | Returns a table of folders in `path` |
| FileExists\(String file\) | Boolean | Returns true if a file in path `file` exists |
| DirectoryExists\(String folder\) | Boolean | Return true if a folder in path `folder` exists |

#### Other

| Function | Description |
| :--- | :--- |
| \*CopyFileTo\(String path, String to\_path\) | Copies a file from `path` to `to_path` |
| \*CopyDirTo\(String path, String to\_path\) | Copies a folder from `path` to `to_path` |
| \*CopyFilesToAsync\(Table copy\_data, Function callback\) | An asynchronous copy of files. `copy_data` should contain tables of file path and path to copy to. Example: . `callback` is the function that will call if the copy succeeded or failed. The function should look like: function\(success, message\) end |
| \*CopyToAsync\(String path, String to\_path, Function callback\) | Copies a directory in `path` to `to_path` asynchronously. `callback` is the same as in `CopyFilesToAsync` |
| \*MoveTo\(String path, String to\_path\) | Moves file from `path` to `to_path`. This function can be used as a rename function |
| \*Delete\(String path\) | Deletes a file or directory in `path` |
| \*DeleteEmptyFolders\(String path, Boolean delete\_current\) | Deletes empty folders in directory `path`. `delete_current` determines if to delete the folder itself if it's empty |
| MakeDir\(String path\) | Creates the directory `path`. \(Creates the directory through os.execute in Linux\) |
| LoadLocalization\(String path, Boolean overwrite\) | Loads a localization file \(json\) from `path`. `overwrite` overwrites existing localization |

