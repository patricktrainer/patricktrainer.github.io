---
date: '2021-01-01'
draft: false
tags: '[]'
title: How-to-Create-Scalable-Data-Pipelines-with-Python
---

# How-to-Create-Scalable-Data-Pipelines-with-Python

The definition of the message structure is available [online](https://www.mediawiki.org/wiki/Manual:RCFeed), but here’s a sample message:
```
event: message
id: [{"topic":"eqiad.mediawiki.recentchange","partition":0,"timestamp":1532031066001},{"topic":"codfw.mediawiki.recentchange","partition":0,"offset":-1}]data: {"event": "data", "is": "here"}
```
Server Side Events (SSE) are defined by the World Wide Web Consortium (W3C) as part of the HTML5 definition.
You have two choices:
- Download the pre-built Data Pipeline runtime environment (including Python 3.6) for [Linux](https://platform.activestate.com/Pizza-Team/Data-Pipeline/distributions?utm_source=activestate.com&utm_medium=referral&utm_content=blog-how-to-create-scalable-data-pipelines-python&utm_campaign=user-acquisition) or [macOS](https://platform.activestate.com/Pizza-Team/Data-Pipeline-Mac/distributions?utm_source=activestate.com&utm_medium=referral&utm_content=blog-how-to-create-scalable-data-pipelines-python&utm_campaign=user-acquisition) and install it using the [State Tool](https://platform.activestate.com/dev-tools?utm_source=activestate.com&utm_medium=referral&utm_content=blog-how-to-create-scalable-data-pipelines-python&utm_campaign=user-acquisition) into a virtual environment, or
- Follow the instructions provided in my [Python Data Pipeline](https://github.com/nickmancol/python_data_pipeline) Github repository to run the code in a containerized instance of JupyterLab.
Once you’ve installed the Moto server library and the [AWS CLI](https://aws.amazon.com/es/cli/) client, you have to create a credentials file at ~/.aws/credentials with the following content in order to authenticate to the AWS services:
```
[default]
AWS_ACCESS_KEY_ID = foo
AWS_SECRET_ACCESS_KEY = bar
```
You can then launch the SQS mock server from your terminal with the following command:
```
moto_server sqs -p 4576 -H localhost
```
If everything is OK, you can create a queue in another terminal using the following command:
```
aws --endpoint-url=http://localhost:4576 sqs create-queue --queue-name sse_queue --region us-east-1
```
This will return the URL of the queue that we’ll use in our SSE Consumer component.
To extract just the JSON, we’ll use the [SSEClient](https://pypi.org/project/sseclient/) Python library and code a simple function to iterate over the message stream to pull out the JSON payload, and then place it into the recently created Message Queue using the AWS [Boto3](https://boto3.amazonaws.com/v1/documentation/api/latest/index.html) Python library:
```
import boto3
import json
from sseclient import SSEClient as EventSource
#SQS client library
sqs = boto3.client('sqs'
, endpoint_url="http://localhost:4576" #only for test purposes
, use_ssl=False #only for test purposes
, region_name='us-east-1')
queue_url = 'http://localhost:4576/queue/sse_queue'
def catch_events():
url = 'https://stream.wikimedia.org/v2/stream/recentchange'
for event in EventSource(url):
if event.event == 'message':
try:
message = json.loads(event.data)
except ValueError:
pass
else:
enqueue_message( json.dumps(message) )
def enqueue_message( message ):
response = sqs.send_message(
QueueUrl = queue_url,
DelaySeconds=1,
MessageBody = message
)
print('\rMessage %s enqueued' % response['MessageId'], sep=' ', end='', flush=True
)
if __name__== "__main__":
catch_events()
```
This component will run indefinitely, consuming the SSE events and printing the id of each message queued.
## Processing Data Streams with Python
In order to explore the data from the stream, we’ll consume it in batches of 100 messages.
Next, the process_batch function will clean the message’s body and enrich each one with their respective ReceiptHandle*,* which is an attribute from the Message Queue that uniquely identifies the message:
```
def process_batch( messages ):
global list_msgs
for message in messages:
d = json.loads(message['Body'])
#This just cleans the message's body from non-desired data
clean_dict = { key:(d[key] if key in d else None) for key in map_keys }
#We enrich our df with the message's receipt handle in order to clean it from the queue
clean_dict['ReceiptHandle'] = message['ReceiptHandle']
list_msgs.append(clean_dict)
if len( list_msgs ) >= 100:
print('Batch ready to be exported to the Data Lake')
to_data_lake( list_msgs )
list_msgs = []
```
This function is an oversimplification.
Finally, if the list contains the desired batch size (i.e., 100 messages), our processing function will persist the list into the data lake, and then restart the batch:
```
def to_data_lake( df ):
batch_df = pd.DataFrame( list_msgs )
csv = batch_df.to_csv( index=False )
filename = 'batch-%s.csv' % df[0]['id']
#csv to s3 bucket
s3.Bucket('sse-bucket').put_object( Key=filename, Body=csv, ACL='public-read' )
print('\r%s saved into the Data Lake' % filename, sep=' ', end='', flush=True
)
remove_messages( batch_df )
```
The to_data_lake function transforms the list into a Pandas DataFrame in order to create a simple CSV file that will be put into the S3 service using the first message of the batch’s ReceiptHandle as a unique identifier.
