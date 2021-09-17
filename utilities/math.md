# Math

Updated for version 3.38

## Math

### math class

This class uses periods not colons. So you'd call it like math.func

#### Functions

| Function | Return Type | Description |
| :--- | :--- | :--- |
| rot\_to\_quat\(Rotation rot\) | Table | Converts a diesel rotation to a diesel quaternion. Returns a table of the 4 values of the quaternion. x,y,z,w |
| quat\_to\_rot\(Number x, Number y, Number z, Number w\) | Rotation | Converts a quaternion to a rotation |

### Color class

#### Functions

| Function | Return Type | Description |
| :--- | :--- | :--- |
| color\(\) | Color | Returns itself \(used when you're not sure if the color is a Vector3 or a color\) |
| vector\(\) | Vector3 | Returns vector3 version of the color |
| from\_hex\(String hex\) | Color | Although Color\(\) does support hex, it doesn't support ARGB. This function makes a color out of RGB or ARGB so you can have a hex color with transparency value. Additionally, the function doesn't mind if the hex string starts with \# |
| to\_hex\(\) | String | Returns the hex value of the color \(in ARGB if the alpha is less than 1\) |
| contrast\(Color white, Color black\) | Color | Returns a color\(white or black but can modified by passing them in the argument\) that fits the color the best, this is used in BeardLib to make an automatic text color that fits the background |

### Vector3 class

#### Functions

| Function | Return Type | Description |
| :--- | :--- | :--- |
| vector\(\) | Vector3 | Returns itself \(used when you're not sure if the color is a Vector3 or a color\) |
| color\(\) | Color | Returns Color\(\) version of the Vector3 |

### mrotation class

This class uses periods not colons. So you'd call it like mrotation.func

#### Functions

| Function | Description |
| :--- | :--- |
| copy\(Rotation rot\) | Same as mvector3.copy, copies the given rotation and returns it |
| set\_yaw\(Rotation rot, Number yaw\) | Sets the yaw value of the rotation |
| set\_pitch\(Rotation rot, Number pitch\) | Sets the pitch value of the rotation |
| set\_roll\(Rotation rot, Number roll\) | Sets the roll value of the rotation |

### Anonymous functions

Functions that aren't contained in a class.

#### Functions

| Function | Description |
| :--- | :--- |
| anim\_dt\(Boolean dont\_pause\) | Returns the current delta time. Works in pause too \(unless `dont_pause` is set to true\) |
| anim\_wait\(Number seconds, Boolean dont\_pause\) | A wait function for animations. `dont_pause` is the same as in `anim_dt` |
| play\_anim\(GUIObject o, Table params\) | Plays an animation. `o` is the GUI object that should get animated. `param` are the parameters of the animation. The parameters should have a table in key `set` that have values to animate. There are more optional parameters that show up in play\_color and play\_value too:  If the table is empty you can just have the set values inside `params` without having to put them in `set` |
| play\_color\(GUIObject o, Color color, Table params\) | Animates a GUI object. `color` is the color you want to animate to, `params` are parameters for the animation same as in `play_anim`. `set` should not be used |
| play\_value\(GUIObject o, String value\_name, Any value, Table params\) | Like `play_anim` but shorter if you want to animate one value. `value_name` is the value you want to animate, `value` is the value that should be animated to. `params` and `o` same before. |
| playing\_anim\(GUIObject o\) | Returns true if the GUIObject is currently playing an animation \(only BeardLib animations\) |
| stop\_anim\(GUIObject o\) | Stops the animation. Recommended to use if you are planning on checking `playing_anim(o)`. |

#### Animation examples

**play\_anim**

```lua
play_anim(bg, {
    set = {alpha = 0},
    callback = function(o)
        if alive(o) then
            o:parent():destroy(o)
        end
    end,
    wait = 0.5,
})

play_anim(bg, {
    alpha = 0
})
```

**play\_color**

```lua
play_color(bg, Color.black)
stop_anim(bg)
play_color(bg, Color.white, {callback = function()
    play_value(bg, "alpha", 0)
end})
```

**play\_value**

```lua
bg:set_alpha(0)
play_value(bg, "alpha", 1)
play_value(bg, "w", 200, {time = 1, callback = function()
    play_value(bg, "w", 0)
end})
```

