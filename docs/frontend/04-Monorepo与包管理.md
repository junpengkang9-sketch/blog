# Monorepo 与包管理

## 先区分三个层级

### 1. Package Manager
解决依赖安装和 package 管理。

主要工具：pnpm、npm、Yarn。

### 2. Workspace / Monorepo
多个项目或 package 放在一个 repository 中，共享依赖和代码。

### 3. Task Orchestration
解决依赖图、任务调度、缓存、affected build。

主要工具：Turborepo、Nx。

## pnpm
- 官网：https://pnpm.io/
- Workspaces：https://pnpm.io/workspaces
- GitHub：https://github.com/pnpm/pnpm

建议作为前端 Monorepo 的基础层。重点理解 workspace、workspace protocol、catalog、依赖链接。

## Turborepo
- 官网：https://turbo.build/repo
- 文档：https://turbo.build/repo/docs
- GitHub：https://github.com/vercel/turborepo

核心能力：Task Graph、缓存、并行执行、Remote Cache、按依赖关系执行任务。

## Nx
- 官网：https://nx.dev/
- What is a Monorepo：https://nx.dev/docs/kb/what-is-a-monorepo
- GitHub：https://github.com/nrwl/nx

相比简单 workspace，Nx 更强调 Project Graph、任务编排、缓存、affected detection 和大型仓库治理。

## Changesets
- 官网：https://changesets.dev/
- Getting Started：https://changesets.dev/guide/getting-started
- GitHub：https://github.com/changesets/changesets

解决：多个 package 的版本变更、Changelog 和 npm 发布。

## 一个常见误区

pnpm workspace ≠ 完整 Monorepo 平台。

更准确的分工：

- pnpm workspace：依赖与 workspace
- Turborepo / Nx：任务图、缓存、增量构建
- Changesets：版本、Changelog、Publish

## 什么时候需要 Monorepo

适合：
- 多个相关应用共享组件或 SDK
- 前端 + BFF / 工具包协作
- 需要统一重构、统一测试、统一发布流程

不适合：
- 项目之间几乎没有共享
- 团队边界要求完全独立权限
- 单仓库只会增加 CI 和权限复杂度

## 简单选型

一个应用 → 普通仓库即可

多个相关应用 / package → pnpm workspace

大型团队 / 大量 package / 强缓存需求 → pnpm + Turborepo 或 Nx

需要发布多个 npm package → 再加 Changesets
