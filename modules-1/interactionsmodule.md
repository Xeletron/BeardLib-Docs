# Interactions

Updated for version 3.38.

## Module Definition

The module is inherited from [ItemModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase#ItemModuleBase). So base parameters can be found there.

This modules allows you to add custom interactions to be used by custom maps for example.

### Module name

The name of the module you use as the meta of the module definition is 'HeistMusic' or 'HeistMusicModule' if `_force_search` is set to true in the module definition.

If you're writing them in level modules the name of the module is 'interactions'.

### XML Structure

```markup
<Interactions>
    <interaction id interact_distance/>
</Interactions>
```

#### `<interaction ...>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String | The ID of the interaction. This has to be unique |
| interact\_distance | Number | The distance \(in centimeters?\) the interaction can be interacted from. For example for buttons you'd use something like 100 |

**Additional parameters**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| based\_on | String | Base your interaction on already existing ineraction data |
| text\_id | String | Optional text localization id defaults to hud\_+`id` |
| special\_equipment | String | Optional ID of some pickup/special equipment that you need to have in order to interact |
| equipment\_consume | Boolean | Should the equipment be "consumed" after interaction? Like imagine some key that can only be used once |
| equipment\_text\_id | String | Optional text localization id of the equipment that is needed. This will need to be localized if it isn't already |
| sound\_start | String | Optional sound ID of the sound that should play when starting interaction |
| sound\_interupt | String | Optional sound ID of the sound that should play when the interaction is interrupted |
| sound\_done | String | Optional sound ID of the sound that should play when the interaction is done |
| required\_deployable | String | Like `special_equipment` but requires a deployable instead |
| deployable\_consume | Boolean | Like `equipment_consume` but for deployables |
| requires\_upgrade | Table | Table that looks like this . Checks for required perks/skills |
| force\_update\_position | Boolean | Determines if the interaction should constantly check for position to update. Useful if the interaction moves around |

And any other interaction tweakdata value. There are more that are not listed here yet.

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<Interactions>
    <interaction id="my_interaction"/>
</Interactions>
```

This will add the interaction `my_interaction`. You will still need to localize the name of the track. In this case `hud_my_interaction` will need to be localized \([LocalizationModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/LocalizationModule)\).

### Functions

| Function | Description |
| :--- | :--- |
| AddInteractionsDataToTweak\(Table i\_self\) | Inserts the interaction data to the tweak\_data. Called by the PostHook inside RegisterHook or by RegisterHook itself if interaction tweakdata is available |

