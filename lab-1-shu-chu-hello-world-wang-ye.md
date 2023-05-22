---
description: 建立C:\demo目錄，所有.bat及.py檔皆存放在C:\demo目錄當中
---

# Lab 1 輸出Hello World網頁

### 建立批次檔

要創建一個批次檔案 (.bat) 以運行 Streamlit，請按照以下步驟操作：

1. 打開一個純文本編輯器，如記事本。
2. 將以下代碼複製並粘貼到編輯器中，並存為c:\demo\run.bat

{% code title="run.bat" %}
```
@echo off
streamlit run .\test.py
pause
```
{% endcode %}

### 建立Python檔案

打開一個純文本編輯器，如記事本，並創建一個新的 Python 腳本文件。將以下代碼複製並粘貼到該文件中，並保存文件test`.py`

{% code title="test.py" lineNumbers="true" %}
```python
import streamlit as st

st.title("Hello World")
```
{% endcode %}



