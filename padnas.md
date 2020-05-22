  
 ## pandas commands
 
 ```py
 # read a csv file or excel
 df = pd.read_csv('data/survey_results_public.csv', delimiter=',')
 df = pd.read_excel('data/survey_results_public.xls ')
 
 # structure of data in dataframe
 people = {
  "column1" : ["value1", "value2", "value3"]
  "column2" : ["value4", "value5", "value6"]
  "column3" : ["value7", "value8", "value9"]
 }
 
 # create dataframe from python dictionary
 df = pd.DataFrame(people) 
 
 # get the shape of the file
 df.shape
 
 # set option
 df.set_option('display.max_columns', 89)
 
 # get top 10 or last 10 rows
 df.head(10),  df.tail(10)

 
 # get series from data frame (series have more functionality in comp to dataframes)
  df['column1'] or df.columns or df['column1'][0:5]
  
  
  # selecting multiple columns (returns the filtered dataframe )
  df[['column1', 'column2']]
  
  # get the dataframe row(returns series) search by integer location
  df.iloc[0]  
  
  #example array1=rowsIndex, array2=columnIndex
  df.iloc[[0, 1], 2] or df.iloc[[0, 1], [2,3]]

 ```
