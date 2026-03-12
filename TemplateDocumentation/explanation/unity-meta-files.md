### Unity Meta files
Unity associate to all the files and folders a [.meta file][unity-metadata] that stores basic information like the unique ID of the entity within Unity. The content of an UPM package is not an exception: somewhere in the development we need to create these files.

A quick way to generate all the meta files is to [import the package in Unity from a local folder][unity-upm-local] using the Package Manager. During this process Unity will automatically generate the meta files for all the elements of the package directly in the source folder.

This process requires Unity to have write permissions on the package destination, therefore trying to do the same process importing the package from git will result in an error since Unity do not have such permissions on the repository.


[unity-metadata]: https://docs.unity3d.com/2023.2/Documentation/Manual/AssetMetadata.html "Unity Manual - Asset metadata"
[unity-upm-local]: https://docs.unity3d.com/6000.3/Documentation/Manual/upm-ui-local.html "Unity Manual - Install UPM from local folder"
