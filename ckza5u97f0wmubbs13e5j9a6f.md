## Create a frontend page in Magento 2

Below are steps to how I created a front-end page using a controller in Magento 2. 

[Create a module](https://blog.azcodez.com/magento-2-create-a-module-in-magento-2)

- Create folders and paths as this example. Replace AzCodez\Page with your module.
   - app\code\AzCodez\Page\Controller\Action\Index.php

- In Index.php add the below code.
   -  This class creates a page and sets page contents to 'Hello From Custom Page'
   -  Replace AzCodez\Page with your module.

```
<?php
/**
 * Render page
 * 
 */
namespace AzCodez\Page\Controller\Action;

use Magento\Framework\View\Result\PageFactory;
use Magento\Framework\App\Action\Action;
use Magento\Framework\App\Action\Context;
use Magento\Framework\Controller\ResultInterface;

/**
 * Class Index
 * @package AzCodez\Page\Controller\Action
 */
class Index extends Action
{

 	/**
 	* @var PageFactory
 	*/
 	protected $_pageFactory;

 	/**
 	* Index constructor.
 	* @param Context $context
 	* @param PageFactory $pageFactory
 	*/
 	public function construct(
        Context $context,
        PageFactory $pageFactory
    )
    {
        $this->_pageFactory = $pageFactory;
        return parent::__construct($context);
 	}

 	/**
 	* @return ResultInterface
 	*/
 	public function execute()
 	{
        $result = $this->resultFactory->create(\Magento\Framework\Controller\ResultFactory::TYPE_RAW);
        $result->setContents('Hello From AzCodez Custom Page');
        return $result;
 	}

}

```

- Create a route to route the page to the frontend.  Replace AzCodez\Page with your module.
   - This is the file path app\code\AzCodez\Page\etc\frontend\routes.xml

- Add code for route. Replace AzCodez_Page with your module name
```
<?xml version="1.0"?>
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:App/etc/routes.xsd">
    <router id="standard">
        <route id="product_list" frontName="product_list">
            <module name="AzCodez_Page" />
        </route>
    </router>
</config>
```

- Run deploy commands 
- If not running docker remove `docker-compose run --rm deploy magento-command` and replace with `php bin/magento`
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

- Load the page 
http://magento2.docker/product_list/action/index

# Shameless Plugs
- Join me and invest commission-free with Freetrade. Get started with a free share worth £3-£200. https://magic.freetrade.io/join/asrin/447192e9
- Want to start a blog on hashnode use this [link ](https://hashnode.com/@azcodez/joinme) so I get a free shirt. I will assist you with setup 🙂
- Sign up for coinbase and get £7.42 of Bitcoin http://coinbase.com/join/dayana_m40?src=android-link

# Credits 
- [Magento 2 / Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html)
- [Magento Dev Docs](https://devdocs.magento.com/)

Feel free to comment if you get stuck or have questions or feedback✌️

Happy Coding 🙂

Az 👨🏾‍💻
