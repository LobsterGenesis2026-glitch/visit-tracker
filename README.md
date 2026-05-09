# 📋 Client Visit Tracker

A lightweight, touch-optimized client visit management tool designed for iPad. Single HTML file, zero installation, works offline. Add to home screen for a native-like full-screen app experience.

![Platform](https://img.shields.io/badge/Platform-iPad%20%7C%20iPhone%20%7C%20Web-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![No Backend](https://img.shields.io/badge/Backend-None-lightgrey)

[繁體中文](./README.md) | **English**

---

## ✨ Features

- 🎯 **Single-file deployment** — All HTML / CSS /JavaScript in one file. No build step, no backend.
- 📱 **iPad touch-optimized** — Large buttons (56px minimum), smooth gestures, Bootstrap 5-inspired UI.
- 🔔 **Smart reminder system** — Automatically calculates due dates and shows a prominent alert on launch.
- 💾 **Local storage** — All data stored in browser localStorage. No account needed.
- 📤 **JSON backup & restore** — One-tap export to iPad's Files app for backup or device migration.
- 🌐 **Offline-ready** — Works fully offline once added to home screen.
- 🎨 **Modern UI** — Card-based design, color-coded status, visual progress bars.

---

## 🚀 Quick Start

### Option 1: Cloud hosting (Recommended)

The most stable deployment method. Allows adding to home screen for long-term use.

#### Using Netlify Drop (30-second deploy)

1. Visit [app.netlify.com/drop](https://app.netlify.com/drop)
2. Drag and drop `client-visit-tracker.html`
3. Open the resulting URL in iPad Safari
4. Tap **Share** → **Add to Home Screen**

#### Using GitHub Pages (free, permanent)

```bash
# 1. Create a new repository
# 2. Upload the file (rename to index.html)
git init
git add index.html
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/visit-tracker.git
git push -u origin main

# 3. Enable Pages in Settings → Pages
# 4. Access at: https://YOUR_USERNAME.github.io/visit-tracker/
```

### Option 2: Open via Files app (Standalone use)

1. Transfer `client-visit-tracker.html` to your iPad (AirDrop / Email / iCloud Drive)
2. Open the **Files** app and long-press the file
3. Select **Share** → **Copy to Safari**

> ⚠️ This method does not support Add to Home Screen. You'll need to reopen via Files app each time.

---

## 🎯 Core Features

### 1. Project Management

Create, edit, and delete client visit projects. Each project includes:

| Field | Description |
|---|---|
| Project Name | Client or visit target name |
| Description | Contact info, address, additional notes |
| Type | Client / Prospect / Partner / Vendor / Other |
| Last Visit Date | The most recent visit date |
| Visit Cycle | Number + Unit (days / weeks / months), auto-converted to days |
| Cycle Type | Minimum or Maximum cycle |
| Alert Lead Days | How many days before due date to start alerting |

### 2. Three-Tier Status System

Each project's status is automatically calculated:

- 🟢 **Normal** — Not yet in alert window. No action needed.
- 🟡 **Reminding** — In alert window. Schedule a visit soon.
- 🔴 **Overdue** — Past the visit cycle. Action required immediately.

### 3. Reminder Logic

```
Alert Trigger Date = Last Visit + Cycle - Alert Lead Days
Due Date           = Last Visit + Cycle

When today >= Alert Trigger Date → Status: Reminding
When today >= Due Date           → Status: Overdue
```

### 4. Startup Alert

On every app launch, if any projects are in **Reminding** or **Overdue** status, a prominent full-screen alert appears listing all projects needing attention — so nothing slips through the cracks.

### 5. Data Backup

Settings → **Backup Data** → Auto-downloads a JSON file to iPad's Files app.  
Filename format: `visit-tracker-YYYYMMDD.json`

Backup files can be restored anytime via **Import Backup**, useful for:
- Migrating to a new iPad
- Manual sync between multiple devices
- Safeguarding before major changes

---

## 📐 Technical Specs

| Item | Spec |
|---|---|
| File Size | Single HTML file, ~35 KB |
| Tech Stack | Vanilla HTML5 + CSS3 + JavaScript (no framework) |
| Storage | Browser localStorage (~5 MB limit) |
| Browser Support | Safari 14+ / Chrome / Edge / Firefox |
| Offline | ✅ Full offline support after adding to home screen |
| Backend | ❌ None |

---

## 🎨 iPad Optimization Details

Special handling for iPad Safari and PWA standalone mode:

- ✅ Complete Apple Mobile Web App meta tag configuration
- ✅ Safe Area support (notch, Home Indicator regions)
- ✅ Minimum 56px touch targets on all interactive elements
- ✅ 16px minimum font size on form controls (prevents iOS auto-zoom)
- ✅ Custom Confirm Dialog (replaces native confirm blocked in PWA mode)
- ✅ Custom Toast notifications (replaces native alerts)
- ✅ Disabled auto-correction and auto-capitalization for input fields
- ✅ Numeric keyboard for number inputs via `inputmode="numeric"`
- ✅ Momentum scrolling inside modals via `-webkit-overflow-scrolling`

---

## 📂 Project Structure

```
visit-tracker/
├── client-visit-tracker.html   # Main app (single file, all features)
├── README.md                    # Chinese documentation
└── README.en.md                 # This file
```

---

## 🔧 Customization

To change defaults, edit the JavaScript section in the HTML file:

```javascript
// Client type options (modify <select id="fType"> in HTML)
// Default: Client / Prospect / Partner / Vendor / Other

// Default alert lead days (modify the value attribute of #fAlert)
<input type="number" id="fAlert" value="7">

// localStorage key (change if running multiple instances)
var STORAGE_KEY = 'visitTracker_v2';
```

---

## 🗺️ Roadmap

### Completed ✅
- [x] Basic CRUD operations
- [x] iPad touch optimization
- [x] Startup alert system
- [x] JSON backup & restore
- [x] PWA full-screen support

### Planned 🚧
- [ ] iOS push notifications (requires native app or Capacitor wrapper)
- [ ] Visit history log (record each visit)
- [ ] Cloud sync (iCloud / Google Drive)
- [ ] Report export (PDF / Excel)
- [ ] Map integration (Apple Maps / Google Maps)
- [ ] Multi-language support (English / Simplified Chinese)

---

## 🆚 Upgrading to a Native iOS App

To publish on the App Store or enable push notifications, consider these paths:

| Path | Tools | Time | Best For |
|---|---|---|---|
| **Enhanced PWA** | Service Worker + Manifest | 1 day | Personal use, no App Store |
| **Wrapped App** | [Capacitor](https://capacitorjs.com/) | 1-2 weeks | Limited budget, App Store goal |
| **Native Rewrite** | SwiftUI + SwiftData | 1-3 months | Commercial product, max performance |

Detailed steps coming soon in the project Wiki.

---

## ❓ FAQ

**Q: Will my data be lost?**  
A: Data is stored in browser localStorage. It generally persists, but be aware:
- Clearing Safari browsing data → data will be erased
- Long inactivity (7+ days) → iOS may clean up data (PWA mode is more stable)
- iPad reset or migration → data will be cleared

**Recommendation**: Periodically use the **Backup Data** feature to save a JSON copy.

**Q: Can multiple users share data?**  
A: Currently single-device only. For team collaboration, you can:
- Place the JSON backup on a shared cloud drive
- Or upgrade to a backend-enabled version

**Q: Buttons don't respond on iPad. What's wrong?**  
A: Please verify:
1. Opened in **Safari** (not Chrome or Firefox)
2. Added to home screen and launched from the home screen icon
3. iPadOS version 14 or higher

**Q: Where do I find the downloaded backup file?**  
A: Open the **Files** app on iPad → Browse → **Downloads** folder.

**Q: Can I customize the project types?**  
A: Yes. Edit the `<select id="fType">` element in the HTML to add or rename options. Make sure to also update the `TYPE_EMOJI` object in the JavaScript if you want custom emojis.

---

## 📄 License

MIT License — Free for personal and commercial use.

---

## 🙏 Acknowledgments

- Design inspired by Apple Human Interface Guidelines
- Bootstrap 5 design system
- All users who provided feedback

---

## 📮 Contact & Contributing

Issues and Pull Requests are welcome!

If this tool helps you, please give it a ⭐ Star to show your support!
# visit-tracker
visit-tracker

# 📋 客戶拜訪追蹤工具 (Client Visit Tracker)

一個專為 iPad 觸控操作設計的輕量化客戶拜訪管理工具。單一 HTML 檔案、零安裝、離線可用，加入主畫面後即可全螢幕執行，提供類原生 App 的使用體驗。

![Platform](https://img.shields.io/badge/Platform-iPad%20%7C%20iPhone%20%7C%20Web-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![No Backend](https://img.shields.io/badge/Backend-None-lightgrey)

**繁體中文** | [English](./README.en.md)

---

## ✨ 主要特色

- 🎯 **單檔部署** — 所有 HTML / CSS / JavaScript 整合於一個檔案，無需編譯、無需後端
- 📱 **iPad 觸控優化** — 大尺寸按鈕（最小 56px）、流暢手勢、Bootstrap 5 風格介面
- 🔔 **智慧預警系統** — 自動計算拜訪到期日，啟動時跳出顯眼預警卡片
- 💾 **本機儲存** — 所有資料儲存於瀏覽器 localStorage，不需註冊帳號
- 📤 **JSON 備份／還原** — 一鍵下載資料到 iPad「檔案」App，可還原與遷移
- 🌐 **離線可用** — 加入主畫面後即可離線使用
- 🎨 **美觀介面** — 現代化卡片設計、狀態色彩標記、進度條視覺化

---

## 🚀 快速開始

### 方法 1：透過雲端託管（推薦）

最穩定的部署方式，可加入主畫面並長期使用。

#### 使用 Netlify Drop（30 秒部署）

1. 開啟 [app.netlify.com/drop](https://app.netlify.com/drop)
2. 拖曳 `client-visit-tracker.html` 上傳
3. 取得網址後，在 iPad Safari 開啟
4. 點擊「分享」→「加入主畫面」

#### 使用 GitHub Pages（免費永久）

```bash
# 1. 新建 Repository
# 2. 上傳檔案並改名為 index.html
git init
git add index.html
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/visit-tracker.git
git push -u origin main

# 3. 到 Settings → Pages 啟用 GitHub Pages
# 4. 取得網址：https://YOUR_USERNAME.github.io/visit-tracker/
```

### 方法 2：透過「檔案」App 開啟（單機使用）

1. 將 `client-visit-tracker.html` 傳到 iPad（AirDrop / Email / iCloud Drive）
2. 打開「檔案」App，長按檔案
3. 選「分享」→「拷貝到 Safari」

> ⚠️ 此方法無法加入主畫面，每次都需要重新從檔案 App 開啟。

---

## 🎯 核心功能

### 1. 專案管理

新增、編輯、刪除客戶拜訪專案，每個專案包含：

| 欄位 | 說明 |
|---|---|
| 專案名稱 | 客戶或拜訪對象名稱 |
| 備註說明 | 聯絡人、地址、附加資訊 |
| 類型 | 客戶 / 潛在客戶 / 合作夥伴 / 廠商 / 其他 |
| 最近拜訪日期 | 最後一次拜訪的日期 |
| 拜訪週期 | 數值 + 單位（天 / 週 / 個月），自動換算為天數 |
| 週期類型 | 最短週期 或 最長週期 |
| 提前提醒天數 | 在到期日前幾天開始顯示提醒 |

### 2. 三層狀態系統

每個專案會根據設定自動計算狀態：

- 🟢 **正常** — 尚未進入提醒區間，無需動作
- 🟡 **提醒中** — 已進入提醒區間，建議盡快預約
- 🔴 **逾期** — 已超過拜訪週期，需立即處理

### 3. 預警邏輯

```
提醒啟動日 = 上次拜訪日 + 拜訪週期 - 提前提醒天數
到期日     = 上次拜訪日 + 拜訪週期

當「今天 ≥ 提醒啟動日」時 → 進入提醒區間
當「今天 ≥ 到期日」時     → 逾期
```

### 4. 啟動警示

每次開啟 App 時，若有專案進入提醒或逾期狀態，會自動跳出**顯眼的全螢幕警示視窗**，列出所有需要關注的專案，避免遺漏。

### 5. 資料備份

設定頁 → 備份資料 → 自動下載 JSON 檔到 iPad「檔案」App  
檔名格式：`visit-tracker-YYYYMMDD.json`

備份檔可隨時透過「匯入備份」還原，方便：
- 換新 iPad 時遷移資料
- 多裝置間手動同步
- 重大變更前先備份保險

---

## 📐 技術規格

| 項目 | 說明 |
|---|---|
| 檔案大小 | 單一 HTML 檔，約 35 KB |
| 技術棧 | 原生 HTML5 + CSS3 + Vanilla JavaScript（無框架） |
| 資料儲存 | Browser localStorage（約 5MB 上限） |
| 瀏覽器支援 | Safari 14+ / Chrome / Edge / Firefox |
| 離線支援 | ✅ 加入主畫面後可離線使用 |
| 後端需求 | ❌ 無 |

---

## 🎨 iPad 優化細節

針對 iPad Safari 與 PWA 全螢幕模式的特殊處理：

- ✅ Apple Mobile Web App meta 標籤完整配置
- ✅ Safe Area 支援（瀏海、Home Indicator 區域）
- ✅ 所有可點擊元件最小 56px 觸控區域
- ✅ 表單元件統一 16px 字級（防止 iOS 自動縮放頁面）
- ✅ 自製 Confirm Dialog（取代被 PWA 模式擋住的原生 confirm）
- ✅ 自製 Toast 提示（取代原生 alert）
- ✅ 關閉中文輸入的自動修正與大寫
- ✅ 數字輸入欄位呼叫 iOS 數字鍵盤
- ✅ Modal 內支援慣性滾動

---

## 📂 專案結構

```
visit-tracker/
├── client-visit-tracker.html   # 主程式（單一檔案包含所有功能）
└── README.md                    # 本說明文件
```

---

## 🔧 自訂配置

如需調整預設值，可直接修改 HTML 檔內的 JavaScript 區段：

```javascript
// 客戶類型選項（在 HTML 的 <select id="fType"> 內修改）
// 預設：客戶 / 潛在客戶 / 合作夥伴 / 廠商 / 其他

// 預設提醒天數（修改 #fAlert 的 value 屬性）
<input type="number" id="fAlert" value="7">

// localStorage 儲存 key（如需多套並行）
var STORAGE_KEY = 'visitTracker_v2';
```

---

## 🗺️ Roadmap

### 已完成 ✅
- [x] 基本 CRUD 功能
- [x] iPad 觸控優化
- [x] 啟動預警系統
- [x] JSON 備份／還原
- [x] PWA 全螢幕支援

### 規劃中 🚧
- [ ] iOS 推播通知（需轉為原生 App 或 Capacitor 套殼）
- [ ] 拜訪歷史記錄（每次拜訪存檔案）
- [ ] 雲端同步（iCloud / Google Drive）
- [ ] 拜訪報告匯出（PDF / Excel）
- [ ] 地圖整合（Apple Maps / Google Maps）
- [ ] 多語言支援（English / 简体中文）

---

## 🆚 升級為原生 iOS App

如需上架 App Store 或加入推播通知，建議走以下路線：

| 路線 | 工具 | 工期 | 適合情境 |
|---|---|---|---|
| **PWA 強化版** | Service Worker + Manifest | 1 天 | 自用、不上架 |
| **套殼 App** | [Capacitor](https://capacitorjs.com/) | 1-2 週 | 預算有限、想上架 |
| **原生重寫** | SwiftUI + SwiftData | 1-3 個月 | 商業產品、追求效能 |

詳細步驟可參考專案 Wiki（待補）。

---

## ❓ 常見問題

**Q: 資料會不會不見？**  
A: 資料儲存於瀏覽器 localStorage。一般情況下不會消失，但以下狀況需注意：
- 清除 Safari 瀏覽資料 → 資料會被清除
- 長期不使用（7+ 天）→ iOS 可能清理資料（PWA 模式較穩定）
- 升級或重置 iPad → 資料會清除

**建議**：定期使用「備份資料」功能下載 JSON 檔保存。

**Q: 可以多人共用嗎？**  
A: 目前為單機版，資料儲存於各裝置本機。若需多人協作，可：
- 將 JSON 備份檔放到共用雲端硬碟
- 或考慮升級為有後端的版本

**Q: 為什麼 iPad 上點按鈕沒反應？**  
A: 請確認：
1. 是用 Safari 開啟（非 Chrome / Firefox）
2. 已加入主畫面後從主畫面開啟（更穩定）
3. iPadOS 版本為 14 以上

**Q: 備份檔下載後找不到？**  
A: 在 iPad 的「檔案」App → 瀏覽 → 「下載項目」資料夾。

---

## 📄 授權

MIT License — 可自由使用、修改、商用。

---

## 🙏 致謝

- 設計靈感來自 Apple Human Interface Guidelines
- Bootstrap 5 設計系統
- 所有提供回饋的使用者

---

## 📮 聯絡與貢獻

歡迎 Issue 回報或 Pull Request！

如果這個工具對你有幫助，給個 ⭐ Star 支持一下吧！

