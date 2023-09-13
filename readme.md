# Welcome to the pyspark tutorial


## Introduction

* Pyspark data frame similar to panda data frame
* Apache spark is 100 times faster than mapReduce

## Installation and getting started

* Install pyspark using pip install pyspark
* import pyspark
* Create some dataset - excel sheet mein 2 columns bana ke kuch rows add krde

    ```python

    #If you had been working with pandas, we would have imported pandas 
        import pandas as pd
        pd.read_csv('test1.csv') #file we created
    
    ```

* To start spark session, do this 

    ```python

    from pyspark.sql import SparkSession
    spark = SparkSession.builder.appName('Practise').getOrCreate()
    spark  #Prints spark

    ```
    

