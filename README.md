
# Unity UPM Package Template
This repository provides a template to develop a UPM package for Unity and is designed to speed up setup, development, and testing of packages that contain pure logic (no Unity-specific runtime classes). It provides a framework that solves many issues that could hinder the efficiency of the development.

![Overview](/TemplateDocumentation/img/overview.png)

## Key Features
- **Develop and test without Unity.** Write and run tests using dotnet/NUnit.
- **Full Unity compatibility.** Package structure, .asmdef files, and package.json are ready for UPM import.
- **UPM Package generation.** GitHub Action generates a clean UPM package.

## Limitations
- **No Unity classes.** The template is for logic-only code and does not support Unity-specific runtime classes (e.g., MonoBehaviour, ScriptableObject).
- **No runtime tests in Unity.** Runtime tests that require the Unity player are not provided by this template.

## Documentation
This documentation combines four types of content:

- **Tutorial**: Step-by-step guides to learn how to use this template
    - [Build a simple package - Part 1: Local](/TemplateDocumentation/tutorial/build-simple-package-1-local.md)
    - [Build a simple package - Part 2: Unity](/TemplateDocumentation/tutorial/build-simple-package-2-unity.md)
- **How To**: Guides on how to achieve specific objectives
    - wip
- **Reference**: Technical description of the software
    - [Placeholder list](/TemplateDocumentation/reference/placeholder-list.md)
    - [Package structure](/TemplateDocumentation/reference/package-structure.md)
    - [Web Resources](/TemplateDocumentation/reference/web-resources.md)
- **Explanation**: In depth explanation of specific topics
    - [Development Workflow](/TemplateDocumentation/explanation/development-workflow.md)
    - [UPM Builder Action](/TemplateDocumentation/explanation/upm-builder-action.md)
    - [Unity Test Runner](/TemplateDocumentation/explanation/unity-test-runner.md)
    - [Unity Meta Files](/TemplateDocumentation/explanation/unity-meta-files.md)

## Maintenance
The project is loosely maintained by me. Feel free to reach out on LinkedIn or just open issues.
