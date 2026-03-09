# Package Structure
The overall structure of files and folders follows the [Unity standard structure for a UPM package][unity-upm-structure] with the addition of some files that are required for the management of the repository, e.g. the local project setup.

The repository uses two branches, main and upm, that cover local and unity side: the main branch is used to develop and test the software for the package whereas the upm branch contains only the minimal information required by Unity for a UPM package. The content of this branch is kept aligned by a GitHub Action.

The following schema describe what the main folder and file purposes and if they are used for local development and/or for Unity.

| Path                                  | Local | Unity |              Purpose                                     |
| ------------------------------------- | ----- | ----- | -------------------------------------------------------- |
| /Documentation                        | x     | x     | Markdown docs for the package                            |
| /Editor                               | x     | x     | Package source code                                      |
| /Editor/**.cs                         | x     | x     | C# files for the source code                             |
| /Editor/SampleSystem.asmdef           |       | x     | Unity assembly definition for the package                |
| /Test/Editor                          | x     | x     | Unit tests                                               |
| /Test/Editor/**.cs                    | x     | x     | C# files for the unit tests                              |
| /Test/Editor/SampleSystem.Test.asmdef |       | x     | Test assembly definition for Unity Test Runner           |
| SampleSystem.csproj                   | x     | x     | dotnet project file for local development and tests      |
| package.json                          |       | x     | UPM package metadata                                     |
| .upmignore                            | x     |       | Files and patterns excluded when building the UPM branch |
