# 🩸 食物配方對凝血時間之影響

此報告為統計實驗設計之實作，運用 **R 語言**與**變異數分析**，探討不同的食物配方是否會對實驗動物的血液凝固時間造成顯著影響，涵蓋了完整的統計建模流程，從資料預處理、假設檢定到事後多重比較，並透過資料轉換（對數與倒數）以確保模型適配度。

## 🔬 實驗設計
* **設計方法：** 完全隨機設計 (Completely Randomized Design, CRD)。
* **實驗對象：** 24 隻實驗動物，隨機分為 4 組。
* **自變項 (控制變因)：** 食物配方 (Diet)，分為 A, B, C, D 四種。
* **應變項 (測量結果)：** 凝血時間 (Coagulation time)，單位為秒。

## 🛠️ 統計分析流程

為了確保 ANOVA 模型的有效性，因此嚴格執行了以下統計前提假設檢驗：

1. **常態性檢定 (Normality Test)：**
   * 運用 **Kolmogorov-Smirnov Test** 與 **Lilliefors Test**，檢定結果顯示數據服從常態分配 (p-value > 0.05)。
   * 針對各組別原始數據及模型殘差 (Residuals) 進行 **Shapiro-Wilk Test** 交叉驗證。
3. **變異數同質性檢定 (Homogeneity of Variance)：**
   * 運用 **Levene's Test** 進行檢定，結果顯示各組變異數具有同質性 ($P-value=0.5926 > 0.05$)。
4. **變異數分析 (ANOVA):**
   * 建立線性模型，檢定結果顯示不同食物配方對凝血時間有極顯著影響 ($P-value=4.658e-05 < 0.05$)。
5. **事後檢定 (Post-hoc Analysis):**
   * 由於 ANOVA 結果顯著，進一步使用 **Tukey-Kramer Procedure** 進行多重比較。

## 💡 研究結論
實驗結果證實，**不同飲食確實會顯著影響血液凝固時間**。
進一步的事後檢定指出：
* 配方 **A 與 D** 之間，以及配方 **C 與 B** 之間的效果類似，凝固時間沒有統計上的顯著差異。
* 其他組別的配方交叉比較（如 A-B, A-C 等）皆存在顯著差異。

## 📂 檔案說明
* `New.Rmd`: 包含資料處理、各式檢定 (ANOVA, Shapiro-Wilk, Lilliefors, Levene's Test) 及資料轉換 (log, reciprocal) 的 R 語言程式碼。
* `黃柏翰張智賢.pdf`: 完整期中報告，包含理論背景、視覺化圖表與數據解讀。

## 💻 開發環境與技術
* **Language:** R (R Markdown)
* **Key Packages:** `HH` (資料集), `nortest` (Lilliefors test), `car` (Levene's test)
