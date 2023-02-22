# challenge_scripts

Challenge description
You work as a DevOps engineer for a small startup that is rapidly growing. The team needs to launch several new EC2 instances to support the growth of the business. Your task is to write a script that will launch an EC2 instance with Boto3, using command-line arguments to specify the instance type, AMI ID, key pair, and security groups. The script should print out the instance ID of the newly launched instance.

Challenge instructions
Create a new Python script called launch_instance.py.
Import the Boto3 library and create an EC2 client object.
Define command-line arguments using the argparse library:
--image-id: the ID of the AMI to use for the instance (required)
--instance-type: the instance type to launch (default: t2.micro)
--key-name: the name of the key pair to use for SSH access (required)
--security-group-ids: the IDs of the security groups to assign to the instance (required)
Use the run_instances() method on the EC2 client object to launch a new EC2 instance with the specified configuration.
Print out the instance ID of the newly launched instance.
Test your script by running it from the command line with the required arguments.

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
    
    

