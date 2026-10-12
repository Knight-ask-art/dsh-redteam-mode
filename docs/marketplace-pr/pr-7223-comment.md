# PR #7223 说明（当前生效）

投稿分支：`Jueze-2019:update-dsh-redteam-mode-v0.13.1`
条目文件：`data/plugins/Jueze-2019__dsh-redteam-mode--packages-redteam-bundle.yml`（只改这一个）

## 这次改了什么

条目描述里补上 v0.13.1 落地的能力：**右侧控制台跟着当前会话走**（中英两段各加一句）。
其余数字（14 个随包技能 / 56 个 `redteam_*` 工具 / 9 个页签 / 5 个执行角色）与代码一致，
本次未变；`version` 字段由站点从 npm 自动取，未手改。

## 复核这些声明的入口（维护者对着代码数时用）

| 声明 | 代码位置 |
| --- | --- |
| 绑定表落盘 `sessions.json`（键 = 根会话 id） | `packages/redteam-store/lib/core.js` → `sessionBindings()` / `setSessionBinding()` |
| 命中顺序：落盘绑定 → 会话标题反查 → 上次选择 | `packages/redteam-ui/lib/client.js` → `applySessionBinding()` |
| 子智能体会话解析到根会话 | `packages/redteam-ui/lib/index.js` → `resolveRootSessionId()` |
| 面板状态标出"按哪一条匹配上的" | 顶部四态标签 + 底部 `会话 <id> · 落盘绑定\|会话标题\|上次选择\|默认单位` |
| 回归测试 | `packages/redteam-ui/test/session-root.test.mjs`、`tabs-render.test.mjs`（「面板跟随会话」一组）、`packages/redteam-tools/test/session-isolation.test.mjs`（落盘绑定一组） |

发布记录：<https://github.com/Jueze-2019/dsh-redteam-mode/releases/tag/v0.13.1>
