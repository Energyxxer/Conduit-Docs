---
layout: default
title: Getting Started
parent: Tutorials
---
# Getting Started

## Creating a Project
Create a new project via `File > New > Conduit Project`. Enter the name of the project and press Enter.

It will set you up with a project that contains:
  * A behavior pack with a `manifest.json` (w/ random UUIDs)
  * A resource pack with a `manifest.json` (w/ random UUIDs)
  * A single script that logs "Hello World"

## Setting up the Standard Library

The Conduit Standard Library for Bedrock doesn't come bundled with the language, as it is still a work-in-progress.
For now, you'll have to set it up manually using project dependencies.
There's also no built-in dialog for editing dependencies, so for now you'll also need to do it by manually editing a json file.

Go to the [Conduit Standard Library repository](https://github.com/Energyxxer/Conduit-Standard-Library) and download the code as a zip.
(or if you'd prefer, clone the repository so you can pull changes as they are made)
Extract the zip.

In Conduit-UI, expand the project you've just created and open a file called `.cdiproj` (if you don't see it, click the cog icon next to "EXPLORER" and tick "Show Project Files").
Add the following properties to the root JSON object:
```json
"dependencies": [
    {
        "path": "PATH/TO/STANDARD/LIBRARY",
        "mode": "combine"
    }
],
"stages": [
    "registry_setup",
    "utility_setup",
    "input_scan",
    "user_setup",
    "tasks",
    "validation",
    "file_generation"
]
```
Copy the path to the Standard Library you extracted/cloned and paste it inside the path string. If you're in Windows, make sure the file separators are escaped (`\` should turn into `\\`)

Double check that there are no missing/duplicated commas and save.

If you've done this right, the project should now be able to reference classes from the Standard Library.
Test this by adding `using Conduit.Entities;` on the first line of the default script. If compiling the project (default Alt+Shift+X) yields the error `Cannot resolve member 'Entities' of package`, you might have done something wrong.

