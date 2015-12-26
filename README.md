# Desel
A Sets Definition/Description Language.  
  
Desel should be pronounced like Diesel.  
Version: 0.1.1  
Its syntax still might be changed.  

## Feature
* *Minimal*, *Readable*, and *Flexible* Syntax

## Spec
* Desel is case sensitive.
* Desel only allows UTF-8 encoded characters.
* Desel treats `LF` and `CRLF` as newline.
  
You can read the syntax description of Desel in [grammar.ebnf](grammar.ebnf).  

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

## Syntax

### Basic
* `%` means `Sets` and `@` means `Elements`.
* Desel is a line oriented language.
* All Desel's lines are beginning with `@` or `%`.
* All lines not beginning with `@` or `%` are ignored.
* Characters after `#` are ignored.

### Single set definition
This defines a set named `A`.  
```desel
%A
```
Names can be wrapped by `"` or `'`.  
```desel
%"This is the name."
%'name'
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
%  %B & !( %C - %D & %E )
```
Note: All sets in expressions requires a prefix, `%`.  
  
You can add homonymous element by adding `@` just after set's name.  
```desel
%A @ # Of course, you can add elements after this.
%B@
%C   @ a b c
```

### Single element definition
This defines a elements named `a`, `b`, and `c`.  
```desel
@a
@"b"
@'c'
```
Sets which contains the element or don't can be specified after element definitions.  
```desel
@a A %B     # %A and %B contain @a,
@  ! C !%D  # %C and %D don't.
```
You can add homonymous set by adding `%` just after element's name.  
```desel
@a % # You can write sets after this.
@a%
@a  % A ! B C
```

### Multiple sets definition
You can write multiple sets in one line by using `%%`.  
```desel
%% A @a @b %B @c @d C @ !@e
```
Note: All elements in multiple sets definition syntax requires a prefix, `@`.  
  
This is the same as the definitions below.  
```desel
%A a b
%B c d
%C @ !@e
```
If you want to convert the definitions below to multiple sets definition syntax,  
```desel
%A a b c %B
%B %C - %D & %E
%C !(%D - %E)
```
use `(` and `)` to cover up sets and expressions like this;  
```desel
%% A @a @b @c (%B) B (%C - %D & %E) C (!(%D - %E))
```

### Multiple elements definition
You can write multiple elements in one line by using `@@`.  
```desel
@@ a %A %B @b %B %C c % !%D
```
Note: All sets in multiple elements definition syntax requires a prefix, `%`.  
  
This is the same as the definitions below.  
```desel
@a A B
@b B C
@c % !%D
```

## Author
[ryo33](https://github.com/ryo33)

## License
MIT
