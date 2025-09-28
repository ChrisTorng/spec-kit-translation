# [PROJECT_NAME] 章程
<!-- 範例：規格章程、TaskFlow 章程等。 -->

## 核心原則

### [PRINCIPLE_1_NAME]
<!-- 範例：I. 以函式庫為先 -->
[PRINCIPLE_1_DESCRIPTION]
<!-- 範例：每個功能從獨立的函式庫開始；函式庫必須自成一體、可獨立測試並有文件；需要明確目的 — 不得只有組織用途的函式庫 -->

### [PRINCIPLE_2_NAME]
<!-- 範例：II. CLI 介面 -->
[PRINCIPLE_2_DESCRIPTION]
<!-- 範例：每個函式庫皆透過 CLI 暴露功能；文字輸入/輸出協定：stdin/args → stdout，錯誤 → stderr；支援 JSON 與可讀格式 -->

### [PRINCIPLE_3_NAME]
<!-- 範例：III. 先行測試（不可談判） -->
[PRINCIPLE_3_DESCRIPTION]
<!-- 範例：強制 TDD：先寫測試 → 使用者核可 → 測試失敗 → 再實作；嚴格執行紅-綠-重構循環 -->

### [PRINCIPLE_4_NAME]
<!-- 範例：IV. 整合測試 -->
[PRINCIPLE_4_DESCRIPTION]
<!-- 範例：需要整合測試的重點領域：新函式庫契約測試、契約變更、服務間通訊、共用 schema -->

### [PRINCIPLE_5_NAME]
<!-- 範例：V. 可觀測性、VI. 版本管理與破壞性變更、VII. 簡潔性 -->
[PRINCIPLE_5_DESCRIPTION]
<!-- 範例：文字 I/O 確保可除錯性；要求結構化日誌；或：MAJOR.MINOR.BUILD 格式；或：以簡單為始，遵循 YAGNI 原則 -->

## [SECTION_2_NAME]
<!-- 範例：額外限制、安全需求、效能標準等。 -->

[SECTION_2_CONTENT]
<!-- 範例：技術棧要求、合規標準、部署政策等。 -->

## [SECTION_3_NAME]
<!-- 範例：開發流程、審查流程、品質門檻等。 -->

[SECTION_3_CONTENT]
<!-- 範例：程式碼審查要求、測試門檻、部署核准流程等。 -->

## 治理
<!-- 範例：本章程優先於其他作法；修訂需有文件、核准與遷移計畫 -->

[GOVERNANCE_RULES]
<!-- 範例：所有 PR/審查必須驗證符合性；複雜性必須具理由；使用 [GUIDANCE_FILE] 作為執行時開發指引 -->

**版本**: [CONSTITUTION_VERSION] | **批准**: [RATIFICATION_DATE] | **最後修訂**: [LAST_AMENDED_DATE]
<!-- 範例：版本：2.1.1 | 批准：2025-06-13 | 最後修訂：2025-07-16 -->