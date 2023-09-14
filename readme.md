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

## Day 2 

```python

        df_pyspark.na.drop().show()

        #using how - any or all
        #thresh=x- row should contain atleast x non null values to not get deleted
        #subset will check in only mentioned columns
        df_pyspark.na.drop(how="all or any", thresh=2, subset=['columnName']).show()
    
        #Filling the null values with missing values
        df_pyspark.na.fill("Missing values").show()

        #Filter operations
        df_pyspark.filter("columnName<=2000").show()      
        df_pyspark.filter("columnName<=2000").select(['Name', 'Age']).show()
        df_pyspark.filter("col1 < 10 &,| col2 > 12").show()
        df_pyspark.filter(~(df_pyspark["colName"] == 1000)).show()

        #Pyspark GroupBy and Aggregrate Functions

        df_pyspark.groupBy('Name').sum().show()

        #Groupby Departments which gives mean salary
        df_pyspark.groupBy('Departments').mean().show()

        #Groupby Departments which gives count of the departments
        df_pyspark.groupBy('Departments').mean().show()

        #Directly applying aggregrate functions
        df_pyspark.agg({'Salary':'sum'}).show()

```

## Task - I have a reducer code written in php, I need to convert it into pyspark job.

* Setup Spark 
* Importing spark libraries - 

```python 

    #Import spark libraries

    from pyspark.sql import SparkSession
    spark = SparkSession.builder.appName("Reducer To Spark").getOrCreate()

    #Reading the input data

    input_data = spark.read.text("input_file.txt")

    #Defining the Reducer logic
    from pyspark.sql.functions import col
    def reducer_function(df):
        #Write logic here of reducer
        result = df.groupBy("key_column").agg({"value_column": "sum"})
        return result


    #Apply the reducer function
    output_data = reducer_function(input_data) #output data jo hoga, woh ek dataframe hoga, toh yahan se hum easily xls, csv mein save kr skte hain

    #Save output data 
    output_data.write.csv("outfut file.csv")

    #Stopping spark session
    spark.stop()
```
