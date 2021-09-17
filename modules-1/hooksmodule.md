# Hooks

Updated for version 3.38.

## Module Definition

The module inherits [BasicModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/BasicModuleBase). All parameters and functions of this class are inherited by the module.

### Module name

The name of the module you use as the meta of the module definition is 'Hooks' or 'HooksModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<Hooks directory type>
    <hook type file source_file use_clbk/>
    <hooks directory>
    </hooks>
</Hooks>
```

**&lt;Hooks directory type&gt;**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| directory | String | Directory/path relative to the mods directory which contains all the hooked. \[OPTIONAL\] |

**&lt;hook type file source\_file use\_clbk/&gt;**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| source\_file | String | The path of the lua source file you wish to hook to. \[REQ\] |
| file | String | File path of the file that is hooking to the `source_file` \[REQ\] |

**Both**

| Parameter | Type | Description |
| :--- | :--- | :--- |
| type | String | The type of hook. If this is set to `pre` then the hook will be called before the source\_file is loaded. Otherwise, it will be called after \(Mostly for pre hooks\) |
| pre | Boolean | Like `type` but as a quick boolean value to set to pre hooks |
| post | Boolean | Like `type` but as a quick boolean value to set to post hooks \(Very specific cases as post is default\) |

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<Hooks directory="Hooks">
    <hook file="Setup.lua" source_file="lib/setups/setup"/>
    <hook file="Setup2.lua" source_file="lib/setups/setup" use_clbk="self.setup_hook_enabled"/>
</Hooks>
```

And if you are using the use\_clbk, have something like this:

```lua
function MyMod:setup_hook_enabled()
    return true
end
```

For this example your hook will be here: `mods/MyMod/Hooks/Setup.lua`. If you are using this module in a BLT mod.

#### `<hooks>` example

```markup
<Hooks directory="Hooks">
    <hooks directory="Other">
        <hook file="Setup.lua" source_file="lib/setups/setup"/>
    </hooks>
</Hooks>
```

Now it will be in: `mods/MyMod/Hooks/Other/Setup.lua`.

## Functions

### Functions

| Function | Description |
| :--- | :--- |
| Load\(Table config, String prev\_div\) | Called normally by the module's init function. This is what adds the hooks. `config` is the current looping hooks table \(or self.\_config if not present\) and `prev_dir` is the previous directory so it will join the directory to it |
| GetPath\(String directory, String prev\_dir\) | Joins directory and prev\_dir. If prev\_dir is not present returns directory alone. Used by the Load function |

