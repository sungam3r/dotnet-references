# dotnet-fix-references

![Nuget](https://img.shields.io/nuget/dt/dotnet-fix-references)

A dotnet global tool that aids with bulk solution and project file references changes.

> dotnet tool install --global dotnet-fix-references --version 0.0.9

Supports the following modes which have varying use cases.

# How to use it

## Mode 1: Directory-first
By passing a root directory, the tool will assume that the current directory structure is the source of truth and will fix all project references inside all .sln and .csproj files to the correct relative path.

> dotnet fix-references ./src

Use cases:
1. You have moved your source code into a new folder structure (via a script or otherwise) and don't want to manually updates all your project references in .sln and .csproj files. (Project file names must be the same).

## Mode 2: File-first
By passing a .sln or .csproj file, the tool will assume the entry point Fix locations of .csproj files by providing a .sln (or .csproj file, coming soon) entry point (assumes the project references in the files are correct, a.k.a. file-first)

> dotnet fix-references Company.Project.sln . true

Use cases:
1. Overcoming Dockerfile COPY globbing limitations... See [here](docs/Dockerfile-use-case.md).

## Mode 3: PackageReference --> ProjectReference
Coming soon...

Use cases:
1. You've consolidated separate projects (and packages) into a mono repo and want to swap all package references to local project references where possible.

## Mode 4: ProjectReference --> PackageReference
Will do if there's interest or I have a need. (Bit more complicated than 3 as you'd be searching package sources rather than local file system.

Use cases:
* You've split out from a 

# Word of warning
Every version until v1.0 could contain breaking changes. 

This tool updates/deletes files in-place. Backup anything you care about before running this tool. 

# Feature backlog
1. Support Mode 2 (file-first) via .csproj entry
1. Support Mode 3
1. Support changed project file names. Use would provide a mapping to be used in the processing
1. Support Mode 4
1. A rudimentary backup facility? Saving existing files where they were as .ext.bak or something like that
