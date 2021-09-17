# String

Updated for version 3.38

## string

An existing class for dealing with strings.

BeardLib doesn't add much to here.

Remember, this class uses periods not colons. So you'd call it like this: string.func.

### Functions

#### Get

| Function | Return Type | Description |
| :--- | :--- | :--- |
| pretty2\(String str\) | String | Converts `str` into a "pretty" string. Basically, it separates capitalized words with a space; so a string such as: "MyCoolString" would be "My Cool String" |
| key\(String str\) | String | Returns the Idstring key of `str` \(Basically Idstring\(str\):key\(\)\) |

## Anonymous functions

### Functions

| Function | Description |
| :--- | :--- |
| prnt\(...\) | Prints all arguments \(separated by a tab\). This function doesn't require to do tostring\(\). Though it won't print nulls. |
| prntf\(String s, ...\) | Like `prnt` but prints using string.format; so you can do things like `prntf("My name is %s and I need a %s", "Dallas", "Medic bag")` |

