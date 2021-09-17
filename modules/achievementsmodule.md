# Achievements

Updated for version 3.38.

## Module Definition

The module is inherited from [ItemModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ModuleBase#ItemModuleBase). So base parameters can be found there.

This module will allow you to add your own achievements within your mods. They will appear in the Custom Achievements menu which can be accessed next to the button to check on BeardLib mods.

### Module Name

The name of the module you use as the meta of the module definition is 'Achievements' or 'AchievementsModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<Achievements id name desc icon banner>
    <achievement id name_id desc_id objective_id icon rank amount reward_type reward_amount hidden_achievement />
</Achievements>
```

#### `<Achievements id name desc icon banner>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String | The ID of your achievement package, which will hold all your achievements. |
| name | String | A localized string ID for the package's name. Default : `<package_id>_name` |
| desc | String | A localized string ID for the package's description. Default : `<package_id>_desc` |
| icon | String | The path to a custom icon for your achievement package. It has to be added through the AddFiles module beforehand. Default: `"guis/textures/achievement_package_default"`. |
| banner | String | The path to a custom banner for your achievement package. It has to be added through the AddFiles module beforehand. Ideal scale: 820x90 |

The `name`, `desc`, `icon` and `banner` options are optional.

#### `<achievement id name_id desc_id objective_id icon rank amount reward_type reward_amount hidden_achievement />`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String | The ID of your achievement, which is used to manipulate that particular achievement later. |
| name\_id | String | A localized string ID for the achievement's name. Default : `<achievement_id>_name` |
| desc\_id | String | A localized string ID for the achievement's description. Default : `<achievement_id>_desc` |
| objective\_id | String | A localized string ID for the achievement's objective. Default : `<achievement_id>_objective` |
| icon | String | The path to a custom icon for your achievement. It has to be added through the AddFiles module beforehand. Default: `"guis/textures/achievement_trophy_white"`. Required scale: 128x128 |
| rank | Integer | Integer from 1 to 4. Defines the achievement rank based on Custom Achievement API: 1 = Bronze, 2 = Silver, 3 = Gold, 4 = Platinum |
| amount | Integer | Useful for counting things, and saving the progress each time it increases. Once amount is reached, the achievement is automatically unlocked. |
| reward\_type | String | Can be `xp`, `cc`, `cash`, `offshore`. Defines what type of reward the player will get when the achievement is unlocked. |
| reward\_amount | Integer | Has to be an integer that defines how much of `xp`, `cc`, `cash`, or `offshore` the player is going to receive. |
| hidden\_achievement | Boolean | Hides the details of the achievement such as the description, objective, icon and rank. Once unlocked, the details will appear. |

### Example

```markup
<Achievements id="test_package" icon="guis/tamamo">
        <achievement id="something" rank="2" name_id="third_ach_test_name" icon="guis/tamamo"/>
        <achievement id="another_blablabla" rank="3"/>
        <achievement id="fourth_new_achievement" rank="4"/>
</Achievements>
```

### CustomAchievementManager - Functions

| Function | Description |
| :--- | :--- |
| HasPackage\( String package\_id \) | Returns `true` or `false`, if the `package_id` specified exists. |
| HasAchievement\( String package\_id, String achievement\_id \) | Returns `true` or `false`, if the `achievement_id` within `package_id` exists. |
| NumberOfPackages\(\) | Returns a integer on the number of packages the user currently has. |
| NumberOfAchievements\(\) | Returns a integer on the number of all the achievements the player has, unlocked or not. |
| CompletedAchievementsTotal\(\) | Returns a integer on the number of all the achievements the player has unlocked only. |

### CustomAchievementPackage - Functions

| Function | Description |
| :--- | :--- |
| init\( String package\_id \) | Initialize a new achievement package with the given `package_id`. The initialization is necessary before using any other function of this class. |
| GetName\(\) | Get the name of the package. The returned value is already passed through `managers.localization:text()`. |
| GetDesc\(\) | Get the description of the package. The returned value is already passed through `managers.localization:text()`. If no description was defined, this will return an empty string. |
| GetIcon\(\) | Get the current package icon path. |
| GetBanner\(\) | Get the current package banner path. |
| ManualAchievementAddition\( String achievement\_id, Table config \) | Allows to add an achievement to the package manually. This is useful for multiple mods adding achievements to a unique package. |
| HasAchievement\( String achievement\_id \) | Returns `true` or `false`, depending on if `achievement_id` exists in the current package. |
| Achievement \(String achievement\_id \) | Initialize the class CustomAchievement with the provided achievement ID. |
| GetTotalAchievements\(\) | Returns an integer of the current total of all the achievements within the package. |
| GetCompletedAchievements\(\) | Returns an integer of the unlocked achievements within the package. |
| AllAchievementsCompletedExceptOne\(\) | Returns `true` or `false`, depending on if all achievements excepted one are unlocked. This is useful for achievements, such as "complete all achievements to unlock this one". |

### CustomAchievement - Functions

| Function | Description |
| :--- | :--- |
| init\( Table config, String package \) | Initialize the class in order to use all other functions. It's better to first initialize the package in order to bypass the manual initialization, through `CustomAchievementPackage:Achievement(achievement_id)`. |
| GetName\(\) | Get the name of the achievement. The returned value is already passed through `managers.localization:text()`. |
| GetDesc\(\) | Get the description of the achievement. The returned value is already passed through `managers.localization:text()`. |
| GetObjective\(\) | Get the objective of the achievement. The returned value is already passed through `managers.localization:text()`. |
| GetIcon\(\) | Get the current achievement icon path. |
| GetUnlockTimestamp\(\) | Get the UNIX timestamp of the unlocked achievement. If the achievement isn't unlocked, this will return `0`. |
| Package\(\) | Initialize CustomAchievementPackage of this achievement. |
| IncreaseAmount\( Integer amount, Boolean to\_max \) | Calling this function will increase the `amount` saved value of the achievement by `amount`. If `to_max` is true, it will automatically set the amount to the maximum, in order to unlock the achievement right away. |
| Unlock\(\) | Unlocks the achievement. |
| Lock\(\) | Lock the achievement. |
| IsUnlocked\(\) | Returns `true` or `false` depending on if the achievement is unlocked or not. |
| IsHidden\(\) | Returns `true` or `false` depending on if the achievement is hidden or not. |
| HasReward\(\) | Returns `true` or `false` depending on if the achievement has a reward or not. |

