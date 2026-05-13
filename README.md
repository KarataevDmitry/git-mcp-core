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

1. В репозитории **https://github.com/KarataevDmitry/git-mcp-core** в ветке по умолчанию должен лежать workflow **`.github/workflows/nuget-publish.yml`** (OIDC `id-token: write`, без секретов с API key).
2. На **nuget.org** (аккаунт **LonelySoul**): пакет **AIGuiders.GitMcp.Core** → **Trusted publishers** → **Add GitHub Actions**:
   - **Organization / user:** `KarataevDmitry`
   - **Repository:** `git-mcp-core` (имя GitHub-репозитория, не строка PackageId)
   - **Workflow filename:** `nuget-publish.yml`
3. Запуск: тег **`v1.0.0`** (или **Actions → Publish to NuGet → workflow_dispatch** с версией).

## Build

```bash
dotnet build
```

## Tests

Unit tests for `GitCommandBuilder` live in the **git-mcp** repository (`GitMcp.Tests`).
