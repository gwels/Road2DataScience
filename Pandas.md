
# Loading data into Python
When working with Python and data, loading data into a dataframe is one of the first steps to take. Using the Pandas package is a great way to load the most common datasources. In this tutorial we will load data from three types of datasources: 
- csv-file
- excel-file
- querying a SQL-database


## Importing packages 
Python's base functionality can be greatly extended by using packages. These packages enhance Python on different areas like: 
- Data visualisation 
- Data transformation 
- Statistical functions 

For this tutorial we will use two packages:
- pandas, will be used to load the data, create a dataframe for datastorage and data export
- pyodbc, to intiate a SQL engine for one of the data imports

We can load the two packages with this code:



```python
import pandas as pd
import pyodbc
```


## Importing data from a CSV file 
Comma Separated Values (CSV) is a file type used to exchange data between systems. Most database systems are able to import and export data in the CSV format. A typical CSV file contains a long string of data seperated by a comma, tabs or a semicolon. 

Using the pandas package we can load the CSV into a dataframe. Before we do the dataload, we need to specify a couple of variables. 



```python
file_location = "./Employee.csv"
```


```python
column_names = ("id", "firstname", "lastname")
```


```python
separator = ";"
```


The variables contain the file location, the column names and the separator. Depending on the structure of the CSV these variables can be changed for a correct dataload. 

The next step is loading the file into a dataframe named df. We use a pandas function: read_csv() and pass it the variables file_location, column_names and separator. After the succesfull load we print the content of the freshly created df. 



```python
df = pd.DataFrame(pd.read_csv (filepath_or_buffer = file_location, sep = separator,  names = column_names))
```


```python
df
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
      <th>id</th>
      <th>firstname</th>
      <th>lastname</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>John</td>
      <td>Snow</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Sindy</td>
      <td>Buzzard</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Easter</td>
      <td>Eaddy</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Simon</td>
      <td>Dore</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Lacie</td>
      <td>Ingham</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Carlee</td>
      <td>Cavazos</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Helena</td>
      <td>Shiver</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Marla</td>
      <td>Putman</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>Marc</td>
      <td>Schoenborn</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>Daniell</td>
      <td>Barba</td>
    </tr>
  </tbody>
</table>
</div>



## Importing data from an Excel file 
Another widely used data exchange filetype is Excel. In this case, we do not need to specify the seperator because seperators are not used in the Excel filetype. We do need to specify a file location and the columnnames. Before we are able to load the data we need to change the value of file_location to the Excel file. 

The pandas packages provides a function to facilitate the data load: read_excel

In read_excel we specifiy 3 parameters:
    io, contains the file location.
    header, specify as None, otherwise the first row in the sheet is used as a name field.
    names, contains the name variable.

After the data load we print the df. 



```python
file_location = "./Employee.xlsx"
```


```python
df = pd.DataFrame(pd.read_excel(io = file_location, header = None ,  names = column_names))
```


```python
df
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
      <th>id</th>
      <th>firstname</th>
      <th>lastname</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>John</td>
      <td>Snow</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Sindy</td>
      <td>Buzzard</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Easter</td>
      <td>Eaddy</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Simon</td>
      <td>Dore</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Lacie</td>
      <td>Ingham</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Carlee</td>
      <td>Cavazos</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Helena</td>
      <td>Shiver</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Marla</td>
      <td>Putman</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>Marc</td>
      <td>Schoenborn</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>Daniell</td>
      <td>Barba</td>
    </tr>
  </tbody>
</table>
</div>



## Importing data from SQL Server
The last data import explained in this blogpost is from a SQL Server database. A SQL Server contains one or more databases, the database(s) contain tables. These database servers are used in companies to store data in a table structured way (rows and columns).  

For the SQL server data import we need to use an extra package: pyodbc
Instead of loading a file like with the excel and csv examples we need to connect to the SQL Server instance. The pyodbc package will be used to initiate the connection.

Before we can start the load we need to define a couple of variables:
- server, to store the servername
- db, to store the databasename
- sql_conn, to build the connection string
- query, the SQL query to run on the database 



```python
server = "servername"
```


```python
db = "databasename"
```


```python
sql_conn = pyodbc.connect('DRIVER={SQL Server};SERVER=' + server + ';DATABASE=' + db + ";Trusted_Connection=yes")
```


```python
query = ('SELECT id, firstname , lastname FROM [dbo].[employees]')
```


```python
df = pd.DataFrame(pd.read_sql(sql = query, con = sql_conn))
```


```python
df
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
      <th>id</th>
      <th>firstname</th>
      <th>lastname</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>John</td>
      <td>Snow</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Sindy</td>
      <td>Buzzard</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Easter</td>
      <td>Eaddy</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Simon</td>
      <td>Dore</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Lacie</td>
      <td>Ingham</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>Carlee</td>
      <td>Cavazos</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Helena</td>
      <td>Shiver</td>
    </tr>
    <tr>
      <th>7</th>
      <td>8</td>
      <td>Marla</td>
      <td>Putman</td>
    </tr>
    <tr>
      <th>8</th>
      <td>9</td>
      <td>Marc</td>
      <td>Schoenborn</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>Daniell</td>
      <td>Barba</td>
    </tr>
  </tbody>
</table>
</div>



## Conclusion
In this post we experimented with 3 different ways of loading data into a Pandas dataframe. The documentation on the Pandas site http://pandas.pydata.org/pandas-docs/stable/ describes some extra examples about other possible datasources or settings we can use to enhance the dataframe.

Once we loaded data into a Pandas dataframe we can start tranforming, combining, visualising, analysing the data.


