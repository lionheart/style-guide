[Back to Home](../README.md)

##

If a variable is assigned based on a conditional, only assign the variable after the conditional is written out. I.e.

Not:

x = 1
if b > 2:
    x = 4

Yes:

if b > 2:
    x = 1
else:
    x = 4

code blocks within if / else / with indent 4 spaces
when indenting for anything else, 8 spaces to differentiate

if a [, (, or { is at the end of a line, the closing bracket must be at the indent level of the opening line

dictionary elements on separate lines

if dictionary has more than 3 elements, move first element to next line

backslashes: can use when attribute called from next line

