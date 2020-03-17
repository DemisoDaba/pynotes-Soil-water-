# Coronavirus COVID-19 Timeseries of Global Cases

The recent outbreak of Coronavirus demonstrates how quickly a threatening disease can spread around the world due to human travel and migration and it shows that we might not be well preapre for a  

The Center for Sytems Science and Engineering (https://systems.jhu.edu/research/public-health/ncov/) at John Hopkins University has generated a dashboard for real-time tracking of confirmed infected cases, recovered cases, and deaths. The data originates from different non-profit and governmental sources and a curated lists of cases by day is available through Github.

In this assignment I would like you to retrieve the same dataset using the Pandas module and then create a figure that shows the timeseries of total number of confirmed cases, recovered cases, and deaths similar to that in the dashboard.


## Goal

Your goal is to replicate the figure below to the best of your abilities. Do not worry about the specific font size and line width. You will learn how to fine-tune more figure attributes in a later class. For now, focus on the basics.


## Steps to obtain data

- Step 1: Go to https://systems.jhu.edu/research/public-health/ncov/

- Step 2: Click on the Coronavirus dashboard

- Step 3: At the bottom of the dashboard go to the Github repository: **Downloadable database: GitHub: Here.**

- Step 4: Click on **csse_covid_19_data**

- Step 5: Click on **csse_covid_19_time_series**


>Just in case, here is the direct link: <https://github.com/CSSEGISandData/COVID-19/tree/master/csse_covid_19_data/csse_covid_19_time_series>




```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

```


```python
# Load data from John Hopkins University
df_infected = pd.read_csv("https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_19-covid-Confirmed.csv")
df_deaths = pd.read_csv("https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_19-covid-Deaths.csv")
df_recovered = pd.read_csv("https://raw.githubusercontent.com/CSSEGISandData/COVID-19/master/csse_covid_19_data/csse_covid_19_time_series/time_series_19-covid-Recovered.csv")

```


```python
# Print Infected
df_infected.head()
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
      <th>Province/State</th>
      <th>Country/Region</th>
      <th>Lat</th>
      <th>Long</th>
      <th>1/22/20</th>
      <th>1/23/20</th>
      <th>1/24/20</th>
      <th>1/25/20</th>
      <th>1/26/20</th>
      <th>1/27/20</th>
      <th>...</th>
      <th>2/23/20</th>
      <th>2/24/20</th>
      <th>2/25/20</th>
      <th>2/26/20</th>
      <th>2/27/20</th>
      <th>2/28/20</th>
      <th>2/29/20</th>
      <th>3/1/20</th>
      <th>3/2/20</th>
      <th>3/3/20</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Anhui</td>
      <td>Mainland China</td>
      <td>31.8257</td>
      <td>117.2264</td>
      <td>1</td>
      <td>9</td>
      <td>15</td>
      <td>39</td>
      <td>60</td>
      <td>70</td>
      <td>...</td>
      <td>989</td>
      <td>989</td>
      <td>989</td>
      <td>989</td>
      <td>989</td>
      <td>990</td>
      <td>990</td>
      <td>990</td>
      <td>990</td>
      <td>990</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Beijing</td>
      <td>Mainland China</td>
      <td>40.1824</td>
      <td>116.4142</td>
      <td>14</td>
      <td>22</td>
      <td>36</td>
      <td>41</td>
      <td>68</td>
      <td>80</td>
      <td>...</td>
      <td>399</td>
      <td>399</td>
      <td>400</td>
      <td>400</td>
      <td>410</td>
      <td>410</td>
      <td>411</td>
      <td>413</td>
      <td>414</td>
      <td>414</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chongqing</td>
      <td>Mainland China</td>
      <td>30.0572</td>
      <td>107.8740</td>
      <td>6</td>
      <td>9</td>
      <td>27</td>
      <td>57</td>
      <td>75</td>
      <td>110</td>
      <td>...</td>
      <td>575</td>
      <td>576</td>
      <td>576</td>
      <td>576</td>
      <td>576</td>
      <td>576</td>
      <td>576</td>
      <td>576</td>
      <td>576</td>
      <td>576</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Fujian</td>
      <td>Mainland China</td>
      <td>26.0789</td>
      <td>117.9874</td>
      <td>1</td>
      <td>5</td>
      <td>10</td>
      <td>18</td>
      <td>35</td>
      <td>59</td>
      <td>...</td>
      <td>293</td>
      <td>293</td>
      <td>294</td>
      <td>294</td>
      <td>296</td>
      <td>296</td>
      <td>296</td>
      <td>296</td>
      <td>296</td>
      <td>296</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Gansu</td>
      <td>Mainland China</td>
      <td>36.0611</td>
      <td>103.8343</td>
      <td>0</td>
      <td>2</td>
      <td>2</td>
      <td>4</td>
      <td>7</td>
      <td>14</td>
      <td>...</td>
      <td>91</td>
      <td>91</td>
      <td>91</td>
      <td>91</td>
      <td>91</td>
      <td>91</td>
      <td>91</td>
      <td>91</td>
      <td>91</td>
      <td>91</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 46 columns</p>
</div>




```python
# Print deaths
df_deaths.head()
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
      <th>Province/State</th>
      <th>Country/Region</th>
      <th>Lat</th>
      <th>Long</th>
      <th>1/22/20</th>
      <th>1/23/20</th>
      <th>1/24/20</th>
      <th>1/25/20</th>
      <th>1/26/20</th>
      <th>1/27/20</th>
      <th>...</th>
      <th>2/23/20</th>
      <th>2/24/20</th>
      <th>2/25/20</th>
      <th>2/26/20</th>
      <th>2/27/20</th>
      <th>2/28/20</th>
      <th>2/29/20</th>
      <th>3/1/20</th>
      <th>3/2/20</th>
      <th>3/3/20</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Anhui</td>
      <td>Mainland China</td>
      <td>31.8257</td>
      <td>117.2264</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Beijing</td>
      <td>Mainland China</td>
      <td>40.1824</td>
      <td>116.4142</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>...</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>4</td>
      <td>5</td>
      <td>7</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chongqing</td>
      <td>Mainland China</td>
      <td>30.0572</td>
      <td>107.8740</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Fujian</td>
      <td>Mainland China</td>
      <td>26.0789</td>
      <td>117.9874</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Gansu</td>
      <td>Mainland China</td>
      <td>36.0611</td>
      <td>103.8343</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 46 columns</p>
</div>




```python
# Print Recovered
df_recovered.head()
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
      <th>Province/State</th>
      <th>Country/Region</th>
      <th>Lat</th>
      <th>Long</th>
      <th>1/22/20</th>
      <th>1/23/20</th>
      <th>1/24/20</th>
      <th>1/25/20</th>
      <th>1/26/20</th>
      <th>1/27/20</th>
      <th>...</th>
      <th>2/23/20</th>
      <th>2/24/20</th>
      <th>2/25/20</th>
      <th>2/26/20</th>
      <th>2/27/20</th>
      <th>2/28/20</th>
      <th>2/29/20</th>
      <th>3/1/20</th>
      <th>3/2/20</th>
      <th>3/3/20</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Anhui</td>
      <td>Mainland China</td>
      <td>31.8257</td>
      <td>117.2264</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>637</td>
      <td>663</td>
      <td>712</td>
      <td>744</td>
      <td>792</td>
      <td>821</td>
      <td>868</td>
      <td>873</td>
      <td>917</td>
      <td>936</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Beijing</td>
      <td>Mainland China</td>
      <td>40.1824</td>
      <td>116.4142</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>...</td>
      <td>189</td>
      <td>198</td>
      <td>215</td>
      <td>235</td>
      <td>248</td>
      <td>257</td>
      <td>271</td>
      <td>276</td>
      <td>282</td>
      <td>288</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chongqing</td>
      <td>Mainland China</td>
      <td>30.0572</td>
      <td>107.8740</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>335</td>
      <td>349</td>
      <td>372</td>
      <td>384</td>
      <td>401</td>
      <td>422</td>
      <td>438</td>
      <td>450</td>
      <td>469</td>
      <td>490</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Fujian</td>
      <td>Mainland China</td>
      <td>26.0789</td>
      <td>117.9874</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>170</td>
      <td>183</td>
      <td>199</td>
      <td>218</td>
      <td>228</td>
      <td>235</td>
      <td>243</td>
      <td>247</td>
      <td>255</td>
      <td>260</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Gansu</td>
      <td>Mainland China</td>
      <td>36.0611</td>
      <td>103.8343</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>78</td>
      <td>80</td>
      <td>80</td>
      <td>81</td>
      <td>81</td>
      <td>82</td>
      <td>82</td>
      <td>84</td>
      <td>85</td>
      <td>86</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 46 columns</p>
</div>




```python
# Compute totals
total_infected = df_infected.iloc[:,4:].sum()
total_deaths = df_deaths.iloc[:,4:].sum()
total_recovered = df_recovered.iloc[:,4:].sum()

```


```python
dates_infected = pd.to_datetime(total_infected.index)
dates_deaths = pd.to_datetime(total_deaths.index)
dates_recovered = pd.to_datetime(total_recovered.index)

# Alternative
#dates = df_infected.columns[4:]
#dates = pd.to_datetime(dates)
#dates
```


```python
plt.figure(figsize=(12,8))
plt.title("Coronavirus Timeseries", size=20)
plt.plot(dates_infected,total_infected,'--y', label="Infected")
plt.plot(dates_deaths,total_deaths,'.r', label="Deaths")
plt.plot(dates_recovered,total_recovered,'-g', label="Recovered")
plt.ylabel('People', size=18)
plt.legend()
plt.xticks(fontsize=14, rotation=20)
plt.yticks(fontsize=14)
#plt.savefig("coronavirus_timeseries_25_feb_2020", dpi=fig.dpi)
plt.show()

```


![png](coronavirus_files/coronavirus_8_0.png)



```python
# Plot US cases
idx_US = df_infected["Country/Region"] == "US"
us_infected = df_infected.loc[idx_US].sum()
us_infected[4:]
```




    1/22/20      1
    1/23/20      1
    1/24/20      2
    1/25/20      2
    1/26/20      5
    1/27/20      5
    1/28/20      5
    1/29/20      5
    1/30/20      5
    1/31/20      7
    2/1/20       8
    2/2/20       8
    2/3/20      11
    2/4/20      11
    2/5/20      12
    2/6/20      12
    2/7/20      12
    2/8/20      12
    2/9/20      12
    2/10/20     12
    2/11/20     13
    2/12/20     13
    2/13/20     15
    2/14/20     15
    2/15/20     15
    2/16/20     15
    2/17/20     15
    2/18/20     15
    2/19/20     15
    2/20/20     15
    2/21/20     35
    2/22/20     35
    2/23/20     35
    2/24/20     53
    2/25/20     53
    2/26/20     59
    2/27/20     60
    2/28/20     62
    2/29/20     70
    3/1/20      76
    3/2/20     101
    3/3/20     122
    dtype: object




```python
# Compute change in infected people
change_infected = np.diff(total_infected.values)

```


```python
plt.figure(figsize=(12,8))
plt.title('Infected Trend', size=20)
plt.plot(dates_infected[1:],change_infected,'-y')
plt.ylabel('Change in infected people', size=18)
plt.show()
```


![png](coronavirus_files/coronavirus_11_0.png)


## Interactive map using the Plotly library

Plotly is not installed in the Anaconda package, but it can be installed suing the `conda` command in the terminal: `conda install -c plotly plotly=4.5.2

To render Plotly charts in the Jupyter Lab you also need another library called `ipywidgets`, which can also be installed using `conda` as follows: `conda install "notebook>=5.3" "ipywidgets>=7.2"`

> You may need to restart your kernel or the entire Jupyter Lab in order to render the new plots from the Plotly library.

You can find out more infromation about installing Plotly here: https://plot.ly/python/getting-started/


```python
# A simple map showing the confirmed cases of coronavirus for a specific date.
import plotly.express as px
fig = px.scatter_geo(df_infected, lon="Long", lat="Lat", size="3/3/20")
fig.show()

```


<div>


            <div id="be7d9ab1-f2fb-49fa-87ae-7309c21c2bd2" class="plotly-graph-div" style="height:525px; width:100%;"></div>
            <script type="text/javascript">
                require(["plotly"], function(Plotly) {
                    window.PLOTLYENV=window.PLOTLYENV || {};

                if (document.getElementById("be7d9ab1-f2fb-49fa-87ae-7309c21c2bd2")) {
                    Plotly.newPlot(
                        'be7d9ab1-f2fb-49fa-87ae-7309c21c2bd2',
                        [{"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "3/3/20=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "lat": [31.8257, 40.1824, 30.0572, 26.0789, 36.0611, 23.3417, 23.8298, 26.8154, 19.1959, 38.0428, 47.861999999999995, 33.882020000000004, 30.9756, 27.6104, 44.0935, 32.9711, 27.614, 43.6661, 41.2956, 37.2692, 35.7452, 35.1917, 36.3427, 31.201999999999998, 37.5777, 30.6171, 39.3054, 31.6927, 41.1129, 24.974, 29.1832, 15.0, 36.0, 36.0, 23.7, 47.6062, 41.7377, 33.4255, 22.1667, 22.3, 1.2833, 16.0, 47.0, 28.1667, 2.5, 43.6532, 49.2827, 33.7879, 34.0522, -33.8688, -37.8136, -28.0167, 11.55, 7.0, 51.0, 64.0, 24.0, 13.0, 21.0, 42.9849, 43.0, 55.0, 60.0, 63.0, 37.3541, 40.0, -34.9285, 42.3601, 36.5761, 50.8333, 43.0731, 35.4437, 32.7157, 29.4241, 26.0, 32.0, 41.2545, 38.2721, 35.4437, 29.3829, 33.8547, 40.745, 38.4747, 33.0, 35.4437, 21.0, 33.0, 26.0275, 29.5, 28.0339, 45.1, 46.8182, 47.5162, 31.0, 30.3753, -14.235, 42.3154, 39.0742, 41.6086, 60.472, 45.9432, 56.2639, 58.5953, 52.1326, 43.9424, 53.7098, 45.5017, 64.9631, 55.1694, 23.6345, -40.9006, 9.082, -31.9505, 53.1424, 49.8153, 43.7333, 25.3548, 48.033, -1.8312, 40.1431, 49.8175, 40.0691, 18.7357, 41.824, -0.7893, 39.3999, 42.5063, -41.4545, 56.8796, 31.7917, 24.0, 14.4974, 43.9088, 27.9904, 40.7128, 39.0916, 37.563, 27.3364, 38.578, 45.775, 33.8034, 45.547, -38.4161, -35.6751, 31.24, 42.1767, 37.8715, 33.2918, 35.8032, 41.122, 48.3794], "legendgroup": "", "lon": [117.2264, 116.4142, 107.874, 117.9874, 103.8343, 113.4244, 108.7881, 106.8748, 109.7453, 114.5149, 127.7615, 113.61399999999999, 112.2707, 111.7088, 113.9448, 119.455, 115.7221, 126.1923, 122.6085, 106.1655, 95.9956, 108.8701, 118.1498, 121.4491, 112.2922, 102.7103, 117.323, 88.0924, 85.2401, 101.48700000000001, 120.0934, 101.0, 138.0, 128.0, 121.0, -122.3321, -87.6976, -111.94, 113.55, 114.2, 103.8333, 108.0, 2.0, 84.25, 112.5, -79.3832, -123.1207, -117.8531, -118.2437, 151.2093, 144.9631, 153.4, 104.9167, 81.0, 9.0, 26.0, 54.0, 122.0, 78.0, -81.2453, 12.0, -3.0, 90.0, 16.0, -121.9552, -4.0, 138.6007, -71.0589, -120.9876, 4.0, -89.4012, 139.638, -117.1611, -98.4936, 30.0, 53.0, -95.9758, -121.9399, 139.638, -98.6134, 35.8623, -123.8695, -121.3542, 44.0, 139.638, 57.0, 65.0, 50.55, 47.75, 1.6596, 15.2, 8.2275, 14.5501, 35.0, 69.3451, -51.9253, 43.3569, 21.8243, 21.7453, 8.4689, 24.9668, 9.5018, 25.0136, 5.2913, 12.4578, 27.9534, -73.5673, -19.0208, 23.8813, -102.5528, 174.886, 8.6753, 115.8605, -7.6921, 6.1296, 7.4167, 51.1839, -121.8339, -78.1834, 47.5769, 15.472999999999999, 45.0382, -70.1627, -71.4128, 113.9213, -8.2245, 1.5218, 145.9707, 24.6032, -7.0926, 45.0, -14.4524, -71.82600000000001, -82.3018, -74.006, -120.8039, -122.3255, -82.5307, -122.9888, -118.7606, -84.3963, -123.1386, -63.6167, -71.543, 36.51, -71.1449, -122.273, -112.4291, -78.5661, -73.7949, 31.1656], "marker": {"color": "#636efa", "size": [990, 414, 576, 296, 91, 1350, 252, 146, 168, 318, 480, 1272, 67217, 1018, 75, 631, 935, 93, 125, 74, 18, 245, 758, 338, 133, 538, 136, 1, 76, 174, 1213, 43, 293, 5186, 42, 21, 4, 1, 10, 100, 110, 16, 204, 1, 36, 19, 9, 1, 1, 13, 9, 11, 1, 1, 196, 6, 27, 3, 5, 1, 2502, 51, 3, 21, 11, 165, 3, 1, 2, 13, 1, 706, 2, 1, 2, 2336, 0, 0, 0, 0, 13, 1, 2, 32, 45, 12, 1, 49, 56, 5, 9, 56, 21, 12, 5, 2, 3, 7, 1, 32, 3, 6, 2, 24, 10, 1, 1, 11, 1, 5, 1, 1, 2, 2, 1, 1, 7, 6, 7, 3, 5, 1, 1, 2, 2, 2, 1, 1, 1, 1, 1, 2, 2, 2, 1, 1, 2, 1, 1, 1, 2, 2, 1, 1, 1, 1, 1, 1, 1, 1, 1], "sizemode": "area", "sizeref": 168.0425}, "name": "", "showlegend": false, "type": "scattergeo"}],
                        {"geo": {"center": {}, "domain": {"x": [0.0, 1.0], "y": [0.0, 1.0]}}, "legend": {"itemsizing": "constant", "tracegroupgap": 0}, "margin": {"t": 60}, "template": {"data": {"bar": [{"error_x": {"color": "#2a3f5f"}, "error_y": {"color": "#2a3f5f"}, "marker": {"line": {"color": "#E5ECF6", "width": 0.5}}, "type": "bar"}], "barpolar": [{"marker": {"line": {"color": "#E5ECF6", "width": 0.5}}, "type": "barpolar"}], "carpet": [{"aaxis": {"endlinecolor": "#2a3f5f", "gridcolor": "white", "linecolor": "white", "minorgridcolor": "white", "startlinecolor": "#2a3f5f"}, "baxis": {"endlinecolor": "#2a3f5f", "gridcolor": "white", "linecolor": "white", "minorgridcolor": "white", "startlinecolor": "#2a3f5f"}, "type": "carpet"}], "choropleth": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "type": "choropleth"}], "contour": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "contour"}], "contourcarpet": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "type": "contourcarpet"}], "heatmap": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "heatmap"}], "heatmapgl": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "heatmapgl"}], "histogram": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "histogram"}], "histogram2d": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "histogram2d"}], "histogram2dcontour": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "histogram2dcontour"}], "mesh3d": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "type": "mesh3d"}], "parcoords": [{"line": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "parcoords"}], "pie": [{"automargin": true, "type": "pie"}], "scatter": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatter"}], "scatter3d": [{"line": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatter3d"}], "scattercarpet": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattercarpet"}], "scattergeo": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattergeo"}], "scattergl": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattergl"}], "scattermapbox": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattermapbox"}], "scatterpolar": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatterpolar"}], "scatterpolargl": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatterpolargl"}], "scatterternary": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatterternary"}], "surface": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "surface"}], "table": [{"cells": {"fill": {"color": "#EBF0F8"}, "line": {"color": "white"}}, "header": {"fill": {"color": "#C8D4E3"}, "line": {"color": "white"}}, "type": "table"}]}, "layout": {"annotationdefaults": {"arrowcolor": "#2a3f5f", "arrowhead": 0, "arrowwidth": 1}, "coloraxis": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "colorscale": {"diverging": [[0, "#8e0152"], [0.1, "#c51b7d"], [0.2, "#de77ae"], [0.3, "#f1b6da"], [0.4, "#fde0ef"], [0.5, "#f7f7f7"], [0.6, "#e6f5d0"], [0.7, "#b8e186"], [0.8, "#7fbc41"], [0.9, "#4d9221"], [1, "#276419"]], "sequential": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "sequentialminus": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]]}, "colorway": ["#636efa", "#EF553B", "#00cc96", "#ab63fa", "#FFA15A", "#19d3f3", "#FF6692", "#B6E880", "#FF97FF", "#FECB52"], "font": {"color": "#2a3f5f"}, "geo": {"bgcolor": "white", "lakecolor": "white", "landcolor": "#E5ECF6", "showlakes": true, "showland": true, "subunitcolor": "white"}, "hoverlabel": {"align": "left"}, "hovermode": "closest", "mapbox": {"style": "light"}, "paper_bgcolor": "white", "plot_bgcolor": "#E5ECF6", "polar": {"angularaxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}, "bgcolor": "#E5ECF6", "radialaxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}}, "scene": {"xaxis": {"backgroundcolor": "#E5ECF6", "gridcolor": "white", "gridwidth": 2, "linecolor": "white", "showbackground": true, "ticks": "", "zerolinecolor": "white"}, "yaxis": {"backgroundcolor": "#E5ECF6", "gridcolor": "white", "gridwidth": 2, "linecolor": "white", "showbackground": true, "ticks": "", "zerolinecolor": "white"}, "zaxis": {"backgroundcolor": "#E5ECF6", "gridcolor": "white", "gridwidth": 2, "linecolor": "white", "showbackground": true, "ticks": "", "zerolinecolor": "white"}}, "shapedefaults": {"line": {"color": "#2a3f5f"}}, "ternary": {"aaxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}, "baxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}, "bgcolor": "#E5ECF6", "caxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}}, "title": {"x": 0.05}, "xaxis": {"automargin": true, "gridcolor": "white", "linecolor": "white", "ticks": "", "title": {"standoff": 15}, "zerolinecolor": "white", "zerolinewidth": 2}, "yaxis": {"automargin": true, "gridcolor": "white", "linecolor": "white", "ticks": "", "title": {"standoff": 15}, "zerolinecolor": "white", "zerolinewidth": 2}}}},
                        {"responsive": true}
                    ).then(function(){

var gd = document.getElementById('be7d9ab1-f2fb-49fa-87ae-7309c21c2bd2');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })
                };
                });
            </script>
        </div>


In addition to many common plots, Plotly also allow us to generate interactive maps and add widgets with very little code. Because the cases for mainland China are so large compared to the number of confirmed cases elsewhere the relative sizes of the markers will be disproportionate and many of them will be hard to see. I will take the square root of the confirmed cases so that the markers can become more visible. This is just arbitrary and for display purposes.

> A tidy version of this DataFrame is one without the dates as columns, but rather as values listed in a single column.



```python
# Flatten DataFrame columns. This is the format required by Plotly
df_flat = pd.melt(df_infected, id_vars=['Country/Region','Lat','Long'], value_vars=df_infected.columns[4:].values)
df_flat["sqrt_value"] = np.sqrt(df_flat["value"])
df_flat.head()

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
      <th>Country/Region</th>
      <th>Lat</th>
      <th>Long</th>
      <th>variable</th>
      <th>value</th>
      <th>sqrt_value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Mainland China</td>
      <td>31.8257</td>
      <td>117.2264</td>
      <td>1/22/20</td>
      <td>1</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Mainland China</td>
      <td>40.1824</td>
      <td>116.4142</td>
      <td>1/22/20</td>
      <td>14</td>
      <td>3.741657</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Mainland China</td>
      <td>30.0572</td>
      <td>107.8740</td>
      <td>1/22/20</td>
      <td>6</td>
      <td>2.449490</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Mainland China</td>
      <td>26.0789</td>
      <td>117.9874</td>
      <td>1/22/20</td>
      <td>1</td>
      <td>1.000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Mainland China</td>
      <td>36.0611</td>
      <td>103.8343</td>
      <td>1/22/20</td>
      <td>0</td>
      <td>0.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
### Create interactive worldmap
fig = px.scatter_geo(df_flat, 
                     lat="Lat", 
                     lon="Long", 
                     color="Country/Region", 
                     hover_name="Country/Region", 
                     size="sqrt_value",
                     animation_frame="variable", 
                     projection="natural earth",
                     width=800, height=600)
fig.show()
```


<div>


            <div id="b68f2928-4de1-4e4b-b531-475adeeaa76e" class="plotly-graph-div" style="height:600px; width:800px;"></div>
            <script type="text/javascript">
                require(["plotly"], function(Plotly) {
                    window.PLOTLYENV=window.PLOTLYENV || {};

                if (document.getElementById("b68f2928-4de1-4e4b-b531-475adeeaa76e")) {
                    Plotly.newPlot(
                        'b68f2928-4de1-4e4b-b531-475adeeaa76e',
                        [{"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Mainland China<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China", "Mainland China"], "lat": [31.8257, 40.1824, 30.0572, 26.0789, 36.0611, 23.3417, 23.8298, 26.8154, 19.1959, 38.0428, 47.861999999999995, 33.882020000000004, 30.9756, 27.6104, 44.0935, 32.9711, 27.614, 43.6661, 41.2956, 37.2692, 35.7452, 35.1917, 36.3427, 31.201999999999998, 37.5777, 30.6171, 39.3054, 31.6927, 41.1129, 24.974, 29.1832], "legendgroup": "Mainland China", "lon": [117.2264, 116.4142, 107.874, 117.9874, 103.8343, 113.4244, 108.7881, 106.8748, 109.7453, 114.5149, 127.7615, 113.61399999999999, 112.2707, 111.7088, 113.9448, 119.455, 115.7221, 126.1923, 122.6085, 106.1655, 95.9956, 108.8701, 118.1498, 121.4491, 112.2922, 102.7103, 117.323, 88.0924, 85.2401, 101.48700000000001, 120.0934], "marker": {"color": "#636efa", "size": [1.0, 3.7416573867739413, 2.449489742783178, 1.0, 0.0, 5.0990195135927845, 1.4142135623730951, 1.0, 2.0, 1.0, 0.0, 2.23606797749979, 21.071307505705477, 2.0, 0.0, 1.0, 1.4142135623730951, 0.0, 1.4142135623730951, 1.0, 0.0, 0.0, 1.4142135623730951, 3.0, 1.0, 2.23606797749979, 2.0, 0.0, 0.0, 1.0, 3.1622776601683795], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Mainland China", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Thailand<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Thailand"], "lat": [15.0], "legendgroup": "Thailand", "lon": [101.0], "marker": {"color": "#EF553B", "size": [1.4142135623730951], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Thailand", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Japan<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Japan"], "lat": [36.0], "legendgroup": "Japan", "lon": [138.0], "marker": {"color": "#00cc96", "size": [1.4142135623730951], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Japan", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=South Korea<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["South Korea"], "lat": [36.0], "legendgroup": "South Korea", "lon": [128.0], "marker": {"color": "#ab63fa", "size": [1.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "South Korea", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Taiwan<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Taiwan"], "lat": [23.7], "legendgroup": "Taiwan", "lon": [121.0], "marker": {"color": "#FFA15A", "size": [1.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Taiwan", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=US<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US", "US"], "lat": [47.6062, 41.7377, 33.4255, 33.7879, 34.0522, 37.3541, 42.3601, 36.5761, 43.0731, 32.7157, 29.4241, 41.2545, 38.2721, 29.3829, 40.745, 38.4747, 35.4437, 48.033, 41.824, 43.9088, 27.9904, 40.7128, 39.0916, 37.563, 27.3364, 38.578, 45.775, 33.8034, 45.547, 42.1767, 37.8715, 33.2918, 35.8032, 41.122], "legendgroup": "US", "lon": [-122.3321, -87.6976, -111.94, -117.8531, -118.2437, -121.9552, -71.0589, -120.9876, -89.4012, -117.1611, -98.4936, -95.9758, -121.9399, -98.6134, -123.8695, -121.3542, 139.638, -121.8339, -71.4128, -71.82600000000001, -82.3018, -74.006, -120.8039, -122.3255, -82.5307, -122.9888, -118.7606, -84.3963, -123.1386, -71.1449, -122.273, -112.4291, -78.5661, -73.7949], "marker": {"color": "#19d3f3", "size": [1.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "US", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Macau<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Macau"], "lat": [22.1667], "legendgroup": "Macau", "lon": [113.55], "marker": {"color": "#FF6692", "size": [1.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Macau", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Hong Kong<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Hong Kong"], "lat": [22.3], "legendgroup": "Hong Kong", "lon": [114.2], "marker": {"color": "#B6E880", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Hong Kong", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Singapore<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Singapore"], "lat": [1.2833], "legendgroup": "Singapore", "lon": [103.8333], "marker": {"color": "#FF97FF", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Singapore", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Vietnam<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Vietnam"], "lat": [16.0], "legendgroup": "Vietnam", "lon": [108.0], "marker": {"color": "#FECB52", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Vietnam", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=France<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["France"], "lat": [47.0], "legendgroup": "France", "lon": [2.0], "marker": {"color": "#636efa", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "France", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Nepal<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Nepal"], "lat": [28.1667], "legendgroup": "Nepal", "lon": [84.25], "marker": {"color": "#EF553B", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Nepal", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Malaysia<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Malaysia"], "lat": [2.5], "legendgroup": "Malaysia", "lon": [112.5], "marker": {"color": "#00cc96", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Malaysia", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Canada<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Canada", "Canada", "Canada", "Canada"], "lat": [43.6532, 49.2827, 42.9849, 45.5017], "legendgroup": "Canada", "lon": [-79.3832, -123.1207, -81.2453, -73.5673], "marker": {"color": "#ab63fa", "size": [0.0, 0.0, 0.0, 0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Canada", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Australia<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Australia", "Australia", "Australia", "Australia", "Australia", "Australia", "Australia"], "lat": [-33.8688, -37.8136, -28.0167, -34.9285, 35.4437, -31.9505, -41.4545], "legendgroup": "Australia", "lon": [151.2093, 144.9631, 153.4, 138.6007, 139.638, 115.8605, 145.9707], "marker": {"color": "#FFA15A", "size": [0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Australia", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Cambodia<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Cambodia"], "lat": [11.55], "legendgroup": "Cambodia", "lon": [104.9167], "marker": {"color": "#19d3f3", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Cambodia", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Sri Lanka<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Sri Lanka"], "lat": [7.0], "legendgroup": "Sri Lanka", "lon": [81.0], "marker": {"color": "#FF6692", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Sri Lanka", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Germany<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Germany"], "lat": [51.0], "legendgroup": "Germany", "lon": [9.0], "marker": {"color": "#B6E880", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Germany", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Finland<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Finland"], "lat": [64.0], "legendgroup": "Finland", "lon": [26.0], "marker": {"color": "#FF97FF", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Finland", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=United Arab Emirates<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["United Arab Emirates"], "lat": [24.0], "legendgroup": "United Arab Emirates", "lon": [54.0], "marker": {"color": "#FECB52", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "United Arab Emirates", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Philippines<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Philippines"], "lat": [13.0], "legendgroup": "Philippines", "lon": [122.0], "marker": {"color": "#636efa", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Philippines", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=India<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["India"], "lat": [21.0], "legendgroup": "India", "lon": [78.0], "marker": {"color": "#EF553B", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "India", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Italy<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Italy"], "lat": [43.0], "legendgroup": "Italy", "lon": [12.0], "marker": {"color": "#00cc96", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Italy", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=UK<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["UK"], "lat": [55.0], "legendgroup": "UK", "lon": [-3.0], "marker": {"color": "#ab63fa", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "UK", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Russia<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Russia"], "lat": [60.0], "legendgroup": "Russia", "lon": [90.0], "marker": {"color": "#FFA15A", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Russia", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Sweden<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Sweden"], "lat": [63.0], "legendgroup": "Sweden", "lon": [16.0], "marker": {"color": "#19d3f3", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Sweden", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Spain<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Spain"], "lat": [40.0], "legendgroup": "Spain", "lon": [-4.0], "marker": {"color": "#FF6692", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Spain", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Belgium<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Belgium"], "lat": [50.8333], "legendgroup": "Belgium", "lon": [4.0], "marker": {"color": "#B6E880", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Belgium", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Others<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Others"], "lat": [35.4437], "legendgroup": "Others", "lon": [139.638], "marker": {"color": "#FF97FF", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Others", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Egypt<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Egypt"], "lat": [26.0], "legendgroup": "Egypt", "lon": [30.0], "marker": {"color": "#FECB52", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Egypt", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Iran<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Iran"], "lat": [32.0], "legendgroup": "Iran", "lon": [53.0], "marker": {"color": "#636efa", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Iran", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Lebanon<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Lebanon"], "lat": [33.8547], "legendgroup": "Lebanon", "lon": [35.8623], "marker": {"color": "#EF553B", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Lebanon", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Iraq<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Iraq"], "lat": [33.0], "legendgroup": "Iraq", "lon": [44.0], "marker": {"color": "#00cc96", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Iraq", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Oman<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Oman"], "lat": [21.0], "legendgroup": "Oman", "lon": [57.0], "marker": {"color": "#ab63fa", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Oman", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Afghanistan<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Afghanistan"], "lat": [33.0], "legendgroup": "Afghanistan", "lon": [65.0], "marker": {"color": "#FFA15A", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Afghanistan", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Bahrain<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Bahrain"], "lat": [26.0275], "legendgroup": "Bahrain", "lon": [50.55], "marker": {"color": "#19d3f3", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Bahrain", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Kuwait<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Kuwait"], "lat": [29.5], "legendgroup": "Kuwait", "lon": [47.75], "marker": {"color": "#FF6692", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Kuwait", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Algeria<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Algeria"], "lat": [28.0339], "legendgroup": "Algeria", "lon": [1.6596], "marker": {"color": "#B6E880", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Algeria", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Croatia<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Croatia"], "lat": [45.1], "legendgroup": "Croatia", "lon": [15.2], "marker": {"color": "#FF97FF", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Croatia", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Switzerland<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Switzerland"], "lat": [46.8182], "legendgroup": "Switzerland", "lon": [8.2275], "marker": {"color": "#FECB52", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Switzerland", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Austria<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Austria"], "lat": [47.5162], "legendgroup": "Austria", "lon": [14.5501], "marker": {"color": "#636efa", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Austria", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Israel<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Israel"], "lat": [31.0], "legendgroup": "Israel", "lon": [35.0], "marker": {"color": "#EF553B", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Israel", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Pakistan<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Pakistan"], "lat": [30.3753], "legendgroup": "Pakistan", "lon": [69.3451], "marker": {"color": "#00cc96", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Pakistan", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Brazil<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Brazil"], "lat": [-14.235], "legendgroup": "Brazil", "lon": [-51.9253], "marker": {"color": "#ab63fa", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Brazil", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Georgia<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Georgia"], "lat": [42.3154], "legendgroup": "Georgia", "lon": [43.3569], "marker": {"color": "#FFA15A", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Georgia", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Greece<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Greece"], "lat": [39.0742], "legendgroup": "Greece", "lon": [21.8243], "marker": {"color": "#19d3f3", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Greece", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=North Macedonia<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["North Macedonia"], "lat": [41.6086], "legendgroup": "North Macedonia", "lon": [21.7453], "marker": {"color": "#FF6692", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "North Macedonia", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Norway<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Norway"], "lat": [60.472], "legendgroup": "Norway", "lon": [8.4689], "marker": {"color": "#B6E880", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Norway", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Romania<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Romania"], "lat": [45.9432], "legendgroup": "Romania", "lon": [24.9668], "marker": {"color": "#FF97FF", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Romania", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Denmark<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Denmark"], "lat": [56.2639], "legendgroup": "Denmark", "lon": [9.5018], "marker": {"color": "#FECB52", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Denmark", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Estonia<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Estonia"], "lat": [58.5953], "legendgroup": "Estonia", "lon": [25.0136], "marker": {"color": "#636efa", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Estonia", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Netherlands<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Netherlands"], "lat": [52.1326], "legendgroup": "Netherlands", "lon": [5.2913], "marker": {"color": "#EF553B", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Netherlands", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=San Marino<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["San Marino"], "lat": [43.9424], "legendgroup": "San Marino", "lon": [12.4578], "marker": {"color": "#00cc96", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "San Marino", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Belarus<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Belarus"], "lat": [53.7098], "legendgroup": "Belarus", "lon": [27.9534], "marker": {"color": "#ab63fa", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Belarus", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Iceland<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Iceland"], "lat": [64.9631], "legendgroup": "Iceland", "lon": [-19.0208], "marker": {"color": "#FFA15A", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Iceland", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Lithuania<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Lithuania"], "lat": [55.1694], "legendgroup": "Lithuania", "lon": [23.8813], "marker": {"color": "#19d3f3", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Lithuania", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Mexico<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Mexico"], "lat": [23.6345], "legendgroup": "Mexico", "lon": [-102.5528], "marker": {"color": "#FF6692", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Mexico", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=New Zealand<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["New Zealand"], "lat": [-40.9006], "legendgroup": "New Zealand", "lon": [174.886], "marker": {"color": "#B6E880", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "New Zealand", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Nigeria<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Nigeria"], "lat": [9.082], "legendgroup": "Nigeria", "lon": [8.6753], "marker": {"color": "#FF97FF", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Nigeria", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Ireland<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Ireland"], "lat": [53.1424], "legendgroup": "Ireland", "lon": [-7.6921], "marker": {"color": "#FECB52", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Ireland", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Luxembourg<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Luxembourg"], "lat": [49.8153], "legendgroup": "Luxembourg", "lon": [6.1296], "marker": {"color": "#636efa", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Luxembourg", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Monaco<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Monaco"], "lat": [43.7333], "legendgroup": "Monaco", "lon": [7.4167], "marker": {"color": "#EF553B", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Monaco", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Qatar<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Qatar"], "lat": [25.3548], "legendgroup": "Qatar", "lon": [51.1839], "marker": {"color": "#00cc96", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Qatar", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Ecuador<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Ecuador"], "lat": [-1.8312], "legendgroup": "Ecuador", "lon": [-78.1834], "marker": {"color": "#ab63fa", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Ecuador", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Azerbaijan<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Azerbaijan"], "lat": [40.1431], "legendgroup": "Azerbaijan", "lon": [47.5769], "marker": {"color": "#FFA15A", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Azerbaijan", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Czech Republic<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Czech Republic"], "lat": [49.8175], "legendgroup": "Czech Republic", "lon": [15.472999999999999], "marker": {"color": "#19d3f3", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Czech Republic", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Armenia<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Armenia"], "lat": [40.0691], "legendgroup": "Armenia", "lon": [45.0382], "marker": {"color": "#FF6692", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Armenia", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Dominican Republic<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Dominican Republic"], "lat": [18.7357], "legendgroup": "Dominican Republic", "lon": [-70.1627], "marker": {"color": "#B6E880", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Dominican Republic", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Indonesia<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Indonesia"], "lat": [-0.7893], "legendgroup": "Indonesia", "lon": [113.9213], "marker": {"color": "#FF97FF", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Indonesia", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Portugal<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Portugal"], "lat": [39.3999], "legendgroup": "Portugal", "lon": [-8.2245], "marker": {"color": "#FECB52", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Portugal", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Andorra<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Andorra"], "lat": [42.5063], "legendgroup": "Andorra", "lon": [1.5218], "marker": {"color": "#636efa", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Andorra", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Latvia<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Latvia"], "lat": [56.8796], "legendgroup": "Latvia", "lon": [24.6032], "marker": {"color": "#EF553B", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Latvia", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Morocco<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Morocco"], "lat": [31.7917], "legendgroup": "Morocco", "lon": [-7.0926], "marker": {"color": "#00cc96", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Morocco", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Saudi Arabia<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Saudi Arabia"], "lat": [24.0], "legendgroup": "Saudi Arabia", "lon": [45.0], "marker": {"color": "#ab63fa", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Saudi Arabia", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Senegal<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Senegal"], "lat": [14.4974], "legendgroup": "Senegal", "lon": [-14.4524], "marker": {"color": "#FFA15A", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Senegal", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Argentina<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Argentina"], "lat": [-38.4161], "legendgroup": "Argentina", "lon": [-63.6167], "marker": {"color": "#19d3f3", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Argentina", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Chile<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Chile"], "lat": [-35.6751], "legendgroup": "Chile", "lon": [-71.543], "marker": {"color": "#FF6692", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Chile", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Jordan<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Jordan"], "lat": [31.24], "legendgroup": "Jordan", "lon": [36.51], "marker": {"color": "#B6E880", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Jordan", "showlegend": true, "type": "scattergeo"}, {"geo": "geo", "hoverlabel": {"namelength": 0}, "hovertemplate": "<b>%{hovertext}</b><br><br>Country/Region=Ukraine<br>variable=1/22/20<br>sqrt_value=%{marker.size}<br>Lat=%{lat}<br>Long=%{lon}", "hovertext": ["Ukraine"], "lat": [48.3794], "legendgroup": "Ukraine", "lon": [31.1656], "marker": {"color": "#FF97FF", "size": [0.0], "sizemode": "area", "sizeref": 0.6481560383117633}, "name": "Ukraine", "showlegend": true, "type": "scattergeo"}],
                        {"geo": {"center": {}, "domain": {"x": [0.0, 1.0], "y": [0.0, 1.0]}, "projection": {"type": "natural earth"}}, "height": 600, "legend": {"itemsizing": "constant", "title": {"text": "Country/Region"}, "tracegroupgap": 0}, "margin": {"t": 60}, "sliders": [{"active": 0, "currentvalue": {"prefix": "variable="}, "len": 0.9, "pad": {"b": 10, "t": 60}, "steps": [{"args": [["1/22/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "1/22/20", "method": "animate"}, {"args": [["1/23/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "1/23/20", "method": "animate"}, {"args": [["1/24/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "1/24/20", "method": "animate"}, {"args": [["1/25/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "1/25/20", "method": "animate"}, {"args": [["1/26/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "1/26/20", "method": "animate"}, {"args": [["1/27/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "1/27/20", "method": "animate"}, {"args": [["1/28/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "1/28/20", "method": "animate"}, {"args": [["1/29/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "1/29/20", "method": "animate"}, {"args": [["1/30/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "1/30/20", "method": "animate"}, {"args": [["1/31/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "1/31/20", "method": "animate"}, {"args": [["2/1/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/1/20", "method": "animate"}, {"args": [["2/2/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/2/20", "method": "animate"}, {"args": [["2/3/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/3/20", "method": "animate"}, {"args": [["2/4/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/4/20", "method": "animate"}, {"args": [["2/5/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/5/20", "method": "animate"}, {"args": [["2/6/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/6/20", "method": "animate"}, {"args": [["2/7/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/7/20", "method": "animate"}, {"args": [["2/8/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/8/20", "method": "animate"}, {"args": [["2/9/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/9/20", "method": "animate"}, {"args": [["2/10/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/10/20", "method": "animate"}, {"args": [["2/11/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/11/20", "method": "animate"}, {"args": [["2/12/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/12/20", "method": "animate"}, {"args": [["2/13/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/13/20", "method": "animate"}, {"args": [["2/14/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/14/20", "method": "animate"}, {"args": [["2/15/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/15/20", "method": "animate"}, {"args": [["2/16/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/16/20", "method": "animate"}, {"args": [["2/17/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/17/20", "method": "animate"}, {"args": [["2/18/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/18/20", "method": "animate"}, {"args": [["2/19/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/19/20", "method": "animate"}, {"args": [["2/20/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/20/20", "method": "animate"}, {"args": [["2/21/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/21/20", "method": "animate"}, {"args": [["2/22/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/22/20", "method": "animate"}, {"args": [["2/23/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/23/20", "method": "animate"}, {"args": [["2/24/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/24/20", "method": "animate"}, {"args": [["2/25/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/25/20", "method": "animate"}, {"args": [["2/26/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/26/20", "method": "animate"}, {"args": [["2/27/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/27/20", "method": "animate"}, {"args": [["2/28/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/28/20", "method": "animate"}, {"args": [["2/29/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "2/29/20", "method": "animate"}, {"args": [["3/1/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "3/1/20", "method": "animate"}, {"args": [["3/2/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "3/2/20", "method": "animate"}, {"args": [["3/3/20"], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "3/3/20", "method": "animate"}], "x": 0.1, "xanchor": "left", "y": 0, "yanchor": "top"}], "template": {"data": {"bar": [{"error_x": {"color": "#2a3f5f"}, "error_y": {"color": "#2a3f5f"}, "marker": {"line": {"color": "#E5ECF6", "width": 0.5}}, "type": "bar"}], "barpolar": [{"marker": {"line": {"color": "#E5ECF6", "width": 0.5}}, "type": "barpolar"}], "carpet": [{"aaxis": {"endlinecolor": "#2a3f5f", "gridcolor": "white", "linecolor": "white", "minorgridcolor": "white", "startlinecolor": "#2a3f5f"}, "baxis": {"endlinecolor": "#2a3f5f", "gridcolor": "white", "linecolor": "white", "minorgridcolor": "white", "startlinecolor": "#2a3f5f"}, "type": "carpet"}], "choropleth": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "type": "choropleth"}], "contour": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "contour"}], "contourcarpet": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "type": "contourcarpet"}], "heatmap": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "heatmap"}], "heatmapgl": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "heatmapgl"}], "histogram": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "histogram"}], "histogram2d": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "histogram2d"}], "histogram2dcontour": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "histogram2dcontour"}], "mesh3d": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "type": "mesh3d"}], "parcoords": [{"line": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "parcoords"}], "pie": [{"automargin": true, "type": "pie"}], "scatter": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatter"}], "scatter3d": [{"line": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatter3d"}], "scattercarpet": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattercarpet"}], "scattergeo": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattergeo"}], "scattergl": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattergl"}], "scattermapbox": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scattermapbox"}], "scatterpolar": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatterpolar"}], "scatterpolargl": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatterpolargl"}], "scatterternary": [{"marker": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "type": "scatterternary"}], "surface": [{"colorbar": {"outlinewidth": 0, "ticks": ""}, "colorscale": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "type": "surface"}], "table": [{"cells": {"fill": {"color": "#EBF0F8"}, "line": {"color": "white"}}, "header": {"fill": {"color": "#C8D4E3"}, "line": {"color": "white"}}, "type": "table"}]}, "layout": {"annotationdefaults": {"arrowcolor": "#2a3f5f", "arrowhead": 0, "arrowwidth": 1}, "coloraxis": {"colorbar": {"outlinewidth": 0, "ticks": ""}}, "colorscale": {"diverging": [[0, "#8e0152"], [0.1, "#c51b7d"], [0.2, "#de77ae"], [0.3, "#f1b6da"], [0.4, "#fde0ef"], [0.5, "#f7f7f7"], [0.6, "#e6f5d0"], [0.7, "#b8e186"], [0.8, "#7fbc41"], [0.9, "#4d9221"], [1, "#276419"]], "sequential": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]], "sequentialminus": [[0.0, "#0d0887"], [0.1111111111111111, "#46039f"], [0.2222222222222222, "#7201a8"], [0.3333333333333333, "#9c179e"], [0.4444444444444444, "#bd3786"], [0.5555555555555556, "#d8576b"], [0.6666666666666666, "#ed7953"], [0.7777777777777778, "#fb9f3a"], [0.8888888888888888, "#fdca26"], [1.0, "#f0f921"]]}, "colorway": ["#636efa", "#EF553B", "#00cc96", "#ab63fa", "#FFA15A", "#19d3f3", "#FF6692", "#B6E880", "#FF97FF", "#FECB52"], "font": {"color": "#2a3f5f"}, "geo": {"bgcolor": "white", "lakecolor": "white", "landcolor": "#E5ECF6", "showlakes": true, "showland": true, "subunitcolor": "white"}, "hoverlabel": {"align": "left"}, "hovermode": "closest", "mapbox": {"style": "light"}, "paper_bgcolor": "white", "plot_bgcolor": "#E5ECF6", "polar": {"angularaxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}, "bgcolor": "#E5ECF6", "radialaxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}}, "scene": {"xaxis": {"backgroundcolor": "#E5ECF6", "gridcolor": "white", "gridwidth": 2, "linecolor": "white", "showbackground": true, "ticks": "", "zerolinecolor": "white"}, "yaxis": {"backgroundcolor": "#E5ECF6", "gridcolor": "white", "gridwidth": 2, "linecolor": "white", "showbackground": true, "ticks": "", "zerolinecolor": "white"}, "zaxis": {"backgroundcolor": "#E5ECF6", "gridcolor": "white", "gridwidth": 2, "linecolor": "white", "showbackground": true, "ticks": "", "zerolinecolor": "white"}}, "shapedefaults": {"line": {"color": "#2a3f5f"}}, "ternary": {"aaxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}, "baxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}, "bgcolor": "#E5ECF6", "caxis": {"gridcolor": "white", "linecolor": "white", "ticks": ""}}, "title": {"x": 0.05}, "xaxis": {"automargin": true, "gridcolor": "white", "linecolor": "white", "ticks": "", "title": {"standoff": 15}, "zerolinecolor": "white", "zerolinewidth": 2}, "yaxis": {"automargin": true, "gridcolor": "white", "linecolor": "white", "ticks": "", "title": {"standoff": 15}, "zerolinecolor": "white", "zerolinewidth": 2}}}, "updatemenus": [{"buttons": [{"args": [null, {"frame": {"duration": 500, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 500, "easing": "linear"}}], "label": "&#9654;", "method": "animate"}, {"args": [[null], {"frame": {"duration": 0, "redraw": true}, "fromcurrent": true, "mode": "immediate", "transition": {"duration": 0, "easing": "linear"}}], "label": "&#9724;", "method": "animate"}], "direction": "left", "pad": {"r": 10, "t": 70}, "showactive": false, "type": "buttons", "x": 0.1, "xanchor": "right", "y": 0, "yanchor": "top"}], "width": 800},
                        {"responsive": true}
                    ).then(function(){
                        }).then(function(){

var gd = document.getElementById('b68f2928-4de1-4e4b-b531-475adeeaa76e');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })
                };
                });
            </script>
        </div>
