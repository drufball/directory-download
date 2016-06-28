# Problem
Currently, sites can only download single files. This restriction hinders several use cases, including:

- Downloading folders attached to emails
- Working with web file managers such as DropBox, Google Drive, and OneDrive
- Downloading applications
- Etc.

Downloading directories is a common use case on the web. Today sites approximate the behavior by generating .zip files of the directory they wish to download. Not only does this require extra infrastructure from sites, it leads to extra steps and leftover .zip files on the users computer.

This proposal suggests a web platform API to enable directory download. More details can be found in the [EXPLAINER](EXPLAINER.md).
