# Публикация `AIGuiders.GitMcp.Core` на nuget.org (Trusted Publishing)

Официальное описание политики GitHub Actions: [Trusted Publishing on nuget.org — GitHub Actions setup](https://learn.microsoft.com/nuget/nuget-org/trusted-publishing#github-actions-setup).

## 1. Код и workflows на GitHub

Репозиторий: **https://github.com/KarataevDmitry/git-mcp-core**

В ветке **`main`** должны быть (после пуша из этого клона):

- `GitMcp.Core.csproj`, исходники `.cs`
- **`LICENSE`**
- **`.github/workflows/nuget-publish.yml`** — публикация (OIDC, `id-token: write`)
- **`.github/workflows/ci.yml`** — проверочная сборка

Если remote `github` ещё не настроен:

```bash
git remote add github https://github.com/KarataevDmitry/git-mcp-core.git
# или SSH: git@github.com:KarataevDmitry/git-mcp-core.git
git push -u github main
```

Если на GitHub уже есть коммиты без workflows — сделай merge/rebase так, чтобы на `main` оказались файлы из `.github/workflows/`.

## 2. Политика на nuget.org

1. Войти на **nuget.org** под учёткой, которой владеет пакет (у тебя — **LonelySoul** / связанный Microsoft account).
2. **Account settings** → **Trusted Publishing** (если пункта нет — фича ещё не включена для аккаунта, см. [обзор](https://learn.microsoft.com/nuget/nuget-org/trusted-publishing)).
3. **Add a new trusted publishing policy** (владелец политики — тот же пользователь/орг, что и владелец пакета **`AIGuiders.GitMcp.Core`**).
4. Заполнить поля (имена как в форме NuGet; **только имя файла** workflow, без пути):

| Поле | Значение |
|------|-----------|
| Repository owner | `KarataevDmitry` |
| Repository name | `git-mcp-core` |
| Workflow name | `nuget-publish.yml` |
| Environment (optional) | пусто (в workflow нет `environment:`) |

5. Сохранить политику. Для **публичного** репозитория политика обычно активна сразу; для приватного возможен «пробный» период до первого успешного publish (см. доку Microsoft).

## 3. Первый push пакета

1. На GitHub: **Actions** → **Publish to NuGet** → **Run workflow** → ввести **`package_version`**, например `1.0.0` → **Run workflow**.  
   Либо создать и запушить тег: `git tag v1.0.0 && git push github v1.0.0`.
2. Дождаться зелёного job: `dotnet pack` → `NuGet/login` → `dotnet nuget push`.
3. Проверить: [nuget.org/packages/AIGuiders.GitMcp.Core](https://www.nuget.org/packages/AIGuiders.GitMcp.Core).

Ошибки вроде «policy mismatch» — перепроверь **точное** имя workflow в форме (`nuget-publish.yml`) и что workflow в репо лежит по пути `.github/workflows/nuget-publish.yml`.

## 4. После публикации

Потребители (`git-mcp`, Cascade IDE) с `PackageReference Include="AIGuiders.GitMcp.Core"` смогут собираться через обычный `dotnet restore` с **nuget.org** без локального checkout этого репозитория.
