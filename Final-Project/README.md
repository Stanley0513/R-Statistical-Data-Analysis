# 📈 年收入和風險態度對壽險購買金額的影響分析

報告中運用 **R 語言**與**迴歸分析**，針對企業經理人族群進行探討，分析其經濟能力（年收入）與心理特質（風險趨避程度）如何共同影響人壽保險的持有額度，完整展示了從基礎線性模型建立、殘差診斷 (Residual Diagnostics)、非線性趨勢修正，到極端影響點排除的模型最佳化迭代過程。

## 👥 專案開發與協作聲明
本專案為統計資料分析課程之期末小組專題，由本人與團隊成員共同研發。

## 📊 資料集說明
使用 `HH` 套件中的 `lifeins` 資料集，包含 18 位企業經理人的觀測值。
* **應變數 (Y)：** `lifeins` - 人壽保險總金額 (千美元)。
* **自變數 (X1)：** `anninc` - 平均年度收入 (千美元)。
* **自變數 (X2)：** `riskaver` - 風險趨避分數 (分數越高代表越保守)。

## 🛠️ 分析流程與模型演進

本研究歷經三個階段的模型優化，以確保預測的準確性與統計推論的穩健性：

### Phase 1： 基礎線性模型 (Model 0)
* 建立包含 `anninc` 與 `riskaver` 的多重線性迴歸模型。
* **診斷發現：** 雖然整體 F 檢定顯著，且常態性 (Shapiro-Wilk)、同質變異數 (Breusch-Pagan) 與序列相關 (Durbin-Watson) 檢定皆通過，但**殘差與擬合值圖 (Residuals vs Fitted) 呈現明顯的 U 型趨勢**，顯示模型存在未捕捉的非線性關係 。

### Phase 2： 多項式迴歸修正 (Model 1)
* **修正方法：** 引入收入的平方項 (`anninc^2`) 以捕捉非線性邊際效應。
* **模型比較：** 比較三個候選模型的 AIC 值，確認加入 `anninc^2` 的模型 (AIC = 86.78) 適配度最佳，成功消除殘差的 U 型分佈。
* **新問題：** 加入平方項後，殘差的常態性檢定遭到拒絕 (p-value = 0.0019)，暗示存在極端值干擾。

### Phase 3: 影響診斷與最終優化 (Model New)
* **影響點分析 (Influence Analysis)：** 綜合運用 `Cook's Distance`、`Leverage`、`DFFITS` 與 `DFBETAS` 四項指標，精準定位出第 1 筆資料為嚴重的影響點 (Influential Point)。
* **最終模型：** 排除第 1 筆異常資料後重新擬合模型。
* **成果：** 最終模型不僅重新通過所有殘差常態性檢定，**Adjusted R-squared 更提升至 0.9998，AIC 大幅下降至 63.85**，模型達到極佳的穩定度與解釋力。

## 💡 結論
1. **非線性收入效應：** 經理人的壽險需求隨著收入增長呈現非線性的邊際變化，單純的線性假設會導致設定偏誤。
2. **心理特質的顯著性：** 在嚴格控制收入水準的非線性效應後，「風險趨避分數」依然對壽險保額具有高度顯著的正向影響。這證實了個性越保守、越規避風險的經理人，會購買更高額的保險。

## 📂 檔案結構
* `期末.Rmd`: 資料載入與初步設定的 R Markdown 原始檔。
* `第十三組期末報告.pdf`: 完整分析報告，包含詳細的統計推論、殘差圖表、AIC 模型比較與影響點診斷視覺化。

## 💻 開發環境與技術
* **Language：** R (R Markdown)
* **Key Packages：** `HH` (資料集套件)
* **Statistical Methods & Models：**
  * 多重線性迴歸 (Multiple Linear Regression)
  * 多項式迴歸 (Polynomial Regression)
  * 模型選擇 (Model Selection by AIC)
* **Model Diagnostics：**
  * 常態性檢定 (Shapiro-Wilk Test)
  * 同質變異數檢定 (Studentized Breusch-Pagan Test)
  * 序列相關檢定 (Durbin-Watson Test)
* **Influence Analysis (極端影響點分析)：**
  * Cook's Distance
  * Leverage (高槓桿點偵測)
  * DFFITS & DFBETAS
