```
A noun is defined as either an atom, which is defined as a natural number, or a cell, which is defined as an ordered pair of nouns. A pair has exactly two items in it.

[a b] is a way to write a cell that consists of two nouns, a and b. In a cell [a b], we say the head of the cell is a and the tail is b. If you have a cell [a b] where b is [c d], that the tail of [a b] is still b. If you have a cell [a b] where a is [e f], that the tail of [a b] is still a.
[a [b c]] is a way to write a cell that consists of a noun a in the head and a tail consisting of a cell containing b and c, which are also nouns.
The previous expression can be written as [a b c] with an implicit right association, and is the preferred way to write the expression. Most expressions are written with implicit right association.

Let's define a few logical operators that may be applied to input nouns to provide a resulting output noun:

We define the noun type logical operator, ? that can be applied to any noun 'a'.
?a will evaluate to 0 for a cell, and 1 for an atom.

We define the increment logical operator, + that can be applied to any noun 'a'.
+a will evaluate to (1 + a) if a is an atom, and will crash if a is a cell.

We define the equivalence logical operator, = that can be applied to any two nouns.

=[a a] will evaluate to 0, and =[a b] where b is a different noun than a will evaluate to 1.
In our defined operations, when the two input nouns are the same, the equivalence operator evaluates to 0, and when they are different the equivalence operator evaluates to 1.

We define the / logical operator that may be applied to nouns:
/(1 a) will output a, and may be applied to any noun.
/(2 [a b]) will output a (the head of the cell), and may only be applied to a cell. If it is applied to an atom, crash.
/(3 [a b]) will output b (the tail of the cell), and may only be applied to a cell. If it is applied to an atom, crash.
If the head atom is greater than 3, will recursively apply the '/' operator using the following reduction:
/(2a b) will reduce to /(2 /(a b)) which will then be further evaluated until it reaches one of the base cases I described to you.
/((2a + 1) b) will reduce to /(3 /(a b)) which will then be further evaluated until it reaches one of the base cases I described to you.


We define the Nock function as a function that takes an input noun (described as a cell of [subject formula]), and returns an output noun or crashes. The Nock function is defined below.

A valid Nock formula is always a cell. If the head of the formula is a cell, Nock treats both head and tail as formulas, evaluates each against the subject, and produces the cell of their products. If the head of the formula is an atom, it's an instruction from 0 to 5. If the head of the formula is higher than 5, it is not valid. Invalid Nock instructions result in a crash.

Nock(a) evaluates to *a.
In the following examples, a is a subject and the following cell is the formula:
*[a 0 b] evaluates to /(b a)
*[a 1 b] evaluates to b
*[a 2 b c] evaluates to *[*[a b] *[a c]]. (Note that the first subformula generates a new subject, the second subformula generates a new formula, and then the old subject and formula are discarded. Then, the new formula is evaluated against the new subject as follows: *[new-subject new-formula] ). Remember, 1. compute new subject, 2. compute new formula, 3. run new formula against new subject.
*[a 3 b evaluates to ?*[a b]
*[a 4 b] evaluates to +*[a b]
*[a 5 b c] evaluates to =[*[a b] *[a c]]


Please evaluate the following Nock expression: [[55 0 1] [2 [0 2] [0 3]]]
```
