## Setup GitHub SSH key using Windows

This is how I installed Git and authenticated with my GitHub repo using a ssh key using Windows OS

# Download and install git
- https://git-scm.com/

# Create a folder for a git repo
- Create a folder in your windows system
- Open folder in git by right clicking and selecting git bash
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649756146144/O4phMyjpq.png)

# Create a ssh key (Open ssh type)
```
ssh-keygen -t ed25519 -C "AddYourEmail@email.com"
```
- Follow prompts and save to your .ssh folder
- View and copy your public key you need to add this later
```
nano <YOUR_LOCATION_YOU_ADDED_ABOVE>/.ssh/github-key.pub
```

# Go to your github security settings
- https://github.com/settings/profile
- Cick SSH and GPG keys
- Click NewSSH key
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1649755581144/UEKGewbU7.png)
- Add public key you copied before new SSH key and add add a Title
- Add SSH key
- You should have a success notification

# Add your ssh-agent  connection to .profile
- Open your git folder using git bash again
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
- [Header Image](https://github.blog/2018-06-04-github-microsoft/)


# Shameless Plugs 
- [Join me and invest commission-free with Freetrade. Get started with a free share worth £3-£200.](https://magic.freetrade.io/join/asrin/447192e9)
- [Start a blog on Hashnode](https://hashnode.com/@azcodez/joinme)
- [Transfer money internationally with Wise](https://wise.com/invite/ath/asrind)
- [Join coinbase with my and you will earn some free crypto as well](https://coinbase.com/join/dayana_m40?src=android-link)

Feel free to comment with questions or feedback✌️

Happy coding,

Az 👨🏾‍💻