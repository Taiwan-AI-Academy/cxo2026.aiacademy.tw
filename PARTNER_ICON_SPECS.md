# 社群夥伴 ICON 規格說明

## 顯示尺寸

### 當前設計
- **容器尺寸**：`w-32 h-32` = **128px × 128px**（正方形）
- **容器樣式**：圓角矩形（`rounded-lg`）、半透明白色背景（`bg-white/10`）、邊框
- **顯示位置**：深色背景（`bg-obsidian`）的社群夥伴區塊

## 最佳 ICON 規格建議

### 1. 原始檔案尺寸（推薦）

#### 標準解析度
- **寬度**：**256px**
- **高度**：**256px**
- **寬高比**：**1:1**（必須為正方形）

#### 高解析度（Retina 顯示器）
- **寬度**：**512px**
- **高度**：**512px**
- **寬高比**：**1:1**（必須為正方形）

### 2. 檔案格式

#### 優先順序
1. **SVG**（向量圖，推薦）
   - 可無限縮放不失真
   - 檔案通常較小（< 20KB）
   - 支援透明背景
   - 適合品牌 Logo

2. **PNG**（點陣圖，次選）
   - 透明背景（必須）
   - 高解析度版本（256px 或 512px）
   - 檔案大小建議 < 50KB

#### 不建議使用
- ❌ JPG（不支援透明背景）
- ❌ GIF（色彩限制）

### 3. 視覺設計規範

#### 內邊距（Padding）
- **建議保留 15-20% 的內邊距**
- 實際圖示內容區域約：**102-109px**（在 128px 容器中）
- 避免圖示貼邊，確保視覺舒適度

#### 色彩模式
- **RGB**（網頁標準）
- **透明背景**（必須）
- 考慮深色背景顯示：
  - 使用白色或淺色版本的 Logo
  - 或使用彩色版本（需確保在深色背景上清晰可見）

#### 對比度
- 確保 Logo 在深色背景（`#0f172a`）上清晰可見
- 建議對比度至少 **4.5:1**（WCAG AA 標準）

### 4. 各夥伴 ICON 具體建議

#### Google
- **原始尺寸**：256px × 256px 或 512px × 512px
- **顯示尺寸**：128px × 128px
- **建議版本**：白色版本（適用深色背景）
- **檔案命名**：`partner-google.svg` 或 `partner-google.png`

#### Microsoft
- **原始尺寸**：256px × 256px 或 512px × 512px
- **顯示尺寸**：128px × 128px
- **建議版本**：白色版本或彩色版本（需測試對比度）
- **檔案命名**：`partner-microsoft.svg` 或 `partner-microsoft.png`

#### AWS (Amazon Web Services)
- **原始尺寸**：256px × 256px 或 512px × 512px
- **顯示尺寸**：128px × 128px
- **建議版本**：官方橙色 Logo（需確認深色背景可見度）
- **檔案命名**：`partner-aws.svg` 或 `partner-aws.png`

#### NVIDIA
- **原始尺寸**：256px × 256px 或 512px × 512px
- **顯示尺寸**：128px × 128px
- **建議版本**：綠色眼睛 Logo（需確認深色背景可見度）
- **檔案命名**：`partner-nvidia.svg` 或 `partner-nvidia.png`

#### IBM
- **原始尺寸**：256px × 256px 或 512px × 512px
- **顯示尺寸**：128px × 128px
- **建議版本**：藍色條紋 Logo（需確認深色背景可見度）
- **檔案命名**：`partner-ibm.svg` 或 `partner-ibm.png`

## 技術實作建議

### HTML 結構更新
將目前的文字顯示改為圖片顯示：

```html
<div class="w-32 h-32 rounded-lg bg-white/10 flex items-center justify-center mb-4 border border-white/20 group-hover:border-prestigeGold/50 transition-colors">
    <img src="assets/partner-google.svg" alt="Google" class="w-24 h-24 object-contain">
</div>
```

### CSS 類別說明
- `w-32 h-32`：容器尺寸（128px × 128px）
- `object-contain`：確保圖片完整顯示，保持比例
- `w-24 h-24`：圖片實際顯示尺寸（96px × 96px），保留內邊距

## 檔案結構建議

```
assets/
├── logo_capture.svg
├── partner-google.svg
├── partner-microsoft.svg
├── partner-aws.svg
├── partner-nvidia.svg
└── partner-ibm.svg
```

## 品質檢查清單

- [ ] 所有 ICON 為正方形（1:1 寬高比）
- [ ] 原始檔案至少 256px × 256px
- [ ] 透明背景（無白色或彩色背景）
- [ ] 在深色背景上清晰可見
- [ ] 檔案大小合理（SVG < 20KB，PNG < 50KB）
- [ ] 符合各品牌官方 Logo 使用規範
- [ ] 已測試在不同裝置上的顯示效果

## 取得官方 Logo 資源

### 建議來源
1. **品牌官方網站**：通常提供品牌資源下載頁面
2. **品牌指南（Brand Guidelines）**：包含 Logo 使用規範與下載連結
3. **品牌資源中心**：
   - Google: [Brand Resource Center](https://about.google/brand-resource-center/)
   - Microsoft: [Brand Assets](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks)
   - AWS: [AWS Brand Guidelines](https://aws.amazon.com/trademark-guidelines/)
   - NVIDIA: [NVIDIA Brand Center](https://www.nvidia.com/en-us/about-nvidia/brand/)
   - IBM: [IBM Brand Center](https://www.ibm.com/brand)

### 使用注意事項
- ⚠️ 確認品牌 Logo 使用授權
- ⚠️ 遵守各品牌的 Logo 使用規範
- ⚠️ 不得修改 Logo 的顏色、比例或設計
- ⚠️ 保持適當的留白空間

---

**最後更新**：2026.01
