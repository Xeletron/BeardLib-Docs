Updated for version 3.38.
# Module Definition

The module is inherited from [ItemModuleBase](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/ModuleBase#ItemModuleBase). So base parameters can be found there.

This modules let's you add masks.

## Module name

The name of the module you use as the meta of the module definition is 'Mask' or 'MaskModule' if `_force_search` is set to true in the module definition.

## XML Structure
```xml
<Mask id global_value unit type .../>
```

### `<Mask ...>`
|Parameter|Type|Description|
|--|--|--|
|id|String|The ID of the material|
|type|String|The type of the mask. Can be helmet, beard, glasses and mask. Defaults to mask.
|global_value|String|For packs of mods, a global id assigned to all. A nice way to label your mods. You'll still have to create the global value through [GlobalValueModule](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/GlobalValueModule)
|unit|String|Optional path to the unit of the mask. Defaults to units/mods/masks/msk_`id`/msk_`id` You still need to add it through [AddFiles](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/AddFilesModule) and all its dependencies such as object and material config.|
|offsets|Table|Optional table of offsets for each character. Should look something like this: <br>`<offsets>`<br>`<old_hoxton>`<br>`<value_node value="0 0 0">`<br>`<value_node value="Rotation(0,0,0)">`<br>`</old_hoxton>`<br>`</offsets>`<br>Each character needs position and rotation offset. First is position and second is rotation.
|name_id|String|Localization ID for the title of the mask (Defaults to bm_msk_ + `id`)
|desc_id|String|Localization ID for the description of the mask (Defaults to bm_msk_ + `id`)
|texture_bundle_folder|String|Optional folder to contain the icon. The path will be guis/dlcs/`texture_bundle_folder`/textures/pd2/blackmarket/icons/masks/`id`. Defaults to `mods`|
|characters|Table|Optional table that contains characters and the mask for them. This allows you to have a unique mask for each character (See bm_msk_balaclava in masks tweakdata)|


And any other tweakdata value. There are more that are not listed here yet.

### The icon
The icon will be stored in guis/dlcs/mods/textures/pd2/blackmarket/icons/masks and will be named `id`.texture then add it using [AddFiles](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/AddFilesModule).


## Example

This example is what you would put inside your main node within your [mod config](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/Module-Config)

```xml
<Mask id="my_cool_mask" type="helmet"/>
```

This will add the mask `my_cool_mask`. You will still need to localize the title and description of the mask. In this case `bm_msk_my_cool_mask` and `bm_msk_my_cool_mask_desc` will need to be localized using [LocalizationModule](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/LocalizationModule). And add unit, object, material_config, textures and icon through [AddFiles](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/AddFilesModule)

### Template
Download template here: [here](https://minhaskamal.github.io/DownGit/#/home?url=https://github.com/Luffyyy/BeardLib-Templates/tree/master/Mask-Template)
