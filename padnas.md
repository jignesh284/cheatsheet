  
 ## Pandas Basics
 
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

  # iteration through rows
  for index, rows in df.iterrows():
      print(index, row)

  
  # get high level starts on frame (mean, sd)
  df.describe()
  
  # sort by column
  df.sort_values('Column1', ascending=false)
  df.sort_values(['Column1', 'Column2'], ascending=[1, 0])
  
  # row wise summmation (axis=0 => vertically, axis=1 => Horizontally )
  df['total'] = df['column1'] + df['column2']+df['column3']
  df['total'] = df.iloc[:, c1:c4].sum(axis=1)
  
  # drop a column
  df = df.drop(columns=['total'])
  
  
  
  #  *******: Filtering Data :********** (Loc finding specific data in dataframe)
  df.loc[df["column1"] == "value1"]
  df.loc[ (df["column1"] == "value1") &  (df["column2"] > "value2") ] 
  df.loc[ (df["column1"] == "value1") |  (df["column2"] == "value2") ] 
  df.loc[ ~df["column1"].str.contains('substring')] # gets all columns which donot contains substring
  
  # gets all columns which based on regex 
  df.loc[ ~df["column1"].str.contains('sub1|sub2', flags=re.I, regex=True)] 
  
  
  # Conditional Changes
  df.loc[df.["column1"] == 'val1', "column1"] = "new_val1"
  df.loc[df.["Total"] > 500, ["Generation", "Legendary"]] = ["val1", "val2"]
  
  # Groupby (Aggregation)
  df.groupby(['column1']).mean().sort_values('Col', ascending=False)
  df.groupby(['column1']).sum()
  
  df['count'] = 1
  df.groupby(['column1', 'column2']).count()['count']
  
    
  #Reset Index
  df.reset_index(drop=true, inplace=true)
  
  # save df to directory
  df.to_csv('path', index=false)
  df.to_excel('path', index=false)
  df.to_csv('path', index=false, sep='\t')
  
  # work with large amount of data
  new_df = pd.DateFrames(columns=df.columns) 
  
  for df in pd.read_csv('filename.csv', chunksize=100000)
    results = df.groupby(['Columns1']).count()
    
    new_df = pd.concat([new_df, results])
  
 ```
