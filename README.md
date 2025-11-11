This style guides lists the coding conventions used in ["The Kitchen"](https://www.roblox.com/communities/34607511/Redstoners) aka "Redstoners" roblox game developing group.
Hopefully lololol will also use this like please bro i beg you with all my heart bro cmon now bro pls :sob::sob::sob:🙏🙏🙏

# Indentation and formatting
- Indent with 4 spaces.
- Replace tabs with spaces, there are options for that in IDEs.
- Use LF (Unix) line endings.
```luau
for i = 1, 10 do
    for j = 1, 20, do
        print("Hello, world!")
    end
end
```

# Documenting functions
- A single line comment will suffice for short functions.
- Use three or more line comments for longer or more complicated functions.
```luau
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

# Variable names
- A very subjective point is of course making the naming as clear as possible. You should make the name as clear as possible not to yourself, but to the other people in the team.
- Another point is making the names readable. If your variable name is longer than 2 words, you should use snake case, as also shown in the example below.
```luau
--
-- THIS IS AN EXAMPLE OF A BAD VARIABLE NAME. EVEN THOUGH I KNOW THAT THIS IS ZETA OF (1), OTHER PEOPLE IN MY TEAM MOST LIKELY HAVE NO IDEA.
--
local zeta = -1/12
--
-- This is a beter name.
--
local riemann_zeta_func_of_1 = -1/12
```
- Constants should be capitalized and put in a separate block on top of the file.
- Numerical constants should also be put in braces, e.g. (5).
- All constants should be vertically alligned for readability.
```luau
--
-- CONSTANTS
--
local MATH_PI                = math.pi
local ONE_HALF               = (0.5)
local COSINE_OF_ONE_HALF     = math.cos(ONE_HALF)
local SOME_BULLSHIT_CONSTANT = (5)
```
- Use underscore '_' character for ignored variables. It is useful for loops and retrieving data from a tuple.
```luau
for _, value in pairs(t) do
    ...
end
local _, second_returned_value, _, fourth_returned_Value = Some_Function_Returning_Four_Values_In_A_Tuple()
```
- Use either i, j, k or some descriptive iterator names in 'numeric for loops' and with 'ipairs'.
- Prefer more descriptive names than k and v when iterating with pairs, unless you are writing a function that operates on generic tables.
```luau
for i = 1, 20, do
    for j = i, 15 do
        for k = j, 25 do
            ...
        end
    end
end

for arrayIndex = 1, 5 do
    array[arrayIndex] += 1
end
```
- When doing OOP, use CamelCase for Classes and their Methods. E.g.
```luau
type SomeClassType = {}
local SomeClass = ({} :: any) :: SomeClassType
SomeClass["__index"] = SomeClass

function SomeClass.SomeMethod(self: SomeClassType)
    ...
end  
```
- Prefer using is_ when naming boolean functions:
```luau
-- Bad.
local function evil(alignment)
   return alignment < 100
end

-- Good.
local function is_evil(alignment)
   return alignment < 100
end
```
