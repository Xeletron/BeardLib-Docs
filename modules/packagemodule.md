# Package

Updated for version 3.38.

## Module Definition

The module is inherited from [ModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase). So base parameters can be found there.

The main purpose of this module is to emulate a 'package' that the game normally uses to load assets for various purposes \(such as levels\). Everything in PackageManager should support your 'added' package, except the PackageManager:package function.

Imagine PackageModule module as a delayed AddFilesModule. Instead of loading it right away it will load when you need it.

### Module name

The name of the module you use as the meta of the module definition is 'Package' or 'PackageModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<Package id directory>
    <extension path force load reload unload/>
</Package>
```

#### `<Package id directory>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String | The id/path of the package which is used when it is being called to be loaded, unloaded etc |
| directory | String | string directory/path relative to the mods directory which contains all files to be added |

#### `<extension path force load reload unload/>`

See: [AddFilesModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/AddFilesModule)

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<Package id="packages/my_test_package" directory="mod_assets">
    <texture path="guis/textures/my_texture"/>
</Package>
```

For this example you would have your custom texture like this: mods/MyMod/mod\_assets/guis/textures/my\_texture.texture

And you could load the package by doing PackageManager:load\("packages/my\_test\_package"\)

If you are using this module in a BLT mod.

### Functions

| Function | Description |
| :--- | :--- |
| Load\(\) | This function is used to add/load all the assets defined in the package. This is usually called by the PackageManager:load function |
| Unload\(\) | This will remove all the added files from the game's database. This is usually called by the PackageManager:unload function |
| Loaded\(\) | Returns a value that determines if the package has been 'loaded'. This is usually called by PackageManager:loaded |

