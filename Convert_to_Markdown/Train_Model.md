For deep learning training, you need to first **change the Colab runtime** to `T4 GPU` in the upper right corner.

![Change Colab Runtime to T4 GPU](/images/Change_Colab_Runtime.png "Change Colab Runtime to T4 GPU")

Upload `thumbnail_ctr.csv` to Colab by drag and drop into the left *Files* section.


```python
import pandas as pd

# Read the CSV file into a Pandas DataFrame
df = pd.read_csv('thumbnail_ctr.csv')

# Delete NaN rows
df = df.dropna()
# Reindex the DataFrame
df = df.reset_index(drop=True)
df.head()
```





  <div id="df-8af9edb3-d195-4b7e-99b3-626362f788c1" class="colab-df-container">
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
      <td>When you want to crochet and you have a baby</td>
      <td>https://i.ytimg.com/vi/9ePFI7814Rc/default.jpg</td>
      <td>1.26</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Crochet Leaves</td>
      <td>https://i.ytimg.com/vi/jx2ojGTX854/default.jpg</td>
      <td>4.57</td>
    </tr>
    <tr>
      <th>2</th>
      <td>How to crochet pet collar | crochet tulips | B...</td>
      <td>https://i.ytimg.com/vi/M5pbgRzZs6w/default.jpg</td>
      <td>4.39</td>
    </tr>
    <tr>
      <th>3</th>
      <td>How to wrap flowers | crochet flower bouquet</td>
      <td>https://i.ytimg.com/vi/rBFqpv-m6gc/default.jpg</td>
      <td>4.69</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Crochet for beginners: How to crochet scrunchi...</td>
      <td>https://i.ytimg.com/vi/2hPsxSXwsf8/default.jpg</td>
      <td>3.11</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-8af9edb3-d195-4b7e-99b3-626362f788c1')"
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
        document.querySelector('#df-8af9edb3-d195-4b7e-99b3-626362f788c1 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-8af9edb3-d195-4b7e-99b3-626362f788c1');
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


<div id="df-f9ca0fe2-3233-4a5f-936a-9963a5453c59">
  <button class="colab-df-quickchart" onclick="quickchart('df-f9ca0fe2-3233-4a5f-936a-9963a5453c59')"
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
        document.querySelector('#df-f9ca0fe2-3233-4a5f-936a-9963a5453c59 button');
      quickchartButtonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';
    })();
  </script>
</div>
    </div>
  </div>




Blow is a code example of using fast.ai library to download and show images from url.


```python
from fastdownload import download_url
dest = 'thumbnail.jpg'
download_url(df['thumbnail'][2], dest, show_progress=False)

from fastai.vision.all import *
im = Image.open(dest)
im.to_thumb(256,256)
```




    
![png](Train_Model_files/Train_Model_3_0.png)
    




```python
average_value = df['Impressions click-through rate (%)'].mean()
average_value
```




    2.716734693877551



Seperate datasest into two caterogies: **below average** and **above average**.


```python
below_average_df = df[df['Impressions click-through rate (%)'] < average_value]
above_average_df = df[df['Impressions click-through rate (%)'] >= average_value]
```

Dowload images from two categories into two different folders named **above_average** and **below_average**. Fast.ai library will use folder's name to lable the images for training.


```python
searches = 'below_average','above_average'
path = Path('thumbnail_cover_image')

for o in searches:
    dest = (path/o)
    dest.mkdir(exist_ok=True, parents=True)
    if o == 'below average':
      o_df = below_average_df
    else:
      o_df = above_average_df

    download_images(dest, urls=o_df['thumbnail'])
    resize_images(path/o, max_size=400, dest=path/o)
```


```python
#Delete unvalid image links
failed = verify_images(get_image_files(path))
failed.map(Path.unlink)
len(failed)
```




    0




```python
#Build fast.ai datablock for next step
dls = DataBlock(
    blocks=(ImageBlock, CategoryBlock),
    get_items=get_image_files,
    splitter=RandomSplitter(valid_pct=0.2, seed=42),
    get_y=parent_label,
    item_tfms=[Resize(192, method='squish')]
).dataloaders(path, bs=32)

dls.show_batch(max_n=6)
```


    
![png](Train_Model_files/Train_Model_10_0.png)
    


**Fine tune** the existing **Resnet** model which has been pre-trained on millions of images. **Fine tune** method only train the last layer of the pre-trained model for the user's dataset. Therefore, it saves time.


```python
learn = vision_learner(dls, resnet18, metrics=error_rate)
learn.fine_tune(3)
```

    /usr/local/lib/python3.10/dist-packages/torchvision/models/_utils.py:208: UserWarning: The parameter 'pretrained' is deprecated since 0.13 and may be removed in the future, please use 'weights' instead.
      warnings.warn(
    /usr/local/lib/python3.10/dist-packages/torchvision/models/_utils.py:223: UserWarning: Arguments other than a weight enum or `None` for 'weights' are deprecated since 0.13 and may be removed in the future. The current behavior is equivalent to passing `weights=ResNet18_Weights.IMAGENET1K_V1`. You can also use `weights=ResNet18_Weights.DEFAULT` to get the most up-to-date weights.
      warnings.warn(msg)
    Downloading: "https://download.pytorch.org/models/resnet18-f37072fd.pth" to /root/.cache/torch/hub/checkpoints/resnet18-f37072fd.pth
    100%|██████████| 44.7M/44.7M [00:00<00:00, 213MB/s]




<style>
    /* Turns off some styling */
    progress {
        /* gets rid of default border in Firefox and Opera. */
        border: none;
        /* Needs to be in here for Safari polyfill so background images work as expected. */
        background-size: auto;
    }
    progress:not([value]), progress:not([value])::-webkit-progress-bar {
        background: repeating-linear-gradient(45deg, #7e7e7e, #7e7e7e 10px, #5c5c5c 10px, #5c5c5c 20px);
    }
    .progress-bar-interrupted, .progress-bar-interrupted::-webkit-progress-bar {
        background: #F44336;
    }
</style>




<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: left;">
      <th>epoch</th>
      <th>train_loss</th>
      <th>valid_loss</th>
      <th>error_rate</th>
      <th>time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1.438015</td>
      <td>1.381293</td>
      <td>0.500000</td>
      <td>00:07</td>
    </tr>
  </tbody>
</table>




<style>
    /* Turns off some styling */
    progress {
        /* gets rid of default border in Firefox and Opera. */
        border: none;
        /* Needs to be in here for Safari polyfill so background images work as expected. */
        background-size: auto;
    }
    progress:not([value]), progress:not([value])::-webkit-progress-bar {
        background: repeating-linear-gradient(45deg, #7e7e7e, #7e7e7e 10px, #5c5c5c 10px, #5c5c5c 20px);
    }
    .progress-bar-interrupted, .progress-bar-interrupted::-webkit-progress-bar {
        background: #F44336;
    }
</style>




<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: left;">
      <th>epoch</th>
      <th>train_loss</th>
      <th>valid_loss</th>
      <th>error_rate</th>
      <th>time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1.690220</td>
      <td>1.451846</td>
      <td>0.500000</td>
      <td>00:01</td>
    </tr>
    <tr>
      <td>1</td>
      <td>1.592969</td>
      <td>1.636217</td>
      <td>0.500000</td>
      <td>00:00</td>
    </tr>
    <tr>
      <td>2</td>
      <td>1.496134</td>
      <td>1.836272</td>
      <td>0.600000</td>
      <td>00:00</td>
    </tr>
  </tbody>
</table>


Upload an example.jpg to text model


```python
is_above_average,_,probs = learn.predict(PILImage.create('example.jpg'))
print(f"This is a: {is_above_average}.")
print(f"Probability its click-through rate above average: {probs[0]:.4f}")
```



<style>
    /* Turns off some styling */
    progress {
        /* gets rid of default border in Firefox and Opera. */
        border: none;
        /* Needs to be in here for Safari polyfill so background images work as expected. */
        background-size: auto;
    }
    progress:not([value]), progress:not([value])::-webkit-progress-bar {
        background: repeating-linear-gradient(45deg, #7e7e7e, #7e7e7e 10px, #5c5c5c 10px, #5c5c5c 20px);
    }
    .progress-bar-interrupted, .progress-bar-interrupted::-webkit-progress-bar {
        background: #F44336;
    }
</style>







    This is a: above_average.
    Probability its click-through rate above average: 0.8472


Export the fine-tuned model and download from the **Files** section of colab for next step.


```python
learn.export('model.pkl')
```

Download and upload this notebook to Colab. Convert it to markdown using nbconvert for blogging reason.


```python
!jupyter nbconvert --to markdown Train_Model.ipynb
```
