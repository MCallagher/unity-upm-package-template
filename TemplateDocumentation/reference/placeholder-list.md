# Placeholder list
The list of placeholders used and their meaning is reported in the following table.

| Id  | Placeholder                     | Meaning                                                  |
| --- | ------------------------------- | -------------------------------------------------------- |
| 1   | SampleSystem                    | Package code and assembly name                           |
| 2   | johndoe.mycompany.sample-system | UPM package name (keep this placeholder in the template) |
| 3   | John Doe                        | Author name shown in Unity                               |
| 4   | john.doe@email.com              | Author email shown in Unity                              |
| 5   | Sample System                   | Display name shown in Unity                              |
| 6   | Description placeholder         | Short package description shown in Unity                 |

The list of the posistions where these placeholders are used is reported in the following table.

| File                                  | Changes                                                                                     |
| ------------------------------------- | ------------------------------------------------------------------------------------------- |
| /Editor/SampleSystem.asmdef           | filename (1), definition of name (1), rootNamespace (1)                                     |
| /Test/Editor/SampleSystem.Test.asmdef | filename (1); definition of name (1), rootNamespace (1), list element in references (1)     |
| /package.json                         | definition of name (2), author.name (3), author.email (4), displayName (5), description (6) |
| /SampleSystem.csproj                  | filename (1)                                                                                |

Back to [Documentation Hub](../index.md)
