This style guides lists the coding conventions used in ["The Kitchen"](https://www.roblox.com/communities/34607511/Redstoners) aka "Redstoners" roblox game developing group.
Hopefully lololol will also use this like please bro i beg you with all my heart bro cmon now bro pls :sob::sob::sob:🙏🙏🙏

# Indentation and formatting
- Indent with 4 spaces.
- Replace tabs with spaces, there are options for that in IDEs.
- Use LF (Unix) line endings.
```lua
for i = 1, 10 do
    for j = 1, 20, do
        print("Hello, world!")
    end
end
```

# Documenting functions
- A single line comment will suffice for short functions.
- Use three or more line comments for longer or more complicated functions.
```lua
-- This function simply adds 2 inputs
local function Add(x: SomeType, y: SomeType): SomeType
    return x + y
end

--
-- This function does some very complicated stuff,
-- that needs to be explained in a long ass comment frfr.
--
local function SomeVeryComplicatedStuff(): ()
    ...
end
```
- Make every function parameter typesafe. If you don't know the exact parameter types ahead of time, put the type as "PossibleType1 | PossibleType2 | PossibleType3".
- If you don't know even the possible type of the input, put the type as "any"

