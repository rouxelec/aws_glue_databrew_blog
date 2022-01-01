# Get the best of your data with absolutely no code 

Or how to leverage AWS Glue DataBrew to easily build data pipelines with no data engineering skills. 

 

## Introduction 

Nowadays, it’s quite common to use a device (like a GPS watch or a cell phone) to track activities such as running or cycling. From those devices, it’s possible to upload your data to AWS and extract some relevant analytics that will help you improve your performance. 

AWS provides a large set of data services to analyze, clean, process, predict and visualize your data. It becomes possible to design solutions that scale even on large datasets. Building efficient data pipelines usually comes with writing some code, which requires specific technical skills.  

AWS Glue DataBrew is a service that allows you to process your data with no code. Non-IT specialists can easily leverage AWS Glue DataBrew to build and maintain data pipelines on their own. In this blog post, we will see how simple it is to transform data with an example that can be adapted to many other use cases. 

I am a Director at Slalom and have been an APN Ambassador since early 2020. APN Ambassadors work closely with AWS Solutions Architects to migrate, design, implement, and monitor AWS workloads. I have been working in IT for 25 years and have oriented my interest and expertise in the cloud. My role at Slalom is focused on helping companies migrate to the cloud. 

Slalom is an AWS Premier Consulting Partner with multiple AWS Competency and Service Delivery designations. Slalom is a modern consulting firm focused on strategy, technology, and business transformation. 

## Use Case 

In this example, I will use a dataset from my personal tracking device that I use when I exercise. As the device is meant for multiple sports, the dataset is a json file with many nested fields, which are used for multiple purposes. In our case, we will forget all swimming or cycling activities, and focus only on the running ones.  

Even if this GPS watch comes with a mobile application and nice ‘out of the box’ features such as the ability to visualize your runs on a map or some nice statistics, you may wish for more customized analytics. Although it is easy to see how many miles or kilometers one runs a month or a week, it gets more challenging to find out how many kilometers one usually runs a week after a marathon or how many long distances you did in preparation for that event.  

Obviously, if you are a data engineer, it is always possible to code a pipeline that will give you all the information you need, leveraging one or many data services available in the AWS platform. However, the goal of the blog post is to show you how easy it is to get more analytics without any specific data engineering skills, leveraging AWS Glue DataBrew. 

A sample activity file and the recipe YAML file are available at this location: https://github.com/rouxelec/aws_glue_databrew_blog 

Note: In this example, I used a file generated from my Garmin watch which uses a specific json format. Any type of personal tracking device file could be used, and the following recipe can be adapted for other input formats. 

## Solution overview 
![Alt text](aws-databrew-blog.drawio.png?raw=true "AWS Glue DataBrew")

We use the json file that contains all the activities I have done for the last 6 years. From this file, we create a dataset, build a recipe to clean and transform the data, and then create a job to automate the full process. 


The steps of the solution are as follows: 

1 - Transfer the json file in an S3 bucket 

2 - Create a dataset in AWS Glue DataBrew 

3 - Create a project in AWS Glue DataBrew 

4 - Create a recipe for data transformations 

5 - Create a job to run my recipe 

6 - Create a schedule to automate my data processing 

 

## Prerequisites 

To deploy this solution in ca-central-1, all you need to do is to create an S3 bucket in ca-central-1. Then, simply upload your activity file in the bucket. In our case, it’s a json file that contains an array of activities, and each activity is a json object with approximately 180 fields.  
