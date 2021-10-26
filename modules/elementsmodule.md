---
description: A module
---

# ElementsModule

A module used to inject custom mission elements into the game.

### XML Definition

```markup
<Elements directory>
    <element name file/>
</Elements>
```

#### `<Elements directory>`

| Parameter | Type   | Description                                  |
| --------- | ------ | -------------------------------------------- |
| directory | String | Sets the directory to load the elements from |

#### `<element name file/>`

| Parameter | Type   | Description                                                                                                                          |
| --------- | ------ | ------------------------------------------------------------------------------------------------------------------------------------ |
| name      | String | The name of the element, without the "Element" part. If the file parameter isn't define, the assumed file will be \<name>Element.lua |
| file      | String | Let's you choose a specific name for the file of the element's code.                                                                 |

### Simple Usage



```markup
<Elements directory="elements">
    <element name="Food"/>
</Elements>
```

```lua
core:import("CoreMissionScriptElement")
FoodElement = FoodElement or class(CoreMissionScriptElement.MissionScriptElement)

function FoodElement:on_executed(instigator)
	log("Nom nom nom", tostring(self._values.food))
end
```

### Editor Integration

The editor integrates into this module using a hook, the editor will attempt to load an editor class named \<name>ElementEditor.lua, place it in the same directory you'd place your regular element class.

### Notes

1. This guide doesn't cover how to make your own elements (the classes themselves) in depth, this is just a convenient way of injecting them into BeardLib (and the editor) without having to go through the hassle of making hooks and injecting them into BeardLib or the editor.
2. The naming convention differs from the game, instead of ElementFood we force the name to be FoodElement. The reason is to avoid clashing with future or existing element names. This happened before to BeardLib itself. So to avoid this situation this element will work best with this naming convention. This includes the editor's integration.
