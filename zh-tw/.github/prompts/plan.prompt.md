---
description: 使用計畫範本執行實作規劃工作流程以產生設計產物。
---

使用者輸入可以直接由代理提供，或作為命令參數傳入 —— 在執行提示之前你**必須**考慮它（如果不是空的）。

使用者輸入:

$ARGUMENTS

根據作為參數提供的實作細節，請執行下列操作：

1. 從儲存庫根目錄執行 `.specify/scripts/bash/setup-plan.sh --json` 並解析 JSON 以取得 FEATURE_SPEC、IMPL_PLAN、SPECS_DIR、BRANCH。所有未來的檔案路徑皆必須為絕對路徑。
   - 在繼續之前，檢查 FEATURE_SPEC 是否包含一個 `## Clarifications` 區段，且至少含有一個 `Session` 子標題。如果缺少或顯然仍有模糊之處（含糊的形容詞、未解決的關鍵選擇），請暫停並指示使用者先執行 `/clarify` 以降低重工風險。僅在下列情況繼續：(a) 已有釐清內容，或 (b) 使用者明確覆寫（例如：「proceed without clarification」）。不要試圖自行捏造釐清內容。
2. 閱讀並分析功能規格以了解：
   - 功能需求與使用者故事
   - 功能性與非功能性需求
   - 成功標準與驗收準則
   - 任何提及的技術限制或相依性

3. 閱讀位於 `.specify/memory/constitution.md` 的章程以了解憲章要求。

4. 執行實作計畫範本：
   - 載入已複製至 IMPL_PLAN 路徑的 `.specify/templates/plan-template.md`
   - 將輸入路徑設定為 FEATURE_SPEC
   - 執行 Execution Flow（main）函式的步驟 1–9
   - 該範本為自包含並可執行
   - 遵循範本中指定的錯誤處理與門檻檢查
   - 讓範本引導在 $SPECS_DIR 中的產物產生：
     * Phase 0 產生 research.md
     * Phase 1 產生 data-model.md、contracts/、quickstart.md
     * Phase 2 產生 tasks.md
   - 將來自參數的使用者提供細節併入技術背景（Technical Context）：$ARGUMENTS
   - 隨著每個階段完成，更新進度追蹤（Progress Tracking）

5. 驗證執行已完成：
   - 檢查進度追蹤顯示所有階段皆已完成
   - 確保所有必要的產物已產生
   - 確認執行中沒有 ERROR 狀態

6. 回報結果並包含分支名稱、檔案路徑與產生的產物清單。

請對所有檔案操作使用以儲存庫根目錄為基礎的絕對路徑，以避免路徑問題。
