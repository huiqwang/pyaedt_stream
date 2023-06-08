# Lab 5 建立天線模擬並返回壓縮檔

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

{% code lineNumbers="true" %}
```python
import streamlit as st
import numpy as np
import matplotlib.pyplot as plt

# Define sidebar inputs
st.sidebar.header("Input Parameters")
freq0 = st.sidebar.number_input("Center Frequency(GHz)", min_value=0.0, max_value=100.0, value=2.0, step=0.1)
freq_low = st.sidebar.number_input("Low Frequency(GHz)", min_value=0.0, max_value=100.0, value=1.0, step=0.1)
freq_high = st.sidebar.number_input("High Frequency(GHz)", min_value=0.0, max_value=100.0, value=3.0, step=0.1)
length = st.sidebar.number_input("Length(mm)", min_value=1.0, max_value=100.0, value=50.0, step=0.1)


if st.sidebar.button('Run'):
    # length = 50
    # freq0 = 2
    # freq_low = 1
    # freq_high = 3


    from pyaedt import Hfss

    hfss = Hfss(specified_version='2023.1')

    hfss.change_material_override()
    hfss.change_automatically_use_causal_materials()

    hfss['length'] = '{}mm'.format(length)

    hfss.modeler.create_cylinder(cs_axis='Z',
                                 position=(0,0,0.5),
                                 radius='0.5mm',
                                 height='length',
                                 matname='copper'
                                 )

    hfss.modeler.create_cylinder(cs_axis='Z',
                                 position=(0,0,-0.5),
                                 radius='0.5mm',
                                 height='-length',
                                 matname='copper'
                                 )

    hfss.modeler.create_rectangle(csPlane=1, 
                                  position=(-0.5, 0, -0.5), 
                                  dimension_list=(1, 1),
                                  name='sheet')

    hfss.create_lumped_port_to_sheet(sheet_name='sheet',
                                     axisdir=2)

    hfss.create_open_region(Frequency='{}GHz'.format(freq0))


    setup = hfss.create_setup('mysetup')

    setup.props['Frequency'] = '{}GHz'.format(freq0)
    setup.props['MaxDeltaS'] = 0.01
    setup.props['MaximumPasses'] = 20


    hfss.create_linear_step_sweep(setupname='mysetup',
                                  unit='GHz',
                                  freqstart=freq_low,
                                  freqstop=freq_high,
                                  step_size=0.1,
                                  sweepname='mysweep',)


    hfss.analyze_nominal(num_cores=4)

    result = hfss.post.get_solution_data('dB(S11)', 'mysetup:mysweep')

    s11 = result.data_real('dB(S11)')
    freq = result.primary_sweep_values


    import matplotlib.pyplot as plt
    plt.title('{}mm dipole antenna return loss'.format(length))
    plt.xlabel('freq (GHz)')
    plt.ylabel('dB(S11)')
    plt.grid()

    plt.plot(freq, s11, c='r')
    #plt.savefig('c:/demo/test.png')
    #plt.clf()

    hfss.archive_project('c:/demo/test.aedtz')
    hfss.close_desktop()

    # Show the plot in Streamlit
    st.pyplot(plt)
    with open('c:/demo/test.aedtz', 'rb') as f:
        data = f.read()
    st.download_button('download', data, 'test.aedtz')
```
{% endcode %}
