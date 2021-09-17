# Slider

Updated for 3.36.

**It's recommended to first read about the base item before reading about other items** [https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item)

## Slider

### Creation

```lua
MyRandomMenu:Slider({
    name = "MySlider",
    text = "Slider of many numbers",
    value = 1,
    min = 0,
    max = 1,
    on_callback = function(item)
        log("Value changed!", tostring(item:Value()))
    end
})
```

### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| value | Number | Value of the slider, has to be in range of the set min/max. Defaults to 0 |
| min | Number | The minimum value that can be set in the slider. Defaults to `value`'s number |
| max | Number | The maximum value that can be set in the slider. Defaults to `value`'s number |
| step | Number | How much should be added/subtracted to the value every time you increase/decresae the number using wheel control. Defaults to 1 |
| floats | Number | How much decimal points does the number allowed to have? Defaults to 3 and can be inherited |
| wheel\_control | Boolean | Should the slider be controlled by the mouse wheel as well? Defaults to false and can be inherited |

### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| Value\(\) | Number | Returns the number value of the slider |

#### Set

| Function | Description |
| :--- | :--- |
| SetValue\(Number value, Boolean run\_callback\) | Sets the value of the item. `value` is the number value and `run_callback` decides whether to run the callback after the value is set |
| SetValueByPercentage\(Number percent, Boolean run\_callback\) | like `SetValue` but sets using a percentage value |
| SetStep\(Number step\) | Sets the step value |

