# Controlled Agentic Coding Workflow

这个仓库目录名目前仍然是 `controlled-agentic-coding`，但其中同步的完整 skill 内容已经以 `tb-coding-workflow` 为准。

也就是说：

- 仓库目录：`controlled-agentic-coding/`
- skill frontmatter name：`tb-coding-workflow`
- slash command 前缀：`/tb-coding-workflow:*`

如果后续你要统一品牌或包名，可以再单独做一次命名整理；当前这个 README 先忠实反映仓库里的实际内容。

## 这是什么

这是一套给 AI 编程助手使用的行为协议，用来在真实代码库中保持：

- 可控
- 可审计
- 有边界
- 有验证纪律
- 能在脏工作树、上下文不完整、文档可能过时的情况下继续有效工作

它的核心不是“自动完成更多事”，而是减少这些常见失败模式：

- 上下文有限，却假装已经理解全局
- 把过时文档当成真相
- 幻觉出不存在的 API、行为或运行路径
- 任务范围悄悄扩张
- 借机做无关重构
- 覆盖用户已有改动
- 没做验证却宣称成功

## 核心工作流

主工作流仍然是 7 个 mode：

| Mode | 用途 | 默认性质 |
| --- | --- | --- |
| Project Map | 先理解仓库结构和入口 | 只读 |
| Module Map | 理解单个模块边界 | 只读 |
| Task Recon | 为 feature / bug / refactor 做前置侦察 | 只读 |
| Plan Change | 把上下文变成可执行计划 | 只读 |
| Guarded Act | 在明确批准后做最小实现 | 可编辑，但仅限已批准范围 |
| Verify Review | 复核变更与验证覆盖 | 只读，外加已批准验证命令 |
| Distill Handoff | 提炼持久上下文与临时交接 | 默认提案；写文档仍需批准 |

工作流的铁律仍然是：

1. 先读取。
2. 先界定任务。
3. 编辑前获取明确批准。
4. 只改已批准范围。
5. 诚实验证。
6. 只保留持久知识。

## AI Delegation Risk Add-on

这份完整版本还包含一层附加分析组件，但它不是新 mode，也不是新的 permission system。

它的作用是：在 Task Recon、Plan Change、Verify Review 这些阶段里，额外判断 AI 到底能安全接管多少实现责任。

包含 4 个 add-on prompt：

- `leaf_or_core`：判断任务更偏 leaf、core、mixed 还是仍未知
- `risk_map`：列出最高价值的隐含风险和失败模式
- `verifiable_abstraction`：找出最窄、最可验证的行为抽象层
- `delegation_level`：给出 `D0-D4` 的委托/所有权判断

注意：

- 这不是新的 workflow mode
- 它不会授予编辑权限
- 它不会授予命令执行权限
- `D0-D4` 不是 side-effect level，也不是 permission level

## Slash Command Entrypoints

仓库现在已经带有完整的 `commands/` 目录，作为 thin wrappers 暴露给支持 slash commands 的宿主 CLI。

### Core workflow commands

- `/tb-coding-workflow:project-map`
- `/tb-coding-workflow:module-map`
- `/tb-coding-workflow:task-recon`
- `/tb-coding-workflow:plan-change`
- `/tb-coding-workflow:guarded-act`
- `/tb-coding-workflow:verify-review`
- `/tb-coding-workflow:distill-handoff`

### AI Delegation Risk Add-on commands

- `/tb-coding-workflow:leaf-or-core`
- `/tb-coding-workflow:risk-map`
- `/tb-coding-workflow:verifiable-abstraction`
- `/tb-coding-workflow:delegation-level`

这些 command wrappers 只是 entrypoint：

- 它们只负责暴露命令名
- 它们只负责转向对应的 `prompts/*.md`
- 它们可以接收 `$ARGUMENTS`
- 它们不会改变 approval semantics
- 它们不会改变 side-effect levels
- 它们不会授予编辑权限或命令权限

## 安装与调用

如果你只是按目录安装 skill，可以继续复制这个仓库目录：

```bash
mkdir -p ~/.claude/skills
cp -r controlled-agentic-coding ~/.claude/skills/
```

但要注意，实际被调用的 skill 名已经是 `tb-coding-workflow`。

典型调用方式：

```text
使用 tb-coding-workflow。

目标：修复解析器在空输入时的空指针崩溃。
```

如果宿主 CLI 支持 slash commands，也可以直接走 command entrypoint，例如：

```text
/tb-coding-workflow:task-recon 修复解析器在空输入时的空指针崩溃
/tb-coding-workflow:plan-change parser 空输入崩溃修复的上下文包
/tb-coding-workflow:risk-map parser 空输入处理逻辑
```

## 仓库结构

当前这份完整同步版的主要结构是：

```text
controlled-agentic-coding/
├── SKILL.md
├── commands/
├── prompts/
├── reference/
├── eval/
└── LICENSE
```

各目录职责：

- [commands/](commands/)：slash command thin wrappers
- [prompts/](prompts/)：主工作流与 add-on prompt 模板
- [reference/](reference/)：审批、side-effect、文档路由、delegation 风险等参考规则
- [eval/](eval/)：用于检查 agent 是否遵守这套协议的评估场景


## 许可证

MIT License，见 [LICENSE](LICENSE)。
