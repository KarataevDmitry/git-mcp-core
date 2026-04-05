# GitMcp.Core

Shared construction of `git` CLI argument lists for [**git-mcp**](https://github.com/KarataevDmitry/git-mcp) and **Cascade IDE** (see ADR 0019 in the cascade-ide repo).

## Layout

- Target: **.NET 10**, **C# 14**.
- No dependency on MCP SDK or Avalonia — only argv shapes and validation messages (`GitArgsResult`).

## Consumers

Add a **project reference** to `GitMcp.Core.csproj`, or clone this repo **next to** git-mcp / IDE (e.g. as a **git submodule** in a meta-repo).

## Build

```bash
dotnet build
```

## Tests

Unit tests for `GitCommandBuilder` live in the **git-mcp** repository (`GitMcp.Tests`).
