
# 过滤、丢弃空值、重复数据删除
使用 `data_08.csv` 和 `data_18.csv`
为保持一致性，仅比较加州认证的汽车。使用 query 过滤两个数据集，仅选择 cert_region 为 CA 的行。然后，删除 `cert_region' 列，因为它不再提供任何有用的信息（我们知道每个值都是 'CA'）。


```python
# 加载数据集
import pandas as pd
df_08 = pd.read_csv('data_08.csv')
df_18 = pd.read_csv('data_18.csv')
```


```python
# 查看数据集维度
df_08.shape
```




    (2404, 15)




```python
# 查看数据集维度
df_18.shape
```




    (1611, 14)



## 按认证区域过滤


```python
df_08.sample(5)
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
      <th>Unnamed: 0</th>
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
      <th>381</th>
      <td>381</td>
      <td>CHEVROLET Express 1500</td>
      <td>5.3</td>
      <td>(8 cyl)</td>
      <td>Auto-L4</td>
      <td>2WD</td>
      <td>ethanol/gas</td>
      <td>FC</td>
      <td>van</td>
      <td>6/6</td>
      <td>9/12</td>
      <td>12/16</td>
      <td>10/14</td>
      <td>4/2</td>
      <td>no</td>
    </tr>
    <tr>
      <th>1976</th>
      <td>1976</td>
      <td>SAAB 9-3 Sport Sedan</td>
      <td>2.8</td>
      <td>(6 cyl)</td>
      <td>Auto-S6</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>FA</td>
      <td>small car</td>
      <td>6</td>
      <td>15</td>
      <td>24</td>
      <td>18</td>
      <td>5</td>
      <td>no</td>
    </tr>
    <tr>
      <th>604</th>
      <td>604</td>
      <td>CHRYSLER Sebring</td>
      <td>2.4</td>
      <td>(4 cyl)</td>
      <td>Auto-L4</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>CA</td>
      <td>midsize car</td>
      <td>7</td>
      <td>21</td>
      <td>30</td>
      <td>24</td>
      <td>7</td>
      <td>yes</td>
    </tr>
    <tr>
      <th>2152</th>
      <td>2152</td>
      <td>TOYOTA 4Runner</td>
      <td>4.7</td>
      <td>(8 cyl)</td>
      <td>Auto-L5</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>FA</td>
      <td>SUV</td>
      <td>6</td>
      <td>15</td>
      <td>19</td>
      <td>17</td>
      <td>4</td>
      <td>no</td>
    </tr>
    <tr>
      <th>593</th>
      <td>593</td>
      <td>CHRYSLER Pacifica</td>
      <td>4.0</td>
      <td>(6 cyl)</td>
      <td>Auto-L6</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>FA</td>
      <td>SUV</td>
      <td>6</td>
      <td>15</td>
      <td>23</td>
      <td>17</td>
      <td>4</td>
      <td>no</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 过滤满足加州标准的行的数据集
df_08 = df_08.query('cert_region =="CA"')
df_18 = df_18.query('cert_region =="CA"')
```


```python
# 确定唯一的认证区域是加州
df_08['cert_region'].unique()
```




    array(['CA'], dtype=object)




```python
# 确定唯一的认证区域是加州
df_18['cert_region'].unique()
```




    array(['CA'], dtype=object)




```python
# 将认证区域列从两个数据集中丢弃
df_08.drop('cert_region',axis=1)
df_18.drop('cert_region',axis=1)
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
      <th>1</th>
      <td>ACURA RDX</td>
      <td>3.5</td>
      <td>6.0</td>
      <td>SemiAuto-6</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>small SUV</td>
      <td>3</td>
      <td>20</td>
      <td>28</td>
      <td>23</td>
      <td>5</td>
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
      <td>small car</td>
      <td>3</td>
      <td>23</td>
      <td>33</td>
      <td>27</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>6</th>
      <td>ACURA TLX</td>
      <td>3.5</td>
      <td>6.0</td>
      <td>SemiAuto-9</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>3</td>
      <td>20</td>
      <td>32</td>
      <td>24</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>8</th>
      <td>ACURA TLX</td>
      <td>3.5</td>
      <td>6.0</td>
      <td>SemiAuto-9</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>3</td>
      <td>21</td>
      <td>30</td>
      <td>24</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>10</th>
      <td>ACURA TLX AWD A-SPEC</td>
      <td>3.5</td>
      <td>6.0</td>
      <td>SemiAuto-9</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>3</td>
      <td>20</td>
      <td>29</td>
      <td>23</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>12</th>
      <td>ACURA TLX FWD A-SPEC</td>
      <td>3.5</td>
      <td>6.0</td>
      <td>SemiAuto-9</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>3</td>
      <td>20</td>
      <td>30</td>
      <td>23</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>14</th>
      <td>ALFA ROMEO 4C</td>
      <td>1.8</td>
      <td>4.0</td>
      <td>AutoMan-6</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>1</td>
      <td>24</td>
      <td>34</td>
      <td>28</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>17</th>
      <td>ALFA ROMEO Giulia</td>
      <td>2.9</td>
      <td>6.0</td>
      <td>Auto-8</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>midsize car</td>
      <td>3</td>
      <td>17</td>
      <td>24</td>
      <td>20</td>
      <td>4</td>
      <td>No</td>
    </tr>
    <tr>
      <th>18</th>
      <td>ALFA ROMEO Giulia</td>
      <td>2.9</td>
      <td>6.0</td>
      <td>Auto-8</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>midsize car</td>
      <td>3</td>
      <td>17</td>
      <td>24</td>
      <td>20</td>
      <td>4</td>
      <td>No</td>
    </tr>
    <tr>
      <th>22</th>
      <td>AUDI A3</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>AMS-6</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>7</td>
      <td>24</td>
      <td>31</td>
      <td>27</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>24</th>
      <td>AUDI A3</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>AMS-7</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>7</td>
      <td>26</td>
      <td>35</td>
      <td>29</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>26</th>
      <td>AUDI A3 Cabriolet</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>AMS-6</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>7</td>
      <td>22</td>
      <td>30</td>
      <td>25</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>28</th>
      <td>AUDI A3 Cabriolet</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>AMS-7</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>7</td>
      <td>25</td>
      <td>33</td>
      <td>28</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>30</th>
      <td>AUDI A4</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>AMS-7</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>5</td>
      <td>24</td>
      <td>34</td>
      <td>27</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>32</th>
      <td>AUDI A4</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>Man-6</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>3</td>
      <td>24</td>
      <td>33</td>
      <td>27</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>34</th>
      <td>AUDI A4 Ultra</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>AMS-7</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>3</td>
      <td>27</td>
      <td>37</td>
      <td>31</td>
      <td>7</td>
      <td>Yes</td>
    </tr>
    <tr>
      <th>36</th>
      <td>AUDI A5</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>AMS-7</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>5</td>
      <td>24</td>
      <td>34</td>
      <td>27</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>38</th>
      <td>AUDI A5</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>Man-6</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>3</td>
      <td>24</td>
      <td>33</td>
      <td>27</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>40</th>
      <td>AUDI A5 Cabriolet</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>AMS-7</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>5</td>
      <td>24</td>
      <td>34</td>
      <td>27</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>42</th>
      <td>AUDI A5 Sportback quattro</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>AMS-7</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>midsize car</td>
      <td>5</td>
      <td>24</td>
      <td>34</td>
      <td>27</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>44</th>
      <td>AUDI A6</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>AMS-7</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>midsize car</td>
      <td>5</td>
      <td>25</td>
      <td>34</td>
      <td>28</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>46</th>
      <td>AUDI A6</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>midsize car</td>
      <td>5</td>
      <td>22</td>
      <td>31</td>
      <td>26</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>49</th>
      <td>AUDI A6</td>
      <td>3.0</td>
      <td>6.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>midsize car</td>
      <td>3</td>
      <td>20</td>
      <td>29</td>
      <td>23</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>51</th>
      <td>AUDI A7</td>
      <td>3.0</td>
      <td>6.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>midsize car</td>
      <td>3</td>
      <td>20</td>
      <td>29</td>
      <td>23</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>53</th>
      <td>AUDI A8 L</td>
      <td>3.0</td>
      <td>6.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>large car</td>
      <td>3</td>
      <td>19</td>
      <td>29</td>
      <td>22</td>
      <td>4</td>
      <td>No</td>
    </tr>
    <tr>
      <th>55</th>
      <td>AUDI Q3</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-6</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>3</td>
      <td>20</td>
      <td>28</td>
      <td>23</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>57</th>
      <td>AUDI Q3</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-6</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>3</td>
      <td>20</td>
      <td>28</td>
      <td>23</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>58</th>
      <td>AUDI Q5</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-7</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small SUV</td>
      <td>3</td>
      <td>23</td>
      <td>27</td>
      <td>25</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>60</th>
      <td>AUDI Q7</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>standard SUV</td>
      <td>3</td>
      <td>19</td>
      <td>25</td>
      <td>21</td>
      <td>4</td>
      <td>No</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1551</th>
      <td>VOLVO Atlas 4Motion</td>
      <td>3.6</td>
      <td>6.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small SUV</td>
      <td>5</td>
      <td>17</td>
      <td>23</td>
      <td>19</td>
      <td>3</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1553</th>
      <td>VOLVO S60</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>7</td>
      <td>25</td>
      <td>36</td>
      <td>29</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1555</th>
      <td>VOLVO S60</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>3</td>
      <td>22</td>
      <td>32</td>
      <td>26</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1556</th>
      <td>VOLVO S60</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>3</td>
      <td>22</td>
      <td>33</td>
      <td>26</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1559</th>
      <td>VOLVO S60 CC</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>3</td>
      <td>22</td>
      <td>30</td>
      <td>25</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1561</th>
      <td>VOLVO S60 Inscription</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>3</td>
      <td>25</td>
      <td>36</td>
      <td>29</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1563</th>
      <td>VOLVO S60 Inscription</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>3</td>
      <td>22</td>
      <td>33</td>
      <td>26</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1565</th>
      <td>VOLVO S60 Polestar</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small car</td>
      <td>1</td>
      <td>20</td>
      <td>27</td>
      <td>22</td>
      <td>4</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1567</th>
      <td>VOLVO S90</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>midsize car</td>
      <td>3</td>
      <td>24</td>
      <td>34</td>
      <td>27</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1569</th>
      <td>VOLVO S90</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>midsize car</td>
      <td>3</td>
      <td>22</td>
      <td>31</td>
      <td>25</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1570</th>
      <td>VOLVO S90</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>midsize car</td>
      <td>3</td>
      <td>23</td>
      <td>32</td>
      <td>26</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1573</th>
      <td>VOLVO S90</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>midsize car</td>
      <td>5</td>
      <td>23</td>
      <td>32</td>
      <td>26</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1575</th>
      <td>VOLVO S90</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>midsize car</td>
      <td>5</td>
      <td>22</td>
      <td>31</td>
      <td>25</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1577</th>
      <td>VOLVO S90</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline/Electricity</td>
      <td>midsize car</td>
      <td>7</td>
      <td>26/70</td>
      <td>33/72</td>
      <td>29/71</td>
      <td>10</td>
      <td>Elite</td>
    </tr>
    <tr>
      <th>1579</th>
      <td>VOLVO V60</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>station wagon</td>
      <td>3</td>
      <td>25</td>
      <td>36</td>
      <td>29</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1581</th>
      <td>VOLVO V60</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>station wagon</td>
      <td>3</td>
      <td>22</td>
      <td>32</td>
      <td>26</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1582</th>
      <td>VOLVO V60</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>station wagon</td>
      <td>3</td>
      <td>22</td>
      <td>33</td>
      <td>26</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1585</th>
      <td>VOLVO V60 CC</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>station wagon</td>
      <td>3</td>
      <td>22</td>
      <td>30</td>
      <td>25</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1587</th>
      <td>VOLVO V60 Polestar</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>station wagon</td>
      <td>1</td>
      <td>20</td>
      <td>27</td>
      <td>22</td>
      <td>4</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1589</th>
      <td>VOLVO V90</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>station wagon</td>
      <td>5</td>
      <td>24</td>
      <td>34</td>
      <td>27</td>
      <td>6</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1591</th>
      <td>VOLVO V90</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>station wagon</td>
      <td>5</td>
      <td>22</td>
      <td>31</td>
      <td>25</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1593</th>
      <td>VOLVO V90 CC</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>station wagon</td>
      <td>5</td>
      <td>23</td>
      <td>31</td>
      <td>26</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1595</th>
      <td>VOLVO V90 CC</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>station wagon</td>
      <td>5</td>
      <td>22</td>
      <td>29</td>
      <td>25</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1597</th>
      <td>VOLVO XC 60</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small SUV</td>
      <td>5</td>
      <td>22</td>
      <td>28</td>
      <td>24</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1599</th>
      <td>VOLVO XC 60</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>small SUV</td>
      <td>5</td>
      <td>21</td>
      <td>27</td>
      <td>23</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1601</th>
      <td>VOLVO XC 60</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline/Electricity</td>
      <td>small SUV</td>
      <td>7</td>
      <td>26/60</td>
      <td>28/58</td>
      <td>26/59</td>
      <td>10</td>
      <td>Elite</td>
    </tr>
    <tr>
      <th>1603</th>
      <td>VOLVO XC 90</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>2WD</td>
      <td>Gasoline</td>
      <td>standard SUV</td>
      <td>5</td>
      <td>22</td>
      <td>29</td>
      <td>25</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1605</th>
      <td>VOLVO XC 90</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>standard SUV</td>
      <td>5</td>
      <td>22</td>
      <td>28</td>
      <td>24</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1607</th>
      <td>VOLVO XC 90</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline</td>
      <td>standard SUV</td>
      <td>5</td>
      <td>20</td>
      <td>27</td>
      <td>23</td>
      <td>5</td>
      <td>No</td>
    </tr>
    <tr>
      <th>1609</th>
      <td>VOLVO XC 90</td>
      <td>2.0</td>
      <td>4.0</td>
      <td>SemiAuto-8</td>
      <td>4WD</td>
      <td>Gasoline/Electricity</td>
      <td>standard SUV</td>
      <td>7</td>
      <td>26/63</td>
      <td>30/61</td>
      <td>27/62</td>
      <td>10</td>
      <td>Elite</td>
    </tr>
  </tbody>
</table>
<p>798 rows × 13 columns</p>
</div>




```python
df_08.shape
```




    (1084, 15)




```python
df_18.shape
```




    (798, 14)



## 丢弃含有缺失值的行


```python
# 查看 2008 年每个特征的缺失值数量
df_08.isnull().sum()
```




    Unnamed: 0               0
    model                    0
    displ                    0
    cyl                     75
    trans                   75
    drive                   37
    fuel                     0
    cert_region              0
    veh_class                0
    air_pollution_score      0
    city_mpg                75
    hwy_mpg                 75
    cmb_mpg                 75
    greenhouse_gas_score    75
    smartway                 0
    dtype: int64




```python
# 查看 2018 年每个特征的缺失值数量
df_18.isnull().sum()

```




    model                   0
    displ                   1
    cyl                     1
    trans                   0
    drive                   0
    fuel                    0
    cert_region             0
    veh_class               0
    air_pollution_score     0
    city_mpg                0
    hwy_mpg                 0
    cmb_mpg                 0
    greenhouse_gas_score    0
    smartway                0
    dtype: int64




```python
# 丢弃两个数据集中有任何空值的行
df_08 = df_08.dropna()
df_18 = df_18.dropna()
```


```python
# 检查 2008 年的任何列是否有空值 - 应打印为“假”
df_08.isnull().sum().any()
```




    False




```python
# 检查 2018 年的任何列是否有空值 - 应打印为“假”
df_18.isnull().sum().any()
```




    False



## 重复数据删除


```python
# 打印 2008 年和 2018 年数据集的重复数量
df_08.duplicated().sum()
df_18.duplicated().sum()
```




    3




```python
# 丢弃两个数据集中的重复数据
df_08 = df_08.drop_duplicates(keep=False)
df_08 = df_18.drop_duplicates(keep=False)
```


```python
# 再次打印重复数量，确认重复数据已删除——均应为 0 
df_08.duplicated().sum()
df_18.duplicated().sum()
```




    3




```python
# 保存进度，以便下一段使用
df_08.to_csv('data_08.csv', index=False)
df_18.to_csv('data_18.csv', index=False)
```
