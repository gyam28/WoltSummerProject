

```python
import pandas as pd
import numpy as np
```

# 1. Reading the file data. #
## Note: in case of updating the file, the name has to be adjusted. ##


```python
pickupT=pd.read_csv("pickup_times.csv")
pickupT.head(10)

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>location_id</th>
      <th>iso_8601_timestamp</th>
      <th>pickup_time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>2019-01-13T19:32:53Z</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1</th>
      <td>55</td>
      <td>2019-01-13T18:12:20Z</td>
      <td>37</td>
    </tr>
    <tr>
      <th>2</th>
      <td>73</td>
      <td>2019-01-10T18:13:26Z</td>
      <td>33</td>
    </tr>
    <tr>
      <th>3</th>
      <td>46</td>
      <td>2019-01-13T19:34:42Z</td>
      <td>33</td>
    </tr>
    <tr>
      <th>4</th>
      <td>59</td>
      <td>2019-01-08T16:11:42Z</td>
      <td>21</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30</td>
      <td>2019-01-12T16:59:40Z</td>
      <td>27</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28</td>
      <td>2019-01-07T18:39:47Z</td>
      <td>43</td>
    </tr>
    <tr>
      <th>7</th>
      <td>51</td>
      <td>2019-01-13T19:40:31Z</td>
      <td>11</td>
    </tr>
    <tr>
      <th>8</th>
      <td>27</td>
      <td>2019-01-08T10:24:19Z</td>
      <td>23</td>
    </tr>
    <tr>
      <th>9</th>
      <td>35</td>
      <td>2019-01-09T11:31:27Z</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>



# 2. Splitting the date and hour from column iso_8601_timestamp and redistributing the data #


```python
pickupT["Date"] = [timestamp.split("T")[0] for timestamp in pickupT["iso_8601_timestamp"]]
pickupT["Hour"] = [timestamp.split("T")[-1] for timestamp in pickupT["iso_8601_timestamp"]]
pickupT["Hour"] = [timestamp.split("Z")[0] for timestamp in pickupT["Hour"]]
pickupT.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>location_id</th>
      <th>iso_8601_timestamp</th>
      <th>pickup_time</th>
      <th>Date</th>
      <th>Hour</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>2019-01-13T19:32:53Z</td>
      <td>20</td>
      <td>2019-01-13</td>
      <td>19:32:53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>55</td>
      <td>2019-01-13T18:12:20Z</td>
      <td>37</td>
      <td>2019-01-13</td>
      <td>18:12:20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>73</td>
      <td>2019-01-10T18:13:26Z</td>
      <td>33</td>
      <td>2019-01-10</td>
      <td>18:13:26</td>
    </tr>
    <tr>
      <th>3</th>
      <td>46</td>
      <td>2019-01-13T19:34:42Z</td>
      <td>33</td>
      <td>2019-01-13</td>
      <td>19:34:42</td>
    </tr>
    <tr>
      <th>4</th>
      <td>59</td>
      <td>2019-01-08T16:11:42Z</td>
      <td>21</td>
      <td>2019-01-08</td>
      <td>16:11:42</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30</td>
      <td>2019-01-12T16:59:40Z</td>
      <td>27</td>
      <td>2019-01-12</td>
      <td>16:59:40</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28</td>
      <td>2019-01-07T18:39:47Z</td>
      <td>43</td>
      <td>2019-01-07</td>
      <td>18:39:47</td>
    </tr>
    <tr>
      <th>7</th>
      <td>51</td>
      <td>2019-01-13T19:40:31Z</td>
      <td>11</td>
      <td>2019-01-13</td>
      <td>19:40:31</td>
    </tr>
    <tr>
      <th>8</th>
      <td>27</td>
      <td>2019-01-08T10:24:19Z</td>
      <td>23</td>
      <td>2019-01-08</td>
      <td>10:24:19</td>
    </tr>
    <tr>
      <th>9</th>
      <td>35</td>
      <td>2019-01-09T11:31:27Z</td>
      <td>14</td>
      <td>2019-01-09</td>
      <td>11:31:27</td>
    </tr>
  </tbody>
</table>
</div>




```python
pickupT.drop('iso_8601_timestamp', axis=1, inplace=True)
pickupT.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>location_id</th>
      <th>pickup_time</th>
      <th>Date</th>
      <th>Hour</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>20</td>
      <td>2019-01-13</td>
      <td>19:32:53</td>
    </tr>
    <tr>
      <th>1</th>
      <td>55</td>
      <td>37</td>
      <td>2019-01-13</td>
      <td>18:12:20</td>
    </tr>
    <tr>
      <th>2</th>
      <td>73</td>
      <td>33</td>
      <td>2019-01-10</td>
      <td>18:13:26</td>
    </tr>
    <tr>
      <th>3</th>
      <td>46</td>
      <td>33</td>
      <td>2019-01-13</td>
      <td>19:34:42</td>
    </tr>
    <tr>
      <th>4</th>
      <td>59</td>
      <td>21</td>
      <td>2019-01-08</td>
      <td>16:11:42</td>
    </tr>
    <tr>
      <th>5</th>
      <td>30</td>
      <td>27</td>
      <td>2019-01-12</td>
      <td>16:59:40</td>
    </tr>
    <tr>
      <th>6</th>
      <td>28</td>
      <td>43</td>
      <td>2019-01-07</td>
      <td>18:39:47</td>
    </tr>
    <tr>
      <th>7</th>
      <td>51</td>
      <td>11</td>
      <td>2019-01-13</td>
      <td>19:40:31</td>
    </tr>
    <tr>
      <th>8</th>
      <td>27</td>
      <td>23</td>
      <td>2019-01-08</td>
      <td>10:24:19</td>
    </tr>
    <tr>
      <th>9</th>
      <td>35</td>
      <td>14</td>
      <td>2019-01-09</td>
      <td>11:31:27</td>
    </tr>
  </tbody>
</table>
</div>



# 3. Organizing ascendingly the content data #


```python
pickupT.sort_values(["location_id","Date","Hour"], axis=0, 
                 ascending=True, inplace=True)
pickupT
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>location_id</th>
      <th>pickup_time</th>
      <th>Date</th>
      <th>Hour</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>15865</th>
      <td>1</td>
      <td>25</td>
      <td>2019-01-07</td>
      <td>10:00:40</td>
    </tr>
    <tr>
      <th>18789</th>
      <td>1</td>
      <td>23</td>
      <td>2019-01-07</td>
      <td>10:02:54</td>
    </tr>
    <tr>
      <th>6870</th>
      <td>1</td>
      <td>31</td>
      <td>2019-01-07</td>
      <td>10:11:04</td>
    </tr>
    <tr>
      <th>45133</th>
      <td>1</td>
      <td>16</td>
      <td>2019-01-07</td>
      <td>10:12:56</td>
    </tr>
    <tr>
      <th>33459</th>
      <td>1</td>
      <td>20</td>
      <td>2019-01-07</td>
      <td>10:13:25</td>
    </tr>
    <tr>
      <th>42273</th>
      <td>1</td>
      <td>20</td>
      <td>2019-01-07</td>
      <td>10:14:19</td>
    </tr>
    <tr>
      <th>38828</th>
      <td>1</td>
      <td>16</td>
      <td>2019-01-07</td>
      <td>10:14:22</td>
    </tr>
    <tr>
      <th>42495</th>
      <td>1</td>
      <td>24</td>
      <td>2019-01-07</td>
      <td>10:21:21</td>
    </tr>
    <tr>
      <th>16596</th>
      <td>1</td>
      <td>20</td>
      <td>2019-01-07</td>
      <td>10:26:37</td>
    </tr>
    <tr>
      <th>15344</th>
      <td>1</td>
      <td>26</td>
      <td>2019-01-07</td>
      <td>10:33:55</td>
    </tr>
    <tr>
      <th>4733</th>
      <td>1</td>
      <td>23</td>
      <td>2019-01-07</td>
      <td>10:34:36</td>
    </tr>
    <tr>
      <th>35053</th>
      <td>1</td>
      <td>28</td>
      <td>2019-01-07</td>
      <td>10:34:50</td>
    </tr>
    <tr>
      <th>64069</th>
      <td>1</td>
      <td>23</td>
      <td>2019-01-07</td>
      <td>10:37:24</td>
    </tr>
    <tr>
      <th>3626</th>
      <td>1</td>
      <td>34</td>
      <td>2019-01-07</td>
      <td>10:37:32</td>
    </tr>
    <tr>
      <th>49227</th>
      <td>1</td>
      <td>30</td>
      <td>2019-01-07</td>
      <td>10:39:02</td>
    </tr>
    <tr>
      <th>27662</th>
      <td>1</td>
      <td>16</td>
      <td>2019-01-07</td>
      <td>10:39:11</td>
    </tr>
    <tr>
      <th>50494</th>
      <td>1</td>
      <td>15</td>
      <td>2019-01-07</td>
      <td>10:40:04</td>
    </tr>
    <tr>
      <th>44502</th>
      <td>1</td>
      <td>22</td>
      <td>2019-01-07</td>
      <td>10:43:14</td>
    </tr>
    <tr>
      <th>52145</th>
      <td>1</td>
      <td>32</td>
      <td>2019-01-07</td>
      <td>10:50:46</td>
    </tr>
    <tr>
      <th>41984</th>
      <td>1</td>
      <td>25</td>
      <td>2019-01-07</td>
      <td>10:52:33</td>
    </tr>
    <tr>
      <th>8830</th>
      <td>1</td>
      <td>15</td>
      <td>2019-01-07</td>
      <td>10:52:52</td>
    </tr>
    <tr>
      <th>28970</th>
      <td>1</td>
      <td>20</td>
      <td>2019-01-07</td>
      <td>10:53:54</td>
    </tr>
    <tr>
      <th>51066</th>
      <td>1</td>
      <td>19</td>
      <td>2019-01-07</td>
      <td>10:54:32</td>
    </tr>
    <tr>
      <th>6428</th>
      <td>1</td>
      <td>15</td>
      <td>2019-01-07</td>
      <td>10:55:24</td>
    </tr>
    <tr>
      <th>55708</th>
      <td>1</td>
      <td>23</td>
      <td>2019-01-07</td>
      <td>11:01:54</td>
    </tr>
    <tr>
      <th>33274</th>
      <td>1</td>
      <td>21</td>
      <td>2019-01-07</td>
      <td>11:09:05</td>
    </tr>
    <tr>
      <th>63755</th>
      <td>1</td>
      <td>24</td>
      <td>2019-01-07</td>
      <td>11:12:13</td>
    </tr>
    <tr>
      <th>19214</th>
      <td>1</td>
      <td>17</td>
      <td>2019-01-07</td>
      <td>11:13:20</td>
    </tr>
    <tr>
      <th>7648</th>
      <td>1</td>
      <td>20</td>
      <td>2019-01-07</td>
      <td>11:14:50</td>
    </tr>
    <tr>
      <th>34851</th>
      <td>1</td>
      <td>29</td>
      <td>2019-01-07</td>
      <td>11:15:07</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1412</th>
      <td>85</td>
      <td>10</td>
      <td>2019-01-13</td>
      <td>18:33:53</td>
    </tr>
    <tr>
      <th>63217</th>
      <td>85</td>
      <td>33</td>
      <td>2019-01-13</td>
      <td>18:35:28</td>
    </tr>
    <tr>
      <th>52633</th>
      <td>85</td>
      <td>23</td>
      <td>2019-01-13</td>
      <td>18:38:46</td>
    </tr>
    <tr>
      <th>54853</th>
      <td>85</td>
      <td>20</td>
      <td>2019-01-13</td>
      <td>18:43:12</td>
    </tr>
    <tr>
      <th>33587</th>
      <td>85</td>
      <td>20</td>
      <td>2019-01-13</td>
      <td>18:43:16</td>
    </tr>
    <tr>
      <th>54821</th>
      <td>85</td>
      <td>21</td>
      <td>2019-01-13</td>
      <td>18:43:47</td>
    </tr>
    <tr>
      <th>61600</th>
      <td>85</td>
      <td>20</td>
      <td>2019-01-13</td>
      <td>18:45:17</td>
    </tr>
    <tr>
      <th>9818</th>
      <td>85</td>
      <td>13</td>
      <td>2019-01-13</td>
      <td>18:50:55</td>
    </tr>
    <tr>
      <th>18030</th>
      <td>85</td>
      <td>18</td>
      <td>2019-01-13</td>
      <td>18:52:55</td>
    </tr>
    <tr>
      <th>63823</th>
      <td>85</td>
      <td>26</td>
      <td>2019-01-13</td>
      <td>18:53:58</td>
    </tr>
    <tr>
      <th>63440</th>
      <td>85</td>
      <td>23</td>
      <td>2019-01-13</td>
      <td>18:55:01</td>
    </tr>
    <tr>
      <th>64889</th>
      <td>85</td>
      <td>25</td>
      <td>2019-01-13</td>
      <td>19:02:09</td>
    </tr>
    <tr>
      <th>4817</th>
      <td>85</td>
      <td>19</td>
      <td>2019-01-13</td>
      <td>19:16:46</td>
    </tr>
    <tr>
      <th>18081</th>
      <td>85</td>
      <td>31</td>
      <td>2019-01-13</td>
      <td>19:18:41</td>
    </tr>
    <tr>
      <th>62423</th>
      <td>85</td>
      <td>23</td>
      <td>2019-01-13</td>
      <td>19:19:39</td>
    </tr>
    <tr>
      <th>8607</th>
      <td>85</td>
      <td>14</td>
      <td>2019-01-13</td>
      <td>19:23:17</td>
    </tr>
    <tr>
      <th>17630</th>
      <td>85</td>
      <td>33</td>
      <td>2019-01-13</td>
      <td>19:24:43</td>
    </tr>
    <tr>
      <th>43008</th>
      <td>85</td>
      <td>19</td>
      <td>2019-01-13</td>
      <td>19:26:02</td>
    </tr>
    <tr>
      <th>27528</th>
      <td>85</td>
      <td>32</td>
      <td>2019-01-13</td>
      <td>19:31:07</td>
    </tr>
    <tr>
      <th>17129</th>
      <td>85</td>
      <td>33</td>
      <td>2019-01-13</td>
      <td>19:36:27</td>
    </tr>
    <tr>
      <th>59544</th>
      <td>85</td>
      <td>15</td>
      <td>2019-01-13</td>
      <td>19:40:13</td>
    </tr>
    <tr>
      <th>26202</th>
      <td>85</td>
      <td>16</td>
      <td>2019-01-13</td>
      <td>19:41:37</td>
    </tr>
    <tr>
      <th>24163</th>
      <td>85</td>
      <td>13</td>
      <td>2019-01-13</td>
      <td>19:44:10</td>
    </tr>
    <tr>
      <th>53555</th>
      <td>85</td>
      <td>34</td>
      <td>2019-01-13</td>
      <td>19:46:45</td>
    </tr>
    <tr>
      <th>42171</th>
      <td>85</td>
      <td>16</td>
      <td>2019-01-13</td>
      <td>19:49:03</td>
    </tr>
    <tr>
      <th>61255</th>
      <td>85</td>
      <td>15</td>
      <td>2019-01-13</td>
      <td>19:50:19</td>
    </tr>
    <tr>
      <th>22241</th>
      <td>85</td>
      <td>19</td>
      <td>2019-01-13</td>
      <td>19:51:00</td>
    </tr>
    <tr>
      <th>26553</th>
      <td>85</td>
      <td>17</td>
      <td>2019-01-13</td>
      <td>19:55:21</td>
    </tr>
    <tr>
      <th>59180</th>
      <td>85</td>
      <td>19</td>
      <td>2019-01-13</td>
      <td>19:55:45</td>
    </tr>
    <tr>
      <th>41956</th>
      <td>85</td>
      <td>36</td>
      <td>2019-01-13</td>
      <td>19:55:51</td>
    </tr>
  </tbody>
</table>
<p>65380 rows × 4 columns</p>
</div>



# 4. Organizing the generalized median calculation and testing of it #


```python
queryDay = "2019-01-13"
queryTime = "10:00:00"
queryTime2 = "11:00:00"
sortedlist=pickupT.loc[(pickupT["Date"]==queryDay) & (pickupT["Hour"]>=queryTime) &(pickupT["Hour"]<queryTime2)].groupby('location_id').median()

```


```python
sortedlist
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pickup_time</th>
    </tr>
    <tr>
      <th>location_id</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>10.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>13.5</td>
    </tr>
    <tr>
      <th>7</th>
      <td>17.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>16.5</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10.5</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12.5</td>
    </tr>
    <tr>
      <th>13</th>
      <td>11.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>11.5</td>
    </tr>
    <tr>
      <th>15</th>
      <td>13.0</td>
    </tr>
    <tr>
      <th>16</th>
      <td>12.5</td>
    </tr>
    <tr>
      <th>17</th>
      <td>13.0</td>
    </tr>
    <tr>
      <th>18</th>
      <td>16.0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>10.5</td>
    </tr>
    <tr>
      <th>20</th>
      <td>10.0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>14.5</td>
    </tr>
    <tr>
      <th>22</th>
      <td>11.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>15.0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>13.0</td>
    </tr>
    <tr>
      <th>25</th>
      <td>10.0</td>
    </tr>
    <tr>
      <th>26</th>
      <td>13.0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>9.5</td>
    </tr>
    <tr>
      <th>28</th>
      <td>8.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>12.0</td>
    </tr>
    <tr>
      <th>30</th>
      <td>10.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>56</th>
      <td>35.0</td>
    </tr>
    <tr>
      <th>57</th>
      <td>20.0</td>
    </tr>
    <tr>
      <th>58</th>
      <td>18.5</td>
    </tr>
    <tr>
      <th>59</th>
      <td>20.0</td>
    </tr>
    <tr>
      <th>60</th>
      <td>21.5</td>
    </tr>
    <tr>
      <th>61</th>
      <td>14.0</td>
    </tr>
    <tr>
      <th>62</th>
      <td>20.0</td>
    </tr>
    <tr>
      <th>63</th>
      <td>17.5</td>
    </tr>
    <tr>
      <th>64</th>
      <td>15.0</td>
    </tr>
    <tr>
      <th>65</th>
      <td>14.0</td>
    </tr>
    <tr>
      <th>66</th>
      <td>16.0</td>
    </tr>
    <tr>
      <th>67</th>
      <td>22.0</td>
    </tr>
    <tr>
      <th>68</th>
      <td>21.0</td>
    </tr>
    <tr>
      <th>69</th>
      <td>19.5</td>
    </tr>
    <tr>
      <th>70</th>
      <td>20.0</td>
    </tr>
    <tr>
      <th>71</th>
      <td>15.0</td>
    </tr>
    <tr>
      <th>72</th>
      <td>20.0</td>
    </tr>
    <tr>
      <th>73</th>
      <td>20.0</td>
    </tr>
    <tr>
      <th>74</th>
      <td>23.0</td>
    </tr>
    <tr>
      <th>75</th>
      <td>19.0</td>
    </tr>
    <tr>
      <th>76</th>
      <td>17.0</td>
    </tr>
    <tr>
      <th>77</th>
      <td>21.0</td>
    </tr>
    <tr>
      <th>78</th>
      <td>20.0</td>
    </tr>
    <tr>
      <th>79</th>
      <td>13.0</td>
    </tr>
    <tr>
      <th>80</th>
      <td>11.0</td>
    </tr>
    <tr>
      <th>81</th>
      <td>18.0</td>
    </tr>
    <tr>
      <th>82</th>
      <td>20.0</td>
    </tr>
    <tr>
      <th>83</th>
      <td>12.0</td>
    </tr>
    <tr>
      <th>84</th>
      <td>16.0</td>
    </tr>
    <tr>
      <th>85</th>
      <td>18.0</td>
    </tr>
  </tbody>
</table>
<p>85 rows × 1 columns</p>
</div>



# 5. Setting up the GUI interface with date and hour picking options #


```python
from __future__ import print_function
from ipywidgets import interact, interactive, fixed, interact_manual
import ipywidgets as widgets
```


```python
datePicker = widgets.DatePicker(
    description='Pick a Date between 07 Jan and 13 Jan 2019',
    disabled=False
)
display(datePicker)

```


    DatePicker(value=None, description='Pick a Date between 07 Jan and 13 Jan 2019')



```python
rawDate = datePicker.value
month = str(rawDate.month)
if len(str(rawDate.month)) < 2:
    month = "0" + month

day = str(rawDate.day)
if len(str(rawDate.day)) < 2:
    day = "0" + day


queryDate = "" + str(rawDate.year) + "-" + month + "-" + day
queryDate
```




    '2019-01-13'




```python
hours = [("0" + str(i)) if len(str(i)) < 2 else str(i) for i in range(0,24)]
options = [str(i) for i in hours]
hourPicker = widgets.SelectionRangeSlider(
    options=options,
    index=(0,23),
    description='Hours',
    disabled=False
)
display(hourPicker)
```


    SelectionRangeSlider(description='Hours', index=(0, 23), options=('00', '01', '02', '03', '04', '05', '06', '0…



```python
hourPicker.value
startHour = hourPicker.value[0] + ":00:00"
endHour = hourPicker.value[1] + ":00:00"

```


```python
sortedList=pickupT.loc[(pickupT["Date"]==queryDate) & (pickupT["Hour"]>=startHour) &(pickupT["Hour"]<endHour)].groupby('location_id').median()
sortedList.head(10)


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>pickup_time</th>
    </tr>
    <tr>
      <th>location_id</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>10.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>11.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>15.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>16.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>7.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>13.5</td>
    </tr>
    <tr>
      <th>7</th>
      <td>17.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>16.5</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10.5</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python

```
