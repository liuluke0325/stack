# 股票複利試算(stock-simulate)

一個推廣「長期存股」重要性的複利試算工具。線上版:
https://liuluke0325.github.io/stock-simulate/

## 功能

- **兩種視角切換**:「單純複利(理論)」是教科書式平滑成長曲線;「模擬真實走勢(卜瓦松)」則用隨機波動 + 卜瓦松過程模擬市場偶發大漲大跌,呈現貼近現實的上下震盪走勢,每次「重新模擬」結果都不同。
- **熱門標的快速帶入**:涵蓋台股、美股、港股/中概股、陸股(A股)共 13 檔,各自標註信心度(✓ 已查證來源 / ‡ 歷史數據但受近期熱潮或存活者偏差影響 / † 低信心度自行估算 / ⚠ 極端異常值,不可外推)。點選標的會在下方顯示該檔數字的具體來源與注意事項。
- **自訂標的**:可自行輸入任何標的的名稱/年化報酬率/波動度/幣別,存在瀏覽器 localStorage,重新整理、下次再開都還記得。
- **股票代號查詢**:選市場(台/港/陸/美)、輸入代號,直接開新分頁連到對應的資料來源(台股 ifa.ai、其他連 Yahoo Finance)查歷史報酬與波動度。
- **匯出 Excel**:把目前設定與試算結果匯出成 `.xlsx`,格式仿照試算表慣用的「指標為列、時間點為欄」寬表,方便直接在 Excel 裡繼續加工。
- **深色/淺色主題**:右上角切換,記在 localStorage。
- 支援台幣(NT$)、美元(US$)、港幣(HK$)、人民幣(¥)四種幣別顯示。

## 技術架構

TypeScript + Vite,純前端、無後端,部署在 GitHub Pages。推上 `main` 分支會自動觸發 GitHub Actions(`.github/workflows/deploy.yml`)build 並部署。

```
src/
  main.ts        入口,event wiring
  state.ts       跨模組共用狀態(幣別、分頁模式、試算結果)
  finance.ts     卜瓦松/常態分布亂數、複利與模擬計算邏輯
  chart.ts       SVG 圖表繪製與滑鼠/觸控互動
  presets.ts     熱門標的選取、自訂標的 CRUD(localStorage)
  presetNotes.ts 各熱門標的的資料來源說明文字
  format.ts      幣別格式化
  lookup.ts      查詢其他股票按鈕
  export.ts      匯出 Excel
  theme.ts       深色/淺色主題切換
```

## 開發

```bash
npm install
npm run dev      # 本地開發伺服器
npm run build    # 產出 dist/,對應 GitHub Pages 的 /stock-simulate/ 子路徑
npm run preview  # 預覽 build 後的結果
```

## 免責聲明

工具內所有標的的報酬率/波動度數字皆為歷史資料或自行估算值,不代表未來表現,不構成投資建議。詳見頁面內各標的的資料來源說明。
