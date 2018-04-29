# Types

Types are nominitive, exclusive, and validated at runtime.

## What they look like

```
.Circle &
	position Coordinates
	radius Length

.Coordinates &
	x num
	y num

.Length |
	meters Meters
	feet Feet

.Meters num
.Feet num
```

Here there 5 types: `Circle`, `Coordinates`, `Length`, `Meters`, and `Feet`

Each definition starts with the `.` operator, followed by their name.

Type definitions only found on the root level of a file.
They are always named, never definied in situ.

Type definition come in 3 variaties: Product, Sum and Alias

## Product

`Circle` and `Coordinates` are "Product" types.

This is denoted by the `&` operator that follows the type name.

Product types are made up of "properties": name and type pairs that when combined
form the whole type. Properties are not optional, they must all be provided.

A `Circle` must have a `position` and a `radius`.
A `Coordinates` must have an `x` and a `y`.

## Sum

`Length` type is a "Sum" types.

This is denoted by the `|` operator that follows the type name.

Sum types are made up of "options": name and type pairs which never co-exist.
One and only one option may be provided.

A `Length` must be either be made up of `meters` or `feet`, but never both.

## Alias

`Meters` and `Feet` are "Alias" types.

Alias types are denoted by following the type name with the name of the
type they alias. In this case they are both aliases of the `num` type.

Alias types can use the operators and methods of the type they alias.
For instance, two value of type `Meters` can be multiplied together like
`num` types.

However, aliases are different types. If a parameter accepts a value in
`Meters`, you can not pass in a value in `Feet` even though the are both
aliases of the `num` type.

## Runtime

Type definitions are transpiled to JavaScript as constructor functions.
This can be helpful in some browser tooling, such at looking memory profiles.

The constructors contain type checks to ensure the runtime type is what we
expect. Any invalid runtime types will result in a runtime error being thrown.

All types are also give a `jasperType` property with the name of the type
assigned. This can help when serializing to JSON so that the intended type is
still present.

So the Javascript for the `Coordinates` type definition would look something
similar to this.

```JavaScript
function Coordinates(x, y) {
	if (x !== undefined && typeof x !== 'number') {
		throw new Error('Expected x property to be a number');
	}
	if (y !== undefined && typeof y !== 'number') {
		throw new Error('Expected y property to be a number');
	}
	this.jasperType = 'Coordinates';
	this.x = x;
	this.y = y;
}
```
