# Tutorial: Build a simple package - Part 1: local
In this tutorial, you will build a simple package using this Unity UPM Package Template. This first part cover the local development.

You will build a custom package for a randomization library. The package MyRandom will provide a class Sampler that contains a Sample method to manage the sampling of items from a list.

This tutorial assumes:
- A GitHub account
- VSCode is installed
- Git is installed
- Dotnet is installed

## 1. Create a GitHub repository
Create a new repository on GitHub following this link: [GitHub/new](https://github.com/new). Be sure to:
- Name the repository "my-random"
- Set the repository public
- Don't add a README
- Don't add a .gitignore
- Don't add a license

## 2. Setup the repository locally
Open a terminal in a folder of your choice and clone the repository just created.

You can use the following command (replacing the user):
```
git clone https://github.com/<user>/my-random.git
```

## 3. Download latest template release
Go to [unity-upm-package-template](https://github.com/MCallagher/unity-upm-package-template) and download the latest release of the package in zip format. Unzip the package and move the content in the folder "my-random" that contains the repository.

Delete the folder "TemplateDocumentation" and replace the content of the "README.md" file with:

```
# My Random - A random utility package
This package provide utility funcitons to perform random-based tasks, e.g. sampling.
```

## 4. Setup VSCode environment
Open the folder in VSCode and add a VSCode setting file to hide files and folders we are not interesting in and setup the C# project.

To do so, create a folder ".vscode" in the root folder and inside it create the file "settings.json" with this content:

```
{
    "files.exclude": {
       "**/*.meta": true,
        "bin/": true,
        "Bin/": true,
        "obj/": true,
        "Obj/": true,
    }
}
```

## 4. Replace the placeholders
Replace the placeholders with actual values for our packages. This process can be done mostly with a find-replace at project level while the remaining placeholders require file renaming.

### 4.1 Package namespace
Our package's namespace will be "MyRandom" so we need to replace the placeholder name "SampleSystem".

To replace the appearances in content, open "replace in files" feature of VSCode (ctrl+shift+H), search for "SampleSystem" and replace with "MyRandom", finally replace all the matches:

| File | Appearances |
| --- | --- |
| SampleSystem.asmdef | "name" definition, "rootNamespace" definition |
| SampleSystem.Test.asmdef | "name" definition, "rootNamespace" definition, "reference" list |

Then, rename the files that contains the namespace in the filename:

| Location | Before | After |
| --- | --- | --- |
| /Editor | SampleSystem.asmdef | MyRandom.asmdef |
| /Test/Editor | SampleSystem.Test.asmdef | MyRandom.Test.asmdef |
| / | SampleSystem.csproj | MyRandom.csproj |

### 4.2 Package definition
Update the package definition file (package.json) with the author and the package name as follow:

| Key | Before | After |
| --- | --- | --- |
| name | johndoe.mycompany.sample-system | isaacasimov.foundation.my-random |
| description | Description placeholder | My random package |
| displayName | Sample System | My Random |
| author.name | John Doe | Isaac Asimov |
| author.email | john.doe@email.com | isaac.asimov@email.com |

## 5. Create Sampler class
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

## 6. Create SamplerTest class
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

## Conclusion
We developed a simple random utility package with unit test and we prepared it for Unity. The package now works locally and it is possible to extend it with more features and more tests.

However, before being imported in Unity, our package requires few more tweaks. You can continue with the second part of the tutorial [here](./build-simple-package-2-unity.md).

Back to [Documentation Hub](../index.md)
