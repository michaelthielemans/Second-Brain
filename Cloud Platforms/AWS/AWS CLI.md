
## Create a ec2 instance

```
aws ec2 run-instances --image-id ami-089f365c7b6a04f00 --count 1 --instance-type t2.micro --key-name ec2key --subnet-id subnet-0f2f738de3cc2b84b
```