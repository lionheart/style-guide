[Back to Home](../README.md)

## Naming Things

### Classes

Classes should be named using UpperCamelCase. In general, if the class is derived from another class, suffix the name of the class with a descriptive name of the class it inherits from.

Some examples:

```python
class MeasurementError(Exception):
    pass

class UserManager(BaseUserManager):
    pass
```

The exception to the subclass suffix rule is if the class represents another object, such as a database table. In this case, a descriptive name should be used.

```python
class Category(models.Model):
    pass

class User(models.Model):
    pass
```

Another exception is if a class is created explicitly to be used as a "mixin" to another class (i.e., to extend functionality). In this scenario, the class should be suffixed with "Mixin" or be named as an adjective to describe the added functionality.

```python
class Orderable(object):
    pass

class CreatedMixin(object):
    pass
```

### Variables

Variables should emphasize readability over anything else. Your code is meant to be read, not thrown in a dumpster and forgotten about until the end of time. A variable's purpose should be known immediately to the reader not because of context or surrounding code, but because it was named descriptively.

#### Dates and Times

In cases where dates need to be hardcoded, use common descriptors like "ago" or "from_now".

```python
import datetime

today = datetime.date.today()
one_week_ago = today - datetime.timedelta(days=7)
yesterday = today - datetime.timedelta(days=1)

now = datetime.datetime.now()
one_hour_ago = now - datetime.timedelta(hours=1)
nine_hours_ago = now - datetime.timedelta(hours=9)
twenty_three_hours_from_now = now + datetime.timedelta(hours=23)
```

#### Ordinals and Numbers

If naming a value representing a count of objects, preface the variable with `num`.

```python
num_orders_completed_successfully = models.Orders.objects.filter(completed=True)
```

#### Lists, Dictionaries, Sets, and other "boxed" types

Any boxed type should be descriptive of the individual elements of the objects it contains.

```python
category_ids = r.smembers("categories")
products = models.Product.objects.all()
```

If there is any sort of filtering on a boxed type, you generally want to prepend the name with an adjective.

```python
sold_out_products = models.Product.objects.filter(sold_out=True)
booked_hotels = models.Hotel.objects.filter(booked=True)
```

When a boxed type is ordered in a specific way, do not prepend with the ordering. Add it as a suffix. We do this so that orderings + filterings can be combined without conflict. If there is an ordering, ascending is assumed. If an ordering is descending, spell it out in the variable name.

```python
products_ordered_by_creation_date = models.Product.objects.order_by("created_on")
products_ordered_by_descending_creation_date = models.Product.objects.order_by("-created_on")
```

#### Booleans / Truthy Values

Truthy values should be named in a way that would allow the variable to "sound right" if placed after an "if" statement as if it were parsed by an English speaker. The pattern can be generalized to "N_is_A" or "is_A" (where N = noun and A = adjective).

```python
subscription_is_paid = models.Subscription.objects.filter(id=123, paid=True).exists()
is_above_drinking_age = models.User.objects.filter(id=123, age__gte=21)
```

#### Class References

In some situations, it makes sense to use a variable to reference a generic class. For instance, in Django, you might present one of either two forms to users: one that lets you edit your first name, and another that just displays the first name but is non-editable. Instead of creating two different views, you may want to save the form class to a variable and just reference this variable when the form is needed.

```python
if user.is_staff():
    FirstNameForm = forms.EditableFirstNameForm
else:
    FirstNameForm = forms.ReadonlyFirstNameForm

if request.method == "POST":
    form = FirstNameForm(request.POST, instance=user)

# Etc...
```

### Methods / Functions

Like variables, methods should also be lowercase_separated_by_underscores. If a method takes no arguments, it should be named pretty similarly as if it were a variable representing the same value.

A function is just like a method, except it is not related to a specified class at runtime. The same rules apply to functions as they do to methods.

```python
class Product(models.Model):
    def is_available(self):
        pass

    def formatted_price(self):
        pass
```

For any methods that take a parameter, the rules change a bit. The parameter itself should be named after the type of the object it represents. Additionally, the object type should be suffixed to the method signature.

```python
class Category(models.Model):
    def is_editable_by_user(self, user):
        pass

    def has_permission(self, permission):
        pass
```

As you may have noticed, there are a few prefixes that are used with method signatures. Here's a non-exhaustive list for the most common scenarios:

Usage | Prefix
----- | ------
state (rarely has parameters) | `is_`
ownership | `has_`
ownership with parameter | `contains_`
potential ability | `should_`
current ability | `can_`

`is` can appear in the middle of a method name in the same scenarios as when it can appear in the middle of a variable name, e.g., when a method name follows the "N_is_A" pattern.

#### Static / Class Methods

Static methods generally follow the same naming pattern as instance methods.

### General Guidelines

1. When using adjectives that have a polar opposite, try to use words containing the same number of letters as the opposite. Here are a few examples:

    ```
readonly <> editable
heavy <> light
```

2. Use "positive" words when possible. Double negatives are discouraged.

    ```
readonly > non-editable
```
