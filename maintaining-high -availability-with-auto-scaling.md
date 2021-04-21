








```PowerShell
aws autoscaling create-launch-configuration --image-id AMIID --instance-type t3.micro --key-name KEYNAME --security-groups EC2SECURITYGROUPID --user-data file:///home/ec2-user/as-bootstrap.sh --launch-configuration-name lab-lc
```
