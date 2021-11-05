## Create new branch with git command line

Say you have made some changes on a branch currently but dont want to put these changes on this branch but instead on a new branch 

- First check your current status of your git 
```
git status
```

- Stash your changes, don't worry they wont be lost
```
git stash
```

- Check your current branch status 
```
git branch -a
```

- Create a new branch, this will copy from current branch 
```
git branch <ADD YOUR NEW BRANCH NAME>
```

- Check your current branch status, see if your new branch exists
```
git branch -a
```

- Switch to this new branch 
```
git checkout <ADD YOUR NEW BRANCH NAME>
```

- Check your current branch status
```
git branch -a
```
Your current branch will be green like so

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1636106844282/beXo52fXB.png)

- Bring your changes back that you stashed before 
```
git stash pop
```

- You will have your changes back now, confirm this by running
```
git status
```

- Add all your changes for commit by running
```
git add .
```

- Add a commit message
```
git commit -m "<ADD YOUR COMMIT MESSAGE>"
```

-  Push your changes, setting the new branch to root of your directory
```
git push --set-upstream origin <ADD YOUR NEW BRANCH NAME>
```

- Your changes will now be on your remote branch


Hope this helped you, if this didn't please comment and I will try help you.

Remember to like, post a comment and share.

Happy Coding 🙂

Asrin 🤙

Want to start a blog on hashnode use this [link ](https://hashnode.com/@azcodez/joinme) so I get a free shirt. I will assist you with setup 🙂

If this helped you consider buying me a coffee 🙂

%%[buymecoffee]
