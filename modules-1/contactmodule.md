# Contact \(contractors\)

Updated for version 3.37.

## Module Definition

The module inherits [ItemModuleBase](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/ItemModuleBase). All parameters and functions of this class are inherited by the module.

### Module name

The name of the module you use as the meta of the module definition is 'contact' or 'ContactModule' if `_force_search` is set to true in the module definition.

### XML Structure

```markup
<contact id name_id desc_id package assets_gui ...>
    ...
</contact>
```

#### `<contact id name_id desc_id package assets_gui>`

| Parameter | Type | Description |
| :--- | :--- | :--- |
| id | String | id of the contact \[REQUIRED\]. This is used as the key for when it is added to the tweak\_data |
| name\_id | String | The localization id for the name of the contact, this is localized when the name of the contact is being displayed |
| desc\_id | String | The localization id for the description of the contact |
| package | String | The package/bundle to be loaded which contains the assets used for the contact |
| assets\_gui | String | The path of the gui file which is to be used by the contact |

And any data which is not present here, but you wish to be included in the tweak data definition

### Example

This example is what you would put inside your main node within your [mod config](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/Module-Config)

```markup
<contact id="shatter" name_id="heist_contact_shatter" desc_id="heist_contact_shatter_description" package="packages/contact_interupt" assets_gui="guis/mission_briefing/preload_contact_interupt"/>
```

### Functions

| Function | Description |
| :--- | :--- |
| AddContactData\(Table narr\_self\) | Called automatically by RegisterHook\(\) if it's called. Adds to narr\_self.contacts \(narr\_self is tweak\_data.narrative\) your new contact. |

