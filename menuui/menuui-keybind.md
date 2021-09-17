# Keybind

Updated for version 3.36.

**It's recommended to first read about the base item before reading about other items** [https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item)

## Keybind

### Creation

```lua
MyRandomMenu:Keybind({
    name = "MyKeybind",
    text = "Keybind item",
    value = "f1",
    on_callback = ClassClbk(self, "MyClbk")
})
```

### Parameters

| Parameter | Return Type | Description |
| :--- | :--- | :--- |
| value | String | The keybind key. Defaults to none |
| supports\_keyboard | Boolean | Should the item listen to the keyboard? Defaults to true and the value can be inherited |
| supports\_mouse | Boolean | Should the item listen to the mouse? Defaults to false and the value can be inherited |

### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| Value\(\) | String | Returns the keybind as a string |
| GetKeyBind\(\) | Idstring | Returns the keybind but in idstring form |

#### Set

| Function | Description |
| :--- | :--- |
| SetValue\(String value, Boolean run\_callback\) | Sets the value of the item. `value` is the keybind key and `run_callback` decides whether to run the callback after the value is set |

