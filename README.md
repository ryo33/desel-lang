# Desel
A Minimal Sets Definition/Description Language.  
  
Version: 0.1.0  
Its name and syntax still might be changed.  

## Features
* *Minimal*, *Flexible*, and *Readable* syntax
* Independent from the order of definitions
* Supports UTF-8

## Example
Writing following sets in Desel.  
A = { a, b, c }  
h ∈ B  
B = { d, e, f, g, h }  
C = { c, d, e }  
i ∈ D, j ∈ D  
D = { i, j, k }  
E = { x | x ∈ A and x ∈ C, x ∈ D, x ∈ { x, y, z } }  
F = { x | x ∈ A and x ∈ B and x ∈ C }  
```setdl
%A a b c
@h B
%B d e
% f
% g
@@ i %D j %D
%% C @c @d @e D @k
%E %A & %C %D x y z
%F %A & %B & %C
```

## Syntax

### Basics
1. Desel is a line oriented programming language.
2. All Desel's lines are beginning with `@` or `%`.
3. All lines not beginning with `@` or `%` are ignored.
4. `@` means `Elements` and `%` means `Sets`.

### [WIP] Single set definition
### [WIP] Multiple sets definition
### [WIP] Single element definition
### [WIP] Multiple elements definition
### Comment

## Author
[ryo33](https://github.com/ryo33)

## License
MIT
