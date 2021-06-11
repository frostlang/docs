# docs
this is a primer for the documentation for frost

# hello world
Frost will be familiar to most programmers, it takes inspiration from rust, go, swift and heavily c. the first thing to note is semicolons ';' are optional (they are useful in some cases we will see later).
```
import("io")

main : pub fn {
    println("hello, world!")
}
```

# types

|type|description|storage|  
|----------|----------------------------|-------|
|u0        |void type                   |0
|u1        |boolean                     |8
|u8        |unsigned int                |8
|s8        |signed int                  |8
|u16       |unsigned int                |16
|s16       |signed int                  |16
|u32       |unsigned int                |32
|s32       |signed int                  |32
|f32       |floating point              |32
|u64       |unsigned int                |64
|s64       |signed int                  |64
|f64       |floating point              |64
|fn        |function                    |ptr size (word)
|struct    |structure                   |unspecified
|interface |interface                   |ptr size (word)
|type      |type information struct     |unspecified
|module    |module information struct   |unspecified
|any       |struct containing ptr to any|unspecified

## any
any is simply a struct that contains a pointer to a heap-allocated value and also contains information about the type of the value
```
any : type struct {
    value : ^u32 = 0
    type  : type = typeof u0
}

x : any 
// when we assign 123 to any, 123 is stored at the location of the heap allocated ptr 'value'
x = 123      
x = "hello!"

if x.type.name == "string" {
    println("x contains string :)")
}
```

# variables
```
x := 123
x : u32 123              // if no = is provided, it's 'const'
x : u32 = 123
x : const u32 = 123
x : pub const u32 = 123
```

# expressions
as mentioned above, semicolons are not required to delimit statements and expressions
```
x : u32 = 123 x = 5 // 2 seperate expressions
```

# flow control
familiar if statement
```
x := valid_age(36)
if x
    println("age is valid :)")
else
    println("age is invalid :(")
```

'pythonic' terniary
```
age := 21
overage := if age > 18 true else false
```

inline if statement decleration
```
if name:="bob"; name.contains('b') {
    println("name contains b :)")
}
```

# functions
functions are first class types and can be passed around
```
sqrt : fn (x : any) any {
    x*x // the last expression can be returned
}
```

function calls do not require parenthesis
```
result := sqrt 2 // 4
```

again, we can pass functions to other functions
```
do_something : (value : u32, f : fn (u32) u32)
    f(value)

result := take_fn(2, (x : u32)u32{
    x*x
}) // result = 4
```

# arrays & slices
a slice is a struct containing information about an array it holds. an array requires a known size at compile time
```
x : [5]u32 = {1, 2, 3, 4, 5}
```

a slice requires no size
```
x : [_]u32
for i in 5 x.push i
size := x.size // 5
```
# resolvers
