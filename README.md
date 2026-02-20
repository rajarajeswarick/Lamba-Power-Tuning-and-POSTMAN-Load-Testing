# Lamba-Power-Tuning-and-POSTMAN-Load-Testing
Determine optimal memory and load test your microservice and get performance info

Lambda Power Tuning
Customers use this to determine optimal memory to allocate to Lambda based on their goal i.e. best performance, or cheapest cost, or a balance etc. (remember Well Architected framework pillars!)

Go to Serverless Application Repository
Click Available Applications, type “power”, check “Show apps that create custom IAM roles or resource policies”
Select aws-lambda-power-tuning
Scroll down, keep everything as is, check “I acknowledge that this app creates custom IAM roles”, click “Deploy”
Once done, go to Step Functions
<img width="788" height="793" alt="image" src="https://github.com/user-attachments/assets/8dba260c-855b-48b6-b920-e1f48b532adc" />
Scroll down, keep everything as is, check “I acknowledge that this app creates custom IAM roles”, click “Deploy”
Once done, go to Step Functions
Select the powerTuningStateMachine, click “Start execution”. 
Get your Lambda ARN and put in the below JSON. Then copy the whole JSON and put it in input
```json
{
  "lambdaARN": "YOUR LAMBDA ARN HERE",
  "powerValues": [
    128,
    256,
    512,
    1024
  ],
  "num": 10,
  "payload": {
    "operation": "list",
    "tableName": "lambda-apigateway",
    "payload": {}
 },
  "parallelInvocation": true,
  "strategy": "cost"
}
```
Once it done running, click Execution input and output tab. 
Select and copy the visualization link
Open in new browser
 
This graph shows cost and performance tradeoff. Raj will explain in class, this part is important, so please pay attention (or watch recording afterwards)
<img width="1180" height="590" alt="AWS Lambda Power Tuning Results" src="https://github.com/user-attachments/assets/bb127355-d243-4d77-b6b9-6878171775f1" />

At 256 MB:

Execution time dropped significantly compared to 128 MB.

Cost is still very low.
Better performance per dollar.
This is called: Optimal Price-Performance Point

Optional Module
Postman Load Testing 

This is another way to load test your microservice and get performance info. This one can be use irrespective of whether it’s serverless or not (Power tuning above is just for Lambda). This also creates very nice graphs for Linkedin Screenshots ;)

Make sure you have the latest Postman app https://www.postman.com/downloads/ 
Under Collections, click “+”
Then click “Blank Collection”
Give a name
Click “Add a request”
IMPORTANT: Make sure to change “GET” to “POST”, and paste the API Gateway POST URL
Click “Body” then “raw” and paste:

```json
{
"operation" = "list",
"tablename" : "lambda-apigateway",
"payload": {
}
}
```
Validate: The request should change to POST, under the collection on left
Now we are all set to run performance testing! 

Click “...” in the collection name, and from the drop down click “Run”

<img width="772" height="421" alt="image" src="https://github.com/user-attachments/assets/237b0d35-c380-4db4-9a62-500392513e5d" />






```


