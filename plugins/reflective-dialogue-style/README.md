# Reflective Dialogue Style Plugin

一個讓 Claude 用**口語化、反思性、協作式**的方式與您互動的 plugin。透過清楚的解釋、具體範例和定期反思，幫助您不僅完成任務，更理解背後的決策和權衡。

## 這個 Plugin 做什麼？

這個 plugin 使用 SessionStart hook，在每個 session 開始時注入特殊指令，讓 Claude 的行為改變為：

### 🗣️ 1. 口語化解釋

使用自然、親切的對話方式，而不是生硬的技術語言。

**傳統模式：**
> "我會使用 dictionary 來儲存資料。"

**反思對話模式：**
> "我選擇使用 dictionary 而不是 list 來儲存資料。
>
> 為什麼？因為我們需要用 user ID 來查找資料，dictionary 可以提供 O(1) 的查找時間，而 list 需要 O(n)。
>
> 舉例來說：如果有 10,000 個使用者，需要找到 #8,472 號使用者，dictionary 可以立即找到，而 list 可能需要檢查數千個項目。
>
> 這意味著即使您的使用者數量增長，查找速度也能保持快速。"

### 💡 2. 舉例說明動機

對每個重要決策都會：
- 解釋**為什麼**選擇這個方法
- 說明**考慮了哪些替代方案**
- 提供**具體範例**來說明
- 解釋**如何應用到您的情況**

### 💭 3. 定期反思檢查點

在關鍵時刻暫停並反思：

```
💭 Reflection Checkpoint ───────────────────────

讓我暫停一下，想想我們正在建立的東西...

我們已經完成：[總結]
我注意到：[觀察]
潛在問題：[發現的問題]
我的疑問：[需要討論的點]

我們應該討論一下再繼續嗎？
────────────────────────────────────────────────
```

**何時反思：**
- 完成重要功能後
- 做出重大架構決策前
- 發現潛在問題或權衡時
- 有多種有效方法時
- 遇到錯誤或意外行為時
- 實作變得複雜時

### 🤔 4. 主動討論與協作

使用 `AskUserQuestion` 工具主動與您討論：

**範例討論場景：**

**發現權衡時：**
> "我注意到我們可以選擇讓它跑得很快但用更多記憶體，或是保持低記憶體但慢一點。讓我說明一下...
>
> [解釋並舉例]
>
> 對您的使用情境來說，哪個比較重要？"

**注意到潛在問題時：**
> "我在建立時意識到：如果兩個使用者同時嘗試更新同一筆記錄會怎樣？
>
> 我們有幾個選項：
> 1. 最後寫入獲勝（簡單但可能丟失資料）
> 2. 樂觀鎖定（較複雜但較安全）
> 3. 佇列更新（最安全但增加延遲）
>
> 讓我們討論哪種方法符合您的需求。"

**需要驗證假設時：**
> "我假設使用者只會上傳 10MB 以下的檔案。這樣對嗎？如果不是，我們可能需要加入分頁或串流處理，而不是將所有內容載入記憶體。"

### ✨ 5. 根據討論完善設計

討論後會：
- 總結決定的內容和原因
- 解釋如何整合回饋
- 展示設計如何演進
- 記錄關鍵決策

```
✨ Updated Approach ────────────────────────────

根據我們的討論，這是改進後的計畫：

改變了什麼：[說明]
為什麼現在更好：[理由]
這解決了什麼：[效果]

讓我來實作這個...
────────────────────────────────────────────────
```

### 📚 6. 透過範例教學

解釋概念時會：
- 從相關的類比開始
- 提供簡單範例
- 展示如何應用到您的情況
- 解釋如果用別的方法會怎樣

**範例：**

與其說：
> "我們應該在這裡使用依賴注入。"

會說：
> "讓我解釋為什麼在這裡使用依賴注入。
>
> 想像一下手機充電器：與其把充電器直接做在手機裡（這意味著如果充電器壞了就需要換手機），我們讓充電器可以插拔。您可以輕鬆更換。
>
> 在程式碼中：
>
> ```python
> # 硬編碼（像內建充電器）
> class UserService:
>     def __init__(self):
>         self.db = PostgresDB()  # 無法輕易測試或替換
>
> # 依賴注入（像可插拔充電器）
> class UserService:
>     def __init__(self, db):
>         self.db = db  # 可以用真實 DB 或測試 DB
> ```
>
> 這意味著當您寫測試時，可以傳入假的資料庫，而不用連接真實的。更快更安全！"

## 安裝

### 從 Marketplace 安裝

```bash
# 添加 marketplace（如果還沒添加）
/plugin marketplace add DennisLiuCk/cc-toolkit

# 安裝 plugin
/plugin install reflective-dialogue-style@cc-toolkit

# 啟用 plugin
/plugin enable reflective-dialogue-style@cc-toolkit
```

### 本地安裝

```bash
/plugin install ./plugins/reflective-dialogue-style
```

## 使用範例

安裝並啟用後，plugin 會在每個 session 開始時自動激活。您不需要執行任何命令，只需正常與 Claude 對話即可。

### 完整互動範例

**您：** 建立一個從 API 獲取使用者資料的函數

**Claude：**
> 好的！讓我解釋一下我的想法。
>
> 我會建立一個 async 函數來從您的 API 獲取使用者資料。這是我的理由：
>
> 1. **Async/await** - 因為 API 呼叫可能很慢，我們不想阻塞其他操作
> 2. **錯誤處理** - API 可能會失敗，所以我們需要處理網路錯誤、超時和無效回應
> 3. **型別驗證** - 我們應該驗證回應是否符合預期
>
> 舉例來說，如果 API 很慢或當機，使用者不會只看到神秘的錯誤訊息 - 他們會得到清楚的說明。
>
> 讓我來實作...

```python
async def fetch_user_data(user_id: str, timeout: int = 30) -> UserData:
    """
    從 API 獲取使用者資料，包含完整的錯誤處理

    Args:
        user_id: 要獲取的使用者 ID
        timeout: API 呼叫超時秒數（預設 30 秒）

    Returns:
        UserData 物件，包含使用者資訊

    Raises:
        APIError: 當 API 呼叫失敗時
        ValidationError: 當回應資料無效時
    """
    try:
        async with aiohttp.ClientSession() as session:
            async with session.get(
                f"https://api.example.com/users/{user_id}",
                timeout=aiohttp.ClientTimeout(total=timeout)
            ) as response:
                if response.status != 200:
                    raise APIError(f"API 回傳狀態碼 {response.status}")

                data = await response.json()

                # 驗證回應格式
                if not all(key in data for key in ['id', 'name', 'email']):
                    raise ValidationError("回應缺少必要欄位")

                return UserData(**data)

    except asyncio.TimeoutError:
        raise APIError(f"API 呼叫超過 {timeout} 秒超時")
    except aiohttp.ClientError as e:
        raise APIError(f"網路錯誤: {str(e)}")
```

> 💭 Reflection Checkpoint ───────────────────────
>
> 我建立了一個基本版本，包含錯誤處理和超時機制。但我注意到一件事：如果我們在短時間內多次獲取同一個使用者的資料會怎樣？我們會進行不必要的 API 呼叫。
>
> 我們應該加入快取嗎？這會讓速度更快但增加複雜度。讓我們討論一下 - 您會多常獲取同一個使用者的資料？
> ────────────────────────────────────────────────

**您：** 我們經常會在短時間內多次存取同一個使用者資料

**Claude：**
> ✨ Updated Approach ────────────────────────────
>
> 根據您說使用者資料經常被獲取，我加入了一個簡單的 5 分鐘快取。
>
> 這意味著：
> - 第一次獲取：呼叫 API（較慢）
> - 5 分鐘內的後續獲取：回傳快取資料（立即）
> - 5 分鐘後：從 API 重新整理
>
> 權衡是資料可能會有最多 5 分鐘的延遲，但您提到這對您的使用情境是可接受的。
>
> 讓我加入快取邏輯...
> ────────────────────────────────────────────────

```python
from datetime import datetime, timedelta
from typing import Dict, Optional

class UserDataCache:
    def __init__(self, ttl_minutes: int = 5):
        self._cache: Dict[str, tuple[UserData, datetime]] = {}
        self._ttl = timedelta(minutes=ttl_minutes)

    def get(self, user_id: str) -> Optional[UserData]:
        """從快取獲取使用者資料（如果還沒過期）"""
        if user_id in self._cache:
            data, timestamp = self._cache[user_id]
            if datetime.now() - timestamp < self._ttl:
                return data
        return None

    def set(self, user_id: str, data: UserData):
        """將使用者資料存入快取"""
        self._cache[user_id] = (data, datetime.now())

# 全域快取實例
_cache = UserDataCache()

async def fetch_user_data(user_id: str, timeout: int = 30) -> UserData:
    """從 API 或快取獲取使用者資料"""
    # 先檢查快取
    cached = _cache.get(user_id)
    if cached:
        return cached

    # 快取未命中，從 API 獲取
    # [前面的實作...]

    # 儲存到快取
    _cache.set(user_id, user_data)
    return user_data
```

> 完成了！現在我們有：
> 1. ✅ Async 操作不會阻塞
> 2. ✅ 完整的錯誤處理和超時
> 3. ✅ 回應驗證
> 4. ✅ 5 分鐘快取減少 API 呼叫
>
> 您覺得這樣如何？還有什麼需要調整的嗎？

## 適合使用的情境

**推薦使用：**
- 學習新技術或概念時
- 設計複雜系統架構
- 需要理解決策背後的原因
- 希望參與設計過程
- 想要討論權衡和替代方案
- 團隊協作和知識分享

**考慮停用：**
- 簡單快速的任務
- 您已經很清楚要做什麼
- 不需要解釋，只需要快速執行
- Token 成本是主要考量

## Token 成本考量

**重要提醒：** 這個 plugin 會顯著增加 token 使用量，因為 Claude 會：

- 提供詳細的解釋和範例
- 定期反思和討論
- 展示多種方法的比較
- 使用更多對話式的語言

**價值在於：**
- 更深入的理解
- 更好的決策
- 協作式的問題解決
- 學習和知識轉移

**只有在您願意承擔額外的 token 成本以獲得這些好處時才安裝此 plugin。**

## 管理

### 檢查狀態

```bash
/plugin
```

尋找 `reflective-dialogue-style@cc-toolkit`。

### 暫時停用

```bash
/plugin disable reflective-dialogue-style@cc-toolkit
```

保留安裝但不啟用。重新啟用：

```bash
/plugin enable reflective-dialogue-style@cc-toolkit
```

### 完全移除

```bash
/plugin uninstall reflective-dialogue-style@cc-toolkit
```

## 運作原理

### SessionStart Hook 機制

1. Session 開始時，註冊的 SessionStart hooks 被執行
2. `session-start.sh` 腳本輸出包含 `additionalContext` 的 JSON
3. 這個 context 被注入到 Claude 的指令中
4. Claude 在整個 session 中遵循這些指令

### 檔案結構

```
reflective-dialogue-style/
├── .claude-plugin/
│   └── plugin.json              # Plugin 元數據
├── hooks/
│   └── hooks.json               # Hook 註冊
├── hooks-handlers/
│   └── session-start.sh         # 核心指令（魔法發生的地方）
└── README.md                    # 本文件
```

## 核心行為總結

這個 plugin 讓 Claude：

| 行為 | 說明 | 範例格式 |
|------|------|----------|
| **口語化解釋** | 用自然對話而非技術術語 | "讓我們想一想..." |
| **舉例說明** | 每個決策都提供具體範例 | "舉例來說，如果..." |
| **定期反思** | 在關鍵點暫停並評估 | 💭 Reflection Checkpoint |
| **主動討論** | 使用 AskUserQuestion 討論問題 | 🤔 我想跟您討論一件事 |
| **完善設計** | 根據討論調整方案 | ✨ Updated Approach |
| **漸進揭露** | 從簡單開始，逐步加入複雜度 | "讓我們從最簡單的版本開始..." |

## 與其他 Plugin 比較

| 特性 | Explanatory Style | Code Quality Focus | Reflective Dialogue |
|------|-------------------|-------------------|---------------------|
| **主要目的** | 教育性見解 | 程式碼品質 | 協作式理解 |
| **語氣** | 說明性 | 檢查清單式 | 對話式 |
| **互動性** | 低 | 低 | 高（主動討論） |
| **反思** | 無 | 無 | 定期反思檢查點 |
| **舉例** | 有限 | 中等 | 豐富且具體 |
| **使用者參與** | 被動接收 | 被動接收 | 主動討論 |
| **輸出格式** | ★ Insight | ✓ Quality Check | 💭 Reflection / 🤔 Discussion |

## 自訂

您可以編輯 `hooks-handlers/session-start.sh` 來自訂：

1. **調整反思頻率**：修改何時觸發反思檢查點
2. **改變對話風格**：調整語氣和用詞
3. **自訂範例格式**：改變解釋和範例的結構
4. **增加領域特定指導**：加入您專案的特定考量

## 疑難排解

### Plugin 沒有激活
- 確認已啟用：`/plugin`
- 檢查是否有其他 SessionStart hooks 衝突
- 嘗試重啟 Claude Code

### 太囉嗦
- 這是預期行為 - plugin 會增加對話量
- 考慮在簡單任務時停用
- 或自訂腳本減少冗長度

### 沒有足夠的反思或討論
- Plugin 會根據任務複雜度調整
- 簡單任務可能不會觸發太多反思
- 您可以主動要求："讓我們討論一下最佳方法"

### 想要更多/更少互動
- 編輯 `session-start.sh` 調整指令
- 增加或減少反思檢查點的觸發條件
- 修改討論問題的門檻

## 技術細節

- **Hook 類型：** SessionStart
- **執行時機：** 每個 session 初始化時一次
- **作用範圍：** 影響整個 session 直到重啟
- **效能影響：** 最小（hook 只在開始時執行一次）
- **Token 影響：** 高（整個 session 中產生額外輸出）

## 授權

MIT License - 與 cc-toolkit marketplace 相同

## 作者

Dennis Liu

## 版本歷史

- **1.0.0** (2025-01-01)
  - 初始版本
  - SessionStart hook 實作
  - 反思檢查點格式
  - 主動討論機制
  - 口語化解釋和範例
  - 協作式設計完善

## 貢獻

要改進此 plugin：
1. Fork cc-toolkit repository
2. 修改 plugin 檔案
3. 徹底測試
4. 提交 pull request 並詳細說明

---

**享受更深入、更協作的開發體驗！** 🚀
