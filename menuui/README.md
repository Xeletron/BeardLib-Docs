# MenuUI

Updated for BeardLib version 3.38.

MenuUI is a built-in menu system in BeardLib that allows you to make menus that are simpler, faster and better looking than the current menu system PD2 has to offer.

## Why was it created?

When I started working on the editor I was in a dilemma on whether to use the in game menu system or make my own thing. The normal menu system\(aka MenuNodeGUI\) is really limited and old. And, it's far too complex for what it's trying to achieve. Plus, not talking about how unfriendly it is when you want to do something more complex.

## What does it offer

* Simple yet extensive menu system.
* Text boxes that support copy pasting and have a history table for undo and redo and in general are much more responsive than any input box overkill made.
* Combo Boxes instead of multi choice.
* Multiple ways of positioning an item: menu aligning, absolute positions, position strings and position functions.
* Every item can host items.

## MenuUI Object

The root of your menu. This will take care of events to supply to the items such as mouse movement and keyboard input and to toggle your menu.

You can create the menu almost anytime. However, if you're creating it before managers.gui\_data gets initialized you'll have to use the "create\_items" value callback so MenuUI can create the items when it's ready.

```lua
self._menu = MenuUI:new({
    name = "YourMenuName",
    create_items = callback(self, self, "CreateItems"),
})
```

### Parameters

each value in MenuUI classes gets automatically merged into the class, you can add your own values and even replace core functions if you want! However, be careful, as some values are handled by MenuUI and will change from what you initially gave it when initializing the item.

#### Basic parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| name | String | The name of your MenuUI, can be used to identify it |
| create\_item | Function | The function will always get called when MenuUI finishes building, you don't have to use it if you're building your menu after managers.gui\_data gets created but it's recommended to use it either way |
| layer | Number | The layer is simply the drawing priority for the engine's GUI, if your menu is hidden by the default menus or any other menus you can increase this |
| enabled | Boolean | Sets the menu enabled or disabled from the moment it's created |

#### Colors/Customization

| Parameter | Type | Description |
| :--- | :--- | :--- |
| background\_color | Color | Color of the background for the MenuUI object. |
| background\_blur | Boolean | **Replaces background\_color** Should the background of the menu be blurred? |
| help\_background\_color | Color | Background color of the help popup |
| help\_color | Color | Color of the help popup text |
| help\_font | String | Font of the help popup text |
| help\_font\_size | Number | Font size of the help popup text |
| animate\_toggle | Boolean | Should MenuUI show/hide with an animation |
| show\_help\_time | Number | How much seconds after the user highlights the item should the help popup show |

### Functions:

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| Enabled\(\) | Boolean | Whether the menu is enabled or not |
| MouseInside\(\) | Boolean | If any menu has the mouse inside, useful if your menu has more functions to it |
| IsMouseActive\(\) | Boolean | Returns true if the menu has a currently active mouse \(It might not be active because of another menu that opened after it\) |
| ShouldClose\(\) | Boolean | Should the menu close, returns false if the menu is focused on something |
| GetItem\(String name, Boolean shallow\) | Any | Returns an item that has the its name equal to `name`. `shallow` searches inside the children too |
| GetMenu\(String name, Boolean shallow\) | Any menu | Returns a menu that has the its name equal to `name`. `shallow` searches inside the children too |
| GetBackground\(\) | Color | Returns the background color |
| GetItemByLabel\(String label, Boolean shallow\) | Any | Returns an item that has the its label equal to `label`. `shallow` searches inside the children too |
| Focused\(\) | Boolean | Returns true if any menu has a highlighted item or user is currently typing in an inputbox |
| Typing\(\) | Boolean | Returns true if the user is typing in an inputbox |
| Param\(Stringh param\) | Any | Returns the value of a parameter with the name of `param` |

#### Set

| Function | Description |
| :--- | :--- |
| SetEnabled\(Boolean enabled\) | Toggles the menu based on `enabled` value |
| SetParam\(String param, Any value\) | Sets the value of parameter with the name of `param` to `value` |
| ReloadInterface\(Table params, Boolean shallow\) | A function that reloads MenuUI's interface. Currently only works properly for MenuUI. `params` Parameters to update, `shallow` Reload only MenuUI? |

#### Other

| Function | Description |
| :--- | :--- |
| Enable\(\) | Enables the menu |
| Disable\(\) | Disables the menu |
| Toggle\(\) | Toggles the menu, if its enabled then it will disable the menu if not it will enable it |
| HideHelp\(\) | Hides any visible help popup |
| CloseLastList\(\) | Closes the last opened list \(not popup menus\) |
| Destroy\(\) | Destroys the menu entirely |
| RemoveItem\(Item item\) | Destroys `item` \(You can also use item:Destroy\(\) which does the same thing\) |

#### Item creation functions

MenuUI can only build menus \(although items can be menus they are still considered "items"\) Each item creation function takes the `params` as its first parameter. `params` is essentially the parameters of the menu.

| Function | Description |
| :--- | :--- |
| Holder\(Table params\) | Creates a [holder](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Menus#Holder) |
| Menu\(Table params\) | Creates a [menu](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Menus#Menu) |
| Group\(Table params\)/DivGroup\(Table params\) | Creates a [group](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Menus#groupdivgroup) \(DivGroup is Group with divider\_type set to true\) |
| NoteBook\(Table params\) | Creates a [notebook](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Menus#NoteBook) |
| ToolBox\(Table params\) | Creates a [holder](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Menus#Holder) that has align set to "grid" which means items stack from left, perfect for toolbars |
| PopupMenu\(Table params\) | Creates a [popup menu](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Menus#PopupMenu) |

## All items

MenuUI has a few items. Each item can be a menu but menus are always menus. Meaning that items by default are not menus; they don't run any menu events. But, if you add an item to the item it will act like a menu. This is done to have a button inside a button for example. **All items inherit the Item class!**

Read about [Item](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item) before reading about any other item. As all items, including menus, inherit it. Most of the menu functions are documented there too.

* [Item/Button/Divider](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item)
* [Menus](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Menus)
* [Toggle](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Toggle)
* [ComboBox](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-ComboBox)
* [Slider](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Slider)
* [TextBox/NumberBox/ColorTextBox](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-TextBox)
* [KeyBind](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Keybind)
* [Image/ImageButton](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-ImageButton)

