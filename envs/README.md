# 多环境 GitOps 模拟（test → dev → main）

## 分支与环境对应

| 动作 | 触发的「流水线」 | 部署到 |
|------|------------------|--------|
| `test` 合并进 `dev` | CI 构建 + 更新 `envs/dev` | 开发环境 namespace `dev` |
| `dev` 合并进 `main` | CI 构建 + 更新 `envs/prod` | 生产环境 namespace `prod` |

说明：本机用脚本模拟「合并后触发」；真实场景里改成 GitHub Actions 的 `on: push: branches: [dev]` / `[main]`。

## 目录

- `envs/dev/go-demo`  ← Argo 应用 go-demo-dev 盯着这里
- `envs/prod/go-demo` ← Argo 应用 go-demo-prod 盯着这里

清单仓库始终推到 `main`（GitOps 常见做法：环境差异用路径/目录，而不是用分支存清单）。