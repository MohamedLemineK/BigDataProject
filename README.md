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

### How does it work ?

#### <ins>1. Analyzing the texts</ins>

  The code first analyzes the text and creates a dataframe containing the `n` most common words in a text using the function `mostcommonwords(path,n)`. Its 
arguments are the `path` where the file is located and the number `n` of words you would like to keep in your _dataframe_. Here we chose to select the top **10** 
most common words.

  To make sure our _dataframe_ is meaningful the function removes all **punctuation** and all **stopwords**. In a future development, we may 
consider how `lemming` and `stemming` may have improved the model. These are techniques, we have used in a [different project relating to text analysis.](github.com/mohamedLemineK/Sentiment-Analysis) 

We then apply the function to the 6 `.txt` file contained in `/FileStore/pos/`  which results in the creation of 6 dataframes each containing **10** words. 

```
cv994_12270 = mostcommonwords('FileStore/pos/cv994_12270.txt',10)
cv995_21821 = mostcommonwords('FileStore/pos/cv995_21821.txt',10)
cv996_11592 = mostcommonwords('FileStore/pos/cv996_11592.txt',10)
cv997_5046 = mostcommonwords('FileStore/pos/cv997_5046.txt',10)
cv998_14111 = mostcommonwords('FileStore/pos/cv998_14111.txt',10)
cv999_13106 = mostcommonwords('FileStore/pos/cv999_13106.txt',10)
```

#### <ins>2. Forming the committees</ins>

  Next, we put all the _dataframes_ into a list called `dataframes` as well as all their names into a list called `names` and then assign an attribute `['name']` to
all the _dataframes_ using the function `nomenclatura(frames,names)`. This simple function takes only two arguments:

- the _list_ of *dataframes* to be labeled in `frames`
- the _list_ of *names* to be given in `names`

  This seemingly insignificant step is critical for the future management of files.

  Once this is done, the function `gathering(frames)` will be applied to the list of _dataframes_. This function is in charge of forming **committees**. Here, a 
**committee**, similarly to its human counterpart, is a group of texts discussing a similar topic. The function `gathering(frames)` will create a _dictionnary_ containing
the list of **committees** and the name of the _dataframes_ that are **members** of each **committee**. The name of the _dataframes_ is necessarily the same as the name
of the file of which it originated.

#### <ins>3. Moving the files into their committees</ins>

  The last function is `directorycreation(dictionnary,source,destination='/FileStore')` is responsible for creating and filling the different directories reprensenting
each **committee**. It takes 3 arguments: 

- The `dictionnary` which lists all the files contained in each **committee**
- The `source` of files. A _string_ containing the path where the text files to be assembled are located. **WARNING : MUST ALWAYS END WITH `\`**
- The `destination` path. A _string_ containing the path where the directories are to be stored. Default value is `/FileStore`
  
  Once it has been executed directories will be created and the files will be placed accordingly.  






