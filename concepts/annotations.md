---
layout: default
title: Annotations
parent: Concepts
---
# Annotations

Annotations are a reflection tool that allows you to mark a class with metadata that can be queried easily by other classes.

Annotation classes must extend from `Conduit.Core.Native.Annotation`. Aside from that, there are no limitations for annotation classes. They may have any constructors, fields or methods.

Annotating a class is done with the following syntax:
```csharp
@AnnotationClassName(<constructorArguments...>)
public class AnnotatedClass {
    #...
}
```
In words, an annotation is formed with an at (`@`) sign, followed by a constructor call to the class, excluding the `new` keyword. The annotation must be placed before the class declaration, with no statements or comments in between (however, a class may have more than one annotation).


## Querying Annotations

The following Reflection methods are used to fetch Annotation information from classes:


> **Reflection.getAnnotationForClass**

> Signature: `Reflection.getAnnotationForClass(definingType : type_definition, annotationType : type_definition) : Conduit.Core.Native.Annotation?`

> Retrieves the annotation of the given `annotationType` annotation class, attached to the given `definingType` class. If the defining type has no annotation of the specified type, returns null. If the defining type has one or more annotations of the specified type, it returns the first of that type.

> **Reflection.getAnnotationsForClass**

> Signature: `Reflection.getAnnotationsForClass(definingType : type_definition, annotationType : type_definition?) : list`

> Retrieves the annotations attached to the given `definingType` class. If the `annotationType` parameter is specified and non-null, the annotations retrieved will only be those that are subtypes of the given annotation type. The return value is in the form of a list of annotation objects, containing all of the matching annotations.

> **Reflection.getClassesAnnotatedWith**

> Signature: `Reflection.getClassesAnnotatedWith(annotationType : type_definition) : list`

> Retrieves all of the classes that are annotated with an instance of the given `annotationType`. The return value is in the form of a list of type definitions, containing all of the matching classes.
