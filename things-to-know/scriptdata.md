# ScriptData

ScriptData is essentially the way diesel uses to store data. We have 3 types of them \(+ 1 which is not actually ScriptData\):

## Custom XML

The most common type of XML used in BeardLib. It's more friendly than the others when writing. Since it's mostly used, I will get into some things you should know when dealing with them. This should help you understand more or so what to write for modules too!

### Things to know

#### What's a meta

A meta or metatable is essentially the text that appears here:

```markup
<TEXT/>
```

In lua it sometimes will be our key.

Not to be confused with values, they look like this:

```markup
<TEXT my_value="Something"/>
```

#### What is a table?

A table is a lua table. It's essentially a place for data to be in. The game reads it and uses it to do many things.

#### How to write tables

We either write it using just

```markup
<table></table>
```

or

```markup
<table/>
```

which is a table without a metatable defined. In code this will always be just an indexed table. Or we can write for example

```markup
<weapons></weapons>
```

or

```markup
<weapons/>
```

which in code can be MyXMLData.weapons.

#### How to write values

Normally to write values in keys we just write it on the head of the node like this:

```markup
<table my_value="Something"/>
```

But what if we want a value that is on an index? We use value\_node:

```markup
<table>
    <value_node value="Something"/>
</table>
```

#### What's a node/The difference between a node and a table

A node is an XML thing only and both tables and values can be nodes. A node is anything that is surrounded with `<>`. So same as `<table>` is a node `<value_node>` is a node of a value.

#### What are the cons of using Custom XML?

**Not required to read for modules**

Conversion between Lua and Custom XML doesn't always go smooth. Since Custom XML introduces a slight problem with how it's converted into a lua table. Custom XML doesn't really separate between "keys" and "index". Consider the following Custom XML:

```markup
<table>
    <MyData/>
</table>
```

Now converting it to a lua table:

```lua
{
    [1] = {},
    MyData = {}
}
```

See this? It created 2 tables. Both are the same table, but we now have a key and a number index when we probably just wanted MyData to be only a key.

#### So how do we solve this?

Using [BeardLib.Utils.XML:Clean\(...\)](https://github.com/simon-wh/PAYDAY-2-BeardLib/wiki/BeardLib.Utils.XML#other)! As the function's description says, it removes keys when they are not needed and indices when they are not needed. In this instance, it would remove the index since we don't have 2 nodes with the same meta name. So if we convert it again \(conversion function has a clean parameter which calls this function\):

```lua
{
    MyData = {}
}
```

And, if our XML looked like this:

```markup
<table>
    <MyData/>
    <MyData/>
</table>
```

After cleanup, it will look like this:

```lua
{
    [1] = {},
    [2] = {}
}
```

You can use the shallow parameter to limit the cleanup only to the table that was provided and not sub tables.

## Generic XML

At first it may seem like "generic" type of XML. But no, this is a special type where every meta of a node is called "entry" and you define the meta \(metatable value\) alone. There's also data for indices and keys separately. Overall, this is better for more sensitive data \(like mission files\). See the cons of custom xml to understand. As this format doesn't have them. However, unlike Custom XML or XML itself even, this format is not meant for writing and only for quick data editing. Mostly because you need to change indices and such which can be a lot of work.

## Binary

Essentially compiled data that once read in the game's code can be converted into a simple Lua table.

## Actual XML

**Not actually ScriptData**

You can see this format in files like .unit, .object. Pretty much traditional XML. You can know one is such when: the type of file is not compiled in the game files or you see something like this in the head of the file:

```markup
<?xml version="1.0"?>
```

Not all XML files have this though.

