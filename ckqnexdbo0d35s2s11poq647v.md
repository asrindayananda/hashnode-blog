## Updated your git ignore but files keep wanting to commit?

If you have updated your git ignore to exclude certain files, but git keeps telling you that those same files keep wanting to be commited. This solution is for you.

This problem occurs when git cache has not refreshed

So, you need to clear your git cache. Below are the steps to clear your git cache.

- Right click in your git folder

- Open your git bash
    - If you havent installed git bash see https://git-scm.com/downloads

- Run the following commands (Warning: This commits and pushed to your repo)
- Refresh your git branch so you don't have any conflicts when pushing

```
git pull
``` 
- Clear your git cache
```
git rm -r --cached .
``` 
- Add your changes and commit your changes

```
git add .
git commit -m 'Update GitIgnore'
``` 
- Push your changes to remote repository

```
git push
``` 

Your new git ignored files shouldn’t track now.

Hope this solution worked for you!

If this didn't please comment and I will try help you.

Remember to like, post a comment and share this blog if this worked for you.

Happy Coding :)

Asrin

If this helped you consider buying me a coffee :)

%%[buymecoffee]