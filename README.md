# Install A Multi-node Kubernetes Cluster on AWS EC2 Instances By Kube-aws

In this article, we will capture full detailed steps to set up a full multi-node kubenetes cluster on AWS EC2 instances by kube-aws tool. The kube-aws tool is one of the Kubernetes supported production grade tools to deploy Kubernetes on AWS EC2 instances of CoreOS. It's CoreOS originated and maintained by Kubernetes Incubator. Refer to https://kubernetes.io/docs/getting-started-guides/aws/

The steps are mainly sourced from CoreOS publication of https://coreos.com/kubernetes/docs/latest/kubernetes-on-aws.html and other various publications with practical adjustments. 

We are using a typical MacPro laptop to execute the steps. The Mac is on version 10.12.6. 

At the high level, the steps are as below: 

Step 1: Download kube-aws tool and set up AWS Command Line interface on the laptop. 

## Step 1 Download kube-aws and Set Up AWS CLI Tool

As the first step, we will download the kube-aws tool and set up AWS command line interface on the Mac laptop. 

Go to https://github.com/kubernetes-incubator/kube-aws/releases to download the file of kube-aws-darwin-amd64.tar.gz to your MacPro laptop, then extract it and put it under MacPro default command PATH as below:
```
MacBook-Pro:~ jaswang$ cd Downloads/
MacBook-Pro:Downloads jaswang$ tar zxvf kube-aws-darwin-amd64.tar.gz 
x darwin-amd64/
x darwin-amd64/kube-aws
MacBook-Pro:Downloads jaswang$ sudo mv darwin-amd64/kube-aws /usr/local/bin/
MacBook-Pro:Downloads jaswang$ kube-aws version
kube-aws version v0.9.7
```
Then we need to install the AWS CLI tool. The AWS CLI is an open source tool built on top of the AWS SDK for Python (Boto) that provides commands for interacting with AWS services. AWS CLI tool requires Python 2 version 2.6.5+ or Python 3 version 3.3+, so we verify the Python version on the MacPro laptop first. On my laptop, I have installed Anaconda3 so it uses the Python 3 shipped with Anaconda3 as shown below. But the default Python 2 shipped with MacOS will work as well. 
```
MacBook-Pro:~ jaswang$ which python
/Users/jaswang/anaconda3/bin/python
MacBook-Pro:~ jaswang$ which pip
/Users/jaswang/anaconda3/bin/pip
MacBook-Pro:~ jaswang$ python -V
Python 3.6.1 :: Anaconda 4.4.0 (x86_64)
```
Based on the steps described in AWS CLI guide - http://docs.aws.amazon.com/cli/latest/userguide/installing.html, we install the AWS CLI tool by the following command using pip: 
```
MacBook-Pro:~ jaswang$ pip install awscli --upgrade --user
MacBook-Pro:~ jaswang$ aws --version
aws-cli/1.11.136 Python/3.6.1 Darwin/16.7.0 botocore/1.6.3
```
Now we need to configure AWS CLI tool with AWS credentials. First we need to create AWS access key and AWS secret access key by the folowing steps if you don't have one yet. 

a. Log onto AWS console - https://aws.amazon.com/console/ 
b. Go ==> Security & Identity & Compliance ==> IAM
c. Create a new user belonging to Admin group
d. In that user setting window, select Security Credentials tab. 
e. In the section of Access Keys, click the button of Create Access Key. 
f. In the pop up window, a Access Key ID and a Secret Access Key will present. Click the button of Download .csv file to download them to your laptop. Then close the pop up window. 

Now we can configure the AWS CLI tool on the laptop with AWS credentials retrieved by the steps above: 
```
MacBook-Pro:~ jaswang$ aws configure
AWS Access Key ID [****************Y3UQ]: AKIAIMYZJGD42HX2NYDA
AWS Secret Access Key [****************stjs]: UcqT37tRaWZPRABJ5t1+9w4czZz2tzfAknrdxbwm
Default region name []: ap-southeast-2
Default output format [json]: json
```
Now verify AWS CLI tool can access your AWS environment to check out EC2 instance, for exaample. 
```
MacBook-Pro:~ jaswang$ aws ec2 describe-instances
{
    "Reservations": []
}
```

## Step 2 Configure Kurbenetes Cluster Assets via kube-aws tool

Now in this step, we will configure Kurbenetes Cluster Assets using kube-aws on the MacPro laptop. The kube-aws tool needs several AWS resources to configure K8S cluster aseets. So we will create those AWS resources beforehand. 

### Configure AWS Resources

For kube-aws tool to configure K8S cluster assets, the following 4 AWS resources are needed. 

  EC2 Key Pairs
  KMS Key
  External DNS Name
  S3 Bucket
  
We will configure those AWS resources one by one.

#### Create AWS EC2 Key Pair

AWS Elastic Compute Cloude (EC2) Key Pair 

### 






