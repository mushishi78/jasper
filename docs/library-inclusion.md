# Library inclusion

A more contraversial aspect of Japser is the unconventional treatment of third party libraries.
Traditionally this code is kept out of the application repository and then later linked into the
application at build time. Typically a dependency manager will have a config file to keep track of
version numbers of dependencies in order to be able to recreate a build.

However, with Jasper the source code is included directly into the application code. This has some
benefits and some drawbacks.

## Benefits

Compile time checks will apply to the whole application, this means that any mismatched contracts
between library boundaries will become obvious through typical compilation errors.

Library tests can be included and run along with the rest of the application. If libraries aren't
mocked out, running these test can ensure the compatibility of the various versions of libraries.

When switching between repository branches with different versions of libraries, a package manager
doesn't also need to be run to install the correct version.

Library updates will be visible in commit diffs, giving a chance for code-review to catch problems.

Modifications can be made to the library that are specific to the application. When updated, conflicts
can be dealt with using typical source control methods.

## Drawbacks

Conflicting names must be wrangled with. However tooling can be used to re-name a library with in a
namespace.

Differing versions must be wrangled with. However, using compile time checks and automated tests will
more reliably establish whether a version is suitable for both consumers.
