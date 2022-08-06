## Combine commands to run on Linux (Debian)

Below we are going to add a bunch of commands into a file and run them all at once where you need to. This should help with development time

In your debian instance

- Create a file for your commands
```
nano /bin/new_script
```

- Add some commands to your script with && symbols at end of each command to run after another like example
- This is example is Magento 2 Commands when rebuilding code on developer environments
```
rm -rf generated/code/* && 
rm -rf pub/static/frontend/* && 
rm -rf pub/static/adminhtml/* && 
docker-compose run --rm deploy magento-command setup:upgrade && 
docker-compose run --rm deploy magento-command setup:di:compile && 
docker-compose run --rm deploy cloud-deploy && 
docker-compose run --rm deploy magento-command cache:clean && 
docker-compose run --rm deploy magento-command cache:flush
```

- Add permissions to file so the script can run anywhere
```
chmod +x /bin/new_script
```

- CD into directory you want to run script and run like so
```
new_script
```

If this didn't please comment and I will try help you.

Remember to like, post a comment and share this blog if this worked for you.

Happy Coding :)

Asrin

If this helped you consider buying me a coffee :)

%%[buymecoffee]

%%[amazonads]