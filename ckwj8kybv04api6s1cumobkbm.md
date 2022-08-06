## Install Magento 2.4.3 Community on AWS EC2 (Debian 10)

# First Calculate your costs

- https://calculator.aws/#/createCalculator/EC2
- Below we are using
   - US East (N.Virginia)
   - t2.medium
   - 10gb storage 
   - Which should cost only $34.87USD on demand OR $21.95USD if you are using EC2 Savings Plan


# Sign up or in to AWS Console
- Select EC2
- Launch Instances
- Search Debian 
- Choose Debian 10 (HVM), SSD Volume Type 
- Select Choose an Instance Type = t2.medium
- Next Configure Instance Details
- Next Add storage
   -Use minimum 10gb
- Add tag if you want
- Configure Security Group add following
   - SSH = Open to IPs you want to ssh to
   - HTTP = Anywhere
   - HTTPS = Anywhere
- Review and Launch
- Launch
   - Create a new key pair OR use exising one if you want

# Add Static IP to EC2 if you prefer to keep same IP address
- See [this Link](https://aws.amazon.com/premiumsupport/knowledge-center/ec2-associate-static-public-ip/) on how to setup a Elastic IP to your VM

# SSH into VM 
- I am using WSL2 on windows and VScode for this
- Add your .pem key to ~/.ssh folder
- SSH using a VSCode Terminal connected to WSL2
```
ssh -i ~/.ssh/<SSH_KEY_NAME>.pem admin@<PUBLIC_IP_OR_DNS_OF_AWS_EC2_SERVER>
```

# Install Docker  
- Below install steps from this [link](https://docs.docker.com/engine/install/debian/) with slight modifications on commands
- Set up the repository
- Update the apt package index and install packages to allow apt to use a repository over HTTPS:
```
 sudo apt-get update
 sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
- Add Docker’s official GPG key:
```
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
- Use the following command to set up the stable repository. To add the nightly or test repository, add the word nightly or test (or both) after the word stable in the commands below. Learn about nightly and test channels.
```
 echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
- Install Docker Engine
- This procedure works for Debian on x86_64 / amd64, armhf, arm64, and Raspbian.
- Update the apt package index, and install the latest version of Docker Engine and containerd, or go to the next step to install a specific version:
```
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```
```
sudo service docker start
```
- Make docker be able to run by non sudo user
```
sudo usermod -a -G docker admin
```
- Reboot server
```
sudo reboot
```
- Check whether can run docker with normal user
```
docker info 
```
- Install docker compose as we are going to build docker with docker-compose.yml
```
sudo apt install docker-compose
```

# Go to install directory
- Go to directory to install. This directory is already created with permissions already to add your whatever you need
```
cd /home/admin/
```

# Install php7.4
- Update apt
```
sudo apt update
```
- Install wget
```
sudo apt install wget
```
- Install dependancies
```
sudo apt install software-properties-common ca-certificates lsb-release apt-transport-https
```
- Enable SURY repo
```
sudo sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
```
- Install gnupg
```
sudo apt-get update && apt-get install -y gnupg
```
- Import the GPG key for the repository
```
wget -qO - https://packages.sury.org/php/apt.gpg | sudo apt-key add -
```
- Installing PHP7.4
```
sudo apt update
sudo apt install php7.4 
sudo apt-get install php7.4-{bcmath,curl,xml,fpm,gd,intl,mbstring,mysql,zip,soap}
```
- Check php is installed
```
php -v
```
- Should look like this
![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1638029604023/F_Qmd6Y_4.png)

# Install composer in Debian
- Install curl
```
sudo apt install curl
```
- Get composer installer
```
curl -sS https://getcomposer.org/installer -o composer-setup.php
```
- Get composer key from here and update below Hash variable https://composer.github.io/pubkeys.html
```
HASH=906a84df04cea2aa72f40b5f787e49f22d4c2f19492ac310e8cba5b96ac8b64115ac402c8cd292b8a03482574915d1a8
```
- Check installer valid
```
php -r "if (hash_file('SHA384', 'composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
```
- Install composer
```
sudo php composer-setup.php --version=2.1.3 --install-dir=/usr/local/bin --filename=composer
```
- Check installer is installed
```
composer -v
```

# Uninstall apache
- Instructions from [this link](https://www.codegrepper.com/code-examples/shell/debian+10+uninstall+apache2+safe+%3F)   
- stop the apache2 service 
```
sudo service apache2 stop
sudo systemctl stop apache2 
```
- Remove apache2 packages
```
sudo apt-get purge apache2 apache2-utils apache2-bin apache2.2-common
```
- Cleanup
```
sudo apt-get autoremove
```
- Check if the apache has been removed, the following command line should return a blank line
```
which apache2
```

# Install fresh Magento 2.4.3 community edition
- Get repo
```
composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition
```
- When it asks you for auth keys, get them from these instructions and store them 
    - https://devdocs.magento.com/guides/v2.4/install-gde/prereq/connect-auth.html
- Go to directory
```
cd project-community-edition
```
- Run composer require
```
composer require --no-update --dev magento/ece-tools magento/magento-cloud-docker
```
- Create a .magento.docker.yml file
```
nano .magento.docker.yml 
```
- Add below, make sure you format yml correctly
```
  name: magento
  system:
  mode: 'production'
  services:
  php:
    version: '7.4'
    extensions:
        enabled:
            - xsl
            - json
            - redis
  mysql:
    version: '10.4'
    image: 'mariadb'
  redis:
    version: '6.0'
    image: 'redis'
  elasticsearch:
    version: '7.9'
    image: 'magento/magento-cloud-docker-elasticsearch'
  hooks:
  build: |
    set -e
    php ./vendor/bin/ece-tools run scenario/build/generate.xml
    php ./vendor/bin/ece-tools run scenario/build/transfer.xml
  deploy: 'php ./vendor/bin/ece-tools run scenario/deploy.xml'
  post_deploy: 'php ./vendor/bin/ece-tools run scenario/post-deploy.xml'
  mounts:
  var:
    path: 'var'
  app-etc:
    path: 'app/etc'
  pub-media:
    path: 'pub/media'
  pub-static:
    path: 'pub/static'
```
- Run install  (This may error, but ignore it)
```
curl -sL https://github.com/magento/magento-cloud-docker/releases/download/1.2.3/init-docker.sh | bash -s -- --php 7.4
```
  - Dont worry about this error
  ```
Installing dependencies (including require-dev) from lock file
Warning: The lock file is not up to date with the latest changes in composer.json. You may be getting outdated dependencies. It is recommended that you run `composer update` or `composer update <package name>`.
  Your requirements could not be resolved to an installable set of packages.
```
- [Get a domain name from AWS R53](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-register.html)  or whereever you prefer
- Build dockers and install
```
composer update
docker volume create --name=magento-sync
docker volume create --name=mymagento-magento-sync
./vendor/bin/ece-docker build:compose --mode="developer" --with-cron --expose-db-port=3306 --no-tls --host=<ADD_YOUR_HOST>.com
docker-compose up -d
docker-compose run --rm deploy php ./vendor/bin/ece-patches apply
docker-compose run --rm deploy cloud-deploy  || true 
docker-compose run --rm deploy cloud-deploy  || true
docker-compose run --rm deploy magento-command deploy:mode:set developer
docker-compose run --rm deploy cloud-deploy  || true
docker-compose run --rm deploy cloud-deploy  || true 
docker-compose run --rm deploy magento-command deploy:mode:set developer
docker-compose run --rm deploy magento-command config:set web/secure/use_in_adminhtml 0
docker-compose run --rm deploy magento-command config:set web/secure/use_in_frontend 0
docker-compose run --rm deploy magento-command config:set web/unsecure/base_url http://<ADD_YOUR_HOST>.com/
docker-compose run --rm deploy magento-command config:set web/secure/base_url http://<ADD_YOUR_HOST>.com/
docker-compose run --rm deploy cloud-deploy
docker-compose run --rm deploy magento-command deploy:mode:set developer
```
- Point your domain at your EC2 at EC2 resource using Route53 point at resource or get Public IP of your EC2 and forward your domain to that IP

- Load your shop ```http://<ADD_YOUR_HOST>.com/```

- This site is setup as dev environment at the moment. If going into production you need to switch site to production mode and check security settings

# Credits 
- Docker image https://mobile.twitter.com/docker
- AWS EC2 Image https://www.google.com/url?sa=i&url=https%3A%2F%2Fdev.to%2Faziz_amghar%2Fall-you-need-to-know-about-ec2-instance-55na&psig=AOvVaw2-8_PE61VZ-QhdiAJG2BmZ&ust=1638118229172000&source=images&cd=vfe&ved=0CAsQjRxqFwoTCNiAk5qAufQCFQAAAAAdAAAAABAI
- Magento 2 logo https://en.wikipedia.org/wiki/Magento
- https://calculator.aws/#/createCalculator/EC2
- https://docs.docker.com/engine/install/debian/
- https://www.codegrepper.com/code-examples/shell/debian+10+uninstall+apache2+safe+%3F
- https://devdocs.magento.com/
- https://www.adobe.com/
- https://aws.amazon.com/

Feel free to comment questions or feedback✌️

Happy coding,

Az 👨🏾‍💻

%%[amazonads]