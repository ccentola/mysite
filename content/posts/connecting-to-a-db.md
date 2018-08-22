---
{
  "title": "Connecting to a Database using Jupyter Notebooks",
  "subtitle": "Generic subtitle",
  "date": "2018-08-22",
  "slug": "connecting-to-a-db",
  "draft": "true"
}
---
<!--more-->

Connecting to a database is a common issue in data analysis. Often it is easy to create SQL statements, but it can be somewhat cumbersome to convert those statements into useable data without installing some additional software. Jupyter Notebooks offer a convenient way to connect directly to your favorite database without ever having to leave the comfort of your notebook.

In this notebook, I will be demonstrating this functionaity using the iris dataset as sample data and sqlite as my database of choice.


```python
# import libraries
import pandas as pd
import sqlite3
```

```python
# read the CSV
df = pd.read_csv('../data/Iris.csv')
```

First we need to connect to a database and import our data.


```python
# connect to a database
conn = sqlite3.connect('iris.db')

# store your table in the database
df.to_sql('iris', conn, if_exists='replace')
```

```python
# read a SQL Query out of your database and into a pandas dataframe
sql_string = 'SELECT * FROM iris'
df_sql = pd.read_sql(sql_string, conn)
```

```python
df.head()
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
      <th>Id</th>
      <th>SepalLengthCm</th>
      <th>SepalWidthCm</th>
      <th>PetalLengthCm</th>
      <th>PetalWidthCm</th>
      <th>Species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_sql.head()
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
      <th>index</th>
      <th>Id</th>
      <th>SepalLengthCm</th>
      <th>SepalWidthCm</th>
      <th>PetalLengthCm</th>
      <th>PetalWidthCm</th>
      <th>Species</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>5.1</td>
      <td>3.5</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2</td>
      <td>4.9</td>
      <td>3.0</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>3</td>
      <td>4.7</td>
      <td>3.2</td>
      <td>1.3</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>4</td>
      <td>4.6</td>
      <td>3.1</td>
      <td>1.5</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>5</td>
      <td>5.0</td>
      <td>3.6</td>
      <td>1.4</td>
      <td>0.2</td>
      <td>Iris-setosa</td>
    </tr>
  </tbody>
</table>
</div>



Next, using Jupyter magic commands, we can query our database tables using the familiar SQL dialect we all know and love.


```python
%load_ext sql
```

```python
%sql sqlite:///iris.db
```

    'Connected: None@iris.db'




```python
%sql select * from iris limit 10
```

    Done.




<table>
    <tr>
        <th>index</th>
        <th>Id</th>
        <th>SepalLengthCm</th>
        <th>SepalWidthCm</th>
        <th>PetalLengthCm</th>
        <th>PetalWidthCm</th>
        <th>Species</th>
    </tr>
    <tr>
        <td>0</td>
        <td>1</td>
        <td>5.1</td>
        <td>3.5</td>
        <td>1.4</td>
        <td>0.2</td>
        <td>Iris-setosa</td>
    </tr>
    <tr>
        <td>1</td>
        <td>2</td>
        <td>4.9</td>
        <td>3.0</td>
        <td>1.4</td>
        <td>0.2</td>
        <td>Iris-setosa</td>
    </tr>
    <tr>
        <td>2</td>
        <td>3</td>
        <td>4.7</td>
        <td>3.2</td>
        <td>1.3</td>
        <td>0.2</td>
        <td>Iris-setosa</td>
    </tr>
    <tr>
        <td>3</td>
        <td>4</td>
        <td>4.6</td>
        <td>3.1</td>
        <td>1.5</td>
        <td>0.2</td>
        <td>Iris-setosa</td>
    </tr>
    <tr>
        <td>4</td>
        <td>5</td>
        <td>5.0</td>
        <td>3.6</td>
        <td>1.4</td>
        <td>0.2</td>
        <td>Iris-setosa</td>
    </tr>
    <tr>
        <td>5</td>
        <td>6</td>
        <td>5.4</td>
        <td>3.9</td>
        <td>1.7</td>
        <td>0.4</td>
        <td>Iris-setosa</td>
    </tr>
    <tr>
        <td>6</td>
        <td>7</td>
        <td>4.6</td>
        <td>3.4</td>
        <td>1.4</td>
        <td>0.3</td>
        <td>Iris-setosa</td>
    </tr>
    <tr>
        <td>7</td>
        <td>8</td>
        <td>5.0</td>
        <td>3.4</td>
        <td>1.5</td>
        <td>0.2</td>
        <td>Iris-setosa</td>
    </tr>
    <tr>
        <td>8</td>
        <td>9</td>
        <td>4.4</td>
        <td>2.9</td>
        <td>1.4</td>
        <td>0.2</td>
        <td>Iris-setosa</td>
    </tr>
    <tr>
        <td>9</td>
        <td>10</td>
        <td>4.9</td>
        <td>3.1</td>
        <td>1.5</td>
        <td>0.1</td>
        <td>Iris-setosa</td>
    </tr>
</table>



And there you have it: A fast and easy way to integrate SQL knowledge into Jupyter Notebooks!
