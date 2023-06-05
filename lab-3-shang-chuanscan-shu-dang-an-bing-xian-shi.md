# Lab 3 上傳S參數檔案並顯示圖表

<figure><img src=".gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% code lineNumbers="true" fullWidth="true" %}
```python
import streamlit as st
import skrf as rf
import matplotlib.pyplot as plt
from os.path import isfile, join
import numpy as np

st.title('Touchstone File Viewer')

folder_path = 'D:/Downloads'
st.header('上傳檔案')

with st.form(key='my_form', clear_on_submit=True):
    file = st.file_uploader("上傳檔案", accept_multiple_files=False)
    
    if st.form_submit_button(label='Submit'):
        file_path = join(folder_path, file.name)
        with open(file_path, 'wb') as f:
            f.write(file.getbuffer())

        ntwk = rf.Network(file_path)
        num_ports = ntwk.number_of_ports
        
        columns = st.columns(4)  # 創建四個欄位
        idx = 0  # 初始化索引

        for m in range(num_ports):
            for n in range(num_ports):
                fig, ax = plt.subplots()
                ax.plot(ntwk.f/1e9, 20*np.log10(abs(ntwk.s[:,m,n])))
                ax.set_xlabel('Frequency (GHz)')
                ax.set_ylabel('S{}{} Magnitude (dB)'.format(m+1, n+1))
                plt.grid(True)

                # 在欄位中顯示圖表
                columns[idx % 4].pyplot(fig)
                plt.close(fig)  # 釋放資源
                idx += 1
```
{% endcode %}

{% file src=".gitbook/assets/AL_D_3_short.s4p" %}
