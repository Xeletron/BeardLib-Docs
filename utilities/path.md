# Path

Updated for version 3.38

## Path

An utility class for dealing with paths. Although in the past you'd call the class using `BeardLib.Utils.Path` \(and still can\), it was shortened because of its heavy use; so now you can call `Path` or `path`.

### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| GetDirectory\(String path\) | String | Returns the directory of `path` which may be a file or a directory. Directory is being the folder that the file/folder resides in |
| GetFileName\(String path\) | String | Returns the file name from the provided path `path` |
| GetFileNameNoExt\(String str\) | String | Returns the file name \(from the provided path\) without the extension |
| Normalize\(String str\) | String | Returns a normalized version of the path `str`. Currently cleans the separators to all be '/' |
| Combine\(String start, ...\) | String | Returns a normalized and combined version of the passed paths. Starting with `start` and adding the passed `...`, `start` cannot be null! Example: `Path:Combine("path", "to", "file")` returns `"path/to/file"` |
| CombineDir\(String start, ...\) | String | Like `path` but adds a forward slash in end of the result |

