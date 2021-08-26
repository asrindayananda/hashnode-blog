## Magento 2: Create a module in Magento 2

A module is needed for your custom code to run in magento. Say you want to change some magento code or add your own code. you need a module. This is best practice and this is how a module works. 

Below steps creates a dummy module called AzCodez_MagentoTraining. Rename as you wish

- Create a folder app/code/Unit1/Test. 

- Create a file app/code/AzCodez/MagentoTraining/etc/module.xml

- Add code below

```
<?xml version="1.0"?>
<!-- Module AzCodez_MagentoTraining -->
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Module/etc/module.xsd">
    <module name="AzCodez_MagentoTraining" setup_version="0.0.1"></module>
</config>
```

- Add a registration file and code below

```
D:\xammp\htdocs\magento\app\code\AzCodez\MagentoTraining\registration.php
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
php bin/magento module:enable AzCodez_MagentoTraining
```
```
php bin/magento setup:upgrade 
```
- Your module is now installed!

See [Link to relevant Magento Docs](https://devdocs.magento.com/videos/fundamentals/create-a-new-module/) for more information

If this didn't please comment and I will try help you.

Remember to like, post a comment and share this blog if this worked for you.

Happy Coding :)

Asrin

If this helped you consider buying me a coffee :)

%%[buymecoffee]

References

- Image from - https://repository-images.githubusercontent.com/2884111/4bf49300-b50e-11e9-8d1f-c7add453ddb5
