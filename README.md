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
- Make every function parameter typesafe. If you don't know the exact parameter types ahead of time, put the type as ```luau "PossibleType1 | PossibleType2 | PossibleType3"```.
- If you don't know even the possible type of the input, put the type as ```luau "any"```

# Variable names
- A very subjective point is of course making the naming as clear as possible. You should make the name as clear as possible !!!NOT TO YOUSELF!!!, but !!!TO THE OTHER PEOPLE!!! in the team.
- Another point is making the names readable. For readability, snake case is our choise for naming variables.
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
- Use underscore '_' character for ignored variables. It is useful in ```luau pairs``` loops and retrieving data from a tuple.
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

local some_class_object = SomeClass.New()
some_class_object:SomeMethod()
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

# Tables
- When creating a table, prefer populating its fields all at once, if possible:
```luau
local player = {
   name  = "Jack",
   class = "Rogue",
}
```

- You can add a trailing comma to all fields, including the last one.
> Rationale: This makes the structure of your tables more evident at a glance. Trailing commas make it quicker to add new fields and produces shorter diffs.
- Use plain key syntax whenever possible, use quoted ["key"] syntax when using names that can't be represented as identifiers and never mix representations. If you can't use only plain key syntax, just use quoted ["key"] everywhere:
```luau
-- Bad. Don't mix.
table = {
   hihi       = val0,
   ["1394-E"] = val1,
   ["UTF-8"]  = val2,
   ["and"]    = val2,
}

-- Good. Just use quoted ["key"] syntax everywhere.
table = {
   ["Hihi"]   = val0,
   ["1394-E"] = val1,
   ["UTF-8"]  = val2,
   ["and"]    = val2,
}
```
- Vertically align all the fields at the same table depth for readability. Don't vertically allign values with tables though because it will be ugly. Example:
```luau
-- Bad. Ugly and reads poorly.
table = {
    ["Hi"]        = "Hello",
    ["Bye"]       = "Goodbye",
    ["Aintnoway"] = {
        ...
    },
}

-- Good.
table = {
    ["Hi"]  = "Hello",
    ["Bye"] = "Goodbye",
    ["Aintnoway"] = {
        ["Hi"]          = "Hello",
        ["Bye"]         = "Goodbye",
        ["KokoiDamage"] = "Neznau",
    },
}
```
# Strings
- Use double quotes whenever possible. Use single quotes for single character constants and strings that contain double quotes:
```luau
--
-- CONSTANTS
--
local SOME_CHAR_CONSTANT = 'E'
...
local name     = "TheKitchen"
local sentence = 'The name of the program is "TheKitchen"'
```
> Rationale: Double quotes are used as string delimiters in a larger number of programming languages. Single quotes are useful for avoiding escaping when using double quotes in literals. Single quotes are also used for single characters in a lot of C family languages.

# Line lengths
- Soft limit: 50 characters. Try to stay under that, but sometimes it is necessary to go beyond.
- USE ONE STATEMENT PER LINE. You can use table sending syntax of calling ```luau Function { TableStuff }```, but if you have not just the table as the parameter, you must separate the table into a variable and then pass the table reference.
- USE ONE STATEMENT PER LINE. Don't do fucking
```luau
local inventory = inventories_table["Inventory .. tostring ( someFunc ( x + 125 ) * 120 )"]
```
- instead do
```luau
local added_x       = x + 125
local modified_x    = someFunc(scaled_x)
local scaled_x      = modified_x * 120
local string_x      = tostring(scaled_x)
local inventory_key = "Inventory" .. string_x
local inventory     = inventories_table[inventory_key]
```
> You could say it is harder to write this type of code.
> But it will be a gajillion times less of a pain in the ass to debug and change this code however you like.
- Line lengths are naturally limited by using one statement per line. If that still produces lines that are too long (e.g. an expression that produces a line over 256-characters long, for example), this means the expression is too complex and would do better split into subexpressions with reasonable names.

> Rationale: No one works on VT100 terminals anymore. If line lengths are a proxy for code complexity, we should address code complexity instead of using line breaks to fit mind-bending statements over multiple lines.

# Function declaration
- Prefer function syntax over variable syntax. This helps differentiate between named and anonymous functions.
```luau
-- bad
local nope = function(name, options)
   -- ...stuff...
end

-- good
local function yup(name, options)
   -- ...stuff...
end
```
- Perform validation early and return as early as possible.
```luau
-- bad
local function is_good_name(name, options, arg)
   local is_good = #name > 3
   is_good = is_good and #name < 30

   -- ...stuff...

   return is_good
end

-- good
local function is_good_name(name, options, args)
   if #name < 3 or #name > 30 then
      return false
   end

   -- ...stuff...

   return true
end 
```
# Function calls

- Even though Lua allows it, do not omit parenthesis for functions that take a unique string literal argument.
```luau
-- bad
local data = get_data"KRP"..tostring(area_number)
-- good
local data = get_data("KRP"..tostring(area_number))
local data = get_data("KRP")..tostring(area_number)
```
> Rationale: It is not obvious at a glace what the precedence rules are when omitting the parentheses in a function call.
> Can you quickly tell which of the two "good" examples in equivalent to the "bad" one? (It's the second one).
- You can and should omit parenthesis for functions that take a single table argument. E.g:
```luau
local an_instance = a_module.new {
   a_parameter = 42,
   another_parameter = "yay",
}
```
# Declaration of Functions in Tables
- Only declare functions inside the table for metatables:
```luau
-- Good.
local version_mt = {
   __eq = function(a, b)
      -- code
   end,
   __lt = function(a, b)
      -- code
   end,
}

-- Good.
function my_module.a_function(x)
   -- code
end

-- Bad.
local my_module = {
    a_function = function(x)
       -- code
    end
}
```
> Rationale: Metatables contain special behavior that affect the tables they're assigned (and are used implicitly at the call site), so it's good to be able to get a view of the complete behavior of the metatable at a glance.

# Variable declaration
-- Always use local to declare variables.
```luau
-- bad
superpower = get_superpower()

-- good
local superpower = get_superpower()
```
> Rationale: Not doing so will result in global variables to avoid polluting the global namespace.

# Variable scope
-- Assign variables with the smallest possible scope.
```luau
-- bad
local function good()
   local name = get_name()

   test()
   print("doing stuff..")

   --...other stuff...

   if name == "test" then
      return false
   end

   return name
end

-- good
local bad = function()
   test()
   print("doing stuff..")

   --...other stuff...

   local name = get_name()

   if name == "test" then
      return false
   end

   return name
end
```
> Rationale: Lua has proper lexical scoping. Declaring the function later means that its scope is smaller, so this makes it easier to check for the effects of a variable.

# Conditional expressions
Don't use the and/or idiom for the pseudo-ternary operator.
```luau
-- Bad.
local function default_name(name)
    -- return the default "Waldo" if name is nil
    return name or "Waldo"
end

-- Good.
local function default_name(name)
    -- return the default "Waldo" if name is nil
    if name == nil then
        return "Waldo"
    end
    return name
end

-- Bad.
local function brew_coffee(machine)
    return (machine and machine.is_loaded) and "coffee brewing" or "fill your water"
end

-- Good.
local function brew_coffee(machine)
    if machine == nil then
        warn("machine is nil")
    end
    if not machine.is_loaded then
r        eturn "fill your water"
    end
    return "coffee brewing"
end
```
