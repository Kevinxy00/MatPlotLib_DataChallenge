

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

csvPath1 = 'raw_data\clinicaltrial_data.csv'
csvPath2 = 'raw_data\mouse_drug_data.csv'

clin_df = pd.read_csv(csvPath1)
mouse_df = pd.read_csv(csvPath2)

clin_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Mouse ID</th>
      <th>Timepoint</th>
      <th>Tumor Volume (mm3)</th>
      <th>Metastatic Sites</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>b128</td>
      <td>0</td>
      <td>45.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>f932</td>
      <td>0</td>
      <td>45.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>g107</td>
      <td>0</td>
      <td>45.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>a457</td>
      <td>0</td>
      <td>45.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>c819</td>
      <td>0</td>
      <td>45.0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
#merge the two dataframes by mouse id
results_df = clin_df.merge(mouse_df, on='Mouse ID')
results_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Mouse ID</th>
      <th>Timepoint</th>
      <th>Tumor Volume (mm3)</th>
      <th>Metastatic Sites</th>
      <th>Drug</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>b128</td>
      <td>0</td>
      <td>45.000000</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b128</td>
      <td>5</td>
      <td>45.651331</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>2</th>
      <td>b128</td>
      <td>10</td>
      <td>43.270852</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>b128</td>
      <td>15</td>
      <td>43.784893</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b128</td>
      <td>20</td>
      <td>42.731552</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Tumor Response to Treatment

drugGroup = results_df.groupby(['Drug', 'Timepoint']).mean()
drugGroup

```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Tumor Volume (mm3)</th>
      <th>Metastatic Sites</th>
    </tr>
    <tr>
      <th>Drug</th>
      <th>Timepoint</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="10" valign="top">Capomulin</th>
      <th>0</th>
      <td>45.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>44.266086</td>
      <td>0.160000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>43.084291</td>
      <td>0.320000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>42.064317</td>
      <td>0.375000</td>
    </tr>
    <tr>
      <th>20</th>
      <td>40.716325</td>
      <td>0.652174</td>
    </tr>
    <tr>
      <th>25</th>
      <td>39.939528</td>
      <td>0.818182</td>
    </tr>
    <tr>
      <th>30</th>
      <td>38.769339</td>
      <td>1.090909</td>
    </tr>
    <tr>
      <th>35</th>
      <td>37.816839</td>
      <td>1.181818</td>
    </tr>
    <tr>
      <th>40</th>
      <td>36.958001</td>
      <td>1.380952</td>
    </tr>
    <tr>
      <th>45</th>
      <td>36.236114</td>
      <td>1.476190</td>
    </tr>
    <tr>
      <th rowspan="10" valign="top">Ceftamin</th>
      <th>0</th>
      <td>45.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>46.503051</td>
      <td>0.380952</td>
    </tr>
    <tr>
      <th>10</th>
      <td>48.285125</td>
      <td>0.600000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>50.094055</td>
      <td>0.789474</td>
    </tr>
    <tr>
      <th>20</th>
      <td>52.157049</td>
      <td>1.111111</td>
    </tr>
    <tr>
      <th>25</th>
      <td>54.287674</td>
      <td>1.500000</td>
    </tr>
    <tr>
      <th>30</th>
      <td>56.769517</td>
      <td>1.937500</td>
    </tr>
    <tr>
      <th>35</th>
      <td>58.827548</td>
      <td>2.071429</td>
    </tr>
    <tr>
      <th>40</th>
      <td>61.467895</td>
      <td>2.357143</td>
    </tr>
    <tr>
      <th>45</th>
      <td>64.132421</td>
      <td>2.692308</td>
    </tr>
    <tr>
      <th rowspan="10" valign="top">Infubinol</th>
      <th>0</th>
      <td>45.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>47.062001</td>
      <td>0.280000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>49.403909</td>
      <td>0.666667</td>
    </tr>
    <tr>
      <th>15</th>
      <td>51.296397</td>
      <td>0.904762</td>
    </tr>
    <tr>
      <th>20</th>
      <td>53.197691</td>
      <td>1.050000</td>
    </tr>
    <tr>
      <th>25</th>
      <td>55.715252</td>
      <td>1.277778</td>
    </tr>
    <tr>
      <th>30</th>
      <td>58.299397</td>
      <td>1.588235</td>
    </tr>
    <tr>
      <th>35</th>
      <td>60.742461</td>
      <td>1.666667</td>
    </tr>
    <tr>
      <th>40</th>
      <td>63.162824</td>
      <td>2.100000</td>
    </tr>
    <tr>
      <th>45</th>
      <td>65.755562</td>
      <td>2.111111</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="10" valign="top">Ramicane</th>
      <th>0</th>
      <td>45.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>43.944859</td>
      <td>0.120000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>42.531957</td>
      <td>0.250000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>41.495061</td>
      <td>0.333333</td>
    </tr>
    <tr>
      <th>20</th>
      <td>40.238325</td>
      <td>0.347826</td>
    </tr>
    <tr>
      <th>25</th>
      <td>38.974300</td>
      <td>0.652174</td>
    </tr>
    <tr>
      <th>30</th>
      <td>38.703137</td>
      <td>0.782609</td>
    </tr>
    <tr>
      <th>35</th>
      <td>37.451996</td>
      <td>0.952381</td>
    </tr>
    <tr>
      <th>40</th>
      <td>36.574081</td>
      <td>1.100000</td>
    </tr>
    <tr>
      <th>45</th>
      <td>34.955595</td>
      <td>1.250000</td>
    </tr>
    <tr>
      <th rowspan="10" valign="top">Stelasyn</th>
      <th>0</th>
      <td>45.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>47.527452</td>
      <td>0.240000</td>
    </tr>
    <tr>
      <th>10</th>
      <td>49.463844</td>
      <td>0.478261</td>
    </tr>
    <tr>
      <th>15</th>
      <td>51.529409</td>
      <td>0.782609</td>
    </tr>
    <tr>
      <th>20</th>
      <td>54.067395</td>
      <td>0.952381</td>
    </tr>
    <tr>
      <th>25</th>
      <td>56.166123</td>
      <td>1.157895</td>
    </tr>
    <tr>
      <th>30</th>
      <td>59.826738</td>
      <td>1.388889</td>
    </tr>
    <tr>
      <th>35</th>
      <td>62.440699</td>
      <td>1.562500</td>
    </tr>
    <tr>
      <th>40</th>
      <td>65.356386</td>
      <td>1.583333</td>
    </tr>
    <tr>
      <th>45</th>
      <td>68.438310</td>
      <td>1.727273</td>
    </tr>
    <tr>
      <th rowspan="10" valign="top">Zoniferol</th>
      <th>0</th>
      <td>45.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>46.851818</td>
      <td>0.166667</td>
    </tr>
    <tr>
      <th>10</th>
      <td>48.689881</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>50.779059</td>
      <td>0.809524</td>
    </tr>
    <tr>
      <th>20</th>
      <td>53.170334</td>
      <td>1.294118</td>
    </tr>
    <tr>
      <th>25</th>
      <td>55.432935</td>
      <td>1.687500</td>
    </tr>
    <tr>
      <th>30</th>
      <td>57.713531</td>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>35</th>
      <td>60.089372</td>
      <td>2.285714</td>
    </tr>
    <tr>
      <th>40</th>
      <td>62.916692</td>
      <td>2.785714</td>
    </tr>
    <tr>
      <th>45</th>
      <td>65.960888</td>
      <td>3.071429</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 2 columns</p>
</div>




```python
#pivot table of time vs. drug for tumor volume

drugTable = pd.pivot_table(drugGroup, values = 'Tumor Volume (mm3)', index = 'Timepoint', columns = 'Drug')

drugTable
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Drug</th>
      <th>Capomulin</th>
      <th>Ceftamin</th>
      <th>Infubinol</th>
      <th>Ketapril</th>
      <th>Naftisol</th>
      <th>Placebo</th>
      <th>Propriva</th>
      <th>Ramicane</th>
      <th>Stelasyn</th>
      <th>Zoniferol</th>
    </tr>
    <tr>
      <th>Timepoint</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>44.266086</td>
      <td>46.503051</td>
      <td>47.062001</td>
      <td>47.389175</td>
      <td>46.796098</td>
      <td>47.125589</td>
      <td>47.248967</td>
      <td>43.944859</td>
      <td>47.527452</td>
      <td>46.851818</td>
    </tr>
    <tr>
      <th>10</th>
      <td>43.084291</td>
      <td>48.285125</td>
      <td>49.403909</td>
      <td>49.582269</td>
      <td>48.694210</td>
      <td>49.423329</td>
      <td>49.101541</td>
      <td>42.531957</td>
      <td>49.463844</td>
      <td>48.689881</td>
    </tr>
    <tr>
      <th>15</th>
      <td>42.064317</td>
      <td>50.094055</td>
      <td>51.296397</td>
      <td>52.399974</td>
      <td>50.933018</td>
      <td>51.359742</td>
      <td>51.067318</td>
      <td>41.495061</td>
      <td>51.529409</td>
      <td>50.779059</td>
    </tr>
    <tr>
      <th>20</th>
      <td>40.716325</td>
      <td>52.157049</td>
      <td>53.197691</td>
      <td>54.920935</td>
      <td>53.644087</td>
      <td>54.364417</td>
      <td>53.346737</td>
      <td>40.238325</td>
      <td>54.067395</td>
      <td>53.170334</td>
    </tr>
    <tr>
      <th>25</th>
      <td>39.939528</td>
      <td>54.287674</td>
      <td>55.715252</td>
      <td>57.678982</td>
      <td>56.731968</td>
      <td>57.482574</td>
      <td>55.504138</td>
      <td>38.974300</td>
      <td>56.166123</td>
      <td>55.432935</td>
    </tr>
    <tr>
      <th>30</th>
      <td>38.769339</td>
      <td>56.769517</td>
      <td>58.299397</td>
      <td>60.994507</td>
      <td>59.559509</td>
      <td>59.809063</td>
      <td>58.196374</td>
      <td>38.703137</td>
      <td>59.826738</td>
      <td>57.713531</td>
    </tr>
    <tr>
      <th>35</th>
      <td>37.816839</td>
      <td>58.827548</td>
      <td>60.742461</td>
      <td>63.371686</td>
      <td>62.685087</td>
      <td>62.420615</td>
      <td>60.350199</td>
      <td>37.451996</td>
      <td>62.440699</td>
      <td>60.089372</td>
    </tr>
    <tr>
      <th>40</th>
      <td>36.958001</td>
      <td>61.467895</td>
      <td>63.162824</td>
      <td>66.068580</td>
      <td>65.600754</td>
      <td>65.052675</td>
      <td>63.045537</td>
      <td>36.574081</td>
      <td>65.356386</td>
      <td>62.916692</td>
    </tr>
    <tr>
      <th>45</th>
      <td>36.236114</td>
      <td>64.132421</td>
      <td>65.755562</td>
      <td>70.662958</td>
      <td>69.265506</td>
      <td>68.084082</td>
      <td>66.258529</td>
      <td>34.955595</td>
      <td>68.438310</td>
      <td>65.960888</td>
    </tr>
  </tbody>
</table>
</div>




```python
#plot of pivot table

#***Scatter plot using line plot with markers just like in example
### makePlot == graphs a pivot table with (index==Timepoint) & (column==a specific drug) 
def makePlot(table):
    #Get a different marker/dot for each drug
    mark_list = ["x", "s", "o", "v", "^", "<", ">", "D", "*", "P"]
    markNum = 0
    #get standard error of the mean
    tableSEM = table.sem()
    #loop through each column to get different marker for each drug (n==10)
    for column in table.columns:
        #plot line by connecting errorbars 
        plt.errorbar(x=table.index, y=table[column], yerr= tableSEM, data=table, marker = mark_list[markNum],\
                     label=column, capsize=4, ls= '--', lw=1)
        markNum += 1

#make graph
    #change figure size
fig, ax = plt.subplots()
    # the size of A4 paper
fig.set_size_inches(11.7, 8.27) 
#make plot from pivot table
makePlot(drugTable)
sns.set_style('dark')  
ax.grid(linestyle='--', linewidth=1)
ax.set_xlim(0, 45)
plt.xlabel('Time (Days)')
plt.ylabel('Tumor Volume (mm3)')
plt.title('Tumor Response to Treatment')
plt.legend()
plt.show()

```


![png](output_4_0.png)



```python
#pivot table of time vs. drug for Metastatic Sites

drugTableM = pd.pivot_table(drugGroup, values = 'Metastatic Sites', index = 'Timepoint', columns = 'Drug')
drugTableM
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Drug</th>
      <th>Capomulin</th>
      <th>Ceftamin</th>
      <th>Infubinol</th>
      <th>Ketapril</th>
      <th>Naftisol</th>
      <th>Placebo</th>
      <th>Propriva</th>
      <th>Ramicane</th>
      <th>Stelasyn</th>
      <th>Zoniferol</th>
    </tr>
    <tr>
      <th>Timepoint</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.160000</td>
      <td>0.380952</td>
      <td>0.280000</td>
      <td>0.304348</td>
      <td>0.260870</td>
      <td>0.375000</td>
      <td>0.320000</td>
      <td>0.120000</td>
      <td>0.240000</td>
      <td>0.166667</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.320000</td>
      <td>0.600000</td>
      <td>0.666667</td>
      <td>0.590909</td>
      <td>0.523810</td>
      <td>0.833333</td>
      <td>0.565217</td>
      <td>0.250000</td>
      <td>0.478261</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.375000</td>
      <td>0.789474</td>
      <td>0.904762</td>
      <td>0.842105</td>
      <td>0.857143</td>
      <td>1.250000</td>
      <td>0.764706</td>
      <td>0.333333</td>
      <td>0.782609</td>
      <td>0.809524</td>
    </tr>
    <tr>
      <th>20</th>
      <td>0.652174</td>
      <td>1.111111</td>
      <td>1.050000</td>
      <td>1.210526</td>
      <td>1.150000</td>
      <td>1.526316</td>
      <td>1.000000</td>
      <td>0.347826</td>
      <td>0.952381</td>
      <td>1.294118</td>
    </tr>
    <tr>
      <th>25</th>
      <td>0.818182</td>
      <td>1.500000</td>
      <td>1.277778</td>
      <td>1.631579</td>
      <td>1.500000</td>
      <td>1.941176</td>
      <td>1.357143</td>
      <td>0.652174</td>
      <td>1.157895</td>
      <td>1.687500</td>
    </tr>
    <tr>
      <th>30</th>
      <td>1.090909</td>
      <td>1.937500</td>
      <td>1.588235</td>
      <td>2.055556</td>
      <td>2.066667</td>
      <td>2.266667</td>
      <td>1.615385</td>
      <td>0.782609</td>
      <td>1.388889</td>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>35</th>
      <td>1.181818</td>
      <td>2.071429</td>
      <td>1.666667</td>
      <td>2.294118</td>
      <td>2.266667</td>
      <td>2.642857</td>
      <td>2.300000</td>
      <td>0.952381</td>
      <td>1.562500</td>
      <td>2.285714</td>
    </tr>
    <tr>
      <th>40</th>
      <td>1.380952</td>
      <td>2.357143</td>
      <td>2.100000</td>
      <td>2.733333</td>
      <td>2.466667</td>
      <td>3.166667</td>
      <td>2.777778</td>
      <td>1.100000</td>
      <td>1.583333</td>
      <td>2.785714</td>
    </tr>
    <tr>
      <th>45</th>
      <td>1.476190</td>
      <td>2.692308</td>
      <td>2.111111</td>
      <td>3.363636</td>
      <td>2.538462</td>
      <td>3.272727</td>
      <td>2.571429</td>
      <td>1.250000</td>
      <td>1.727273</td>
      <td>3.071429</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Make scatterplot using makePlot() defined 2 cells above
#change figure size
fig, ax = plt.subplots()
    # the size of A4 paper
fig.set_size_inches(11.7, 8.27) 
#make plot from pivot table
makePlot(drugTableM)
ax.grid(linestyle='--', linewidth=1)
ax.set_xlim(0, 45)
plt.title('Metastatic Spread During Treatment')
plt.xlabel('Treatment Duration (Days)')
plt.ylabel('Metastatic Sites')
plt.legend()
plt.show()
```


![png](output_6_0.png)



```python
#Survival rate over time of mice for each drug
#The count of mice for each time period
mouseNum = results_df.groupby(['Drug', 'Timepoint']).count()
#The count of mice at the beginning 
mouseNStart = results_df[results_df['Timepoint']==0].groupby(['Drug']).count()
mouseNStart_s = pd.Series(mouseNStart['Mouse ID'])
#Get % of surviving mice by dividing mice count from starting mice count
mouseSurv = mouseNum['Mouse ID'].div(mouseNStart_s, level='Drug') * 100
mouseSurv = pd.DataFrame(data=mouseSurv)
mouseSurvTable = pd.pivot_table(mouseSurv, values = 'Mouse ID', index = 'Timepoint', columns = 'Drug')

#make Graph
#change figure size
fig, ax = plt.subplots()
    # the size of A4 paper
fig.set_size_inches(11.7, 8.27)
#make plot from pivot table
makePlot(mouseSurvTable)
ax.grid(linestyle='--', linewidth=1)
ax.set_xlim(0, 45)
ax.set_ylim(0, 100)
plt.title('Survival During Treatment')
plt.xlabel('Time (Days)')
plt.ylabel('Survival Rate (%)')
plt.legend()
plt.show()

```


![png](output_7_0.png)



```python
# Creating a bar graph that compares the total % tumor volume change for each drug across the full 45 days.
#drugTable from pivot table of tumor volume section
#Gets row & column where timepoint == 0 and timepoint == 45 
TumorStart = drugTable.xs(0)
TumorEnd = drugTable.xs(45)
#percent change = (new - old)/old times 100
def percChng(end, start):
    Change = ((end - start)/start) * 100
    return round(Change, 2)
TumorChng = percChng(TumorEnd, TumorStart)
TumorChng_df = pd.DataFrame(TumorChng)
TumorChng_df = TumorChng_df.rename(columns={0:'Tumor Change (%)'})

#color list where positive change == red & neg chng == green
color_ls = []
for i in TumorChng:
    if i >= 0:
        color_ls.append('r')
    else:
        color_ls.append('g')

#change figure size
fig, ax = plt.subplots()
    # the size of A4 paper
fig.set_size_inches(11.7, 8.27)   

#bargraph of the results
sns.barplot(x= TumorChng_df.index ,y='Tumor Change (%)', data=TumorChng_df, palette=color_ls, orient='v')

#add annotations for each graph
for p in ax.patches:
    if p.get_height() > 0:
        ax.annotate(str(p.get_height()) + '%', (p.get_x() + .17, 2), color='black')
    else:
        ax.annotate(str(p.get_height()) + '%', (p.get_x() + .17, -2.75), color='white')
        
ax.grid(linestyle='--', linewidth=1)
ax.axhline(color='gray')
plt.title('Tumor Change Over 45 Day Treatment')
plt.ylabel('% Tumor Volume Change')
plt.show()
```


![png](output_8_0.png)

