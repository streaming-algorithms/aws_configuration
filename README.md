# AWS configuration

The goal of this project is to get ready to develop new streaming algorithms on AWS.

Let's go through the following steps:

__1. Create an AWS account:__

Go to https://aws.amazon.com/ and create a new free account.
During this course, we will onl use free resources. 


__2. Run an EC2 instance:__
Launch a new EC2 instance with the following characteristics:
- __AMI:__ Ubuntu Server 18.04 LTS (HVM), SSD Volume Type
- __Type:__ t2.micro with 1 vCPUs and 1GiB of memory
- __Storage:__ 24GiB
- __Ports:__ Open ports 22 and 8080
- __Key pair:__ Create new key pair or use existing one. 
    Make sure you download your private key.
    If you created a new key pair, make sure to change mode on your private key file.
    ```bash
    chmod 600 private_key.pem
    ```

__NB:__ All the sited options are free tier eligible.
https://docs.aws.amazon.com/fr_fr/awsaccountbilling/latest/aboutv2/free-tier-limits.html

 
 __3. Connect to your remote machine:__
 ```bash
 ssh -i private_key.pem ubuntu@ecx-xx-xx-xxx-xxx.us-east-2.compute.amazonaws.com
 ```
Use your private key and your machine's public DNS in the command above.
 
 
 __4. Configure environment:__
 
 Install python and pip
 ```bash
 sudo apt-get update
 sudo apt-get install python3.6
 sudo apt-get install python3-pip

 ```
 Install virtualenv
 ```bash
 sudo pip3 install virtualenv 
 ```
 Create a virtualenv and activate it
 ```bash
 virtualenv -p python3.6 venv
 source venv/bin/activate
 ```
 Install requirements
 ```bash
 mkdir projects
 cd projects
 git clone https://github.com/streaming-algorithms/aws_configuration.git
 pip install -r aws_configuration/requirements.txt
 ```
 
 __5. Use jupyter notebook on a distant machine:__
 Run jupyter notebook
 ```bash
 jupyter notebook --no-browser --port=8080 &
 ```
 Copy your token, you'll need it later.
 Disown your jupyter job to avoid shutting down the notebook when closing your console.
 ```bash
 disown -h
 ```
 On your local machine run the following command to do port forwarding
 ```bash
 ssh -i privete_key.pem -N -f -L localhost:8080:localhost:8080 ubuntu@ecx-xx-xxx-xxx-xxx.eu-west-1.compute.amazonaws.com
 ```
 Use your private key and your machine's public DNS in the command above.
 Type 127.0.0.1:8080 in your browser and enter the token you copied earlier to access the notebook.
 
 
 __6. Data:__
 
 We will use through this course one day od wikimedia data. Let's download it.
 Open the data_exploration.ipynp notebook in aws_configuration project and run the 
 first cell. This step may take several minutes.
 
Go through the notebook to learn more about the data.   
Source: https://wikitech.wikimedia.org/wiki/Analytics/Archive/Data/Pagecounts-raw
 
 
 You are now ready to build your first streaming algorithms.