## Continuous Delivery

1. Grant AWS user Permissions **AWSCodePipelineApproverAccess**, **AWSCodeCommitFullAccess**
```js
// ARN:

arn:aws:iam::aws:policy/AWSCodeCommitFullAccess
arn:aws:iam::aws:policy/AWSCodePipelineApproverAccess
```
2. Create role for EC2 to Access AmazonS3ReadOnlyAccess

3. Create role for AWSCodeDeployRole

4. Create policy **EC2 codedeploy policy** <br/>
https://docs.aws.amazon.com/codedeploy/latest/userguide/getting-started-create-iam-instance-profile.html#getting-started-create-iam-instance-profile-console
```json


{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "s3:Get*",
                "s3:List*"
            ],
            "Effect": "Allow",
            "Resource": "*"
        }
    ]
}
```
5. Go to EC2 instance and from Actions>Instance Settings>Attach/Replace IAM Role add the role we created in ** Step# 2 **
6. Add CodeDeploy agent to be running on EC2 <br/>
https://docs.aws.amazon.com/codedeploy/latest/userguide/instances-ec2-create.html <br/>
https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-ubuntu.html <br/>

7. ssh to your instance and check the status of the code deploy agent
```ts
check status: sudo service codedeploy-agent status
start Agent: sudo service codedeploy-agent start

# it should say that the agent is running 
```

8. Now From AWS Console navigate to CodeDeploy service
9. Create an code deployment application
10. 


