# MS-NRRR 報告中心

自動產生的台股分析報告，每日 18:00 由 [MS-NRRR](https://github.com/yoshiagent) 系統更新。

## 報告

進入點：**[index.html](./index.html)**（書籤這個）

| 報告 | 內容 |
|---|---|
| [index.html](./index.html) | 主頁：市場結構 + 5 個 Agent 簡要統計 + 最終行動建議 |
| [hotflow.html](./hotflow.html) | 主流形成偵測（HotFlow）A/B/C |
| [n_pattern.html](./n_pattern.html) | N 型波段結構候選 |
| [rr.html](./rr.html) | RR 相對輪動（簡版：RS_MA20 穿越） |
| [rrr.html](./rrr.html) | RRR 共振輪動（嚴格版：Z60 折返） |
| [backtest.html](./backtest.html) | 歷史回測 |

對應 JSON 檔案提供結構化資料，供下游應用串接。

## 不對搜尋引擎收錄

本站附 `robots.txt` 阻擋爬蟲收錄。

## 系統架構

- 程式碼：[MS_N_RRR](https://github.com/yoshiagent)（私有 / 規畫中）
- 資料層：DuckDB（全市場 1,935 檔 × 4 年歷史）
- 7 Agents：Data / Market Structure / HotFlow / N-Pattern / RR / RRR / Risk-Report
- Orchestrator 串連 + 排程 18:00 / 自動 7 日備份輪轉
