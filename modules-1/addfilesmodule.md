# Add Files

Updated for version 4.0.

The module inherits [BasicModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/BasicModuleBase). All parameters and functions of this class are inherited by the module.

## Module name

The name of the module you use as the meta of the module definition is 'AddFiles' or 'AddFilesModule' if `_force_search` is set to true in the module definition.

## XML Structure

```markup
<AddFiles directory force_all use_clbk>
    <extension path force load reload unload/>
</AddFiles>
```

### `<AddFiles directory force use_clbk ...>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| directory | String | directory/path relative to the mods directory which contains all files to be added |
| use\_clbk | String | Pointer to a function which should return a value that determines if the added files should be added. Example: "self:UseClbk" |
| unload\_on\_restart | Boolean | Determines whether to unload files when the game is restarted |

### `<extension path force load reload unload .../>`

| Parameter | Type | Description |  |
| :--- | :--- | :--- | :--- |
| extension | String | The extension/type of the file you are adding |  |
| path | String | Path of the file you wish to add \(**without the extension**\), relative to your mod's directory and the directory you may or may not have specified in the main node.\[REQUIRED\] |  |
| force | Boolean | Determines if the file should be forced to be added even if a file with the extension and path is already in the database. Defaults to true and **can be inherited from the parent node** |  |
| force\_if\_not\_loaded | Boolean | Sort of like `force` but checks if the file is not loaded in the **memory** |  |
| load | Boolean | Determines if the file should be loaded through dyn_resource as soon as it is available. Defaults to false. \_Can be inherited from the parent node_ Scroll down to know more about load |  |
| unload | Boolean | Determines if the file should be unloaded when the AddFilesModule is unloaded. Defaults to true. **Can be inherited from the parent node** |  |
| reload | Boolean | Determines if the file should be called with PackageManager:reload after it has been added. Defaults to false. **Can be inherited from the parent node** |  |
| full\_path | String | Allows you to define a full path instead of automatic path that is constructed from the `directory` value |  |
| auto\_cp | Boolean | Determines if an automatic cooked physics should be loaded. This means a cooked physics from BeardLib there isn't a need to create a file for it. This is highly recommended when your cooked physics is 0 bytes. Some units don't require a cooked_physics file. \_Can be inherited from the parent node_ |  |
| use\_clbk | String | Pointer to a function which should return a value that determines if the file should be added. Example: "self:UseClbk" |  |

## `<add ...>`

_Allows you to categorize your added files. Useful when you add a few units and want to keep track of the dependencies of the unit. Used in custom levels' add.xml._

**Has the same parameters as  and accepts files**.

**Note:** custom levels' add.xml use `path` and `type` parameter in their `<add>`. This is only used by the editor. You can categorize them with comments.

## Types/Load

_Any file that exists in the game can be added through AddFiles. It doesn't mean all will load but most do._

### Does not need `load=true`:

_The files either don't need load at all \(like textures\). Or, are loaded automatically by BeardLib when they are used_

* texture/dds/png/tga
* bik/movie
* unit
* object
* material\_config
* sequence\_manager
* cooked\_physics \(Added automatically for new units\)
* effect \(supposed to load by itself, if it doesn't work you can still try load=true\)
* environment
* mission
* continent
* world
* any scriptdata

### Needs `load=true`:

* font
* scene

### Untested

* merged\_font
* strings
* bnk

## Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<AddFiles directory="assets">
    <texture path="guis/textures/my_texture"/>
</AddFiles>
```

For this example you would have your custom texture like this: mods/MyMod/assets/guis/textures/my\_texture.texture

If you are using this module in a BLT mod.

**Example of using `<add>`**

```markup
<AddFiles directory="assets">
    <texture path="guis/textures/my_texture"/>
    <add>
        <movie path="path/to/movie"/>
        <unit path="path/to/unit"/>
    </add>
</AddFiles>
```

## Shortcuts

Introduced in 3.38.

Shortcuts are mainly for units and are used to add units using special metas that "guess" your files based on a path you provide. There are also some for textures. This let's you reduce the amount of copy pasting you have to do in AddFiles.

#### Things to know:

* Most paths are supposed to be the same \(except of course the extension\). But, things like textures are path + \_df and path + \_nm.
* df stands for diffuse and nm stands for normal.
* cc is the texture used for skins.
* thq stands for \(presumably\) third-person high quality and are essentially the high quality third models. Mostly the templates already have the things in the material config setup so you don't have to touch it. That also has a cc variant \(Weird I know\).
* `auto_cp` option above is actually turned on here by default. This means you don't have to include cooked\_physics. If your unit does use cooked physics \(meaning the cooked physics file isn't 0kb\) you should set this value to false. In some cases, the unit doesn't need a cooked physics at all so there you should turn that off too.

#### Current shortcuts:

| Meta | Description |
| :--- | :--- |
| unit\_obj | Adds unit, model, and object \(object and model **always** have the same path\) |
| unit\_tex | Adds unit, model, object, material\_config, and textures |
| unit\_seq | Adds unit, model, object, material\_config, textures, and sequence\_manager |
| unit\_mat | Adds unit, model, object, and material\_config |
| unit\_mat\_seq | Adds unit, model, object, material\_config and sequence\_manager |
| unit\_obj\_seq | Adds unit, model, object, and sequence\_manager |
| unit\_thq | Adds unit, model, object, material\_config, textures, and \_thq material\_config \(path + \_thq\) |
| unit\_mat\_thq | Adds unit, model, object, material\_config, and \_thq material\_config |
| unit\_npc | Adds unit, model, object, and npc unit \(path + \_npc\) |
| unit\_cc | Adds unit, model, object, material\_config, textures, \_thq material\_config, \_cc material\_config, \_cc\_thq material\_config and \_df\_cc texture |
| unit\_mat\_cc | Adds unit, model, object, material\_config, \_thq material\_config, \_cc material\_config, and \_cc\_thq material config |
| df\_nm | Adds textures \(path + \_df and path + \_nm\) |
| df\_nm\_cc | Adds textures and cc texture \(path + \_df\_cc\) |
| df\_nm\_cc\_gsma | Adds textures, cc texture, and gsma texture \(path + \_gsma\) |
| df\_nm\_gsma | Adds textures, textures, and gsma texture |

Remember that these replace the meta name. So you'll write it like

```markup
<unit_obj path="path"/>
```

This will add a unit, model, and an object that are all located in `path` \(path is a file path\) If we were to use unit\_tex it would add material\_config too and textures which would be in path + \_df, path + \_nm

The parameters these nodes accept are: `path`, `full_path`, `file_path`, and `auto_cp` \(custom\_cp only working in unit\_x of course\).

Possibly in the future this list may expand. It's also possible that a feature will be added to add shortcuts.

## Auto Generation

Introduced in 4.0.

A step up to shortcuts; now you can forget about adding entries every time.

**Warning:** it's currently being tested and some things may not work as intended.

To use this in the most simple way, you just need to add `auto_generate="true"` to the AddFiles config.

This will auto generate an xml which by default will be named `gen_add.xml`. The file will be generated once and that's it.

If you want to have it generate every reload, go to the your mod's settings in the BeardLib Mods Manager and enable "Develop Mode". This will tell BeardLib that the mod is being developed and it should auto generate it every reload.

Need more options? Remove that auto\_generate value and convert it to:

```markup
<auto_generate>
</auto_generate>
```

### XML Structure:

Now for the structure and how to do some things.

```markup
<AddFiles directory="assets">
    <auto_generate ...>
        <ignore>
            <unit/> <!--Ignores type unit-->
            <unit path/> <!--Ignores path + unit -->
            <table path/> <!--Ignores path -->
            <table pattern/> <!--Ignores all files matching the pattern -->
        </ignore>
        <set>
            <unit .../> <!--Set any unit-->
            <unit path .../> <!--Set unit with path-->
            <table path .../> <!--Set any file equal to that path-->
            <table .../> <!--Set any file-->
            <table pattern .../> <!--Set any file matching the pattern-->
        </set>
    </auto_generate>
</AddFiles>
```

### `<auto_generate ...>`

Uses the same parameters as `<AddFiles>`. It will inherit the top AddFiles's values.

| Parameter | Type | Description |
| :--- | :--- | :--- |


file\|String\|Path to the file that will be auto generated. Defaults to gen\_add.xml \(Do not confuse with add.xml. gen\_add.xml is loaded by the module not framework\).

### `<ignore>`

Let's you ignore files using: paths, types and patterns.

#### To ignore a type, simply write:

```markup
<ignore>
    <unit/>
</ignore>
```

#### To ignore a path, write:

```markup
<ignore>
    <table path="path/to/file"/>
</ignore>
```

This will ignore all paths that equal to "path/to/file"

#### To ignore a path AND type, write:

```markup
<ignore>
    <unit path="path/to/file"/>
</ignore>
```

This will ignore a unit with the path "path/to/file"

#### Patterns

Patterns let you ignore multiple files that match the pattern you write. This utilizes lua patterns \(which you can read in [here](https://www.lua.org/pil/20.2.html) about\). Let's see an example:

```markup
<ignore>
    <table pattern="_barrel"/>
</ignore>
```

This will ignore all files that match this pattern. If you want to specify a type you'd write it like this:

```markup
<ignore>
    <unit pattern="_barrel"/>
</ignore>
```

Remember! This uses lua patterns so you must be aware of the magic characters. The following characters must be escaped if you want to use them normally: `+, -, . and %`. Escape them by placing a `%` before them. Generally, these shouldn't be used in file/folder names.

### `<set>`

Uses similar syntax to ignore. So read that first.

Not everything can be automated. And so, sometimes we need to set values for some files.

#### Let's say you want to set load for all units:

```markup
<set>
    <unit load="true"/>
</set>
```

#### What about a specific unit?

```markup
<set>
    <unit path="path/to/unit" load="true"/>
</set>
```

#### Multiple values and setting them for all paths that equal:

```markup
<set>
    <table path="path/to/unit" unload="true" load="true"/>
</set>
```

#### And of course, patterns:

```markup
<ignore>
    <table pattern="_barrel" load="true"/>
</ignore>
```

Or a unit with patterns:

```markup
<ignore>
    <unit pattern="_barrel" auto_cp="true"/>
</ignore>
```

## Functions

| Function | Description |
| :--- | :--- |
| Load\(\) | This is called normally by the module's init function, this is what adds all the files to the game that have been defined in the module definition |
| Unload\(\) | This will remove all the added files from the game's database. This is only called by default if the AddFilesModule has been added through the [LevelModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/LevelModule) |
| LoadPackageConfig\(...\) | Same as in [CustomPackageManager](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/CustomPackageManager). Called in :Load\(\) |
| UnloadPackageConfig\(...\) | Same as in [CustomPackageManager](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/CustomPackageManager). Called in :Unload\(\) |
| AddFileWithCheck\(...\) | Same as in [CustomPackageManager](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/CustomPackageManager) |

