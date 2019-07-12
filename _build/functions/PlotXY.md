---
redirect_from:
  - "/functions/plotxy"
interact_link: content/functions/PlotXY.ipynb
kernel_name: python3
has_widgets: false
title: 'Plotxy'
prev_page:
  url: /functions/DepthProfile
  title: 'Depthprofile'
next_page:
  url: /functions/Histogram
  title: 'Histogram'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---


## Reformat netCDF File for a Function Call



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
import opedia
import xarray as xr
import sys
import os
import numpy as np
import pandas as pd
import db
import common as com
import timeSeries as TS
import itertools as itt
from bokeh.io import output_notebook
from datetime import datetime, timedelta
import time
from math import pi
from bokeh.plotting import figure, show, output_file
from bokeh.layouts import column
from bokeh.models import DatetimeTickFormatter
from bokeh.palettes import all_palettes
from bokeh.models import HoverTool
from bokeh.embed import components
import jupyterInline as jup
if jup.jupytered():
    from tqdm import tqdm_notebook as tqdm
else:
    from tqdm import tqdm

```
</div>

</div>



### Testing Original Function



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
tables = ['tblSST_AVHRR_OI_NRT', 'tblAltimetry_REP']
variables = ['sst', 'sla']                                        # see catalog.csv  for the complete list of tables and variable names
startDate = '2016-03-29'
endDate = '2016-05-29'
lat1, lat2 = 25, 30
lon1, lon2 = -160, -155
depth1, depth2 = 0, 5
fname = 'XY'
exportDataFlag = False      # True if you you want to download data

plotXY(tables, variables, startDate, endDate, lat1, lat2, lon1, lon2, depth1, depth2, fname, exportDataFlag)


```
</div>

<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">
{:.output_data_text}
```
HBox(children=(IntProgress(value=0, description='overall', max=1, style=ProgressStyle(description_width='initi…
```

</div>
</div>
<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">
{:.output_stream}
```
------------Time1:
[datetime.datetime(2016, 3, 29, 0, 0), datetime.datetime(2016, 3, 30, 0, 0), datetime.datetime(2016, 3, 31, 0, 0), datetime.datetime(2016, 4, 1, 0, 0), datetime.datetime(2016, 4, 2, 0, 0), datetime.datetime(2016, 4, 3, 0, 0), datetime.datetime(2016, 4, 4, 0, 0), datetime.datetime(2016, 4, 5, 0, 0), datetime.datetime(2016, 4, 6, 0, 0), datetime.datetime(2016, 4, 7, 0, 0), datetime.datetime(2016, 4, 8, 0, 0), datetime.datetime(2016, 4, 9, 0, 0), datetime.datetime(2016, 4, 10, 0, 0), datetime.datetime(2016, 4, 11, 0, 0), datetime.datetime(2016, 4, 12, 0, 0), datetime.datetime(2016, 4, 13, 0, 0), datetime.datetime(2016, 4, 14, 0, 0), datetime.datetime(2016, 4, 15, 0, 0), datetime.datetime(2016, 4, 16, 0, 0), datetime.datetime(2016, 4, 17, 0, 0), datetime.datetime(2016, 4, 18, 0, 0), datetime.datetime(2016, 4, 19, 0, 0), datetime.datetime(2016, 4, 20, 0, 0), datetime.datetime(2016, 4, 21, 0, 0), datetime.datetime(2016, 4, 22, 0, 0), datetime.datetime(2016, 4, 23, 0, 0), datetime.datetime(2016, 4, 24, 0, 0), datetime.datetime(2016, 4, 25, 0, 0), datetime.datetime(2016, 4, 26, 0, 0), datetime.datetime(2016, 4, 27, 0, 0), datetime.datetime(2016, 4, 28, 0, 0), datetime.datetime(2016, 4, 29, 0, 0), datetime.datetime(2016, 4, 30, 0, 0), datetime.datetime(2016, 5, 1, 0, 0), datetime.datetime(2016, 5, 2, 0, 0), datetime.datetime(2016, 5, 3, 0, 0), datetime.datetime(2016, 5, 4, 0, 0), datetime.datetime(2016, 5, 5, 0, 0), datetime.datetime(2016, 5, 6, 0, 0), datetime.datetime(2016, 5, 7, 0, 0), datetime.datetime(2016, 5, 8, 0, 0), datetime.datetime(2016, 5, 9, 0, 0), datetime.datetime(2016, 5, 10, 0, 0), datetime.datetime(2016, 5, 11, 0, 0), datetime.datetime(2016, 5, 12, 0, 0), datetime.datetime(2016, 5, 13, 0, 0), datetime.datetime(2016, 5, 14, 0, 0), datetime.datetime(2016, 5, 15, 0, 0), datetime.datetime(2016, 5, 16, 0, 0), datetime.datetime(2016, 5, 17, 0, 0), datetime.datetime(2016, 5, 18, 0, 0), datetime.datetime(2016, 5, 19, 0, 0), datetime.datetime(2016, 5, 20, 0, 0), datetime.datetime(2016, 5, 21, 0, 0), datetime.datetime(2016, 5, 22, 0, 0), datetime.datetime(2016, 5, 23, 0, 0), datetime.datetime(2016, 5, 24, 0, 0), datetime.datetime(2016, 5, 25, 0, 0), datetime.datetime(2016, 5, 26, 0, 0), datetime.datetime(2016, 5, 27, 0, 0), datetime.datetime(2016, 5, 28, 0, 0), datetime.datetime(2016, 5, 29, 0, 0)]
------------Time2:
[datetime.datetime(2016, 3, 29, 0, 0), datetime.datetime(2016, 3, 30, 0, 0), datetime.datetime(2016, 3, 31, 0, 0), datetime.datetime(2016, 4, 1, 0, 0), datetime.datetime(2016, 4, 2, 0, 0), datetime.datetime(2016, 4, 3, 0, 0), datetime.datetime(2016, 4, 4, 0, 0), datetime.datetime(2016, 4, 5, 0, 0), datetime.datetime(2016, 4, 6, 0, 0), datetime.datetime(2016, 4, 7, 0, 0), datetime.datetime(2016, 4, 8, 0, 0), datetime.datetime(2016, 4, 9, 0, 0), datetime.datetime(2016, 4, 10, 0, 0), datetime.datetime(2016, 4, 11, 0, 0), datetime.datetime(2016, 4, 12, 0, 0), datetime.datetime(2016, 4, 13, 0, 0), datetime.datetime(2016, 4, 14, 0, 0), datetime.datetime(2016, 4, 15, 0, 0), datetime.datetime(2016, 4, 16, 0, 0), datetime.datetime(2016, 4, 17, 0, 0), datetime.datetime(2016, 4, 18, 0, 0), datetime.datetime(2016, 4, 19, 0, 0), datetime.datetime(2016, 4, 20, 0, 0), datetime.datetime(2016, 4, 21, 0, 0), datetime.datetime(2016, 4, 22, 0, 0), datetime.datetime(2016, 4, 23, 0, 0), datetime.datetime(2016, 4, 24, 0, 0), datetime.datetime(2016, 4, 25, 0, 0), datetime.datetime(2016, 4, 26, 0, 0), datetime.datetime(2016, 4, 27, 0, 0), datetime.datetime(2016, 4, 28, 0, 0), datetime.datetime(2016, 4, 29, 0, 0), datetime.datetime(2016, 4, 30, 0, 0), datetime.datetime(2016, 5, 1, 0, 0), datetime.datetime(2016, 5, 2, 0, 0), datetime.datetime(2016, 5, 3, 0, 0), datetime.datetime(2016, 5, 4, 0, 0), datetime.datetime(2016, 5, 5, 0, 0), datetime.datetime(2016, 5, 6, 0, 0), datetime.datetime(2016, 5, 7, 0, 0), datetime.datetime(2016, 5, 8, 0, 0), datetime.datetime(2016, 5, 9, 0, 0), datetime.datetime(2016, 5, 10, 0, 0), datetime.datetime(2016, 5, 11, 0, 0), datetime.datetime(2016, 5, 12, 0, 0), datetime.datetime(2016, 5, 13, 0, 0), datetime.datetime(2016, 5, 14, 0, 0), datetime.datetime(2016, 5, 15, 0, 0), datetime.datetime(2016, 5, 16, 0, 0), datetime.datetime(2016, 5, 17, 0, 0), datetime.datetime(2016, 5, 18, 0, 0), datetime.datetime(2016, 5, 19, 0, 0), datetime.datetime(2016, 5, 20, 0, 0), datetime.datetime(2016, 5, 21, 0, 0), datetime.datetime(2016, 5, 22, 0, 0), datetime.datetime(2016, 5, 23, 0, 0), datetime.datetime(2016, 5, 24, 0, 0), datetime.datetime(2016, 5, 25, 0, 0), datetime.datetime(2016, 5, 26, 0, 0), datetime.datetime(2016, 5, 27, 0, 0), datetime.datetime(2016, 5, 28, 0, 0), datetime.datetime(2016, 5, 29, 0, 0)]
------------------Var1:
[21.27561842 20.58254344 20.55189344 20.71746843 20.78506843 20.89689343
 21.06076843 20.93099343 20.93099343 20.73986843 20.90556843 21.02274343
 21.15584342 21.14424342 21.07299343 21.13734342 21.21871842 21.35879342
 21.42886842 21.36644342 21.00244343 21.22411842 21.36564342 21.42474342
 21.68201841 21.79419341 22.1272684  22.52514339 22.88849338 23.06329338
 23.11751838 22.98036838 23.01819338 22.87729339 22.56101839 22.44994339
 22.48929339 22.62281839 22.68919339 22.52076839 21.91494341 21.93604341
 22.0114434  21.97844341 21.88144341 22.0522184  22.1390684  22.3720934
 22.75844339 23.03199338 22.91399338 22.91156838 23.02686838 23.11726838
 23.16216838 23.24964338 23.38746837 23.48811837 23.63334337 23.77659337
 23.82414336 23.85194336]
------------------Var2:
[ 2.420700e-02  2.280100e-02  2.149575e-02  2.077275e-02  1.969825e-02
  1.894475e-02  1.802600e-02  1.732750e-02  1.665750e-02  1.607475e-02
  1.551375e-02  1.490375e-02  1.411650e-02  1.351250e-02  1.306800e-02
  1.276425e-02  1.284650e-02  1.251200e-02  1.223825e-02  1.223000e-02
  1.204050e-02  1.175425e-02  1.115475e-02  1.065150e-02  9.951500e-03
  9.552500e-03  8.762250e-03  7.644250e-03  6.882500e-03  6.317250e-03
  5.331500e-03  4.255000e-03  2.715500e-03  1.416750e-03  5.425000e-04
 -2.432500e-04 -1.052500e-03 -2.240500e-03 -2.897750e-03 -3.003000e-03
 -2.937250e-03 -2.957000e-03 -3.111250e-03 -3.060750e-03 -2.992500e-03
 -2.903250e-03 -2.863500e-03 -3.258750e-03 -3.385250e-03 -3.207500e-03
 -3.264750e-03 -3.298250e-03 -3.138000e-03 -2.649500e-03 -2.542500e-03
 -2.093750e-03 -1.770500e-03 -1.794500e-03 -1.388000e-03 -7.010000e-04
 -8.825000e-05  1.075750e-03]
1: sst retrieved (tblSST_AVHRR_OI_NRT).
[0m1: sla retrieved (tblAltimetry_REP).
[0m```
</div>
</div>
<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">

<div markdown="0" class="output output_html">

    <div class="bk-root">
        <a href="https://bokeh.pydata.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
        <span id="1333">Loading BokehJS ...</span>
    </div>
</div>

</div>
</div>
<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">

</div>
</div>
<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">
{:.output_stream}
```

```
</div>
</div>
<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">

<div markdown="0" class="output output_html">






  <div class="bk-root" id="0bc0dbe5-44e1-42a4-8cb7-83f8beda0403" data-root-id="1408"></div>

</div>

</div>
</div>
<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">

</div>
</div>
</div>



### Testing NetCDF Compatible Function



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
xFile = xr.open_dataset('http://engaging-opendap.mit.edu:8080/thredds/dodsC/las/id-a1d60eba44/data_usr_local_tomcat_content_cbiomes_20190510_20_darwin_v0.2_cs510_darwin_v0.2_cs510_nutrients.nc.jnl')

tables = [xFile, xFile]
variables = ['O2','FeT']                                        # see catalog.csv  for the complete list of tables and variable names
startDate = '1992-04-30'
endDate = '1993-04-30'
lat1, lat2 = 25, 30
lon1, lon2 = -160, -155
depth1, depth2 = 0, 5
fname = 'XY'
exportDataFlag = False      # True if you you want to download data

xarrayPlotXY(tables, variables, startDate, endDate, lat1, lat2, lon1, lon2, depth1, depth2, fname, exportDataFlag)


```
</div>

<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">
{:.output_data_text}
```
HBox(children=(IntProgress(value=0, description='overall', max=1, style=ProgressStyle(description_width='initi…
```

</div>
</div>
<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">
{:.output_stream}
```
------------Time1:
[cftime.DatetimeGregorian(1992, 5, 1, 12, 0, 0, 0, 4, 122)
 cftime.DatetimeGregorian(1992, 5, 4, 12, 0, 0, 0, 0, 125)
 cftime.DatetimeGregorian(1992, 5, 7, 12, 0, 0, 0, 3, 128)
 cftime.DatetimeGregorian(1992, 5, 10, 12, 0, 0, 0, 6, 131)
 cftime.DatetimeGregorian(1992, 5, 13, 12, 0, 0, 0, 2, 134)
 cftime.DatetimeGregorian(1992, 5, 16, 12, 0, 0, 0, 5, 137)
 cftime.DatetimeGregorian(1992, 5, 19, 12, 0, 0, 0, 1, 140)
 cftime.DatetimeGregorian(1992, 5, 22, 12, 0, 0, 0, 4, 143)
 cftime.DatetimeGregorian(1992, 5, 25, 12, 0, 0, 0, 0, 146)
 cftime.DatetimeGregorian(1992, 5, 28, 12, 0, 0, 0, 3, 149)
 cftime.DatetimeGregorian(1992, 5, 31, 12, 0, 0, 0, 6, 152)
 cftime.DatetimeGregorian(1992, 6, 3, 12, 0, 0, 0, 2, 155)
 cftime.DatetimeGregorian(1992, 6, 6, 12, 0, 0, 0, 5, 158)
 cftime.DatetimeGregorian(1992, 6, 9, 12, 0, 0, 0, 1, 161)
 cftime.DatetimeGregorian(1992, 6, 12, 12, 0, 0, 0, 4, 164)
 cftime.DatetimeGregorian(1992, 6, 15, 12, 0, 0, 0, 0, 167)
 cftime.DatetimeGregorian(1992, 6, 18, 12, 0, 0, 0, 3, 170)
 cftime.DatetimeGregorian(1992, 6, 21, 12, 0, 0, 0, 6, 173)
 cftime.DatetimeGregorian(1992, 6, 24, 12, 0, 0, 0, 2, 176)
 cftime.DatetimeGregorian(1992, 6, 27, 12, 0, 0, 0, 5, 179)
 cftime.DatetimeGregorian(1992, 6, 30, 12, 0, 0, 0, 1, 182)
 cftime.DatetimeGregorian(1992, 7, 3, 12, 0, 0, 0, 4, 185)
 cftime.DatetimeGregorian(1992, 7, 6, 12, 0, 0, 0, 0, 188)
 cftime.DatetimeGregorian(1992, 7, 9, 12, 0, 0, 0, 3, 191)
 cftime.DatetimeGregorian(1992, 7, 12, 12, 0, 0, 0, 6, 194)
 cftime.DatetimeGregorian(1992, 7, 15, 12, 0, 0, 0, 2, 197)
 cftime.DatetimeGregorian(1992, 7, 18, 12, 0, 0, 0, 5, 200)
 cftime.DatetimeGregorian(1992, 7, 21, 12, 0, 0, 0, 1, 203)
 cftime.DatetimeGregorian(1992, 7, 24, 12, 0, 0, 0, 4, 206)
 cftime.DatetimeGregorian(1992, 7, 27, 12, 0, 0, 0, 0, 209)
 cftime.DatetimeGregorian(1992, 7, 30, 12, 0, 0, 0, 3, 212)
 cftime.DatetimeGregorian(1992, 8, 2, 12, 0, 0, 0, 6, 215)
 cftime.DatetimeGregorian(1992, 8, 5, 12, 0, 0, 0, 2, 218)
 cftime.DatetimeGregorian(1992, 8, 8, 12, 0, 0, 0, 5, 221)
 cftime.DatetimeGregorian(1992, 8, 11, 12, 0, 0, 0, 1, 224)
 cftime.DatetimeGregorian(1992, 8, 14, 12, 0, 0, 0, 4, 227)
 cftime.DatetimeGregorian(1992, 8, 17, 12, 0, 0, 0, 0, 230)
 cftime.DatetimeGregorian(1992, 8, 20, 12, 0, 0, 0, 3, 233)
 cftime.DatetimeGregorian(1992, 8, 23, 12, 0, 0, 0, 6, 236)
 cftime.DatetimeGregorian(1992, 8, 26, 12, 0, 0, 0, 2, 239)
 cftime.DatetimeGregorian(1992, 8, 29, 12, 0, 0, 0, 5, 242)
 cftime.DatetimeGregorian(1992, 9, 1, 12, 0, 0, 0, 1, 245)
 cftime.DatetimeGregorian(1992, 9, 4, 12, 0, 0, 0, 4, 248)
 cftime.DatetimeGregorian(1992, 9, 7, 12, 0, 0, 0, 0, 251)
 cftime.DatetimeGregorian(1992, 9, 10, 12, 0, 0, 0, 3, 254)
 cftime.DatetimeGregorian(1992, 9, 13, 12, 0, 0, 0, 6, 257)
 cftime.DatetimeGregorian(1992, 9, 16, 12, 0, 0, 0, 2, 260)
 cftime.DatetimeGregorian(1992, 9, 19, 12, 0, 0, 0, 5, 263)
 cftime.DatetimeGregorian(1992, 9, 22, 12, 0, 0, 0, 1, 266)
 cftime.DatetimeGregorian(1992, 9, 25, 12, 0, 0, 0, 4, 269)
 cftime.DatetimeGregorian(1992, 9, 28, 12, 0, 0, 0, 0, 272)
 cftime.DatetimeGregorian(1992, 10, 1, 12, 0, 0, 0, 3, 275)
 cftime.DatetimeGregorian(1992, 10, 4, 12, 0, 0, 0, 6, 278)
 cftime.DatetimeGregorian(1992, 10, 7, 12, 0, 0, 0, 2, 281)
 cftime.DatetimeGregorian(1992, 10, 10, 12, 0, 0, 0, 5, 284)
 cftime.DatetimeGregorian(1992, 10, 13, 12, 0, 0, 0, 1, 287)
 cftime.DatetimeGregorian(1992, 10, 16, 12, 0, 0, 0, 4, 290)
 cftime.DatetimeGregorian(1992, 10, 19, 12, 0, 0, 0, 0, 293)
 cftime.DatetimeGregorian(1992, 10, 22, 12, 0, 0, 0, 3, 296)
 cftime.DatetimeGregorian(1992, 10, 25, 12, 0, 0, 0, 6, 299)
 cftime.DatetimeGregorian(1992, 10, 28, 12, 0, 0, 0, 2, 302)
 cftime.DatetimeGregorian(1992, 10, 31, 12, 0, 0, 0, 5, 305)
 cftime.DatetimeGregorian(1992, 11, 3, 12, 0, 0, 0, 1, 308)
 cftime.DatetimeGregorian(1992, 11, 6, 12, 0, 0, 0, 4, 311)
 cftime.DatetimeGregorian(1992, 11, 9, 12, 0, 0, 0, 0, 314)
 cftime.DatetimeGregorian(1992, 11, 12, 12, 0, 0, 0, 3, 317)
 cftime.DatetimeGregorian(1992, 11, 15, 12, 0, 0, 0, 6, 320)
 cftime.DatetimeGregorian(1992, 11, 18, 12, 0, 0, 0, 2, 323)
 cftime.DatetimeGregorian(1992, 11, 21, 12, 0, 0, 0, 5, 326)
 cftime.DatetimeGregorian(1992, 11, 24, 12, 0, 0, 0, 1, 329)
 cftime.DatetimeGregorian(1992, 11, 27, 12, 0, 0, 0, 4, 332)
 cftime.DatetimeGregorian(1992, 11, 30, 12, 0, 0, 0, 0, 335)
 cftime.DatetimeGregorian(1992, 12, 3, 12, 0, 0, 0, 3, 338)
 cftime.DatetimeGregorian(1992, 12, 6, 12, 0, 0, 0, 6, 341)
 cftime.DatetimeGregorian(1992, 12, 9, 12, 0, 0, 0, 2, 344)
 cftime.DatetimeGregorian(1992, 12, 12, 12, 0, 0, 0, 5, 347)
 cftime.DatetimeGregorian(1992, 12, 15, 12, 0, 0, 0, 1, 350)
 cftime.DatetimeGregorian(1992, 12, 18, 12, 0, 0, 0, 4, 353)
 cftime.DatetimeGregorian(1992, 12, 21, 12, 0, 0, 0, 0, 356)
 cftime.DatetimeGregorian(1992, 12, 24, 12, 0, 0, 0, 3, 359)
 cftime.DatetimeGregorian(1992, 12, 27, 12, 0, 0, 0, 6, 362)
 cftime.DatetimeGregorian(1992, 12, 30, 12, 0, 0, 0, 2, 365)
 cftime.DatetimeGregorian(1993, 1, 2, 12, 0, 0, 0, 5, 2)
 cftime.DatetimeGregorian(1993, 1, 5, 12, 0, 0, 0, 1, 5)
 cftime.DatetimeGregorian(1993, 1, 8, 12, 0, 0, 0, 4, 8)
 cftime.DatetimeGregorian(1993, 1, 11, 12, 0, 0, 0, 0, 11)
 cftime.DatetimeGregorian(1993, 1, 14, 12, 0, 0, 0, 3, 14)
 cftime.DatetimeGregorian(1993, 1, 17, 12, 0, 0, 0, 6, 17)
 cftime.DatetimeGregorian(1993, 1, 20, 12, 0, 0, 0, 2, 20)
 cftime.DatetimeGregorian(1993, 1, 23, 12, 0, 0, 0, 5, 23)
 cftime.DatetimeGregorian(1993, 1, 26, 12, 0, 0, 0, 1, 26)
 cftime.DatetimeGregorian(1993, 1, 29, 12, 0, 0, 0, 4, 29)
 cftime.DatetimeGregorian(1993, 2, 1, 12, 0, 0, 0, 0, 32)
 cftime.DatetimeGregorian(1993, 2, 4, 12, 0, 0, 0, 3, 35)
 cftime.DatetimeGregorian(1993, 2, 7, 12, 0, 0, 0, 6, 38)
 cftime.DatetimeGregorian(1993, 2, 10, 12, 0, 0, 0, 2, 41)
 cftime.DatetimeGregorian(1993, 2, 13, 12, 0, 0, 0, 5, 44)
 cftime.DatetimeGregorian(1993, 2, 16, 12, 0, 0, 0, 1, 47)
 cftime.DatetimeGregorian(1993, 2, 19, 12, 0, 0, 0, 4, 50)
 cftime.DatetimeGregorian(1993, 2, 22, 12, 0, 0, 0, 0, 53)
 cftime.DatetimeGregorian(1993, 2, 25, 12, 0, 0, 0, 3, 56)
 cftime.DatetimeGregorian(1993, 2, 28, 12, 0, 0, 0, 6, 59)
 cftime.DatetimeGregorian(1993, 3, 3, 12, 0, 0, 0, 2, 62)
 cftime.DatetimeGregorian(1993, 3, 6, 12, 0, 0, 0, 5, 65)
 cftime.DatetimeGregorian(1993, 3, 9, 12, 0, 0, 0, 1, 68)
 cftime.DatetimeGregorian(1993, 3, 12, 12, 0, 0, 0, 4, 71)
 cftime.DatetimeGregorian(1993, 3, 15, 12, 0, 0, 0, 0, 74)
 cftime.DatetimeGregorian(1993, 3, 18, 12, 0, 0, 0, 3, 77)
 cftime.DatetimeGregorian(1993, 3, 21, 12, 0, 0, 0, 6, 80)
 cftime.DatetimeGregorian(1993, 3, 24, 12, 0, 0, 0, 2, 83)
 cftime.DatetimeGregorian(1993, 3, 27, 12, 0, 0, 0, 5, 86)
 cftime.DatetimeGregorian(1993, 3, 30, 12, 0, 0, 0, 1, 89)
 cftime.DatetimeGregorian(1993, 4, 2, 12, 0, 0, 0, 4, 92)
 cftime.DatetimeGregorian(1993, 4, 5, 12, 0, 0, 0, 0, 95)
 cftime.DatetimeGregorian(1993, 4, 8, 12, 0, 0, 0, 3, 98)
 cftime.DatetimeGregorian(1993, 4, 11, 12, 0, 0, 0, 6, 101)
 cftime.DatetimeGregorian(1993, 4, 14, 12, 0, 0, 0, 2, 104)
 cftime.DatetimeGregorian(1993, 4, 17, 12, 0, 0, 0, 5, 107)
 cftime.DatetimeGregorian(1993, 4, 20, 12, 0, 0, 0, 1, 110)
 cftime.DatetimeGregorian(1993, 4, 23, 12, 0, 0, 0, 4, 113)
 cftime.DatetimeGregorian(1993, 4, 26, 12, 0, 0, 0, 0, 116)
 cftime.DatetimeGregorian(1993, 4, 29, 12, 0, 0, 0, 3, 119)]
------------Time2:
[cftime.DatetimeGregorian(1992, 5, 1, 12, 0, 0, 0, 4, 122)
 cftime.DatetimeGregorian(1992, 5, 4, 12, 0, 0, 0, 0, 125)
 cftime.DatetimeGregorian(1992, 5, 7, 12, 0, 0, 0, 3, 128)
 cftime.DatetimeGregorian(1992, 5, 10, 12, 0, 0, 0, 6, 131)
 cftime.DatetimeGregorian(1992, 5, 13, 12, 0, 0, 0, 2, 134)
 cftime.DatetimeGregorian(1992, 5, 16, 12, 0, 0, 0, 5, 137)
 cftime.DatetimeGregorian(1992, 5, 19, 12, 0, 0, 0, 1, 140)
 cftime.DatetimeGregorian(1992, 5, 22, 12, 0, 0, 0, 4, 143)
 cftime.DatetimeGregorian(1992, 5, 25, 12, 0, 0, 0, 0, 146)
 cftime.DatetimeGregorian(1992, 5, 28, 12, 0, 0, 0, 3, 149)
 cftime.DatetimeGregorian(1992, 5, 31, 12, 0, 0, 0, 6, 152)
 cftime.DatetimeGregorian(1992, 6, 3, 12, 0, 0, 0, 2, 155)
 cftime.DatetimeGregorian(1992, 6, 6, 12, 0, 0, 0, 5, 158)
 cftime.DatetimeGregorian(1992, 6, 9, 12, 0, 0, 0, 1, 161)
 cftime.DatetimeGregorian(1992, 6, 12, 12, 0, 0, 0, 4, 164)
 cftime.DatetimeGregorian(1992, 6, 15, 12, 0, 0, 0, 0, 167)
 cftime.DatetimeGregorian(1992, 6, 18, 12, 0, 0, 0, 3, 170)
 cftime.DatetimeGregorian(1992, 6, 21, 12, 0, 0, 0, 6, 173)
 cftime.DatetimeGregorian(1992, 6, 24, 12, 0, 0, 0, 2, 176)
 cftime.DatetimeGregorian(1992, 6, 27, 12, 0, 0, 0, 5, 179)
 cftime.DatetimeGregorian(1992, 6, 30, 12, 0, 0, 0, 1, 182)
 cftime.DatetimeGregorian(1992, 7, 3, 12, 0, 0, 0, 4, 185)
 cftime.DatetimeGregorian(1992, 7, 6, 12, 0, 0, 0, 0, 188)
 cftime.DatetimeGregorian(1992, 7, 9, 12, 0, 0, 0, 3, 191)
 cftime.DatetimeGregorian(1992, 7, 12, 12, 0, 0, 0, 6, 194)
 cftime.DatetimeGregorian(1992, 7, 15, 12, 0, 0, 0, 2, 197)
 cftime.DatetimeGregorian(1992, 7, 18, 12, 0, 0, 0, 5, 200)
 cftime.DatetimeGregorian(1992, 7, 21, 12, 0, 0, 0, 1, 203)
 cftime.DatetimeGregorian(1992, 7, 24, 12, 0, 0, 0, 4, 206)
 cftime.DatetimeGregorian(1992, 7, 27, 12, 0, 0, 0, 0, 209)
 cftime.DatetimeGregorian(1992, 7, 30, 12, 0, 0, 0, 3, 212)
 cftime.DatetimeGregorian(1992, 8, 2, 12, 0, 0, 0, 6, 215)
 cftime.DatetimeGregorian(1992, 8, 5, 12, 0, 0, 0, 2, 218)
 cftime.DatetimeGregorian(1992, 8, 8, 12, 0, 0, 0, 5, 221)
 cftime.DatetimeGregorian(1992, 8, 11, 12, 0, 0, 0, 1, 224)
 cftime.DatetimeGregorian(1992, 8, 14, 12, 0, 0, 0, 4, 227)
 cftime.DatetimeGregorian(1992, 8, 17, 12, 0, 0, 0, 0, 230)
 cftime.DatetimeGregorian(1992, 8, 20, 12, 0, 0, 0, 3, 233)
 cftime.DatetimeGregorian(1992, 8, 23, 12, 0, 0, 0, 6, 236)
 cftime.DatetimeGregorian(1992, 8, 26, 12, 0, 0, 0, 2, 239)
 cftime.DatetimeGregorian(1992, 8, 29, 12, 0, 0, 0, 5, 242)
 cftime.DatetimeGregorian(1992, 9, 1, 12, 0, 0, 0, 1, 245)
 cftime.DatetimeGregorian(1992, 9, 4, 12, 0, 0, 0, 4, 248)
 cftime.DatetimeGregorian(1992, 9, 7, 12, 0, 0, 0, 0, 251)
 cftime.DatetimeGregorian(1992, 9, 10, 12, 0, 0, 0, 3, 254)
 cftime.DatetimeGregorian(1992, 9, 13, 12, 0, 0, 0, 6, 257)
 cftime.DatetimeGregorian(1992, 9, 16, 12, 0, 0, 0, 2, 260)
 cftime.DatetimeGregorian(1992, 9, 19, 12, 0, 0, 0, 5, 263)
 cftime.DatetimeGregorian(1992, 9, 22, 12, 0, 0, 0, 1, 266)
 cftime.DatetimeGregorian(1992, 9, 25, 12, 0, 0, 0, 4, 269)
 cftime.DatetimeGregorian(1992, 9, 28, 12, 0, 0, 0, 0, 272)
 cftime.DatetimeGregorian(1992, 10, 1, 12, 0, 0, 0, 3, 275)
 cftime.DatetimeGregorian(1992, 10, 4, 12, 0, 0, 0, 6, 278)
 cftime.DatetimeGregorian(1992, 10, 7, 12, 0, 0, 0, 2, 281)
 cftime.DatetimeGregorian(1992, 10, 10, 12, 0, 0, 0, 5, 284)
 cftime.DatetimeGregorian(1992, 10, 13, 12, 0, 0, 0, 1, 287)
 cftime.DatetimeGregorian(1992, 10, 16, 12, 0, 0, 0, 4, 290)
 cftime.DatetimeGregorian(1992, 10, 19, 12, 0, 0, 0, 0, 293)
 cftime.DatetimeGregorian(1992, 10, 22, 12, 0, 0, 0, 3, 296)
 cftime.DatetimeGregorian(1992, 10, 25, 12, 0, 0, 0, 6, 299)
 cftime.DatetimeGregorian(1992, 10, 28, 12, 0, 0, 0, 2, 302)
 cftime.DatetimeGregorian(1992, 10, 31, 12, 0, 0, 0, 5, 305)
 cftime.DatetimeGregorian(1992, 11, 3, 12, 0, 0, 0, 1, 308)
 cftime.DatetimeGregorian(1992, 11, 6, 12, 0, 0, 0, 4, 311)
 cftime.DatetimeGregorian(1992, 11, 9, 12, 0, 0, 0, 0, 314)
 cftime.DatetimeGregorian(1992, 11, 12, 12, 0, 0, 0, 3, 317)
 cftime.DatetimeGregorian(1992, 11, 15, 12, 0, 0, 0, 6, 320)
 cftime.DatetimeGregorian(1992, 11, 18, 12, 0, 0, 0, 2, 323)
 cftime.DatetimeGregorian(1992, 11, 21, 12, 0, 0, 0, 5, 326)
 cftime.DatetimeGregorian(1992, 11, 24, 12, 0, 0, 0, 1, 329)
 cftime.DatetimeGregorian(1992, 11, 27, 12, 0, 0, 0, 4, 332)
 cftime.DatetimeGregorian(1992, 11, 30, 12, 0, 0, 0, 0, 335)
 cftime.DatetimeGregorian(1992, 12, 3, 12, 0, 0, 0, 3, 338)
 cftime.DatetimeGregorian(1992, 12, 6, 12, 0, 0, 0, 6, 341)
 cftime.DatetimeGregorian(1992, 12, 9, 12, 0, 0, 0, 2, 344)
 cftime.DatetimeGregorian(1992, 12, 12, 12, 0, 0, 0, 5, 347)
 cftime.DatetimeGregorian(1992, 12, 15, 12, 0, 0, 0, 1, 350)
 cftime.DatetimeGregorian(1992, 12, 18, 12, 0, 0, 0, 4, 353)
 cftime.DatetimeGregorian(1992, 12, 21, 12, 0, 0, 0, 0, 356)
 cftime.DatetimeGregorian(1992, 12, 24, 12, 0, 0, 0, 3, 359)
 cftime.DatetimeGregorian(1992, 12, 27, 12, 0, 0, 0, 6, 362)
 cftime.DatetimeGregorian(1992, 12, 30, 12, 0, 0, 0, 2, 365)
 cftime.DatetimeGregorian(1993, 1, 2, 12, 0, 0, 0, 5, 2)
 cftime.DatetimeGregorian(1993, 1, 5, 12, 0, 0, 0, 1, 5)
 cftime.DatetimeGregorian(1993, 1, 8, 12, 0, 0, 0, 4, 8)
 cftime.DatetimeGregorian(1993, 1, 11, 12, 0, 0, 0, 0, 11)
 cftime.DatetimeGregorian(1993, 1, 14, 12, 0, 0, 0, 3, 14)
 cftime.DatetimeGregorian(1993, 1, 17, 12, 0, 0, 0, 6, 17)
 cftime.DatetimeGregorian(1993, 1, 20, 12, 0, 0, 0, 2, 20)
 cftime.DatetimeGregorian(1993, 1, 23, 12, 0, 0, 0, 5, 23)
 cftime.DatetimeGregorian(1993, 1, 26, 12, 0, 0, 0, 1, 26)
 cftime.DatetimeGregorian(1993, 1, 29, 12, 0, 0, 0, 4, 29)
 cftime.DatetimeGregorian(1993, 2, 1, 12, 0, 0, 0, 0, 32)
 cftime.DatetimeGregorian(1993, 2, 4, 12, 0, 0, 0, 3, 35)
 cftime.DatetimeGregorian(1993, 2, 7, 12, 0, 0, 0, 6, 38)
 cftime.DatetimeGregorian(1993, 2, 10, 12, 0, 0, 0, 2, 41)
 cftime.DatetimeGregorian(1993, 2, 13, 12, 0, 0, 0, 5, 44)
 cftime.DatetimeGregorian(1993, 2, 16, 12, 0, 0, 0, 1, 47)
 cftime.DatetimeGregorian(1993, 2, 19, 12, 0, 0, 0, 4, 50)
 cftime.DatetimeGregorian(1993, 2, 22, 12, 0, 0, 0, 0, 53)
 cftime.DatetimeGregorian(1993, 2, 25, 12, 0, 0, 0, 3, 56)
 cftime.DatetimeGregorian(1993, 2, 28, 12, 0, 0, 0, 6, 59)
 cftime.DatetimeGregorian(1993, 3, 3, 12, 0, 0, 0, 2, 62)
 cftime.DatetimeGregorian(1993, 3, 6, 12, 0, 0, 0, 5, 65)
 cftime.DatetimeGregorian(1993, 3, 9, 12, 0, 0, 0, 1, 68)
 cftime.DatetimeGregorian(1993, 3, 12, 12, 0, 0, 0, 4, 71)
 cftime.DatetimeGregorian(1993, 3, 15, 12, 0, 0, 0, 0, 74)
 cftime.DatetimeGregorian(1993, 3, 18, 12, 0, 0, 0, 3, 77)
 cftime.DatetimeGregorian(1993, 3, 21, 12, 0, 0, 0, 6, 80)
 cftime.DatetimeGregorian(1993, 3, 24, 12, 0, 0, 0, 2, 83)
 cftime.DatetimeGregorian(1993, 3, 27, 12, 0, 0, 0, 5, 86)
 cftime.DatetimeGregorian(1993, 3, 30, 12, 0, 0, 0, 1, 89)
 cftime.DatetimeGregorian(1993, 4, 2, 12, 0, 0, 0, 4, 92)
 cftime.DatetimeGregorian(1993, 4, 5, 12, 0, 0, 0, 0, 95)
 cftime.DatetimeGregorian(1993, 4, 8, 12, 0, 0, 0, 3, 98)
 cftime.DatetimeGregorian(1993, 4, 11, 12, 0, 0, 0, 6, 101)
 cftime.DatetimeGregorian(1993, 4, 14, 12, 0, 0, 0, 2, 104)
 cftime.DatetimeGregorian(1993, 4, 17, 12, 0, 0, 0, 5, 107)
 cftime.DatetimeGregorian(1993, 4, 20, 12, 0, 0, 0, 1, 110)
 cftime.DatetimeGregorian(1993, 4, 23, 12, 0, 0, 0, 4, 113)
 cftime.DatetimeGregorian(1993, 4, 26, 12, 0, 0, 0, 0, 116)
 cftime.DatetimeGregorian(1993, 4, 29, 12, 0, 0, 0, 3, 119)]
------------------Var1:
[223.11557006835938, 221.9438018798828, 221.8140106201172, 222.05514526367188, 221.9300994873047, 221.59202575683594, 220.8131561279297, 220.2032470703125, 220.04214477539062, 219.3798065185547, 218.103515625, 217.37628173828125, 215.52098083496094, 214.50900268554688, 214.05906677246094, 213.059326171875, 211.69723510742188, 211.15106201171875, 210.4863739013672, 209.68116760253906, 209.54156494140625, 209.27822875976562, 209.19239807128906, 209.3609161376953, 209.8040313720703, 209.49354553222656, 208.9561004638672, 208.76173400878906, 208.63673400878906, 208.7616424560547, 208.60935974121094, 207.95498657226562, 207.4456024169922, 207.5854034423828, 207.37570190429688, 207.29464721679688, 206.9185791015625, 206.71054077148438, 206.66046142578125, 206.58499145507812, 206.5628662109375, 206.77227783203125, 206.95872497558594, 207.17898559570312, 207.0110321044922, 206.72427368164062, 206.4315643310547, 206.22303771972656, 206.39205932617188, 206.29702758789062, 206.0764923095703, 206.0755157470703, 206.0810089111328, 206.04075622558594, 206.6553497314453, 207.7744903564453, 208.12513732910156, 208.49803161621094, 208.63113403320312, 208.3790740966797, 208.23716735839844, 208.2624969482422, 209.67971801757812, 210.9297637939453, 210.8618621826172, 211.33926391601562, 212.47804260253906, 213.3290557861328, 214.4900665283203, 215.29322814941406, 215.9776611328125, 216.19512939453125, 215.9586944580078, 216.08016967773438, 216.20069885253906, 216.4625701904297, 216.65594482421875, 216.8386993408203, 216.86822509765625, 217.0234375, 217.27996826171875, 217.43051147460938, 218.10020446777344, 218.64846801757812, 219.40756225585938, 220.22715759277344, 221.1670684814453, 222.00205993652344, 222.13937377929688, 222.16209411621094, 222.35919189453125, 222.7753143310547, 223.6350860595703, 224.2841339111328, 224.9336395263672, 225.40081787109375, 225.66600036621094, 225.94699096679688, 225.74618530273438, 225.49330139160156, 224.81842041015625, 224.21290588378906, 222.95877075195312, 221.85479736328125, 221.15855407714844, 220.6728973388672, 222.57798767089844, 225.26876831054688, 227.08294677734375, 225.60366821289062, 224.18670654296875, 224.68218994140625, 223.9373779296875, 221.2315216064453, 219.7241973876953, 218.8666534423828, 218.505615234375, 218.1119842529297, 217.94349670410156, 218.3512725830078, 218.3766632080078, 218.12945556640625]
------------------Var2:
[1.8699977317737648e-06, 1.7030317849275889e-06, 1.2199531056467094e-06, 1.397972027916694e-06, 1.8590178569866112e-06, 2.451550699333893e-06, 2.2460897071141517e-06, 1.7662408708929433e-06, 1.794068907656765e-06, 2.5392387215106282e-06, 2.4256853521364974e-06, 2.200222297688015e-06, 1.8892502566814073e-06, 1.293990408157697e-06, 1.273378529731417e-06, 1.3175330195736024e-06, 1.3202283071223064e-06, 1.4671226153950556e-06, 1.4339698282128666e-06, 9.214538181367971e-07, 7.716643040112103e-07, 8.233504900090338e-07, 9.834145657805493e-07, 1.13705550575105e-06, 1.1791184988396708e-06, 1.2756848946082755e-06, 1.2582946737893508e-06, 1.2198855756651028e-06, 1.2812246268367744e-06, 1.3231093589638476e-06, 1.3970025065646041e-06, 1.576343265696778e-06, 1.7354720966977766e-06, 1.7077043139579473e-06, 1.7235327050002525e-06, 1.5648772659915267e-06, 1.4376404351423844e-06, 1.413581230735872e-06, 1.4421271998799057e-06, 1.4850011211819947e-06, 1.3147893014320289e-06, 1.2682968417720986e-06, 1.2790349046554184e-06, 1.2716803894363693e-06, 1.7657008584137657e-06, 1.5152533023865544e-06, 1.4587960777134867e-06, 1.2978910035599256e-06, 1.1267452464380767e-06, 1.291074568143813e-06, 1.282710854866309e-06, 1.1159229416080052e-06, 1.3812865518048056e-06, 1.1400628636693e-06, 9.18344426281692e-07, 8.262929895863635e-07, 8.515459626323718e-07, 9.54267306951806e-07, 1.120786805586249e-06, 1.0574864290902042e-06, 1.0432141834826325e-06, 1.0639150787028484e-06, 8.412418992520543e-07, 6.619796408813272e-07, 8.642333568786853e-07, 9.760434522831929e-07, 8.839019756123889e-07, 8.46264299525501e-07, 6.582086484741012e-07, 5.76201273361221e-07, 5.676289447364979e-07, 6.281823061726755e-07, 6.872983817629574e-07, 6.288182134994713e-07, 5.932287763243949e-07, 5.871376629329461e-07, 5.780349852102518e-07, 6.543318704643752e-07, 7.62506886076153e-07, 6.864958663754805e-07, 7.205930501186231e-07, 8.061796847869118e-07, 7.490534130738524e-07, 7.754077842037077e-07, 7.751717703285976e-07, 8.005614517969661e-07, 8.521130325789272e-07, 9.713140798339737e-07, 1.0931577207884402e-06, 1.3158057754480978e-06, 1.2712253010249697e-06, 1.319074385719432e-06, 1.44519970035617e-06, 1.629124540158955e-06, 1.84860869012482e-06, 2.067993136734003e-06, 2.3376173885480966e-06, 3.2310172173311003e-06, 3.3292842545051826e-06, 2.4428222786809783e-06, 2.0484160359046655e-06, 1.5956686638674e-06, 1.1383971241230029e-06, 8.780877465142112e-07, 7.167565172494506e-07, 6.504005227725429e-07, 6.561199938914797e-07, 1.1931011840715655e-06, 2.439803211018443e-06, 2.3742720713926246e-06, 2.6326927127229283e-06, 2.623149839564576e-06, 2.358844540140126e-06, 2.4374953682126943e-06, 2.1192288386373548e-06, 1.911011395350215e-06, 2.072626784865861e-06, 2.518577502996777e-06, 1.701122528174892e-06, 1.5920745681796689e-06, 1.772317318682326e-06, 1.964325520020793e-06]
```
</div>
</div>
<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">

<div markdown="0" class="output output_html">

    <div class="bk-root">
        <a href="https://bokeh.pydata.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
        <span id="1580">Loading BokehJS ...</span>
    </div>
</div>

</div>
</div>
<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">

</div>
</div>
<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">
{:.output_traceback_line}
```

    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    <ipython-input-50-d5f28ec9deac> in <module>()
         11 exportDataFlag = False      # True if you you want to download data
         12 
    ---> 13 xarrayPlotXY(tables, variables, startDate, endDate, lat1, lat2, lon1, lon2, depth1, depth2, fname, exportDataFlag)
    

    <ipython-input-49-6ae4622b961a> in xarrayPlotXY(tables, variables, startDate, endDate, lat1, lat2, lon1, lon2, depth1, depth2, fname, exportDataFlag, marker, msize, clr)
         45         output_notebook()
         46         p1 = figure(tools=TOOLS, toolbar_location="above", plot_width=w, plot_height=h)
    ---> 47         p1.xaxis.axis_label = variablePairs[i][0] + ' [' + db.getVar(tablePairs[i][0], variablePairs[i][0]).iloc[0]['Unit'] + ']'
         48         p1.yaxis.axis_label = variablePairs[i][1] + ' [' + db.getVar(tablePairs[i][1], variablePairs[i][1]).iloc[0]['Unit'] + ']'
         49         leg = variablePairs[i][0] + ' / ' + variablePairs[i][1]


    /anaconda3/lib/python3.7/site-packages/pandas/core/indexing.py in __getitem__(self, key)
       1498 
       1499             maybe_callable = com.apply_if_callable(key, self.obj)
    -> 1500             return self._getitem_axis(maybe_callable, axis=axis)
       1501 
       1502     def _is_scalar_access(self, key):


    /anaconda3/lib/python3.7/site-packages/pandas/core/indexing.py in _getitem_axis(self, key, axis)
       2228 
       2229             # validate the location
    -> 2230             self._validate_integer(key, axis)
       2231 
       2232             return self._get_loc(key, axis=axis)


    /anaconda3/lib/python3.7/site-packages/pandas/core/indexing.py in _validate_integer(self, key, axis)
       2137         len_axis = len(self.obj._get_axis(axis))
       2138         if key >= len_axis or key < -len_axis:
    -> 2139             raise IndexError("single positional indexer is out-of-bounds")
       2140 
       2141     def _getitem_tuple(self, tup):


    IndexError: single positional indexer is out-of-bounds


```
</div>
</div>
</div>



### Original Function



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
def plotXY(tables, variables, startDate, endDate, lat1, lat2, lon1, lon2, depth1, depth2, fname, exportDataFlag, marker='-', msize=15, clr='green'):
    p = []
    lw = 2
    w = 500
    h = 500
    TOOLS = 'pan,wheel_zoom,zoom_in,zoom_out,box_zoom, undo,redo,reset,tap,save,box_select,poly_select,lasso_select'
    tablePairs = list(itt.combinations(tables, 2))
    variablePairs = list(itt.combinations(variables, 2))
    for i in tqdm(range(len(tablePairs)), desc='overall'):
        t1, y1, y_std1 = TS.timeSeries(tablePairs[i][0], variablePairs[i][0], startDate, endDate, lat1, lat2, lon1, lon2, depth1, depth2)
        t2, y2, y_std2 = TS.timeSeries(tablePairs[i][1], variablePairs[i][1], startDate, endDate, lat1, lat2, lon1, lon2, depth1, depth2)
        
        if exportDataFlag:
            exportData(t1, y1, y_std1, t2, y2, y_std2, tablePairs[i][0], variablePairs[i][0], tablePairs[i][1], variablePairs[i][1], lat1, lat2, lon1, lon2, depth1, depth2)

        if len(y1[~np.isnan(y1)]) < 1:
            com.printTQDM('%d: No matching entry found: Table: %s, Variable: %s ' % (i+1, tablePairs[i][0], variablePairs[i][0]), err=True )
            # continue
        com.printTQDM('%d: %s retrieved (%s).' % (i+1, variablePairs[i][0], tablePairs[i][0]), err=False)    
        if len(y2[~np.isnan(y2)]) < 1:
            com.printTQDM('%d: No matching entry found: Table: %s, Variable: %s ' % (i+1, tablePairs[i][1], variablePairs[i][1]), err=True )
            # continue
        com.printTQDM('%d: %s retrieved (%s).' % (i+1, variablePairs[i][1], tablePairs[i][1]), err=False)     

        if len(t1)<1 or len(y1)<1 or len(t2)<1 or len(y2)<1:
            continue
        if (len(t1)-len(t2) != 0) or (len(y1)-len(y2) != 0):   
            continue
        output_notebook()
        p1 = figure(tools=TOOLS, toolbar_location="above", plot_width=w, plot_height=h)
        p1.xaxis.axis_label = variablePairs[i][0] + ' [' + db.getVar(tablePairs[i][0], variablePairs[i][0]).iloc[0]['Unit'] + ']'
        p1.yaxis.axis_label = variablePairs[i][1] + ' [' + db.getVar(tablePairs[i][1], variablePairs[i][1]).iloc[0]['Unit'] + ']'
        leg = variablePairs[i][0] + ' / ' + variablePairs[i][1]
        fill_alpha = 0.3       
        cr = p1.circle(y1, y2, fill_color="grey", hover_fill_color="firebrick", fill_alpha=fill_alpha, hover_alpha=0.6, line_color=None, hover_line_color="white", legend=leg, size=msize)
        #p1.line(y1, y2, line_color=clr, line_width=lw, legend=leg)
        p1.add_tools(HoverTool(tooltips=None, renderers=[cr], mode='hline'))    
        p.append(p1)
    dirPath = 'embed/'
    if not os.path.exists(dirPath):
        os.makedirs(dirPath)        
   # if not inline:      ## if jupyter is not the caller
   #     output_file(dirPath + fname + ".html", title="XY")
    show(column(p))
    return

```
</div>

</div>



### NetCDF Compatible Function



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
def xarrayPlotXY(tables, variables, startDate, endDate, lat1, lat2, lon1, lon2, depth1, depth2, fname, exportDataFlag, marker='-', msize=15, clr='green'):
    p = []
    lw = 2
    w = 500
    h = 500
    TOOLS = 'pan,wheel_zoom,zoom_in,zoom_out,box_zoom, undo,redo,reset,tap,save,box_select,poly_select,lasso_select'
    tablePairs = list(itt.combinations(tables, 2))
    variablePairs = list(itt.combinations(variables, 2))
    for i in tqdm(range(len(tablePairs)), desc='overall'):
        #t1, y1, y_std1 = TS.timeSeries(tablePairs[i][0], variablePairs[i][0], startDate, endDate, lat1, lat2, lon1, lon2, depth1, depth2)
        #t2, y2, y_std2 = TS.timeSeries(tablePairs[i][1], variablePairs[i][1], startDate, endDate, lat1, lat2, lon1, lon2, depth1, depth2)
        
        table = tables[i].sel(TIME = slice(startDate, endDate), LAT_C = slice(lat1, lat2), LON_C = slice(lon1, lon2), DEP_C = slice(depth1, depth2))
        y1 = table.variables[variables[0]][:,0,0,0].values.tolist()
        y2 = table.variables[variables[1]][:,0,0,0].values.tolist()
        t1 = table.variables['TIME'].values
        t2 = table.variables['TIME'].values
        
        #print tests
        print('------------Time1:')
        print(t1)
        print('------------Time2:')
        print(t2)
        print('------------------Var1:')
        print(y1)
        print('------------------Var2:')
        print(y2)
        
        if exportDataFlag:
            exportData(t1, y1, y_std1, t2, y2, y_std2, tablePairs[i][0], variablePairs[i][0], tablePairs[i][1], variablePairs[i][1], lat1, lat2, lon1, lon2, depth1, depth2)

        #if len(y1[~np.isnan(y1)]) < 1:
        #    com.printTQDM('%d: No matching entry found: Table: %s, Variable: %s ' % (i+1, tablePairs[i][0], variablePairs[i][0]), err=True )
            # continue
        #com.printTQDM('%d: %s retrieved (%s).' % (i+1, variablePairs[i][0], tablePairs[i][0]), err=False)    
        #if len(y2[~np.isnan(y2)]) < 1:
        #    com.printTQDM('%d: No matching entry found: Table: %s, Variable: %s ' % (i+1, tablePairs[i][1], variablePairs[i][1]), err=True )
            # continue
        #com.printTQDM('%d: %s retrieved (%s).' % (i+1, variablePairs[i][1], tablePairs[i][1]), err=False)     

        if len(t1)<1 or len(y1)<1 or len(t2)<1 or len(y2)<1:
            continue
        if (len(t1)-len(t2) != 0) or (len(y1)-len(y2) != 0):   
            continue
        output_notebook()
        p1 = figure(tools=TOOLS, toolbar_location="above", plot_width=w, plot_height=h)
        p1.xaxis.axis_label = variablePairs[i][0] + ' [' + db.getVar(tablePairs[i][0], variablePairs[i][0]).iloc[0]['Unit'] + ']'
        p1.yaxis.axis_label = variablePairs[i][1] + ' [' + db.getVar(tablePairs[i][1], variablePairs[i][1]).iloc[0]['Unit'] + ']'
        leg = variablePairs[i][0] + ' / ' + variablePairs[i][1]
        fill_alpha = 0.3       
        cr = p1.circle(y1, y2, fill_color="grey", hover_fill_color="firebrick", fill_alpha=fill_alpha, hover_alpha=0.6, line_color=None, hover_line_color="white", legend=leg, size=msize)
        #p1.line(y1, y2, line_color=clr, line_width=lw, legend=leg)
        p1.add_tools(HoverTool(tooltips=None, renderers=[cr], mode='hline'))    
        p.append(p1)
    dirPath = 'embed/'
    if not os.path.exists(dirPath):
        os.makedirs(dirPath)        
   # if not inline:      ## if jupyter is not the caller
   #     print('test')
   #     output_file(dirPath + fname + ".html", title="XY")
    show(column(p))
    return

```
</div>

</div>



#### Helper Functions

