# Toggle

Updated for version 3.36.

**It's recommended to first read about the base item before reading about other items** [https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item)

## Toggle

### Creation

```lua
MyRandomMenu:Toggle({
    name = "MyToggle",
    text = "This is a toggle",
    value = true,
    on_callback = function(item)
        log("I was toggled to", tostring(item:Value()))
    end
})
```

### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| value | Boolean | Value of the toggle true for on false for off |

#### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| Value\(\) | Boolean | Returns the boolean value of the toggle |

#### Set

| Function | Description |
| :--- | :--- |
| SetValue\(Boolean value, Boolean run\_callback\) | Sets the value of the item. `value` is the boolean value and `run_callback` decides whether to run the callback after the value is set |

