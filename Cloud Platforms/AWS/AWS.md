Deploying to ECS

## Diagrams for AWS VPC
altijd een routing tabel er bij plaatsen
het icoon van de routing tabel in het diagram is niet noodzakelijk en dus ook niet de lijnen ernaar to dus oook niet

Altijd een label plaatsen bij een security group en hiernaar verwijzen in een tabel.


# Foundational services
## Compute

##### EC2
-> Elastic Cloud Compute
	comparable with a on-premise virtual machine
	AMI : Amazon Machine Images -> Amazone has a list of all available images , linux, windows,.....
	you can also create your own AMI, 
	vmware image can be converted into a AMI
	marketplace contains preconfigured AMI templates from 3e parties.
	
##### ECS -> Elastic Container Service , you need ECR 

##### AWS Fargate = cluster met 

##### EKS =  Elastic Kubernetes Service

##### ECR =  container Registry -> private docker hub.
	-> is free but you need to pay for the storage .
##### AWS Elastic Beanstalk = aws will create the frame
##### AWS Lambda -> serverless -> you deliver the code , for example a function -> amazon will execute the code only on request. when there is no request -> no running instance.
## Storage

##### Block storage
-> like a conventional harddisk
has a filesystem ext3, ext4, ntfs, fat32,....
##### Object storage
scalable
cheaper than object storage

#### databases RDS

aws aurora = in fact postgresql

## Networking
VPC



taak:

