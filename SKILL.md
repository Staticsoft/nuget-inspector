---
name: nuget-inspector
description: Use proactively when writing C# code that depends on a NuGet package whose API is unknown or uncertain. Inspect the package before writing code to get the correct type names, method signatures, and properties — avoiding compile errors and blind guessing.
user-invocable: false
allowed-tools: Bash(nuget-inspector *)
---

When you need to use a NuGet package in C# code and you are unsure of its API, follow this procedure before writing any code.

## Step 1: Determine package ID and version

If not already known, read the relevant `.csproj` file to find the `PackageReference` for the package:

```bash
# Example: look for the package reference
grep -i "<PackageReference" path/to/Project.csproj
```

Use the `Include` value as the package ID and `Version` as the version.

## Step 2: List all public types

```bash
nuget-inspector list-types --package <package-id> --version <version>
```

Read the output to understand what CLASSES, INTERFACES, ENUMS, and STRUCTS the package exposes.

## Step 3: Describe types you intend to use

For each type you plan to use in your code, run:

```bash
nuget-inspector describe --type <FullyQualifiedTypeName> --package <package-id> --version <version>
```

The output shows CONSTRUCTORS, STATIC METHODS, INSTANCE METHODS, PROPERTIES, and enum VALUES — use this to write correct call sites.

## Step 4: Write the code

With the API surface confirmed, write the C# code using the exact signatures from the describe output. Do not guess parameter types or method names.

## If nuget-inspector is not installed

If the command is not found, install it silently:

```bash
dotnet tool install --global Staticsoft.NuGetInspector
```

Then retry.
