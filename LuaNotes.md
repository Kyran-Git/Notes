# Lua Programming Language Study Guide

## Table of Contents
1. [Basic Syntax and Variables](#1-basic-syntax-and-variables)
2. [Functions](#2-functions)
3. [Tables](#3-tables)
4. [Metatables and Metamethods](#4-metatables-and-metamethods)
5. [Object-Oriented Programming](#5-object-oriented-programming)
6. [Modules](#6-modules)

## 1. Basic Syntax and Variables

### Comments
```lua
-- Single line comment

--[[
    Multi-line
    comment
--]]
```

### Variables and Data Types
- Numbers (integer or float): `num = 42`
- Strings:
  ```lua
  s = 'single quotes'
  t = "double quotes"
  u = [[Multi-line
        string]]
  ```
- `nil`: Used to undefine variables
- Variables are global by default
- Use `local` keyword for local variables

### Control Flow

#### While Loops
```lua
while condition do
    -- code
end
```

#### If Statements
```lua
if condition then
    -- code
elseif other_condition then
    -- code
else
    -- code
end
```

#### For Loops
```lua
-- Counting up
for i = 1, 100 do
    -- code
end

-- Counting down
for i = 100, 1, -1 do
    -- code
end
```

#### Repeat Until
```lua
repeat
    -- code
until condition
```

### Important Notes
- No `++` or `+=` operators
- `~=` is the not equals operator
- Only `nil` and `false` are falsy
- String concatenation uses `..` operator
- Logical operators: `and`, `or`, `not`

## 2. Functions

### Basic Function Definition
```lua
function name(params)
    return value
end
```

### Anonymous Functions and Closures
```lua
-- Anonymous function
f = function(x) return x * x end

-- Closure example
function adder(x)
    return function(y) return x + y end
end
```

### Function Features
- Multiple return values
- Variable number of arguments
- First-class functions (can be assigned to variables)
- Functions with one string parameter don't need parentheses

## 3. Tables

### Basic Usage
```lua
-- As dictionaries
table = {
    key1 = 'value1',
    key2 = 'value2'
}

-- As arrays (1-based indexing!)
array = {'value1', 'value2', 'value3'}
```

### Key Features
- Only compound data structure in Lua
- Can be used as both dictionaries and arrays
- 1-based indexing for arrays
- Can use dot notation for string keys: `table.key`
- Can use bracket notation for any key: `table['key']`

### Table Iteration
```lua
for key, value in pairs(table) do
    -- code
end
```

## 4. Metatables and Metamethods

### Setting Metatables
```lua
setmetatable(table, metatable)
getmetatable(table)
```

### Common Metamethods
- `__add(a, b)`: For `a + b`
- `__sub(a, b)`: For `a - b`
- `__mul(a, b)`: For `a * b`
- `__div(a, b)`: For `a / b`
- `__index(a, b)`: For `a.b`
- `__newindex(a, b, c)`: For `a.b = c`

## 5. Object-Oriented Programming

### Basic Class Pattern
```lua
MyClass = {}

function MyClass:new()
    local obj = {}
    self.__index = self
    return setmetatable(obj, self)
end

function MyClass:method()
    -- method implementation
end
```

### Inheritance
```lua
SubClass = ParentClass:new()

function SubClass:method()
    -- override method
end
```

## 6. Modules

### Creating Modules
```lua
local M = {}

-- Private function
local function private()
end

-- Public function
function M.public()
end

return M
```

### Using Modules
```lua
local myModule = require('module_name')
```

### Module Features
- Modules are cached
- Use `dofile()` for uncached loading
- Use `loadfile()` to load without executing
- Use `load()` for string loading

---

## Tips for Learning
1. Remember that Lua uses 1-based indexing
2. Tables are the only compound data structure
3. Everything is global unless declared `local`
4. Metatables provide operator overloading
5. The `:` syntax automatically passes `self`
6. `nil` is used for undefined values
