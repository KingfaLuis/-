
# 清除列标签
使用 `all_alpha_08.csv` 和 `all_alpha_18.csv`


```python
# 加载数据集
import pandas as pd
df_08 = pd.read_csv('all_alpha_08.csv')
df_18 = pd.read_csv('all_alpha_18.csv')
```


```python
# 查看 2008 数据集
df_08.head(1)
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
      <th>Model</th>
      <th>Displ</th>
      <th>Cyl</th>
      <th>Trans</th>
      <th>Drive</th>
      <th>Fuel</th>
      <th>Sales Area</th>
      <th>Stnd</th>
      <th>Underhood ID</th>
      <th>Veh Class</th>
      <th>Air Pollution Score</th>
      <th>FE Calc Appr</th>
      <th>City MPG</th>
      <th>Hwy MPG</th>
      <th>Cmb MPG</th>
      <th>Unadj Cmb MPG</th>
      <th>Greenhouse Gas Score</th>
      <th>SmartWay</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ACURA MDX</td>
      <td>3.7</td>
      <td>(6 cyl)</td>
      <td>Auto-S5</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>CA</td>
      <td>U2</td>
      <td>8HNXT03.7PKR</td>
      <td>SUV</td>
      <td>7</td>
      <td>Drv</td>
      <td>15</td>
      <td>20</td>
      <td>17</td>
      <td>22.0527</td>
      <td>4</td>
      <td>no</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 查看 2018 数据集
df_18.head(1)
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
      <th>Model</th>
      <th>Displ</th>
      <th>Cyl</th>
      <th>Trans</th>
      <th>Drive</th>
      <th>Fuel</th>
      <th>Cert Region</th>
      <th>Stnd</th>
      <th>Stnd Description</th>
      <th>Underhood ID</th>
      <th>Veh Class</th>
      <th>Air Pollution Score</th>
      <th>City MPG</th>
      <th>Hwy MPG</th>
      <th>Cmb MPG</th>
      <th>Greenhouse Gas Score</th>
      <th>SmartWay</th>
      <th>Comb CO2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ACURA RDX</td>
      <td>3.5</td>
      <td>6.0</td>
      <td>SemiAuto-6</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>FA</td>
      <td>T3B125</td>
      <td>Federal Tier 3 Bin 125</td>
      <td>JHNXT03.5GV3</td>
      <td>small SUV</td>
      <td>3</td>
      <td>20</td>
      <td>28</td>
      <td>23</td>
      <td>5</td>
      <td>No</td>
      <td>386</td>
    </tr>
  </tbody>
</table>
</div>



### 丢弃多余列
删除不一致（不同时存在于两个数据集中）的特征或与我们的问题无关的列。使用 Pandas 的 drop 函数。

要删除的列：
2008 数据集中: 'Stnd'、'Underhood ID'、'FE Calc Appr'、'Unadj Cmb MPG'
2018 数据集中: 'Stnd'、'Stnd Description'、'Underhood ID'、'Comb CO2'


```python
# 从 2008 数据集中丢弃列
df_08.drop(['Stnd', 'Underhood ID', 'FE Calc Appr', 'Unadj Cmb MPG'], axis=1, inplace=True)

# 确认更改
df_08.head(1)
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
      <th>Model</th>
      <th>Displ</th>
      <th>Cyl</th>
      <th>Trans</th>
      <th>Drive</th>
      <th>Fuel</th>
      <th>Sales Area</th>
      <th>Veh Class</th>
      <th>Air Pollution Score</th>
      <th>City MPG</th>
      <th>Hwy MPG</th>
      <th>Cmb MPG</th>
      <th>Greenhouse Gas Score</th>
      <th>SmartWay</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ACURA MDX</td>
      <td>3.7</td>
      <td>(6 cyl)</td>
      <td>Auto-S5</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>CA</td>
      <td>SUV</td>
      <td>7</td>
      <td>15</td>
      <td>20</td>
      <td>17</td>
      <td>4</td>
      <td>no</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 从 2018 数据集中丢弃列
df_18.drop(['Stnd','Stnd Description','Underhood ID','Comb CO2'],axis=1,inplace=True)

# 确认更改
df_18.head()
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
      <th>Model</th>
      <th>Displ</th>
      <th>Cyl</th>
      <th>Trans</th>
      <th>Drive</th>
      <th>Fuel</th>
      <th>Cert Region</th>
      <th>Veh Class</th>
      <th>Air Pollution Score</th>
      <th>City MPG</th>
      <th>Hwy MPG</th>
      <th>Cmb MPG</th>
      <th>Greenhouse Gas Score</th>
      <th>SmartWay</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ACURA RDX</td>
      <td>3.5</td>
      <td>6.0</td>
      <td>SemiAuto-6</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>FA</td>
      <td>small SUV</td>
      <td>3</td>
      <td>20</td>
      <td>28</td>
      <td>23</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ACURA RDX</td>
      <td>3.5</td>
      <td>6.0</td>
      <td>SemiAuto-6</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>CA</td>
      <td>small SUV</td>
      <td>3</td>
      <td>20</td>
      <td>28</td>
      <td>23</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ACURA RDX</td>
      <td>3.5</td>
      <td>6.0</td>
      <td>SemiAuto-6</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>FA</td>
      <td>small SUV</td>
      <td>3</td>
      <td>19</td>
      <td>27</td>
      <td>22</td>
      <td>4</td>
      <td>No</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ACURA RDX</td>
      <td>3.5</td>
      <td>6.0</td>
      <td>SemiAuto-6</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>CA</td>
      <td>small SUV</td>
      <td>3</td>
      <td>19</td>
      <td>27</td>
      <td>22</td>
      <td>4</td>
      <td>No</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ACURA TLX</td>
      <td>2.4</td>
      <td>4.0</td>
      <td>AMS-8</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>CA</td>
      <td>small car</td>
      <td>3</td>
      <td>23</td>
      <td>33</td>
      <td>27</td>
      <td>6</td>
      <td>No</td>
    </tr>
  </tbody>
</table>
</div>



### 重命名列
1. 删除无关列
将 2008 数据集中的"Sales Area""列标签改为"Cert Region"以确保一致性。
重命名所有列标签以空格替换为下划线，并将所有内容转换为小写。（在 Python 中，下划线比空格更好用。例如，空格不允许你使用 df.column_name 代替 df['column_name'] 来选择列，或使用 query()。保持小写和下划线一致也使列名更好记。）


```python
# 将销售区域重命名为特定区域
df_08.rename(columns={'Sales Area':'Cert Region'},inplace=True)

# 确认更改
df_08.head(1)
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
      <th>Model</th>
      <th>Displ</th>
      <th>Cyl</th>
      <th>Trans</th>
      <th>Drive</th>
      <th>Fuel</th>
      <th>Cert Region</th>
      <th>Veh Class</th>
      <th>Air Pollution Score</th>
      <th>City MPG</th>
      <th>Hwy MPG</th>
      <th>Cmb MPG</th>
      <th>Greenhouse Gas Score</th>
      <th>SmartWay</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ACURA MDX</td>
      <td>3.7</td>
      <td>(6 cyl)</td>
      <td>Auto-S5</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>CA</td>
      <td>SUV</td>
      <td>7</td>
      <td>15</td>
      <td>20</td>
      <td>17</td>
      <td>4</td>
      <td>no</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 在 2008 数据集中用下划线和小写标签代替空格
df_08.rename(columns=lambda x: x.strip().lower().replace(" ", "_"), inplace=True)

# 确认更改
df_08.head(1)
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
      <th>model</th>
      <th>displ</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drive</th>
      <th>fuel</th>
      <th>cert_region</th>
      <th>veh_class</th>
      <th>air_pollution_score</th>
      <th>city_mpg</th>
      <th>hwy_mpg</th>
      <th>cmb_mpg</th>
      <th>greenhouse_gas_score</th>
      <th>smartway</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ACURA MDX</td>
      <td>3.7</td>
      <td>(6 cyl)</td>
      <td>Auto-S5</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>CA</td>
      <td>SUV</td>
      <td>7</td>
      <td>15</td>
      <td>20</td>
      <td>17</td>
      <td>4</td>
      <td>no</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 在 2018 数据集中用下划线和小写标签代替空格
df_18.rename(columns=lambda x: x.strip().lower().replace(" ", "_"),inplace=True)

# 确认更改
df_18.head(1)
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
      <th>model</th>
      <th>displ</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drive</th>
      <th>fuel</th>
      <th>cert_region</th>
      <th>veh_class</th>
      <th>air_pollution_score</th>
      <th>city_mpg</th>
      <th>hwy_mpg</th>
      <th>cmb_mpg</th>
      <th>greenhouse_gas_score</th>
      <th>smartway</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ACURA RDX</td>
      <td>3.5</td>
      <td>6.0</td>
      <td>SemiAuto-6</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>FA</td>
      <td>small SUV</td>
      <td>3</td>
      <td>20</td>
      <td>28</td>
      <td>23</td>
      <td>5</td>
      <td>No</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 确认 2008 和 2018 数据集的列标签相同
df_08.columns == df_18.columns
```




    array([ True,  True,  True,  True,  True,  True,  True,  True,  True,
            True,  True,  True,  True,  True], dtype=bool)




```python
# 确定所有的列标签都相同，如下所示
(df_08.columns == df_18.columns).all()
```




    True




```python
# 保存新数据集，供下一段使用
df_08.to_csv('data_08.csv', index=True)
df_18.to_csv('data_18.csv', index=False)
```


```python
df_08.head()
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
      <th>model</th>
      <th>displ</th>
      <th>cyl</th>
      <th>trans</th>
      <th>drive</th>
      <th>fuel</th>
      <th>cert_region</th>
      <th>veh_class</th>
      <th>air_pollution_score</th>
      <th>city_mpg</th>
      <th>hwy_mpg</th>
      <th>cmb_mpg</th>
      <th>greenhouse_gas_score</th>
      <th>smartway</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>ACURA MDX</td>
      <td>3.7</td>
      <td>(6 cyl)</td>
      <td>Auto-S5</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>CA</td>
      <td>SUV</td>
      <td>7</td>
      <td>15</td>
      <td>20</td>
      <td>17</td>
      <td>4</td>
      <td>no</td>
    </tr>
    <tr>
      <th>1</th>
      <td>ACURA MDX</td>
      <td>3.7</td>
      <td>(6 cyl)</td>
      <td>Auto-S5</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>FA</td>
      <td>SUV</td>
      <td>6</td>
      <td>15</td>
      <td>20</td>
      <td>17</td>
      <td>4</td>
      <td>no</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ACURA RDX</td>
      <td>2.3</td>
      <td>(4 cyl)</td>
      <td>Auto-S5</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>CA</td>
      <td>SUV</td>
      <td>7</td>
      <td>17</td>
      <td>22</td>
      <td>19</td>
      <td>5</td>
      <td>no</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ACURA RDX</td>
      <td>2.3</td>
      <td>(4 cyl)</td>
      <td>Auto-S5</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>FA</td>
      <td>SUV</td>
      <td>6</td>
      <td>17</td>
      <td>22</td>
      <td>19</td>
      <td>5</td>
      <td>no</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ACURA RL</td>
      <td>3.5</td>
      <td>(6 cyl)</td>
      <td>Auto-S5</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>CA</td>
      <td>midsize car</td>
      <td>7</td>
      <td>16</td>
      <td>24</td>
      <td>19</td>
      <td>5</td>
      <td>no</td>
    </tr>
  </tbody>
</table>
</div>


