# Adding your own modules

Updated for version 3.38.

## Module Definition

The module is inherited from [ItemModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase#ItemModuleBase). So base parameters can be found there.

This modules let's you add custom modules.

### Module name

The name of the module you use as the meta of the module definition is 'Modules' or 'ModulesModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<Modules directory>
    <module file name type_name/>
    <modules directory>
</Modules>
```

#### `<Modules directory>` / `<modules directory>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| directory | String | An optional directory for the modules. All modules will join their file to this directory |

#### `<module file name type_name/>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| file | String | The file path to module. This will join the mod path + `directory` |
| type\_name | String | The friendly/short name for your module to be defined from BeardLib mods |
| name | String | The name of the module class you just made in your file. Defaults to `type_name` + Module |

### Warning

Modules loaded through this method have to be loaded from mods that have very high priority; making sure all mods that want to use this module, are able to.

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<Modules directory="Modules">
    <module file="FoodModule.lua" name="FoodModule" type_name="Food"/>
</Modules>
```

The module will inherit either ModuleBase or ItemModuleBase \(for tweakdata stuff\)

Modules/FoodModule.lua:

```lua
FoodModule = FoodModule or class(ModuleBase)

function FoodModule:Load()
    self:OrderFood()
end

function FoodModule:OrderFood()
    local order = self._config.order
    -- TODO
end
```

And a mod that would want to use this module:

```markup
<Food order="spaghetti"/>
```

This adds a food module! The heisters are pretty hungry after a day of heisting so they gotta eat.

Just... Gotta code it.

