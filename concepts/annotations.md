---
layout: default
title: Annotations
parent: Concepts
---
# Annotations

Annotations are a reflection tool that allows you to mark a class with metadata that can be queried easily by other classes.

Annotation classes must extend from `Conduit.Core.Native.Annotation`. Aside from that, there are no limitations for annotation classes. They may have any constructors, fields or methods.

Annotating a class is done with the following syntax:
```java
@AnnotationClassName(<constructorArguments...>)
public class AnnotatedClass {
    #...
}
```
In words, an annotation is formed with an at (`@`) sign, followed by a constructor call to the class, excluding the `new` keyword. The annotation must be placed before the class declaration, with no statements or comments in between (however, a class may have more than one annotation).


## Querying Annotations

The following Reflection methods are used to fetch Annotation information from classes:

```csharp
Reflection.getAnnotationForClass(definingType : type_definition) : Conduit.Core.Native.Annotation?
```

