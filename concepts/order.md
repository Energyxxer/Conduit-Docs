---
layout: default
title: Stages & Evaluation Order
nav_order: 1
parent: Concepts
---
# Stages & Evaluation Order

In typical programming languages, programs have a single entry point, which is the function that is evaluated first; this file will usually reference and load other files as they are needed.
In Conduit, all files are entry points, meaning every file will be evaluated on compilation.
This is useful because Bedrock map projects typically have numerous components that aren't necessarily connected to one another; for instance, a music system and passive mob AI.
However, a need to specify an order in which files are evaluated arise when a system needs to operate on the results of many other files. This is what file stages are for.

## Stages

Stages are "tags" given to files. The project configuration defines these tags and gives them an order in relation to each other.
For example, you might use an `entity_definition` stage to define all your custom entities and a `file_generation` stage to turn all of the defined entities into JSON files.

Stages are defined via the `.cdiproj` file, as "stages": an array of strings.
Here's an example, using the stages required by the Standard Library:

```json
{
    "stages": [
        "input_scan",
        "user_setup",
        "validation",
        "file_generation"
    ]
}
```
This means that input_scan will run first, and file_generation will run last.

Conduit script files can be assigned stages by using the `stage` file directive. Example:
```
stage user_setup;
```
This will make its file's statements run after the Standard Library has scanned the input directories, but before the Standard Library does any validation on your project's generated data.

**INFO**: File directives are statements that can only be placed at the beginning of Conduit script files, such as `stage` and `using`
{: .fs-3 .ls-15 .code-example }

## Classes

Classes are outliers in the way they are evaluated by Conduit.
Classes are defined by name when the project starts evaluation - before any statements are executed - but their bodies aren't evaluated until the class itself is *accessed* by an outside statement, such as a constructor of static field/method access.
Because of this, you do not need to ensure that a class gets defined at an earlier stage than the statements that use it - classes can be accessed at all times of the project execution.
This also means that classes are very lightweight, and that unused classes don't incur a significant performance penalty. This is how the Standard Library has hundreds of classes for Entity Components - not all need to be evaluated unless the project uses them.
