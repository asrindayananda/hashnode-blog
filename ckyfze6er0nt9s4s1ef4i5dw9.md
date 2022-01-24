## How to turn on AWS EC2 using Github Actions

Below we are going to write a  [Github Action](https://github.com/features/actions)  that turns on an AWS EC2 server

## Create a  [GitHub](https://github.com/) account

- Create a new repository

- Setup file for workflow
    - Folder named .github
    - Folder in .github called workflows
    - Create a file called turnOnAWSEC2.yml
    - See  [Link for more info](https://docs.github.com/en/actions/quickstart) 

## Add code to workflow (turnOnAWSEC2.yml) file
    
- Please see comments starting with '#' explaining what each bit of the file does
- This code is set up only to run when you click action in the repository
- Github workflows servers that are used to run the workflows have AWS CLI commands built-in, so all you need to do is run the AWS CLI command  [See this link for more information](https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners) 

```
name: startMagent2DevEC2

# Controls when the action will run. 
# This code is set up only to run when you click action in the repository, If you require to run on a push or cron edit below
on:
  # Triggers the workflow on push or pull request events but only for the main branch
  # push:
  #  branches: [ main ]
  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:

    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Below this are each of the steps that are run
    steps:

     # Name of step
      - name: Start AWS EC2
        # Run AWS Command on the GitHub Hosted runner which starts the instance using AWS authentication stored in GitHub Secrets (see below how to add)
        run: |
          aws ec2 start-instances --instance-ids ${{secrets.AWS_EC2_INSTANCE_ID }}
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_DEFAULT_REGION: ${{ secrets.AWS_REGION }}
         
```       

## Add GitHub Repository Secrets

- In the above workflow, we have many secrets to add eg. ${{ secrets.AWS_ACCESS_KEY_ID }}
    - Secrets are secret values stored so that GitHub workflow can use them without exposing them in your workflow file

- Create AWS Keys 
    - Log into your AWS portal that has high privileges to create accounts
    - Create a new IAM user as its AWS best practice to keep your logins separate from your root account  [See this link](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html) 
    - Logout and login as your new IAM user
    - Click your cloud name 
    - Click 'My Security Credentials'
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636198012667/FZ3bAswSN.png)
    - Click create 
    - Here you will have 2 keys that you will need to add to your repository. Keep this page open or copy these to add to below
- To add these AWS keys to your GitHub Repository
    - Click settings in your repository
    - Then secrets
    - Add repository secret named AWS_ACCESS_KEY_ID and add the key from the AWS portal you generated above
    - Create another secret named AWS_SECRET_ACCESS_KEY and add relevant keys from your keys created in your AWS Account

- Create a secret for your instance id ie. ${{secrets.AWS_EC2_INSTANCE_ID }}
    - Go to your AWS Console
    - Select Services > EC2
    - Instance ID is the identifier of what EC2 VM as below screenshot
    - Copy this ID and add it to your GitHub Secrets
    - Click settings in your repository
    - Then secrets
    - Add repository secret named AWS_EC2_INSTANCE_ID and add instance id

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1642256417358/3zhO4jSvK.png)

- Create a secret for your AWS region where your AWS EC2 is running id ie. ${{ secrets.AWS_REGION }}
- Go to your AWS Console 
    - Select Services > EC2
    - Region is in the right-hand corner as below screenshot
    - Make sure you match your region with code in this  [link](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html#concepts-regions) 
    - Add to your GitHub Secrets
    - Click settings in your repository
    - Then secrets
    - Add repository secret named AWS_REGION and add AWS region

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1642256512013/zAxKXXY9o.png)

Commit and push code if you haven't already

# Run your GitHub action
- In your repo
- Click Actions
- Select Action to run
- Click run the workflow

If successful you should have a complete success workflow and your EC2 should be switched on in AWS.

Don't forget to turn off your EC2 if you don't want it to run.

# Shameless Plugs
- Join me and invest commission-free with Freetrade. Get started with a free share worth £3-£200. https://magic.freetrade.io/join/asrin/447192e9
- Want to start a blog on hashnode use this [link ](https://hashnode.com/@azcodez/joinme) so I get a free shirt. I will assist you with setup 🙂
- Sign up for coinbase and get £7.42 of Bitcoin http://coinbase.com/join/dayana_m40?src=android-link

# Credits 
-  [AWS CLI commands](https://docs.aws.amazon.com/cli/latest/reference/ec2/start-instances.html) 
-  [GitHub Actions](https://docs.github.com/en/actions) 
-  [Amazon Web Services](https://aws.amazon.com/) 

Feel free to comment if you get stuck or have questions or feedback✌️

Happy Coding 🙂

Az 👨🏾‍💻
