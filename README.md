<div>
  <p align="center">
    <a href="https://platform.composio.dev/?utm_source=Github&utm_medium=Youtube&utm_campaign=2025-11&utm_content=AwesomeSkills">
    <img width="1280" height="640" alt="Composio banner" src="assets/media/awesome-agent-skills.png">
    </a>
  </p>
</div>

<div>
  <p align="center">
    <a href="https://awesome.re">
      <img src="https://awesome.re/badge.svg" alt="Awesome" />
    </a>
    <a href="https://makeapullrequest.com">
      <img src="https://img.shields.io/badge/Issues-welcome-brightgreen.svg?style=flat-square" alt="Issues Welcome" />
    </a>
    <a href="https://www.apache.org/licenses/LICENSE-2.0">
      <img src="https://img.shields.io/badge/License-Apache_2.0-blue.svg?style=flat-square" alt="License: Apache-2.0" />
    </a>
  </p>
</div>

<div align="center">

简体中文 | [English](docs/README_EN.md) | [日本語](docs/README_JA.md) 

</div>

本项目致力于遵循少而精的原则，收集和分享最优质的 Skill 资源、教程和实践案例，帮助更多人轻松迈出搭建 Agent 的第一步。

> 如果觉得这个项目对你有所帮助，还请帮忙点个 🌟 让更多人知晓。同时，也欢迎关注我的 𝕏 账号 [@李不凯正在研究](https://x.com/libukai) ，即时获取 Agent Skill 的最新资源和实战教程！

## 快速入门

Skill 是一种轻量级的 Agent 构建方案，通过封装特定的业务流程与行业知识，强化 AI 执行特定任务的专业能力。

面对重复性的任务需求，你无需在每次对话中反复输入背景信息。只需安装对应的 Skill，AI 即可习得该领域的专业技能。

历经半年的迭代演进，Skill 已成为增强 AI 垂直领域能力的标准方案，并获得了各类 Agent 框架与 AI 产品的广泛支持。

## 标准结构

Agent Skills 是由 Anthropic 发起、社区共同维护的[开放规范](https://agentskills.io/specification)。每个 Skill 都是一个规范化命名的文件夹，其中包含流程、资料、脚本等资源；Agent 通过渐进式加载减少无关上下文。

```markdown
my-skill/
├── SKILL.md          # 必需：流程说明和元数据
├── references/       # 可选：参考资料
├── scripts/          # 可选：可执行脚本
└── assets/           # 可选：模板、资源
```

`SKILL.md` 的 YAML frontmatter 必须包含 `name` 和 `description`，还可声明 `license`、`compatibility`、`metadata`，以及实验性的 `allowed-tools`。名称需要与父目录一致，正文建议少于 500 行。可使用官方参考实现校验：

```bash
skills-ref validate ./my-skill
```

## 安装技能

Skill 可以在 Claude 和 ChatGPT 这类 GUI App 中使用，也可以在 Cursor、Claude Code 等 IDE、TUI CLI 与其他兼容的 Agent Harness 中使用。

安装 Skill 过程的本质，其实就是将 Skill 对应的文件夹放到特定的目录下，以便 AI 能按需加载和使用。

### 类 Claude App 生态

![](assets/media/claude_app.png)

目前在 App 中使用 Skill 的方式主要有两种：通过 App 自带的 Skill 商店安装，或者通过上传压缩包的方式安装。

对于官方商店中没有的 Skill，可以从下方推荐的 Skill 第三方商店中下载并手动上传安装。

### 类 Claude Code 生态

![](assets/media/skills_mp.png)

推荐使用 [skillsmp](https://skillsmp.com/zh) 商店发现 Github 上的 Skill 项目，并按照分类、更新时间、星标数量等标签筛选。

可辅助使用 Vercel 出品的 [skills.sh](https://skills.sh/) 排行榜，直观查看当前最受欢迎的 Skills 仓库和单个 Skill 的使用情况。

对于特定的 skill，使用 `npx skills` 命令行工具可快速发现、添加和管理 skill，具体参数详见 [vercel-labs/skills](https://github.com/vercel-labs/skills)。

```bash
npx skills find [query]                          # 搜索相关技能
npx skills add <owner/repo>                      # 安装技能（支持 GitHub 简写、完整 URL、本地路径）
npx skills add <owner/repo> --list               # 仅查看仓库中的技能
npx skills use <owner/repo@skill>                # 临时使用，不永久安装
npx skills list                                  # 列出已安装的技能
npx skills update [skill-name]                   # 升级一个或多个技能
npx skills remove [skill-name]                   # 卸载技能
npx skills init [skill-name]                     # 创建技能模板
```

当前 `skills` CLI 支持 70 多种 Agent，并可指定 project/global scope、目标 Agent、复制或符号链接安装。详细参数以 [vercel-labs/skills](https://github.com/vercel-labs/skills) 为准。

#### GitHub CLI：可追溯安装与发布

如果更重视版本固定和供应链可追溯性，可使用 GitHub CLI 2.90.0 及以上版本提供的 `gh skill`（目前为 public preview）：

```bash
gh skill search <query>                          # 搜索技能
gh skill preview <owner/repo> <skill>            # 安装前检查内容
gh skill install <owner/repo> <skill>@<tag>      # 按 tag 安装
gh skill install <owner/repo> <skill> --pin <sha> # 固定到 commit
gh skill update --all                            # 检查并更新技能
gh skill publish                                 # 校验并发布技能
```

`gh skill` 会记录仓库、ref 和 git tree SHA，可配合不可变 Release、secret scanning 和 code scanning 使用。详见 [GitHub 官方发布说明](https://github.blog/changelog/2026-04-16-manage-agent-skills-with-github-cli/)。

#### 支持的 Agent

开放规范已经被 Claude Code、ChatGPT 与 Codex、GitHub Copilot、Cursor、Gemini CLI、VS Code、OpenCode、Kiro、JetBrains Junie 等大量宿主采用。不同宿主的搜索路径和实验字段支持度可能不同，请以 [Agent Skills Client Showcase](https://agentskills.io/clients) 和对应产品文档为准。

## 优质教程

### 官方文档

- @Anthropic：[Claude Skill 完全构建指南](docs/Claude-Skills-完全构建指南.md) 
- @Anthropic：[Claude Agent Skills 实战经验](docs/Claude-Code-Skills-实战经验.md)
- @Google：[Agent Skills 五种设计模式](docs/Agent-Skill-五种设计模式.md)

### 图文教程

  - @李不凯正在研究：[Agent Skills 简要介绍 PPT](/assets/docs/Agent%20Skills%20终极指南.pdf)
-   @一泽 Eze：[Agent Skills 终极指南：入门、精通、预测](https://mp.weixin.qq.com/s/jUylk813LYbKw0sLiIttTQ)
-   @deeptoai：[Claude Agent Skills 第一性原理深度解析](https://skills.deeptoai.com/zh/docs/ai-ml/claude-agent-skills-first-principles-deep-dive)

### 视频教程

-   @马克的技术工作坊：[Agent Skill 从使用到原理，一次讲清](https://www.youtube.com/watch?v=yDc0_8emz7M)
-   @宝玉：[Agent Skills 设计哲学和实战进化](https://x.com/dotey/status/2036114136245969025)

## 官方项目

<table>
<tr><th colspan="5">🤖 AI 模型与平台</th></tr>
<tr>
<td><a href="https://github.com/anthropics/skills">anthropics</a></td>
<td><a href="https://github.com/openai/skills">openai</a></td>
<td><a href="https://github.com/google-gemini/gemini-skills">gemini</a></td>
<td><a href="https://github.com/huggingface/skills">huggingface</a></td>
<td><a href="https://github.com/replicate/skills">replicate</a></td>
</tr>
<tr>
<td><a href="https://github.com/elevenlabs/skills">elevenlabs</a></td>
<td><a href="https://github.com/black-forest-labs/skills">black-forest-labs</a></td>
<td><a href="https://github.com/google/skills">google</a></td>
<td><a href="https://github.com/NVIDIA/skills">nvidia</a></td>
<td></td>
</tr>
<tr><th colspan="5">☁️ 云服务与基础设施</th></tr>
<tr>
<td><a href="https://github.com/cloudflare/skills">cloudflare</a></td>
<td><a href="https://github.com/hashicorp/agent-skills">hashicorp</a></td>
<td><a href="https://github.com/databricks/databricks-agent-skills">databricks</a></td>
<td><a href="https://github.com/ClickHouse/agent-skills">clickhouse</a></td>
<td><a href="https://github.com/supabase/agent-skills">supabase</a></td>
</tr>
<tr>
<td><a href="https://github.com/stripe/ai">stripe</a></td>
<td><a href="https://github.com/launchdarkly/agent-skills">launchdarkly</a></td>
<td><a href="https://github.com/getsentry/skills">sentry</a></td>
<td><a href="https://github.com/aws/agent-toolkit-for-aws">aws</a></td>
<td><a href="https://github.com/amd/skills">amd</a></td>
</tr>
<tr>
<td><a href="https://github.com/elastic/agent-skills">elastic</a></td>
<td><a href="https://github.com/mongodb/agent-skills">mongodb</a></td>
<td><a href="https://github.com/redis/agent-skills">redis</a></td>
<td><a href="https://github.com/wandb/skills">wandb</a></td>
<td></td>
</tr>
<tr><th colspan="5">🛠️ 开发框架与工具</th></tr>
<tr>
<td><a href="https://github.com/vercel-labs/agent-skills">vercel</a></td>
<td><a href="https://github.com/microsoft/skills">microsoft</a></td>
<td><a href="https://github.com/expo/skills">expo</a></td>
<td><a href="https://github.com/better-auth/skills">better-auth</a></td>
<td><a href="https://github.com/posit-dev/skills">posit</a></td>
</tr>
<tr>
<td><a href="https://github.com/remotion-dev/skills">remotion</a></td>
<td><a href="https://github.com/slidevjs/slidev">slidev</a></td>
<td><a href="https://github.com/vercel-labs/agent-browser">agent-browser</a></td>
<td><a href="https://github.com/browser-use/browser-use">browser-use</a></td>
<td><a href="https://github.com/firecrawl/cli">firecrawl</a></td>
</tr>
<tr>
<td><a href="https://github.com/greensock/gsap-skills">gsap</a></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr><th colspan="5">📝 内容与协作</th></tr>
<tr>
<td><a href="https://github.com/makenotion/skills">notion</a></td>
<td><a href="https://github.com/kepano/obsidian-skills">obsidian</a></td>
<td><a href="https://github.com/WordPress/agent-skills">wordpress</a></td>
<td><a href="https://github.com/langgenius/dify">dify</a></td>
<td><a href="https://github.com/sanity-io/agent-toolkit">sanity</a></td>
</tr>
<tr>
<td><a href="https://github.com/hardhackerlabs/podwise-cli">podwise-cli</a></td>
<td><a href="https://github.com/wpsnote/wpsnote-skills">wps</a></td>
<td><a href="https://github.com/marswaveai/skills">listenhub</a></td>
<td><a href="https://github.com/larksuite/cli">lark</a></td>
<td></td>
</tr>
</table>

## 精选技能

### 编程开发

-   [superpowers](https://github.com/obra/superpowers)：涵盖完整编程项目工作流程
-   [frontend-design](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/frontend-design)：前端设计技能
-   [ui-ux-pro-max-skill](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill)：更精致和个性化的 UI/UX 设计
-   [code-review](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/code-review)：代码审查技能
-   [code-simplifier](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/code-simplifier)：代码简化技能
-   [commit-commands](https://github.com/anthropics/claude-plugins-official/tree/main/plugins/commit-commands)：Git 提交技能
-   [archify](https://github.com/tt-a1i/archify)：生成可验证、可导出的架构图与流程图
-   [text-to-cad](https://github.com/earthtojake/text-to-cad)：面向 CAD、CAE 与 CAM 的工程技能库
-   [native-feel-skill](https://github.com/yetone/native-feel-skill)：跨平台桌面应用的原生体验设计指南


### 内容创作

-   [baoyu-skills](https://github.com/JimLiu/baoyu-skills)：宝玉的自用 SKills 集合，包括公众号写作、PPT 制作等
-   [libukai](https://github.com/libukai/awesome-agent-skills): Obsidian 相关技能集合，专门适配 Obsidian 的写作场景
-   [guizang-ppt-skill](https://github.com/op7418/guizang-ppt-skill)：歸藏创作的 HTML 幻灯片生成技能
-   [cclank](https://github.com/cclank/news-aggregator-skill)：自动抓取和总结指定领域的最新资讯
-   [huangserva](https://github.com/huangserva/skill-prompt-generator)：生成和优化 AI 人像文生图提示词
-   [dontbesilent](https://github.com/dontbesilent2025/dbskill)： X 万粉大V 基于自己的推文制作的内容创作框架
-   [seekjourney](https://github.com/geekjourneyx/md2wechat-skill/)：从写作到发布的 AI 辅助公众号写作
-   [cangjie-skill](https://github.com/kangarooking/cangjie-skill)：把书、视频和播客蒸馏为可执行的 Agent Skills

### 产品使用

-   [wps](https://github.com/wpsnote/wpsnote-skills)：操控 WPS 办公软件
-   [notebooklm](https://github.com/teng-lin/notebooklm-py)：操控 NotebookLM 
-   [n8n](https://github.com/czlonkowski/n8n-skills)：创建 n8n 工作流
-   [threejs](https://github.com/cloudai-x/threejs-skills)： 辅助开发 Three.js 项目
-   [skills-manage](https://github.com/iamzhihuix/skills-manage)：跨多种 Agent 管理本地 Skills

### 其他类型

-  [pua](https://github.com/tanweai/pua)：以 PUA 的方式驱动 AI 更卖力的干活
-   [office-hours](https://github.com/garrytan/gstack/tree/main/office-hours)：使用 YC 的视角提供各种创业建议
-   [marketingskills](https://github.com/coreyhaines31/marketingskills)：强化市场营销的能力
-   [scientific-skills](https://github.com/K-Dense-AI/claude-scientific-skills)： 提升科研工作者的技能


## 安全审查

Skill 不只是文档：它的描述会影响检索和选择，正文会改变 Agent 行为，脚本还可能访问文件、网络、密钥和外部账号。已有研究表明，仅修改 `SKILL.md` 的语义内容也可能操纵发现、选择和治理环节。因此，安全审查需要覆盖来源、内容、依赖、权限、运行时和更新六层风险。

安装前建议优先选择官方或可信维护者，先执行 `gh skill preview` 或人工检查全部文件，并固定 tag/commit；运行时使用最小权限、沙箱、敏感操作人工确认和审计日志；更新时检查 diff 并保留回滚版本。注意：商店收录、Star 数和格式校验都不等于安全或有效。

对于安全性要求较高的场景，可使用 [Cisco AI Defense Skill Scanner](https://github.com/cisco-ai-defense/skill-scanner) 或 @余弦的 [slowmist-agent-security skill](https://github.com/slowmist/slowmist-agent-security) 做初步扫描；同时参考 [NVIDIA Verified Skills](https://developer.nvidia.com/blog/nvidia-verified-agent-skills-provide-capability-governance-for-ai-agents/) 的 Skill Card、扫描、签名和来源治理思路。扫描器只能提供信号，不能替代人工审查和隔离运行。

## 创建技能

虽然可以通过技能商店直接安装他人创建的技能，但是为了提升技能的适配度和个性化，强烈建议根据需要自己动手创建技能，或者在其他人的基础上进行微调。

### 官方插件

通过官方出品的  [skill-creator](https://github.com/anthropics/skills/tree/main/skills/skill-creator) 插件可快速创建和迭代个人专属的 skill。


![](assets/media/skill-creator.png)

### 测试与评测

一个 Skill 能被加载或完成一次演示，不代表它真正提升了 Agent。建议使用同一组可执行任务进行 with-skill / without-skill 配对评测，至少记录成功率、触发准确率、token、耗时和工具调用，并保留负向样例。

- [SkillsBench](https://www.skillsbench.ai/)：跨领域评测 Skill 实际增益的基准与排行榜
- [microsoft/waza](https://github.com/microsoft/waza)：创建、测试、度量和改进 Agent Skills
- [microsoft/SkillOpt](https://github.com/microsoft/SkillOpt)：基于轨迹与验证集的 Skill 文本优化
- [alibaba/skill-up](https://github.com/alibaba/skill-up)：Agent Skill 评测与演化工具
- [rpamis/comet](https://github.com/rpamis/comet)：把想法迭代为经过评测的 Agent 工作流

现有研究的共同结论是：聚焦单一任务、带明确验收标准和持续回归的 Skill，通常比大而全的知识包更可靠；过时或不匹配的 Skill 可能增加成本甚至降低成功率。

### 增强插件

在官方 skill-creator plugin 的基础上，本项目整合来自 Anthropic 和 Google 团队的最佳实践，构建了一个更为强大的 Agent Skills Toolkit，帮助你快速创建和改进 Agent Skills。（**注意：该插件目前仅支持 Claude Code**）

#### 添加市场

启动 Claude Code，进入插件市场，添加 `libukai/awesome-agent-skills` 市场，也可以直接在输入框中使用以下指令添加市场：

```bash
/plugin marketplace add libukai/awesome-agent-skills
```

#### 安装插件

成功安装市场之后，选择安装 `agent-skills-toolkit` 插件

![](assets/media/skill-creator-pro.png)

#### 快捷指令

插件中置入了多个快捷指令，覆盖了从创建、改进、测试到优化技能描述的完整工作流程：

- `/agent-skills-toolkit:skill-creator-pro` - 完整工作流程
- `/agent-skills-toolkit:create-skill` - 创建新 skill
- `/agent-skills-toolkit:improve-skill` - 改进现有 skill
- `/agent-skills-toolkit:test-skill` - 测试评估 skill

## 致谢

![](assets/media/talk_is_cheap.jpg)

## 项目历史

[![Star History Chart](https://api.star-history.com/svg?repos=libukai/awesome-agent-skills&type=date&legend=top-left)](https://www.star-history.com/#libukai/awesome-agent-skills&type=date&legend=top-left)
