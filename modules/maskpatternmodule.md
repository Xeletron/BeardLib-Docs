# Mask Pattern

Updated for version 3.38.

## Module Definition

The module is inherited from [ItemModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase#ItemModuleBase). So base parameters can be found there.

This modules let's you add mask patterns.

### Module name

The name of the module you use as the meta of the module definition is 'MaskPattern' or 'MaskPatternModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<MaskPattern id texture global_value/>
```

#### `<MaskPattern ...>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String | The ID of the pattern |
| texture | String | Optional path of the pattern's texture. If you're loading a custom one you'll need to load it through [AddFiles](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/AddFiles) first. Defaults to units/mods/masks/shared_textures/pattern_`id` |
| global\_value | String | For packs of mods, a global id assigned to all. A nice way to label your mods. You'll still have to create the global value through [GlobalValueModule](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/GlobalValueModule) |
| name\_id | String | A localization ID for the pattern \(Defaults to pattern\_ + `id` + \_title\) |

And any other tweakdata value. There are more that are not listed here yet.

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<MaskPattern id="spade"/>
```

This will add the mask pattern `spade`. You will still need to localize the name of the pattern. In this case `pattern_spade_title` will need to be localized using [LocalizationModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/LocalizationModule). And add the texture which in this is in "units/mods/masks/shared\_textures/pattern\_spade" through [AddFiles](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/AddFiles)

#### Template

Download template [here](https://minhaskamal.github.io/DownGit/#/home?url=https://github.com/ModWorkshop/BeardLib-Templates/tree/master/Pattern-Template)

