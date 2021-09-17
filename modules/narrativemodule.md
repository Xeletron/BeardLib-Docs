# Narrative

## Module Definition

The module is inherited from [ModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase). So base parameters can be found there.

### Module name

The name of the module you use as the meta of the module definition is 'narrative' or 'NarrativeModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<narrative id name_id brief_id contact jc briefing_event debrief_event>
    <chain>
        <table level_id type_id type ...>
            ...
        </table>
    </chain>
    <crimenet_callouts>
        <value_node value/>
    </crimenet_callouts>
    <crimenet_videos>
        <value_node value/>
    </crimenet_videos>
    <payout>
        <value_node value/>
    </payout>
    <contract_cost>
        <value_node value/>
    </contract_cost>
    <experience_mul>
        <value_node value/>
    </experience_mul>
    <min_mission_xp>
        <value_node value/>
    </min_mission_xp>
    <max_mission_xp>
        <value_node value/>
    </max_mission_xp>
    <merge_data ...>
        ...
    </merge_data>
</narrative>
```

#### `<narrative id name_id brief_id contact jc briefing_event debrief_event>`

* `id` The narrative tweak key, which must be unique. \[REQUIRED\]
* `name_id` The localization id of the name of the narrative. Defaults to heist\_ID\_name
* `brief_id` The localization id of the briefing of the narrative. Defaults to heist\_ID\_brief

#### `<merge_data ...> ...`

* `...` Any additional data you wish to be included in the narrative tweak definition table.

### Example

See [MapFramework](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/MapFramework)

## Functions

### NarrativeModule:RegisterHooks\(\)

This is used to register the hooks that are used for inserting the tweak definitions. Usually this will be called by the MapFramework if this is running under that, otherwise you need to call it yourself.

