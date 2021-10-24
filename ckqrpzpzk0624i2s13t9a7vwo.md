## Magento 2: Create a module in Magento 2

A module is needed for your custom code to run in magento. Say you want to change some magento code or add your own code. you need a module. This is best practice and this is how a module works. 

Below steps creates a dummy module called AzCodez_MagentoTraining

- Create a folder app/code/AzCodez/MagentoTraining 

- Create a file app/code/AzCodez/MagentoTraining/etc/module.xml

- Add code below

```
<?xml version="1.0"?>
<!-- Module AzCodez_MagentoTraining -->
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="AzCodez_MagentoTraining" setup_version="0.0.1">
        <!-- Add modules that this module dependent on 
        <sequence>
            <module name="Magento_Catalog"/>
        </sequence>
        -->
    </module>
</config>
```

- Add a registration file app/code/AzCodez/MagentoTraining/registration.php
- Add code below

```
<?php
/**
 * Module AzCodez_MagentoTraining
 */
\Magento\Framework\Component\ComponentRegistrar::register(
    \Magento\Framework\Component\ComponentRegistrar::MODULE,
    'AzCodez_MagentoTraining',
    __DIR__
);
```

- Run following commands from your root folder
```
php bin/magento setup:upgrade 
php bin/magento module:enable AzCodez_MagentoTraining
```
    - If you are running Magento cloud run
```
docker-compose run --rm deploy cloud-deploy
docker-compose run --rm deploy magento-command module:enable AzCodez_MagentoTraining
```
- If you get 'No modules were changed.' Your module is now installed!
- Double check its installed properly by searching AzCodez_MagentoTraining in your app\etc\config.php

- If you get error module not found
    - Double check where you put the module.xml and registration.php
    - module.xml goes under etc folder and registration goes in root of MagentoTraining folder

- Now you can create your own module by Modifing 'AzCodez' and 'MagentoTraining' in above instructions to your own preference

If this didn't please comment and I will try help you.

Remember to like, post a comment and share this blog if this worked for you.

Happy Coding :)

Asrin

If this helped you consider buying me a coffee :)

%%[buymecoffee]

References
- See [Link to relevant Magento Docs](https://devdocs.magento.com/videos/fundamentals/create-a-new-module/) for more information
- Image from - https://repository-images.githubusercontent.com/2884111/4bf49300-b50e-11e9-8d1f-c7add453ddb5
