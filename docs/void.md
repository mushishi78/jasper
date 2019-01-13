# The Void

`_` is the "void" operator. It performs multiple functions depending on it's context.

# As a value

The void operator can be used as a value for any variable. This in the only nil value
in Jasper. Whilst JavaScript has both `undefined` and `null`, `_` will always be
translated to the former and semantically covers both cases.

Here is an example where the default value returned is `_`, if none of the earlier
conditions match:

```
(numberToString n num < str)
	? [= n 1]
		< 'One'
	? [= n 2]
		< 'Two'
	< _
```

# As a type

The `_` type is a special type. It denotes a thing that should not be validated and
can not be used, only passed around.

One use for this is as type alias for a foreign object, as it can be passed around and
then used by ffi functions:

```
+ HTMLElement _

function (getElement id str < dom:HTMLElement)
	return document.getElementById(id);;

function (setText element dom:HTMLElement text str)
	element.textContent = text;;

(onload)
	= label (dom:getElement id 'my-label')
	. (dom:setText element label text 'This is my label')
```
