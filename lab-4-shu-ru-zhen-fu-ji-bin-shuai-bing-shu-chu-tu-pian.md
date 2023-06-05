# Lab 4 輸入振幅及頻率並輸出圖片

<figure><img src=".gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

{% code lineNumbers="true" %}
```python
import streamlit as st
import numpy as np
import matplotlib.pyplot as plt

# Define sidebar inputs
st.sidebar.header("Input Parameters")
frequency = st.sidebar.number_input("Frequency", min_value=0.0, max_value=10.0, value=1.0, step=0.1)
amplitude = st.sidebar.number_input("Amplitude", min_value=0.0, max_value=10.0, value=1.0, step=0.1)

# Create time data for the plot
time = np.arange(0.0, 2.0, 0.01)

# Define the sinewave function
sinewave = amplitude * np.sin(2 * np.pi * frequency * time)

# Create the plot
plt.figure(figsize=(10, 6))
plt.plot(time, sinewave)
plt.title("Sine Wave")
plt.xlabel("Time")
plt.ylabel("Amplitude")
plt.grid(True)

# Show the plot in Streamlit
st.pyplot(plt)

```
{% endcode %}
