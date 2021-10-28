## PHPUnit checking method is called once


Below we are going to use PHP Unit to check if a function was called inside a method.

- First setup your class that you are going to test. 
- This is a simple class with two functions. mainFunction calls secondFunction.

```
<?php

namespace AzCodez\MagentoTraining\Controller;

class TestOneMethod
{
    public function mainFunction()
    {
        $this->secondFunction();
    }

    public function secondFunction()
    {
        return 1;
    }
}
```

Setup your php unit test
- First setup basic configuration of calling php unit dependency so we can run tests

```
<?php

use PHPUnit\Framework\TestCase;

class TestOneMethodCallsTest extends TestCase
{
   
}
```

- Then add real class dependency and setup a variable for it

```
<?php

use PHPUnit\Framework\TestCase;
use AzCodez\MagentoTraining\Controller\TestOneMethod;

class TestOneMethodCallsTest extends TestCase
{
    /**
     * @var TestOneMethod
     */
    protected $testOneMethod;

}
```

- Add a new test funtion with comments for arranging the test, asseting (checking), and calling real class to php unit tests your class

```
<?php

use PHPUnit\Framework\TestCase;
use AzCodez\MagentoTraining\Controller\TestOneMethod;

class TestOneMethodCallsTest extends TestCase
{
    /**
     * @var TestOneMethod
     */
    protected $testOneMethod;

    /**
     * 
     */
    public function testFirstUnitTest()
    {
        //Arrange

        //Asset

        //Act

    }
}
```

- Add to Arrange setting up of method. 
- We are mocking method so we can test it here
- We don't need to set method of 'mainFunction' as we want 'mainFunction' to act like normal and call our secondFunction. We don't want to do any mocking with 'mainFunction'

```
<?php

use PHPUnit\Framework\TestCase;
use AzCodez\MagentoTraining\Controller\TestOneMethod;

class TestOneMethodCallsTest extends TestCase
{
    /**
     * @var TestOneMethod
     */
    protected $testOneMethod;

    /**
     * 
     */
    public function testFirstUnitTest()
    {
        //Arrange
        $this->testOneMethod = $this->getMockBuilder(TestOneMethod::class)
            ->setMethods(['secondFunction'])
            ->getMock();

        //Asset

        //Act

    }
}
```

- Add assert
- Here we are testing if the 'secondFunction' is called only once

```
<?php

use PHPUnit\Framework\TestCase;
use AzCodez\MagentoTraining\Controller\TestOneMethod;

class TestOneMethodCallsTest extends TestCase
{
    /**
     * @var TestOneMethod
     */
    protected $testOneMethod;

    /**
     * 
     */
    public function testFirstUnitTest()
    {
        //Arrange
        $this->testOneMethod = $this->getMockBuilder(TestOneMethod::class)
            ->setMethods(['secondFunction'])
            ->getMock();

        //Asset
        $this->testOneMethod->expects($this->once())
        ->method('secondFunction');

        //Act

    }
}
```

- Finally add act. This is where php unit test calls our real class

```
<?php

use PHPUnit\Framework\TestCase;
use AzCodez\MagentoTraining\Controller\TestOneMethod;

class TestOneMethodCallsTest extends TestCase
{
    /**
     * @var TestOneMethod
     */
    protected $testOneMethod;

    /**
     * 
     */
    public function testFirstUnitTest()
    {
        //Arrange
        $this->testOneMethod = $this->getMockBuilder(TestOneMethod::class)
            ->setMethods(['secondFunction'])
            ->getMock();

        //Asset
        $this->testOneMethod->expects($this->once())
        ->method('secondFunction');

        //Act
        $this->testOneMethod->mainFunction();
    }
}
```

- Run your test (I am running a magento instance with phpUnit inside vendor/bin/phpunit folder

```
./vendor/bin/phpunit -c dev/tests/unit/phpunit.xml.dist app/code/AzCodez/MagentoTraining/Test/Unit
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1635450474608/wY97LfG8r.png)

- If you want to check if you are testing properly change your assert to check if secondFunction never calls like below

```
<?php

use PHPUnit\Framework\TestCase;
use AzCodez\MagentoTraining\Controller\TestOneMethod;

class TestOneMethodCallsTest extends TestCase
{
    /**
     * @var TestOneMethod
     */
    protected $testOneMethod;

    /**
     * 
     */
    public function testFirstUnitTest()
    {
        //Arrange
        $this->testOneMethod = $this->getMockBuilder(TestOneMethod::class)
            ->setMethods(['secondFunction'])
            ->getMock();

        //Asset
        $this->testOneMethod->expects($this->never())
        ->method('secondFunction');

        //Act
        $this->testOneMethod->mainFunction();
    }
}
```

- You should get error like below


![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1635450662717/T5wRciMdr.png)

Hope this works for you. Let me know if you get stuck. 

Happy Coding,
Asrin

If this helped you consider buying me a coffee :)

%%[buymecoffee]

References
- https://phpunit.readthedocs.io/en/9.5/
- https://stackoverflow.com/questions/25214407/how-to-use-phpunit-to-test-a-method-that-calls-other-methods-of-the-same-class