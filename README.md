# AWS Employee Face Recognition: Granting/Denying Access
## Overview
This project utilizes various AWS services to implement a facial recognition system for employee authentication. It involves the setup of S3 buckets for storing employee and visitor photos, creation of Lambda functions for registration and authentication, configuration of IAM roles for security, utilization of AWS Rekognition for facial detection and comparison, setting up a REST API via API Gateway, and developing a React frontend application for user interaction.

## 1.) Setting up S3 Buckets:
As a foundational step in my project, two Amazon S3 (Simple Storage Service) buckets were created. These buckets serve different purposes within the application's architecture. The first bucket, named ‘david-employee-photos’, is designated for the storage of employee photos. This bucket acts as a repository for images uploaded by employees, which are later processed and indexed for facial recognition. The second bucket, named ‘david-ilori-visitor-photos’, is intended for storing photos submitted by visitors to the workplace. Although the second bucket is not technically needed, it serves to provide clarity and some organization within this application architecture.
<img src="https://i.imgur.com/y1RdmJ5.png" height="80%" width="80%" alt="Code commit permissions"/>
<br />
<br />


## 2.)  IAM Role Configuration
IAM (Identity and Access Management) roles were critical to my project to provide least privilege access to the many different Aws services used, as well as granting execution access to my lambda functions. These roles are tailored to grant secure access to essential AWS services, including CloudWatchLogs, DynamoDB, S3, and Rekognition. By carefully defining the permissions granted to each Lambda function, the project ensures strict control over access to sensitive resources, enhancing overall security and compliance with best practices.


## 3.) Lambda Registration Function and DynamoDB Table
The initial Lambda function was designed to index employee data within DynamoDB. Whenever an employee uploaded an image file to the 'david-employee-photos' S3 bucket, the Lambda function executed, extracting and storing essential employee information, including first and last names, alongside a unique identifier, into the DynamoDB table. 


## 4.) AWS CLI Configuration for Rekognition
After conducting research, I discovered that the AWS CLI is the primary method for interacting with Rekognition. Since I already had an AWS CLI configuration set up using secret and access keys for my IAM non-root account, configuring this setup was relatively straightforward. Upon executing the 'aws rekognition create-collection --collection-id employees --region us-east-1' command in the AWS CLI, the collection aspect of Felix’s Lambda code was prepared to commence indexing S3 photos submitted by employees. This indexed data would then be stored in DynamoDB for future reference.


## 5.) CloudWatchLogs for Debugging
I faced some issues when deploying the registration lambda function for the authentication, but after utilizing the error catches and debugging logs in his code, I was able to troubleshoot my issue after a couple of hours. CloudWatch was extremely helpful as the issues were logged and eventually after researching the code I realized I made a mistake in the faceId function call. I was then able to successfully upload Dwayne Johnson and John Cena as my first employees registered. 


## 6.) Creating a REST API via API Gatewa
A REST API is set up to act as an interface for another Lambda function responsible for authenticating user images. Requests from the frontend application are forwarded to the authentication Lambda function through the REST API.


## 7.) React Frontend Application
The frontend was created using react with the purpose of giving users a UI to upload visitor images for authentication. This application was a key component in this project as it connected different Aws services like my lambda authentication function and Api Gateway.


## 8.) Lambda Authentication Function
Another Lambda function is created to trigger when a user uploads a photo to the website application. This function retrieves visitor photos from the S3 bucket, utilizes Rekognition for face detection and comparison, and references DynamoDB to confirm if the employee is registered.


## 9.) Some notes
Overall, working on this project was an enjoyable experience, although a significant portion of the time was devoted to debugging and testing various components. Tools such as CloudWatch, console logs, and ChatGPT proved to be invaluable resources in diagnosing issues and ensuring the smooth functioning of the project.
