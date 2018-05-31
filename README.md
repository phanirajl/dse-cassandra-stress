# dse-multi-cloud-demo
Do you want a single cluster that can span multiple public clouds all while securing your data in the process? Also, I hope you mind if you don't have any downtime... with DataStax we make it really easy to be on-prem, in the cloud, hybrid, or even multi-cloud.

Multi-cloud is starting to be very important for customers. By leveraging multiple public clouds, they're able to maintain data portability as well as being able to shop around to find the best infrastructure price for their given workloads. DataStax Enterprise provides that level of portability that they would not have by just using one public cloud.

Yes, it is possible. And yes, you can do it!

## Create your VMs
* Go to a few of your favorite public cloud providers and create some VMs!
* Make note of the public and private IP addresses of all of the VMs
* Use the same public key on all of the servers
* Use the same username on all of the servers
* Put the private key on your laptop
* Make sure all of the DSE appropriate ports are open (e.g. nuclear option is 7000-65535)

## Set these environmental variables to whatever the values are for you:
```
export cassandra_default_password="blah"
export academy_user="blah"
export academy_pass="blah"
export academy_token="blah"
```
If you don't have credentials for DataStax Academy, then go and sign up for it at http://academy.datastax.com - it's free!  Be sure to create a download key (token) for your downloads too.

## Make sure that Python is installed on all of the VMs
If it isn't installed, then it won't work

## Create a text file that has your different VMs that you want in the cluster:
Format is: public-ip:private-ip:dc-name:node-number for example, I call it as multi-list.txt below:
```
18.236.78.240:172.31.16.53:aws:0
34.217.211.58:172.31.21.235:aws:1
34.208.176.38:172.31.17.235:aws:2
35.224.38.177:10.128.0.2:gcp:0
35.193.235.66:10.128.0.3:gcp:1
35.192.167.240:10.128.0.4:gcp:2
104.42.173.94:172.16.0.4:azure:0
104.42.168.14:172.16.0.4:azure:1
104.42.173.219:172.16.0.4:azure:2
```

## From your laptop, run the following command:
`python dse-multi-cloud-demo/setup.py -lcm 52.160.36.16 -u ubuntu -k keys/ubuntu -n dse-cluster -s dse-multi-cloud-demo/server-list`

Let's break down the switches:
* -u --> username that you'll use to log into all of the servers
* -k --> location of the private key on your laptop
* -n --> name of the dse cluster that you'd like to create
* -s --> list of servers that you created in the previous step

The script could take a few minutes to deploy so be patient.

## Gotchas and things to know
* Yes, I am using public IP addresses. I realize that your security team would feel better using a VPC and private IP addresses, but this demo is all about being quick and dirty. Feel free to adjust this to fit your needs.

# Up next:
* Automate the IaaS component of creating the VMs - almost done!
* Deploy some cool stuff and make that cluster work for you (e.g. load testing, cool demos)

# Credit to:
* Wei Deng (weideng1)
* Richard Lewis (Lewisr650)
* Collin Poczatek (cpoczatek)
