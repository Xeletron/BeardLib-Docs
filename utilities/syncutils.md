# Sync

Updated for version 4.0

## BeardLib.Utils.Sync Class

A class used for helping synching things between BeardLib clients. From weapons to maps!

### Functions

| Function | Return Type | Description |
| :--- | :--- | :--- |
| GetBasedOnFactoryId\(String id, Table wep\) | String | Returns the based on factory of a weapon with factory id `id`. `wep` is an optional parameter to give the weapon tweakdata from which the function will search the based on |
| CleanOutfitString\(String str, Boolean is\_henchman\) | String | Cleans outfit string `str` from custom content. `is_henchman` is for AI outfits |
| DownloadMap\(level\_name, job\_id, udata, done\_callback\) | None | Opens a dialog to download a map, level\_name is a string that should show in the dialog, update\_key is the download id from modworkshop and done\_callback is used in BeardLib to let the game know that the user has installed the map and it's safe to proceed |
| GetJobString\(\) | String | Returns a string of the game settings. The data includes: narrative ID, level ID, difficulty, level name update ID, update provider, and download URL \(last 4 used for downloading heists\) |
| SyncGameSettings\(Number peer\_id\) | None | Synchronizes the game settings with the other peers or the optional peer\_id that was specified in the parameters. This is used for synching custom heists. |
| GetUpdateData\(Table data\) | Table/Boolean | Receives game settings data \(after it's turned from a string to a table in the client\) and returns update data found there. If it doesn't have an update data it will return false. Otherwise, a table with the following values: Update ID, provider name, and download URL. |
| GetCleanedWeaponData\(Unit unit\) | Number, String, Number | Used to spoof a weapon. Returns first a sync index \(-1 if it's a custom weapon, BeardLib knows this way it's a custom weapon\), then blueprint string of the spoofed weapon and finally its selection index. |
| OutfitStringFromList\(Table outfit, boolean is\_henchman\) | String | A wrapper for BlacmarketManager:henchman\_loadout\_string\_from\_loadout and outfit\_string\_from\_list. `is_henchman` means it's for AI. |
| GetCleanedBlueprint\(Table blueprint, string factory\_id\) | Table | Cleans the blueprint of a weapon from custom parts. You must provide a factory ID of the weapon. |
| IsCurrentJobCustom\(\) | Boolean | Returns whether or not the current level is a custom level. |
| Send\(NetworkPeer peer, String id, String data\) | None | Sends a message to a peer. This is used for synching stuff in BeardLib. |
| CompactOutfit\(\) | String | Returns a compact version of the outfit string. Not including some information that BeardLib doesn't need. |
| UnpackCompactOutfit | Table | Unpacks a compact string into a table. |
| GetEquippedWeapon\(Number selection\_index\) | Table | Returns either BlackmarketManager:equipped\_primary\(\) or equipped\_secondary\(\). 2 is primary and 1 is secondary \(game's logic, secondary is first\). |
| BeardLibWeaponString\(Number selection\_index\) | String | Returns a string of data containing the factory ID of the weapon + CRC32 hashed blueprint parts \(since the length of the message we can send is highly limited\). This is used for synching custom weapons. |
| UnpackBeardLibWeaponString\(String weapon\_string\) | Table | Unpacks what BeardLibWeaponString produces. The table contains id \(factory ID\) of the weapon, blueprint \(a table of CRC32 hashes which are later checked against other parts\) and cosmetics of the weapon |

