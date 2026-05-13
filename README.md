# GitMcp.Core

Shared construction of `git` CLI argument lists for **git-mcp** and **Cascade IDE** (ADR 0019 in cascade-ide).

## Remotes (политика)

- **`origin`** — GitLab (`Krawler/git-mcp-core`), канон для разработки и субмодуля в meta-repo `open`.
- **`github`** — зеркало на GitHub: **[KarataevDmitry/git-mcp-core](https://github.com/KarataevDmitry/git-mcp-core)** (`git push github main` после согласования с GitLab). Отсюда же **Trusted Publishing** пакета `AIGuiders.GitMcp.Core` на nuget.org.

## Layout

- Target: **.NET 10**, **C# 14**.
- No dependency on MCP SDK or Avalonia — only argv shapes and validation messages (`GitArgsResult`).

## Consumers

- **NuGet (рекомендуется):** пакет [`AIGuiders.GitMcp.Core`](https://www.nuget.org/packages/AIGuiders.GitMcp.Core) — `PackageReference` в `git-mcp` и Cascade IDE; отдельный checkout исходников для сборки не нужен после публикации на nuget.org.
- **Исходники:** публичный репозиторий **[KarataevDmitry/git-mcp-core](https://github.com/KarataevDmitry/git-mcp-core)** (зеркало GitLab); `ProjectReference` на `GitMcp.Core.csproj` или субмодуль в meta-repo `open`.

## Публикация на nuget.org (Trusted Publishing)

**Полный чеклист** (пуш на GitHub, форма на nuget.org, первый запуск workflow): **[docs/nuget-trusted-publishing.md](docs/nuget-trusted-publishing.md)**.

Кратко:

1. В репозитории **https://github.com/KarataevDmitry/git-mcp-core** в ветке по умолчанию должны лежать **`.github/workflows/nuget-publish.yml`** и **`LICENSE`** (OIDC `id-token: write` в publish-workflow).

## Build

```bash
dotnet build
```

## Tests

Unit tests for `GitCommandBuilder` live in the **git-mcp** repository (`GitMcp.Tests`).
