# Special Hook IDs

Updated for version 4.0.

## Hooks IDs

Essentially these are hooks added by Beardlib using [Hooks:Register](https://payday-2-blt-docs.readthedocs.io/en/latest/lua/hooks/#hooksregisterhook-hook_id) which can be used with [Hooks:Add](https://payday-2-blt-docs.readthedocs.io/en/latest/lua/hooks/#hooksaddhook-hook_id-id-func).

| Hook ID | Description |  |
| :--- | :--- | :--- |
| BeardLibCreateCustomMenus | Called from the hook `MenuManagerInitialize`. This hook should be used to create all your menus \(MenuHelperPlus\). Receives the self of MenuManager |  |
| BeardLibMenuHelperPlusInitMenus | Called from the hook `MenuManagerInitialize` after `BeardLibCreateCustomMenus`. Used by MenuHelperPlus to register menus. Receives the self of MenuManager |  |
| BeardLibCreateCustomNodesAndButtons | Called from the hook `MenuManagerInitialize` after `BeardLibMenuHelperPlusInitMenus` This hook should be used to create your nodes and buttons. Receives the self of MenuManager |  |
| BeardLibAddCustomWeaponModsToWeapons | Called after the initialization of BlackMarketTweakData. Used by custom weapon mods to inherit stuff from based\_on and place stuff in tables. Gets tweak\_data.weapon.factory and tweak\_data as parameters |  |
| BeardLibCreateCustomWeapons | Called after the initialization of WeaponFactoryTweakData. Used by WeaponModule to insert custom weapons into the factory tweakdata. Gets tweak\_data.weapon.factory as the parameter |  |
| BeardLibCreateCustomWeaponMods | Called after `BeardLibCreateCustomWeapons` and is used to insert custom weapon parts into the factory.parts tweakdata | Gets tweak\_data.weapon.factory as the parameter |
| BeardLibPreProcessScriptData | Called before scriptdata get processed in `FileManager:Process`. Receives the parameters: `ids_ext` which is Idstring of the extension, `ids_path` Idstring of the part and `data` which is the data of the scripdata |  |
| BeardLibProcessScriptData | Called after scriptdata get processed in FileManager:Process. Receives the same parameters as \`BeardLibPreProcessScriptData | only that `data` gets changed by the process |
| BeardLibSetupUnloadPackages | Called after Setup:unload\_packages gets called |  |
| BeardLibRequireHook | Gets called before and after `require`. The first parameter is if the call is post hook and the rest is what parameters were in `require` |  |
| BeardLibSetupInitFinalize | Gets called after `Setup:init_finalize` receives one parameter which is the self of Setup |  |
| GameSetupPauseUpdate | Called after a paused update in GameSetup receives `t` for time and `dt` for delta time |  |
| SetupInitManagers | Called after `Setup:init_managers` gets one parameter which is the self of Setup |  |
| BeardLibCreateCustomProjectiles | Called after `BeardLibAddCustomWeaponModsToWeapons`. Was supposed to be used by the projectile module \(An unstable module!\) |  |
| BeardLibPostCreateCustomProjectiles | Called after the initialization of WeaponTweakData. Was supposed to be used by the projectile module \(An unstable module!\) |  |
| BeardLibPreInit | Called right before BeardLib gets initialized |  |
| BeardLibPostInit | Called right after BeardLib gets initialized |  |

