# challenge_scripts [EC2]

Challenge description
You work as a DevOps engineer for a small startup that is rapidly growing. The team needs to launch several new EC2 instances to support the growth of the business. Your task is to write a script that will launch an EC2 instance with Boto3, using command-line arguments to specify the instance type, AMI ID, key pair, and security groups. The script should print out the instance ID of the newly launched instance.

Challenge instructions
1:Create a new Python script called launch_instance.py.
2:Import the Boto3 library and create an EC2 client object.
3:Define command-line arguments using the argparse library:
4:--image-id: the ID of the AMI to use for the instance (required)
5:--instance-type: the instance type to launch (default: t2.micro)
6:--key-name: the name of the key pair to use for SSH access (required)
7:--security-group-ids: the IDs of the security groups to assign to the instance (required)
8:Use the run_instances() method on the EC2 client object to launch a new EC2 instance with the specified configuration.
9:Print out the instance ID of the newly launched instance.
10:Test your script by running it from the command line with the required arguments.

Challenge hints
You can find a list of available AMIs in the AWS documentation.

Make sure to handle errors that may occur when launching an instance, such as insufficient permissions or invalid arguments.

You can use the describe_instances() method on the EC2 client object to list all running instances and their attributes, for example:

response = ec2.describe_instances()
for reservation in response['Reservations']:
    for instance in reservation['Instances']:
        print(f"Instance ID: {instance['InstanceId']}")
        print(f"Instance type: {instance['InstanceType']}")
        print(f"Public DNS name: {instance['PublicDnsName']}")
        
        
        
solution of this challenge

import boto3
client = boto3.client('ec2')
resp = client.run_instances(ImageId='ami-00b3e95ade0a05b9b',
                           InstanceType='t2.micro',
                           MinCount=1,
                           MaxCount=1)
for instance in resp['Instances']:
    print(instance['InstanceId'])
    
    


challenge script2 [S3 Bucket]

Welcome to the Boto3 S3 Challenge Lab! In this lab, you will be using the Boto3 Python library to interact with Amazon S3, which is a cloud-based object storage service. The goal of this lab is to help you get familiar with using Boto3 to perform common S3 operations.

Prerequisites:

Basic knowledge of Python programming language.
Basic knowledge of Amazon S3.
Lab Tasks:

1:Create a Bucket: Use the Boto3 library to create a new S3 bucket. The name of the bucket should be unique across all of S3. You can use your name or a random string of characters to generate a unique name.

2:Upload a File: Use the Boto3 library to upload a file to the bucket that you created in step 1. The file can be any file of your choice.

3:Download a File: Use the Boto3 library to download the file that you uploaded in step 2 to your local machine.

4:List Buckets: Use the Boto3 library to list all of the buckets in your S3 account.

5:List Objects: Use the Boto3 library to list all of the objects in the bucket that you created in step 1.

6:Delete a File: Use the Boto3 library to delete the file that you uploaded in step 2 from the bucket.

7:Delete a Bucket: Use the Boto3 library to delete the bucket that you created in step 1.

Bonus Task:
8:Enable Versioning: Use the Boto3 library to enable versioning for the bucket that you created in step 1. Once versioning is enabled, upload the same file that you uploaded in step 2 to the bucket again. Then, use the Boto3 library to list all of the versions of the file.

Tips:
Before you start, make sure that you have installed the Boto3 library on your machine.
You will need to configure your AWS credentials to use Boto3. You can either set environment variables or use the AWS CLI to configure your credentials.
Refer to the Boto3 documentation for information on how to use the library.
Good luck with the challenge lab!


detailed solution to the Boto3 S3 Challenge Lab:

Step 1: Create a Bucket
To create a bucket, you can use the create_bucket method of the s3 client. Here's how you can do it:

import boto3

# Create an S3 client
s3 = boto3.client('s3')

# Create a unique bucket name
bucket_name = 'my-unique-bucket-name'

# Create the bucket
s3.create_bucket(Bucket=bucket_name)

In the above code, we first import the boto3 library and create an S3 client. We then generate a unique name for our bucket and use the create_bucket method to create the bucket in S3

Step 2: Upload a File
To upload a file, you can use the put_object method of the s3 client. Here's how you can do it

# Upload a file to the bucket
file_name = 'path/to/file.txt'
object_name = 'file.txt'

s3.upload_file(file_name, bucket_name, object_name)

In the above code, we specify the path of the file that we want to upload and the name that we want to give to the object in S3. We then use the upload_file method to upload the file to the S3 bucket.

Step 3: Download a File
To download a file, you can use the download_file method of the s3 client. Here's how you can do it

# Download the file from the bucket
download_path = 'path/to/download/file.txt'

s3.download_file(bucket_name, object_name, download_path)
In the above code, we specify the path where we want to download the file to and use the download_file method to download the file from the S3 bucket.

Step 4: List Buckets
To list all of the buckets in your S3 account, you can use the list_buckets method of the s3 client. Here's how you can do it:

# List all buckets in your account
response = s3.list_buckets()

# Print out the bucket names
for bucket in response['Buckets']:
    print(f'Bucket Name: {bucket["Name"]}')
    
In the above code, we use the list_buckets method to get a list of all the buckets in our account. We then loop through the response and print out the name of each bucket.

Step 5: List Objects

To list all of the objects in a bucket, you can use the list_objects method of the s3 client. Here's how you can do it:

# List all objects in the bucket
response = s3.list_objects(Bucket=bucket_name)

# Print out the object names
for obj in response['Contents']:
    print(f'Object Name: {obj["Key"]}')
In the above code, we use the list_objects method to get a list of all the objects in the bucket that we created in step 1. We then loop through the response and print out the name of each object.

Step 6: Delete a File
To delete a file from a bucket, you can use the delete_object method of the s3 client. Here's how you can do it:

# Delete the file from the bucket
s3.delete_object(Bucket=bucket_name, Key=object_name)

In the above code, we use the delete_object method to delete the object that we uploaded in step
