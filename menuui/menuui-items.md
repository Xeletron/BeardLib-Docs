# Items

**This page is missing some information and will be updated**

All items including menus inherit the **Item** class, this means that all values and functions that this class has they have too.

## Item / Button

#### Basic values

* `name` \[String\] The name of the item, used to identify the item.
* `text` \[String\] The text or string\_id\(if localized\) of the item's title.
* `help` \[String\] If defined, this will show help text in a tooltip near the item.
* `on_callback` \[Function\] The function that should be called if the item got its value changed or pressed\(buttons only\) The function gets called with the "item" parameter which you can use to get the value from.
* `enabled` \[Boolean\] Is the item enabled. If disabled, the item is grayed out.
* `visible` \[Boolean\] Should the item be rendered?
* `label` \[Anything\] Sets a "label" to the item, can be used if you need to mark a few items, delete items with label x or get items with label x.
* `position` \[Function/String/Table\]  Sets a custom position for the item, this overrides align items.
  * Function: function\(item\) item:Panel\(\):set\_position\(0, 10\) end
  * String: Left, Right, Top, Bottom, Center\(can be combined\)
  * Table: {0, 10}
* `index` \[Number\] Lets you insert the item in a specific place, setting this to 1 will put it as first item.
* `on_right_click` \[Function\] A function that should be called when pressing right click on an item\(will not work if you have a context menu and did not change its key from right click\)
* `inherit_value` \[Table\] A table where you can define values to **only** inherit to the items, this means that if you put a value inside of it and have a different value outside of it the outer one will not be inherited. Values that can inherit from other values like `help_localized` can from `localized` will not inherit as you'd expect them to.
* `private` \[Table\] A table that sets private values, any value inside of it will **not** inherit to the children at all.
* `highlight` \[Boolean\] Should the item be highlighted as soon as it's created?

#### Context menu

* `items` \[Table\] Tells the item you need a context menu, the items can be defined like this: 
  * {{text = "Item" on\_callback = ClassClbk\(self, "clbk"\)}, "An item without callback"} _Currently you can't use a context menu on a ComboBox_.
* `open_list_key` \[String/Idstring\] Changes the key that opens the list\(only mouse keys, left = "0" right = "1"\(default\)\)
* `searchbox` \[Boolean\] Adds a searchbox to the context menu.

#### Inherit values

_Values that if are defined from a menu, are inherited by their items._

* `localized` \[Boolean\] Is the item localized? defaults to false.
* `items_localized` \[Boolean\] Are context menu or combobox items localized? Defaults to `localized` value.
* `help_localized` \[Boolean\] Is the help text localized? Defaults to `localized` value.
* `size` \[Number\] The size of the item, defaults to 18.
* `offset`\[Number/Table\] How much is the item pushed in its x and y position\(will shrink the item horizontally\).

  Typing a number will use that number for x,y offset.

* `text_offset`\[Number/Table\] Like offset but inside the item itself\(will grow the item vertically\).
* `font` \[String\] Font of the item. Defaults to "fonts/font\_large\_mf"
* `font_size` \[Number\] The size of the font\(currently it might not be recommended to use it, use "size" instead\).
* `kerning` \[Number\] The kerning of the text, like spacing between characters.
* `text_align`\[String left/center/right\] The horizontal placement of the text inside its own body, defaults to left.
* `text_vertical` \[String top/center/bottom\] Same as text\_vertical but vertically, defaults to top.
* `size_by_text` \[Boolean\] Sets the item's size based of its text\(used mostly by buttons and dividers\)
* `ignore_align` \[Boolean\] Should align items ignore the item when aligning?

#### Customization

_Who doesn't like that ;\)_

\* - _Does not inherit_

* `foreground` The foreground color, this includes text, anything beyond the background.
* `foreground_highlight` The foreground but when highlighted.
* `auto_foreground` MenuUI will try to guess which foreground color\(white or black\) will fit to the background color.
* `background_color` Color of the background for the item.
* `highlight_color` The color of the background for the item but when highlighted.
* `accent_color` Accent color of the item, is set automatically for things like border color, scroll color and more.
* `line_color` Some items like the texbox and combobox have a line below their control, this controls their color, defaults to accent\_color.
* `enabled_alpha`\[Number 0-1\] The opacity of the item while enabled, defaults to 1.
* `disabled_alpha` \[Number 0-1\] The opacity of the item when disabled, defaults to 0.5.
* `control_slice` \[Number 0-1\] The "slice" of the control, for example, the slider's slide, defaults to 0.5\(50%\).
* `w`\[Number\] A constant width for the item.
* \*`max_width`\[Number\] This sets a maximum value for the width.
* \*`min_width`\[Number\] This sets a minimum value for the width.
* \*`max_height`\[Number\] This sets a maximum value for the height.

  \*`min_height`\[Number\] This sets a minimum value for the height.

* `last_y_offset` \[Number\] Normally when the align items function reaches the end, it takes the last item's offset\(or the one with largest bottom position\) and adds it to the menu's height, this overrides it.
* `background_alpha` \[Number\] Opacity for the background.

#### Animations

_Hopefully expanded in the future_

* `animate_colors` Should colors in the item be animated\(on highlighting/un-highlighting\)

#### Border

* `border_color` Color for the border if used.
* `border_visible` \[Boolean\] Sets the whole border visible.
* `border_left` \[Boolean\] Sets the left border visible.
* `border_right` \[Boolean\] Sets the right border visible.
* `border_top` \[Boolean\] Sets the top border visible.
* `border_bottom` \[Boolean\] Sets the bottom border visible.
* `border_lock_height` \[Boolean\] Locks the height of the border to the title's height instead of the whole item.
* `border_center_as_title` \[Boolean\] Positions the border around the title.
* `border_position_below_title` \[Boolean\] Sets the bottom border below the title.

  _Will probably change in the future to make it less confusing._

* `border_size` \[Number\] The size of the border, probably can be used to set a size for the all border sides.
* `border_width` \[Number\] Width of the border.
* `border_height` \[Number\] Height of the border.
* `override_panel` \[MenuUI Item\] Can be used to override the panel of the item. For example, if you want to put the item inside a button.

#### Functions

* `Name()` Returns the name of the item.
* `Text()` Returns the text of the item.
* `Label()` Returns the label of the item if is set.
* `SetEnabled(boolean enabled)` Sets whether the item is enabled or not.
* `SetVisible(boolean visible, boolean no_align)` Sets whether the item is visible or not. Normally if you set something visible or not the menu has to update itself so it can re-align items properly `no_align` can disable that if is set to true\(mostly used for optimization\)
* `SetCallback(function callback)` Sets a callback for the item.
* `SetLabel(anything label)` Sets a label for the item.
* `Configure(params)` Sets new parameters for the item and recreats the item.
* `Enabled()` Returns if the item is enabled.
* `Visible()` Returns if the item is visible.
* `Destroy()` Destroys the item\(Don't worry it's safe to call\).
* `Index()` Returns the place of the item. You should use this instead of item.index as this will find the exact place of it.
* `SetIndex(number index, boolean no_align)` Sets an index for the item, no\_align will disable auto aligning if is set to true\(important for the item's position to update\).
* `SetLayer(number layer)` Sets a layer for the item. In other words, the higher the layer the higher it will be among other panels.
* `RunCallback(function clbk, params...)` Runs clbk or `on_callback` if is set, the callback will be called with the item as first parameter and then `params...` which can be anything.
* `Panel()` Returns the GUI panel of the item.
* `Parent()` Returns the parent menu of the item.
* `ParentPanel()` Returns the parent GUI panel of the item's panel.
* `TextHeight()` Returns the height of the title if is alive or 0 if not.
* `Inside(number x, number y)` Returns whether `x` and `y` is inside the item.
* `MouseFocused(number x, number y)` A better version of `Inside` that checks if the item is alive and visible and will use the mouse position if x and y are not defined.
* `alive()` Returns if the item's GUI panel is alive. Lets you do stuff like this: alive\(item\).
* `title_alive()` Returns whether the item has an alive title GUI text, mostly used internally.

**Position and Size Functions**

* `SetPosition(number x, number y)` Sets an exact position using X and Y.
* `SetPosition(table position)` Sets an exact position using X and Y inside a table\(like {0, 10}\).
* `SetPosition(function position)` Sets a position function, might look like this: function\(item\) item:Panel\(\):set\_x\(0\) end.
* `SetPosition(string position)` Sets a string position for the item, like: Left, Right, Top, Bottom, Center\(can be combined\).
* `X` Returns the X position.
* `Y` Returns the Y position.
* `W()/Width()` Returns the width.
* `H()/Height()` Returns the height.
* `Right` Returns the right position.
* `AdoptedItems()` Returns items taht were "adopted" by the item\(aka injected\).
* `Position()` Returns the last set position\(not exact position\).
* `Location()/LeftTop()` Returns the exact position of the item\(X,Y\).
* `RightTop()` Returns right and top\(Y\) position.
* `LeftBottom()` Returns left\(X\) and bottom position.
* `RightBottom()` Returns right and bottom position.
* `Center()` Returns the center X,Y position.
* `CenterX()` Returns the center X position.
* `CenterY()` Returns the center Y position.
* `OuterWidth()` Returns the X position added with X offset.
* `OuterHeight()` Returns the Y position added with Y offset.
* `Offset()` Returns the offset.
* `OffsetX()` Returns the X offset.
* `OffsetY()` Returns the Y offset.
* `TextOffset()` Returns the text offset.
* `TextOffsetX()` Returns the X text offset.
* `TextOffsetY()` Returns the Y text offset.

## ComboBox

#### Values

* `items` \[Table\] The items of the ComboBox, can be like:
  * {"First", "Second", "Third"}
  * * They can even have their own callback:  note: The original callback still runs.
* `value` \[Anything\] Index/Key of the selected item, if free\_typing is enabled can be a string.
* `free_typing` \[Boolean\] Should the combobox act as a textbox? This means the values will save even if it's not inside the items, calling Item:Value\(\) or item.value will not always return an index. 

#### Functions

* `Value()` Returns the index/key of the selected item.
* `SetItems(table items)` Sets the items of the ComboBox, items being the new items.
* `SetValue(anything value, boolean run_callback, boolean no_items_clbk)` Sets the value of the item. `value` is mostly the index of the selected item but can be a string if free\_typing is enabled, `run_callback` determines if any callback should be called and `no_items_clbk` will disable individual callbacks for items if enabled.
* `SetSelectedItem(string/table item, boolean run_callback, boolean no_items_clbk)` Sets the selected item or if free\_typing is enabled sets the value. Note: `item` has to be the exact value of what you want to select, if it's a table then you need to give this function the table.
* `SelectedItem()` Returns the currently selected items or if free\_typing is enabled the value written.

## Slider

#### Values

* `value` \[Number\] Value of the slider, has to be in range of the set min/max. Defaults to 0.
* `min` \[Number\] The minimum value that can be set in the slider. Defaults to `value`'s number..
* `max` \[Number\] The maximum value that can be set in the slider. Defaults to `value`'s number..
* `step` \[Number\] How much should be added/subtracted to the value every time you increase/decresae the number using wheel control. Defaults to 1.
* `floats` \[Number\] How much decimal points does the number allowed to have? Defaults to 3 and can be inherited.
* `wheel_control` \[Boolean\] Should the slider be controlled by the mouse wheel as well? Defaults to false and can be inherited.

#### Functions

* `Value()` Returns the number value of the slider.
* `SetValue(number value, boolean run_callback)` Sets the value of the item. `value` is the number value and `run_callback` decides whether to run the callback after the value is set.
* `SetValueByPercentage(number percent, boolean run_callback)` like `SetValue` but sets using a percentage value.
* `SetStep(number step)` Sets the step value.

## TextBox / NumberBox

#### Why would you use NumberBox instead of Slider?

* You don't have to set a minimum and a maximum.
* Sliding is not based on mouse position but is based on step.
* You prefer the style of the numberbox.

#### Values

* `value` \[String\] Value of the textbox.
* `filter` \[String\] Currently only used to make the textbox numbers only by setting this value to "number"\(NumberBox pretty much\)
* `lines` \[Number\]
* `forbidden_chars` \[Table\] Characters that the textbox shouldn't allow to type\(does not affect SetValue\).
* `focus_mode` \[Boolean\] Normally if the mouse exits the textbox this closes the textbox, if you turn this on, only when you press enter or click with the mouse somewhere it will close the textbox.
* `auto_focus` \[Boolean\] If `focus_mode` is on, this will auto focus the textbox without you actually press the mouse, this is used in the InputDialog so you can type as soon as the dialog opens.
* `step` \[Number\] How much should be added/subtracted to the value every time you slide the number by holding right mouse button and move the mouse.
* `floats` \[Number\] Same as slider the one in slider but only active with NumberBox\(filter="number"\).
* `no_slide` \[Boolean\] Turns off sliding of the number if the textbox is a numberbox.

#### Functions

* `Value()` Returns the value of the textbox.
* `SetValue(String/Number value, Boolean run_callback)` Sets the value of the item. `value` is the string value if it's a textbox or number value if it's a numberbox, `run_callback` decides whether to run the callback after the value is set.
* `SetStep(number step)` Sets the step value, use only if it's a numberbox.

## ColorTextBox

Very similar to textbox but for colors. Read about TextBox before reading about this.

#### Values

* `value` \[String/Color\] A hex value\(string/argb\) of the color or a color value.
* `color_dialog` \[Boolean\] Should a color dialog show up\(It has a cool ARGB slider :c\)

#### Functions

* `Value()` Returns the color of the item.
* `HexValue()` Returns the color of the item in hex format.
* `SetValue(string value, ...)` Sets the color of the item, can be both hex color and color, the rest of the parameters are explained in TextBox.

## Toggle

### Values

* `value` \[Boolean\] Value of the toggle true for on false for off.

  **Functions**

* `Value()` Returns the boolean value of the toggle.
* `SetValue(boolean value, boolean run_callback)` Sets the value of the item. `value` is the boolean value and `run_callback` decides whether to run the callback after the value is set.

## Keybind

#### Values

* `value` \[String\] The keybind key. Defaults to none.
* `supports_keyboard` \[Boolean\] Should the item listen to the keyboard? Defaults to true and the value can be inherited.
* `supports_mouse` \[Boolean\] Should the item listen to the mouse? Defaults to false and the value can be inherited.

#### Functions

* `Value()` Returns the keybind as a string
* `GetKeyBind()` Returns the keybind but in idstring form.
* `SetValue(string value, boolean run_callback)` Sets the value of the item. `value` is the keybind key and `run_callback` decides whether to run the callback after the value is set.

## ImageButton

#### Values

* `texture` Texture of the image.
* `texture_rect` Texture rectangle of the image, if used. Pivot points have to be left and top of what you need.
* `icon_w` Specific width for the image\(unlike 'w' which gets subtracted with the x image offset\)
* `icon_h` Specific height for the image\(unlike 'h' which gets subtracted with the y image offset\)
* `img_offset` \[Table/Number\] Offset for the image, useful if you want to have the image smaller while button itself bigger, defaults to {0,0}
* `img_offset_x` \[Number\] Specific x offset for the image.
* `img_offset_y` \[Number\] Specific y offset for the image.
* `highlight_image` \[Boolean\] Should the image change color when highlighting\(uses forground color\)

#### Functions

* `SetImage(texture, texture_rect)` Sets a texture and texture rectangle for the item.

