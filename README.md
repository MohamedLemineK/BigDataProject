# BigDataProject

## Text File Relocation Project : Big Data class ECE ING4 App

### Overview

  In this project, our aim is to gather text files sharing a common theme. To do so, we look at the most common words in each text.
If two files share words that are frequent in both texts, we may consider them to be part of a same theme or to be 
discussing a similar topic. 

  The main technology used for this project is **Apache Spark** via the interface of **Databricks**. Based on this, we developed a python code capable
of ***analyzing*** files and then ***assembling*** them into specific directories based on a ***general theme***. 

  To run this code we are storing a directory on the Databricks File System containing multiple movie reviews to be used as an example. The code exploits some of the Databricks tools adapted to the treatment of files such as the **Databricks Utilities** package.
  
  Suchly, the code may not be run on any IDE or any system as it calls for very specific ressources. Intructions are to be presented in the following section.

### Instructions

To run this project you need to :
- Log into your [Databricks workspace](https://accounts.cloud.databricks.com/login?tuuid=1f15a7e6-a8ea-4d42-856d-dea4fac9358b)
- Upload the `/pos` directory to your **DBFS** `/FileStore` so that all texts are contained within `/FileStore/pos/`
- Import the notebook `Gather.ipynb`
- Run all cells of the notebook `Gather.ipynb` with any compute cluster of your choosing

### How it works ?

1. Analyzing the texts

  The code first analyzes the text and creates a dataframe containing the `n` most common words in a text using the function `mostcommonwords(path,n)`. Its 
arguments are the `path` where the file is located and the number `n` of words you would like to keep in your _dataframe_. Here we chose to select the top **10** 
most common words.

  To make sure our _dataframe_ is meaningful the function removes all **punctuation** and all **stopwords**. In a future development, we may 
consider how `lemming` and `stemming` may have improved the model. These are techniques, we have used in a [different project relating to text analysis.](github.com/mohamedLemineK/Sentiment-Analysis) 

We then apply the function to the 6 `.txt` file contained in `/FileStore/pos/`  which results in the creation of 6 dataframes each containing **10** words. 

2. Forming the committees

  Next, we put all the _dataframes_ into a list called `dataframes` as well as all their names into a list called `names` and then assign an attribute `['name']` to
all the _dataframes_ using the function `nomenclatura(frames,names)`. This simple function takes only two arguments the list of *dataframes* to be labeled in `frames`
and the list of *names* to be given in `names`. This seemingly insignificant step is critical for the future management of files. 

3. Moving the files into their committees







