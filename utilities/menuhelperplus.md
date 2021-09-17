# Menu Helper Plus

Updated for version 3.38.

MenuHelperPlus is effectively an extension on the 'MenuHelper' found in the base of BLT. So you will find that a lot of variable names will be the same \(intentionally\).

Side note: `merge_data` will be used a lot in this page, effectively it means a table that should be merged using [table.merge](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Main#tablemergebase_table-new_table). So extra variables that you want included can be put into that table and they will be added to the main table.

## Functions

### MenuHelperPlus:NewMenu\(Table params\)

This function will create a new menu, not a node a menu. As in 'start\_menu' or 'pause\_menu' which contains nodes.

* `params` the table of parameters for the new menu

#### `params` parameters

**Required**

* `name` the name of menu
* `id` the ID of the menu
* `fake_path` the string representation of the path that should be used to 'fake' the script\_data function and then insert our own data into that call. \(Shouldn't include an extension\)
* `init_node` a table which includes data for the initial node present in the menu
* `init_node : name` the name of the initial node in the menu

**Optional**

* `callback_handler` string representation of the class which should be used as the callback handler for the menu \(Default is "MenuCallbackHandler"\)
* `input` string representation of the class which should be used as the menu's 'input' \(Default is "MenuInput"\)
* `renderer` string representation of the class which should be used as the menu's 'renderer' \(Default is "MenuRenderer"\)
* `merge_data` table which contains any data that you wish to be merged with the data of the menu \(Could include stuff such as new nodes, however for this `AddNode` should be used\)
* `init_node : align_line` 
* `init_node : back_callback` string representation of the function that should be called upon leaving the node. \(Should be a function in the callback\_handler used by the menu\)
* `init_node : gui_class` string representation of the class which should be used to form the gui of the node \(Defaut is "MenuNodeMainGui"\)
* `init_node : menu_components` string which contains a list of the components which should be shown in the menu \(separated with a space\) 
* `init_node : modifier` string representation of the class\(es\) that should be used as the 'modifier' of the node \(separated using a space\)
* `init_node : refresh` string representation of the class\(es\) that should be used as the 'refresh' object of the node \(separated using a space\)
* `init_node : topic_id` string which is the ID of the topic of the node
* `init_node : legends` table of tables for legends which should be added to the node
* `init_node : legends :: name` name of the legend
* `init_node : legends :: pc` bool that determines if it should be shown when using a keyboard \(Default is false\)
* `init_node : legends :: visible_callback` string representation of a function which would return a bool that determines if the legend is visible

### MenuHelperPlus:NewNode\(String MenuName, Table params\)

This will create a node in the menu with the name `MenuName` and the parameters `params`

* `MenuName` This is the **name** of the menu you wish to create the node in. \(Defaults to "menu\_main" at the menu and "menu\_pause" when in-game\)
* `params` table of variables that are used to create the node

#### `params` parameters

* `name` name of the node \(Required\)
* `align_line`
* `back_callback` string representation of the function to be called when leaving the node
* `gui_class` string representation of the class that should be used to create the gui of the node \(Default = "MenuNodeGui"\)
* `menu_components` string which contains a list of the components which should be shown in the menu \(separated with a space\) 
* `modifier` string representation of the class\(es\) that should be used as the 'modifier' of the node \(separated using a space\)
* `refresh` string representation of the class\(es\) that should be used as the 'refresh' object of the node \(separated using a space\)
* `stencil_align`
* `stencil_image`
* `topic_id` string which is the ID of the topic of the node
* `type` string representation of the class that should be used to create the node \(Default = "CoreMenuNode.MenuNode"\)
* `update` string representation of the class\(es\) that should be used as the 'update' object of the node \(separated using a space\)
* `scene_state` the scene in MenuSceneManager that should be used for the node
* `merge_data` table which contains any data that you wish to be merged with the parameters of the node
* `legends` table containing tables of the legends you wish to be added to the node
* `legends :: name` name of the legend
* `legends :: pc` bool that determines if it should be shown when using a keyboard \(Default is false\)
* `legends :: visible_callback` string representation of a function which would return a bool that determines if the legend is visible
* `callback_overwrite` string representation of the class that should overwrite the menu's default callback handler

### MenuHelperPlus:AddLegend\(String MenuId, String node\_name, Table params\)

This function will add a legend to the node of name `node_name` with the parameters of `params`

* `MenuId` The ID of the menu that the node is present in. \(Defaults to "menu\_main" at the menu and "menu\_pause" when in-game\)
* `node_name` The name of the node the legend should be added to
* `params` The parameters of the legend
* `params :: name` name of the legend
* `params :: pc` bool that determines if it should be shown when using a keyboard \(Default is false\)
* `params :: visible_callback` string representation of a function which would return a bool that determines if the legend is visible

### MenuHelperPlus:GetNode\(String menu\_name, String node\_name\)

This function will return the node in menu `menu_name` with the name `node_name`

* `menu_name` \(Defaults to "menu\_main" at the menu and "menu\_pause" when in-game if the passed parameter is nil\)
* `node_name` Node name \(Required\)

### MenuHelperPlus:AddButton\(Table params\)

This function will add a normal button to a node of your choice with the parameters `params` that you define. returns the created item

* `params` table of parameters \(Required\)
* `params : id` unique name of the button \(Required\)
* `params : title` string title of the button. Can be localization ID \(Required\)
* `params : node` the node that the button should be added to.
* `params : menu` menu that the node is present in \(Not needed if `node` is passed\) \(Defaults to "menu\_main" at the menu and "menu\_pause" when in-game\)
* `params : node_name` name of the node that the button should be created on \(Only required if `node` isn't passed\)
* `params : desc` string description of the button. Can be localization ID.
* `params : callback` string representation of the function that will be called on button press. Should be a function that is present in the node's callback handler.
* `params : disabled_colour` `Color` that should be used when the button is disabled \(Default = Color\(0.25, 1, 1, 1\)\)
* `params : next_node` name of the node that should be opened on button press
* `params : localized` bool to determine if the title of the button should be localized.
* `params : localized_help` bool to determine if the description of the button should be localized.
* `params : merge_data` table of data that should be merged with the table of parameters for the button.
* `params : enabled` bool to set whether the button is enabled or disabled.
* `params : position` index that the button should be inserted at in the node.

### MenuHelperPlus:AddDivider\(Table params\)

Will create a divider in the node of your choice with the parameters `params` that you define. returns the created item.

* `params` table of parameters \(Required\)
* `params : id` unique name of the divider \(Required\)
* `params : node` the node that the divider should be added to.
* `params : menu` menu that the node is present in \(Not needed if `node` is passed\) \(Defaults to "menu\_main" at the menu and "menu\_pause" when in-game\)
* `params : node_name` name of the node that the divider should be created on \(Only required if `node` isn't passed\)
* `params : size` height of the divider.
* `params : no_text` bool to toggle the showing of text.
* `params : merge_data` table of data that should be merged with the table of parameters for the divider.
* `params : position` index that the divider should be inserted at in the node.

### MenuHelperPlus:AddToggle\(Table params\)

Will create a toggle button in the node of your choice with the parameters `params` that you define. returns the created item.

* `params` table of parameters \(Required\)
* `params : id` unique name of the toggle \(Required\)
* `params : node` the node that the toggle should be added to.
* `params : menu` menu that the node is present in \(Not needed if `node` is passed\) \(Defaults to "menu\_main" at the menu and "menu\_pause" when in-game\)
* `params : node_name` name of the node that the toggle should be created on \(Only required if `node` isn't passed\)
* `params : desc` string description of the toggle. Can be localization ID.
* `params : callback` string representation of the function that will be called on toggle press. Should be a function that is present in the node's callback handler.
* `params : disabled_colour` `Color` that should be used when the toggle is disabled \(Default = Color\(0.25, 1, 1, 1\)\)
* `params : localized` bool to determine if the title of the toggle should be localized.
* `params : localized_help` bool to determine if the description of the toggle should be localized.
* `params : icon_by_text` bool which toggles the showing of an icon beside the text \(Defaults to false\)
* `params : value` bool which is the default value of the node. \(ticked or not ticked\) \(Defaults to false\)
* `params : merge_data` table of data that should be merged with the table of parameters for the toggle.
* `params : enabled` bool to set whether the toggle is enabled or disabled.
* `params : position` index that the toggle should be inserted at in the node.

### MenuHelperPlus:AddSlider\(Table params\)

Will create a slider in the node of your choice with the parameters `params` that you define. returns the created item.

* `params` table of parameters \(Required\)
* `params : id` unique name of the slider \(Required\)
* `params : node` the node that the slider should be added to.
* `params : menu` menu that the node is present in \(Not needed if `node` is passed\) \(Defaults to "menu\_main" at the menu and "menu\_pause" when in-game\)
* `params : node_name` name of the node that the slider should be created on \(Only required if `node` isn't passed\)
* `params : desc` string description of the slider. Can be localization ID.
* `params : callback` string representation of the function that will be called on slider press. Should be a function that is present in the node's callback handler.
* `params : disabled_colour` `Color` that should be used when the slider is disabled \(Default = Color\(0.25, 1, 1, 1\)\)
* `params : localized` bool to determine if the title of the slider should be localized.
* `params : localized_help` bool to determine if the description of the slider should be localized.
* `params : min` minimum value the slider can have.
* `params : max` maximum value the slider can have.
* `params : step` value that the slider changes by when the arrow keys are used.
* `params : value` starting value of the slider.
* `params : merge_data` table of data that should be merged with the table of parameters for the slider.
* `params : enabled` bool to set whether the slider is enabled or disabled.
* `params : position` index that the slider should be inserted at in the node.

### MenuHelperPlus:AddMultipleChoice\(Table params\)

Will create a multi-choice item in the node of your choice with the parameters `params` that you define. returns the created item.

* `params` table of parameters \(Required\)
* `params : id` unique name of the multi-choice \(Required\)
* `params : node` the node that the multi-choice should be added to.
* `params : menu` menu that the node is present in \(Not needed if `node` is passed\) \(Defaults to "menu\_main" at the menu and "menu\_pause" when in-game\)
* `params : node_name` name of the node that the multi-choice should be created on \(Only required if `node` isn't passed\)
* `params : desc` string description of the multi-choice. Can be localization ID.
* `params : callback` string representation of the function that will be called on multi-choice press. Should be a function that is present in the node's callback handler.
* `params : localized` bool to determine if the title of the multi-choice should be localized.
* `params : localized_help` bool to determine if the description of the multi-choice should be localized.
* `params : items` table of items that are in the multi-choice
* `params : localized_items` determines if the items are localized
* `params : value` starting value of the multi-choice \(Default = 1\)
* `params : merge_data` table of data that should be merged with the table of parameters for the multi-choice.
* `params : enabled` bool to set whether the multi-choice is enabled or disabled.
* `params : position` index that the multi-choice should be inserted at in the node.

### MenuHelperPlus:AddKeybinding\(Table params\)

Will create a keybinding button in the node of your choice with the parameters `params` that you define. returns the created item.

* `params` table of parameters \(Required\)
* `params : id` unique name of the keybinding \(Required\)
* `params : node` the node that the keybinding should be added to.
* `params : menu` menu that the node is present in \(Not needed if `node` is passed\) \(Defaults to "menu\_main" at the menu and "menu\_pause" when in-game\)
* `params : node_name` name of the node that the keybinding should be created on \(Only required if `node` isn't passed\)
* `params : desc` string description of the keybinding. Can be localization ID.
* `params : callback` string representation of the function that will be called on keybinding press. Should be a function that is present in the node's callback handler.
* `params : disabled_colour` `Color` that should be used when the keybinding is disabled \(Default = Color\(0.25, 1, 1, 1\)\)
* `params : localized` bool to determine if the title of the keybinding should be localized.
* `params : localized_help` bool to determine if the description of the keybinding should be localized.
* `params : connection_name` unique name to save the keybind as.
* `params : binding` default binding on the button \(Default unbound\)
* `params : button` default binding on the button \(Default unbound\)
* `params : merge_data` table of data that should be merged with the table of parameters for the keybinding.
* `params : position` index that the keybinding should be inserted at in the node.

### MenuHelperPlus:GetMenus\(\)

returns the table of menus that have been created through MenuHelperPlus.

### MenuHelperPlus:AddColorButton\(Table params\)

Will create a color button in the node of your choice with the parameters `params` that you define. returns the created item. The item is used to choose colors using a user friendly dialog.

* `params` table of parameters \(Required\)
* `params : id` unique name of the keybinding \(Required\)
* `params : node` the node that the keybinding should be added to.
* `params : menu` menu that the node is present in \(Not needed if `node` is passed\) \(Defaults to "menu\_main" at the menu and "menu\_pause" when in-game\)
* `params : node_name` name of the node that the keybinding should be created on \(Only required if `node` isn't passed\)
* `params : value` the Color value of the item \(Defaults to Color.white\)
* `params : desc` string description of the keybinding. Can be localization ID.
* `params : callback` string representation of the function that will be called on keybinding press. Should be a function that is present in the node's callback handler.
* `params : disabled_colour` `Color` that should be used when the keybinding is disabled \(Default = Color\(0.25, 1, 1, 1\)\)
* `params : localized` bool to determine if the title of the keybinding should be localized.
* `params : localized_help` bool to determine if the description of the keybinding should be localized.
* `params : merge_data` table of data that should be merged with the table of parameters for the keybinding.
* `params : position` index that the keybinding should be inserted at in the node.

