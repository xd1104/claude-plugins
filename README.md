# Benson 的 AI 團隊（Claude Code plugin marketplace）

把 team-lab 團隊（角色＋工作流程＋累積的開發經驗）包成一個外掛，**所有專案共用同一份**。
改這裡一個地方，電腦端與手機雲端的所有專案下次開啟時都是最新的。

## 這裡面有什麼

```
plugins/ai-team/
  agents/            lab-ux（UX 設計）／lab-dev（開發）／lab-qa（品管驗收）
  skills/team-lab/
    SKILL.md         /ai-team:team-lab 的工作流程
    handbook.md      跨專案經驗手冊（Benson 偏好、環境雷、架構教訓）
```

## 怎麼讓一個專案用到它

在該專案 repo 的 `.claude/settings.json` 放這幾行：

```json
{
  "extraKnownMarketplaces": {
    "benson": {
      "source": { "source": "github", "repo": "xd1104/claude-plugins" }
    }
  },
  "enabledPlugins": { "ai-team@benson": true }
}
```

commit＋push 之後，在那個 repo 開 Claude Code（**含手機的雲端 session**）就叫得出 `/ai-team:team-lab`，三個角色也都在。

新專案不必手動加 —— 從 `xd1104/app-template` 按「Use this template」建立，這幾行已經在裡面了。

## 怎麼更新

- **手冊**（最常變）：正本在 Benson 的 Obsidian `ai-team/lab-team-handbook.md`。電腦端收工更新完，把副本同步到這裡的 `handbook.md` 再 push。
- **角色／流程**：直接改 `agents/` 或 `skills/`。
- 改完把 `.claude-plugin/marketplace.json` 與 `plugins/ai-team/.claude-plugin/plugin.json` 的 `version` 一起往上加，使用者才收得到更新。

## 為什麼要有這個

手機版 Claude Code 是雲端 session：它只看得到你打開的那個 GitHub repo，看不到 Benson 電腦上的 `~/.claude/`，也讀不到 Obsidian。
所以團隊與經驗必須住在雲端讀得到的地方 —— 就是這個 repo。
