## Create a AWS S3 bucket with Github Actions

Below we are going to run a Github Action that creates a S3 bucket in AWS Cloud

Github workflows have AWS CLI commands built in so all you need to do it run the command  [See this link for more information](https://docs.github.com/en/actions/using-github-hosted-runners/about-github-hosted-runners) 

Create a  [GiHub ](https://github.com/) account

Create a new repository

Setup file for workflow
- Folder named .github
- Folder in .github called workflows
- Create a file called addS3BucketAWS.yml
- See  [Link for more info](https://docs.github.com/en/actions/quickstart) 

Add Below code to workflow file
- This code is setup only to run when you click action in repository

```
# This is a basic workflow to help you get started with Actions

name: addS3BucketAWS

# Controls when the action will run. 
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

    steps:
      - uses: actions/checkout@master

      - name: Upload to S3
        run: |
          aws s3 mb s3://<ADD BUCKET NAME MAKE SURE IT'S UNIQUE>
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_DEFAULT_REGION: 'eu-west-1'
```

- Change this in your action 
```
<ADD BUCKET NAME MAKE SURE IT'S UNIQUE>
```
    - Change it to a unique name. Remember S3 names are publicly chosen. Add a random string to end of your bucket name to make sure its unique eg. I used ```az-test-bucket-8923yhr98uh```

- Create AWS Keys
- Log into your AWS portal
- Click your cloud name 
- Click 'My Security Credentials'
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636198012667/FZ3bAswSN.png)
- Click create 
- Here you will have 2 keys which you will need to add to your repository

Add keys to your GitHub Repository
- Click settings in your repository
- Then secrets
- Add repository secrets named AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY and add relevant keys from your keys created in your AWS Account

Commit and push code if you havent already

Run your action
- In your repo
- Click Actions
- Select Action to run
- Click run workflow

If successful you should have a complete success workflow like below

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636204211053/a3lop3Bi0.png)

Hope this helped you, if this didn't please comment and I will try help you.

Remember to like, post a comment and share.

Happy Coding 🙂

Asrin 🤙

Want to start a blog on hashnode use this [link ](https://hashnode.com/@azcodez/joinme) so I get a free shirt. I will assist you with setup 🙂

If this helped you consider buying me a coffee 🙂

%%[buymecoffee]

Credits
- https://stackoverflow.com/questions/59166099/github-action-aws-cli
- AWS CLI commands https://docs.aws.amazon.com/cli/latest/userguide/cli-services-s3-commands.html#using-s3-commands-managing-buckets-creating
- Image https://chillplanet.org/tag/aws/
- Image https://www.coletiv.com/blog/android-github-actions-setup/