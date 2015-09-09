# code-deploy-demo


## Preparing your instance for deployment by CodeDeploy

Use the following script within your EC2 instance's user data to install the CodeDeploy Agent:
    #!/bin/bash
    yum -y update
    yum install -y aws-cli
    cd /home/ec2-user
    aws s3 cp s3://aws-codedeploy-us-east-1/latest/install . --region * **us-east-1** *
    chmod +x ./install
    ./install auto

