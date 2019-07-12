---
redirect_from:
  - "/functions/depthprofile"
interact_link: content/functions/DepthProfile.ipynb
kernel_name: python3
has_widgets: false
title: 'Depthprofile'
prev_page:
  url: /functions/RegionalMap
  title: 'Regionalmap'
next_page:
  url: /functions/PlotXY
  title: 'Plotxy'
comment: "***PROGRAMMATICALLY GENERATED, DO NOT EDIT. SEE ORIGINAL FILES IN /content***"
---


## Reformat netCDF4 File for Function Call



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
import opedia
import sys
import os
import numpy as np
import pandas as pd
import db
import common as com
import climatology as clim
import subset
from datetime import datetime, timedelta
import time
from math import pi
from bokeh.io import output_notebook
from bokeh.plotting import figure, show
from bokeh.layouts import column
from bokeh.models import DatetimeTickFormatter
from bokeh.palettes import all_palettes
from bokeh.models import HoverTool
from bokeh.embed import components
import jupyterInline as jup
import xarray as xr
if jup.jupytered():
    from tqdm import tqdm_notebook as tqdm
else:
    from tqdm import tqdm

```
</div>

</div>



### Testing - Original Function



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
tables = ['tblArgoMerge_REP', 'tblPisces_NRT', 'tblDarwin_Chl_Climatology']     # see catalog.csv  for the complete list of tables and variable names
variables = ['argo_merge_chl_adj', 'CHL', 'chl01_darwin_clim']
startDate = '2016-04-30'   # PISCES is a weekly model, and here we are using monthly climatology of Darwin model
endDate = '2016-04-30'
lat1, lat2 = 20, 24
lon1, lon2 = -170, -150
depth1, depth2 = 0, 1500
fname = 'DEP'
exportDataFlag = False      # True if you you want to download data

plotDepthProfile(tables, variables, startDate, endDate, lat1, lat2, lon1, lon2, depth1, depth2, fname, exportDataFlag)

```
</div>

<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">
{:.output_data_text}
```
HBox(children=(IntProgress(value=0, description='overall', max=3, style=ProgressStyle(description_width='initi…
```

</div>
</div>
<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">

<div markdown="0" class="output output_html">

    <div class="bk-root">
        <a href="https://bokeh.pydata.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
        <span id="1001">Loading BokehJS ...</span>
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

<div markdown="0" class="output output_html">

    <div class="bk-root">
        <a href="https://bokeh.pydata.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
        <span id="1093">Loading BokehJS ...</span>
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

<div markdown="0" class="output output_html">

    <div class="bk-root">
        <a href="https://bokeh.pydata.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
        <span id="1185">Loading BokehJS ...</span>
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






  <div class="bk-root" id="ce61e11e-732b-4d29-8b95-39005b225b91" data-root-id="1277"></div>

</div>

</div>
</div>
<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">

</div>
</div>
</div>



### Testing - NetCDF Compatible Function



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
xFile = xr.open_dataset('http://engaging-opendap.mit.edu:8080/thredds/dodsC/las/id-a1d60eba44/data_usr_local_tomcat_content_cbiomes_20190510_20_darwin_v0.2_cs510_darwin_v0.2_cs510_nutrients.nc.jnl')

tables = [xFile]     # see catalog.csv  for the complete list of tables and variable names
variables = ['O2']
startDate = '2010-04-30'   # PISCES is a weekly model, and here we are using monthly climatology of Darwin model
endDate = '2010-04-30'
lat1, lat2 = 20, 24
lon1, lon2 = -170, -150
depth1, depth2 = 0, 1500
fname = 'DEP'
exportDataFlag = False      # True if you you want to download data

xarrayPlotDepthProfile(tables, variables, startDate, endDate, lat1, lat2, lon1, lon2, depth1, depth2, fname, exportDataFlag)


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

<div markdown="0" class="output output_html">

    <div class="bk-root">
        <a href="https://bokeh.pydata.org" target="_blank" class="bk-logo bk-logo-small bk-logo-notebook"></a>
        <span id="1572">Loading BokehJS ...</span>
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






  <div class="bk-root" id="9cf3cf7b-eb33-428d-9c60-d39c066e956b" data-root-id="1664"></div>

</div>

</div>
</div>
<div class="output_wrapper" markdown="1">
<div class="output_subarea" markdown="1">

</div>
</div>
</div>



### Original Function



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
def plotDepthProfile(tables, variables, dt1, dt2, lat1, lat2, lon1, lon2, depth1, depth2, fname, exportDataFlag, marker='-', msize=25, clr='orangered'):
    p = []
    lw = 2
    w = 800
    h = 400
    TOOLS = 'pan,wheel_zoom,zoom_in,zoom_out,box_zoom, undo,redo,reset,tap,save,box_select,poly_select,lasso_select'
    for i in tqdm(range(len(tables)), desc='overall'):
        if not db.hasField(tables[i], 'depth'):
            continue
        if not iterative(tables[i]):    
            depths, y, yErr = depthProfile(tables[i], variables[i], dt1, dt2, lat1, lat2, lon1, lon2, depth1, depth2, fname, exportDataFlag)
        else:    
            depths, y, yErr = depthProfile_iterative(tables[i], variables[i], dt1, dt2, lat1, lat2, lon1, lon2, depth1, depth2, fname, exportDataFlag)
        
        output_notebook()
        p1 = figure(tools=TOOLS, toolbar_location="above", plot_width=w, plot_height=h)
        #p1.xaxis.axis_label = 'Depth'
        p1.yaxis.axis_label = variables[i] + ' [' + db.getVar(tables[i], variables[i]).iloc[0]['Unit'] + ']'
        leg = variables[i]
        cr = p1.circle(depths, y, fill_color="grey", hover_fill_color="firebrick", fill_alpha=0.25, hover_alpha=0.3, line_color=None, hover_line_color="white", legend=leg, size=msize)
        p1.line(depths, y, line_color=clr, line_width=lw, legend=leg)
        p1.add_tools(HoverTool(tooltips=None, renderers=[cr], mode='hline'))
        p.append(p1)
    dirPath = 'embed/'
    if not os.path.exists(dirPath):
        os.makedirs(dirPath)        
  #  if not inline:      ## if jupyter is not the caller
  #      output_file(dirPath + fname + ".html", title="Depth Profile")
    show(column(p))
    return


```
</div>

</div>



### NetCDF Compatible Function



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
def xarrayPlotDepthProfile(tables, variables, dt1, dt2, lat1, lat2, lon1, lon2, depth1, depth2, fname, exportDataFlag, marker='-', msize=25, clr='orangered'):
    p = []
    lw = 2
    w = 800
    h = 400
    TOOLS = 'pan,wheel_zoom,zoom_in,zoom_out,box_zoom, undo,redo,reset,tap,save,box_select,poly_select,lasso_select'
    for i in tqdm(range(len(tables)), desc='overall'):
        #if not db.hasField(tables[i], 'depth'):
        #    continue
        #if not iterative(tables[i]):    
        #    depths, y, yErr = depthProfile(tables[i], variables[i], dt1, dt2, lat1, lat2, lon1, lon2, depth1, depth2, fname, exportDataFlag)
        #else:    
        #    depths, y, yErr = depthProfile_iterative(tables[i], variables[i], dt1, dt2, lat1, lat2, lon1, lon2, depth1, depth2, fname, exportDataFlag)
        
        table = tables[i].sel(TIME = slice(dt1, dt2), LAT_C = slice(lat1, lat2), LON_C = slice(lon1, lon2), DEP_C = slice(depth1, depth2))
        depths = np.unique(table.variables['DEP_C'].values)
        
        varList = table.variables[variables[i]][:].values
        varList[varList < 0] = float('NaN')
        varList = varList.tolist()[0][:][0][0]
        
        varData = []
        for list in varList:
            varData.append(np.mean(list))
        
        output_notebook()
        p1 = figure(tools=TOOLS, toolbar_location="above", plot_width=w, plot_height=h)
        #p1.xaxis.axis_label = 'Depth'
        p1.yaxis.axis_label = variables[i] + ' [PLACEHOLDER]'
        leg = variables[i]
        cr = p1.circle(depths, varData, fill_color="grey", hover_fill_color="firebrick", fill_alpha=0.25, hover_alpha=0.3, line_color=None, hover_line_color="white", legend=leg, size=msize)
        p1.line(depths, varData, line_color=clr, line_width=lw, legend=leg)
        p1.add_tools(HoverTool(tooltips=None, renderers=[cr], mode='hline'))
        p.append(p1)
    dirPath = 'embed/'
    if not os.path.exists(dirPath):
        os.makedirs(dirPath)        
  #  if not inline:      ## if jupyter is not the caller
  #      output_file(dirPath + fname + ".html", title="Depth Profile")
    show(column(p))
    return


```
</div>

</div>



#### Helper Functions (for both)



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
def iterative(table):
    table = table.lower()
    it = False
    if table.find('tblDarwin'.lower()) != -1:
        it = True
    if table.find('tblPisces'.lower()) != -1:
        it = True
    return it

```
</div>

</div>



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
def depthProfile(table, field, dt1, dt2, lat1, lat2, lon1, lon2, depth1, depth2, fname, exportDataFlag):
    df = subset.depthProfile(table, field, dt1, dt2, lat1, lat2, lon1, lon2, depth1, depth2)
    if exportDataFlag:
        exportData(df['depth'], df[field], df[field + '_std'], table, field, dt1, dt2, lat1, lat2, lon1, lon2, fname)    
    return df['depth'], df[field], df[field + '_std']


```
</div>

</div>



<div markdown="1" class="cell code_cell">
<div class="input_area" markdown="1">
```python
def depthProfile_iterative(table, field, dt1, dt2, lat1, lat2, lon1, lon2, depth1, depth2, fname, exportDataFlag):
    if db.isClimatology(table) and db.hasField(table, 'month'):
        m1 = clim.timeToMonth(dt1)
        m2 = clim.timeToMonth(dt2)
        if m2>m1:
            timesteps = range(m1, m2+1)
        else:
            timesteps = range(m2, m1+1)
        timesteps = ['2016-%2.2d-01' % m for m in timesteps]    
    elif table.lower().find('tblPisces'.lower()) != -1:        # currently (Nov 2018) only Pisces table has a calendar table. all datasets have to have a calendar  table. we can then remove thw else: clause below 
        calTable = table+'_Calendar'
        timesteps = com.timesBetween(calTable, dt1, dt2)   
    else:        
        delta = datetime.strptime(dt2, '%Y-%m-%d') - datetime.strptime(dt1, '%Y-%m-%d')
        timesteps = [(datetime.strptime(dt1, '%Y-%m-%d') + timedelta(days=x)).strftime('%Y-%m-%d') for x in range(delta.days+1)]

    zs, ys, y_stds = [], [], []
    for dt in timesteps:
        df = subset.depthProfile(table, field, dt, dt, lat1, lat2, lon1, lon2, depth1, depth2)
        if len(df[field]) < 1:
            continue
        zs.append(df['depth'])
        ys.append(df[field])
        y_stds.append(df[field + '_std'])

    depth = np.mean( np.stack(zs, axis=0), axis=0 )
    y = np.mean( np.stack(ys, axis=0), axis=0 )
    y_std = np.mean( np.stack(y_stds, axis=0), axis=0 )

    if exportDataFlag:
        exportData(depth, y, y_std, table, field, dt1, dt2, lat1, lat2, lon1, lon2, fname)    
    return depth, y, y_std

```
</div>

</div>

