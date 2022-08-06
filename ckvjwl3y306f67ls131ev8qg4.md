## Sync AWS S3 Bucket on Git Push using GitHub Actions

Below we are going to setup a GitHub Action to upload files to a S3 Bucket

- If you haven't got an S3 bucket on AWS you can set one up using this  [link](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html) 

- If you want to host your files as a static web server set up instructions are [here](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html) 


- Create a GitHub Reposiory
    - https://github.com/

- Add a github action workflow folder and file in repository
    - Path should look like this <repositoryName>/.github/workflows/<workflowName>.yml

- Add this code to the yml file

```
# This is a basic workflow to help you get started with Actions

name: SyncToS3

# Controls when the action will run. 
on:
  # Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches: [ main ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest
    # https://github.com/marketplace/actions/s3-sync 
    steps:
      - uses: actions/checkout@master
      - uses: jakejarvis/s3-sync-action@master
        with:
          args: --acl public-read --follow-symlinks --delete --exclude '.git/*' --exclude '.github/*'
        env:
          AWS_S3_BUCKET: ${{ secrets.AWS_S3_BUCKET }}
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_REGION: ${{ secrets.AWS_REGION }}
          SOURCE_DIR: './public'
```

- Create Secrets
    - In your reposiory click Settings > Secrets
    - Add below secrets, this  [link ](https://github.com/marketplace/actions/s3-sync#configuration) provides what secret should be 

```
AWS_S3_BUCKET 
AWS_ACCESS_KEY_ID 
AWS_SECRET_ACCESS_KEY 
AWS_REGION
```

- Create a folder in root of your repository called public
    - Add files in this folder

- Push your changes
    - Check Actions in your repo to see if its building

- Check your S3 Bucket to see whether files added

Hope this helped you, if this didn't please comment and I will try help you.

Remember to like, post a comment and share.

Happy Coding :)

Asrin

If this helped you consider buying me a coffee :)

%%[buymecoffee]

- Credits 
    - GitHub Action from https://github.com/marketplace/actions/s3-sync 

%%[amazonads]