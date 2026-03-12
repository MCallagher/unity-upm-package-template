# Unity Test Runner
The display of tests in Unity is a delicate subject and there are several requirements that must be met to have them [appear in the Test Runner][unity-upm-test]. In general, the tests appears in the Test Runner only if there is an associate asmdef file that contains reference to TestAssemblies, includes only the Editor platform, and references the NUnit library.

The asmdef file is already setup correctly by the template but it may be needed to [explicitly tell Unity that our package is testable][unity-upm-test-runner]. To do so, you must modify the Unity project manifest file and add one entity to the list of testable packages.

[unity-upm-test]: https://docs.unity3d.com/6000.3/Documentation/Manual/cus-tests.html "Unity Manual - UPM package tests"
[unity-upm-test-runner]: https://discussions.unity.com/t/test-runner-not-showing-any-of-my-tests/729955/10 "Unity Community - UPM test on Test Runner"