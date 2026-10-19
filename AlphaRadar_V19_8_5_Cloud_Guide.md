# Alpha Radar V19.8.6 — Cloud 操作指南

## 升級後

1. 覆蓋 V19.8.6 程式碼，保留 `data/` 與 Secrets。
2. 開啟完整系統，確認標題顯示 `Alpha Radar V19.8.6`。
3. 既有 S1～S6 Stage Gate 紀錄會沿用，不要清 checkpoint。
4. 「選股與規劃」預設可查看 **V19.8.6凍結最佳化候選（前瞻研究）**；可隨時切回「原模型對照」。

## 凍結候選

- 5日：近一年高點位置 100%（實驗性）。
- 20日：近一年高點位置 100%（主要候選）。
- 60日：成交金額容量 70%＋近一年高點位置 30%（次要候選）。
- 市場 gate 為 `CAUTION` 時：候選顯示現金／不新增部位。

這些是排序係數，不是資金配置比例或上漲機率。

## S7 操作

S7 = 150檔 × 24個不同時間點；股票數不再增加。

- 日期 seed：`271828`
- 抽樣：`stratified`
- 自動排除 S4/S6 已用過的精確基準日
- 沿用 S6 的150檔歷史快取

**先按 B。** 若 S6 快取完整度仍達門檻，S7 不需重新下載；只有 B 顯示資料完整度不足時才按 A 補齊後再按 B。

S7 結果會在「V19.8.6最佳化候選：多角度穩健性檢查」顯示 bootstrap、leave-one-out、前後半期、固定假說排名及 confirmation gate。

## 如何看結果

- `S7_HISTORICAL_CROSSCHECK_PASS_NOT_FUTURE_HOLDOUT`：20/60日核心候選通過不同精確日期的歷史交叉確認，但仍不是未來盲測。
- `S7_HISTORICAL_CROSSCHECK_NOT_CONFIRMED`：至少一個核心週期不穩定；**不要在 S7 上立即重新調權再測 S7**，否則會把確認集重新變成開發集。
- 5日另看 `EXPERIMENTAL_SHORT_HORIZON_NEEDS_FORWARD_CONFIRMATION`，不因20/60日通過就自動視為已確認。

## Stage Gate

S1～S7 仍把「執行完成」與「研究完整」分開。少量 outcome 缺值可以是 `STAGE_COMPLETE + RESEARCH_PARTIAL`；缺值不補成0。下載完整度、基準日數、所有日期×週期運算或報告彙整未完成，才會真正阻擋階段完成。
