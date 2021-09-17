# Menus

Updated for version 3.36.

All values and functions are inherited from here: [https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item)

## Holder

The most simple type of menu. Only holds items. If you don't need a scroll-able panel you should use this menu type instead of `Menu`.

### Creation

```lua
MyRandomMenu:Holder({
    name = "Holdon"
})
```

### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| auto\_height | Boolean | Should the menu automatically set the height based on items it has? Defaults to true |

## Menu

A Menu is a menu type with a scroll-able panel for the items.

### Creation

```lua
MyRandomMenu:Menu({
    name = "Menu"
})
```

### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| scrollbar | Boolean | Should there by a scrollbar for the menu? You should set this to false if you are sure the menu will never have too many items to require a scrollbar. Defaults to true if the menu has `auto_height` set to false or `min_height` not set to null or `max_height` not set to null \(Recommended to use Holder instead in that case\) |
| scroll\_width | Number | Set a custom size for the scrollbar. Defaults to 8 |
| auto\_height | Boolean | Should the menu automatically set the height based on items it has? Defaults to true if menu is a group |

### Functions

### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| ScrollY\(\) | Number | Returns the current scroll Y position. Useful if you want to retain the position of the scroll |

### Set

| Function | Description |
| :--- | :--- |
| SetScrollSpeed\(Number speed\) | Sets the scrolling speed |
| SetSize\(Number w, Number h\) | Sets the size for the menu. `w` is the width and `h` is the height `w` and `h` can be null and will default to the current size if not defined |
| SetScrollY\(Number y\) | Sets the Y position of the scroll |

## Group/DivGroup

_Inherits `Menu`_

Features a title and a scroll-able panel for items. Additionally allows you to close and open the menu.

### Creation

```lua
MyRandomMenu:Group({
    name = "2ndMenu",
    text = "A group!"
})
```

or if a DivGroup:

```lua
MyRandomMenu:DivGroup({
    name = "3rdMenu",
    text = "Div group!"
})
```

### DivGroup

The difference between Group and DivGroup is that div group sets `divider_type` to true which makes the item like a divider but it has items, this also disables toggling for the group.

### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| closed | Boolean | is the group closed? |

### Functions

| Function | Description |
| :--- | :--- |
| ToggleGroup\(\) | Toggles the group, if it's closed then it will open it and if not it will close it |
| CloseGroup\(\) | Closes the group |
| OpenGroup\(\) | Opens the group |

## PopupMenu

A menu that is like a simple button. But, opens up a popup menu when pressed. Kind of like those context menus in every Windows app.

### Creation

```lua
MyRandomMenu:PopupMenu({
    name = "ooo",
    text = "File"
})
```

### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| keep\_menu\_open | Boolean | Decides whether the popup menu should stay open after pressing outside of it. Defaults to false |

### Functions

| Function | Description |
| :--- | :--- |
| Open\(\) | Opens the menu |
| Close\(\) | Closes the menu |

## NoteBook

_Inherits `Menu`_ A menu that is like a notebook; it has pages. You can control the page using the arrow keys at the top right corner of the menu.

### Creation

```lua
local nb = MyRandomMenu:NoteBook({
    name = "NoteBook",
    text = "My book..."
})
local item = nb:Button({
    text = "Dummy button"
})
--Create a page and inserts the item into it.
nb:AddItemPage(item)
```

This is a little weird type of item, it has items; but only renders them based on pages. So be careful with it.

### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |
| page | Number | The current page. Defaults to 1 |

### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| GetCurrentPage\(\) | Number | Returns the current page |
| GetPageCount\(\) | Number | Returns the page count |
| GetItemPage\(Item item\) | Table | Returns the page of an item; if it's inside any |

#### Set

| Function | Description |
| :--- | :--- |
| SetPage\(Number page\) | Sets the current page |

#### Other

| Function | Description |
| :--- | :--- |
| AddToPage\(Item item, Number page\) | Adds an item to a page |
| RemoveFromPage\(Item item, Number page\) | Removes an item from a page |
| AddPage\(String name, Number indx\) | Adds a page. `name` is the name of the page. It will also be displayed near the arrow page controls. `indx` is used to insert it to a specific index. By default it inserts it to the last position |
| AddItemPage\(String name, Item item, Number indx\) | Adds a page by the name of `name` and adds `item` to it. `indx` is same as in `AddPage` |
| SetPageName\(Number indx, String name\) | Sets a page name/title. `indx` is the page number and `name` is the title |
| RemovePage\(Number indx\) | Removes a page that has the index `indx` |
| RemoveAllPages\(\) | Removes all pages |
| RemovePageWithItem\(Item item\) | Removes a page that has a certain item |

