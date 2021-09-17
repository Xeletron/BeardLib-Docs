# DLC

Updated for version 3.38.

This page is incomplete.

## Module Definition

The module is inherited from [ModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase). So base parameters can be found there.

Let's you make a DLC.

### Module name

The name of the module you use as the meta of the module definition is 'DLC' or 'DLCModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<DLC id>
    <content loot_global_value>
        <loot_drops/>
        <upgrades/>
    </content>
</DLC>
```

#### `<DLC id>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String | The ID of the DLC |

#### `<content loot_global_value ...>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| loot\_drops | Table | Items that can drop \(use value\_node\) |
| upgrades | Table | ... |
| loot\_global\_value | String | The global value of this DLC. |

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<DLC id="beard"/>
```

This will add a DLC named beard.

