## Add GitHub ssh-agent and ssh key on startup (Windows)

If you have GitHub ssh key setup to access your remote repo, whenever you log out your PC your ssh key drops out! So you have to run `eval `ssh-agent -s` && 
ssh-add ~/.ssh/xxx-key` everytime you login.😡

This is how I added ssh-agent and ssh key authentification on start up of git terminal in Windows and in Android studio git bash terminal. 

# Add your ssh-agent  connection to .profile
- In git terminal
- Create a .profile or edit it 
```
nano ~/.profile 
```
- Add these contents. Remember to edit to set path to your ssh key!
```
#! /bin/bash 
eval `ssh-agent -s` 
ssh-add ~/.ssh/<ADD_PATH_TO_SSH_KEY>
```

# Add your ssh-agent connection to .bashrc
- You will need to add to bash as well. eg. I am using git terminal in Android studio so I will need to change bashrc
- Create a .bashrc or edit it 
```
nano ~/.bashrc 
```
- Add these contents. Remember to edit to set path to your ssh key!
```
#! /bin/bash 
eval `ssh-agent -s` 
ssh-add ~/.ssh/<ADD_PATH_TO_SSH_KEY>
```
- Restart the app that you are using git cli
- You should see something like 
```
Agent pid XXXX
Identity added: xxxxxxxxx
```
- Go to one of your repos and fetch remote repo by running
```
git fetch
```
- This should fetch contents without asking for key or ssh agent

# Credits
- https://stackoverflow.com/questions/3669001/getting-ssh-agent-to-work-with-git-run-from-windows-command-shell/15870387#15870387
- https://stackoverflow.com/questions/18404272/running-ssh-agent-when-starting-git-bash-on-windows
- https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
- [Create ssh key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

# Shameless Plugs 
- [Join me and invest commission-free with Freetrade. Get started with a free share worth £3-£200.](https://magic.freetrade.io/join/asrin/447192e9)
- [Start a blog on Hashnode](https://hashnode.com/@azcodez/joinme)
- [Transfer money internationally with Wise](https://wise.com/invite/ath/asrind)

Hope this saves you some time and getting annoyed 😒😁

Feel free to comment with questions or feedback✌️

Happy coding,

Az 👨🏾‍💻
