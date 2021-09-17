# Sounds

Updated for version 3.38.

## Module Definition

The module is inherited from [ModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase). So base parameters can be found there.

This module requires SuperBLT to be installed or else the sounds will not load [http://superblt.znix.xyz/](http://superblt.znix.xyz/)

### Module name

The name of the module you use as the meta of the module definition is 'Sounds' or 'SoundsModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<Sounds directory prefix load_on_play unload auto_pause relative dont_store_float ...>
    <prefixes>
        <value_node value="prefix"/>
    </prefixes>
    <sound id stop_id prefix load_on_play unload auto_pause relative dont_store_float full_path ...>
    <sounds directory ...>
    </sounds>
</Sounds>
```

#### Only `sound` node

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String | The id of the sound, can be found in tweak datas and in here [https://docs.google.com/spreadsheets/d/1m0LBg2PKpB-bnWfOFj40AglCI1dLmAHLH3ydi3Y7uz8/edit?pli=1\#gid=821157629](https://docs.google.com/spreadsheets/d/1m0LBg2PKpB-bnWfOFj40AglCI1dLmAHLH3ydi3Y7uz8/edit?pli=1#gid=821157629) don't forget the prefix if there is. |
| path | String | The path to the sound file \(Has to be OGG format\). The final directory will be _Mod Path + `directory` + `path`_ Mod Path is your mod path, `directory` is the directory value of `Sounds` node that holds the sound and `path` is the path to the sound file itself, usually used as a file name. If not defined the path will be `id` + .ogg |
| full\_path | String | The full path\(from Payday 2's root directory\) to the sound.  Unless you need to be highly specific, don't use this value. |

#### Only `Sounds` node

| Parameter | Type | Description |
| :--- | :--- | :--- |
| directory | String | Directory of the sounds \(Full explanation in the `path` value\) |

#### Both `Sound` and `Sounds` node

_those values are mostly optional_ _if defined from the sounds node, all sounds inside it will inherit the value_

| Parameter | Type | Description |
| :--- | :--- | :--- |
| prefix | String | The prefix of the sound. Some sounds in Payday 2 are separated by a "prefix" this lets you have multiple voices for heisters and many more things. |
| prefixes | Table | Like `prefix` but allows to define a few prefixes. Normally, the sound will play if one of the prefixes match |
| stop\_id | String | An id that should stop the sound like g18c\_stop. if not defined, the stop id will be the id + "\_stop" |
| load\_on\_play | Boolean | By default the module will load the sounds as soon as the module itself loads\(or if inside level module, when the level itself loads\) you can change that so the sound is loaded only when it's played first, don't use that for heavy in file size sounds. |
| unload | Boolean | By default when the game loads to main menu or into a game it will unload all previously loaded sounds, you can set this to false to disable it. |
| auto\_pause | Boolean | Normally custom sounds auto pause automatically if they're 3D sounds\(being played from a 3D position or linked to a unit\) you can disable that if you set this value to false, you can also set this to true if you want 2D sounds to pause. |
| relative | Boolean | Sets whether the sound is 2D\(true\) or 3D\(false\), this is mostly automatic and shouldn't be changed. |
| dont\_store\_float | Boolean | To solve the issue of networked sound ids, Beardlib stores the networked sound ids of custom sounds, you can set this to true to not store it\(if you're 100% sure that your sound isn't going to be synced\). |
| volume | Float | The volume of the sounds. Ranges from 0 to 1 |
| wait | Number | Wait x seconds before playing the sound? |
| prefixes\_strict | Boolean | Normally the sound will play if at least **one** of the prefixes matches the sound. This makes the sound play only when **all** prefixes match |
| loop | Boolean | Should the sound loop? |

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<Sounds direcotry="sounds">
    <sounds directory="m4" prefix="regular">
        <sound id="m4_fire_single" path="fire.ogg"/>
        <sound id="m4_tighten" path="enter_sight.ogg"/>
        <sound id="m4_fire_single" path="fire.ogg" prefix="suppressed_a"/>
    </sounds>
</Sounds>
```

This replaces the m4 sounds. Due to how SuperBLT loops the sounds, you should either define use\_fix in the sounds section of your custom weapon or use the autofire sound fix mod: [https://modworkshop.net/mydownloads.php?action=view\_down&did=20403](https://modworkshop.net/mydownloads.php?action=view_down&did=20403)

### Extra nodes

#### `<scan>` node

_Scans a directory to quickly add sounds. Useful when you have a lot of sound ids. The parameters are pretty much the same as `<Sounds>`._

Example:

```markup
<Sounds prefix="prefixx">
    <scan prefix="some_prefix" directory="sounds"/>
</Sounds>
```

_These nodes below use mostly the `id` and `prefix` parameter. But, some can use more parameters such as `stop_id`. These nodes cannot load files so don't define paths or directories._

#### `<queue>` node

_A queue of sound ids._ Example:

```markup
<Sounds directory="sounds">
    <sound id="one"/>
    <sound id="two"/>
    <queue id="one_and_two">
        <sound id="one"/>
        <sound id="two"/>
    </queue>
</Sounds>
```

#### `<random>` node

_Like `<queue>` but randomizes which sound to play every time. The sounds inside of it are just ids._ Example:

```markup
<Sounds directory="sounds">
    <sound id="one"/>
    <sound id="two"/>
    <random id="one_or_two">
        <sound id="one"/>
        <sound id="two"/>
    </random>
</Sounds>
```

#### `<stop>` node

_Makes a stop ID. This can be used to stop a few sounds. The sounds inside of it are just ids._ Example:

```markup
<Sounds directory="sounds">
    <sound id="one"/>
    <sound id="two"/>
    <stop id="stop_my_stuff">
        <sound id="one"/>
        <sound id="two"/>
    </stop>
</Sounds>
```

#### `<redirect>` node

_Redirects a sound id to a different sound id. You can even redirect it to a randomized or queued sound._ Example:

```markup
<Sounds directory="sounds">
    <sound id="one"/>
    <redirect id="whistling_attention" to="one"/>
</Sounds>
```

### Functions

| Function | Description |
| :--- | :--- |
| ReadSounds\(Table data, String prev\_dir\) | Called by the init function to load the sounds into the CustomSoundManager and called by itself if it finds any `sounds` nodes inside. `data` is the current sound data \(the place that contains the sounds and `sounds` nodes\) `prev_dir` is the path that the sounds should join to. \(If it's null it will be mod path\) |

