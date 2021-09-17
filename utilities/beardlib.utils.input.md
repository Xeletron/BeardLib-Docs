# Input

Updated for version 3.38

## BeardLib.Utils.Input / BeardLib.Utils.MouseInput

An utility class for dealing with input.

BeardLib.Utils.MouseInput is for dealing with mouse input.

Also useful for bringing a few Input:keyboard\(\)/Input:mouse\(\) functions into a cozy place.

### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| Down\(Idstring/String key\) | Boolean | Returns true if the key that is defined in `key` is pressed down |
| Released\(Idstring/String key\) | Boolean | Returns true if the key that is defined in `key` was released in the last frame |
| Pressed\(Idstring/String key\) | Boolean | Returns true if the key that is defined in `key` was pressed in the last frame |
| Trigger\(Idstring/String key, function clbk\) | Userdata \(trigger\) | Adds a trigger, basically every time the key gets pressed the callback will run, returns a trigger object |
| TriggerRelease\(Idstring/String key, function clbk\) | Userdata \(trigger\) | Adds a release trigger, same as trigger just for releasing the key and returns a trigger object also |
| Triggered\(Table trigger, Boolean check\_mouse\_too\) | Boolean | Checks trigger table \(not be confused with the trigger userdata object\) if it's pressed. The trigger is a product from the function `TriggerDataFromString`. Mostly cotains the values: `key` for the key, `additional_key` for another key that is required for the trigger and `clbk` for a callback when the trigger is pressed \(Something you need to call by yourself\) |
| TriggerDataFromString\(String str, Function clbk\) | Table | Converts a string to a table of trigger data. The table contains `key`, `additional_key` and `clbk` \(from the parameter `clbk` which is from the function's parameters\). `str` is supposed to be either a simple key or "key+additional\_key" for keybinds like "ctrl+s" etc |

#### Other

| Function | Description |
| :--- | :--- |
| RemoveTrigger\(Userdata trigger\) | Removes a trigger by passing a trigger object |

