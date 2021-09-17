# Table

Updated for version 3.38

## table

Bunch of functions useful when dealing with tables. This class uses a period not a colon so you'd write it as table.func

### Functions

| Function | Return Type | Description |
| :--- | :--- | :--- |
| merge\(Table base\_table, Table new\_table\) | Table | Merges the two passed tables. For example: `table.merge({[1] = true, [2] = "test"}, {[2] = "no test", [3] = false})` will return `{[1] = true, [2] = "no test", [3] = false}` |
| careful\_merge\(Table base\_tbl, Table  new\_table\) | Table | Same as `merge` but reads for "type\_name" value in tables to not merge these types of tables \(Example, MenuUI items use this to not merge with each other\) |
| map\_indices\(Table base\_table\) | Table | Packs all indices \(Not keys!\) into a table |
| add\(Table t, Table items\) | Table | Adds the items from the table items to the end of t. If the index of the item in items already exists in t it will be inserted to the end, if it doesn't, it will be placed at the same index. |
| add\_merge\(Table t, Table items\) | Table | Like merge but instead of setting everything as keys, if the key is a number it will insert it to the table instead |
| search\(Table tbl, String search\_term\) | Number, Table, Table | Search the table. Table being an XML table containing \_meta values. To navigate through the table you'd write the `search_term` like this: "meta1/meta2/meta3". If you want to find a specific meta with value set to something you can do: "meta1/meta2;param1=true"  The function returns you first the index of the result, then the table itself and then the table it's contained in. |
| custom\_insert\(Table tbl, Table add\_tbl, String/Number pos\_phrase\) | Table | A dynamic insert to a table from XML. `tbl` is the table you want to insert to, `val` is what you want to insert, and `pos_phrase` is a special string split into 2 parts using a colon. First part is position to insert which is: before, after, and inside. Second part is a search for the table you want to insert into basically the same string as in `table.search`. So, `pos_phrase` is supposed to look like this: "after:meta1" or "before:meta1" or "before:meta1/meta2", "inside:meta1", etc.  The function will log a warning if the table search has failed and it returns the table it inserts the value into. |

#### Other

| Function | Description |
| :--- | :--- |
| remove\_key\(Table tbl, String/Number key\) | Removes a key or an index \(unlike table.remove\). Checks if the index is not higher of the table's size |
| delete\_value\(Table tbl, Any value\) | Like table delete but can remove any value even if it's in a key \(instead of only index\) |
| script\_merge\(Table base\_tbl, Table new\_tbl\) | This function is a little more complicated to explain. Therefore, you will see examples below. `base_tbl` is the table the script merge will be going in. `new_tbl` is a table that contains some data that decides how the script merge goes. `new_tbl` contains tables and each table can have some parameters: `search`, `mode`, `insert`, and an old parameter that is only used in old mods, `index`.`insert` Basically `table.custom_insert` the value acts as the `pos_phrase` parameter of it. The table that gets inserted is the first indexed table \(like in `mode`\)`index` Same as `insert` but inserts the table itself instead. The parameters above was added because of inconsistency and the fact that this has to remove the parameters which the table may be using.&lt;/ul&gt;Please see examples below. |

### `script_merge` Examples

Lets assume we have the following XML:

```markup
<table>
    <meta1 value="1">
        <meta3/>
    </meta1>
    <meta2 test="true"/>
</table>
```

There will be examples for lua and XML. For **lua** imagine `tbl` variable is the XML data loaded in lua and for **XML** you'll see scriptdata replacement examples.

#### Modes

**merge**

Lua:

```lua
table.script_merge(deep_clone(tbl_test), {
    {
        search = "meta2", mode = "merge",
        {test = "false", str = "hello", tbl = {}}
    }
})
```

XML:

```markup
<mod target_file="x" target_type="y" merge_mode="script_merge">
    <tbl>
        <table search="meta2" mode="merge">
            <table test="false" str="hello">
                <tbl/>
            </table>
        </table>
    </tbl>
</mod>
```

This will merge with the table "meta2". Result:

```markup
<table>
    <meta1 value="1">
        <meta3/>
    </meta1>
    <meta2 test="false" str="hello">
        <tbl/>
    </meta2>
</table>
```

**replace**

Lua:

```lua
table.script_merge(deep_clone(tbl_test), {
    {
        search = "meta1", mode = "replace",
        {_meta = "meta1", something = "value"}
    }
})
```

XML:

```markup
<mod target_file="x" target_type="y" merge_mode="script_merge">
    <tbl>
        <table search="meta1" mode="replace">
            <meta1 something="value"/>
        </table>
    </tbl>
</mod>
```

This will merge with the table "meta2". Result:

```markup
<table>
    <meta1 something="value"/>
    <meta2 test="false" str="hello">
        <tbl/>
    </meta2>
</table>
```

**remove**

Lua:

```lua
table.script_merge(deep_clone(tbl_test), {{search = "meta1", mode = "remove"}, {search = "meta2", mode = "remove"}})
```

XML:

```markup
<mod target_file="x" target_type="y" merge_mode="script_merge">
    <tbl>
        <table search="meta1" mode="remove"/>
        <table search="meta2" mode="remove"/>
    </tbl>
</mod>
```

This will remove both tables. Result:

```markup
<table/>
```

In this example I wanted to show you that you can have multiple stuff in the `new_tbl` table.

**insert**

Lua:

```lua
table.script_merge(deep_clone(tbl_test), {
    {
        search = "meta1/meta3", mode = "insert",
        {_meta = "meta4", val = "true"}
    }
})
```

XML:

```markup
<mod target_file="x" target_type="y" merge_mode="script_merge">
    <tbl>
        <table search="meta1/meta3" mode="insert">
            <meta4 val="true"/>
        </table>
    </tbl>
</mod>
```

This will insert into the table with meta "meta3" which is inside a table with meta "meta1". Result:

```markup
<table>
    <meta1 value="1">
        <meta3>
            <meta4 val="true"/>
        </meta3>
    </meta1>
    <meta2 test="false" str="hello">
        <tbl/>
    </meta2>
</table>
```

#### Just `search`

Lua:

```lua
table.script_merge(deep_clone(tbl_test), {{search = "meta2", test = false, new_val = true}})
```

XML:

```markup
<mod target_file="x" target_type="y" merge_mode="script_merge">
    <tbl>
        <table search="meta2" test="false" new_val="true"/>
    </tbl>
</mod>
```

This example searches for "meta2" and then does another script\_merge with the result. So since there were no properties inside the sub table it will just set the value test=false and new\_val=true in the table it found. The result:

```markup
<table>
    <meta1 value="1">
        <meta3/>
    </meta1>
    <meta2 test="false" new_val="true"/>
</table>
```

#### `insert`

Lua:

```lua
table.script_merge(tbl, {
    {
        insert = "after:meta2",
        {
            _meta = "meta4",
            value = true
        }
    }
})
```

XML:

```markup
<mod target_file="x" target_type="y" merge_mode="script_merge">
    <tbl>
        <table insert="after:meta2">
            <meta4 value="true"/>
        </table>
    </tbl>
</mod>
```

This example inserts a new table with meta "meta4" and value named "value" set to true after the table "meta2".

The result:

```markup
<table>
    <meta1 value="1">
        <meta3/>
    </meta1>
    <meta2 test="true"/>
    <meta4 value="true"/>
</table>
```

