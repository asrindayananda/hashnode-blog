## Magento 2 - Creating an observer

In Magento 2 (Adobe Commerce) observers are events that are already setup thoughout the whole ecommerce eco-system. 

This is a great way to customise magento. Just find an event that happens and put your custom code in after it. 

Firstly view all observers and pick one you want to use all observers are listed in [here via Adobe Magento Documentation](https://devdocs.magento.com/guides/v2.4/extension-dev-guide/event-list.html) 

Here we will be using checkout_cart_add_product_complete.
This fires when a product has been added to cart.

- If you havent created a custom module please [see my previous blog ](https://blog.azcodez.com/magento-2-create-a-module-in-magento-2) 

- Add events.xml file under your custom plugin eg. app\code\AzCodez\MagentoTraining\etc\events.xml

- Add xml code as below
    - **event name** is the observer we picked to use
    - **instance** is your custom class that you are going to execute after this observer is fired
```
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Event/etc/events.xsd">
    <event name="controller_action_predispatch">
        <observer name="magento_training_test" instance="AzCodez\MagentoTraining\Observer\Log" shared="false" />
    </event>
</config>
```

- Add php observer class, this fires when observer is fired
    - eg. magento2\app\code\AzCodez\MagentoTraining\Observer\Log.php

- Add below php code to this file 
    - This code just logs a message to the system.log file
    - Modify namespace to suit your's

```
<?php
/**
 * Observer Test
 * 
 */
namespace AzCodez\MagentoTraining\Observer;

use Psr\Log\LoggerInterface;
use Magento\Framework\Event\Observer;

class Log implements \Magento\Framework\Event\ObserverInterface
{
 	/**
 	* @var LoggerInterface
 	*/
 	protected $logger;

 	/**
 	* Dependency Constructor
 	* @param LoggerInterface $logger
 	*/
 	public function construct(
 	    LoggerInterface $logger
		)
 	{
        $this->logger = $logger;
 	}

 	/**
 	* @param Observer $observer
 	*/
 	public function execute(Observer $observer) 
	{
        $this->logger->debug("test");
 	}
}

```

Hard Deploy Magento
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

Add product to cart and see if you get a log line in system.log

Hope this was helpful,
Az 😎

Credits
- https://devdocs.magento.com/guides/v2.4/extension-dev-guide/events-and-observers.html
- https://devdocs.magento.com/guides/v2.4/extension-dev-guide/event-list.html#abstract_search_result_load_after
- https://www.mageplaza.com/magento-2-module-development/magento-2-create-events.html
