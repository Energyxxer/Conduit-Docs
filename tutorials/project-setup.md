---
layout: default
title: Project Setup
parent: Tutorials
---
# Project Setup

## Creating a Project
Create a new project via `File > New > Conduit Project`. Enter the name of the project and press Enter.

It will set you up with a project that contains:
  * A behavior pack with a `manifest.json` (w/ random UUIDs)
  * A resource pack with a `manifest.json` (w/ random UUIDs)
  * A single script that logs "Hello World"

At the moment, there is no built-in dialog for editing project settings, so for now it'll have to be done by editing special json files `.cdiproj` and `.cdibuild` inside the project directory. If you don't see them, click the cog icon next to **EXPLORER** and tick "Show Project Files"

# Setting an output directory

Open up `.cdibuild` inside the project directory.
Inside `output>directories` are two string properties: one for the output of the behavior pack, and another for the output of the resource pack.
Change these to wherever you want the output packs to be, such as the world's behavior_packs and resource_packs folder.
Example:
`C:\\Users\\PC\\AppData\\Local\\Packages\\Microsoft.MinecraftUWP_8wekyb3d8bbwe\\LocalState\\games\\com.mojang\\minecraftWorlds\\Project TEST\\behavior_packs\\testBP`

NOTE
{: .label .label-blue }
Windows file paths use `\` as the separator, which also happens to be the escape character in JSON. Make sure to either escape the separators (turning `\` into `\\`), or replace them with `/`, which do not need to be escaped.

## Setting up the Standard Library

The Conduit Standard Library for Bedrock doesn't come bundled with the language, as it is still a work-in-progress.
For now, you'll have to set it up manually using project dependencies.
There's also no built-in dialog for editing dependencies, so for now you'll also need to do it by manually editing a json file.

Go to the [Conduit Standard Library repository](https://github.com/Energyxxer/Conduit-Standard-Library) and download the code as a zip.
(or if you'd prefer, clone the repository so you can pull changes as they are made)
Extract the zip.

Open the file called `.cdiproj` inside the project directory and add the following properties to the root JSON object:
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
Copy the path to the Standard Library you extracted/cloned and paste it inside the path string. Make sure to escape any characters such as `\` in Windows paths.

Double check that there are no missing/duplicated commas and save.

If you've done this right, the project should now be able to reference classes from the Standard Library.
Test this by adding `using Conduit.Entities;` on the first line of the default script. If compiling the project (default Alt+Shift+X) yields the error `Cannot resolve member 'Entities' of package`, you might have done something wrong.

