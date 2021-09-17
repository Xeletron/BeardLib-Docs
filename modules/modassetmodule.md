# AssetUpdates \(Mod Updates\)

Updated for version ~4.0+.

## Module Definition

The module is inherited from [BasicModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/BasicModuleBase). So base parameters can be found there.

The purpose of this module is to provide updating of a mod or a mods assets.

### Module name

The name of the module you use as the meta of the module definition is 'AssetUpdates' or 'ModAssetsModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<AssetUpdates id provider use_local_dir use_local_path folder_name version_file>
    <custom_provider update_func download_file_func version_api_url download_info_url download_api_url/>
    <folder_name>
        <value_node value/>
        ...
    </folder_name>
</AssetUpdates>
```

#### `<AssetUpdates id provider install_directory use_local_dir use_local_path folder_name version version_file important is_standalone>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String/Number | The id of the mod on the server |
| provider | String | The provider of updates for the mod/assets. Currently implemented: `modworkshop`, `Paydaymods` and `Payday2Concepts` |
| install\_directory | String | The directory that contains the folder for the mod |
| use\_local\_path | Boolean | \(Defaults to true\) Determines if the folder of the mod should be used as the folder that is being updated |
| use\_local\_dir | Boolean | \(Defaults to true\) Determines if the location of the mod should be used as the installation directory |
| folder\_name | String/Table | the folder name\(s\) that are being updated |
| version | String/Number | \(Optional\) The current version of the mod. Every time you update the mod, you should increase the version number. For example, from 1.11 to 1.12, just make sure the number is larger than the older one. Generally, you can use any string or number you want for updates. Version check for Modworkshop only checks if the version equals to the curent version and not if it's lower |
| version\_file | String | \(Optional\) The version file which is used to determine the current version of the mod. Defaults to InstallDirectory/FirstFolderName/version.txt. To assign this you can do it as just a path relative to the InstallDirectory |
| important | Boolean | If set to true, every time the mod will receive an update, the game will notify the user with a dialog \(By default, the update will show up in the updates counter in the main menu without notifying the user directly\). Use it only if updating the mod is crucial \(For example, BeardLib updates are important\) |
| is\_standalone | Boolean | \(Defaults to true\) Mostly used for custom maps. Where users can download them by joining a game. However, this shouldn't apply to all maps due to some maps needing assets/code which means the map cannot run without these important assets/code. Setting `is_standalone` to false will disable it. And, users will simply disconnect from the server if they don't have the map |
| dont\_delete | Boolean | \(Defaults to false\)  Doesn't delete the mod folder when updating. This is useful if your mod contains things users might want to change and you don't wish for that content to be deleted each update |

\|dont\_delete\|Boolean\|\|

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<AssetUpdates id="16212" provider="modworkshop" version="1.0"/>
```

Where `id` is the unique identifier on Modworkshop. So this example will update the directory of the mod with the mod with id '16212' and `version` being the current version set in the mod page on Modworkshop. You can set it as any string/number you'd like. Numbers are recommended.

The example is what you'll see in most mods. Some old mods may have `use_local_path` & `use_local_dir` set to true. These parameters are already set to true by default.

### Custom providers

You can either ask the current developers of BeardLib if they can add your site as a provider. Or, use custom providers feature of the module.

To make custom providers you need to have an API in your website. BeardLib will need to communicate with your API to get the version, mod files.

Providers are defined inside the module itself.

Since this is a more complicated topic, we'll start with an XML example:

```markup
    <AssetUpdates id="MyMod" version="1.0">
        <custom_provider version_api_url="mycoolwebsite.com/api/check_version/$id$" download_url="mycoolwebsite.com/api/download/$id$"/>
    </AssetUpdates>
```

#### `<custom_provider check_func download_url/>`

_In the future a module will be added to add a provider instead of repeating it in the module._ **Pay attention to the dollar signs in the URL, these will be replaced.**

_For example, `$id$` in this case, will turn into `MyMod`_

| Parameter | Type | Description |
| :--- | :--- | :--- |
| version\_api\_url | String | The URL that checks the version. If you don't use a custom check\_func function, the function will expect the URL to return the latest version. It will then compare the version to the current version |
| download\_url | String | The URL that will download the file. If you have something more special you'll need to handle it yourself in `download_file_func` |
| version\_is\_number | Boolean | \[Defaults to false\] Determines whether the versions are a number. This will force all versions to be a number so no string versions! |
| check\_func | String or Function \(in classes\) | String path to a function \(self.Func for example\) or a function if defined inside a provider class. The function must deal with the version check all by itself. Use the BLT function `dohttpreq` to do communication with the web. See the providers inside BeardLib to understand more how it works |
| download\_file\_func | String or Function \(in classes\) | Exactly like `check_func` rules but this will donwload the update |
| page\_url | String | The page of the mod for users to get more information. Used in the mods manager |

#### Creating a provider class

At the moment, it's possible to create a class for custom providers. The class acts like "custom\_provider" only the functions have to be actual functions and not a path to the function. And you can use them like normal providers in the modules themselves.

Example of payday2concepts website \(built in BeardLib\):

```lua
ModAssetsModule._providers.payday2concepts = {}
local pd2c = ModAssetsModule._providers.payday2concepts
pd2c.version_api_url = "http://payday2concepts.net/crimenet/checkversion/$id$.txt"
pd2c.download_url = "http://payday2concepts.net/crimenet/downloads/$id$.zip"
pd2c.version_is_number = true
```

You'll have to create these early enough so BeardLib mods can use it.

### Having more than one update module in the mod.

At the moment, BeardLib adds updates into mods manager as single mod updates and does not account for individual updates. This will be changed in the future.

### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| GetMainInstallDir\(\) | String | Returns the path of the primary installation directory for the mod. i.e. The directory that contains that `version` file |

#### Other

| Function | Description |
| :--- | :--- |
| CheckVersion\(\) | Checks the version if the mod/assets are updated |
| RetrieveCurrentVersion\(\) | Sets `self.version` to the current version |
| PrepareForUpdate\(\) | Called by the check function \(or \_CheckVersion\(\)\) to let BeardLib know there's an update. This informs the mods manager & informs the user if `important` is set to true |
| \_CheckVersion\(\) | The default version check function if the provider doesn't have one set |
| DownloadAssets\(\) | Downloads the mod/assets |
| \_DownloadAssets\(\) | The default download function if the provider doesn't have `download_file_func` set |
| ViewMod\(\) | Opens the page of the mod in the provider's site. Don't call this if provider doesn't have `page_url` set |
| StoreDownloadedAssets\(String data, String id\) | The function that recieves the downloaded file and stores it. `data` is the data string of the file, basically all of the bytes and pieces of it. `id` is the ID of the download; the function doesn't use it. |

