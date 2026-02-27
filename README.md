
# Unity UPM Package Template
This repository provides a template to develop a UPM package for Unity and is designed to speed up setup, development, and testing of packages that contain pure logic (no Unity-specific runtime classes). It provides a framework that solves many issues that could hinder the efficiency of the development.

![Overview](/img/overview.png)

## Key Features
- **Develop and test without Unity.** Write and run tests using dotnet/NUnit.
- **Full Unity compatibility.** Package structure, .asmdef files, and package.json are ready for UPM import.
- **UPM Package generation.** GitHub Action generates a clean UPM package.

## Limitations
- **No Unity classes.** The template is for logic-only code and does not support Unity-specific runtime classes (e.g., MonoBehaviour, ScriptableObject).
- **No runtime tests in Unity.** Runtime tests that require the Unity player are not provided by this template.

## Repository Layout
Overall the layout of files and folders follows the Unity standard for a UPM package with the addition of some files that are required for the management of the repository, e.g. the local project setup.

| Path                                  | Purpose                                                  |
| ------------------------------------- | -------------------------------------------------------- |
| /Documentation                        | Markdown docs for the package                            |
| /Editor                               | Package source code (namespace: SampleSystem)            |
| /Editor/SampleSystem.asmdef           | Unity assembly definition for the package                |
| /Test/Editor                          | Unit tests (namespace: SampleSystem.Test)                |
| /Test/Editor/SampleSystem.Test.asmdef | Test assembly definition for Unity Test Runner           |
| SampleSystem.csproj                   | dotnet project file for local development and tests      |
| package.json                          | UPM package metadata                                     |
| .upmignore                            | Files and patterns excluded when building the UPM branch |

The repository uses two branches, main and upm, that cover local and unity side: the main branch is used to develop and test the software for the package whereas the upm branch contains only the minimal information required by Unity for a UPM package. The content of these branch is kept aligned by a GitHub Action.

![How it works](/img/howitworks.png)

## Placeholders
The template contains several placeholders that are used consistently to simplify their replacements with the real values required to instantiate a new package. The placeholder list with their meaning is shown in the following table.

| Placeholder                     | Meaning                                                  |
| ------------------------------- | -------------------------------------------------------- |
| SampleSystem                    | Package code and assembly name                           |
| johndoe.mycompany.sample-system | UPM package name (keep this placeholder in the template) |
| John Doe                        | Author name shown in Unity                               |
| john.doe@email.com              | Author email shown in Unity                              |
| Sample System                   | Display name shown in Unity                              |
| Description placeholder         | Short package description shown in Unity                 |

The placeholders appears both in file content and in file names; so the replace can mostly be done with a case sensitive find-replace at project level plus renaming few files. To provide a double check, all the spots that use a placeholder are shown in the following table.

| File                                  | Changes                                                          |
| ------------------------------------- | ---------------------------------------------------------------- |
| /Editor/SampleSystem.asmdef           | rename file; update name and rootNamespace                       |
| /Test/Editor/SampleSystem.Test.asmdef | rename file; update name, rootNamespace, and references          |
| /package.json                         | update name, displayName, description, author.name, author.email |
| /SampleSystem.csproj                  | rename file                                                      |
| /README.md                            | update content to describe your package                          |

## Quickstart
The overall workflow has just three phases: setup the template, develop locally, bring the package to Unity. But for clarity, all the required steps are explicitly described.

1. Clone the template
2. Replace placeholders listed above
3. Develop the software
4. Develop the unit tests
5. Run and debug tests locally
    - You may use the ```dotnet test```
6. Push the changes to main
    - This step triggers the GitHub Action
7. Generate the package on upm branch with the GitHub Action
    - The GITHUB_TOKEN must have the read and write permission on the repo
8. Import package into Unity
    - Use the Asset Manager to load the package
9. Make tests visible in Unity
    - Add the package to dependencies and testables in "MyUnityProject/Packages/manifest.json"
10. Run the test in Unity
    - The test can be run in the Test Runner in the Editor section

![Workflow suggested](/img/workflow.png)

## Annex
The section that follows present in deeper detail some of the topics presented above.

### Unity compatibility
The Unity compatibility is granted by several design choices:
- Clear and standard folder and file structure
- Tests implemented with NUit, same as Unity
- CS Proj file is set as Unity
- Use of Unity Assembly Definition files, that specify how the files should be compiled and used in Unity
- GitHub action that build a clean package in a specific branch

### UPM package builder - GitHub Action
The repository includes a GitHub Actions workflow (.github/workflows/sync-upm.yml) that runs automatically on every push to the main branch and creates a clean UPM-ready copy of the package on the upm branch. The job checks out the main branch, filters out files and folders that match the patterns listed in .upmignore (removing editor settings, build artifacts, CI files, etc.), assembles the remaining package tree, and then commits and pushes those changes to upm using the GITHUB_TOKEN.

To allow the workflow to push the cleaned package you must enable Actions read and write permissions for the GITHUB_TOKEN in the repository settings: Setting/Action/General/Workflow permissions.

### Unity Test Runner
The display of tests in Unity is a delicate subject and there are several requirements that must be met to have them appear in the Test Runner. In general, the tests appears in the Test Runner only if there is an associate asmdef file that contains reference to TestAssemblies, includes only the Editor platform, and references the NUnit library. The asmdef file is already setup correctly but it may be needed to explicitly tell Unity that our package is testable. To do so, you must modify the "MyUnityProject/Packages/manifest.json" file in your Unity project and add one entity to the testable list of packages:
```
{
    "dependencies": {
        ...
        "johndoe.mycompany.sample-system": "3.0.0",
        ...
    },
    "testables": ["johndoe.mycompany.sample-system"]
}
```

## Maintenance
The project is maintained by me. Feel free to reach out on LinkedIn or just open issues.

## References
Unity Documentation
- [UPM structure](https://docs.unity3d.com/6000.3/Documentation/Manual/cus-layout.html)
- [UPM add tests](https://docs.unity3d.com/6000.3/Documentation/Manual/cus-tests.html)
- [UPM tests on Test Runner](https://discussions.unity.com/t/test-runner-not-showing-any-of-my-tests/729955/10)
