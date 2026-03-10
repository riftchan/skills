---
name: auto-memory-manager
description: 自動化管理專案的長期記憶 (memory.md) 與每日日誌 (memory-YYYY-MM-DD.md)。當使用者提到「記憶」、「進度」或需要「自動管理對話狀態」時，必須嚴格執行此協議。
---

# Auto-Memory Manager

此技能將對話的脈絡與技術細節「持久化」，讓 AI 具備連續性的工作能力。

## 核心行為協議 (Core Protocols)

### 1. 啟動即喚醒 (Auto-Resume on Research)
在每一輪對話的 **研究階段 (Research Phase)**，AI 必須：
- 自動讀取根目錄下的 `memory.md` 以獲取長期目標。
- 自動讀取當日或最近一日的 `memory-YYYY-MM-DD.md`。
- 向使用者回報：「我已讀取記憶，目前進度停在...，接下來準備執行...」。

### 2. 執行中即時紀錄 (Real-time Tracking on Execution)
在 **執行階段 (Execution Phase)**，每當完成以下任一情境，必須主動調用 `run_shell_command` 或 `write_file` 將紀錄追加至當日的 `memory-YYYY-MM-DD.md`：
- **數據變動**：成功執行抓取腳本並產生新的 JSON/CSV 數據文件時。
- **文件修改**：修改了代碼、配置或範本文件（如 `.tsx`, `.py`, `.json`）時。
- **環境變更**：安裝了新的依賴、修改了環境變數或專案結構時。
- **渲染成果**：產出了影片、圖片或預覽圖時（記錄其路徑與參數）。
- **錯誤修復**：遇到技術報錯並成功解決後，記錄錯誤原因與解決方案，以防再犯。

### 3. 決策後更新目標 (Update Goals on Strategy)
當使用者在 **策略階段 (Strategy Phase)** 確認了新的計畫或修改了現有目標時：
- 必須同步更新 `memory.md` 中的 `Active Goals` 列表。

### 4. 結案總結 (End-of-Session Summarization)
在準備回覆使用者的最後一個工具調用中，若今日任務有實質進展：
- 提煉今日日誌中的技術發現，更新至 `memory.md` 的 `Technical Context`。

## 記憶文件結構要求

### memory-YYYY-MM-DD.md (每日日誌)
- 格式：`[HH:mm] **Phase**: 具體操作描述 (產出物路徑)`
- 範例：`[14:25] **Act**: 執行 fetch_data.py (data.json)`

### memory.md (長期記憶)
- **Core Objective**: 項目最終目標。
- **Active Goals**: 當前待辦事項（使用 [ ] 和 [x]）。
- **Technical Context**: 腳本參數、數據結構、依賴版本等關鍵技術資訊。
- **Key Files**: 核心文件清單。
