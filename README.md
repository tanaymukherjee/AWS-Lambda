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

![lambda](https://user-images.githubusercontent.com/6689256/82111699-f09a3700-9714-11ea-80a3-104107632145.PNG)

Lambda URL
```
https://dv5430asxj.execute-api.us-east-2.amazonaws.com/default/sta9760-lambda-tm
```


## AWS Kinesis
Amazon Kinesis offers managed services for streaming data called Kinesis Data Streams, Kinesis Video Streams, Kinesis Data Firehose, and Kinesis Data Analytics. Kinesis itself is based on Apache Kafka, a distributed data store for building real-time streaming data pipelines and applications. Amazon paints a thorough description of what constitutes “data streaming”. To paraphrase, when you stream data, thousands of data sources simultaneously and continuously generate records, which you must process “sequentially and incrementally on a record-by-record basis or over sliding time windows”.

