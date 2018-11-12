

What good is data without a good plot to tell the story?

Below I have generic uber data renamed as Pyber that I will be analyzing to help depict a story beyond just the raw data.


```python
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
import csv

#import csvs
ride_csv= "../raw_data/ride_data.csv"
city_csv= "../raw_data/city_data.csv"

#read csvs into df
ride_df = pd.read_csv(ride_csv)
city_df = pd.read_csv(city_csv)

#merge dataframes
data = pd.merge(ride_df,city_df, on='city', how='outer')
data
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
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Sarabury</td>
      <td>2016-07-23 07:42:44</td>
      <td>21.76</td>
      <td>7546681945283</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sarabury</td>
      <td>2016-04-02 04:32:25</td>
      <td>38.03</td>
      <td>4932495851866</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sarabury</td>
      <td>2016-06-23 05:03:41</td>
      <td>26.82</td>
      <td>6711035373406</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Sarabury</td>
      <td>2016-09-30 12:48:34</td>
      <td>30.30</td>
      <td>6388737278232</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Sarabury</td>
      <td>2016-08-04 00:25:52</td>
      <td>27.20</td>
      <td>2429366407526</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Sarabury</td>
      <td>2016-07-25 10:44:01</td>
      <td>17.73</td>
      <td>4467299640441</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Sarabury</td>
      <td>2016-06-22 16:24:01</td>
      <td>23.94</td>
      <td>6153395712431</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Sarabury</td>
      <td>2016-01-27 17:46:45</td>
      <td>16.39</td>
      <td>8220809448298</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Sarabury</td>
      <td>2016-04-26 11:31:30</td>
      <td>21.80</td>
      <td>5969441875705</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Sarabury</td>
      <td>2016-08-14 19:56:59</td>
      <td>7.83</td>
      <td>4979570237054</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Sarabury</td>
      <td>2016-01-06 03:02:55</td>
      <td>5.19</td>
      <td>9988466326333</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Sarabury</td>
      <td>2016-03-29 15:47:35</td>
      <td>17.00</td>
      <td>3574423871181</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Sarabury</td>
      <td>2016-11-20 11:44:23</td>
      <td>28.47</td>
      <td>3793266633941</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Sarabury</td>
      <td>2016-07-17 20:41:06</td>
      <td>17.79</td>
      <td>9661023488490</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Sarabury</td>
      <td>2016-11-06 02:23:59</td>
      <td>19.48</td>
      <td>7305651789766</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Sarabury</td>
      <td>2016-09-26 07:30:31</td>
      <td>26.71</td>
      <td>6310253827816</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Sarabury</td>
      <td>2016-06-04 20:50:52</td>
      <td>14.19</td>
      <td>8765571028809</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Sarabury</td>
      <td>2016-01-22 23:12:06</td>
      <td>38.40</td>
      <td>1176229756048</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Sarabury</td>
      <td>2016-03-29 19:07:55</td>
      <td>20.56</td>
      <td>7019491956393</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Sarabury</td>
      <td>2016-10-18 04:33:23</td>
      <td>37.50</td>
      <td>1054393799736</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Sarabury</td>
      <td>2016-09-30 20:41:18</td>
      <td>44.32</td>
      <td>2103508227691</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Sarabury</td>
      <td>2016-07-30 10:37:38</td>
      <td>25.99</td>
      <td>5233926699781</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Sarabury</td>
      <td>2016-04-01 07:15:24</td>
      <td>6.94</td>
      <td>1931215121299</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Sarabury</td>
      <td>2016-11-23 03:08:59</td>
      <td>37.17</td>
      <td>9141412183460</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Sarabury</td>
      <td>2016-10-23 02:40:28</td>
      <td>17.23</td>
      <td>1977978528067</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Sarabury</td>
      <td>2016-04-06 21:02:54</td>
      <td>7.14</td>
      <td>6096364843852</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>27</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
      <td>35</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>28</th>
      <td>South Roy</td>
      <td>2016-12-03 08:39:02</td>
      <td>32.88</td>
      <td>7098916182845</td>
      <td>35</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>29</th>
      <td>South Roy</td>
      <td>2016-11-20 02:09:58</td>
      <td>6.81</td>
      <td>6512612750531</td>
      <td>35</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2377</th>
      <td>East Leslie</td>
      <td>2016-11-28 09:09:15</td>
      <td>37.76</td>
      <td>804829686137</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2378</th>
      <td>East Leslie</td>
      <td>2016-09-08 19:19:38</td>
      <td>30.59</td>
      <td>8211833105097</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2379</th>
      <td>East Leslie</td>
      <td>2016-03-02 22:09:34</td>
      <td>36.61</td>
      <td>5500269118478</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2380</th>
      <td>East Leslie</td>
      <td>2016-06-22 07:45:30</td>
      <td>34.54</td>
      <td>684950063164</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2381</th>
      <td>North Whitney</td>
      <td>2016-04-01 21:21:37</td>
      <td>51.01</td>
      <td>612689673941</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2382</th>
      <td>North Whitney</td>
      <td>2016-04-26 09:35:48</td>
      <td>42.09</td>
      <td>9465134041656</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2383</th>
      <td>North Whitney</td>
      <td>2016-06-24 21:09:09</td>
      <td>50.03</td>
      <td>9224879345166</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2384</th>
      <td>North Whitney</td>
      <td>2016-06-10 18:27:03</td>
      <td>29.25</td>
      <td>4071225680519</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2385</th>
      <td>North Whitney</td>
      <td>2016-02-21 18:20:14</td>
      <td>42.01</td>
      <td>3306522110065</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2386</th>
      <td>North Whitney</td>
      <td>2016-11-14 10:46:11</td>
      <td>55.07</td>
      <td>8000095653619</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2387</th>
      <td>North Whitney</td>
      <td>2016-01-24 09:14:51</td>
      <td>24.37</td>
      <td>7069044920500</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2388</th>
      <td>North Whitney</td>
      <td>2016-03-24 10:27:00</td>
      <td>29.72</td>
      <td>3818227780479</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2389</th>
      <td>North Whitney</td>
      <td>2016-11-11 16:24:16</td>
      <td>22.99</td>
      <td>3454326063039</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2390</th>
      <td>North Whitney</td>
      <td>2016-01-26 01:06:41</td>
      <td>34.92</td>
      <td>4165974278063</td>
      <td>10</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2391</th>
      <td>Manuelchester</td>
      <td>2016-03-21 22:15:25</td>
      <td>49.62</td>
      <td>6045427401799</td>
      <td>7</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2392</th>
      <td>Shelbyhaven</td>
      <td>2016-05-24 15:29:59</td>
      <td>18.11</td>
      <td>1144791937271</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2393</th>
      <td>Shelbyhaven</td>
      <td>2016-10-17 14:47:38</td>
      <td>53.42</td>
      <td>8515375903761</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2394</th>
      <td>Shelbyhaven</td>
      <td>2016-04-21 19:22:03</td>
      <td>37.19</td>
      <td>5142074323359</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2395</th>
      <td>Shelbyhaven</td>
      <td>2016-06-12 16:57:25</td>
      <td>30.18</td>
      <td>2015025942653</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2396</th>
      <td>Shelbyhaven</td>
      <td>2016-07-22 05:59:01</td>
      <td>10.64</td>
      <td>1406024986969</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2397</th>
      <td>Shelbyhaven</td>
      <td>2016-01-25 01:39:16</td>
      <td>59.43</td>
      <td>8088329954312</td>
      <td>9</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2398</th>
      <td>South Elizabethmouth</td>
      <td>2016-04-03 11:13:07</td>
      <td>22.79</td>
      <td>8193837300497</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2399</th>
      <td>South Elizabethmouth</td>
      <td>2016-03-11 12:27:01</td>
      <td>26.72</td>
      <td>4943246873754</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2400</th>
      <td>South Elizabethmouth</td>
      <td>2016-11-23 07:47:18</td>
      <td>46.39</td>
      <td>1939838068038</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2401</th>
      <td>South Elizabethmouth</td>
      <td>2016-07-19 09:35:59</td>
      <td>31.09</td>
      <td>2959749591417</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2402</th>
      <td>South Elizabethmouth</td>
      <td>2016-04-21 10:20:09</td>
      <td>16.50</td>
      <td>5702608059064</td>
      <td>3</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2403</th>
      <td>Matthewside</td>
      <td>2016-02-23 17:46:29</td>
      <td>59.65</td>
      <td>241191157535</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2404</th>
      <td>Matthewside</td>
      <td>2016-02-23 00:43:51</td>
      <td>40.84</td>
      <td>8665248512368</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2405</th>
      <td>Matthewside</td>
      <td>2016-05-18 02:00:30</td>
      <td>48.67</td>
      <td>2049161404256</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
    <tr>
      <th>2406</th>
      <td>Matthewside</td>
      <td>2016-08-08 14:02:35</td>
      <td>24.97</td>
      <td>2872494724827</td>
      <td>4</td>
      <td>Rural</td>
    </tr>
  </tbody>
</table>
<p>2407 rows × 6 columns</p>
</div>




```python
unique_cities = data["city"].unique()
cityid_df = pd.DataFrame(unique_cities).reset_index()
data_with_cityid = pd.merge(data,cityid_df,left_on='city', right_on=0, how='left')
data_with_cityid = data_with_cityid.rename(columns={0: "city1",'index': 'city id'})
data_with_cityid['city id'] = data_with_cityid['city id'] + 101
data_with_cityid
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
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
      <th>type</th>
      <th>city id</th>
      <th>city1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Sarabury</td>
      <td>2016-07-23 07:42:44</td>
      <td>21.76</td>
      <td>7546681945283</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Sarabury</td>
      <td>2016-04-02 04:32:25</td>
      <td>38.03</td>
      <td>4932495851866</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Sarabury</td>
      <td>2016-06-23 05:03:41</td>
      <td>26.82</td>
      <td>6711035373406</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Sarabury</td>
      <td>2016-09-30 12:48:34</td>
      <td>30.30</td>
      <td>6388737278232</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Sarabury</td>
      <td>2016-08-04 00:25:52</td>
      <td>27.20</td>
      <td>2429366407526</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Sarabury</td>
      <td>2016-07-25 10:44:01</td>
      <td>17.73</td>
      <td>4467299640441</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Sarabury</td>
      <td>2016-06-22 16:24:01</td>
      <td>23.94</td>
      <td>6153395712431</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Sarabury</td>
      <td>2016-01-27 17:46:45</td>
      <td>16.39</td>
      <td>8220809448298</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Sarabury</td>
      <td>2016-04-26 11:31:30</td>
      <td>21.80</td>
      <td>5969441875705</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Sarabury</td>
      <td>2016-08-14 19:56:59</td>
      <td>7.83</td>
      <td>4979570237054</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Sarabury</td>
      <td>2016-01-06 03:02:55</td>
      <td>5.19</td>
      <td>9988466326333</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Sarabury</td>
      <td>2016-03-29 15:47:35</td>
      <td>17.00</td>
      <td>3574423871181</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Sarabury</td>
      <td>2016-11-20 11:44:23</td>
      <td>28.47</td>
      <td>3793266633941</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Sarabury</td>
      <td>2016-07-17 20:41:06</td>
      <td>17.79</td>
      <td>9661023488490</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Sarabury</td>
      <td>2016-11-06 02:23:59</td>
      <td>19.48</td>
      <td>7305651789766</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Sarabury</td>
      <td>2016-09-26 07:30:31</td>
      <td>26.71</td>
      <td>6310253827816</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Sarabury</td>
      <td>2016-06-04 20:50:52</td>
      <td>14.19</td>
      <td>8765571028809</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Sarabury</td>
      <td>2016-01-22 23:12:06</td>
      <td>38.40</td>
      <td>1176229756048</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Sarabury</td>
      <td>2016-03-29 19:07:55</td>
      <td>20.56</td>
      <td>7019491956393</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Sarabury</td>
      <td>2016-10-18 04:33:23</td>
      <td>37.50</td>
      <td>1054393799736</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Sarabury</td>
      <td>2016-09-30 20:41:18</td>
      <td>44.32</td>
      <td>2103508227691</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Sarabury</td>
      <td>2016-07-30 10:37:38</td>
      <td>25.99</td>
      <td>5233926699781</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Sarabury</td>
      <td>2016-04-01 07:15:24</td>
      <td>6.94</td>
      <td>1931215121299</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Sarabury</td>
      <td>2016-11-23 03:08:59</td>
      <td>37.17</td>
      <td>9141412183460</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Sarabury</td>
      <td>2016-10-23 02:40:28</td>
      <td>17.23</td>
      <td>1977978528067</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Sarabury</td>
      <td>2016-04-06 21:02:54</td>
      <td>7.14</td>
      <td>6096364843852</td>
      <td>46</td>
      <td>Urban</td>
      <td>101</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>27</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
      <td>35</td>
      <td>Urban</td>
      <td>102</td>
      <td>South Roy</td>
    </tr>
    <tr>
      <th>28</th>
      <td>South Roy</td>
      <td>2016-12-03 08:39:02</td>
      <td>32.88</td>
      <td>7098916182845</td>
      <td>35</td>
      <td>Urban</td>
      <td>102</td>
      <td>South Roy</td>
    </tr>
    <tr>
      <th>29</th>
      <td>South Roy</td>
      <td>2016-11-20 02:09:58</td>
      <td>6.81</td>
      <td>6512612750531</td>
      <td>35</td>
      <td>Urban</td>
      <td>102</td>
      <td>South Roy</td>
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
    </tr>
    <tr>
      <th>2377</th>
      <td>East Leslie</td>
      <td>2016-11-28 09:09:15</td>
      <td>37.76</td>
      <td>804829686137</td>
      <td>9</td>
      <td>Rural</td>
      <td>220</td>
      <td>East Leslie</td>
    </tr>
    <tr>
      <th>2378</th>
      <td>East Leslie</td>
      <td>2016-09-08 19:19:38</td>
      <td>30.59</td>
      <td>8211833105097</td>
      <td>9</td>
      <td>Rural</td>
      <td>220</td>
      <td>East Leslie</td>
    </tr>
    <tr>
      <th>2379</th>
      <td>East Leslie</td>
      <td>2016-03-02 22:09:34</td>
      <td>36.61</td>
      <td>5500269118478</td>
      <td>9</td>
      <td>Rural</td>
      <td>220</td>
      <td>East Leslie</td>
    </tr>
    <tr>
      <th>2380</th>
      <td>East Leslie</td>
      <td>2016-06-22 07:45:30</td>
      <td>34.54</td>
      <td>684950063164</td>
      <td>9</td>
      <td>Rural</td>
      <td>220</td>
      <td>East Leslie</td>
    </tr>
    <tr>
      <th>2381</th>
      <td>North Whitney</td>
      <td>2016-04-01 21:21:37</td>
      <td>51.01</td>
      <td>612689673941</td>
      <td>10</td>
      <td>Rural</td>
      <td>221</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>2382</th>
      <td>North Whitney</td>
      <td>2016-04-26 09:35:48</td>
      <td>42.09</td>
      <td>9465134041656</td>
      <td>10</td>
      <td>Rural</td>
      <td>221</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>2383</th>
      <td>North Whitney</td>
      <td>2016-06-24 21:09:09</td>
      <td>50.03</td>
      <td>9224879345166</td>
      <td>10</td>
      <td>Rural</td>
      <td>221</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>2384</th>
      <td>North Whitney</td>
      <td>2016-06-10 18:27:03</td>
      <td>29.25</td>
      <td>4071225680519</td>
      <td>10</td>
      <td>Rural</td>
      <td>221</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>2385</th>
      <td>North Whitney</td>
      <td>2016-02-21 18:20:14</td>
      <td>42.01</td>
      <td>3306522110065</td>
      <td>10</td>
      <td>Rural</td>
      <td>221</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>2386</th>
      <td>North Whitney</td>
      <td>2016-11-14 10:46:11</td>
      <td>55.07</td>
      <td>8000095653619</td>
      <td>10</td>
      <td>Rural</td>
      <td>221</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>2387</th>
      <td>North Whitney</td>
      <td>2016-01-24 09:14:51</td>
      <td>24.37</td>
      <td>7069044920500</td>
      <td>10</td>
      <td>Rural</td>
      <td>221</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>2388</th>
      <td>North Whitney</td>
      <td>2016-03-24 10:27:00</td>
      <td>29.72</td>
      <td>3818227780479</td>
      <td>10</td>
      <td>Rural</td>
      <td>221</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>2389</th>
      <td>North Whitney</td>
      <td>2016-11-11 16:24:16</td>
      <td>22.99</td>
      <td>3454326063039</td>
      <td>10</td>
      <td>Rural</td>
      <td>221</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>2390</th>
      <td>North Whitney</td>
      <td>2016-01-26 01:06:41</td>
      <td>34.92</td>
      <td>4165974278063</td>
      <td>10</td>
      <td>Rural</td>
      <td>221</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>2391</th>
      <td>Manuelchester</td>
      <td>2016-03-21 22:15:25</td>
      <td>49.62</td>
      <td>6045427401799</td>
      <td>7</td>
      <td>Rural</td>
      <td>222</td>
      <td>Manuelchester</td>
    </tr>
    <tr>
      <th>2392</th>
      <td>Shelbyhaven</td>
      <td>2016-05-24 15:29:59</td>
      <td>18.11</td>
      <td>1144791937271</td>
      <td>9</td>
      <td>Rural</td>
      <td>223</td>
      <td>Shelbyhaven</td>
    </tr>
    <tr>
      <th>2393</th>
      <td>Shelbyhaven</td>
      <td>2016-10-17 14:47:38</td>
      <td>53.42</td>
      <td>8515375903761</td>
      <td>9</td>
      <td>Rural</td>
      <td>223</td>
      <td>Shelbyhaven</td>
    </tr>
    <tr>
      <th>2394</th>
      <td>Shelbyhaven</td>
      <td>2016-04-21 19:22:03</td>
      <td>37.19</td>
      <td>5142074323359</td>
      <td>9</td>
      <td>Rural</td>
      <td>223</td>
      <td>Shelbyhaven</td>
    </tr>
    <tr>
      <th>2395</th>
      <td>Shelbyhaven</td>
      <td>2016-06-12 16:57:25</td>
      <td>30.18</td>
      <td>2015025942653</td>
      <td>9</td>
      <td>Rural</td>
      <td>223</td>
      <td>Shelbyhaven</td>
    </tr>
    <tr>
      <th>2396</th>
      <td>Shelbyhaven</td>
      <td>2016-07-22 05:59:01</td>
      <td>10.64</td>
      <td>1406024986969</td>
      <td>9</td>
      <td>Rural</td>
      <td>223</td>
      <td>Shelbyhaven</td>
    </tr>
    <tr>
      <th>2397</th>
      <td>Shelbyhaven</td>
      <td>2016-01-25 01:39:16</td>
      <td>59.43</td>
      <td>8088329954312</td>
      <td>9</td>
      <td>Rural</td>
      <td>223</td>
      <td>Shelbyhaven</td>
    </tr>
    <tr>
      <th>2398</th>
      <td>South Elizabethmouth</td>
      <td>2016-04-03 11:13:07</td>
      <td>22.79</td>
      <td>8193837300497</td>
      <td>3</td>
      <td>Rural</td>
      <td>224</td>
      <td>South Elizabethmouth</td>
    </tr>
    <tr>
      <th>2399</th>
      <td>South Elizabethmouth</td>
      <td>2016-03-11 12:27:01</td>
      <td>26.72</td>
      <td>4943246873754</td>
      <td>3</td>
      <td>Rural</td>
      <td>224</td>
      <td>South Elizabethmouth</td>
    </tr>
    <tr>
      <th>2400</th>
      <td>South Elizabethmouth</td>
      <td>2016-11-23 07:47:18</td>
      <td>46.39</td>
      <td>1939838068038</td>
      <td>3</td>
      <td>Rural</td>
      <td>224</td>
      <td>South Elizabethmouth</td>
    </tr>
    <tr>
      <th>2401</th>
      <td>South Elizabethmouth</td>
      <td>2016-07-19 09:35:59</td>
      <td>31.09</td>
      <td>2959749591417</td>
      <td>3</td>
      <td>Rural</td>
      <td>224</td>
      <td>South Elizabethmouth</td>
    </tr>
    <tr>
      <th>2402</th>
      <td>South Elizabethmouth</td>
      <td>2016-04-21 10:20:09</td>
      <td>16.50</td>
      <td>5702608059064</td>
      <td>3</td>
      <td>Rural</td>
      <td>224</td>
      <td>South Elizabethmouth</td>
    </tr>
    <tr>
      <th>2403</th>
      <td>Matthewside</td>
      <td>2016-02-23 17:46:29</td>
      <td>59.65</td>
      <td>241191157535</td>
      <td>4</td>
      <td>Rural</td>
      <td>225</td>
      <td>Matthewside</td>
    </tr>
    <tr>
      <th>2404</th>
      <td>Matthewside</td>
      <td>2016-02-23 00:43:51</td>
      <td>40.84</td>
      <td>8665248512368</td>
      <td>4</td>
      <td>Rural</td>
      <td>225</td>
      <td>Matthewside</td>
    </tr>
    <tr>
      <th>2405</th>
      <td>Matthewside</td>
      <td>2016-05-18 02:00:30</td>
      <td>48.67</td>
      <td>2049161404256</td>
      <td>4</td>
      <td>Rural</td>
      <td>225</td>
      <td>Matthewside</td>
    </tr>
    <tr>
      <th>2406</th>
      <td>Matthewside</td>
      <td>2016-08-08 14:02:35</td>
      <td>24.97</td>
      <td>2872494724827</td>
      <td>4</td>
      <td>Rural</td>
      <td>225</td>
      <td>Matthewside</td>
    </tr>
  </tbody>
</table>
<p>2407 rows × 8 columns</p>
</div>




```python
data_with_cityid = data_with_cityid.set_index('city id')
data_with_cityid
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
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
      <th>type</th>
      <th>city1</th>
    </tr>
    <tr>
      <th>city id</th>
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
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-07-23 07:42:44</td>
      <td>21.76</td>
      <td>7546681945283</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-04-02 04:32:25</td>
      <td>38.03</td>
      <td>4932495851866</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-06-23 05:03:41</td>
      <td>26.82</td>
      <td>6711035373406</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-09-30 12:48:34</td>
      <td>30.30</td>
      <td>6388737278232</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-08-04 00:25:52</td>
      <td>27.20</td>
      <td>2429366407526</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-07-25 10:44:01</td>
      <td>17.73</td>
      <td>4467299640441</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-06-22 16:24:01</td>
      <td>23.94</td>
      <td>6153395712431</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-01-27 17:46:45</td>
      <td>16.39</td>
      <td>8220809448298</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-04-26 11:31:30</td>
      <td>21.80</td>
      <td>5969441875705</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-08-14 19:56:59</td>
      <td>7.83</td>
      <td>4979570237054</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-01-06 03:02:55</td>
      <td>5.19</td>
      <td>9988466326333</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-03-29 15:47:35</td>
      <td>17.00</td>
      <td>3574423871181</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-11-20 11:44:23</td>
      <td>28.47</td>
      <td>3793266633941</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-07-17 20:41:06</td>
      <td>17.79</td>
      <td>9661023488490</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-11-06 02:23:59</td>
      <td>19.48</td>
      <td>7305651789766</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-09-26 07:30:31</td>
      <td>26.71</td>
      <td>6310253827816</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-06-04 20:50:52</td>
      <td>14.19</td>
      <td>8765571028809</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-01-22 23:12:06</td>
      <td>38.40</td>
      <td>1176229756048</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-03-29 19:07:55</td>
      <td>20.56</td>
      <td>7019491956393</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-10-18 04:33:23</td>
      <td>37.50</td>
      <td>1054393799736</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-09-30 20:41:18</td>
      <td>44.32</td>
      <td>2103508227691</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-07-30 10:37:38</td>
      <td>25.99</td>
      <td>5233926699781</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-04-01 07:15:24</td>
      <td>6.94</td>
      <td>1931215121299</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-11-23 03:08:59</td>
      <td>37.17</td>
      <td>9141412183460</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-10-23 02:40:28</td>
      <td>17.23</td>
      <td>1977978528067</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>101</th>
      <td>Sarabury</td>
      <td>2016-04-06 21:02:54</td>
      <td>7.14</td>
      <td>6096364843852</td>
      <td>46</td>
      <td>Urban</td>
      <td>Sarabury</td>
    </tr>
    <tr>
      <th>102</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
      <td>35</td>
      <td>Urban</td>
      <td>South Roy</td>
    </tr>
    <tr>
      <th>102</th>
      <td>South Roy</td>
      <td>2016-12-03 08:39:02</td>
      <td>32.88</td>
      <td>7098916182845</td>
      <td>35</td>
      <td>Urban</td>
      <td>South Roy</td>
    </tr>
    <tr>
      <th>102</th>
      <td>South Roy</td>
      <td>2016-11-20 02:09:58</td>
      <td>6.81</td>
      <td>6512612750531</td>
      <td>35</td>
      <td>Urban</td>
      <td>South Roy</td>
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
    </tr>
    <tr>
      <th>220</th>
      <td>East Leslie</td>
      <td>2016-11-28 09:09:15</td>
      <td>37.76</td>
      <td>804829686137</td>
      <td>9</td>
      <td>Rural</td>
      <td>East Leslie</td>
    </tr>
    <tr>
      <th>220</th>
      <td>East Leslie</td>
      <td>2016-09-08 19:19:38</td>
      <td>30.59</td>
      <td>8211833105097</td>
      <td>9</td>
      <td>Rural</td>
      <td>East Leslie</td>
    </tr>
    <tr>
      <th>220</th>
      <td>East Leslie</td>
      <td>2016-03-02 22:09:34</td>
      <td>36.61</td>
      <td>5500269118478</td>
      <td>9</td>
      <td>Rural</td>
      <td>East Leslie</td>
    </tr>
    <tr>
      <th>220</th>
      <td>East Leslie</td>
      <td>2016-06-22 07:45:30</td>
      <td>34.54</td>
      <td>684950063164</td>
      <td>9</td>
      <td>Rural</td>
      <td>East Leslie</td>
    </tr>
    <tr>
      <th>221</th>
      <td>North Whitney</td>
      <td>2016-04-01 21:21:37</td>
      <td>51.01</td>
      <td>612689673941</td>
      <td>10</td>
      <td>Rural</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>221</th>
      <td>North Whitney</td>
      <td>2016-04-26 09:35:48</td>
      <td>42.09</td>
      <td>9465134041656</td>
      <td>10</td>
      <td>Rural</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>221</th>
      <td>North Whitney</td>
      <td>2016-06-24 21:09:09</td>
      <td>50.03</td>
      <td>9224879345166</td>
      <td>10</td>
      <td>Rural</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>221</th>
      <td>North Whitney</td>
      <td>2016-06-10 18:27:03</td>
      <td>29.25</td>
      <td>4071225680519</td>
      <td>10</td>
      <td>Rural</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>221</th>
      <td>North Whitney</td>
      <td>2016-02-21 18:20:14</td>
      <td>42.01</td>
      <td>3306522110065</td>
      <td>10</td>
      <td>Rural</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>221</th>
      <td>North Whitney</td>
      <td>2016-11-14 10:46:11</td>
      <td>55.07</td>
      <td>8000095653619</td>
      <td>10</td>
      <td>Rural</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>221</th>
      <td>North Whitney</td>
      <td>2016-01-24 09:14:51</td>
      <td>24.37</td>
      <td>7069044920500</td>
      <td>10</td>
      <td>Rural</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>221</th>
      <td>North Whitney</td>
      <td>2016-03-24 10:27:00</td>
      <td>29.72</td>
      <td>3818227780479</td>
      <td>10</td>
      <td>Rural</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>221</th>
      <td>North Whitney</td>
      <td>2016-11-11 16:24:16</td>
      <td>22.99</td>
      <td>3454326063039</td>
      <td>10</td>
      <td>Rural</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>221</th>
      <td>North Whitney</td>
      <td>2016-01-26 01:06:41</td>
      <td>34.92</td>
      <td>4165974278063</td>
      <td>10</td>
      <td>Rural</td>
      <td>North Whitney</td>
    </tr>
    <tr>
      <th>222</th>
      <td>Manuelchester</td>
      <td>2016-03-21 22:15:25</td>
      <td>49.62</td>
      <td>6045427401799</td>
      <td>7</td>
      <td>Rural</td>
      <td>Manuelchester</td>
    </tr>
    <tr>
      <th>223</th>
      <td>Shelbyhaven</td>
      <td>2016-05-24 15:29:59</td>
      <td>18.11</td>
      <td>1144791937271</td>
      <td>9</td>
      <td>Rural</td>
      <td>Shelbyhaven</td>
    </tr>
    <tr>
      <th>223</th>
      <td>Shelbyhaven</td>
      <td>2016-10-17 14:47:38</td>
      <td>53.42</td>
      <td>8515375903761</td>
      <td>9</td>
      <td>Rural</td>
      <td>Shelbyhaven</td>
    </tr>
    <tr>
      <th>223</th>
      <td>Shelbyhaven</td>
      <td>2016-04-21 19:22:03</td>
      <td>37.19</td>
      <td>5142074323359</td>
      <td>9</td>
      <td>Rural</td>
      <td>Shelbyhaven</td>
    </tr>
    <tr>
      <th>223</th>
      <td>Shelbyhaven</td>
      <td>2016-06-12 16:57:25</td>
      <td>30.18</td>
      <td>2015025942653</td>
      <td>9</td>
      <td>Rural</td>
      <td>Shelbyhaven</td>
    </tr>
    <tr>
      <th>223</th>
      <td>Shelbyhaven</td>
      <td>2016-07-22 05:59:01</td>
      <td>10.64</td>
      <td>1406024986969</td>
      <td>9</td>
      <td>Rural</td>
      <td>Shelbyhaven</td>
    </tr>
    <tr>
      <th>223</th>
      <td>Shelbyhaven</td>
      <td>2016-01-25 01:39:16</td>
      <td>59.43</td>
      <td>8088329954312</td>
      <td>9</td>
      <td>Rural</td>
      <td>Shelbyhaven</td>
    </tr>
    <tr>
      <th>224</th>
      <td>South Elizabethmouth</td>
      <td>2016-04-03 11:13:07</td>
      <td>22.79</td>
      <td>8193837300497</td>
      <td>3</td>
      <td>Rural</td>
      <td>South Elizabethmouth</td>
    </tr>
    <tr>
      <th>224</th>
      <td>South Elizabethmouth</td>
      <td>2016-03-11 12:27:01</td>
      <td>26.72</td>
      <td>4943246873754</td>
      <td>3</td>
      <td>Rural</td>
      <td>South Elizabethmouth</td>
    </tr>
    <tr>
      <th>224</th>
      <td>South Elizabethmouth</td>
      <td>2016-11-23 07:47:18</td>
      <td>46.39</td>
      <td>1939838068038</td>
      <td>3</td>
      <td>Rural</td>
      <td>South Elizabethmouth</td>
    </tr>
    <tr>
      <th>224</th>
      <td>South Elizabethmouth</td>
      <td>2016-07-19 09:35:59</td>
      <td>31.09</td>
      <td>2959749591417</td>
      <td>3</td>
      <td>Rural</td>
      <td>South Elizabethmouth</td>
    </tr>
    <tr>
      <th>224</th>
      <td>South Elizabethmouth</td>
      <td>2016-04-21 10:20:09</td>
      <td>16.50</td>
      <td>5702608059064</td>
      <td>3</td>
      <td>Rural</td>
      <td>South Elizabethmouth</td>
    </tr>
    <tr>
      <th>225</th>
      <td>Matthewside</td>
      <td>2016-02-23 17:46:29</td>
      <td>59.65</td>
      <td>241191157535</td>
      <td>4</td>
      <td>Rural</td>
      <td>Matthewside</td>
    </tr>
    <tr>
      <th>225</th>
      <td>Matthewside</td>
      <td>2016-02-23 00:43:51</td>
      <td>40.84</td>
      <td>8665248512368</td>
      <td>4</td>
      <td>Rural</td>
      <td>Matthewside</td>
    </tr>
    <tr>
      <th>225</th>
      <td>Matthewside</td>
      <td>2016-05-18 02:00:30</td>
      <td>48.67</td>
      <td>2049161404256</td>
      <td>4</td>
      <td>Rural</td>
      <td>Matthewside</td>
    </tr>
    <tr>
      <th>225</th>
      <td>Matthewside</td>
      <td>2016-08-08 14:02:35</td>
      <td>24.97</td>
      <td>2872494724827</td>
      <td>4</td>
      <td>Rural</td>
      <td>Matthewside</td>
    </tr>
  </tbody>
</table>
<p>2407 rows × 7 columns</p>
</div>




```python
# Create the GroupBy object based on the "city column
fare_by_city = data_with_cityid.groupby(["city id",'city','type'])

# Calculate averages for fares from each city using the .mean() method
fare_by_city.mean()
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
      <th></th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
    </tr>
    <tr>
      <th>city id</th>
      <th>city</th>
      <th>type</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>101</th>
      <th>Sarabury</th>
      <th>Urban</th>
      <td>23.490000</td>
      <td>5.493915e+12</td>
      <td>46.0</td>
    </tr>
    <tr>
      <th>102</th>
      <th>South Roy</th>
      <th>Urban</th>
      <td>26.031364</td>
      <td>4.862249e+12</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>103</th>
      <th>Wiseborough</th>
      <th>Urban</th>
      <td>22.676842</td>
      <td>6.046575e+12</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>104</th>
      <th>Spencertown</th>
      <th>Urban</th>
      <td>23.681154</td>
      <td>4.850559e+12</td>
      <td>68.0</td>
    </tr>
    <tr>
      <th>105</th>
      <th>Nguyenbury</th>
      <th>Urban</th>
      <td>25.899615</td>
      <td>4.138011e+12</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>106</th>
      <th>New Jeffrey</th>
      <th>Urban</th>
      <td>24.130000</td>
      <td>4.605064e+12</td>
      <td>58.0</td>
    </tr>
    <tr>
      <th>107</th>
      <th>Port Johnstad</th>
      <th>Urban</th>
      <td>25.882941</td>
      <td>4.853955e+12</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>108</th>
      <th>Jacobfort</th>
      <th>Urban</th>
      <td>24.779355</td>
      <td>4.099091e+12</td>
      <td>52.0</td>
    </tr>
    <tr>
      <th>109</th>
      <th>Travisville</th>
      <th>Urban</th>
      <td>27.220870</td>
      <td>3.317507e+12</td>
      <td>37.0</td>
    </tr>
    <tr>
      <th>110</th>
      <th>Sandymouth</th>
      <th>Urban</th>
      <td>23.105926</td>
      <td>4.511717e+12</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>111</th>
      <th>New Andreamouth</th>
      <th>Urban</th>
      <td>24.966786</td>
      <td>5.616858e+12</td>
      <td>42.0</td>
    </tr>
    <tr>
      <th>112</th>
      <th>New Christine</th>
      <th>Urban</th>
      <td>24.157727</td>
      <td>4.285710e+12</td>
      <td>22.0</td>
    </tr>
    <tr>
      <th>113</th>
      <th>Stewartview</th>
      <th>Urban</th>
      <td>21.614000</td>
      <td>4.936695e+12</td>
      <td>49.0</td>
    </tr>
    <tr>
      <th>114</th>
      <th>Rodriguezburgh</th>
      <th>Urban</th>
      <td>21.332609</td>
      <td>5.703310e+12</td>
      <td>52.0</td>
    </tr>
    <tr>
      <th>115</th>
      <th>West Sydneyhaven</th>
      <th>Urban</th>
      <td>22.368333</td>
      <td>4.432234e+12</td>
      <td>70.0</td>
    </tr>
    <tr>
      <th>116</th>
      <th>Swansonbury</th>
      <th>Urban</th>
      <td>27.464706</td>
      <td>4.443028e+12</td>
      <td>64.0</td>
    </tr>
    <tr>
      <th>117</th>
      <th>Lisatown</th>
      <th>Urban</th>
      <td>22.225217</td>
      <td>5.372689e+12</td>
      <td>47.0</td>
    </tr>
    <tr>
      <th>118</th>
      <th>East Erin</th>
      <th>Urban</th>
      <td>24.478214</td>
      <td>5.226259e+12</td>
      <td>43.0</td>
    </tr>
    <tr>
      <th>119</th>
      <th>Port Martinberg</th>
      <th>Urban</th>
      <td>22.329524</td>
      <td>3.589751e+12</td>
      <td>44.0</td>
    </tr>
    <tr>
      <th>120</th>
      <th>Edwardsbury</th>
      <th>Urban</th>
      <td>26.876667</td>
      <td>5.296117e+12</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>121</th>
      <th>Pamelahaven</th>
      <th>Urban</th>
      <td>25.549333</td>
      <td>5.805728e+12</td>
      <td>30.0</td>
    </tr>
    <tr>
      <th>122</th>
      <th>Fosterside</th>
      <th>Urban</th>
      <td>23.034583</td>
      <td>5.101131e+12</td>
      <td>69.0</td>
    </tr>
    <tr>
      <th>123</th>
      <th>West Alexis</th>
      <th>Urban</th>
      <td>19.523000</td>
      <td>5.133766e+12</td>
      <td>47.0</td>
    </tr>
    <tr>
      <th>124</th>
      <th>Carrollfort</th>
      <th>Urban</th>
      <td>25.395517</td>
      <td>4.759008e+12</td>
      <td>55.0</td>
    </tr>
    <tr>
      <th>125</th>
      <th>New David</th>
      <th>Urban</th>
      <td>27.084286</td>
      <td>4.926039e+12</td>
      <td>31.0</td>
    </tr>
    <tr>
      <th>126</th>
      <th>Williamshire</th>
      <th>Urban</th>
      <td>26.990323</td>
      <td>4.937704e+12</td>
      <td>70.0</td>
    </tr>
    <tr>
      <th>127</th>
      <th>Torresshire</th>
      <th>Urban</th>
      <td>24.207308</td>
      <td>5.117907e+12</td>
      <td>70.0</td>
    </tr>
    <tr>
      <th>128</th>
      <th>New Aaron</th>
      <th>Urban</th>
      <td>26.861818</td>
      <td>4.469816e+12</td>
      <td>60.0</td>
    </tr>
    <tr>
      <th>129</th>
      <th>Kelseyland</th>
      <th>Urban</th>
      <td>21.806429</td>
      <td>4.506717e+12</td>
      <td>63.0</td>
    </tr>
    <tr>
      <th>130</th>
      <th>Lake Sarashire</th>
      <th>Urban</th>
      <td>26.610000</td>
      <td>4.658841e+12</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>196</th>
      <th>West Evan</th>
      <th>Suburban</th>
      <td>27.013333</td>
      <td>5.445616e+12</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>197</th>
      <th>Sarahview</th>
      <th>Suburban</th>
      <td>33.862000</td>
      <td>5.642540e+12</td>
      <td>18.0</td>
    </tr>
    <tr>
      <th>198</th>
      <th>South Jennifer</th>
      <th>Suburban</th>
      <td>29.798750</td>
      <td>5.440050e+12</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>199</th>
      <th>Floresberg</th>
      <th>Suburban</th>
      <td>32.310000</td>
      <td>2.630319e+12</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>200</th>
      <th>Williamchester</th>
      <th>Suburban</th>
      <td>34.278182</td>
      <td>5.679295e+12</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>201</th>
      <th>Martinmouth</th>
      <th>Suburban</th>
      <td>30.498889</td>
      <td>4.656883e+12</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>202</th>
      <th>Port Guytown</th>
      <th>Suburban</th>
      <td>28.242000</td>
      <td>5.108728e+12</td>
      <td>26.0</td>
    </tr>
    <tr>
      <th>203</th>
      <th>New Cindyborough</th>
      <th>Suburban</th>
      <td>31.034615</td>
      <td>5.265153e+12</td>
      <td>20.0</td>
    </tr>
    <tr>
      <th>204</th>
      <th>New Michelleberg</th>
      <th>Suburban</th>
      <td>24.971818</td>
      <td>5.700807e+12</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>205</th>
      <th>North Tracyfort</th>
      <th>Suburban</th>
      <td>26.856000</td>
      <td>4.448434e+12</td>
      <td>18.0</td>
    </tr>
    <tr>
      <th>206</th>
      <th>Tiffanyton</th>
      <th>Suburban</th>
      <td>28.510000</td>
      <td>4.968458e+12</td>
      <td>21.0</td>
    </tr>
    <tr>
      <th>207</th>
      <th>East Cherylfurt</th>
      <th>Suburban</th>
      <td>31.416154</td>
      <td>3.981187e+12</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>208</th>
      <th>Horneland</th>
      <th>Rural</th>
      <td>21.482500</td>
      <td>5.351789e+12</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>209</th>
      <th>Kinghaven</th>
      <th>Rural</th>
      <td>34.980000</td>
      <td>8.157453e+12</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>210</th>
      <th>New Johnbury</th>
      <th>Rural</th>
      <td>35.042500</td>
      <td>7.017742e+12</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>211</th>
      <th>South Joseph</th>
      <th>Rural</th>
      <td>38.983333</td>
      <td>4.374671e+12</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>212</th>
      <th>Kennethburgh</th>
      <th>Rural</th>
      <td>36.928000</td>
      <td>2.920650e+12</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>213</th>
      <th>East Stephen</th>
      <th>Rural</th>
      <td>39.053000</td>
      <td>5.306327e+12</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>214</th>
      <th>Stevensport</th>
      <th>Rural</th>
      <td>31.948000</td>
      <td>3.125721e+12</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>215</th>
      <th>West Kevintown</th>
      <th>Rural</th>
      <td>21.528571</td>
      <td>7.002171e+12</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>216</th>
      <th>East Troybury</th>
      <th>Rural</th>
      <td>33.244286</td>
      <td>5.948234e+12</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>217</th>
      <th>Erikport</th>
      <th>Rural</th>
      <td>30.043750</td>
      <td>6.883015e+12</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>218</th>
      <th>Hernandezshire</th>
      <th>Rural</th>
      <td>32.002222</td>
      <td>5.206210e+12</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>219</th>
      <th>Jacksonfort</th>
      <th>Rural</th>
      <td>32.006667</td>
      <td>4.610855e+12</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>220</th>
      <th>East Leslie</th>
      <th>Rural</th>
      <td>33.660909</td>
      <td>6.051052e+12</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>221</th>
      <th>North Whitney</th>
      <th>Rural</th>
      <td>38.146000</td>
      <td>5.318812e+12</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>222</th>
      <th>Manuelchester</th>
      <th>Rural</th>
      <td>49.620000</td>
      <td>6.045427e+12</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>223</th>
      <th>Shelbyhaven</th>
      <th>Rural</th>
      <td>34.828333</td>
      <td>4.385271e+12</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>224</th>
      <th>South Elizabethmouth</th>
      <th>Rural</th>
      <td>28.698000</td>
      <td>4.747856e+12</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>225</th>
      <th>Matthewside</th>
      <th>Rural</th>
      <td>43.532500</td>
      <td>3.457024e+12</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
<p>125 rows × 3 columns</p>
</div>




```python
averages_per_city = fare_by_city.mean()
```


```python
rural_data = data_with_cityid.loc[(data_with_cityid["type"] == "Rural")]
rural_avg = rural_data.groupby(["city","city id"]).mean()
```


```python
urban_data = data_with_cityid.loc[(data_with_cityid["type"] == "Urban")]
urban_avg = urban_data.groupby(["city","city id"]).mean()
```


```python
suburban_data = data_with_cityid.loc[(data_with_cityid["type"] == "Suburban")]
suburban_avg = suburban_data.groupby(["city","city id"]).mean()
```


```python
avg_fare_per_city = averages_per_city["fare"]
avg_fare_per_city
```




    city id  city                  type    
    101      Sarabury              Urban       23.490000
    102      South Roy             Urban       26.031364
    103      Wiseborough           Urban       22.676842
    104      Spencertown           Urban       23.681154
    105      Nguyenbury            Urban       25.899615
    106      New Jeffrey           Urban       24.130000
    107      Port Johnstad         Urban       25.882941
    108      Jacobfort             Urban       24.779355
    109      Travisville           Urban       27.220870
    110      Sandymouth            Urban       23.105926
    111      New Andreamouth       Urban       24.966786
    112      New Christine         Urban       24.157727
    113      Stewartview           Urban       21.614000
    114      Rodriguezburgh        Urban       21.332609
    115      West Sydneyhaven      Urban       22.368333
    116      Swansonbury           Urban       27.464706
    117      Lisatown              Urban       22.225217
    118      East Erin             Urban       24.478214
    119      Port Martinberg       Urban       22.329524
    120      Edwardsbury           Urban       26.876667
    121      Pamelahaven           Urban       25.549333
    122      Fosterside            Urban       23.034583
    123      West Alexis           Urban       19.523000
    124      Carrollfort           Urban       25.395517
    125      New David             Urban       27.084286
    126      Williamshire          Urban       26.990323
    127      Torresshire           Urban       24.207308
    128      New Aaron             Urban       26.861818
    129      Kelseyland            Urban       21.806429
    130      Lake Sarashire        Urban       26.610000
                                                 ...    
    196      West Evan             Suburban    27.013333
    197      Sarahview             Suburban    33.862000
    198      South Jennifer        Suburban    29.798750
    199      Floresberg            Suburban    32.310000
    200      Williamchester        Suburban    34.278182
    201      Martinmouth           Suburban    30.498889
    202      Port Guytown          Suburban    28.242000
    203      New Cindyborough      Suburban    31.034615
    204      New Michelleberg      Suburban    24.971818
    205      North Tracyfort       Suburban    26.856000
    206      Tiffanyton            Suburban    28.510000
    207      East Cherylfurt       Suburban    31.416154
    208      Horneland             Rural       21.482500
    209      Kinghaven             Rural       34.980000
    210      New Johnbury          Rural       35.042500
    211      South Joseph          Rural       38.983333
    212      Kennethburgh          Rural       36.928000
    213      East Stephen          Rural       39.053000
    214      Stevensport           Rural       31.948000
    215      West Kevintown        Rural       21.528571
    216      East Troybury         Rural       33.244286
    217      Erikport              Rural       30.043750
    218      Hernandezshire        Rural       32.002222
    219      Jacksonfort           Rural       32.006667
    220      East Leslie           Rural       33.660909
    221      North Whitney         Rural       38.146000
    222      Manuelchester         Rural       49.620000
    223      Shelbyhaven           Rural       34.828333
    224      South Elizabethmouth  Rural       28.698000
    225      Matthewside           Rural       43.532500
    Name: fare, Length: 125, dtype: float64




```python
total_rides_per_city = data_with_cityid["city"].value_counts()
```


```python
total_rides_per_urban_city = urban_data["city"].value_counts()
total_rides_per_rural_city = rural_data["city"].value_counts()
total_rides_per_suburban_city = suburban_data["city"].value_counts()
```


```python
avg_fare_per_urban_city = urban_avg['fare']
avg_fare_per_suburban_city = suburban_avg['fare']
avg_fare_per_rural_city = rural_avg['fare']
```


```python
Suburban = plt.scatter(total_rides_per_suburban_city, avg_fare_per_suburban_city, marker="o", facecolors="lightskyblue", edgecolors="black", alpha= 0.8)
Urban = plt.scatter(total_rides_per_urban_city, avg_fare_per_urban_city, marker="o", color="lightcoral", edgecolors="black", alpha= 0.8)
Rural = plt.scatter(total_rides_per_rural_city, avg_fare_per_rural_city,  marker="o", color="gold", edgecolors="black", alpha= 0.8)
```


```python
#idk why my legend is incorrect
plt.grid()
plt.ylim(0,55)
plt.xlim(0,70)
plt.title("Pyber Ride Sharing Data (2016)")
plt.xlabel("Total Number of Rides (Per City)")
plt.ylabel("Average Fare ($)")
plt.scatter(total_rides_per_suburban_city, avg_fare_per_suburban_city, s= suburban_avg['driver_count']*10, marker="o",label="Suburban", facecolors="lightskyblue", edgecolors="black", alpha= 0.8)
plt.scatter(total_rides_per_urban_city, avg_fare_per_urban_city, s= urban_avg['driver_count']*10, marker="o",label="Urban", color="lightcoral", edgecolors="black", alpha= 0.8)
plt.scatter(total_rides_per_rural_city, avg_fare_per_rural_city, s= rural_avg['driver_count']*10, marker="o",label="Rural", color="gold", edgecolors="black", alpha= 0.8)
plt.legend(handles=[Urban, Suburban, Rural],loc='lower right', fancybox=True, framealpha=0)
plt.savefig("PyberBubbleChart.png")
plt.show()
```


![png](output_15_0.png)



```python
suburban_drivers = suburban_avg["driver_count"].sum()
urban_drivers = urban_avg["driver_count"].sum()
rural_drivers = rural_avg["driver_count"].sum()
```


```python
suburban_fares = suburban_data["fare"].sum()
urban_fares = urban_data["fare"].sum()
rural_fares = rural_data["fare"].sum()
```


```python
urban_rides = len(urban_data)
rural_rides = len(rural_data)
suburban_rides = len(suburban_data)
```


```python
#pie by driver type
pie_labels = ["Rural","Urban","Suburban"]
drivers_by_type = [rural_drivers, urban_drivers, suburban_drivers]
colors= ["gold", "lightcoral", "lightskyblue"]
explode = (0, 0.1, 0)
plt.title("% of Drivers By City Type")
plt.pie(drivers_by_type, explode=explode, labels=pie_labels, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=202)
plt.axis("equal")
plt.savefig("PyberDriversByType.png")
plt.show()
```


![png](output_19_0.png)



```python
rides_by_type = [rural_rides, urban_rides, suburban_rides]
colors= ["gold", "lightcoral", "lightskyblue"]
explode = (0, 0.1, 0)
plt.title("% of Rides By City Type")
plt.pie(rides_by_type, explode=explode, labels=pie_labels, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=215)
plt.axis("equal")
plt.savefig("PyberRidersByType.png")
plt.show()
```


![png](output_20_0.png)



```python
fares_by_type = [rural_fares, urban_fares, suburban_fares]
colors= ["gold", "lightcoral", "lightskyblue"]
explode = (0, 0.1, 0)
plt.title("% of Fares By City Type")
plt.pie(fares_by_type, explode=explode, labels=pie_labels, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=220)
plt.axis("equal")
plt.savefig("PyberFaresByType.png")
plt.show()
```


![png](output_21_0.png)

Analysis:
Rural cities have the least drivers therefore resulting in a surge in prices of Pyber rides.
Urban cities have the most drivers therefore resulting in them owning the largest share of Pyber Revenue by city type.
The more drivers a city has the cheaper the Pyber price per ride will be.
