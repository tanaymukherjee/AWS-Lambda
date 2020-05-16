# AWS-Lambda
AWS Lambda, a server-less computation service provided by AWS 

In this exercise we try to learn how to use the AWS services - Lambda and Kinesis

## AWS Lambda
AWS Lambda lets you run code without provisioning or managing servers. You pay only for the compute time you consume.
With Lambda, you can run code for virtually any type of application or backend service - all with zero administration. Just upload your code and Lambda takes care of everything required to run and scale your code with high availability. You can set up your code to automatically trigger from other AWS services or call it directly from any web or mobile app.

**Provisioning a Simple Lambda Service:**
- Let’s begin by creating a simple Lambda service for ourselves. Begin by going to AWS Console homepage and typing in “Lambda”.
- Then, click on the Create Function button to go ahead and start the process for making a new lambda function.
- Make sure you have the “blank” item picked and while filling out the fields, ensure you have Python 3.8 chosen.
- Click on the Add trigger button on the left. Then, make sure you choose API Gateway as your trigger.
- In trigger configuration, choose Open for the Security option.

**Lambda Function Configuration**
![lambda](https://user-images.githubusercontent.com/6689256/82111699-f09a3700-9714-11ea-80a3-104107632145.PNG)

**Lambda URL**
```
https://dv5430asxj.execute-api.us-east-2.amazonaws.com/default/sta9760-lambda-tm
```


## AWS Kinesis
Amazon Kinesis offers managed services for streaming data called Kinesis Data Streams, Kinesis Video Streams, Kinesis Data Firehose, and Kinesis Data Analytics. Kinesis itself is based on Apache Kafka, a distributed data store for building real-time streaming data pipelines and applications. Amazon paints a thorough description of what constitutes “data streaming”. To paraphrase, when you stream data, thousands of data sources simultaneously and continuously generate records, which you must process “sequentially and incrementally on a record-by-record basis or over sliding time windows”.

**Provisioning a Simple Kinesis Service:**
- Start by going to the AWS homepage as per usual and type in “Kinesis”.
- For the next page, you only really need to add a name for your delivery stream.
- For the next page, you want to choose “Enabled” for the Transform source records with AWS Lambda option. 
- In a new tab, navigate to the Lambda landing page and create a new lambda function.
- Note that you ought to choose Python 3.8 here.
- Click Create Function and ensure you are on your new function landing page.
- Update your Timeout for this function, since Kinesis requires at least a timeout of one minute (AWS minimum requirement for lambdas that transform records).
- Click on the Edit button and increase the timeout to at least 1 min (by default it is super low, like 3s).
- Having created this function, let us go back to where we left off with the delivery stream:
- On the next page, we have to create a new s3 bucket to hold this data.
- On the next page, update the Buffer size and Buffer interval to the lowest possible values (1MB, 60 seconds).
- And then finally, before hitting Next, click on the AIM role button and pick the default option.
- At this point you are good to go! Hit Next. On the review page, ensure your options are entered as intended and hit Create.

**Kinesis Delivery Stream Configuration**
![Kinesis Delivery Stream](https://user-images.githubusercontent.com/6689256/82111947-98643480-9716-11ea-9c84-fb189e27b861.PNG)


**Lambda Function Configuration**
![lambda_kinesis](https://user-images.githubusercontent.com/6689256/82111941-8c787280-9716-11ea-80d4-b3030540fdf3.PNG)


**Lambda Function**
```
import json
import boto3
import random

CHOICES = ["TECHNOLOGY", "ENERGY", "FINANCIAL"]

def lambda_handler(event, context):
    # just generate some random data
    data = {"ticker_symbol":"HJK","sector":random.choice(CHOICES),"change":0.04,"price":4.79}
    
    # convert it to JSON -- IMPORTANT!!
    as_jsonstr = json.dumps(data)
    
    # initialize boto3 client
    fh = boto3.client("firehose", "us-east-2")
    
    # this actually pushed to our firehose datastream
    # we must "encode" in order to convert it into the
    # bytes datatype as all of AWS libs operate over

# bytes not strings
    fh.put_record(
        DeliveryStreamName="tm-delivery-stream", 
        Record={"Data": as_jsonstr.encode('utf-8')})

    # return
    return {
        'statusCode': 200,
        'body': json.dumps(f'Done! Recorded: {as_jsonstr}')
    }

```

**Lambda URL**
```
https://dv5430asxj.execute-api.us-east-2.amazonaws.com/default/delivery-stream-processor-latest
```
