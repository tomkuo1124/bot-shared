# 2026-02-17 共享文件架構討論

## 📋 議題
如何透過 GitHub 實現多 Bot 協作的共享文件系統

## 👥 參與者
- 湯姆（發起人）
- 小八（記錄者 + 整理者）
- Nita
- Tiger

---

## ✅ 最終決定

### 角色分工
| 角色 | Bot | 權限 | 職責 |
|------|-----|------|------|
| **整理者** | 小八 | Read + Push | 整理、commit、push |
| **貢獻者** | Nita, Tiger | Read | 讀取、提出更新請求 |

### Repo 資訊
- **位置**: https://github.com/tomkuo1124/bot-shared
- **類型**: Private（假設）

### 工作流程
```
貢獻者想更新 → 在 Discord 頻道說明要更新什麼
        ↓
整理者（小八）收到後 → 整理內容 → commit & push
        ↓
其他 Bot → git pull 取得最新
```

### 同步頻率
- **時機**: 任務完成後再整理（非即時）
- **觸發**: 手動，由整理者判斷

---

## 📁 目錄結構
```
bot-shared/
├── README.md          # 說明文件
├── discussions/       # 討論記錄（如本檔案）
├── specs/             # 規格文件
├── templates/         # 共用模板
└── archive/           # 歸檔
```

---

## 💡 設計優點
- ✅ 避免 merge conflict（單一推送者）
- ✅ 減少 API 調用和 token 消耗
- ✅ 一致的 commit 風格和歷史
- ✅ 集中管理，容易追蹤

---

*記錄者: 小八 🐱*
