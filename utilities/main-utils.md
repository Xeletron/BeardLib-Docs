# Main

Updated for version 4.0 Utilities are useful functions for bunch of purposes.

## BeardLib.Utils class

The main utilities class

### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| CheckParamsValidity\(Table tbl, Table schema\) | Boolean | Checks `tbl` which contains parameters you want to check. `schema` contains what you expect the parameters to be. `schema` should have a `func_name` string value which is where the function was called from \(So user knows where they wrote wrong parameters\).  Then, a `params` table which contains expectancy from the parameters in `tbl` \(Ordered by indices\), each table with these values: `type` for desired type and `allow_nil` to allow nullable parameters. [Example](main-utils.md#CheckParamsValidity) |
| CheckParamValidity\(String func\_name, Number vari, Any var, String desired\_type, Boolean allow\_nil\) | Boolean | The function `CheckParamsValidity uses to check the parameters.`func\_name`being the function this is called from,`vari`is the index of the variable,`var`is the variable value,`desired\_type`is the type this variable should be and`allow\_nil\` \(which defaults to false\) to allow the variable to be null |
| GetSubValues\(Table tbl, String key\) | Table | Returns a table of sub values that correspond to the key `key`. [Example](main-utils.md#GetSubValues) |
| normalize\_string\_value\(String value\) | Any | Returns the object value from a string representation of the value. For example: "Vector3\(0,0,0\)" will return a vector3 object. This function supports: Vector3, Rotation, Color and callback, ClassClbk, SimpleClbk, etc |
| StringToValue\(String str, Table global\_tbl, Boolean silent\) | Any | Returns a value from a string. `str` can be like "self.value" self being `global_tbl`. It can also do something like self.tbl.x.y.z `str` is the string that needs conversion, `global_tbl` can be left out which will default to \_G or set as some class. `silent` decides whether to log when an error has hit |
| UrlEncode\(String str\) | String | Returns a string version of the passed str which is encoded for urls |
| FindMod\(String name\) | ModCore | Searches a mod \(All mods including these not in frameworks\) with the name `name` and returns its ModCore class if it finds it; returns null if not found. If you know which framework the mod resides in, please use the [framework](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/Frameworks) functions |
| ModExists\(String name\) | Boolean | Returns a boolean determining if the mod exists in the game |
| ModLoaded\(String name\) | Boolean | Returns a boolean determining if the mod exists and is loaded \(not disabled\) |
| FindModWithPath\(String path\) | ModCore | Returns a mod in `path` |
| FindModWithMatchingPath\(String path\) | ModCore | Returns a mod with a path that matches `path`. For example the mod path is "mods/BeardLib". We pass the argument "mods/BeardLib/Hooks" to it and the function will return BeardLib because `path` matches with BeardLib's path. This is used to find mods even if the path is a folder inside of the mod |

#### Other

| Function | Description |
| :--- | :--- |
| RefreshCurrentNode\(\) | Refreshes the current menu node |
| SetupXAudio\(\) | A quick function to automatically setup BLT's XAudio stuff. Automatically called by BeardLib when adding sounds |

## json class

Existing class added by BLT. BeardLib adds a special encoding and decoding function that add support for these values: Vector3, Color, Rotation, and callback.

This class uses periods and not a colon for function calls; so you'd call it like: json.func\(\).

### Functions

| Function | Description |
| :--- | :--- |
| custom\_encode | This is a variation of the default json encoder that comes bundled with BLT. This version of the encoder will output with proper formatting and can write data such as `Vector3`, `Color`, etc. It also doesn't have the issue where it saves an empty table as '\[\]', which would error when decode was attempted |
| custom\_decode | Similar to the custom\_encode function, it is a variation of the default json decoder that comes bundled with BLT. This decoder will parse `Vector3`, `Color` etc and will attempt to do conversions for the json ScriptData output created from the DieselScriptTool |

## Anonymous functions

### Functions

| Function | Return type | Description |
| :--- | :--- | :--- |
| NotNil\(...\) | Any | Checks every value in parameters and returns the first value it finds that isn't null. Returns the null if no value was found. Useful when you want to differentiate between false and null |
| type\_name\(Any value\) | String | The same as CoreClass.type\_name which returns the type of an object. But, adds support for tables that have `type_name` value in them \(like MenuUI items\). Which lets us differentiate between different tables |
| CRC32Hash\(String str\) | Creates a CRC32 hash of a string. Good if you need something shorter than a Idstring key |  |

## Examples

### CheckParamsValidity

```lua
BeardLib.Utils:CheckParamsValidity({x, y}, {
    func_name = "MyCoolClass:init", 
    params = {{type="string", allow_nil = false}, {type="number", allow_nil = true}}
}))
```

This function checks if `x` is a string and not null \(allow\_nil defaults to false but for this example I wrote it\) and checks if `y` is a number but allows it to be a null.

### GetSubValues

```lua
BeardLib.Utils:GetSubValues({
    {test = false, test2 = "this wont come through"}, 
    {test = true, test3 = "this also wont come through"}
}, "test")
```

Returns:

```lua
{[1] = false, [2] = true}
```

