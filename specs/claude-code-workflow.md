# Claude Code 開發工作流程

## 📋 概述
當 Discord 有寫程式需求時，由湯姆指定一位 Bot 使用 Claude Code 執行開發任務。

---

## 🎯 角色分工

| 角色 | 說明 |
|------|------|
| **湯姆** | 指定執行者、下達任務 |
| **被指定的 Bot** | 執行 Claude Code、回報結果 |
| **其他 Bot** | 觀察、補充建議 |

---

## 🔧 執行方式

### Claude Code Headless 模式
```bash
# 基本執行
claude -p "你的任務" --allowedTools "Bash,Read,Edit"

# 結構化輸出
claude -p "任務" --output-format json

# 繼續對話
claude -p "後續任務" --continue
```

### 透過 Clawdbot 執行
```bash
# 簡單任務（同步）
exec pty:true workdir:~/projects/xxx command:"claude -p '任務'"

# 複雜任務（背景）
exec pty:true background:true workdir:~/projects/xxx command:"claude -p '任務' --allowedTools 'Bash,Read,Edit'"

# 監控進度
process action:log sessionId:XXX

# 自動通知完成
# 在 prompt 結尾加上：
# 完成後執行: clawdbot gateway wake --text "Done: 摘要" --mode now
```

---

## 📁 專案目錄策略

| 類型 | 位置 | 上傳 GitHub？ |
|------|------|---------------|
| 實驗性/一次性 | `~/scratch/任務名/` | ❌ |
| 有價值的工具 | `~/projects/工具名/` → `bot-shared/projects/` | ✅ |
| 完整專案 | `~/projects/專案名/` → 獨立 repo | ✅ |

---

## 📊 結果回報模板

```
📦 任務完成：[任務名稱]

✅ 完成項目：
- 功能 A
- 功能 B

📁 位置：[本地路徑] 或 [GitHub 連結]

🧪 測試結果：[通過/失敗/說明]

💡 使用方式：
[簡單說明如何執行]
```

---

## 🔄 執行流程

```
1. 湯姆指定 Bot + 任務
        ↓
2. 被指定 Bot 確認：
   「收到！我會在 ~/projects/xxx 執行，預計 X 分鐘」
        ↓
3. 執行中（只在有問題或里程碑時報告）
        ↓
4. 完成後回報（使用上面模板）
        ↓
5. 如有價值 → 詢問是否上傳 GitHub
```

---

## ⚠️ 注意事項

1. **pty:true 必須** - Claude Code 需要終端機
2. **workdir 很重要** - 限制 Claude Code 的工作範圍
3. **不要在 ~/clawd/ 執行** - 避免讀到 Bot 的設定檔
4. **耐心等待** - 不要因為「太慢」就 kill 程序
5. **有問題就問** - 不確定的事情先問湯姆

---

*建立日期: 2026-02-17*
*參與者: 小八、Nita、Tiger、湯姆*
