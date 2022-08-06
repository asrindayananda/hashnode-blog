## Twitter tweet bot using GitHub Actions

This is how I created a GitHub Action that sends tweets to my Twitter automaticly

# Twitter Authentification

Log into your Twitter account 

Register as Twitter dev
- https://developer.twitter.com/en/apply-for-access

Once approved create a new app
- https://developer.twitter.com/en/portal/apps/new
- Name your twitter bot
- You should have keys now 

- Create new repo in github
- Save your twitter keys to your GitHub repository secrets 
- Click on settings > secrets in your repository
- Add the keys from your twitter app you created 
- Name them as close as twitter state so you can recall them later easily
- eg.
```
TWITTER_API_KEY
API_KEY_SECRET
TIH_BEARER_TOKEN 
```
- Also create more keys by clicking new access token and secret and save all these values

# Create a GitHub Action

- Create a new file in your GitHub repo like this path
```
twitterBot/.github/workflows/twitterBot.yml
```

Add the below code to file
```
# This is a basic workflow to help you get started with Actions

name: TwitterBot

# Controls when the action will run. 
on:
  # Triggers the workflow on push or pull request events but only for the main branch
  push:
    branches: [ main ]
  schedule:
    - cron: '0 16 * * *' 
  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest
    steps:
    #Tweet to twitter https://github.com/marketplace/actions/tweet-to-twitter
      - name: TweetToTwitter
        uses: InfraWay/tweet-action@v1.0.1
        with:
          status: Test Tweet
          api_key: ${{ secrets.TWITTER_API_KEY }}
          api_key_secret: ${{ secrets.API_KEY_SECRET }}
          access_token: ${{ secrets.BEARER_TOKEN }}
          access_token_secret: ${{ secrets.BEARER_TOKEN }} 
```

- Commit your changes 

- Click actions and see your GitHub action build

- If you get this error
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631969888721/lZLmKTNl6.png)
- Your keys arnt set correctly
- Re generate your keys in twitter and reset them in your github repository secrets

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631970190368/cXIzVr7ZX.png)

- Re run job or add empty space commit to your yml file and push commit. The action is set to build on push at the moment.

- If you get this error
```
Error: {"request":"\/1.1\/statuses\/update.json","error":"Read-only application cannot POST."}
```
- Set your twitter app to be able to write posts
- Twitter App Settings > App permissions > Edit

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631970520907/DfhUrd_4x.png)
- Set to read and write

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631970552662/27wR1g8s5.png)

- You will have to regenerate all your keys and save them to your GitHub Secrets

- If you see success your github action will succeed

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631970771835/jBHcto4r0.png)

- And you will have a successful tweet !😵

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1631970801928/Iv4mjHumV.png)

# Shameless Plugs 
- [Join me and invest commission-free with Freetrade. Get started with a free share worth £3-£200.](https://magic.freetrade.io/join/asrin/447192e9)
- [Start a blog on Hashnode](https://hashnode.com/@azcodez/joinme)
- [Transfer money internationally with Wise](https://wise.com/invite/ath/asrind)
- [Join coinbase with my and you will earn some free crypto as well](https://coinbase.com/join/dayana_m40?src=android-link)

Hope this works for you. Let me know if you get stuck. 

Happy Coding,
Asrin

If this helped you consider buying me a coffee :)

%%[buymecoffee]

References 
- https://github.com/marketplace/actions/tweet-to-twitter
in 
- https://images.app.goo.gl/6bhWC7NVab2f1NKg9

%%[amazonads]