# UPM Builder Action
The repository includes a GitHub Actions workflow (.github/workflows/sync-upm.yml) that runs automatically on every push to the main branch and creates a clean UPM-ready copy of the package on the upm branch. The job checks out the main branch, filters out files and folders that match the patterns listed in .upmignore (removing editor settings, build artifacts, CI files, etc.), assembles the remaining package tree, and then commits and pushes those changes to upm using the default GitHub bot authenticated with the GITHUB_TOKEN.

To allow the workflow to push the cleaned package you must enable read and write [permissions for the GITHUB_TOKEN][github-token-permission] in the repository settings.

Back to [Documentation Hub](../index.md)


[github-token-permission]: https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository#setting-the-permissions-of-the-github_token-for-your-repository "GitHub Docs - Repository token permissions"
