## Magento 2: Blank page after compiling on Developer Environment


After re-compiling Magento 2 sometimes you get a blank page. Below is solution to fixing this issue

- Deleting the global.php file which is under - magento\generated\metadata\global.php

- If you want to delete it via command line run this
```
rm -rf <PathToYourRootDirectory>\generated\metadata\global.php
```

Re-load your page and it should load.

%%[buyMeCoffee]

Happy Coding,
Asrin