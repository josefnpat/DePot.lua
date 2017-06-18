# DePot.lua
## A fault tolerant gettext encoder/decoder for Lua

# Utility

`depot: usage: depot [--pot] <source> [target]`

`--pot`: Make into a gettext template

`<source>`: The source file

`<target>`: The target file

# Library

## depot.decode(data)

This function takes a `gettext` po/pot file and renders it into a table with each element in the form of `{id=msgid,str=msgstr}`

e.g.;

```lua

raw = [[
# Greetings
msgid "Hello"
msgstr "Hallo"
]]

local source_data = depot.decode(raw)
for _,v in pairs(source_data) do
  print(v.id,v.str)
end
```

## depot.decode_file(filename)

This function uses Lua's `io` module to read a file in line by line to create a table with each element in the form of `{id=msgid,str=msgstr}`

e.g.;

```lua
local source_data = depot.decode_file('foo.po')
for _,v in pairs(source_data) do
  print(v.id,v.str)
end
```

## depot.encode(data)

This function takes a table with each element in the form of `{id=msgid,str=msgstr,comment=comment}` to create a valid `gettext` string that can be saved to a file.

e.g.;

```lua
raw = depot.encode({id="Hello",str="Hallo"})
```

## depot._decode(iterator)

This function uses a Lua iterator to create a table with each element in the form of `{id=msgid,str=msgstr}`. This function is used by `depot.decode` and `depot.decode_file`.

# License

This library is untder the MIT license. See license for details.
