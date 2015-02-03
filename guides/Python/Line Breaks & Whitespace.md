[Back to Home](../../README.md)

## Line Breaks & Whitespace

A big component of following one of Python's most important rules--limiting lines to 80 characters (or 100, depending on your project's guidelines), is knowing when to break lines (code structure is another component which I'll tackle in another article).

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

### Dictionaries, Lists, and Sets

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

The same rule applies to lists and sets.

```python
colors = ["aqua", "brown", "charcoal", "emerald", "fuschia", "green", "indigo", "khaki", "lime", "maroon"]
```

The difference with dictionaries, however, is that it's encouraged to list multiple elements on the same line when the list elements are of a small size (in general, less than 20 characters) and strings, OR if there are less than three elements in the list.

```python
colors = ["aqua", "brown", "charcoal", "emerald", "fuschia", "green",
        "indigo", "khaki", "lime", "maroon"]
```

Here are two more complicated examples.

```python
colors_two = [aqua_color, brown_color]
colors_three = [aqua_color, brown_color, charcoal_color, emerald_color]
```

When a list contains variables or contains strings equal to or greater than 20 characters, separate out the elements into separate lines. However&mdash;as mentioned above&mdash;if the list contains less than three elements, it shouldn't be broken.

```python
colors_two = [aqua_color, brown_color]
colors_three = [
    aqua_color,
    brown_color,
    charcoal_color,
    emerald_color
]
```

### Objects with Attributes

There might be situations where an object can be altered or manipulated by chaining attributes to it. We see this a lot when using the Django ORM, where objects in the database can be filtered by many parameters, which can end up taking much more than our line-spacing limit. Here's an example for how we might break up a long database query.

```python
users = models.User.objects.annotate(num_orders=Count('orders')).filter(approved=True, birthdate__year=2014).exclude(num_orders=0)
```

Preferred:

```python
users = models.User.objects.annotate(num_orders=Count('orders') \
    .filter(approved=True, birthdate__year=2014) \
    .exclude(num_orders=0)
```

If an individual method call within the group of attribute calls itself contains multiple method parameters, we split those up as we would a dictionary or list (see above).

```python
users = models.User.objects.annotate(num_orders=Count('orders')) \
    .filter(
        preferred_os=MAC_OS_X,
        approved=True,
        birthdate__year=2014
    ) \
    .exclude(num_orders=0)
```


