# Lab 2 建立簡單計算機

{% code lineNumbers="true" %}
```python
# 引入streamlit和math模組
import streamlit as st
from math import *

# 在streamlit應用中添加一個標題
st.title('線上計算機')

# 創建一個輸入框讓使用者輸入方程式，並將輸入的方程式存到變數equation中
equation = st.text_input('請在此輸入你的方程式：')

# 檢查變數equation是否有內容
if equation:
    try:
        # 使用Python的內建函數eval()解析和執行使用者輸入的數學表達式，並將結果存到變數result中
        result = eval(equation)

        # 將結果顯示到streamlit應用中
        st.write('結果是：', result)

    except Exception as e:
        # 如果使用者輸入的數學表達式無法解析或執行，則捕獲異常並顯示錯誤訊息
        st.write('發生錯誤：', str(e))

```
{% endcode %}
