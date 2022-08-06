## Installing the AWS EB CLI command on Debian 11 (WSL2)

In order to create docker containers in Amazon Web Services Elastic Beanstalk, you need the EB CLI command to run. I didn’t find the installation of this very straightforward forward so hopefully, this helps you.

# Install python
```
sudo apt update 
sudo apt -y upgrade
sudo apt install wget build-essential libreadline-gplv2-dev libncursesw5-dev \ libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev
sudo apt -y install wget
wget https://www.python.org/ftp/python/3.9.1/Python-3.9.1.tgz
tar xzf Python-3.9.1.tgz
python3.9 --version
```

## Set python symlink to run off just the python command
```
sudo ln -s /usr/bin/python3.9 /usr/bin/python
python --version
```

# Install pip
```
sudo apt-get -y install python3-pip
```

# Install virtualenv
```
sudo pip install virtualenv
virtualenv --version
```

# Install git
```
sudo apt-get -y install git
```

# Create a folder and pull the eb command repo
```
sudo mkdir /eb-command
chown -R <ADDUSER>:<ADDUSER> /eb-command
cd eb-command
git clone https://github.com/aws/aws-elastic-beanstalk-cli-setup.git
```

Run EB CLI install file
```
python ./aws-elastic-beanstalk-cli-setup/scripts/ebcli_installer.py
```

A successful install will look like this
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656755359315/IXKMnwhEW.png align="left")

Run the bash command provided above

# Test EB CLI Command
```
eb --help
```
Successful will look like this

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1656755433235/3FktOnXG-.png align="left")

# Credits
- https://github.com/aws/aws-elastic-beanstalk-cli-setup
- https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install.html#eb-cli3-install.scripts
- https://linuxize.com/post/how-to-install-python-3-9-on-debian-10/
- https://virtualenv.pypa.io/en/latest/user_guide.html
- https://github.com/pyenv/pyenv
- https://stackoverflow.com/questions/18363022/importerror-no-module-named-pip
- https://stackoverflow.com/questions/31133050/virtualenv-command-not-found

# Shameless Plugs 
- [Join me and invest commission-free with Freetrade. Get started with a free share worth £3-£200.](https://magic.freetrade.io/join/asrin/447192e9)
- [Start a blog on Hashnode](https://hashnode.com/@azcodez/joinme)
- [Transfer money internationally with Wise](https://wise.com/invite/ath/asrind)
- [Join coinbase with my and you will earn some free crypto as well](https://coinbase.com/join/dayana_m40?src=android-link)

Now you can create apps in elastic beanstalk! I will blog creating an app soon.

Hope this helps😁

Feel free to comment with questions or feedback✌️

Happy coding,

Az 👨🏾‍💻

%%[amazonads]