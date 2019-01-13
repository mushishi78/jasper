# Namespaces

## Implicitly named by folder

Jasper does not have explicit statements for importing and exporting modules.
Instead, every root level entity in a file is implicitly exported under a
namespaced derived from the name of the folder that contains the file.

For example, if there's a file named `shapes/Circle.jasp` and it contains the
following:

```
& Circle
	radius num
	x num
	y num
&

(circleArea circle shapes:Circle < num)
	< (* circle.radius circle.radius math:pi)
```

Then the type `Circle` and the function `circleArea` would be referred to as
`shapes:Circle` and `shapes:circleArea` respectively.

## Present within the namespace

Namespaces apply throughout the project, even from within the namespace. This can
be seen in the example above: The type of the `circle` parameter of the
`circleArea` function is given as `shapes:Circle`, even though it's within the
`shapes` namespace.

This makes it easier to copy code from one namespace to another without having to add the
namespaces or worse potential conflate to similarly named things in the two
namespaces.

## One level deep

Namespaces are only one level deep and everything must be in a namespace. If a file is
in the root of the project or a subfolder of a namespace folder, it will be ignored.
This is fairly restrictive to custom folder organisation, but has benefits:

* Having a consistent folder structure across projects makes it easier for new devs.
* Wide and shallow organisation hopefully leads to hubs of dunbar numbered sizes, i.e
  100 namespaces with 100 functions each is hopefully faster for the brain to recal
  than 1000 namespaces with nested-namespaces and only 10 functions each.
* Easier to write tooling if you don't need to walk down a folder structure.

## Runtime

Each namespace is present at runtime transparently. The `shapes` namespace will be attached
to the `window` object so that everything is easily available on the console and for end to
end tests. For example, in the console you could write something similar to:

```
var circle = new shapes.Circle(25, 5, 7);
var area = shapes.circleArea(circle);
```
