# ImageButton

Updated for version 3.36.

**It's recommended to first read about the base item before reading about other items** [https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/MenuUI-Item)

## ImageButton/Image

### Creation

```lua
    MyRandomMenu:ImageButton({
        name = "MyImageButton",
        texture = "path/to/my/texture",
        on_callback = function(item)
            log("I was pressed!")
        end
    })
```

Or if you need a divider type image:

```lua
    MyRandomMenu:Image({
        name = "MyImageButton",
        texture = "path/to/my/texture"
    })
```

### Parameters

| Parameter | Type | Description |
| :--- | :--- | :--- |


texture\|String/Idstring\|Texture of the image\| texture\_rect\|Table\|Texture rectangle of the image, if used. Pivot points have to be left and top of what you need\| icon\_w\|Number\|Specific width for the image\(unlike 'w' which gets subtracted with the x image offset\)\| icon\_h\|Number\|Specific height for the image\(unlike 'h' which gets subtracted with the y image offset\)\| img\_offset\|Table/Number\|Offset for the image, useful if you want to have the image smaller while button itself bigger, defaults to {0,0}\| img\_offset\_x\|Number\|Specific x offset for the image\| img\_offset\_y\|Number\|Specific y offset for the image\| highlight\_image\|Boolean\|Should the image change color when highlighting\(uses `forground` color\)\| img\_color\|Color\|Color of the image, defaults to `foreground` color\|

### Functions

| Function | Description |
| :--- | :--- |


SetImage\(String/Idstring texture, Table texture\_rect\)\|Sets a texture and texture rectangle for the item\|

