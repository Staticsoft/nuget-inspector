# nuget-inspector Claude Code Skill

A Claude Code skill that teaches Claude to inspect NuGet package APIs before writing C# code — avoiding compile errors caused by guessed method signatures or missing types.

## What it does

When Claude is about to write C# code that uses a NuGet package, this skill triggers automatically and instructs Claude to:

1. Identify the package ID and version from the `.csproj` file
2. Run `nuget-inspector list-types` to discover all public types
3. Run `nuget-inspector describe` on each type it intends to use
4. Write code using the confirmed signatures — no guessing

## Requirements

The [`Staticsoft.NuGetInspector`](https://www.nuget.org/packages/Staticsoft.NuGetInspector) .NET global tool must be installed on the machine where Claude Code runs:

```bash
dotnet tool install --global Staticsoft.NuGetInspector
```

## Installation

Add this skill as a git submodule inside your repository's `.claude/skills/` directory:

```bash
git submodule add <repo-url> .claude/skills/nuget-inspector
```

Claude Code automatically discovers skills placed under `.claude/skills/`. No additional configuration is needed.

## Skill behaviour

- **Not user-invocable** — does not appear in the `/` autocomplete menu; Claude invokes it autonomously.
- **Auto-allowed tool:** `nuget-inspector *` commands run without a permission prompt. Other commands (e.g. `dotnet tool install`) still prompt as usual.
