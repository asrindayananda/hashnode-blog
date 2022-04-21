## Creating a AWS EC2 using Github Actions and Terraform Cloud

These are steps on how I created an AWS EC2 using Github Actions and Terraform. 

# Create a Terraform Cloud account
- [Create Terraform Cloud Account using this link](https://app.terraform.io/?utm_source=learn)
- Create a workspace - remember the name you called it
- In your AWS portal
    - [Create a new AWS IAM user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)
    - Give this IAM User full AWS EC2 access
    - Store AWS Access Credentials in the Terraform cloud workspace under variables named 
        - AWS_ACCESS_KEY_ID
        - AWS_SECRET_ACCESS_KEY
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650561122135/-tu54VtdA.png)

# Create Terraform Cloud token
- Go to this link which will take you to terraform tokens page 
    - https://app.terraform.io/app/settings/tokens?utm_source=learn
- Create an API token Copy this token we will store this in Gitub Repo

# Create a new GitHub repo
- [Follow these instructions on how to create a GitHub repo if you havent before](https://docs.github.com/en/get-started/quickstart/create-a-repo)
- Add above Terraform Cloud API token secret
    - In your GitHub repo 
    - Settings > Secrets > Actions
    - Create repository secret named TF_API_TOKEN
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650561599991/9TbKNUZAd.png)

# [Pull repo down locally to modify code](https://docs.github.com/en/desktop/contributing-and-collaborating-using-github-desktop/adding-and-cloning-repositories/cloning-a-repository-from-github-to-github-desktop)

# Add Terraform files 
- Copy this file to your repo [main.tf](https://github.com/hashicorp/learn-terraform-github-actions/blob/main/main.tf)

#  Add GitHub Action file
- Copy this terraform.ym to your repo as well https://github.com/hashicorp/learn-terraform-github-actions/blob/main/.github/workflows/terraform.yml
- See this for more info to what it does
https://learn.hashicorp.com/tutorials/terraform/github-actions?in=terraform/automation

# Change main.tf
- Configure these lines to suit what you have created in terraform cloud 
- Change ADD_TERRAFORM_ORGANISATION_NAME & ADD_TERRAFORM_WORKSPACE_NAME 

```
  cloud {
    organization = "ADD_TERRAFORM_ORGANISATION_NAME"

    workspaces {
      name = "ADD_TERRAFORM_WORKSPACE_NAME"
    }
  }
}
```
- Change this line to where you want your EC2 to be created (us-west-2)
```
provider "aws" {
  region = "us-west-2"
}
```

# Create a branch and push changes up
```
git branch NewEC2
git checkout NewEC2
git push NewEC2
```

# Create a in GitHub PR to merge into main
- [Create PR in GitHub Repo](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)
- GitHub Action Check will kick off and check if everything is ok
- If you get errors like
```
Error: No valid credential sources found for AWS Provider. 
```
- Double check your organization and workspace in terraform or Terraform API key we added into secrets in github
- If checks succeed you are ready to create your EC2 from Terraform code
- Merge pull request into main 
- Wait for GitHub action to run
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1650562128763/Z5LsKzVr-.png)

# Check if EC2 got provisioned
- Go to your Github Action in your repo and click under Terraform Apply step you should have a url to check server
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648326842609/CF7XZfpBY.png)
- Copy it and go to the site and check it should respond to hello world.
- You also could login to your AWS account and find the server

Congrats you have created a server with GitHub Actions and Terraform 🎉

# Now delete resources
- Open  your Terraform Cloud 
- Find your workspace
- Click settings
- Queue destroy plan 
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648327119697/r8yz6TIo5.png)
- You will see triggers running to destroy it
- You have to confirm you want to accept deleting
- Check your url before is broken 
- Check your EC2 server is removed in the AWS portal or via AWS CLI command

# Credits
- [Hashicorp Terraform Github Actions](https://learn.hashicorp.com/tutorials/terraform/github-actions?in=terraform/automation)
- [Learn Hashicorp Terraform Github Actions](https://learn.hashicorp.com/tutorials/terraform/aws-build?in=terraform/aws-get-started)
- [Github Action image](https://www.coletiv.com/blog/android-github-actions-setup/)
- [Terraform AWS image](https://www.parkmycloud.com/blog/terraform-on-aws/)

# Shameless Plugs 
- [Join me and invest commission-free with Freetrade. Get started with a free share worth £3-£200.](https://magic.freetrade.io/join/asrin/447192e9)
- [Start a blog on Hashnode](https://hashnode.com/@azcodez/joinme)
- [Transfer money internationally with Wise](https://wise.com/invite/ath/asrind)

Feel free to comment with questions or feedback✌️

Happy coding,

Az 👨🏾‍💻