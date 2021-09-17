# Menu

Updated for version 3.38.

## Module Definition

The module is inherited from [ModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase). So base parameters can be found there.

**Note**: The module is one of the original modules of BeardLib and was never really touched until version 3.38. It's still missing some features and is really only used to build menus and nodes and not the items themselves. It's used in PDTH HUD to build the options menu inside a sub menu.

I might update it or I might create a whole new module for building MenuUI menus instead which are superior than these menus.

### Module name

The name of the module you use as the meta of the module definition is 'Menu' or 'MenuModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<Menu parent_node name node_name title_id desc_id>
    <merge_data ...>
        ...
    </merge_data>
    <sub_menu key ...>
        ...
    </sub_menu>
    <item_group key/>
    <divider name size>
        <merge_data ...>
            ...
        </merge_data>
    </divider>
</Menu>
```

#### `<menu parent_node name node_name title_id desc_id>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| parent\_node | string | The key/name of the node which the menu should be parented to |
| name | String | The foundation of the base name of the node. Defaults to the name of the mod plus the defined name of the module \(name parameter or "Menu"\) |
| node\_name | String | The name of the node, defaults to the resulting `name` + Node |
| title\_id | String | Localization id of the title of the node's button, defaults to the resulting `name` + ButtonTitleID |
| desc\_id | String | Localization id of the desc of the node's button, defaults to the resulting `name` + ButtonDescID |

#### `<sub_menu key ...> ...`

This can be any of the parameters you see in the main `menu` node. Only has an affect if `key` is not specified.

| Parameter | Type | Description |
| :--- | :--- | :--- |
| key | String | The key/name of the module you may or may not be referencing for the creation of the items for this menu. \[OPTIONAL\]. If this is specified, the 'BuildMenu' function will be called on the module with the key, to create the items for this menu. |

#### `<item_group key/>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| key | String | The key/name of the module you are referencing for creating the items inside the current node. \[REQ\], with this the 'InitializeNode' function will be called on the module to create the items from the Module inside of the current node |

#### `<divider name size>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| name | String | The name of the divider |
| size | Number | The height of the divider |

#### `<merge_data ...> ...`

Any additional parameters you wish to be included in the table

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<Menu>
    <menu>
        <sub_menu key="Options"/>
        <divider name="Divider" size="20"/>
    </menu>
</Menu>
```

This will produce an options menu in the Mod Options node. With the Options sub\_menu. and a divider.

### Functions

| Function | Description |
| :--- | :--- |
| BuildNode\(Table node\_data, Table parent\_node\) | Builds the node. `node_data` is the node data; what the head of the module will contain. `parent_node` is the parent node for the node to reside in. Defaults to the mod options menu \(If node\_data has a parent\_node it will use that instead\). Called by the `Load()` function from the `MenuManagerSetupCustomMenus` hook |
| BuildNodeItems\(Table node, Table data\) | Builds the node items. `node` is the node the items will be created in. `data` is the data of the items. Called by `BuildNode`. |
| CreateDivider\(Table node, Table tbl\) | Creates a divider. `parent_node` is the parent node the item should be in. `tbl` is the data of the divider |

