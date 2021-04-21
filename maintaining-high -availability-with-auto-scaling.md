aws autoscaling put-scaling-policy --policy-name lab-scale-up-policy --auto-scaling-group-name lab-as-group --scaling-adjustment 1 --adjustment-type ChangeInCapacity --cooldown 300 --query 'PolicyARN' --output text

# Create a Launch Configuration


```PowerShell
aws autoscaling create-launch-configuration 
  --image-id AMIID 
  --instance-type t3.micro 
  --key-name KEYNAME 
  --security-groups EC2SECURITYGROUPID 
  --user-data file:///home/ec2-user/as-bootstrap.sh 
  --launch-configuration-name lab-lc
```

# Create an Auto Scaling Group

```PowerShell
aws autoscaling create-auto-scaling-group 
  --auto-scaling-group-name lab-as-group 
  --launch-configuration-name lab-lc 
  --load-balancer-names LOADBALANCER 
  --max-size 4 
  --min-size 1 
  --vpc-zone-identifier SUBNET1,SUBNET2
```


```PowerShell
aws autoscaling create-or-update-tags --tags 

  "ResourceId=lab-as-group, ResourceType=auto-scaling-group, Key=Name, Value=AS-Web-Server, PropagateAtLaunch=true"
```


```PowerShell
aws autoscaling describe-auto-scaling-notification-types
```




# Create Auto Scaling Notification

## Check Auto Scaling Notofication Available

```powerShell
aws autoscaling describe-auto-scaling-notification-types
```
## Configure Auto Scaling Notofication Available

```powerShell
aws autoscaling put-notification-configuration 
  --auto-scaling-group-name lab-as-group 
  --topic-arn SNSARN 
  --notification-types autoscaling:EC2_INSTANCE_LAUNCH autoscaling:EC2_INSTANCE_TERMINATE
```


# Create Auto Scaling Policy

## Create Scale-up Policy

```PowerShell
aws autoscaling put-scaling-policy 
  --policy-name lab-scale-up-policy 
  --auto-scaling-group-name lab-as-group 
  --scaling-adjustment 1 
  --adjustment-type ChangeInCapacity 
  --cooldown 300 
  --query 'PolicyARN' 
  --output text
```


## Create Scale-down Policy

```PowerShell
aws autoscaling put-scaling-policy 
  --policy-name lab-scale-down-policy 
  --auto-scaling-group-name lab-as-group 
  --scaling-adjustment -1 
  --adjustment-type ChangeInCapacity 
  --cooldown 300 
  --query 'PolicyARN' 
  --output text
```


# Viewing Auto Scaling Activity 

```PowerShell
aws autoscaling describe-scaling-activities --auto-scaling-group-name lab-as-group
```
