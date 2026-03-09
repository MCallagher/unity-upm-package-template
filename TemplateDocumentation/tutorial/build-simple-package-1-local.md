# Tutorial: Build a simple package - Part 1: local
In this tutorial, you will build a simple package using this Unity UPM Package Template.

You will build a custom package for a randomization library. The package MyRandom will provide a class Sampler that contains a Sample method to manage the sampling of items from a list.

This tutorial assumes:
- VSCode is installed
- Git is installed

## 1. Cloning the repository
Open a terminal from your favourite directory and clone the template repository.

You can use the following command:
```
git clone https://github.com/MCallagher/unity-upm-package-template.git
```

Then rename the folder from "unity-upm-package-template" to "my-random" and then open the folder in VSCode.

## 2. Setup VSCode environment
Add VSCode setting file to hide files and folders we are not interesting in and setup the C# project.

To do so, create a folder ".vscode" in the root folder and inside it create the file "settings.json" with this content:

```
{
    "files.exclude": {
       "**/*.meta": true,
        "bin/": true,
        "Bin/": true,
        "obj/": true,
        "Obj/": true,
    },
    "dotnet.defaultSolution": "my-random.sln"
}
```

## 3. Replace placeholders
Replace the placeholders with actual values for our packages. This process can be done mostly with a find-replace at project level while the remaining placeholders require file renaming.

### 3.1 Package namespace
Our package's namespace will be "MyRandom" so we need to replace the placeholder name "SampleSystem".

Open "replace in files" feature of VSCode (ctrl+shift+H), search for "SampleSystem" and replace with "MyRandom", finally replace all the matches.

The following results should appear:
- SampleSystem.asmdef
    - "name" definition
    - "rootNamespace" definition
- SampleSystem.Test.asmdef
    - "name" definition
    - "rootNamespace" definition
    - "reference" list
- README.md
    - TODO: REMOVE REFERENCES

Then, rename the following files:
| Location | Before | After |
| --- | --- | --- |
| /Editor | SampleSystem.asmdef | MyRandom.asmdef |
| /Test/Editor | SampleSystem.Test.asmdef | MyRandom.Test.asmdef |
| / | SampleSystem.csproj | MyRandom.csproj |

### 3.2 Package definition
Update the package definition file (package.json) with the author and the package name as follow:

| Key | Before | After |
| --- | --- | --- |
| name | johndoe.mycompany.sample-system | isaacasimov.foundation.my-random|
| description | Description placeholder | My random package |
| displayName | Sample System | My Random |
| author.name | John Doe | Isaac Asimov |
| author.email | john.doe@email.com | isaac.asimov@email.com |

## 4. Create Sampler class
In folder Editor, create the file "Sampler.cs" with this code.

```
using System;
using System.Collections.Generic;

namespace MyRandom
{
    public class Sampler
    {
        Random rng;

        public Sampler() { rng = new Random(); }
        public Sampler(int seed) { rng = new Random(seed); }

        public T Sample<T>(List<T> elements)
        {
            return elements[rng.Next(0, elements.Count)];
        }
    }
}
```

## 5. Create SamplerTest class
In folder Test/Editor, create the file "SamplerTest.cs" with this code:

```

using MyRandom;
using NUnit.Framework;
using System.Collections.Generic;

namespace MyRandom.Test
{
    public class SamplerTest
    {
        [Test]
        public void ValidExtraction()
        {
            Sampler sampler = new(0);
            List<int> elements = new List<int>() { 1, 20, 300 };
            Assert.AreEqual(300, sampler.Sample(elements));
        }
    }
}
```

## 6. Perform the test
Open the console (ctrl+J, go to Terminal) and run the test with the command:

```
dotnet test
```

It will perform the unit test we defined and print the results, that should be positive.

## 7. Clean the repository
Finally, clean the elements that still refers to the template
- Delete the "TemplateDocumentation" folder
- Delete the "unity-upm-package-template.sln" file
- Change the README.md to reflect what MyRandom package is for

A possible content for the readme:
```
# My Random - A random utility package
This package provide utility funcitons to perform random-based tasks, e.g. sampling.
```

## Conclusion
We developed a simple random utility package with unit test and we prepared it for Unity. The package now works locally and it is possible to extend it with more features and more tests.

However, before being imported in Unity, our package requires few more tweaks. You can continue with the second part of the tutorial [here](./build-simple-package-2-unity.md).

Back to [Documentation Hub](../index.md)
