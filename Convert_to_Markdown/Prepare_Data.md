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

Download csv file of click-through rate from youtube studio (Youtube studio -> Analytics -> Advanced mode -> Export current view -> Comma-seperated values (.csv)), because the Youtube API I used only allow access to public information. You can use another API to get access to creator's data but this is a minimal product.

![Download CTR data from Youtube Studio](images/youtube_analytic.png "Download CTR data from Youtube Studio")

And upload the `Table data.csv` to the colab by drag and drop it in the left *Files* sections of colab.


```python
# Read the CSV file into a Pandas DataFrame
df_ctr = pd.read_csv('Table data.csv')
df_ctr.head()
```


```python
# Rename the df 'title' column to the same name of df_ctr whihch is 'Video title' for merging purpose
df = df.rename(columns={'title': 'Video title'})
```


```python
# Merge the DataFrames based on the video title
df_merged = pd.merge(df, df_ctr[['Video title', 'Impressions click-through rate (%)']], on='Video title', how='left')
df_merged.head()
```


```python
# Remove rows with NaN values
df_cleaned = df_merged.dropna()
df_cleaned.head()
```





  <div id="df-accbe3af-2c08-4d16-bd4c-382bf5f1866d" class="colab-df-container">
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
    <button class="colab-df-convert" onclick="convertToInteractive('df-accbe3af-2c08-4d16-bd4c-382bf5f1866d')"
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
        document.querySelector('#df-accbe3af-2c08-4d16-bd4c-382bf5f1866d button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-accbe3af-2c08-4d16-bd4c-382bf5f1866d');
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


<div id="df-add39e28-43b3-48c4-b7ff-e6ce066f5eeb">
  <button class="colab-df-quickchart" onclick="quickchart('df-add39e28-43b3-48c4-b7ff-e6ce066f5eeb')"
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
        document.querySelector('#df-add39e28-43b3-48c4-b7ff-e6ce066f5eeb button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>
    </div>
  </div>





```python
# Export merged dataframe to csv file
df_merged.to_csv('thumbnail_ctr.csv', index=False)
```

You can find the exported file in the files section of the Colab as thumbnail_ctr.csv , and you can right-click on it (or click on the three dots next to it) and then download it for model training in next step.

For blogging reason, I converted this notebook to markdown with nbconvert. Therefore, markdown file can be rendered in my personal [website](chuhaoliu.com) hosted by Github Page.

You can need to download this notebook and upload it to the folder sections in colab for the below code to run. Details shows [here](https://www.python-engineer.com/posts/convert-colab-markdown/). For some reason, nbconvert converts output of pandas dataframe (e.g. pd.head()) with html scripts. So I deleted the previous pd.head() output and only shows the last one by mannually deleted unwanted html script shown in converted markdown file.


```python
!jupyter nbconvert --to markdown Prepare_Data.ipynb
```
