## Automatically Tweet Hashnode blogs using GitHub Actions

This is how I post my Hashnode blogs to Twitter automatically by using GitHub Actions. You can see these tweets on [my Twitter account](https://twitter.com/az_codez). 

# Costs
- [Github provides 2,000 minutes a month](https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions) for free account which is plenty!
- This GitHub action only uses 20s / 1 billable minute
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1659189142209/6t5XAkee_.png align="left")


# Setup Hashnode API

- First, check out this awesome blog by Catalin about the [Hashnode API](https://catalins.tech/hashnode-api-how-to-display-your-blog-articles-on-your-portfolio-page) and make sure you can call the API and your blogs

- Load the Hashnode API playground https://api.hashnode.com/

- Setup your  Hashnode API playground like so, including your own blog name if hasnode playground hasn't done it for you already
```
{
  user(username: "<ADD_YOUR_BLOG_USERNAME") {
    publication {
      posts(page: 0) {
        title
        brief
        slug
        
      }
    }
  }
}
```

# Create a GitHub Action 

- [Follow this my previous blog on how to tweet using GitHub actions](https://blog.azcodez.com/twitter-tweet-bot-using-github-actions)

- Add some more steps before the tweet step

- Add fetching Hashnode API
```
      # API request https://github.com/marketplace/actions/http-request-action
      - name: Deploy Stage
        id: myRequest
        uses: fjogeleit/http-request-action@master
        with:
          url: 'https://api.hashnode.com/'
          method: 'POST'
          data: '{"query":"{\n  user(username: \"<ADD_YOUR_USERNAME>\") {\n    publication {\n      posts(page: 0) {\n        title\n        brief\n        slug\n      }\n    }\n  }\n}\n"}'
          customHeaders: '{"headers": {"Content-Type": "application/json"}}'
```

- Add another step to check your response
```
      - name: Show Response
        run: echo ${{ steps.myRequest.outputs.response }}
```

- Add a JavaScript executor to run some JavaScript to modify the query
```
 # Sort Json array https://github.com/marketplace/actions/execute-javascript-inline
      - name: Execute JavaScript inline
        id: quoteFiltered
        uses: satackey/action-js-inline@v0.0.2
        with:
          # Edit the following line to install packages required to run your script.
          required-packages: axios
          script: |
            //setup
            const core = require('@actions/core')
            const axios = require('axios')
            
            //set output from other step            
            const quoteJson = ${{ steps.myRequest.outputs.response }}
            
            //Filter what blog to receive 
            randomNumber = Math.floor(Math.random() * 6);            
            const title = (String(quoteJson['data']['user']['publication']['posts'][randomNumber]['title']));
            const slug = (String(quoteJson['data']['user']['publication']['posts'][randomNumber]['slug']));
            //What tweet contents will be
            const finalQuote = (title+' '+'https://blog.azcodez.com/'+slug+'{ by @az_codez } from @hashnode #softwaredevelopment #coding #softwareengineering #programming #techblog') 
            
            console.log(finalQuote)
            
            //Output
            core.setOutput('finalQuote', finalQuote)
```

- Make sure you run your GitHub action multiple times to check what you are going to tweet is correct and GitHub Action passes

- Now add your tweet to Twitter step
```
 # Tweet to twitter https://github.com/marketplace/actions/tweet-to-twitter
      - name: TweetToTwitter
        uses: InfraWay/tweet-action@v1.0.1
        with:
          status: ${{ steps.quoteFiltered.outputs.finalQuote }}
          api_key: ${{ secrets.TWITTER_API_KEY }}
          api_key_secret: ${{ secrets.TWITTER_API_SECRET_KEY }}
          access_token: ${{ secrets.TWITTER_ACCESS_TOKEN }}
          access_token_secret: ${{ secrets.TWITTER_ACCESS_TOKEN_SECRET }} 
```

# Credits

- Github Actions Image coletiv.com/blog/android-github-actions-setup
- Twitter image https://www.nytimes.com/2014/08/10/magazine/who-made-that-twitter-bird.html

# Shameless Plugs 
- [Join me and invest commission-free with Freetrade. Get started with a free share worth £3-£200.](https://magic.freetrade.io/join/asrin/447192e9)
- [Start a blog on Hashnode](https://hashnode.com/@azcodez/joinme)
- [Transfer money internationally with Wise](https://wise.com/invite/ath/asrind)
- [Join coinbase with my and you will earn some free crypto as well](https://coinbase.com/join/dayana_m40?src=android-link)

Now you don't have to worry about reposing your blogs!

Hope this helps😁

Feel free to comment with questions or feedback✌️

Happy coding,

Az 👨🏾‍💻

%%[amazonads]