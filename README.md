# BigDataProject
Project to be made for the Big Data class ECE ING4 App

In this project, our aim is to gather text files sharing a common theme. To do so we look at the most common words in each text.
If two files share words that are frequent in both texts, we may consider them to be part of a same theme or to be 
discussing a similar topic. 

The main technology used for this project was Apache Spark via the interface of Databricks. Based on this, we developed a python code capable
of analyzing files and then assembling them into specific directories based on a general theme. To run this code we are storing a directory
on the Databricks File System conatining multiple movie reviews to be used as an example. The code exploits some of the Databricks tools adapted to 
the treatment of files such as the Databricks utilisties package. Suchly, the code may not be run on any IDE or any system as it calls for very
specific ressources. 

