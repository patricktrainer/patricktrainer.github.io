---
                title: Building-Serverless-Python-Apps-Using-AWS-Chalice
                date: 2021-01-01    
                draft: true
                tags: []
               ---


            # Building-Serverless-Python-Apps-Using-AWS-Chalice

**By the end of this tutorial, you’ll be able to**:
- Discuss the benefits of a serverless architecture
- Explore Chalice, a Python serverless framework
- Build a full blown serverless app for a real world use case
- Deploy to Amazon Web Services (AWS) Lambda
- Compare Pure and Lambda functions
**Free Bonus:** 5 Thoughts On Python Mastery, a free course for Python developers that shows you the roadmap and the mindset you'll need to take your Python skills to the next level.## Getting Started With AWS Chalice
[Chalice](https://github.com/aws/chalice/), a Python Serverless Microframework developed by AWS, enables you to quickly spin up and deploy a working serverless app that scales up and down on its own as required using AWS Lambda.Updating policy for IAM role: hello-world-dev
Creating lambda function: hello-world-dev
Creating Rest API
Resources deployed:
- Lambda ARN: arn:aws:lambda:ap-south-1:679337104153:function:hello-world-dev
- Rest API URL: https://fqcdyzvytc.execute-api.ap-south-1.amazonaws.com/api/
```
**Note**: The generated ARN and API URL in the above snippet will vary from user to user.First, let’s include all the import statements:
```
from os import environ as env
# 3rd party imports
from chalice import Chalice, Response
from twilio.rest import Client
from twilio.base.exceptions import TwilioRestException
# Twilio Config
ACCOUNT_SID = env.get('ACCOUNT_SID')
AUTH_TOKEN = env.get('AUTH_TOKEN')
FROM_NUMBER = env.get('FROM_NUMBER')
TO_NUMBER = env.get('TO_NUMBER')
```
Next, you’ll encapsulate the Twilio API and use it to send SMS:
```
app = Chalice(app_name='sms-shooter')
# Create a Twilio client using account_sid and auth token
tw_client = Client(ACCOUNT_SID, AUTH_TOKEN)
@app.route('/service/sms/send', methods=['POST'])
def send_sms():
request_body = app.current_request.json_body
if request_body:
try:
msg = tw_client.messages.create(
from_=FROM_NUMBER,
body=request_body['msg'],
to=TO_NUMBER)
if msg.sid:
return Response(status_code=201,
headers={'Content-Type': 'application/json'},
body={'status': 'success',
'data': msg.sid,
'message': 'SMS successfully sent'})
else:
return Response(status_code=200,
headers={'Content-Type': 'application/json'},
body={'status': 'failure',
'message': 'Please try again!!!'})Updating policy for IAM role: sms-shooter-dev
Creating lambda function: sms-shooter-dev
Creating Rest API
Resources deployed:
- Lambda ARN: arn:aws:lambda:ap-south-1:679337104153:function:sms-shooter-dev
- Rest API URL: https://qtvndnjdyc.execute-api.ap-south-1.amazonaws.com/api/
```
**Note**: The above command succeeds, and you have your API URL in the output as expected.Updating policy for IAM role: sms-shooter-dev
Updating lambda function: sms-shooter-dev
Updating rest API
Resources deployed:
- Lambda ARN: arn:aws:lambda:ap-south-1:679337104153:function:sms-shooter-dev
- Rest API URL: https://fqcdyzvytc.execute-api.ap-south-1.amazonaws.com/api/
```
Do a sanity check by making a curl request to the generated API endpoint:
```
$ curl -H "Content-Type: application/json" -X POST -d '{"msg": "hey mate!!!"}'Now to make this work, we need to make changes to `app.py` as well:
```
# Core imports
from chalice import Chalice, Response
from twilio.base.exceptions import TwilioRestException
# App level imports
from chalicelib import sms
app = Chalice(app_name='sms-shooter')
@app.route('/')
def index():
return {'hello': 'world'}
@app.route('/service/sms/send', methods=['POST'])
def send_sms():
request_body = app.current_request.json_body
if request_body:
try:
resp = sms.send(request_body)
if resp:
return Response(status_code=201,
headers={'Content-Type': 'application/json'},
body={'status': 'success',
'data': resp.sid,
'message': 'SMS successfully sent'})
else:
return Response(status_code=200,
headers={'Content-Type': 'application/json'},
body={'status': 'failure',
'message': 'Please try again!!!'})