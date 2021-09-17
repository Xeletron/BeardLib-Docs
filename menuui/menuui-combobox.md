# ComboBox

Updated for version 3.37.

**It's recommended to first read about the base item before reading about other items** [https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item)

## ComboBox

### Creation

```lua
MyRandomMenu:ComboBox({
    name = "MyComboBox",
    text = "MANY ITEMS",
    items = {"OOO", {text = "Boop", on_callback = function() log("Booped") end}},
    value = 1,
    on_callback = function(item)
        log("Selected item", tostring(item:SelectedItem()))
        log("Index", tostring(item:Value()))
    end
})
MyRandomMenu:ComboBox({
    name = "MyComboBox2",
    text = "ITEMS",
    items = {"OOO", "Simple", "Yes"},
    value = 1,
    on_callback = function(item)
        log("Selected item", tostring(item:SelectedItem()))
        log("Index", tostring(item:Value()))
    end
})
```

### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| items | Table | The items of the ComboBox, can be like: `{"First", "Second", "Third"}` `{{name = "First" whatever="yes"}, "Second", {name = "Third" whatever="lol"}}` They can even have their own callback: `{{name = "Item with a callback", on_callback = ClassClbk(self, "clbk")}}` Note: The original callback still runs |
| value | Any | Index/Key of the selected item, if free\_typing is enabled can be a string |
| free\_typing | Boolean | Should the combobox act as a textbox? This means the values will save even if it's not inside the items, calling Item:Value\(\) or item.value will not always return an index |
| items\_uppercase | Boolean | Makes all items' text capitalized |
| items\_lowercase | Boolean | Makes all items' text non-capitalized |

### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| Value\(\) | Any | Returns the index/key of the selected item |
| SelectedItem\(\) | Any | Returns the currently selected items or if free\_typing is enabled the value written |

#### Set

| Function | Description |
| :--- | :--- |
| SetItems\(Table items\) | Sets the items of the ComboBox, items being the new items |
| SetValue\(Number value, Boolean run\_callback, Boolean no\_items\_clbk\) | Sets the value of the item. `value` is mostly the index of the selected item but can be a string if free\_typing is enabled, `run_callback` determines if any callback should be called and `no_items_clbk` will disable individual callbacks for items if enabled |
| SetSelectedItem\(Some item, Boolean run\_callback, Boolean no\_items\_clbk\) | Sets the selected item or if free\_typing is enabled sets the value. Note: `item` has to be the exact value of what you want to select, if it's a table then you need to give this function the table |

#### Other

| Function | Description |
| :--- | :--- |
| Clear\(\) | Clears all items |
| Append\(Any item\) | Appends an item to the items list |
| Prepend\(Any item\) | Prepends an item to the items list |
| RefreshList\(\) | Refreshes the list |

