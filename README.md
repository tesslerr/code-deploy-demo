# code-deploy-demo


## Preparing your instance for deployment by CodeDeploy
Use the following script within your EC2 instance's user data to install the CodeDeploy Agent. Make sure to modify the Amazon S3 bucket name and region parameter to reflect the region your instance belongs to:

    #!/bin/bash
    yum -y update
    yum install -y aws-cli
    cd /home/ec2-user
    aws s3 cp s3://aws-codedeploy-us-east-1/latest/install . --region us-east-1
    chmod +x ./install
    ./install auto

The Code deploy agent will need to access specific Amazon S3 buckets to communicate with the CodeDeploy service. It will also need access to any bucket that contains your code for deployment. To allow access to these resources you will need to set and assign an instance profile with the following IAM policy:

    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Action": [
            "s3:Get*",
            "s3:List*"
          ],
          "Effect": "Allow",
          "Resource": [
            "arn:aws:s3:::CodeDeployDemoBucket/*",
            "arn:aws:s3:::aws-codedeploy-us-east-1/*",
            "arn:aws:s3:::aws-codedeploy-us-west-2/*",        
            "arn:aws:s3:::aws-codedeploy-eu-west-1/*",
            "arn:aws:s3:::aws-codedeploy-ap-southeast-2/*",
            "arn:aws:s3:::aws-codedeploy-ap-northeast-1/*"
          ]
        }
      ]
    }
