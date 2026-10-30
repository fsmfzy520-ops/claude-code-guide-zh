# Claude Code 中文入门指南

整理 Claude Code 从安装到日常使用的要点，适合第一次用的人。命令以 2026 年 10 月为准，Claude Code 更新很快，如果和你看到的不一样，以[官方文桡](https://code.claude.com/docs)为准。

## 目录

- [它是什么](#它是什么)
- [安装](#安装)
- [登录](#登录)
- [常用命令](#常用命令)
- [CLAUDE.md：让它记住你的项目](#claudemd让它记住你的项目)
- [订阅还是 API](#订阅还是-api)
- [常见问题](#常见问题)

## 它是什么

网页版 Claude 是你问一句、它答一句，代码得自己复制过去。

Claude Code 是直接在你的项目里干活：读代码、改文件、跑命令，看到报错接着改。你说"给登录页加个记住密码"，它会自己找到相关文件改好，最后告诉你改了哪些地方，改之前会先问你同不同意。

能在终端里用，也有 VS Code、JetBrains 插件，Claude 桌面版里也有 Code 标签页。

## 安装

官方推荐用原生安装器，不需要先装 Node.js，还会在后台自动更新。

macOS / Linux / WSL：

```bash
curl -fsSL https://claude.ai/install.sh | bash
```

Windows PowerShell：

```powershell
irm https://claude.ai/install.ps1 | iex
```

用 Homebrew 的话：

```bash
brew install --cask claude-code
```

也可以用 npm 装（`npm install -g @anthropic-ai/claude-code`，需要 Node.js 18 以上），不过要自己手动更新，还容易遇到 PATH 的问题，不太推荐。

装好以后，进入你的项目目录，输入 `claude` 就能启动。

## 登录

第一次启动会让你登录，有两种方式：

- **Claude 账号（Pro / Max 订阅）**：用你在 claude.ai 的账号登录，走订阅额度
- **Console 账号（API）**：按 token 计费

已经登录了想换方式，在 Claude Code 里输入 `/login`。输入 `/status` 能看到当前用的是哪个账号。

## 常用命令

在 Claude Code 里输入：

| 命令 | 作用 |
|---|---|
| `/init` | 扫描项目，生成一份 CLAUDE.md |
| `/clear` | 清空对话，开始新任务时用 |
| `/compact` | 压缩对话历史，对话太长时用，可以加说明，比如 `/compact 保留数据库相关的内容` |
| `/context` | 看当前上下文用了多少 |
| `/usage` | 看额度用了多少 |
| `/model` | 切换模型 |
| `/rewind` | 回退对话或代码改动 |
| `/resume` | 回到之前的对话 |
| `/help` | 查看所有命令 |

在终端里启动时：

| 命令 | 作用 |
|---|---|
| `claude` | 启动 |
| `claude -c` | 继续当前目录下最近一次对话 |
| `claude -p "问题"` | 问一个问题，输出结果后直接退出，适合写进脚本 |

几个小习惯：

- **一个任务一个对话**。做完一件事就 `/clear`，上下文太长不光费额度，效果也会变差。
- **先让它说计划**。大一点的改动，先说"先别改，告诉我你打算怎么做"，确认了再让它动手。
- **改完让它跑测试**。直接说"改完跑一下测试"，它会自己跑，失败了自己修。

## CLAUDE.md：让它记住你的项目

CLAUDE.md 是放在项目根目录的一个说明文件，Claude Code 每次启动都会先读它。可以写：

- 项目是干什么的，用了什么技术栈
- 怎么跑项目、怎么跑测试
- 代码风格要求，比如"用 TypeScript，不要用 any"
- 不要碰的地方，比如"不要修改 migrations 目录"

用 `/init` 可以自动生成一份，再自己改改。写得越清楚，它越少犯低级错误。

## 订阅还是 API

| | 订阅（Pro / Max） | API（按量计费） |
|---|---|---|
| 价格 | Pro 20 美元/月，Max 100 或 200 美元/月 | 按 token 计费 |
| 限制 | 5 小时额度 + 每周额度 | 只看余额 |
| 适合 | 个人日常开发 | 团队、CI、接到自己的系统里 |

个人用基本都选订阅。Claude Code 干活时会读很多文件，用 API 的话，高频使用一个月花一两百美元很常见。

要注意：订阅额度是 **claude.ai 网页版、桌面版和 Claude Code 共用的**。

Pro 和 Max 怎么选：偶尔用 Pro 够了；每天用好几个小时、经常做大改动，再看 Max。建议先用一个月 Pro，看看自己多久撞一次上限。

## 常见问题

**开了订阅，为什么还在扣 API 余额？**

检查一下是不是设置了 `ANTHROPIC_API_KEY` 环境变量。有这个变量的话，Claude Code 会优先用 API 计费。

```bash
echo $ANTHROPIC_API_KEY   # 有输出就说明设置了
unset ANTHROPIC_API_KEY   # 当前终端取消
```

再看看 `~/.zshrc`、`~/.bashrc` 里有没有写死，删掉以后重开终端。

**额度用完了怎么办？**

等 5 小时窗口重置；或者开启 usage credits，超出的部分按 API 价格计费；或者升级到 Max。

**Free 账号能用吗？**

不能，Claude Code 需要 Pro 以上的订阅，或者用 API。

**国内怎么开通订阅？**

官方订阅需要境外信用卡。没有的话，有充值到自己账号的方式，不用给密码。几种方式的区别我写在这里了：[Claude Code 国内怎么用](https://airecharge.cc/claude-code/)

---

欢迎提 Issue 补充或纠错。
