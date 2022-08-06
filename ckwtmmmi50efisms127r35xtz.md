## Method Chaining in PHP with PHPUnit test

# What is method chaining

Method chaining is where you can call multiple methods after one another in one line like so
```
$methodChain->addHelloToChain()->addSpaceToChain()->addThereToChain()->getOutputOfChain();
```

# Let's write some code 

Setup an initial class with this code which has a few methods that you can call. 

```
<?php

namespace AzCodez\MagentoTraining\Controller\UnitTesting;

class MethodChainingTest
{
    public $outputOfChain = '';

    public function __construct()
    {
        $this->outputOfChain = '';
    }
    
    public function addHelloToChain()
    {
        $this->outputOfChain .= "hello";
        return $this;
    }

    public function addSpaceToChain()
    {
        $this->outputOfChain .= " ";
        return $this;
    }

    public function addThereToChain()
    {
        $this->outputOfChain .= "there";
        return $this;
    }
    
    public function addByeToChain()
    {
        $this->outputOfChain .= "bye";
        return $this;
    }
    
    public function addNowToChain()
    {
        $this->outputOfChain .= "now";
        return $this;
    }

    public function getOutputOfChain()
    {
        return $this->outputOfChain;
    }
}
```

The above four methods are what you call to make your chain.
- addHelloToChain()
- addSpaceToChain()
- addThereToChain()
- addByeToChain()

The last method getOutputOfChain() gets the output of the chain result.

# Write a PHPUnit Test

Now we will write a PHP Unit test, call the chain, and test output. Explanation is in comment of code.
```
<?php

use PHPUnit\Framework\TestCase;
use AzCodez\MagentoTraining\Controller\UnitTesting\TestClassMethodChaining;

class TestMethodChaining extends TestCase
{
    /**
     * Unit test to check method chaining of calling addByeToChain + addNowToChain() + addNowToChain should result in 'bye now'
     */
    public function testMethodChaningHelloThere()
    {
        //Arrange
        $methodChain = new TestClassMethodChaining();

        //Act
        $result = $methodChain->addHelloToChain()->addSpaceToChain()->addThereToChain()->getOutputOfChain();
        
        // Asset
        $this->assertEquals('hello there', $result);

    }

    /**
     * Unit test to check method chaining of calling addByeToChain + addNowToChain() + addNowToChain should result in 'bye now'
     */
    public function testMethodChaningByeNow()
    {
        //Arrange
        $methodChain = new TestClassMethodChaining();

        //Act
        $result = $methodChain->addByeToChain()->addSpaceToChain()->addNowToChain()->getOutputOfChain();
        
        // Asset
        $this->assertEquals('bye now', $result);

    }
}
```

Run the tests 
```
./vendor/bin/phpunit -c dev/tests/unit/phpunit.xml.dist app/code/AzCodez/MagentoTraining/Test/Unit/
```

# Shameless Plugs 
- Join me and invest commission-free with Freetrade. Get started with a free share worth £3-£200. https://magic.freetrade.io/join/asrin/447192e9
- Start a blog on Hashnode https://hashnode.com/@azcodez/joinme

# Credits
- https://www.php.net/
- Image https://unsplash.com/photos/2zGTh-S5moM

Feel free to comment with questions or feedback✌️

Happy coding,

Az 👨🏾‍💻

%%[amazonads]