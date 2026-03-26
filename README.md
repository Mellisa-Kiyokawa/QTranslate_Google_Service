# QTranslate Google Translate Service.js — Fixed

[English](#english) | [中文](#中文)

---

## English

### What is this?

A fixed `Service.js` plugin file that restores **Google Translate** functionality in [QTranslate](https://www.portablefreeware.com/index.php?id=2237), the beloved Windows desktop translation tool.

QTranslate has been abandoned since its developer — believed to be Ukrainian — disappeared around the start of the Russia-Ukraine war. The software still works, but all translation services gradually broke as APIs changed with no one to update the plugins.

This fix brings Google Translate back to life.

### What was broken?

The original `Service.js` used an obfuscated `tk()` token generation function to authenticate requests to `translate.google.com`. Google deprecated this token mechanism, killing the plugin silently.

### What was changed?

Three changes. That's it.

1. **Endpoint**: `translate.google.com` → `translate.googleapis.com`
2. **Removed `tk()` function**: The entire broken token generator was deleted. The `translate.googleapis.com` endpoint with `client=gtx` does not require token authentication.
3. **Removed `&tk=` parameter** from all request functions (`serviceDetectLanguageRequest`, `serviceTranslateRequest`, `serviceListenRequest`).

Response parsing logic was left completely untouched — the JSON format returned by `translate.googleapis.com` is identical to the old endpoint.

### How to install

1. Download `Service.js` from this repo
2. Navigate to your QTranslate installation folder
3. Find the Google Translate service directory (usually `services/google/` or similar)
4. **Back up** the original `Service.js`
5. Replace it with the fixed version
6. Restart QTranslate

### Tested environment

- QTranslate v6.10.0 (last official release)
- Windows 10/11
- March 2026

### Limitations

- This uses Google's unofficial `client=gtx` endpoint. It works without an API key, but Google could change or block it at any time.
- For heavy usage, consider using [DeepL Desktop](https://www.deepl.com/app) as your primary translator and QTranslate as a quick-lookup companion.

### Credits

- **Original QTranslate developer** — wherever you are, thank you for building one of the most elegant translation tools ever made. 🇺🇦
- Fix generated with the assistance of [Claude](https://claude.ai) (Anthropic) — diagnosed the broken `tk()` token mechanism and identified the working alternative endpoint.

### License

This fix is provided as-is, for the QTranslate community. The original QTranslate software is freeware by QuestSoft.

---

## 中文

### 這是什麼？

這是一個修復過的 `Service.js` 外掛檔案，用來恢復 [QTranslate](https://www.portablefreeware.com/index.php?id=2237)（Windows 桌面翻譯工具）中 **Google 翻譯**的功能。

QTranslate 的開發者據信為烏克蘭人，在俄烏戰爭爆發後消失，軟體從此停止更新。程式本身仍可運行，但隨著各翻譯服務的 API 陸續改版，所有翻譯引擎逐一失效，無人維護。

這個修復讓 Google 翻譯重新復活。

### 原本壞在哪？

原版 `Service.js` 使用一個混淆過的 `tk()` token 生成函式來向 `translate.google.com` 驗證請求。Google 停用了這個 token 機制，外掛因此靜默失效。

### 改了什麼？

只改了三個地方：

1. **端點**：`translate.google.com` → `translate.googleapis.com`
2. **移除 `tk()` 函式**：整個壞掉的 token 產生器已刪除。`translate.googleapis.com` 搭配 `client=gtx` 不需要 token 驗證。
3. **移除 `&tk=` 參數**：從所有請求函式中清除（`serviceDetectLanguageRequest`、`serviceTranslateRequest`、`serviceListenRequest`）。

回應解析邏輯完全沒動——`translate.googleapis.com` 回傳的 JSON 格式與舊端點相同。

### 安裝方式

1. 從此 repo 下載 `Service.js`
2. 找到你的 QTranslate 安裝資料夾
3. 找到 Google 翻譯服務的目錄（通常是 `services/google/` 或類似路徑）
4. **備份**原本的 `Service.js`
5. 用修復版替換
6. 重新啟動 QTranslate

### 測試環境

- QTranslate v6.10.0（最後一個官方版本）
- Windows 10/11
- 2026 年 3 月

### 限制

- 這使用的是 Google 非官方的 `client=gtx` 端點，無需 API 金鑰即可運作，但 Google 隨時可能更改或封鎖。
- 大量使用建議搭配 [DeepL 桌面版](https://www.deepl.com/app) 作為主力翻譯工具，QTranslate 作為快速查詢的輔助。

### 致謝

- **QTranslate 原始開發者** —— 無論你身在何處，謝謝你打造了最優雅的翻譯工具之一。🇺🇦
- 修復過程由 [Claude](https://claude.ai)（Anthropic）協助完成 —— 診斷出壞掉的 `tk()` token 機制，並找到可用的替代端點。
