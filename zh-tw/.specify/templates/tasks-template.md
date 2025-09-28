# 任務：[功能名稱]

**輸入**：來自 `/specs/[###-feature-name]/` 的設計文件
**先決條件**：plan.md (必要)、research.md、data-model.md、contracts/

## 執行流程 (主要)
```
1. 從功能目錄載入 plan.md
   → 若未找到：ERROR "No implementation plan found"
   → 擷取：技術堆疊、程式庫、結構
2. 載入選用設計文件：
   → data-model.md：擷取實體 → 模型任務
   → contracts/：每個檔案 → 契約測試任務
   → research.md：擷取決策 → 設定任務
3. 依類別產生任務：
   → 設定：專案初始化、相依性、程式碼檢查
   → 測試：契約測試、整合測試
   → 核心：模型、服務、CLI 命令
   → 整合：資料庫、中介軟體、日誌記錄
   → 優化：單元測試、效能、文件
4. 套用任務規則：
   → 不同檔案 = 標記 [P] 表示平行
   → 相同檔案 = 循序 (無 [P])
   → 測試先於實作 (TDD)
5. 循序編號任務 (T001, T002...)
6. 產生相依性圖
7. 建立平行執行範例
8. 驗證任務完整性：
   → 所有契約都有測試嗎？
   → 所有實體都有模型嗎？
   → 所有端點都已實作嗎？
9. 回傳：成功 (任務已準備好執行)
```

## 格式：`[ID] [P?] Description`
- **[P]**：可平行執行 (不同檔案，無相依性)
- 在說明中包含確切的檔案路徑

## 路徑慣例
- **單一專案**：儲存庫根目錄下的 `src/`、`tests/`
- **Web 應用程式**：`backend/src/`、`frontend/src/`
- **行動應用程式**：`api/src/`、`ios/src/` 或 `android/src/`
- 下面顯示的路徑假設為單一專案 - 請根據 plan.md 結構進行調整

## 階段 3.1：設定
- [ ] T001 依據實作計畫建立專案結構
- [ ] T002 使用 [framework] 相依性初始化 [language] 專案
- [ ] T003 [P] 設定程式碼檢查與格式化工具

## 階段 3.2：測試先行 (TDD) ⚠️ 必須在 3.3 之前完成
**關鍵：這些測試必須撰寫，並且在任何實作之前必須失敗**
- [ ] T004 [P] 在 tests/contract/test_users_post.py 中進行 POST /api/users 的契約測試
- [ ] T005 [P] 在 tests/contract/test_users_get.py 中進行 GET /api/users/{id} 的契約測試
- [ ] T006 [P] 在 tests/integration/test_registration.py 中進行使用者註冊的整合測試
- [ ] T007 [P] 在 tests/integration/test_auth.py 中進行身份驗證流程的整合測試

## 階段 3.3：核心實作 (僅在測試失敗之後)
- [ ] T008 [P] src/models/user.py 中的使用者模型
- [ ] T009 [P] src/services/user_service.py 中的 UserService CRUD
- [ ] T010 [P] src/cli/user_commands.py 中的 CLI --create-user
- [ ] T011 POST /api/users 端點
- [ ] T012 GET /api/users/{id} 端點
- [ ] T013 輸入驗證
- [ ] T014 錯誤處理與日誌記錄

## 階段 3.4：整合
- [ ] T015 將 UserService 連接到資料庫
- [ ] T016 身份驗證中介軟體
- [ ] T017 請求/回應日誌記錄
- [ ] T018 CORS 與安全標頭

## 階段 3.5：優化
- [ ] T019 [P] 在 tests/unit/test_validation.py 中為驗證編寫單元測試
- [ ] T020 效能測試 (<200ms)
- [ ] T021 [P] 更新 docs/api.md
- [ ] T022 移除重複程式碼
- [ ] T023 執行 manual-testing.md

## 相依性
- 測試 (T004-T007) 先於實作 (T008-T014)
- T008 阻擋 T009、T015
- T016 阻擋 T018
- 實作先於優化 (T019-T023)

## 平行範例
```
# 同時啟動 T004-T007：
任務：「在 tests/contract/test_users_post.py 中進行 POST /api/users 的契約測試」
任務：「在 tests/contract/test_users_get.py 中進行 GET /api/users/{id} 的契約測試」
任務：「在 tests/integration/test_registration.py 中進行註冊的整合測試」
任務：「在 tests/integration/test_auth.py 中進行身份驗證的整合測試」
```

## 備註
- [P] 任務 = 不同檔案，無相依性
- 在實作之前驗證測試失敗
- 每個任務完成後提交
- 避免：模糊的任務、相同檔案衝突

## 任務生成規則
*在 main() 執行期間套用*

1. **來自契約**：
   - 每個契約檔案 → 契約測試任務 [P]
   - 每個端點 → 實作任務
   
2. **來自資料模型**：
   - 每個實體 → 模型建立任務 [P]
   - 關係 → 服務層任務
   
3. **來自使用者故事**：
   - 每個故事 → 整合測試 [P]
   - 快速入門情境 → 驗證任務

4. **排序**：
   - 設定 → 測試 → 模型 → 服務 → 端點 → 優化
   - 相依性阻擋平行執行

## 驗證清單
*關卡：在回傳之前由 main() 檢查*

- [ ] 所有契約都有對應的測試
- [ ] 所有實體都有模型任務
- [ ] 所有測試都在實作之前
- [ ] 平行任務確實獨立
- [ ] 每個任務指定確切的檔案路徑
- [ ] 沒有任務修改與另一個 [P] 任務相同的檔案