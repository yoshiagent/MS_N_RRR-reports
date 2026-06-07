# MS_N_RR/RRR Ver.A 報告中心

自動產生的台股分析報告，由 [MS_N_RR/RRR Ver.A](https://github.com/yoshiagent) 系統每日 3 時段更新（14:45 / 18:30 / 21:30，22:45 為 safety net）。

## 報告

進入點：**[index.html](./index.html)**（書籤這個）

### 核心入口

| 報告 | 內容 |
|---|---|
| [index.html](./index.html) | 主頁：市場結構 + 全套 Agent 簡要 + 最終行動建議 |
| [stock_ops.html](./stock_ops.html) | ⭐ 操作 Agent — 今日操作主入口，5 階段建議 + S/A/B 風險分級 |
| [system_flow.html](./system_flow.html) | 系統流程圖（資料流 + Agent + 排程） |

### 結構偵測層

| 報告 | 內容 |
|---|---|
| [shsl.html](./shsl.html) | 📐 SHSL — 波段轉折引擎（3 階段事件驅動 SH/SL × 三時段 + Wave State + 結構標籤） |
| [box_structure.html](./box_structure.html) | 📦 股票箱結構分析 |
| [n_shape.html](./n_shape.html) | 🔁 多時段箱型狀態 |
| [wyckoff_phase.html](./wyckoff_phase.html) | 🎯 Wyckoff Phase Agent（10 phases × 9 events） |

### 評分層

| 報告 | 內容 |
|---|---|
| [chip_score.html](./chip_score.html) | 🪙 籌碼評分（外資/投信/自營/融資/融券 5 維） |
| [fundamental_score.html](./fundamental_score.html) | 🧪 基本面評分（5 維 × 各 20 分） |
| [accumulation_pool.html](./accumulation_pool.html) | ⛰️ 底部轉強股池（Wyckoff Accumulation） |
| [distribution_score.html](./distribution_score.html) | 🌋 派發評分（Wyckoff Distribution） |
| [rotation_signals.html](./rotation_signals.html) | 🔄 換股建議（DS×AS 對撞） |

### 主流偵測層

| 報告 | 內容 |
|---|---|
| [hotflow.html](./hotflow.html) | 🔥 主流形成偵測 A/B/C |
| [sector_rotation.html](./sector_rotation.html) | 🔄 族群輪動（RRG + lifecycle heatmap） |
| [mainstream_pool.html](./mainstream_pool.html) | 🏆 主流股池 |
| [strong_stocks.html](./strong_stocks.html) | 💪 強勢股池 |

### 配對 / 對照層

| 報告 | 內容 |
|---|---|
| [rr.html](./rr.html) | 相對強度輪動 |
| [rrr.html](./rrr.html) | RRR 共振輪動 |
| [rrr_resonance.html](./rrr_resonance.html) | 共振配對 |
| [custom_pool.html](./custom_pool.html) | 📋 自選股池 |
| [fs_compare.html](./fs_compare.html) | 📊 Feature Store 對照（baseline vs UAA tuned） |

對應 JSON 檔案提供結構化資料，供下游應用串接。

## 不對搜尋引擎收錄

本站附 `robots.txt` 阻擋爬蟲收錄。

## 系統架構（2026-06 版）

- 程式碼：[MS_N_RRR](https://github.com/yoshiagent/MS_N_RRR)（私有）
- 資料層：DuckDB + Feature Store（衍生特徵集中查詢平面）
- 工作流層：Watermark + atomic_write + require_fresh（時序保證三道防線）
- ~30 個 Agent：Data / Market / HotFlow / N-Pattern / SHSL / Box / Wyckoff /
  Chip / Fundamental / Accumulation / Distribution / Custom / Stock-Ops / ...
- Adaptive：UAA Universal Adaptive Agent — 5 個註冊 adapter (chip/fund/acc/dist/wyckoff)
- Orchestrator 串連 + Windows Task Scheduler 3 時段排程
