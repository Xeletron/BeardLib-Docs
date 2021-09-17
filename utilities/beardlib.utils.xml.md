# XML

Updated for version 3.38

## BeardLib.Utils.XML

Bunch of functions useful when dealing with tables from custom\_xml files.

### Functions

| Function | Return Type | Description |
| :--- | :--- | :--- |
| GetNode\(Table tbl, String meta\) | Table | Returns the first node the function finds that have the meta `meta` |
| FindNode\(Table tbl, String metas\) | Table | Same as GetNode but allows you to find the node like this: node/a/b/c |
| GetNodes\(Table tbl, String meta\) | Table | Same as GetNode but packs every node it finds into a table |
| GetNodeIndex\(Table tbl, Table node\) | Number | Returns the index of `node` in `tbl` if it finds it. Returns null if it doesn't exist |
| GetIndexMeta\(Table tbl, String meta\) | Number | Returns the index of the first node the function find that has the meta `meta` |
| GetMetaIndics\(Table tbl, String meta\) | Table | Like `GetIndexMeta` but packs every result into a table |

#### Other

| Function | Description |
| :--- | :--- |
| SetNode\(Table tbl, Table node, Table new\_node\) | Searches for `node` in `tbl` and sets it as `new_node` |
| SetNodeMeta\(Table tbl, String node, Table new\_node\) | Like `SetNode` but searches for the node using a meta |
| CleanKeys\(Table tbl, Boolean shallow\) | Cleans the table from keys; keeping only the indices. `shallow` keeps the cleaning process only in the first level of the table without cleaning it all |
| CleanIndices\(Table tbl, Boolean shallow\) | Like `CleanKeys` but cleans the indices instead. This function including `CleanKeys` can be used for nodes too |
| Clean\(Table tbl, Boolean shallow\) | A special clean function. Removes keys only if the table contains at least two indices of the same meta, removes indices if only one of the same meta as the key exists. In other words, makes sure that when you save the XML it won't duplicate shit |
| InsertNode\(Table tbl, Table node\) | Like table insert but, inserts a node properly so script serializer \(what converts it into custom\_xml\) won't think the key and first index are the same thing |

