# The Void

`_` is the "void" operator. It performs multiple functions depending on it's context.

# As a value

The void operator can be used as a value for any variable. This in the only nil value
in Jasper. Whilst JavaScript has both `undefined` and `null`, `_` will always be
translated to the former and semantically covers both cases.

Here is an example where the default value returned is `_`, if none of the earlier
conditions match:

```
@numberToString(n num)str?
	if n == 1
		<< 'One'
	if n == 2
		<< 'Two'
	<< _
```

# In a type constructor

It sometimes useful to create a variable with a specfic type, but with a void value.
In these cases, the void operator can be passed as the only argument to the type
constructor:

```
>> a num?(_)
if (== b 'HIGH')
	>> a 10
if (== b 'LOW')
	>> a 4
```

# As a type

The `_` type is a special type. It denotes a thing that should not be validated and
can not be used, only passed around.

One use for this is as type alias for a foreign object, as it can be passed around and
then used by `ffi` functions:

```
.HTMLElement _

ffi getElement(id str)dom:HTMLElement >>>
	return document.getElementById(id)
<<<

ffi setText(element dom:HTMLElement text str) >>>
	element.textContent = text
<<<

@onload()_
	>> label dom:getElement(id 'my-label')
	do dom:setText(element label text 'This is my label')

```
