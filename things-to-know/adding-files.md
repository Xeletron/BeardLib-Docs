# Adding Files

Updated for version 3.38.

## Adding files to the game

There are two primary ways of adding files. The first is through the [AddFilesModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/AddFilesModule) and the other is through using an `add.xml` file in your mod overrides. This follows a particular structure, similar to the one used in the [AddFilesModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/AddFilesModule).

NOTE: If you're adding a model you must have a cooked\_physics file with the same name! Even if it is empty! \(Unless you use the include\_x parameters found in [AddFilesModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/AddFilesModule)\).

### Example

```markup
<table>
    <texture path="path/to/my/texture"/>
    <effect path="path/to/my/effect"/>
</table>
```

This follows almost the same syntax as [AddFilesModule](https://github.com/GreatBigBushyBeard/PAYDAY-2-BeardLib/wiki/AddFilesModule).

