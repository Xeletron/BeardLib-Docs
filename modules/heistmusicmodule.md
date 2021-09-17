# Heist Music

Updated for version 4.4.

## Module Definition

The module is inherited from [ItemModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase#ItemModuleBase). So base parameters can be found there.

This modules creates a heist track.

### Module name

The name of the module you use as the meta of the module definition is 'HeistMusic' or 'HeistMusicModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<HeistMusic id directory>
    <event name source/>
</HeistMusic>
```

#### `<HeistMusic ...>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String | The ID of the track. This has to be unique |
| volume | Float | The volume of the music \(from 0 to 1\) |

#### `<event name source>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| name | String | The name of the event. At the moment it can only be `setup` for stealth, `anticipation` for build up, `assault` and `control` |
| source | String | The path to the .ogg file that the track should play in the event |
| start\_source | String | Optional path to sound to play before playing `source` |
| volume | Float | Volume of this specific music event |
| allow\_switch | Bool | Wether a random track is selected each loop or only once per event if multiple tracks are available \(See `<track>` node\) |
| weight | Integer | Base weight of any tracks added via `<track>` nodes \(See `<track>` node\) |
| alt\_source \(deprecated\) | String | Use `<track>` nodes instead |
| alt\_chance \(deprecated\) | Float | Use `<track>` nodes instead |
| alt\_start\_source \(deprecated\) | String | Use `<track>` nodes instead |

**&lt;track source&gt;**

`<track>` nodes can be placed as children of `<event>` nodes to specify multiple tracks for a single event.  
They inherit any values set on the `<event>` node if not specified in the `<track>` node itself.

| Parameter | Type | Description |
| :--- | :--- | :--- |
| source | String | The path to the .ogg file that the track should play in the event |
| start\_source | String | Optional path to sound to play before playing `source` |
| volume | Float | Volume of this specific music track |
| weight | Integer | Weight of this track for being chosen randomly |

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<HeistMusic id="my_heist_music_name" directory="sounds">
    <event name="setup" source="stealth.ogg"/>
    <event name="anticipation" source="buildup.ogg"/>
    <event name="assault" source="assault.ogg"/>
    <event name="control" source="control.ogg"/>
</HeistMusic>
```

This will add the track. You will still need to localize the name of the track. In this case menu\_jukebox\_my\_heist\_music\_name and menu\_jukebox\_screen\_my\_heist\_music\_name will need to be localized.

Having multiple tracks for a single event will allow you to create a random track selection, similar to how "Ode to Greed" or "Break the Rules" have a chance to play a lyric version of their assault tracks.  
For this you would simply set up an event like this

```markup
<event name="assault">
    <track source="assault.ogg" weight="10">
    <track source="assault_lyrics.ogg" weight="1">
</event>
```

The weight defines how likely a track is going to be selected whenever this event plays. In the example above this would mean the regular assault track is 10 times more likely to play than the lyric version.

#### Template

Download template here: [https://modworkshop.net/mydownloads.php?action=view\_down&did=21651](https://modworkshop.net/mydownloads.php?action=view_down&did=21651)

### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| MakeBuffer\(String source\) | XAudioBuffer | Called by RegisterHook to create an XAudio buffer |

