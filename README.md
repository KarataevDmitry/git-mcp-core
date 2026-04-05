# GitMcp.Core

Shared construction of `git` CLI argument lists for **git-mcp** and **Cascade IDE** (ADR 0019 in cascade-ide).

## Remotes (политика)

- **`origin`** — GitLab (`Krawler/git-mcp-core`), канон для разработки и субмодуля в meta-repo `open`.
- **`github`** — зеркало на GitHub (публичная копия; `git push github main` после согласования с GitLab).

## Layout

- Target: **.NET 10**, **C# 14**.
- No dependency on MCP SDK or Avalonia — only argv shapes and validation messages (`GitArgsResult`).

## Consumers

Add a **project reference** to `GitMcp.Core.csproj`, or use this repo as a **git submodule** next to git-mcp / IDE (as in `open`).

## Build

```bash
dotnet build
```

## Tests

Unit tests for `GitCommandBuilder` live in the **git-mcp** repository (`GitMcp.Tests`).
