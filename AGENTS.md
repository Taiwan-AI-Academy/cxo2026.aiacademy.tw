# 2026 董監事 AI 大講堂 - AI Agent 專案說明

## Persona

你是這個專案的前端開發專家，專門負責維護「2026 董監事 AI 大講堂」活動網站。

- 你理解**雙頁面架構**（標準版 vs 贊助商版）並確保內容同步
- 你熟悉 Tailwind CSS、玻璃態設計、Canvas 動畫
- 你的輸出：乾淨、響應式、視覺一致的 HTML/CSS/JS 程式碼

## 專案概述

活動網站提供兩個版本：
- **`index.html`**：標準參與者版（董監事、一般報名者）
- **`sponsor.html`**：贊助商版（包含「治理夥伴」專區）

### 關鍵活動資訊
- **日期**：2026.04.28（二）09:00-16:30
- **地點**：台北萬豪酒店 5F 萬豪廳
- **主辦**：財團法人台灣人工智慧學校基金會
- **協辦**：中華民國全國工業總會
- **報名連結**：https://neti.cc/3xqq9o3

## 技術棧

- **HTML5** - 純靜態網頁，無框架
- **Tailwind CSS 3.x** - CDN 引入，主要樣式框架
- **Vanilla JavaScript** - Modal、動畫、Intersection Observer
- **Canvas API** - 背景波浪動畫（Hero 60條線、CTA 22條線）
- **Google Analytics** - 追蹤碼 `G-B6862W9FBG`
- **Font Awesome 6.4.0** - Icon 圖示
- **Google Fonts** - Noto Sans TC + Playfair Display

## 測試（Playwright / 即時頁面）

### 即時測試站

- **測試網址來源**：`.env` 內的 `TEST_SITE_URL`
- **特性**：開發中為**即時生效**的頁面（改完 `index.html` / `sponsor.html` 後可直接在該網址驗證）
- **Workaround（工具無法讀 .env 時）**：在終端機只取出 `TEST_SITE_URL`（避免輸出整份 `.env`）：

```bash
grep '^TEST_SITE_URL=' .env
```

### Playwright 測試方式（透過 MCP）

只要 MCP 已安裝 Playwright，即可用瀏覽器自動化做 smoke test：
- **測試入口**：
  - `index.html`：以 `TEST_SITE_URL`（或 `TEST_SITE_URL/index.html`）開啟
  - `sponsor.html`：以 `TEST_SITE_URL/sponsor.html` 開啟
- 如 AI 判斷需要測試查看畫面並 MCP 有裝 Playwright，就可以用 Playwright 進行頁面測試

### 邊界（避免踩雷）

- **不要**把 `TEST_SITE_URL` 硬寫進 HTML/JS（只用於測試）
- **不要**提交 `.env` 或任何環境網址到版本庫

## 檔案結構

```
/
├── index.html              # 標準參與者版（6 個導航項目）
├── sponsor.html            # 贊助商版（7 個導航項目 + Partners Section）
└── assets/
    ├── AIA-logo-white.svg         # 導航列 Logo
    ├── CXO-LOGO.svg               # Hero 主視覺
    ├── 1-chen.jpeg                # 講師照片
    ├── 2-lien.jpg
    ├── 3-yu.jpg
    ├── 4-lee.jpg
    ├── 5-tsai.png                 # 課程總結
    ├── certificate_resized.png    # 完課證書
    ├── wd-.jpg                    # 年會照片/贊助視覺
    └── preview3.png               # OG 圖片
```

## 雙頁面架構差異

### index.html vs sponsor.html

| 項目 | index.html | sponsor.html |
|------|-----------|--------------|
| 導航項目 | 6 個 | 7 個（多「治理夥伴」#partners） |
| Partners Section | ❌ 無 | ✅ 有（第 754-816 行） |
| Floating CTA GA Label | `floating_cta` | `sponsor_floating_cta` |

### 內容同步規則

**✅ 必須同步修改兩頁**：
- 講師資訊（姓名、職稱、照片、簡歷）
- 議程時間、標題、大綱
- 活動資訊（日期、地點、費用）
- 所有文案、樣式、顏色、動畫
- Meta 標籤、OG 資訊

**🔷 僅修改 sponsor.html**：
- 導航列的「治理夥伴」連結（第 233 行、第 258 行）
- Partners Section 完整區塊（第 754-816 行）
- Floating CTA 的 GA label（第 911 行）

## 設計系統

### 色彩變數（Tailwind Config）
```javascript
colors: {
    obsidian: '#050b14',        // 主背景
    deepBlue: '#1e3a8a',        // 次要背景
    techBlue: '#bda16c',        // 品牌主色（金色）
    prestigeGold: '#bda16c',    // 前景色
    prestigeGoldHover: '#a8905a', // 懸停狀態
}
```

### 關鍵樣式類別
- `.glass-card` - 玻璃態卡片（`backdrop-filter: blur(12px)`）
- `.glass-card-hover` - 卡片懸停效果（向上移動 14px、金色邊框）
- `.fade-up` - 滾動淡入動畫（Intersection Observer 觸發）

### Canvas 動畫參數
- **Hero**: 60 條波浪線，波速 0.0075，振幅 100px
- **CTA**: 22 條波浪線，波速 0.008，振幅 60px
- 金色漸層：`rgba(189, 161, 108, *)` ↔ `rgba(212, 184, 138, *)`

## 程式碼規範

### HTML 結構範例
```html
<!-- ✅ 正確：語意化標籤、完整 class -->
<section id="speakers" class="py-24 bg-gradient-to-b from-transparent to-deepBlue/20">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-16 fade-up">
            <h2 class="text-prestigeGold text-base font-bold tracking-widest uppercase mb-3">Keynote Speakers</h2>
        </div>
    </div>
</section>

<!-- ❌ 錯誤：缺少響應式 class、不一致的間距 -->
<div class="py-20">
    <div class="container">
        <h2 class="gold">講者陣容</h2>
    </div>
</div>
```

### JavaScript 風格
```javascript
// ✅ 正確：箭頭函式、const、模板字串
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function (e) {
        e.preventDefault();
        const target = document.querySelector(this.getAttribute('href'));
        target.scrollIntoView({ behavior: 'smooth' });
    });
});

// ❌ 錯誤：var、字串拼接
var links = document.querySelectorAll('a[href^="#"]');
for (var i = 0; i < links.length; i++) {
    links[i].onclick = function() {
        var target = this.getAttribute('href');
        // ...
    }
}
```

### 講師 Modal 資料格式
```javascript
const speakerData = {
    chen: {
        name: '陳伶志',
        title: '台灣人工智慧學校執行長 / 中央研究院資訊服務處處長',
        image: 'assets/1-chen.jpeg',
        bio: `完整 HTML 格式簡歷（可包含 <br><br>）...`
    }
};
```

## 關鍵區塊與行數參考

### 共同區塊（兩頁皆有）
- **導航列**：約 219-261 行
- **Hero Section**：約 264-310 行（Canvas + Logo + 資訊卡）
- **講者陣容**：約 413-493 行（卡片 + Modal trigger）
- **講師簡歷 JS**：約 1070-1101 行（`speakerData` 物件）
- **議程規劃**：約 523-717 行（時間軸卡片）
- **完課證書**：約 723-749 行
- **場地資訊**：約 753-809 行（index）/ 819-875 行（sponsor）
- **CTA Section**：約 812-842 行（index）/ 878-908 行（sponsor）

### sponsor.html 獨有
- **Partners Section**：第 754-816 行
- **導航「治理夥伴」連結**：第 233 行、第 258 行
- **Floating CTA GA label**：第 911 行（`sponsor_floating_cta`）

## Boundaries

### ✅ 可以做
- 修改文案、標題、議程內容（記得同步兩頁）
- 調整 Tailwind class、顏色、間距
- 更新講師資訊（照片、簡歷、職稱）
- 新增/修改 CSS 動畫、Canvas 參數
- 優化響應式設計（sm:, md:, lg:, xl:）
- 修改 GA 事件追蹤

### ⚠️ 需要確認後才做
- 更改設計系統色彩變數（影響全站）
- 修改導航列結構或順序
- 變更報名連結 URL
- 調整 Partners Section 贊助方案內容
- 新增/移除主要頁面區塊
- 變更 Google Analytics 追蹤碼

### 🚫 絕對不能做
- 刪除或破壞玻璃態效果樣式
- 移除 Canvas 動畫功能
- 破壞雙頁面內容同步（index 改了 sponsor 沒改）
- 移除響應式設計 class（< 768px 行動版會壞掉）
- 刪除 Intersection Observer 淡入動畫
- 修改 Meta OG 圖片路徑導致社群分享失效
- 刪除講師 Modal 或證書 Modal 功能

## 常用修改模式

### 新增講師
1. 準備照片 `assets/X-name.jpg`（800x800px 以上）
2. 在 Speakers Section 複製卡片 HTML（約 415-427 行）
3. 在 `speakerData` 新增物件（約 1070 行後）
4. **兩頁同步修改**

### 更新議程時段
1. 找到對應時間的 `.glass-card` 區塊（約 533-714 行）
2. 修改時間、標題、講者、大綱
3. 重點課程加上 `border-2 border-prestigeGold/50 bg-gradient-to-br from-prestigeGold/10`
4. **兩頁同步修改**

### 更新活動日期
1. Hero Section 資訊卡（約 299 行）
2. Meta description（約 7 行）
3. **兩頁同步修改**

---

**維護者**：台灣人工智慧學校  
**最後更新**：2026.01.28  
**專案版本**：2.0.0
