## Install Magento 2.4.3 Community on Docker WSL2

##  Install and activate Windows WSL2
- Follow these instructions to setup your windows for linux subsystem
    - https://docs.microsoft.com/en-us/windows/wsl/install-win10

## Setup Debian 
- In windows search and open Microsoft store 
- Search for Debian App and Install it
- Launch the Debian terminal and create a user account
- Switch to using the "root" user for the whole installation as this is doesnt cause file permission issues for magento generating files NOTE: Only do this on developer environments!
- Change the password for the root user.
``` 
sudo passwd root
```
- Then login under root
```
su root
```
- We then need to set root as the default user for Debian. 
- Close Debian
- Open CMD or Powershell and run
```
debian config --default-user root
```
- The root user has been set as the primary default user for Debian

- Check if you have internet connectivity by running
```
apt update
```
- If not see this for more info https://gist.github.com/coltenkrauter/608cfe02319ce60facd76373249b8ca6

## Install Docker Desktop
-  [See these instructions for installation](https://docs.docker.com/docker-for-windows/install/) 
- Once installed, Open docker desktop > Settings > General and select "Use the WSL 2 based engine".
- Then click on Resources > WSL Integration and select Enable integration with my default WSL distro
- Apply and restart Docker desktop
- After Docker Desktop has reinitialized, restart windows to be save everything is set properly

## Install php7.4 in Debian
- Update apt
```
sudo apt update
```
- Install wget
```
sudo apt install wget
```
- Install dependencies
```
sudo apt install software-properties-common ca-certificates lsb-release apt-transport-https
```
- Enable SURY repo
```
sudo sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
```
- Install gnupg
```
apt-get update
```
```
apt install gnupg
```
- Import the GPG key for the repository
```
wget -qO - https://packages.sury.org/php/apt.gpg | sudo apt-key add - 
```
- Install PHP7.4
```
sudo apt update
```
```
sudo apt install php7.4 
```
```
sudo apt-get install php7.4-{bcmath,curl,xml,fpm,gd,intl,mbstring,mysql,zip,soap}
```
Check php is installed
```
php -v
```

## Install composer in Debian
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
Check installer is installed
```
composer -v
```

## See WSL files
- Open your windows file explorer and put below in your search bar. You will see your Debian installation here
```
\\wsl$
```

## Install magento on docker desktop
- [Referencing these instructions ](https://magepow.com/blog/install-magento-2-on-docker-p1/) 
- Get magento community repository using composer
```
composer create-project --repository-url=https://repo.magento.com/ magento/project-community-edition 
```
- Get magento auth keys
    - Following this link 
         - https://devdocs.magento.com/guides/v2.4/install-gde/prereq/connect-auth.html
    - Rename auth.json.sample to auth.json and add your public and private keys here
    - If asks for authentification required again using cli commands. 
        - Public key = username 
        - Private key = password 
- Go to your install directory of magento
```
cd project-community-edition/
```
- Install magento ece tools
```
composer require --no-update --dev magento/ece-tools magento/magento-cloud-docker
```
- Add .magento.docker.yml file to your repository
    - Check requirements https://devdocs.magento.com/guides/v2.4/install-gde/system-requirements.html
    - Add below code to .magento.docker.yml file (Make sure this is formatted properly)
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
- Run install script (this may error, just continue installing)
```
curl -sL https://github.com/magento/magento-cloud-docker/releases/download/1.2.3/init-docker.sh | bash -s -- --php 7.4
```
 - If you get this error
```
Unable to find image 'magento/magento-cloud-docker-php:7.4-cli-1.1' locally docker: Error response from daemon: Get "https://registry-1.docker.io/v2/": net/http: request canceled while waiting for connection (Client.Timeout exceeded while awaiting headers).
```
    - Look at these links, this will help
        - https://gist.github.com/coltenkrauter/608cfe02319ce60facd76373249b8ca6#file-fix-wsl2-dns-resolution
        - https://stackoverflow.com/questions/59360629/docker-windows-timeout
            - This was my fix - commented out the registry one seems to work now
- Deploy your magento installation (run all at once or remove the && if you want to run one at a time)
```
composer update &&
docker volume create --name=magento-sync && 
docker volume create --name=mymagento-magento-sync && 
./vendor/bin/ece-docker build:compose --mode="developer" --with-cron --expose-db-port=3306 --no-tls --host=magento2.docker && 
docker-compose up -d && 
docker-compose run --rm deploy php ./vendor/bin/ece-patches apply && 
docker-compose run --rm deploy cloud-deploy  || true && 
docker-compose run --rm deploy cloud-deploy  || true && 
docker-compose run --rm deploy magento-command deploy:mode:set developer && 
docker-compose run --rm deploy cloud-deploy  || true && 
docker-compose run --rm deploy cloud-deploy  || true && 
docker-compose run --rm deploy magento-command deploy:mode:set developer && 
docker-compose run --rm deploy magento-command config:set web/secure/use_in_adminhtml 0 && 
docker-compose run --rm deploy magento-command config:set web/secure/use_in_frontend 0 && 
docker-compose run --rm deploy magento-command config:set web/unsecure/base_url http://magento2.docker/ && 
docker-compose run --rm deploy magento-command config:set web/secure/base_url http://magento2.docker/ && 
docker-compose run --rm deploy cloud-deploy && 
docker-compose run --rm deploy magento-command deploy:mode:set developer
```

If you have any errors try redeploy few times
```
docker-compose run --rm deploy cloud-deploy && 
docker-compose run --rm deploy magento-command deploy:mode:set developer && 
docker-compose run --rm deploy magento-command config:set web/secure/use_in_adminhtml 0 && 
docker-compose run --rm deploy magento-command config:set web/secure/use_in_frontend 0 && 
docker-compose run --rm deploy magento-command config:set web/unsecure/base_url http://magento2.docker/ && 
docker-compose run --rm deploy magento-command config:set web/secure/base_url http://magento2.docker/ && 
docker-compose run --rm deploy cloud-deploy && 
docker-compose run --rm deploy magento-command deploy:mode:set developer
```

- If errors on deploy, run cloud-deploy again until it works, this is just initially needs a few deploys
```
Call to undefined method Magento\Eav\Api\Data\AttributeExtension::setIsPagebuilderEnabled()#0 /app/vendor/magento/framework/Interception/Interceptor.php(146): Magento\
  PageBuilder\Plugin\Catalog\Model\Product\Attribute\RepositoryPlugin->afterGet(Object(Magento\Catalog\Model\Product\Attribute\Repository\Interceptor), Object(Magento\Ca
  talog\Model\ResourceModel\Eav\Attribute\Interceptor), 'sku')
```
```
docker-compose run --rm deploy cloud-deploy 
```

- Set your URL to magento instance and https off because its local
```
docker-compose run --rm deploy magento-command deploy:mode:set developer && 
docker-compose run --rm deploy magento-command config:set web/secure/use_in_adminhtml 0 && 
docker-compose run --rm deploy magento-command config:set web/secure/use_in_frontend 0 && 
docker-compose run --rm deploy magento-command config:set web/unsecure/base_url http://magento2.docker/ && 
docker-compose run --rm deploy magento-command config:set web/secure/base_url http://magento2.docker/ && 
docker-compose run --rm deploy cloud-deploy && 
docker-compose run --rm deploy magento-command deploy:mode:set developer
```

- Set varnish
```
docker-compose run --rm deploy magento-command config:set system/full_page_cache/caching_application 2 --lock-env && 
docker-compose run --rm deploy magento-command setup:config:set --http-cache-hosts=varnish &&
docker-compose run --rm deploy cloud-deploy && 
docker-compose run --rm deploy cloud-post-deploy && 
docker-compose run --rm deploy magento-command cache:clean
```

- Add localhost ip to your windows host file
    - Go to C:\Windows\System32\drivers\etc and open hosts file and add
```
127.0.0.1 magento2.docker
```

- Disable vernish as it was loading https 
```
docker-compose run --rm deploy magento-command config:set system/full_page_cache/caching_application 0 --lock-env
docker-compose run --rm deploy cloud-deploy
docker-compose run --rm deploy magento-command cache:flush
docker-compose run --rm deploy magento-command cache:clean
```

- This should load a blank magento luma theme site!
http://magento2.docker/

- To create an admin user run below, add your variables first.
```
docker-compose run --rm deploy magento-command admin:user:create --admin-user=<ADD_USER> --admin-password=<ADD_PASSWORD> --admin-email=<ADD_EMAIL>@gmail.com --admin-firstname=Az --admin-lastname=Codez
```

## Credits
- Windows Image https://www.pngkit.com/view/u2q8a9o0u2o0y3t4_upgrade-gobierno-open-business-logo-windows-10-home/
- Docker image https://mobile.twitter.com/docker
- Magento 2 logo https://en.wikipedia.org/wiki/Magento
- https://docs.docker.com/
- https://devdocs.magento.com/
- https://www.adobe.com/
- https://www.debian.org/

Feel free to comment questions or feedback✌️

Happy coding,

Az 👨🏾‍💻

%%[amazonads]