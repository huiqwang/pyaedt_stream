# 基本介紹

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### PyAEDT 的應用

&#x20;PyAEDT 是一個基於 Python 的 Ansys Electronics Desktop (AEDT) 的 API，可用於進行電子設計自動化。通過使用 PyAEDT，工程師可以編寫程式碼以自動執行 AEDT 的模擬工作，例如建立幾何模型、設定邊界條件、選擇求解器等。

### Streamlit 的應用

Streamlit 是一個用於創建和部署數據科學和機器學習應用的開源框架。它可以快速將 Python 程式碼轉換為具有互動式網頁界面的應用程序。通過在公司內部的伺服器上部署 Streamlit，可以實現一個私有雲服務，讓使用者通過瀏覽器訪問應用程序。

### 整合 PyAEDT 與 Streamlit

整合 PyAEDT 和 Streamlit 可以實現以下功能：

* 使用者可以通過瀏覽器作為界面，進行模擬工作的設定。
* 使用者在瀏覽器上設定模擬參數後，將資料通過區域網路傳送到伺服器。
* 伺服器收到資料後，使用 PyAEDT 執行 AEDT 模擬工作。
* 模擬結束後，使用者可以在瀏覽器上直接檢視模型或下載模擬結果。
