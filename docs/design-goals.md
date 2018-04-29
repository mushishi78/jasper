# Design Goals

* fast compilation
  - single pass
  - not written in itself, not a compiler language
  - incremental
  - cached with file hashes
* small feature set
  - can fit in head
  - be understood by beginers
  - easy to write tooling
* fixed version 1
  - no churn
* built for platform
  - use named constructors that show in memory profiles
  - ensure break points can be put at arbitrary points
  - readable output should no source maps be available
  - allow direct transparent access through console
  - set properties in consistent order
* first class ffi to js
  - drop down to javascript to break safety
* implicit folder mapped modules
  - deal with namespace conflicts transparently
  - avoid excessive import boiler plate
  - include all 3rd party code directly in project
  - import tool that prompts to rename or replace
  - imports tests too, run with packages in project
* run time types
  - type based reflection/logical branching
  - transparent implementation
  - run time type checks
* minimize personal syntax preference
  - avoid time wrestling with how to write things
  - avoid code review disputes
* only types, functions, singletons at root level
  - encourages explicit runtime order
* _ is the void. `undefined`, `never`, unused parameters
* public and serializable ast to encourage tooling
