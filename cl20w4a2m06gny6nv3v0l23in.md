## Automate login to GitHub with ssh key (linux)

# Intro

If you have setup ssh authentification to GitHub and if you are annoyed at setting ssh-agent and github key everytime you pull/push to git, here is how you automate it 😁

# Edit linux profile

This is based on linux WSL2 system

- Edit your linux profile 
```
nano ~/.profile 
```
- And add eval 
```
`eval `ssh-agent` 
ssh-add ~/.ssh/github-key 
```
- Close current terminal and open new terminal 
- You should have these lines printed out at start of terminal 
```
Agent pid XXXX Identity added: /root/.ssh/github-key XXXX
```
- Test fetching/commiting and pushing a change. eg
```
git fetch
git commit --allow-empty -m "test"
git push
```

# Credits
- https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
- [Create ssh key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

# Shameless Plugs 
- [Join me and invest commission-free with Freetrade. Get started with a free share worth £3-£200.](https://magic.freetrade.io/join/asrin/447192e9)
- [Start a blog on Hashnode](https://hashnode.com/@azcodez/joinme)
- [Transfer money internationally with Wise](https://wise.com/invite/ath/asrind)
- [Join coinbase with my and you will earn some free crypto as well](https://coinbase.com/join/dayana_m40?src=android-link)

Hope this saves you some time and getting annoyed 😒😁

Feel free to comment with questions or feedback✌️

Happy coding,

Az 👨🏾‍💻