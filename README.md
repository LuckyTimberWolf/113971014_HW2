-----

````markdown
# 傳統 NLP (TF-IDF) vs. 現代 AI (GPT-4o) 效能比較專案

本專案旨在比較傳統自然語言處理（NLP）方法（以 TF-IDF 為代表）與現代大型語言模型（LLM，以 GPT-4o 為代表）在三項核心任務上的表現。我們將透過量化指標，分析它們在**速度**、**成本**、**準確性**與**輸出品質**上的顯著差異。

---

##  核心任務

本專案圍繞以下三個 NLP 任務進行對比：

1.  **文本相似度 (Text Similarity)**
    * **傳統:** `TF-IDF` + `餘弦相似度 (Cosine Similarity)`
    * **現代:** `GPT-4o (Embedding API)` + `餘弦相似度`
2.  **文本分類 (Text Classification)**
    * **傳統:** 基於 `TF-IDF` 和 `手動定義關鍵詞` 的規則分類器
    * **現代:** `GPT-4o` 的 `零樣本學習 (Zero-shot) JSON 模式` 分類
3.  **自動摘要 (Text Summarization)**
    * **傳統:** `TF-IDF` 抽取式摘要 (Extractive Summarization)
    * **現代:** `GPT-4o` 生成式摘要 (Abstractive Summarization)

---

##  實驗結果速覽

根據 `results/performance_metrics.json` 的數據，兩種方法的差異極為明顯：

| 任務 | 指標 | TF-IDF (傳統方法) | GPT-4o (現代方法) | 贏家 |
| :--- | :--- | :--- | :--- | :--- |
| **相似度** | **執行時間** | **0.004 秒** | 0.511 秒 | **TF-IDF** |
| **分類** | **執行時間** | **0.001 秒** | 2.587 秒 | **TF-IDF** |
| | **準確率** | 50.0% | **100.0%** | **GPT-4o** |
| **摘要** | **執行時間** | **0.006 秒** | 1.869 秒 | **TF-IDF** |
| | **品質** | 低 (語句不連貫) | **高 (語意通順)** | **GPT-4o** |

**結論：**
* **TF-IDF**：在**速度**與**成本**上擁有絕對優勢（快 100-1000 倍）。
* **GPT-4o**：在**品質**與**準確性**上完勝，展現了強大的語意理解能力。

---

## 🛠️ 技術棧 (Dependencies)

本專案的核心函式庫如下：

```text
scikit-learn
jieba
numpy
pandas
openai
google-colab
````

-----

##  安裝與設定

本專案預設在 **Google Colab** 環境中執行，並依賴 Google 雲端硬碟和 Colab 的密鑰管理。

1.  **Clone 儲存庫**

    ```bash
    git clone [您的儲存庫 URL]
    ```

2.  **安裝依賴**
    (如果在 Colab 中，大部分已預裝，只需確保 `openai` 和 `jieba` 已安裝)

    ```bash
    pip install -r requirements.txt
    ```

3.  **設定 OpenAI API Key**
    本專案使用 `from google.colab import userdata` 來安全讀取 API Key。

      * 在您的 Google Colab 筆記本中，點擊左側的「鑰匙」圖示 (密鑰)。
      * 新增一個名為 `OpenAI` 的密鑰。
      * 將您的 OpenAI API Key (格式為 `sk-...`) 貼入其「值」中並儲存。

4.  **上傳檔案至 Google Drive**

      * 將整個專案資料夾（包含 `.py` 檔案和 `results` 資料夾）上傳到您的 Google 雲端硬碟。

-----

##  如何執行

1.  **開啟 `comparison.py`**

      * 建議使用 Google Colab 開啟 `comparison.py` (它本質上是一個 .ipynb 檔案)。

2.  **修改專案路徑**

      * 在 `comparison.py` 檔案的開頭，找到 `project_path` 變數：
        ```python
        # 專案檔案所在的「絕對路徑」
        project_path = '//content/drive/MyDrive/113971014_HW2' 
        ```
      * **請將此路徑修改為您自己在 Google 雲端硬碟中的專案絕對路徑。**

3.  **執行 Colab 筆記本**

      * 依序執行 `comparison.py` 中的所有儲存格。
      * 程式將首先掛載您的雲端硬碟，然後執行所有比較任務。

4.  **查看結果**

      * 執行完成後，您可以到您的 Google 雲端硬碟中，在專案的 `results/` 資料夾下找到所有最新的輸出檔案：
          * `performance_metrics.json`: 包含時間、成本、準確率的量化數據。
          * `classification_results.csv`: 兩種方法詳細的分類結果對比。
          * `summarization_comparison.txt`: 原始文章、TF-IDF 摘要、GPT-4o 摘要的逐字稿。
          * `tfidf_similarity_matrix.png`: TF-IDF 相似度熱力圖。

-----

##  專案架構

```
.
├── comparison.py               # (主執行檔) 運行所有比較的腳本
├── traditional_methods.py      # (模組) 包含所有 TF-IDF 相關的類和函數
├── modern_methods.py           # (模組) 包含所有 OpenAI API 相關的函數
├── requirements.txt            # 專案依賴
│
├── results/                    # (輸出目錄) 存放所有實驗結果
│   ├── performance_metrics.json
│   ├── classification_results.csv
│   ├── summarization_comparison.txt
│   └── tfidf_similarity_matrix.png
│
└── README.md                   # 本說明檔案
```

```
```
