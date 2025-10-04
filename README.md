# spec-kit-translation

本專案為 [spec-kit](https://github.com/github/spec-kit) 的 GitHub Copilot 英文樣版翻譯專案。

- 英文原始樣版位於 [en](en) 資料夾，內容來自官方 Copilot 樣版。
- 繁體中文翻譯位於 [zh-tw](zh-tw) 資料夾，翻譯流程採用 [mass-translate](https://github.com/ChrisTorng/mass-translate) 工具，以 [GitHub model - OpenAI GPT-4o mini](https://github.com/marketplace/models/azure-openai/gpt-4o-mini) 及 [Gemini 2.5 Flash](https://ai.google.dev/gemini-api/docs/models?hl=zh-tw#gemini-2.5-flash) 模型來進行整批翻譯。
- 翻譯文件未包含 [en/.specify/scripts](en/.specify/scripts) 資料夾，該資料夾包含 spec-kit 的執行腳本。

## 目錄結構

```
en/             # 英文原始樣版
zh-tw/          # 繁體中文翻譯
```

## 授權

MIT License

## 相關專案
- [spec-kit](https://github.com/github/spec-kit)
- [mass-translate](https://github.com/ChrisTorng/mass-translate)
