# Desel
A Sets Definition/Description Language.  
  
Desel should be pronounced like Diesel.  
Version: 0.2.0  
Its syntax still might be changed.  
You can read the syntax description of Desel in [grammar.ebnf](grammar.ebnf).  

## Feature
* *Minimal*
* *Readable*
* *Flexible*

## Spec
* Line oriented
* Case sensitive
* UTF-8
  

## Example

### Mathematical
A = { a, b, c }  
B = { x | x ∈ A, x ∈ { d, e } }  
C = { x | x ∈ A and x ∈ B, x ∈ { c, e, x, y, z } }  
```desel
%A a b c
@c B C
@@ @d B @e B C
%B %A
%C %A & %B x y z
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
* Desel is a line oriented language.
* `%` means `Sets` and `@` means `Elements`.
* All Desel's lines are beginning with `@` or `%`.
* All lines not beginning with `@` or `%` are ignored. (comment)
* Characters after `#` are ignored. (comment)

### Single set definition

This defines a set labeled as `A`.  
```desel
%A
```
Names can be wrapped by `"` or `'`.  
```desel
%"This is the label."
%'label'
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
Note: A prefix is required for all sets in expressions.  
  
You can add homonymous element by adding `@` just after set's label.  
```desel
%A @ # Same as "%A A"
%B@
%C   @ a b c # Off course, you can add something after homonymous element.
```
  
You can add homonymous set of elements by adding `%` just after their labels.  
```desel
%A a% b % # Same as "%A a %a b %b
```

### Single element definition

This defines a elements labeled as `a`, `b`, and `c`.  
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
You can add homonymous set by adding `%` just after element's label.  
```desel
@a % # You can add sets after this.
@a%
@a  % A ! B C
```

### Multiple sets definition

You can write multiple sets in one line by using `%%`.  
```desel
%% %A @a @b %B c d %C @ ! e
```
Note: A prefix is required for all sets in multiple sets definition syntax.  
  
This is the same as the definitions below.  
```desel
%A a b
%B c d
%C @ !@e
```
It can also contain expressions.  
```desel
%% %A @a @b @c (%B) %B (%C - %D & %E) %C !(%D - %E)
```

### Multiple elements definition

You can write multiple elements in one line by using `@@`.  
```desel
@@ @a %A %B @b B C @c % !D
```
Note: A prefix is required for all elements in multiple sets definition syntax.  
  
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
