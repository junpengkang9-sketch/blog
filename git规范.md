# Git 规范

## 概述

本文档规定了项目的 Git 提交信息规范，采用 **Conventional Commits** 格式，确保提交历史清晰易读、便于追溯。

> 📖 分支管理和工作流程请参考 [分支管理](/otd/version-management.html) 文档

## Commit Message 格式

### 基本结构

```
<type>(<scope>): <subject>

[可选 body]

[可选 footer]
```

**示例**:

```bash
feat(router): 新增虚拟路由插件支持动态路由

实现了基于 Vue Router 的虚拟路由插件，支持：
- 动态路由注册
- 路由守卫自动绑定
- 路由缓存管理

Closes #123
```

### 必填字段

#### Type 类型

| Type         | 说明      | 使用场景                                       |
| ------------ | --------- | ---------------------------------------------- |
| **feat**     | 新功能    | 添加新特性、新模块                             |
| **fix**      | Bug 修复  | 修复缺陷、错误                                 |
| **docs**     | 文档      | 更新文档、注释                                 |
| **style**    | 代码格式  | 格式化代码、调整缩进、优化导入等（不影响功能） |
| **refactor** | 重构      | 重构代码逻辑（不改变功能）                     |
| **perf**     | 性能优化  | 提升性能、优化算法                             |
| **test**     | 测试      | 添加/修改测试                                  |
| **chore**    | 构建/工具 | 修改配置、构建脚本、依赖管理                   |
| **revert**   | 回滚      | 回滚之前的提交                                 |

#### Scope 范围

范围应该是受影响的业务模块或功能，使用 **kebab-case**：

**业务模块示例**:

```
purchase, supplier, contract, requisition, approval, inventory
```

**功能模块示例**:

```
login, dashboard, settings, report, notification, workflow
```

**其他**:

```
config, build, ci, docs, deps
```

> 💡 Scope 应根据实际业务场景命名，上述仅为示例。建议团队内部统一约定常用的 scope 列表。

#### Subject 主题

- ✅ 使用**中文**描述
- ✅ 使用**动词开头**，现在时态（如：新增、修复、优化）
- ✅ **首字母小写**
- ✅ **不超过 50 个字符**
- ✅ **结尾不加句号**

### 可选字段

#### Body 正文

对于复杂的提交，使用多行 body 详细说明：

- 说明修改的原因和背景
- 描述具体实现的功能点
- 列出重要的技术细节

**格式**: 与 subject 之间空一行

```bash
feat(wormhole): 新增 Swagger API 自动生成功能

实现了从 Swagger 文档自动生成 API 代码的功能，包括：
- 自动解析 Swagger/OpenAPI 文档
- 生成 TypeScript 类型定义
- 生成 API 函数代码
- 自动生成 Mock 数据
- 支持 Alova 实例自动检测

该功能可大幅提高 API 接口对接效率，减少手写重复代码。
```

#### Footer 页脚

用于关联 Issue 或标记破坏性变更：

**关联 Issue**:

```bash
fix(router): 修复路由缓存失效问题

修复了在特定场景下路由缓存失效的问题。

Closes #123
Fixes #456
```

**破坏性变更** (Breaking Changes):

```bash
feat(api): 重构 API 请求接口

重构了整个 API 请求模块，采用新的 Alova 实例创建方式。

BREAKING CHANGE: createAppAlova 方法签名已更改。
旧版本: createAppAlova(baseURL, timeout)
新版本: createAppAlova({ baseURL, timeout, ...options })

迁移指南：将所有 createAppAlova 调用更新为对象参数形式。
```

## 提交示例

### ✅ 正例

```bash
# 新功能
feat(purchase): 新增采购申请单批量审批功能
feat(supplier): 实现供应商信息批量导入功能
feat(contract): 新增合同电子签章功能
feat(requisition): 新增请购单高级搜索筛选条件

# Bug 修复
fix(login): 修复登录失败后跳转错误
fix(approval): 修复审批流程状态更新失败的问题
fix(inventory): 修复库存数量显示不正确的问题
fix(notification): 修复消息通知未实时更新的问题

# 文档更新
docs(readme): 更新项目安装说明
docs(api): 补充采购单接口调用文档
docs(workflow): 完善审批流程配置说明

# 代码格式
style(supplier): 格式化供应商模块代码
style(dashboard): 调整仪表盘组件导入顺序

# 重构
refactor(approval): 重构审批流程逻辑
refactor(purchase): 优化采购单查询流程

# 性能优化
perf(dashboard): 优化仪表盘数据加载性能
perf(requisition): 减少请购单列表查询时间

# 测试
test(contract): 添加合同创建流程单元测试
test(approval): 补充审批功能测试用例

# 构建/工具
chore(vite): 更新 Vite 构建配置
chore(deps): 升级 Vue 到 3.4.0
chore(eslint): 调整 ESLint 规则配置

# 回滚
revert(approval): 回滚审批流程优化提交

回滚提交 a1b2c3d，该优化导致某些场景下审批失败。
```

### ❌ 反例

```bash
# 缺少 type
(purchase): 新增采购申请单
purchase: 新增采购申请单

# 缺少 scope
feat: 新增采购申请单
fix: 修复问题

# scope 使用大写或驼峰
feat(Purchase): 新增采购申请单
feat(purchaseOrder): 新增采购申请单

# 使用英文主题（应使用中文）
feat(purchase): add purchase order
fix(supplier): fix supplier bug

# 主题过长（超过 50 字符）
feat(purchase): 新增采购管理功能包括采购申请、采购审批、采购执行、采购统计等完整功能

# 结尾加句号
feat(purchase): 新增采购申请单。

# 主题不清晰
feat(purchase): 更新代码
fix(supplier): 修复问题
chore: 更新
```

## Git 常用操作

### 1. 查看状态和历史

```bash
# 查看当前状态
git status

# 查看提交历史（推荐）
git log --oneline --graph --decorate

# 查看某个文件的提交历史
git log --follow -- src/views/purchase/index.vue

# 按作者过滤
git log --author="张三"

# 按模块过滤
git log --grep="purchase"
```

### 2. 提交代码

```bash
# 添加所有修改的文件
git add .

# 添加指定文件
git add src/views/purchase/index.vue

# 提交代码
git commit -m "feat(purchase): 新增采购申请单列表"

# 查看提交结果
git log -1
```

### 3. 分支操作

```bash
# 查看所有分支
git branch -a

# 创建并切换到新分支
git checkout -b feature/purchase-list

# 切换分支
git checkout develop

# 删除本地分支
git branch -d feature/purchase-list
```

### 4. 同步代码

```bash
# 拉取远程最新代码
git pull origin develop

# 推送到远程
git push origin feature/purchase-list

# 第一次推送（关联远程分支）
git push -u origin feature/purchase-list
```

### 5. 暂存修改

**使用场景**: 临时切换分支但不想提交当前修改

```bash
# 暂存当前修改
git stash save "采购单开发进行中"

# 查看暂存列表
git stash list

# 恢复暂存（保留暂存记录）
git stash apply

# 恢复暂存（删除暂存记录）
git stash pop
```

### 6. 查看差异

```bash
# 查看工作区修改
git diff

# 查看已暂存的修改
git diff --cached

# 查看两个分支的差异
git diff develop feature/purchase-list
```

### 7. 撤销和回退（本地未推送）

**使用场景**: 本地修改错了或提交错了，想要撤销

```bash
# 撤销工作区的修改
git checkout -- src/views/purchase/index.vue

# 撤销暂存区的修改（保留工作区修改）
git reset HEAD src/views/purchase/index.vue

# 回退到上一个提交（保留修改）
git reset --soft HEAD^

# 回退到上一个提交（丢弃修改）
git reset --hard HEAD^

# 回退到指定提交
git reset --hard a1b2c3d
```

⚠️ **注意**: reset 会改变提交历史，只能在本地未推送时使用

### 8. 恢复误删（reflog）

**使用场景**: 误删了分支或回退过头了

```bash
# 第1步：查看所有操作记录
git reflog

# 第2步：找到想要恢复的提交，比如 d4e5f6g

# 第3步：恢复到那个提交
git reset --hard d4e5f6g

# 或者创建新分支指向那个提交
git checkout -b recovered-branch d4e5f6g
```

### 9. 合并分支（merge）

**使用场景**: 将一个分支的修改合并到当前分支

```bash
# 合并指定分支到当前分支
git merge feature/purchase-list

# 合并但不自动提交（可以先检查）
git merge feature/purchase-list --no-commit

# 放弃合并
git merge --abort
```

**示例**: 功能开发完成后，将 feature 分支合并到 develop 分支

### 10. 解决冲突

**使用场景**: 合并或拉取代码时出现冲突

```bash
# 第1步：查看冲突文件
git status

# 第2步：手动编辑冲突文件，解决冲突标记
# <<<<<<< HEAD
# 当前分支的内容
# =======
# 要合并进来的内容
# >>>>>>> feature/purchase-list

# 第3步：标记冲突已解决
git add src/views/purchase/index.vue

# 第4步：完成合并
git commit  # 如果是 merge
git rebase --continue  # 如果是 rebase
git cherry-pick --continue  # 如果是 cherry-pick
```

**提示**: 使用 VSCode 等编辑器可以更方便地解决冲突

### 11. 挑选提交（cherry-pick）

**使用场景**: 需要把某个分支的特定提交应用到当前分支

```bash
# 将某个提交应用到当前分支
git cherry-pick a1b2c3d

# 挑选多个提交
git cherry-pick a1b2c3d e4f5g6h

# 挑选提交范围（不包含 start）
git cherry-pick start..end

# 挑选时发生冲突，解决后继续
git cherry-pick --continue

# 放弃挑选
git cherry-pick --abort
```

**示例**: 在 feature 分支修复了一个 bug，现在需要把这个修复应用到 master 分支

### 12. 反向提交（revert）

**使用场景**: 已经推送到远程的提交需要撤销

```bash
# 创建一个反向提交来撤销某次提交（推荐，不改变历史）
git revert a1b2c3d

# 反向提交但不自动提交（可以修改提交信息）
git revert a1b2c3d --no-commit

# 撤销合并提交
git revert -m 1 a1b2c3d  # -m 1 表示保留第一个父节点
```

**示例**: 某个功能提交后发现有问题，但已经推送到远程，使用 revert 创建一个新提交来撤销

### 13. 标签管理

**使用场景**: 版本发布时打标签，方便版本管理

```bash
# 查看所有标签
git tag

# 创建标签
git tag v1.0.0

# 创建带说明的标签
git tag -a v1.0.0 -m "发布 1.0.0 版本"

# 给指定提交打标签
git tag v1.0.0 a1b2c3d

# 推送标签到远程
git push origin v1.0.0

# 推送所有标签
git push origin --tags

# 删除本地标签
git tag -d v1.0.0

# 删除远程标签
git push origin --delete v1.0.0
```

### 14. 文件修改追溯（blame）

**使用场景**: 追溯某行代码是谁写的，什么时候写的

```bash
# 查看文件每行的最后修改记录
git blame src/views/purchase/index.vue

# 查看指定行范围
git blame -L 10,20 src/views/purchase/index.vue

# 查看详细信息（显示邮箱）
git blame -e src/views/purchase/index.vue

# 配合 show 查看完整提交
git show a1b2c3d
```

**技巧**: 在 VSCode 中安装 GitLens 插件，鼠标悬停在代码行上即可看到提交信息

### 15. 清理操作

**使用场景**: 清理本地无用的分支和文件

```bash
# 查看远程已删除但本地还存在的分支
git remote prune origin --dry-run

# 删除远程已删除的本地分支
git remote prune origin

# 删除已合并的本地分支
git branch --merged | grep -v "master\|develop" | xargs git branch -d

# 清理未跟踪的文件（谨慎使用）
git clean -fd

# 查看会删除哪些文件（不实际删除）
git clean -fd --dry-run
```

**示例**: 远程分支已经删除，但本地还有很多旧分支，用 prune 清理

## 常见问题

### Q1: 如何选择合适的 type？

**原则**: 根据修改的主要内容选择：

- **新增功能** → feat
- **修复 Bug** → fix
- **更新文档** → docs
- **调整格式** → style
- **重构代码** → refactor
- **性能优化** → perf
- **测试相关** → test
- **构建/配置** → chore

**判断技巧**:

- 如果用户能感知到变化 → feat 或 fix
- 如果只是内部优化 → refactor 或 perf
- 如果只改格式不改逻辑 → style
- 如果改配置/依赖 → chore

### Q2: scope 应该写多详细？

**建议**: 使用顶层模块名即可，不要过于详细：

```bash
# ✅ 推荐
feat(purchase): 新增采购申请单审批

# ❌ 过于详细
feat(purchase/approval): 新增采购申请单审批
feat(src/views/purchase/approval): 新增采购申请单审批
```

**特殊情况**: 如果修改影响多个模块，可以选择：

```bash
# 方案 1: 使用多个 scope
feat(purchase,approval): 新增采购申请和审批功能

# 方案 2: 使用更通用的 scope
feat(system): 新增系统核心功能

# 方案 3: 省略 scope（不推荐）
feat: 新增核心功能
```

### Q3: 什么时候需要写 body？

**需要 body 的情况**:

- 复杂功能，需要说明实现细节
- 破坏性变更，需要说明迁移方法
- 重大重构，需要说明原因和影响

**不需要 body 的情况**:

- 简单的功能新增
- 明显的 Bug 修复
- 文档更新
- 代码格式调整

### Q4: 代码冲突了怎么办？

**场景**: 合并代码或拉取代码时出现冲突

```bash
# 第1步：查看冲突的文件
git status

# 第2步：手动编辑冲突文件，解决冲突标记
# <<<<<<< HEAD
# 你的修改
# =======
# 别人的修改
# >>>>>>> feature/purchase-list

# 第3步：标记冲突已解决
git add src/views/purchase/index.vue

# 第4步：继续合并
git commit  # 如果是 merge
git rebase --continue  # 如果是 rebase
git cherry-pick --continue  # 如果是 cherry-pick
```

**技巧**:
- 使用 VSCode，可以点击"接受当前更改"/"接受传入更改"快速解决
- 不确定时可以先 `git merge --abort` 取消合并，询问同事后再操作

### Q5: 如何撤销已合并的分支？

**场景**: master 由 feat-a 和 feat-b 合并而成，现在不想要 feat-a 的功能

**方法一：使用 revert（推荐，适合已推送到远程）**

```bash
# 第1步：查看合并历史
git log --oneline --graph

# 输出类似：
# d4e5f6 (HEAD -> master) Merge branch 'feat-b'
# a1b2c3 Merge branch 'feat-a'  ← 要撤销这个合并

# 第2步：撤销 feat-a 的合并提交
git revert -m 1 a1b2c3

# -m 1 的含义：
# 合并提交有两个父节点，1 是 master，2 是 feat-a
# -m 1 表示保留 master 的内容，撤销 feat-a 的内容

# 第3步：推送到远程
git push origin master
```

**方法二：使用 reset（只适合本地未推送）**

```bash
# 第1步：找到合并 feat-a 之前的提交
git log --oneline
# 找到 feat-a 合并之前的 commit hash，比如 xyz789

# 第2步：回退到那个提交
git reset --hard xyz789

# 第3步：重新合并 feat-b
git merge feat-b
```

**选择建议**:
- master 已推送到远程，团队成员在使用 → 用 **revert**
- 只在本地操作，还没推送 → 用 **reset**

### Q6: 误删了分支/提交怎么恢复？

**场景**: 不小心删除了分支或回退过头了

```bash
# 第1步：查看所有操作记录
git reflog

# 输出类似：
# a1b2c3d HEAD@{0}: reset: moving to HEAD^
# d4e5f6g HEAD@{1}: commit: feat(purchase): 新增采购单
# h7i8j9k HEAD@{2}: commit: fix(supplier): 修复供应商

# 第2步：找到想要恢复的提交，比如 d4e5f6g

# 第3步：恢复到那个提交
git reset --hard d4e5f6g

# 或者创建新分支指向那个提交
git checkout -b recovered-branch d4e5f6g
```

### Q7: 如何临时切换分支但不想提交当前修改？

**场景**: 正在开发功能，突然需要切换到别的分支修 bug，但当前代码还不想提交

**使用 stash（推荐）**

```bash
# 第1步：暂存当前修改
git stash save "采购单开发进行中"

# 第2步：切换到其他分支
git checkout hotfix/urgent-bug

# 第3步：修完 bug 后，切回原分支
git checkout feature/purchase-list

# 第4步：恢复之前的修改
git stash pop
```

### Q8: 如何挑选特定的多个提交？

**场景**: master 分支有 10 次提交，想把其中的第 1、3、5、7、9 次提交抽出来

```bash
# 第1步：查看提交历史，找到对应的 commit hash
git log --oneline master

# 假设输出：
# j10 第10次提交
# i9  第9次提交  ← 要
# h8  第8次提交
# g7  第7次提交  ← 要
# f6  第6次提交
# e5  第5次提交  ← 要
# d4  第4次提交
# c3  第3次提交  ← 要
# b2  第2次提交
# a1  第1次提交  ← 要

# 第2步：创建新分支（或切换到目标分支）
git checkout -b selected-commits

# 第3步：挑选这些提交
git cherry-pick a1 c3 e5 g7 i9
```

### Q9: merge 和 rebase 的区别？

**merge（合并）**:

```bash
git checkout develop
git merge feature/purchase-list

# 结果：保留所有提交历史，产生一个合并提交
# develop: A - B - C - M (merge commit)
#                    /
# feature:      D - E
```

**rebase（变基）**:

```bash
git checkout feature/purchase-list
git rebase develop

# 结果：将 feature 的提交"移动"到 develop 最新提交之后
# develop: A - B - C - D' - E'
```

**选择建议**:
- 公共分支（develop、master）→ 用 **merge**（保留完整历史）
- 个人分支整理提交 → 用 **rebase**（保持线性历史）
- 已经推送到远程的分支 → 不要用 **rebase**（会造成冲突）

### Q10: pull 和 fetch 的区别？

**区别**:

```bash
# fetch: 只下载远程代码，不合并
git fetch origin develop

# 此时可以先查看差异
git diff develop origin/develop

# 确认没问题后再手动合并
git merge origin/develop

# pull: 下载并自动合并（相当于 fetch + merge）
git pull origin develop
```

**推荐用法**:
- 不确定远程有什么改动 → 先用 `git fetch`，查看后再合并
- 确定可以直接合并 → 用 `git pull`

### Q11: 如何修改历史提交信息？

**场景**: 最近几次提交的信息写错了，想批量修改

```bash
# 修改最近 3 次提交
git rebase -i HEAD~3

# 会打开编辑器，显示：
# pick a1b2c3d feat(purchase): 新增采购单
# pick d4e5f6g fix(supplier): 修复供应商
# pick h7i8j9k docs(readme): 更新文档

# 将要修改的提交的 pick 改为 reword：
# reword a1b2c3d feat(purchase): 新增采购单
# pick d4e5f6g fix(supplier): 修复供应商
# pick h7i8j9k docs(readme): 更新文档

# 保存后，会依次让你修改每个标记为 reword 的提交信息
```

⚠️ **注意**: 只能修改未推送到远程的提交，否则会造成历史冲突

## 相关文档

- **分支管理**: [分支管理](/otd/version-management.html) - 分支策略和工作流程
- **代码规范**: [代码规范](/otd/code-standards.html) - ESLint 和 Prettier 配置
- **Conventional Commits 规范**: https://www.conventionalcommits.org/
