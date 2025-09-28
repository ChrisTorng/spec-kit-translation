
# 實作計畫：[FEATURE]

**分支**: `[###-feature-name]` | **日期**: [DATE] | **規格**: [link]  
**輸入**: 來自 `/specs/[###-feature-name]/spec.md` 的功能規格

## 執行流程 (/plan 指令範圍)
```
1. 從輸入路徑載入功能規格
   → 若找不到: ERROR "No feature spec at {path}"
2. 填寫技術背景（掃描 NEEDS CLARIFICATION）
   → 從檔案系統結構或環境判斷專案類型（web=frontend+backend、mobile=app+api）
   → 根據專案類型設定架構決策
3. 根據憲章文件內容填寫憲章檢查（Constitution Check）區段。
4. 評估下方的憲章檢查區段
   → 若存在違規：記錄於複雜度追蹤（Complexity Tracking）
   → 若無法提出合理化：ERROR "Simplify approach first"
   → 更新進度追蹤：初始憲章檢查
5. 執行第 0 階段 → research.md
   → 若仍有 NEEDS CLARIFICATION：ERROR "Resolve unknowns"
6. 執行第 1 階段 → contracts、data-model.md、quickstart.md、代理程式專用範本檔案（例如 `CLAUDE.md` 用於 Claude Code、`.github/copilot-instructions.md` 用於 GitHub Copilot、`GEMINI.md` 用於 Gemini CLI、`QWEN.md` 用於 Qwen Code 或 `AGENTS.md` 用於 opencode）。
7. 重新評估憲章檢查區段
   → 若出現新違規：重構設計，回到第 1 階段
   → 更新進度追蹤：設計後憲章檢查
8. 規劃第 2 階段 → 描述任務產生方法（請勿建立 tasks.md）
9. 停止 - 準備好接受 /tasks 指令
```

**重要**: /plan 指令在第 7 步驟停止。第 2-4 階段由其他指令執行：
- 第 2 階段：/tasks 指令建立 tasks.md
- 第 3-4 階段：實作執行（手動或透過工具）

## 摘要
[從功能規格擷取：主要需求 + 來自研究的技術方法]

## 技術背景
**語言/版本**： [例如 Python 3.11、Swift 5.9、Rust 1.75 或 NEEDS CLARIFICATION]  
**主要相依**： [例如 FastAPI、UIKit、LLVM 或 NEEDS CLARIFICATION]  
**儲存**： [如適用，例：PostgreSQL、CoreData、檔案系統 或 N/A]  
**測試**： [例如 pytest、XCTest、cargo test 或 NEEDS CLARIFICATION]  
**目標平台**： [例如 Linux server、iOS 15+、WASM 或 NEEDS CLARIFICATION]  
**專案類型**： [single/web/mobile - 決定原始碼結構]  
**效能目標**： [領域特定，例：1000 req/s、10k lines/sec、60 fps 或 NEEDS CLARIFICATION]  
**限制**： [領域特定，例：<200ms p95、<100MB 記憶體、離線可用 或 NEEDS CLARIFICATION]  
**規模/範圍**： [領域特定，例：10k 使用者、1M LOC、50 個畫面 或 NEEDS CLARIFICATION]

## 憲章檢查
*門檻：必須在第 0 階段研究前通過。設計後（第 1 階段）須重新檢查。*

[依據憲章檔案決定的門檻]

## 專案結構

### 文件（此功能）
```
specs/[###-feature]/
├── plan.md              # 此檔案（/plan 指令輸出）
├── research.md          # 第 0 階段輸出（/plan 指令）
├── data-model.md        # 第 1 階段輸出（/plan 指令）
├── quickstart.md        # 第 1 階段輸出（/plan 指令）
├── contracts/           # 第 1 階段輸出（/plan 指令）
└── tasks.md             # 第 2 階段輸出（/tasks 指令 - 非 /plan 所建立）
```

### 原始程式碼（儲存庫根目錄）
<!-- 需要執行的動作：將下方的佔位目錄樹替換為此功能的具體結構。 刪除未使用的選項，並將所選結構擴充為實際路徑（例如：apps/admin, packages/something）。 提交的方案中不得包含「選項」標籤。 -->
```
# [若未使用請移除] 選項 1：單一專案（預設）
src/
├── models/
├── services/
├── cli/
└── lib/

tests/
├── contract/
├── integration/
└── unit/

# [若未使用請移除] 選項 2：Web 應用（當偵測到 "frontend" + "backend" 時）
backend/
├── src/
│   ├── models/
│   ├── services/
│   └── api/
└── tests/

frontend/
├── src/
│   ├── components/
│   ├── pages/
│   └── services/
└── tests/

# [若未使用請移除] 選項 3：Mobile + API（當偵測到 "iOS/Android" 時）
api/
└── [同上方 backend 結構]

ios/ 或 android/
└── [平台特定結構：功能模組、UI 流程、平台測試]
```

**架構決策**： [記錄選定的結構並參照上方實際的目錄路徑]

## 第 0 階段：大綱與研究
1. **從上方技術背景擷取未知項目**：
   - 對於每個 NEEDS CLARIFICATION → 建立研究任務
   - 對於每個相依 → 最佳實務調查任務
   - 對於每個整合 → 模式調查任務

2. **產生並派遣研究代理**：
   ```
   對於技術背景中的每個未知：
     任務: "Research {unknown} for {feature context}"
   對於每個技術選擇：
     任務: "Find best practices for {tech} in {domain}"
   ```

3. **在 research.md 中彙整調查結果，使用格式：**
   - 決策： [所選擇項目]
   - 理由： [選擇原因]
   - 考量的替代方案： [評估過的其他選項]

**輸出**： research.md，並解決所有 NEEDS CLARIFICATION

## 第 1 階段：設計與合約
*先決條件：research.md 完成*

1. **從功能規格擷取實體（entities）** → `data-model.md`：
   - 實體名稱、欄位、關聯
   - 從需求推導的驗證規則
   - 若適用：狀態轉換

2. **根據功能需求產生 API 合約**：
   - 對於每個使用者動作 → 定義 endpoint
   - 使用標準 REST / GraphQL 模式
   - 輸出 OpenAPI / GraphQL schema 至 `/contracts/`

3. **從合約產生合約測試**：
   - 每個 endpoint 一個測試檔案
   - 斷言請求/回應結構
   - 測試應該失敗（尚無實作）

4. **從使用者故事擷取測試情境**：
   - 每個故事 → 一個整合性測試情境
   - Quickstart 測試 = 故事驗證步驟

5. **逐步更新代理程式檔案**（O(1) 操作）：
   - 執行 `.specify/scripts/bash/update-agent-context.sh copilot`
     **重要**：請完全依照上列命令執行。不要新增或移除任何參數。
   - 若檔案已存在：僅加入本次計畫中的新技術
   - 保留標記間的手動新增內容
   - 更新近期變更（保留最近 3 次）
   - 為了 token 效率，檔案維持在 150 行以內
   - 輸出至儲存庫根目錄

**輸出**： data-model.md、/contracts/*、會失敗的測試、quickstart.md、代理程式專用檔案

## 第 2 階段：任務規劃方法
*本段描述 /tasks 指令將執行的內容 — 不要在 /plan 期間執行*

**任務產生策略**：
- 載入 `.specify/templates/tasks-template.md` 作為基底
- 根據第 1 階段設計文件（合約、資料模型、quickstart）產生任務
- 每個合約 → 合約測試任務 [P]
- 每個實體 → 模型建立任務 [P]
- 每個使用者故事 → 整合測試任務
- 產生使測試通過的實作任務

**排序策略**：
- TDD 順序：先測試後實作
- 相依順序：模型先於服務，服務先於 UI
- 標註 [P] 為可平行執行（獨立檔案）

**預估輸出**：在 tasks.md 中產生 25-30 項編號且有順序的任務

**重要**：此階段由 /tasks 指令執行，而非 /plan

## 第 3 階段起：後續實作
*以下階段超出 /plan 指令範圍*

**第 3 階段**：任務執行（/tasks 指令建立 tasks.md）  
**第 4 階段**：實作（依 tasks.md 執行）  
**第 5 階段**：驗證（執行測試、執行 quickstart.md、效能驗證）

## 複雜度追蹤
*僅在憲章檢查有違規且需說明時填寫*

| 違規 | 為何需要 | 為何捨棄較簡單替代方案 |
|-----------|------------|-------------------------------------|
| [例如，第 4 個專案] | [當前需求] | [為何 3 個專案不足以應對] |
| [例如，Repository pattern] | [具體問題] | [為何直接存取 DB 不足以應對] |


## 進度追蹤
*此核取清單會在執行流程中更新*

**階段狀態**：
- [ ] 第 0 階段：研究完成（/plan 指令）
- [ ] 第 1 階段：設計完成（/plan 指令）
- [ ] 第 2 階段：任務規劃完成（/plan 指令 - 僅描述方法）
- [ ] 第 3 階段：任務已產生（/tasks 指令）
- [ ] 第 4 階段：實作完成
- [ ] 第 5 階段：驗證通過

**門檻狀態**：
- [ ] 初始憲章檢查：通過
- [ ] 設計後憲章檢查：通過
- [ ] 所有 NEEDS CLARIFICATION 已解決
- [ ] 複雜度偏差已記錄

---
*根據 Constitution v2.1.1 - 參見 `/memory/constitution.md`*