# Dependencies

Updated for version 4.6.

## Module Definition

The module inherits [ModuleBase](https://luffyyy.gitbook.io/beardlib/modules/modulebase). All parameters and functions of this class are inherited by the module.

### Module name

The name of the module you use as the meta of the module definition is 'Dependencies' or 'DependenciesModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<Dependencies>
    <Dependency name type version id provider/>
</Dependencies>
```

**&lt;dependency name type version id provider/&gt;**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| name | String | The name of the mod to depend on. \[REQ\] For `mod_overrides` or `map` mods, this will be the name in main.xml. For `blt` mods, it will be the name in mod.txt or main.xml if present |
| type | String | The type of mod the dependency is. Options are `blt`, `mod_overrides` and `map` \[Default: `blt`\] |
| version | String | The minimum required version of the dependency. \[OPTIONAL\] |
| id | String/Number | The id of the mod on the server. \[OPTIONAL\] Having `id` and `provider` will add a [ModAssetModule](https://luffyyy.gitbook.io/beardlib/modules/modassetmodule) to download the dependency. |
| provider | String | The provider of updates for the mod/assets. \[OPTIONAL\] Having `id` and `provider` will add a [ModAssetModule](https://luffyyy.gitbook.io/beardlib/modules/modassetmodule) to download the dependency. |

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<Dependencies>
    <Dependency name="Custom Attachment Points" version="2.3.1" id="22546" provider="modworkshop"/>
    <Dependency name="My Cool Mask" type="mod_overrides"/>
    <Dependency name="TheGreatMaze" type="map" version="1.1" id="27125" provider="modworkshop"/>
</Dependencies>
```

### Functions

| Function | Description |
| :--- | :--- |
| Load\(Table config | Called normally by the module's init function. This is what checks the dependencies. `config` is the current looping dependencies table \(or self.\_config if not present\) |
| CheckBLTMod\(String name\) | Goes through the currently added BLT mods and compares the mod name with `name`, returns true and the mod if found. |
| CompareVersion\(Table dep, String/Number mod\) | Compares the versions of the Dependency (dep) and the mod. Creates a ModError if Dependency version is higher than mod version. |
| CreateErrorDialog\(Table dep\) | Creates an ModError and add calls AddDepDownload if `id` and `provider` are in the Dependency's config. |
| AddDepDownload\(Table dep\) | Adds an [ModAssetModule](https://luffyyy.gitbook.io/beardlib/modules/modassetmodule) to the mod. Called by CreateErrorDialog. |


