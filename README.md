# Unity UPM Package template
This repository provide a template to develop a UPM package for Unity.

The purpose is to speed-up the setup, the development, and the testing of a new
UPM package, providing a framework that solves many issues that could hinder the
efficiency of the development.

This template was designed to build packages for systems that provide pure logic
to Unity, but without using its elements (e.g. MonoBehavior, Components).
E.g. A system to generate a map based on a seeds, a system to compute the price
variation of a merchant's items.

## Features
There are two features that this repository aims to achieve:
- Independence from Unity during the development
    - The code can be developed without Unity
    - The code can be tested without Unity
- Full compatibility with Unity
    - The code can be imported in Unity as a UPM Package

The independence from Unity means that it is not required to have Unity open or
even to have Unity at all. All the development should focus on the logic that is
being developed.

The compatibility with Unity is obtained by having:
- Clear and standard folder and file structure
- Tests implemented with NUit, same as Unity
- CS Proj file that is set as Unity
- Assembly files, that specify how the files should be compiled and used in
    Unity
- GitHub action that build a clean package in a specific branch

## Limitation
The limitation of this template are:
- It is not possible to use Unity classes
- Runtime tests in unity are not available

## How does it work
Before starting, let's assume that we are developing a system called
"SampleSystem" and that we are going to build tests and write documentation for
it. Now, let's analyse every file and folder to understand what's their role.

| Element | Function |
| ------- | -------- |
| /Documentation | Contains the documentation, written in markdown |
| /Editor | Contains the software of SampleSystem. All the software belongs to SampleSystem namespace. |
| /Editor/SampleSystem.asmdef | Unity Assembly Definition file, just specify name and namespace of the software. |
| /Test/Editor | Contains the tests for SampleSystem. All the software belongs to SampleSystem.Test namespace. |
| /Test/Editor/SampleSystem.Test.asmdef | Unity Assembly Definition file, states that this folder contains tests and tells Unity how to include them in Test Runner |
| SampleSystem.csproj | Defines the dotnet configuration and the tests libraries |
| package.json | Specifies the UPM package information |
| CHANGELOG.md | Contains the changes between the various versions of the software |
| README.md | Contains the information on the package |
| .upmignore | Contains the list of files that should not appear in the upm package |

The "main" branch contains more files than the ones needed by the UPM package.
To clean the repository, a GitHub action push all the changes made in "main" to
a new branch "upm" filtering out the files that match an excluding pattern in
".upmignore".

## Getting started
To instantiate the framework, there are several spots that need to be changed.
Many of those spots can be changed with find-replace on the placeholder names.

The placeholder used are the following:
| Placeholder | Description |
| ----------- | ----------- |
| SampleSystem | The name of the system implemented |
| johndoe.mycompany.sample-system | The name of the package |
| Sample System | Name of the system shown in Unity |
| Description placeholder | Description of the system shown in Unity |

The spots to change:
- /Editor/SampleSystem.asmdef
  - Rename file
  - Change name
  - Change rootNamespace
- /Test/Editor/SampleSystem.Test.asmdef
  - Rename file
  - Change name
  - Change rootNamespace
  - Change reference
- /package.json
  - Change name
  - Change description
  - Change displayName
  - Change author.name
  - Change author.email
- /SampleSystem.csproj
  - Rename file
- /README.md
  - Change content

## Maintenance
The project is maintained by me, feel free to reach out for a feedback or just
to let me know if this was useful to you and saved you some time.
