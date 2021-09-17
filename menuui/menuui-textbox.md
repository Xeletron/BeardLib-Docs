# TextBox

Updated for version 3.37.

**It's recommended to first read about the base item before reading about other items** [https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item)

## TextBox / NumberBox

### Creation

```lua
MyRandomMenu:TextBox({
    name = "MyTextBox",
    text = "Text box",
    value = "Textbox value",
    on_callback = function(item)
        log("Value changed!", tostring(item:Value()))
    end
})
```

Or if a NumberBox:

```lua
MyRandomMenu:NumberBox({
    name = "MyNumberBox",
    text = "Number box",
    value = "0",
    on_callback = function(item)
        log("Value changed!", tostring(item:Value()))
    end
})
```

### Why would you use NumberBox instead of Slider?

* You don't have to set a minimum and a maximum.
* Sliding is not based on mouse position but is based on step.
* You prefer the style of the numberbox.

### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| value | String | Value of the textbox |
| filter | String | Currently only used to make the textbox numbers only by setting this value to "number"\(NumberBox pretty much\) |
| lines | Number | How many lines the item can have \(Not really maximum lines at the moment..\) |
| forbidden\_chars | Table | Characters that the textbox shouldn't allow to type\(does not affect SetValue\) |
| focus\_mode | Boolean | Normally if the mouse exits the textbox this closes the textbox, if you turn this on, only when you press enter or click with the mouse somewhere it will close the textbox |
| auto\_focus | Boolean | If `focus_mode` is on, this will auto focus the textbox without you actually press the mouse, this is used in the InputDialog so you can type as soon as the dialog opens |
| step | Number | How much should be added/subtracted to the value every time you slide the number by holding right mouse button and move the mouse |
| floats | Number | Same as slider the one in slider but only active with NumberBox\(filter="number"\) |
| no\_slide | Boolean | Turns off sliding of the number if the textbox is a numberbox |
| fit\_text | Boolean | Fit text shrinks the text if the text is too large to fit the whole textbox |

### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| \`Value\(\) | String/Number | Returns the value of the textbox |

#### Set

| Function | Description |
| :--- | :--- |
| SetValue\(String/Number value, Boolean run\_callback\) | Sets the value of the item. `value` is the string value if it's a textbox or number value if it's a numberbox, `run_callback` decides whether to run the callback after the value is set |
| SetStep\(Number step\) | Sets the step value, use only if it's a numberbox |

## ColorTextBox

Pretty much TextBox but modified for colors

### Creation

```lua
MyRandomMenu:ColorTextBox({
    name = "ColorItem",
    text = "My cool color",
    value = Color(1,1,1),
    on_callback = function(item)
        log("New color!", tostring(item:Value()))
    end
})
```

### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| value | String/Color | A hex value\(string/argb\) of the color or a color value |
| no\_color\_dialog | Boolean | Should the color dialog not show up when pressing item \(It has a cool ARGB slider :c\) |
| use\_alpha | Boolean | Should the color dialog include option for transparency slider? Defaults to true |

### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| \`Value\(\) | Color | Returns the color of the item |
| \`HexValue\(\) | String | Returns the color of the item in hex format |
| \`VectorValue\(\) | Vector3 | Returns the vector color of the item \(Vector3\(value.r, value.g, value.b\)\) |

#### Set

| Function | Description |
| :--- | :--- |
| \`SetValue\(String value, ...\) | Sets the color of the item, can be both hex color and color the rest of the parameters are explained in TextBox |

