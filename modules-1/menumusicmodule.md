# Menu Music

Updated for version 3.38.

## Module Definition

The module is inherited from [ItemModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase#ItemModuleBase). So base parameters can be found there.

This modules creates a menu track.

### Module name

The name of the module you use as the meta of the module definition is 'MenuMusic' or 'MenuMusicModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<MenuMusic id source start_source volume/>
```

#### `<MenuMusic ...>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String | The ID of the track. This has to be unique |
| source | String | The path to the .ogg file that the track should play |
| start\_source | String | Optional path to sound to play before playing `source` |
| volume | Float | The volume of the music \(from 0 to 1\) |

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<MenuMusic id="my_menu_music_name" source="sounds/menu.ogg"/>
```

This will add the track. You will still need to localize the name of the track. In this case menu\_jukebox\_my\_menu\_music\_name and menu\_jukebox\_screen\_my\_menu\_music\_name will need to be localized.

#### Template

Download template here: [https://modworkshop.net/mydownloads.php?action=view\_down&did=21651](https://modworkshop.net/mydownloads.php?action=view_down&did=21651)

### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| MakeBuffer\(String source\) | XAudioBuffer | Called by RegisterHook to create an XAudio buffer |

