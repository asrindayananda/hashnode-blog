## Create a PHPUnit Test in Magento 2

In your module create a Test folder and add a unit test file

app\code\AzCodez\MagentoTraining\Test\Unit\TestUnitTest.php

Add code to your test class
```
<?php

use PHPUnit\Framework\TestCase;

class TestUnitTest extends TestCase
{
    public function testFirstUnitTest()
    {
        //Arrange

        //Asset

        //Act
        $this->assertEquals(1,1);
    }
}
```

- In command line go to your root of your project and run the test
```
./vendor/bin/phpunit -c dev/tests/unit/phpunit.xml.dist app/code/AzCodez/MagentoTraining/Test/Unit/TestUnitTest.php
```

- You should get success like below

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1635009999872/O1MgA9PIL.png)


If this didn't please comment and I will try help you.

Remember to like, post a comment and share this blog if this worked for you.

Happy Coding :)

Asrin

If this helped you consider buying me a coffee :)

%%[buymecoffee]

%%[amazonads]