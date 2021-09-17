# Tweak Data Helper

Updated for version 3.38

## TweakDataHelper

An utilities class that allows you to modify tweakdata even before its initialized.

**Note**: `Apply` and `ApplyOverwrites` are missing parameters because there isn't a need for them anymore.

### Functions

| Function | Description |
| :--- | :--- |
| ModifyTweak\(Table data, ...\) | Adds `data` for add merging into tweak\_data. `...` contains keys of where you want merge to. For example `TweakDataHelper:ModifyTweak({test = true}, "weapon", "factory")` this will add merge with tweak\_data.weapon.factory. Remember that this is an add\_merge not merge which means that it will merge keys and all but indexed values will insert into the table so the end result may not necessarily have the same index |
| OverwriteTweak\(Table data, ...\) | Similar to `ModifyTweak` but instead of add merging this just overrides the data so if we did the example `TweakDataHelper:ModifyTweak({test = true}, "weapon", "factory")` that would overwrite tweak\_data.weapon.factory entirely! The function automatically calls `self:ApplyOverwrites(tweak_data)` if tweak\_data exists |
| Apply\(\) | The function that applies the changes to tweak\_data. Calls `self:ApplyOverwrites` too. Not called again after tweak\_data is present \(`self:ModifyTweak` automatically add merges with it after that\) |
| ApplyOverwrites\(\) | Applies the overwrites to the tweak\_data. Called either by `self:Apply` or by `self:OverwriteTweak` |

