## Creating database tables and adding data in Magento 2 Adobe Commerce

## Create a db schema 
- Reference https://devdocs.magento.com/guides/v2.4/extension-dev-guide/declarative-schema/db-schema.html
- Path will be a similar path to this
app\code\AzCodez\CustomerViewing\etc\db_schema.xml

- Add this code to set up your table. Modify table names, columns, types to suit your own
```
<?xml version="1.0"?>
<!-- Database schema -->
<schema xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:Setup/Declaration/Schema/etc/schema. xsd">
    <table name="az_codez_followers" resource="default" engine="innodb" comment="Azcodez followers">
        <column xsi:type="int" name="follower_id" padding="19" unsigned="true" nullable="false" identity="true" comment="Follower id"/>
        <column xsi:type="text" name="name" nullable="false" comment="Follower Name"/>
        <column xsi:type="text" name="email" nullable="false" comment="Follower Contact"/>
        <constraint xsi:type="primary" referenceId="PRIMARY">
            <column name="follower_id"/>
        </constraint>
    </table>
</schema>
```

## Generate  generate db_schema_whitelist.json
```
docker-compose run --rm deploy magento-command setup:db-declaration:generate-whitelist
```

## Redeploy

## Find your table and see if it worked eg.
```
Select * From az_codez_followers;
```

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646408394493/fzvAB2a3I.png)

# Updating a database 

- Following this reference https://devdocs.magento.com/guides/v2.4/extension-dev-guide/declarative-schema/data-patches.html

# Create a data patch
- This file will run on deploy and modify table 
app\code\AzCodez\Databases\Setup\Patch\Data\NewColumn.php

## 
 Add sample code from https://devdocs.magento.com/guides/v2.4/extension-dev-guide/declarative-schema/data-patches.html and add what you want to do 
- Here i will be creating a new table column with this patch

```
<?php
/**
 * Adds new column twitter_handle
 */

namespace AzCodez\Databases\Setup\Patch\Data;

use Magento\Framework\Setup\ModuleDataSetupInterface;
use Magento\Framework\Setup\Patch\DataPatchInterface;
use Magento\Framework\Setup\Patch\PatchRevertableInterface;

class NewColumn implements DataPatchInterface, PatchRevertableInterface
{
    /**
     * @var ModuleDataSetupInterface
     */
    private $moduleDataSetup;

    /**
     * @param ModuleDataSetupInterface $moduleDataSetup
     */
    public function __construct(
        ModuleDataSetupInterface $moduleDataSetup
    ) {
        /**
         * If before, we pass $setup as argument in install/upgrade function, from now we start
         * inject it with DI. If you want to use setup, you can inject it, with the same way as here
         */
        $this->moduleDataSetup = $moduleDataSetup;
    }

    /**
     * @inheritdoc
     */
    public function apply()
    {
        $this->moduleDataSetup->getConnection()->startSetup();
        //The code that you want apply in the patch
        //Please note, that one patch is responsible only for one setup version
        //So one UpgradeData can consist of few data patches
        $this->moduleDataSetup->getConnection()->addColumn('az_codez_followers', 'twitter_handle',
            [
            'type' => \Magento\Framework\DB\Ddl\Table::TYPE_TEXT,
            'length' => 64,
            'unsigned' => true,
            'nullable' => false,
            'comment' => 'twitter'
            ]
        );
   
        $this->moduleDataSetup->getConnection()->endSetup();
    }

    /**
     * @inheritdoc
     */
    public static function getDependencies()
    {
        /**
         * This is dependency to another patch. Dependency should be applied first
         * One patch can have few dependencies
         * Patches do not have versions, so if in old approach with Install/Ugrade data scripts you used
         * versions, right now you need to point from patch with higher version to patch with lower version
         * But please, note, that some of your patches can be independent and can be installed in any sequence
         * So use dependencies only if this important for you
         */
        return [
            SomeDependency::class
        ];
    }

    public function revert()
    {
        $this->moduleDataSetup->getConnection()->startSetup();
        //Here should go code that will revert all operations from `apply` method
        //Please note, that some operations, like removing data from column, that is in role of foreign key reference
        //is dangerous, because it can trigger ON DELETE statement
        $this->moduleDataSetup->getConnection()->endSetup();
    }

    /**
     * @inheritdoc
     */
    public function getAliases()
    {
        /**
         * This internal Magento method, that means that some patches with time can change their names,
         * but changing name should not affect installation process, that's why if we will change name of the patch
         * we will add alias here
         */
        return [];
    }
}
```

## Credits
- https://devdocs.magento.com/
- https://www.adobe.com/

Feel free to comment questions or feedback✌️

Happy coding,

Az 👨🏾‍💻

%%[amazonads]
%%[openinnewtab]