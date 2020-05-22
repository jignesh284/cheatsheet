
## Python Lambda Boilerplate
```py
import json

def lambda_handler(event, context):
  #TODO: implement
  
  return {
    'status_code': 200,
    'body': json.dumps('Hello from Aws')
  }
```

## lambda reading number of s3 buckets 
```py
import json
import boto3  # AWS SDK for Python

s3 = boto3.resource('s3')

def lambda_handler(event, context):
  #TODO: implement
  bucket_list = []
  
  for bucket in s3.buckets.all():
    print(bucket.name)
    bucket_list.append(bucket.name)
    
  return {
    'status_code' : 200,
    'body': bucket_list
  }
```

## lambda reading an item from dynamoDB
```py
import json
import boto3

dynamodb = boto3.resource('dynamodb')
planetTable = dynamodb.Table('planet')

def lambda_handler(event, context):
  #TODO: implementation
  response = planetTable.get_item(
    key = {
      'id': 'value'
    }
  )
  
  print(response)
  
  return {
    'status_code': 200,
    'body': response
  }
```

## lambda wirting an item to dynamoDB
```py
import json
import boto3

dynamodb = boto3.resource('dynamodb')
planetTable = dynamodb.Table('planet')

def lambda_handler(event, context):
  #TODO: implementation
  response = planetTable.set_item(
    Item = {
      'id': 'value',
      'temp': 'cold',
       ...
    }
  )
  
  response = {
    'message': 'Item added'
  }
  
  return {
    'status_code': 200,
    'body': response
  }
```

