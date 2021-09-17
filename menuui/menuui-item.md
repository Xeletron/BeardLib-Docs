# Item

Updated for version 3.38.

Back to [MenuUI](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI)

All items including menus inherit the **Item** class. This means that all values and functions that this class has they have too. **This includes Menus too**.

## Item / Button / Divider

### Creation

Can be created inside menu type items:

```lua
MyRandomMenu:Button({
    name = "MyButton",
    text = "Press me!",
    on_callback = function(item)
        log("I was pressed!")
    end
})
```

Or if a Divider:

```lua
MyRandomMenu:Divider({
    name = "Divider",
    text = "I cannot be pressed :("
})
```

You can also create a quick divider like this

```lua
MyRandomMenu:Text("another_div")
```

### Parameters

#### Basic values

| Parameter | Type | Description |
| :--- | :--- | :--- |
| name | String | The name of the item, used to identify the item |
| text | String | The text or String\_id\(if localized\) of the item's title |
| help | String | If defined, this will show help text in a tooltip near the item |
| on\_callback | Function | The function that should be called if the item got its value changed or pressed\(buttons only\) The function gets called with the "item" parameter which you can use to get the value from |
| enabled | Boolean | Is the item enabled. If disabled, the item is grayed out |
| visible | Boolean | Should the item be rendered? |
| label | Any | Sets a "label" to the item, can be used if you need to mark a few items, delete items with label x or get items with label x |
| position | Function/String/Table | Sets a custom position for the item, this overrides align items Function: function\(item\) item:Panel\(\):set\_position\(0, 10\) end String: Left, Right, Top, Bottom, Center\(can be combined\) Table: {0, 10} |
| index | Number | Lets you insert the item in a specific place, setting this to 1 will put it as first item |
| on\_right\_click | Function | A function that should be called when pressing right click on an item\(will not work if you have a context menu and did not change its key from right click\) |
| inherit\_value | Table | A table where you can define values to **only** inherit to the items. If you put a value inside of it and have a different value outside of it the outer one will not be inherited. Values that can inherit from other values like `help_localized` can from `localized`, will not inherit as you'd expect them to |
| private | Table | A table that sets private values, any value inside of it, will **not** inherit to the children at all |
| highlight | Boolean | Should the item be highlighted as soon as it's created? |
| divider\_type | Boolean | This makes the item a "divider". Essentially disabling some mouse events. This usually means that no callbacks will be called and the item doesn't highlight at all. For groups this disables closing/opening of the group making them static |
| ignore\_align | Boolean | Should align items ignore the item when aligning? |
| count\_as\_aligned | Boolean | Normally, if you set a custom position to the item or use ignore\_align, MenuUI will ignore the item when aligning the item \(no item will use its position\) This bypasses this behavior |

#### Inherit values

_Values that if are defined from a menu, are inherited by their items._

| Parameter | Type | Description |
| :--- | :--- | :--- |
| localized | Boolean | Is the item localized? defaults to false |
| items\_localized | Boolean | Are context menu or combobox items localized? Defaults to `localized` value |
| help\_localized | Boolean | Is the help text localized? Defaults to `localized` value |
| size | Number | The size of the item, defaults to 18 |
| offset | Number/Table | How much is the item pushed in its x and y position\(will shrink the item horizontally\) |
| text\_offset | Number/Table | Offset but for the text inside the item \(if present\) |
| font | String/Idstring | Font of the item. Defaults to "fonts/font\_large\_mf" |
| font\_size | Number | Font size of the item, default to `size` |
| kerning | Number | The kerning of the text, like spacing between characters |
| text\_align | String | The horizontal placement of the text inside its own body, defaults to left. Can be left, right, center or justified |
| text\_vertical | String | Same as text\_vertical but vertically, defaults to top. Can be top, bottom or center |
| size\_by\_text | Boolean | Sets the item's size based of its text\(used mostly by buttons and dividers\) |
| bg\_callbacks | Boolean | Background callbacks call through menu ui's update function instead of calling the callback right away. This is done sometimes to avoid erroring in some place or not having to wait for callbacks to finish in the main thread. Usually this should be turned off |

#### Context menu

| Parameter | Type | Description |
| :--- | :--- | :--- |
| items | Table | Tells the item you need a context menu. The items can be defined like this: `lua{{text = "Item" on_callback = ClassClbk(self, "clbk")}, "An item without callback"}` **Currently you can't use a context menu on a ComboBox** |
| open\_list\_key | String/Idstring | Changes the key that opens the list\(only mouse keys, left = "0" right = "1"\(default\)\) |
| searchbox | Boolean | Adds a searchbox to the context menu |

#### Customization values

_Who doesn't like that ;\)_

\* - _Does not inherit_

| Parameter | Type | Description |
| :--- | :--- | :--- |
| foreground | Color | The foreground color, this includes text, anything beyond the background |
| foreground\_highlight | Color | The foreground but when highlighted |
| auto\_foreground | Boolean | MenuUI will try to guess which foreground color\(white or black\) will fit to the background color |
| background\_color | Color | Color of the background for the item |
| full\_bg\_color | Color | Background that menu type items use in order to differentiate from background\_color. You should use this value for menu type items |
| unhighlight\_color | Color | Color of the item when un-highlighted \(uses background\_color otherwise\) |
| highlight\_color | Color | The color of the background for the item but when highlighted |
| accent\_color | Color | Accent color of the item, is set automatically for things like border color, scroll color and more |
| line\_color | Color | Some items like the textbox and combobox have a line below their control, this controls their color, defaults to accent\_color |
| enabled\_alpha | Float 0-1 | The opacity of the item while enabled, defaults to 1 |
| disabled\_alpha | Float 0-1 | The opacity of the item when disabled, defaults to 0.5 |
| control\_slice | Float 0-1 | The "slice" of the control, for example, the slider's slide, defaults to 0.5\(50%\) |
| w | Number | A constant width for the item |
| \*max\_width | Number | This sets a maximum value for the width |
| \*min\_width | Number | This sets a minimum value for the width |
| \*max\_height | Number | This sets a maximum value for the height |
| \*min\_height | Number | This sets a minimum value for the height |
| \*last\_y\_offset | Number | Normally when the align items function reaches the end, it takes the last item's offset\(or the one with largest bottom position\) and adds it to the menu's height, this overrides it. |
| background\_alpha | Number | Opacity for the background |
| context\_background\_color | Color | Color of the context menu if present. Defaults to background\_color \(if set\) or black color |
| scroll\_color | Color | Color of any scroll \(menu's scroll, context menu scroll etc\) |
| click\_btn | Idstring | Sets the mouse button that runs the callback of the item |
| range\_color | Table | A table that has tables with starting and ending point of the text they want to color and then the color that text should be. For example {0, 10, Color.blue} will color characters 0 to 10 green. You can also put the starting point and then the color which would assume you want the color to continue until the end of text like  this: {10, Color.green} |
| alone\_in\_row | Boolean | Determines if the item should be alone in a row \(used only with align\_method set to "centered\_grid" or "reversed\_centered\_grid"\) |

### Animation values

_Hopefully expanded in the future_

| Parameter | Type | Description |
| :--- | :--- | :--- |
| animate\_colors | Boolean | Should colors in the item be animated\(on highlighting/un-highlighting\) |

#### Border values

| Parameter | Type | Description |
| :--- | :--- | :--- |
| border\_color | Color | Color for the border if used |
| border\_visible | Boolean | Sets the whole border visible |
| border\_left | Boolean | Sets the left border visible |
| border\_right | Boolean | Sets the right border visible |
| border\_top | Boolean | Sets the top border visible |
| border\_bottom | Boolean | Sets the bottom border visible |
| border\_lock\_height | Boolean | Locks the height of the border to the title's height instead of the whole item |
| border\_center\_as\_title | Boolean | Positions the border around the title |
| border\_position\_below\_title | Boolean | Sets the bottom border below the title |
| border\_size | Number | The size of the border, probably can be used to set a size for the all border sides |
| border\_width | Number | Width of the border |
| border\_height | Number | Height of the border |

#### Context menu values

| Parameter | Type | Description |
| :--- | :--- | :--- |
| context\_screen\_offset\_y | Number | defaults to 32. Offset from top and bottom of the screen for context menus so they float a little |
| context\_font\_size | Number | defaults to 20. The text font size for context menus. |
| context\_text\_offset | Number/Table | The text offset for context menus. Offsets are either a Number for both X,Y offsets or a table |

#### Menu specific values

| Parameter | Type | Description |
| :--- | :--- | :--- |
| delay\_align\_items | Boolean | Delay align items is for any item that is a menu to essentially delay the align of items \(which meant to reduce the amount of aligns are called\) this is a good optimization method for complicated menus that you want MenuUI to automatically align |
| background\_visible | Boolean | Should background be visible? Defaults to true if the menu is not Group |
| background\_blur | Boolean | Should the background be a blurred background? \(`background_color` wil not work with this\) |
| auto\_align | Boolean | Should the menu automatically align items when for example, an item gets added or removed, an item gets its visibilty toggled? If you have many items it would be more recommended to set this to false and use manual align by calling menu:AlignItems\(true\) when you do things such as adding/removing items |

### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| Name\(\) | String | Returns the name of the item |
| Text\(\) | String | Returns the text of the item |
| Label\(\) | Any | Returns the label of the item if is set |
| Enabled\(\) | Boolean | Returns if the item is enabled |
| Visible\(\) | Boolean | Returns if the item is visible |
| Value\(\) | Any | Returns the value of the item. Only relevant for items that use a value |
| Index\(\) | Number | Returns the place of the item. You should use this instead of item.index as this will find the exact place of it |
| Key\(\) | String | Returns a unique key for the item based on diesel panel \(Changes when item is recreated\) |
| alive\(\) | Boolean | Returns if the item's GUI panel is alive. Lets you do stuff like this: alive\(item\) |
| Panel\(\) | Diesel Panel | Returns the GUI panel of the item |
| Parent\(\) | Item | Returns the parent menu of the item |
| ParentPanel\(\) | Diesel Panel | Returns the parent GUI panel of the item's panel |
| TextHeight\(\) | Number | Returns the height of the title. Will return 0 if no title is present |
| title\_alive\(\) | Boolean | Returns whether the item has an alive title GUI text, mostly used internally |

#### Set

| Function | Description |
| :--- | :--- |
| SetEnabled\(Boolean enabled\) | Sets whether the item is enabled or not |
| SetVisible\(Boolean visible, Boolean no\_align\) | Sets whether the item is visible or not. Normally if you set something visible or not the menu has to update itself so it can re-align items properly `no_align` can disable that if is set to true\(mostly used for optimization\) |
| SetText\(String text\) | Sets the title of the item |
| SetTextLight\(String text\) | Like `SetText` but lighter. Don't use ths blindly |
| SetCallback\(Function callback\) | Sets a callback for the item |
| SetLabel\(Any label\) | Sets a label for the item |
| Configure\(params\) | Sets new parameters for the item and recreats the item |
| SetIndex\(Number index, Boolean no\_align\) | Sets an index for the item, no\_align will disable auto aligning if is set to true\(important for the item's position to update\) |
| SetLayer\(Number layer\) | Sets a layer for the item. In other words, the higher the layer the higher it will be among other panels |
| SetEnabledAlpha\(Number alpha\) | Sets enabled alpha |
| SetDisabledAlpha\(Number alpha\) | Sets disabled alpha |
| SetBorder\(Table config\) | Updates the border based on `config` parameter |
| SetPointer\(String pointer\) | Basically the same as `MenuUI:SetPointer` |
| SetParam\(String k, Any v\) | Sets the parameter with the name `k` to the value of `v` |

#### Other

| Function | Description |
| :--- | :--- |
| Destroy\(\) | Destroys the item \(Don't worry it's safe to call\) |
| RunCallback\(Function clbk, ...\) | Runs clbk or `on_callback` if is set, the callback will be called with the item as first parameter and then `...` which can be anything |
| TryRendering\(\) | A function mostly used internally to check if the item should render. It will not render if it's outside of the visible area. This is done for optimization |

### Position and Size functions

#### Get

| Parameter | Type | Description |
| :--- | :--- | :--- |
| X\(\) | Number | Returns the X position |
| Y\(\) | Number | Returns the Y position |
| W\(\)/Width\(\) | Number | Returns the width |
| H\(\)/Height\(\) | Number | Returns the height |
| Right | Number | Returns the right position |
| Position\(\) | String/Table/Function | Returns the last set position\(not exact position\) |
| Location\(\)/LeftTop\(\) | Table | Returns the exact position of the item\(X,Y\) |
| RightTop\(\) | Table | Returns right and top\(Y\) position |
| Bottom\(\) | Number | Returns bottom position |
| LeftBottom\(\) | Table | Returns left\(X\) and bottom position |
| RightBottom\(\) | Table | Returns right and bottom position |
| Center\(\) | Table | Returns the center X,Y position |
| CenterX\(\) | Number | Returns the center X position |
| CenterY\(\) | Number | Returns the center Y position |
| OuterWidth\(\) | Number | Returns the X position added with X offset |
| OuterHeight\(\) | Number | Returns the Y position added with Y offset |
| Offset\(\) | Table | Returns the offset |
| OffsetX\(\) | Number | Returns the X offset |
| OffsetY\(\) | Number | Returns the Y offset |
| TextOffset\(\) | Table | Returns the text offset |
| TextOffsetX\(\) | Number | Returns the X text offset |
| TextOffsetY\(\) | Number | Returns the Y text offset |
| Inside\(Number x, Number y\) | Boolean | Returns whether `x` and `y` is inside the diesel panel of the item |
| MouseFocused\(Number x, Number y\) | Boolean | A better version of `Inside` that checks if the item is alive and visible and will use the mouse position if x and y are not defined |

#### Set

| Function | Description |
| :--- | :--- |
| SetPosition\(Number x, Number y\) | Sets an exact position using X and Y |
| SetPosition\(Table position\) | Sets an exact position using X and Y inside a table\(like {0, 10}\) |
| SetPosition\(Function position\) | Sets a position function, might look like this: function\(item\) item:Panel\(\):set\_x\(0\) end |
| SetPosition\(String position\) | Sets a String position for the item, like: Left, Right, Top, Bottom, Center\(can be combined\) |

#### Other

### Menu functions

This is more relevant for menu type items but items can use these too.

Almost all item creation functions use `params` parameter as the settings of the item. How it should be called, how it looks.

#### Item creation

_All functions return the item that is created_

| Function | Description |
| :--- | :--- |
| Button\(Table params\)/Divider\(Table params\) | Creates a [button](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item) item. \(Divider is Button with divider\_type set to true\) |
| Toggle\(Table params\) | Creates a [toggle](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Toggle) item |
| ComboBox\(Table params\) | Creates a [combobox](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-ComboBox) item |
| TextBox\(Table params\)/NumberBox\(Table params\) | Creates a [text box](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-TextBox) item. \(NumberBox is TextBox with filter set to "Number"\) |
| ColorTextBox\(Table params\) | Creates a [color text box](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-TextBox#colortextbox) item |
| Slider\(Table params\) | Creates a [slider](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Slider) item |
| KeyBind\(Table params\) | Creates a [keybind](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-KeyBind) item |
| Image/ImageButton\(Table params\) | Creates an [image button](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-ImageButton) item \(Image is ImageButton with divider\_type set to true\) |
| Holder\(Table params\) | Creates a [holder](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Menus#holder) |
| Menu\(Table params\) | Creates a [menu](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Menus#menu) |
| Group\(Table params\)/DivGroup\(Table params\) | Creates a [group](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Menus#groupdivgroup) \(DivGroup is Group with divider\_type set to true\) |
| NoteBook\(Table params\) | Creates a [notebook](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Menus#notebook) |
| ToolBox\(Table params\) | Creates a [holder](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Menus#holder) that has align set to "grid" which means items stack from left, perfect for toolbars |
| PopupMenu\(Table params\) | Creates a [popup menu](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Menus#popupmenu) |
| Text\(String text, Table params\) | Quick function to create a divider without needing to use a table |
| Create\(String type, ...\) | Allows creating any type of item from one function. For example `Item:Create("Button", {text = "something"})`. There are specific cases you'd want to use it |

#### Get

| Parameter | Type | Description |
| :--- | :--- | :--- |
| GetItem\(String name, Boolean shallow\) | Any item | Searches for an item. `name` name of the item, `shallow` limits search to current menu |
| GetItemValue\(String name, Boolean shallow\) | Any value | Uses `GetItem` function to get the item and its value \(Safe function\) |
| GetMenu\(String name, Boolean shallow\) | Any item that is a menu | Searches for an item of type menu. `name` name of the menu, `shallow` limit search to the current menu? Or search the items of the items? |
| GetMenus\(match, deep, menus\) | Any item that is a menu | Returns a table of menus that have a matching name to `match`. `deep` searches inside children too |
| GetItemWithType\(name, type, shallow\) | Any item | Basically like `GetItem` but with type specifity |
| GetItemByLabel\(Any label, Boolean shallow\) | Any item | Like `GetItem` but uses label value instead of name |
| GetItemByLabel\(Any label, Boolean shallow\) | Any item | Basically `GetItem` but uses a label instead of a name |
| Items\(\) | Table | Returns the list of the items \(Be careful it's not a cloned list and any changes to it can affect the items\) |
| ItemsWidth\(\) | Number | Returns the width of the items panel, very useful when you're trying to fit items in the menu |
| ItemsHeight\(\) | Number | Returns the height of the items panel |
| ItemsPanel\(\) | Diesel Panel | Returns the items panel |
| ShouldClose\(\) | Booolean | Used mostly by MenuUI root class to know whether the menu is focused |
| ChildrenMouseFocused\(x, y, excluded\_label\) | Boolean | Like `MouseFocused` but checks the children. `excluded_label` will not check items with their label set to it |
| GetIndex\(Item item\) | Number | Returns the index of `item` |

#### Set

| Function | Description |
| :--- | :--- |
| SetItemValue\(String name, ...\) | Uses `GetItem` function to get the item and set its value. Use it as you would use a normal `SetValue` function \(Safe function\) |
| SetChecked\(String name, Boolean checked, Boolean run\_callback\) | A quick function to find a `Toggle` item and set its value to `checked`. `run_callback` will run the callback when changed |

#### Other

| Function | Description |
| :--- | :--- |
| RecreateItems\(\) | Recreats all items |
| AlignItems\(Boolean menus, Boolean no\_parent\) | Aligns items using the set `align_method`, `menus` sets whether to align first the children menus before aligning for the menu, `no_parent` will disable aligning of parent menu after the menu is aligned\(note that when `menus` is on it sets `no_parent` to true for the children so it won't cause a stack overflow\) |
| ClearItems\(Any label\) | Clear all items. `label` if a label is defined, this will only remove items that have the label |
| RecreateItem\(Item item, Boolean align\_items\) | Recreats an item. `item` the item that should be recreated, `align_items` should items be re-aligned after the recreation? |
| RemoveItem\(Item item\) | Removes an item. Same as Item:Destroy\(\) |

### Making items into menus

You can also make items into "menus" by creating an item inside of that item like this: We use "size\_by\_text" to make the item small enough so it won't clog the whole item.

By default items have align\_method set to "grid\_from\_right" which positions the items from the right side.

This method replaces override\_panel which was really hacky and weird to use.

**Warning! Even though you can make items into menus they're not a replacement for menu type items!**

```lua
local button = MyRandomMenu:Button({
    name = "MyButton",
    text = "Press me!",
    on_callback = function(item)
        log("I was pressed!")
    end
})
button:Button({
    name = "SmallButton",
    text = "Press!",
    size_by_text = true
})
```

