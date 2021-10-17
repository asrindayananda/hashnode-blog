## Run a PHP script using GitHub Actions

- SignUp and Create a new reposiory in [ Github](https://github.com/)  

- Add a php file to your repository root named PHPTest.php
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1634490078009/Y0M0FpWni.png)

- Add some php in to file 
```
<?php
echo "testing";
```

- Commit and push this file into repository

- Create new file in your GitHub repo like this path
```
twitterBot/.github/workflows/runPHP.yml
```

- Add below code to yml file

```
# This is a basic workflow to help you get started with Actions

name: RunPHP

# Controls when the action will run. 
on:
  # Triggers the workflow on push of repository
  push:
    branches: [ main ]
  # Can add a schedule cron of when to run action but leaving this commented out for now
  #schedule:
  #  - cron: '0 08 * * *' 
  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest
    steps:
    # PHP GitHub Action created by https://github.com/nanasess
    - uses: actions/checkout@master
    - uses: nanasess/setup-php@master
      with:
        php-version: '7.4'
    # This triggers our php file we created before
    - run: php ./PHPTest.php
```

- Commit and Push your changes and click actions on your repo. 

- Click on Actions in your repository 

- You should see it building and if successful you can see php script returning "testing"

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1634491635850/KOHcyip65.png)

- After you get this working you can modify your PHPTest.php file to do whatever you want! 

Hope this works for you. Let me know if you get stuck. 

Happy Coding,
Asrin

If this helped you consider buying me a coffee :)

%%[buymecoffee]

References 
- https://github.com/nanasess
- https://docs.github.com/en/actions
