[Back to Home](../README.md)

## Line Breaking

A big component of following one of Python's most important rules--limiting lines to 80 characters (or 100, dependeing on your project's guidelines), is knowing when to break lines (code structure is another component which I'll tackle in another article).

### General Rules

Whenever a block of code continues to the following line, always indent the next line two indent levels past the indent level of the line the block started on.

### Strings

We'll start off with a pretty straightforward example.

```python
nasa_description = "The National Aeronautics and Space Administration (NASA) is the agency of the United States government that is responsible for the nation's civilian space program and for aeronautics and aerospace research."
```

When strings must overflow onto another line, always use the continuation character (`\`) to indicate a line break and repeat the quote on the beginning of the next line. We use this to signify to the reader that the line is the continuation of the previous line.

If a space separates the end of one string and the beginning of the next line, place the extra space on the first line.

```python
nasa_description = "The National Aeronautics and Space Administration " \
        "(NASA) is the agency of the United States government that is " \
        "responsible for the nation's civilian space program and for " \
        "aeronautics and aerospace research."
```

Note: while the below is technically following PEP-8's line break rule, it's just hard to read and looks bad. As a result, if the breaking character is in an awkward location within the string (grammatically, or for any other reason), you can shorten to less than 79 characters to a breaking location which makes reading the string easier.

```python
nasa_description = "The National Aeronautics and Space Administration (NASA)" \
        "is the agency of the United States government that is responsible f" \
        "or the nation's civilian space program and for aeronautics and aero" \
        "space research."
```

### Dictionaries

Here's another example with a string within a dictionary.

```python
error_messages = {
    'required': "Username is a required field.",
    'already_taken': "This username has already been taken."
    'invalid': "Username cannot contain quotes, brackets, parentheses, ampersands, or punctuation."
}
```

If a string is contained within a dictionary, the preferred course of action is to extract the string from the expression and refer to it via a variable (following the rules in [Naming Things](Naming-Things.md), of course).

```python
invalid_error_message = "Username cannot contain quotes, brackets, " \
        "parentheses, ampersands, or punctuation."

error_messages = {
    'required': "Username is a required field.",
    'already_taken': "This username has already been taken.",
    'invalid': invalid_error_message
}
```
