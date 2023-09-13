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
## Reading a dataset and more

    ```python

    df_pyspark = spark.read.csv("test1.csv")
    #another way to read this
    spark.read.option('header', 'true').csv("test1.csv")
    df_pyspark  #prints csv file
    df_pyspark.show() 

    #prints the schema
    df_pyspark.printSchema()
    ```

## Part 1 - Basics

    ```python
    #Do the same to initialize the spark as above
    #Read the dataset
    df_pyspark = spark.read.option('header', 'true').csv('test1.csv', inferSchema=True) or spark.read.csv('test1.csv', header=True, inferSchmea=True)
    type(df_pyspark) #data frame

    #To get the columns
    df_pyspark.columns()
    
    #To get the first 3 rows
    df_pyspark.head(3)

    #To get only one column
    df_pyspark.select('Name').show()

    #To get multiple column
    df_pyspark.select('Name1', 'Name2').show()

    #To check the data types of the columns
    df_pyspark.dtypes

    #Describe
    df_pyspark.describe().show()

    #Adding columns in data frame which will have value as oldColumnName value + 2
    df_pyspark.withColumn('newColumnName', df_pyspark['oldColumnName'] + 2)

    #Drop the columns in data frame
    df_pyspark.drop('columnName')

    #Rename the columns
    df_pyspark.withColumnRenamed('oldName', 'newName')


    
    ```