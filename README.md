# Desel
A Minimal Sets Definition/Description Language.  
  
Version: 0.1.0  
Its name and syntax still might be changed.  

## Features
* *Minimal*, *Flexible*, and *Readable* syntax
* Independent from the order of definitions
* Supports UTF-8

## Example
### Mathematical
A = { a, b, c }  
c ∈ B, c ∈ C,  
d ∈ B, e ∈ B, e ∈ C  
B = { x | x ∈ A, x ∈ { d, e } }  
C = { x | x ∈ A and x ∈ C, x ∈ B, x ∈ { e, x, y, z } }  
```desel
%A a b c
@c B C
@@ d %B e %B %C
%B %A
%C %A & %C %B x y z
```
### Tagging
```desel
@"html/dog.html" dog html
@"image/dog.png" dog picture
@"image/cat.png" cat picture
%animal %dog %cat
%animal-pictures %animal & %picture
```
### [WIP] Tree-Structured Data
### [WIP] Config File
### [WIP] [WIP]

## Syntax

### Basics
1. Desel is a line oriented programming language.
2. All Desel's lines are beginning with `@` or `%`.
3. All lines not beginning with `@` or `%` are ignored.
4. `@` means `Elements` and `%` means `Sets`.

### Single set definition
This defines a set named `A`  
```desel
%A
```
Names can be wrapped by `"` or `'`.  
```desel
%"This is the name."
```
Elements can be added after set definitions.  
```desel
%A element1 "This is the element2." @"Specifies prefix" ! "This is not contained."
```
You can also write like this;  
```desel
%A element1
%  "This is the element2."
%

%  @"Specifies prefix" !"This is not contained."
```
Expressions also can be added the same as elements.  
```desel
%A %B !%C - %D %E
%  %B & !( %C - %D * %E )
```
You can add homonymous element by writing a prefix just after set's name.  
```desel
%A @
%B@
%C   @ "Of course, you can add elements after this."
```

### [WIP] Multiple sets definition
### [WIP] Single element definition
### [WIP] Multiple elements definition
### Comment

## Author
[ryo33](https://github.com/ryo33)

## License
MIT
