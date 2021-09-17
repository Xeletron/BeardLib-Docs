# Classes

Updated for version 3.37.

## Module Definition

The module inherits [BasicModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/BasicModuleBase). All parameters and functions of this class are inherited by the module.

### Module name

The name of the module you use as the meta of the module definition is 'Classes' or 'ClassesModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<Classes directory>
    <class file/>
    <classes>
    </classes>
</Classes>
```

#### `<Classes directory>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| directory | String | directory/path relative to the mods directory which contains all the classes being used. \[OPTIONAL\] |

#### `<class file/>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| file | String | File name of the class relative to the Mod directory and the directory defined in the main node if it was specified |

#### `<classes directory>`

\*Allows you to define classes in a more organized way. `directory` will join to the head `directory`

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<Classes directory="Classes">
    <class file="my_class.lua"/>
</Classes>
```

For this example your class will be in: `mods/MyMod/Classes/my_class.lua`. If you are using this module in a BLT mod.

#### `<classes>` example

```markup
<Classes directory="Classes">
    <classes directory="SubClasses">
        <class file="my_class.lua"/>
    </classes>
</Classes>
```

Now it will be in: `mods/MyMod/Classes/SubClasses/my_class.lua`.

### Functions

| Function | Description |
| :--- | :--- |
| Load\(Table config, String prev\_div\) | This is called normally by the module's init function, this is what loads all the classes. `config` is the current looping classes table \(or self.\_config if not present\) and `prev_dir` is the previous directory so it will join the directory to it |

