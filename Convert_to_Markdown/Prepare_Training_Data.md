Use Youtube API to extract thumbnail data from my wife's [Youtube Channel](https://www.youtube.com/channel/UCN_hbfsIsYgj-PtGJT8aSAQ). You need to replace `Your Youtube API` with your won API key which can be obtained from Youtube Data API key from [here](https://developers.google.com/youtube/v3).


```python
from googleapiclient.discovery import build
import pandas as pd
```


```python
# Set up API client
api_key = "AIzaSyDRtin-ZzXXEK_BUzID4se9Esk8SxrtaHk"
youtube = build('youtube', 'v3', developerKey=api_key)
```


```python
# Retrieve video data
channel_id = "UCN_hbfsIsYgj-PtGJT8aSAQ"
videos = []
next_page_token = None
```


```python
request = youtube.search().list(
            part='snippet',
            channelId=channel_id,
            maxResults=50,  # Adjust the number of results per page as needed
            pageToken=next_page_token
        )
response = request.execute()
```


```python
for item in response['items']:
  video = {}
  video['title'] = item['snippet']['title']
  video['thumbnail'] = item['snippet']['thumbnails']['default']['url']
  videos.append(video)
```


```python
# Create a Pandas DataFrame from data
df = pd.DataFrame(videos)
df.head()
```





  <div id="df-5350d1d2-479e-4049-ad17-6e4f1bb2803b" class="colab-df-container">
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
      <th>title</th>
      <th>thumbnail</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Crochet ideas</td>
      <td>https://i.ytimg.com/vi/2hPsxSXwsf8/default.jpg</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Lingzhi Handmade</td>
      <td>https://yt3.ggpht.com/NMgSWTrRKKBRi15_vl0Dc9XY...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>When you want to crochet and you have a baby</td>
      <td>https://i.ytimg.com/vi/9ePFI7814Rc/default.jpg</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Crochet Leaves</td>
      <td>https://i.ytimg.com/vi/jx2ojGTX854/default.jpg</td>
    </tr>
    <tr>
      <th>4</th>
      <td>How to crochet pet collar | crochet tulips | B...</td>
      <td>https://i.ytimg.com/vi/M5pbgRzZs6w/default.jpg</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-5350d1d2-479e-4049-ad17-6e4f1bb2803b')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-5350d1d2-479e-4049-ad17-6e4f1bb2803b button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-5350d1d2-479e-4049-ad17-6e4f1bb2803b');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-0617f8db-cdd1-4563-b6fa-8cb9d18078a9">
  <button class="colab-df-quickchart" onclick="quickchart('df-0617f8db-cdd1-4563-b6fa-8cb9d18078a9')"
            title="Suggest charts."
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
    background-color: #E8F0FE;
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: #1967D2;
    height: 32px;
    padding: 0 0 0 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: #E2EBFA;
    box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: #174EA6;
  }

  [theme=dark] .colab-df-quickchart {
    background-color: #3B4455;
    fill: #D2E3FC;
  }

  [theme=dark] .colab-df-quickchart:hover {
    background-color: #434B5C;
    box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
    filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
    fill: #FFFFFF;
  }
</style>

  <script>
    async function quickchart(key) {
      const charts = await google.colab.kernel.invokeFunction(
          'suggestCharts', [key], {});
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-0617f8db-cdd1-4563-b6fa-8cb9d18078a9 button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>
    </div>
  </div>




Download csv file of click-through rate from youtube studio (Youtube studio -> Analytics -> Advanced mode -> Export current view -> Comma-seperated values (.csv)), because the Youtube API I used only allow access to public information. You can use another API to get access to creator's data but this is a minimal product.

![Download CTR data from Youtube Studio](images/youtube_analytic.png "Download CTR data from Youtube Studio")

And upload the `Table data.csv` to the colab from following cell.


```python
from google.colab import files
files.upload()
```


```python
# Read the CSV file into a Pandas DataFrame
df_ctr = pd.read_csv('Table data.csv')
df_ctr.head()
```





  <div id="df-cb2f0959-efd6-4816-82e5-bf90d0cdd670" class="colab-df-container">
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
      <th>Content</th>
      <th>Video title</th>
      <th>Video publish time</th>
      <th>Views</th>
      <th>Watch time (hours)</th>
      <th>Subscribers</th>
      <th>Estimated revenue (USD)</th>
      <th>Impressions</th>
      <th>Impressions click-through rate (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Total</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>364688</td>
      <td>16858.4932</td>
      <td>7318</td>
      <td>717.182</td>
      <td>6093138</td>
      <td>3.80</td>
    </tr>
    <tr>
      <th>1</th>
      <td>z4VoUx2mC_U</td>
      <td>How to crochet a rose | Crochet flower bouquet</td>
      <td>Nov 22, 2022</td>
      <td>35529</td>
      <td>1436.0488</td>
      <td>308</td>
      <td>65.502</td>
      <td>444426</td>
      <td>4.92</td>
    </tr>
    <tr>
      <th>2</th>
      <td>x2nzzuQwbs4</td>
      <td>How to Crochet Sunflower | Beginner Friendly F...</td>
      <td>Feb 8, 2023</td>
      <td>32785</td>
      <td>2353.8223</td>
      <td>313</td>
      <td>84.698</td>
      <td>364717</td>
      <td>5.11</td>
    </tr>
    <tr>
      <th>3</th>
      <td>fjOS79LYg2I</td>
      <td>Crochet keychain | Crochet Afghan flower</td>
      <td>Aug 10, 2022</td>
      <td>29020</td>
      <td>1564.6322</td>
      <td>246</td>
      <td>57.722</td>
      <td>512561</td>
      <td>3.82</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Lvz0qSF5-k0</td>
      <td>How to crochet a PingPang Flower | crochet flo...</td>
      <td>Mar 30, 2023</td>
      <td>28090</td>
      <td>1084.0254</td>
      <td>303</td>
      <td>36.813</td>
      <td>490394</td>
      <td>3.76</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-cb2f0959-efd6-4816-82e5-bf90d0cdd670')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-cb2f0959-efd6-4816-82e5-bf90d0cdd670 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-cb2f0959-efd6-4816-82e5-bf90d0cdd670');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-e8a000d0-1d81-4d12-87ae-aa95c6ea336d">
  <button class="colab-df-quickchart" onclick="quickchart('df-e8a000d0-1d81-4d12-87ae-aa95c6ea336d')"
            title="Suggest charts."
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
    background-color: #E8F0FE;
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: #1967D2;
    height: 32px;
    padding: 0 0 0 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: #E2EBFA;
    box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: #174EA6;
  }

  [theme=dark] .colab-df-quickchart {
    background-color: #3B4455;
    fill: #D2E3FC;
  }

  [theme=dark] .colab-df-quickchart:hover {
    background-color: #434B5C;
    box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
    filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
    fill: #FFFFFF;
  }
</style>

  <script>
    async function quickchart(key) {
      const charts = await google.colab.kernel.invokeFunction(
          'suggestCharts', [key], {});
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-e8a000d0-1d81-4d12-87ae-aa95c6ea336d button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>
    </div>
  </div>





```python
# Rename the df 'title' column to the same name of df_ctr whihch is 'Video title' for merging purpose
df = df.rename(columns={'title': 'Video title'})
```


```python
# Merge the DataFrames based on the video title
df_merged = pd.merge(df, df_ctr[['Video title', 'Impressions click-through rate (%)']], on='Video title', how='left')
df_merged.head()
```





  <div id="df-549d66bd-8bdb-45fb-b679-2b6d32ed6df8" class="colab-df-container">
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
      <th>Video title</th>
      <th>thumbnail</th>
      <th>Impressions click-through rate (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Crochet ideas</td>
      <td>https://i.ytimg.com/vi/2hPsxSXwsf8/default.jpg</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Lingzhi Handmade</td>
      <td>https://yt3.ggpht.com/NMgSWTrRKKBRi15_vl0Dc9XY...</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>When you want to crochet and you have a baby</td>
      <td>https://i.ytimg.com/vi/9ePFI7814Rc/default.jpg</td>
      <td>1.26</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Crochet Leaves</td>
      <td>https://i.ytimg.com/vi/jx2ojGTX854/default.jpg</td>
      <td>4.57</td>
    </tr>
    <tr>
      <th>4</th>
      <td>How to crochet pet collar | crochet tulips | B...</td>
      <td>https://i.ytimg.com/vi/M5pbgRzZs6w/default.jpg</td>
      <td>4.39</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-549d66bd-8bdb-45fb-b679-2b6d32ed6df8')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-549d66bd-8bdb-45fb-b679-2b6d32ed6df8 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-549d66bd-8bdb-45fb-b679-2b6d32ed6df8');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-07a51af4-f15e-483f-ab61-71d08059fb01">
  <button class="colab-df-quickchart" onclick="quickchart('df-07a51af4-f15e-483f-ab61-71d08059fb01')"
            title="Suggest charts."
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
    background-color: #E8F0FE;
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: #1967D2;
    height: 32px;
    padding: 0 0 0 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: #E2EBFA;
    box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: #174EA6;
  }

  [theme=dark] .colab-df-quickchart {
    background-color: #3B4455;
    fill: #D2E3FC;
  }

  [theme=dark] .colab-df-quickchart:hover {
    background-color: #434B5C;
    box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
    filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
    fill: #FFFFFF;
  }
</style>

  <script>
    async function quickchart(key) {
      const charts = await google.colab.kernel.invokeFunction(
          'suggestCharts', [key], {});
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-07a51af4-f15e-483f-ab61-71d08059fb01 button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>
    </div>
  </div>





```python
# Remove rows with NaN values
df_cleaned = df_merged.dropna()
df_cleaned.head()
```





  <div id="df-3b9ddb3d-0879-49dc-ae71-b2dda7ada25f" class="colab-df-container">
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
      <th>Video title</th>
      <th>thumbnail</th>
      <th>Impressions click-through rate (%)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>When you want to crochet and you have a baby</td>
      <td>https://i.ytimg.com/vi/9ePFI7814Rc/default.jpg</td>
      <td>1.26</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Crochet Leaves</td>
      <td>https://i.ytimg.com/vi/jx2ojGTX854/default.jpg</td>
      <td>4.57</td>
    </tr>
    <tr>
      <th>4</th>
      <td>How to crochet pet collar | crochet tulips | B...</td>
      <td>https://i.ytimg.com/vi/M5pbgRzZs6w/default.jpg</td>
      <td>4.39</td>
    </tr>
    <tr>
      <th>5</th>
      <td>How to wrap flowers | crochet flower bouquet</td>
      <td>https://i.ytimg.com/vi/rBFqpv-m6gc/default.jpg</td>
      <td>4.69</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Crochet for beginners: How to crochet scrunchi...</td>
      <td>https://i.ytimg.com/vi/2hPsxSXwsf8/default.jpg</td>
      <td>3.11</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-3b9ddb3d-0879-49dc-ae71-b2dda7ada25f')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    .colab-df-buttons div {
      margin-bottom: 4px;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

    <script>
      const buttonEl =
        document.querySelector('#df-3b9ddb3d-0879-49dc-ae71-b2dda7ada25f button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-3b9ddb3d-0879-49dc-ae71-b2dda7ada25f');
        const dataTable =
          await google.colab.kernel.invokeFunction('convertToInteractive',
                                                    [key], {});
        if (!dataTable) return;

        const docLinkHtml = 'Like what you see? Visit the ' +
          '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
          + ' to learn more about interactive tables.';
        element.innerHTML = '';
        dataTable['output_type'] = 'display_data';
        await google.colab.output.renderOutput(dataTable, element);
        const docLink = document.createElement('div');
        docLink.innerHTML = docLinkHtml;
        element.appendChild(docLink);
      }
    </script>
  </div>


<div id="df-1c5fbc76-1342-453c-92bc-b16a6c5f356f">
  <button class="colab-df-quickchart" onclick="quickchart('df-1c5fbc76-1342-453c-92bc-b16a6c5f356f')"
            title="Suggest charts."
            style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
  </button>

<style>
  .colab-df-quickchart {
    background-color: #E8F0FE;
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: #1967D2;
    height: 32px;
    padding: 0 0 0 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: #E2EBFA;
    box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: #174EA6;
  }

  [theme=dark] .colab-df-quickchart {
    background-color: #3B4455;
    fill: #D2E3FC;
  }

  [theme=dark] .colab-df-quickchart:hover {
    background-color: #434B5C;
    box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
    filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
    fill: #FFFFFF;
  }
</style>

  <script>
    async function quickchart(key) {
      const charts = await google.colab.kernel.invokeFunction(
          'suggestCharts', [key], {});
    }
    (() => {
      let quickchartButtonEl =
        document.querySelector('#df-1c5fbc76-1342-453c-92bc-b16a6c5f356f button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>
    </div>
  </div>





```python
# Export merged dataframe to csv file and download it from colab folder for model training in next step
df_merged.to_csv('thumbnail_ctr.csv', index=False)
```
