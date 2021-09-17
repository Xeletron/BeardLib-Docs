# Hooks

Updated for version 3.38

This page assumes you already have some knowledge in lua and payday 2 lua structure. The functions like almost everywhere are class functions so you'd call them like Hooks:QuickClass\(...\)

## Hooks

Already an existing class in BLT. BeardLib adds a few useful functions to it. [https://payday-2-blt-docs.readthedocs.io/en/latest/lua/hooks/](https://payday-2-blt-docs.readthedocs.io/en/latest/lua/hooks/)

### Functions

| Function | Description |
| :--- | :--- |
| RemovePostHookWithObject\(Table object, String id\) | Removes a post hook with the id `id`. Added since BLT didn't have such function. `object` is of course, the class you want to add hooks to |
| RemovePreHookWithObject\(object, id\) | Removes a pre hook with the id `id` |
| QuickClass\(hooks\_name\) | Returns a class that has functions for quicker hooking. `hook_name` is the name that will prefix to each hook you add. The functions are: `Post(object, func_name, hook_func)`, `Pre(object, func_name, hook_func)`, `RemovePost(object, func_name)`, and `RemovePre(object, func_name)`. `object` is the class you want to add hooks to, `func_name` is the function name you want to hook to, and `hook_func` is the function that should run in post or pre hook |
| LazyClass\(object, hooks\_name\) | Like `QuickClass` but lazier! This one takes an object with `hooks_name`. `object` is the class you want to add hooks to. Because of that, the functions don't have a class parameter so: `Post(func_name, hook_func)`, `Pre(func_name, hook_func)`, `RemovePost(func_name)`, and `RemovePre(func_name)`. There's an additional function to set the class which is `SetClass(object)` |

## Anonymous functions

Functions that don't have a class and are called like func\(\).

Useful functions for dealing with functions/hooks.

| Function | Description |
| :--- | :--- |
| ClassClbk\(Table clss, String func, a, b, c, ...\) | A replacement for the function `callback`. It's faster \(in most cases\) and doesn't require writing self twice \(Cases where you'd want to modify self you'd probably be more interested in using `SimpleClbk`\). `clss` is the table/class of the function you want to have a callback of, `func` is the name of the function and `a`, `b`, `c`, `...` are the arguments for the callback \(unlike callback, this accepts infinite number of arguments\) the arguments will be before the arguments when the callback will be called |
| SimpleClbk\(Funciton f, a, b, c, ...\) | Like `ClassClbk` but `f` is a direct function instead. So you can have anonymous functions as callbacks \(without doing the old `callback(nil, _G, "func")` bullshit\). It's even faster than `ClassClbk` is. The rest of the arguments are the same as in `ClassClbk` |
| SafeClbk\(...\) | Same as `SimpleClbk` but runs the call through a pcall. This is slower so don't use it blindly! |
| SafeClassClbk\(...\) | Same as `ClassClbk` but runs the call through a pcall. This is even slower. |

### Example

#### ClassClbk

```lua
local clbk = ClasClbk(self, "MyCallback", 1,2,3)
local clbk2 = ClassClbk(OtherClass, "CallMe", "hey")
```

#### SimpleClbk

```lua
local clbk = SimpleClbk(clbkFunc, 1,2)
local clbk2 = SimpleClbk(SomeClass.Func, self, 3)
```

