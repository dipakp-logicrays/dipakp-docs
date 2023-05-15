Magento Open Source 2.3.0 Release Notes
=======================================

**Official link**: https://devdocs.magento.com/guides/v2.3/release-notes/ReleaseNotes2.3.0OpenSource.html

Release notes published November 28, 2018 and last updated on June 3, 2020.

We are pleased to present Magento Open Source 2.3.0 General Availability. This release includes numerous functional fixes and enhancements.

Merchant tool enhancements
--------------------------

**Inventory Management provided by `Magento Inventory (was MSI) <https://github.com/magento/inventory>`_** is now available with Magento 2.3.0. It lets merchants manage inventory for all product types in a single warehouse and across complex shipping networks. Merchants can manage these locations as sources, tracking on-hand inventory quantities per product. Stocks map these sources and sales channels (websites) to provide an accurate, salable quantity as inventory pools for concurrent checkout and product reservations. Inventory Management also updates order and shipment options, giving you full control over your stock.

Improved developer experience
-----------------------------

*  **PWA Studio** is a set of tools that support the development, deployment and maintenance of progressive web applications. See `Magento PWA documentation <https://developer.adobe.com/commerce/pwa-studio/>` for information about this toolset as well as information about contributing to this ongoing project.

*  **Declarative schema** simplifies installation and upgrade procedures for Magento and extensions. Declarative schema reduce the need for many database scripts, eliminating the need to maintain these scripts. And here's a big advantage: This features enables Magento to roll out database schema changes in patch releases (not currently possible). This feature supports split and shared database structures and database structure validation.

*  **GraphQL API** is now available with Magento 2.3.0. This API provides an alternative to REST and SOAP web APIs for custom frontend development, including headless storefronts and PWAs.

*  **Asynchronous Web APIs** allow any previous Magento REST APIs to be called asynchronously. This community-contributed feature includes separate status APIs that have been created to check the status of each request. Developers can now use the asynchronous APIs  in conjunction with queues that have also been migrated to Magento Open Source.

*  **Bulk Web APIs**  allow all existing REST APIs to accept payloads with multiple entities. These community-contributed bulk APIs support more efficient and scalable implementations that eliminate round-trip network overhead. Like asynchronous APIs, bulk web APIs can be used in conjunction with queues that have also been migrated to Magento Open Source. 

*  **Updates to Magento's tech stack (including upgraded PHP support to maintain PCI compliance)** include upgrades to Redis, MySQL, Elasticsearch, compatibility with PHP 7.2.x.

Substantial security enhancements
---------------------------------

*  Over 30 security fixes to core Magento code

*  Cache flush ACL provides granular access to cache management settings to prevent accidental changes that could potentially affect system performance. This ACL also lets merchants control which administrative users can clear site caches.

*  2FA/CAPTCHA protects the Admin against stolen passwords and affects stores against bots.


Core bundled extension enhancements
-----------------------------------

Amazon Payments
~~~~~~~~~~~~~~~

*  Added branding to the Amazon Pay configuration section in the Admin

*  Improved extension architecture and performance

dotmailer
~~~~~~~~~

*  dotmailer now supports the {{site.data.var.ee}} split database mode.

Klarna
~~~~~~

*  Added descriptive text to the Refund API call

*  Added a link to the Klarna merchant portal

*  Added a detailed Klarna message in the Admin where needed

*  Added an initial Magento Functional Test Framework (MFTF) test and support for future tests

*  Extended cleanser filtering

*  Added support for PHP 7.2 and dropped support for PHP 5.6

Magento Shipping
~~~~~~~~~~~~~~~~

*  The Magento Shipping **Click & Collect** feature offers merchants the ability to:

   *  Provide Click & Collect as a shipping option to customers, enabling them to directly collect shipments from designated source locations or stores

   *  Configure source locations available for Click & Collect pick-ups

   *  Updates to Shipment Form for UPS (U.S. only)

   *  Customers can also select Click & Collect locations during checkout. This feature is supported by workflows and notifications for Click & Collect pick up, packing, and collection.

*  The batch details page now displays collection point addresses, as applicable

*  Activation notices can now be translated.

*  Tracking popups for multi-package shipments are now displayed.

*  The dispatch details page has been enhanced.

Vertex
~~~~~~

*  The Magento implementation of Vertex now supports Vertex O Series 7.0.

Other improvements
------------------

*  **Elasticsearch support for Magento Open Source version**. Elasticsearch support was previously provided in {{site.data.var.ee}} only.

*  **Improvements to release packaging** plus an increase in test automation, results in a faster, more efficient release process and improved product quality.

*  Upgrade of Magento Functional Test Framework (MFTF) to 2.3.6.

Installation, upgrade, deployment
---------------------------------

*  Magento backup functionality is no longer enabled by default, and the code has been deprecated.


*  All existing installation and data scripts have been converted into declarative schema data patches for easier deployment.


*  The `bin/magento setup` command now provides a rollback option that prompts the user to optionally retain files for future rollbacks. 


*  The `user.ini` files now recommend the correct values for `php_value memory_limit`.

*  You can now use the `bin/magento cron:install`  and `cron:remove` commands to install or uninstall cron across multiple Magento installations with the same crontab. Previously, you could not create different crontab entries for multiple Magento installations that were in different folders because they used the same `#~ MAGENTO START` and `#~ MAGENTO END` suffixes.


*  The default time setting for `cron` success  and failure history is now seven days.


*  In Magento deployments using multiple languages, the `Framework/translation.php` constructor that sets a store's locale now uses the correct locale.


*  The `.htaccess` template now uses Apache 2.4 syntax.

*  When a callback during commit throws an exception, the calling plugin can now distinguish this exception from an unsuccessful commit, and logs an exception. Previously, Magento threw an asymmetric transaction rollback error.

*  The links that the Admin provides to backup packages now link to the expected packages. Previously, these links permitted you to download only the latest backup package.


*  All `cron` schedule times are now saved in UTC and then displayed to the user in the expected time zone. Previously, the `cron` schedule times in the database were in local date time formats and not UTC, while the other system dates and times were saved as UTC in the database.

*  You can install and deploy Magento without first creating an administrator account.


*  Improved the cron job management process during the deploy phase to prevent database locks and other critical issues. Now, all cron jobs stop during the deploy phase and restart after deployment completes.


*  Statistics collection for the Reports module is now disabled by default. To enable or partially disable it, see **System Configuration** > **General** > **Reports**. Note that certain product features, such as  dynamic customer segments (specifically the ones based on viewed products), rely on Reports data collection to function properly.


*  You can now add a new IP address to an existing list by appending the new address with the `- add` flag rather than replacing a former address with a new one. 


*  Magento now provides an input/output helper object that supports easier access to styling objects in the Symfony console.

*  The `.htaccess` file in the `pub/static` folder now includes a `RewriteBase` directive, which supports the installation of Magento under a directory inside the web root. Note: Setting this directive in the `.htaccess` file in Magento root  without setting it in `.htaccess` under `pub/static`  will result in a missing file.


*  The list of IP addresses for maintenance status no longer includes commas, which facilitates directly copy and pasting the addresses as needed.  

*  `PhpFormatter` has been refactored to recursively return the array representation using short array syntax `[]` instead of long `array()`. If the given variable is not an array, it uses the standard `var_export` behavior. This change supports Magento coding standards. 


*  The icons that represent the Extension Manager and Module Manager in the main area and left-hand menu of the Web Setup Wizard have been refactored for consistency with Magento UI guidelines.

*  You can now deploy static content on demand while in production mode.


*  Magento now restarts cron jobs as needed after a cron job was terminated during execution.


*  The `CrontabManager.php` file has been updated as follows: If `crontab` has already been populated, the `bin/magento cron:install` command adds `#~ MAGENTO START` and the rest of code directly to the last row of crontab without any spaces. 


*  `Zend_Json` in the setup `PackagesAuth` has been replaced with the new `Serializer\Json`.


*  Static versioning and minification no longer  break email font styles.


*  We've fixed an issue with using the command line to install or remove `crontab`. Previously, installing or removing `crontab`  via the command line appended `2>&1` to entries, even those not related to Magento. 


*  The **Back** button that was previously accessible during the first step of installation has been disabled.


*  Multifields that previously lacked labels in forms now display labels. 


*  The `app:config:dump` command now has an argument that supports dumping only the specified settings that are required to prepare static content on a build system, not all system settings. This new option (`config-types`) makes it possible to dump scopes and themes automatically (which are needed for a build system) while managing system settings manually using `config:set --lock-config`.


*  You can now switch to default mode from production mode. Previously, if you tried to switch back to default mode, Magento displayed this error, `Cannot switch into given mode 'default'`.


*  The Web Setup wizard now loads successfully when session storage is configured to use memcache in `env.php`.

*  Triggers now work as expected during database backup. Previously, triggers were missing, which resulted in incorrect indexing.


*  Magento no longer automatically disables maintenance mode during a scheduled back up.


*  Database rollback with SSH now works as expected.


*  New command-line interface commands that support enabling and disabling the Magento Profiler have been added.


*  A fatal error no longer occurs when you run `bin/magento sampledata:deploy`  before installing Magento.  

*  Disabling the Amazon Payments feature while using the Web Wizard to  install Magento no longer breaks the checkout process.

Web server configuration
~~~~~~~~~~~~~~~~~~~~~~~~

*  `web/unsecure/base_url` config has been added to website and store scope. 


*  The `static/` string has been removed from the `resource` parameter, allowing `static.php` to generate the specified resource correctly.

*  Fixed an issue with the shared configuration settings in `app/etc/config.php` that caused `recursion detected` errors during deployment.


*  You can now set a default value to fields with config field type `image` or `file`. 


*  We've removed `Zend_Json` from `Setup/Migration.php`. 


*  The licenses listed in `composer.json` have been updated for accuracy.


*  Magento multi-store installations now use the store view-specific values from the Store Configuration if they differ from the global default configuration settings. Previously, Magento loaded the wrong home page in multi-store deployments.

*  Magento no longer displays deprecated currencies in the currency dropdown menu that is displayed during the setup process.


*  You can now successfully create a new store view from the Admin. Previously, Magento displayed this message when you attempted to create a new storeview: `Requested store is not found`.

*  Magento now sends order sent email as expected.

*  The output of the `setup:static-content:deploy` command has been  changed to a less alarming color. 

*  XML sitemap generation can now be scheduled.


*  Issues with the database backup command have been resolved.

*  Magento now displays a more informative message you update a module and then switch to a different branch of source control that contains a lower version of that module.


*  Disabling the **State is Required for** field from **Admin** > **Stores** > **Settings** > **Configuration** > **General** now works as expected.

Fixed issues
------------

Analytics
~~~~~~~~~

*  PHPDocs have been added as needed for methods throughout the code base. 


*  Users are now subscribed by default to the Advanced Reporting service.

Backend
~~~~~~~

*  Customers can now successfully download and export PDFs after logging in. Previously, customers were redirected to the Admin when trying to download or export data to a PDF right after logging in. 

*  Admin tabs are now ordered as expected. Previously, when you used the `addTabAfter` method to add two or more tabs to the Admin (for example, to the order view page), the sort order of the tabs was incorrect. 

*  The headers of the User Agent Rules table now align as expected with the content of the table's rows.


*  The **Enter** button on the customer grid now filters the table as expected. Previously, clicking **Enter**  did not filter contents but simply changed the display to the next page of the grid.

*  The **Report an Issue** link on Admin pages now opens in a new tab. 

Bundle
~~~~~~

*  You can now successfully save updates to bundle products. 

*  Unused `count()` methods have been removed from template files throughout the code base.


*  You can now successfully delete an option from a bundle product.


*  Imported bundle products are now assigned stock status as expected. Previously, when you imported a new or replacement bundle product, Magento did not generate an entry  in `cataloginventory_stock_status`, and as a result,  Magento could not successfully display the product on the storefront.


*  Magento no longer includes expired special prices for bundle options when displaying product price ranges. 


*  Reports now handle bundle and group products as expected. Previously, when a merchant viewed the Products in cart report, the report gives error if the cart contains a bundle or a grouped product.

CAPTCHA
~~~~~~~

*  Customers can now successfully log in when guest checkout is disabled and CAPTCHA is enabled. Previously, Magento threw the `Provided form does not exist` error when a customer tried to log in under these conditions.


*  CAPTCHA validation now works when the **Website Restrictions** setting is enabled.

Cart and checkout
~~~~~~~~~~~~~~~~~

*  Magento no longer displays an integrity constraint violation error after when a customer reorders a  product with custom options.


*  You can now save emoji in custom product options. 


*  Magento no longer caches warning messages as often as a customer clicks the **Update Shopping Cart** button while the shopping cart page loads. Previously, Magento cached a warning message each time a customer clicked this button while the page loaded in Firefox or Chrome, and this action resulted in multiple warning messages appearing on the top of the shopping cart page.


*  Magento now displays the expected state in the Multishipping New Address form when a customer enters information on the Ship to Multiple Addresses page.


*  `update button.phtml` has been simplified to optimize translation. *Fix submitted by Karla Saaremäe in pull request 12155*.


*  You can now enter zip codes that contain no spaces for locations in the Netherlands. 


*  The text that appears above the billing address field on the checkout page has been edited to remove redundancy. 


*  The One Touch Ordering feature allows users to place orders without going through full checkout. 

*  You can now delete the last product in your shopping cart even when the **Minimum Order Amount** setting (**Admin** > **Sales**) is enabled. Previously, if you tried to delete the last item in your cart under these circumstances, Magento would throw an exception. 


*  The checkout agreements `getList` method was refactored to include a new listing interface that supports the ability to set search criteria. 


*  The shopping cart totals description on the checkout page now displays  discount labels as expected. 


*  The checkout controller's JSON usage has been updated to use `$this->resultFactory->create(ResultFactory::TYPE_JSON);` instead of the object manager.


*  Refreshing the checkout page no longer deletes the shipping address when a guest checks out. Previously, when the persistent shopping cart was enabled, refreshing the check out  page affected information entered into form fields for a guest checkout.

*  Cart price rule condition values now handle commas as expected.

*  When a customer is on the payment page and tries to reorder or retrace her steps backward through the checkout process, Magento now displays all the relevant shipping methods. Previously, Magento displayed only one shipping method under these circumstances.


*  You can now successfully change currency for an order before you complete the order. Previously, if you changed currency, when you  proceeded to checkout by choosing a Bank Transfer Payment as Payment Method, Magento displayed this message: **Your credit card will be charged for**. 


*  Magento no longer combines the Custom Checkout and Shipping steps when Magento loads the checkout page.


*  Magento now alerts customers when a previously applied gift card has been removed during checkout.


*  Guest orders placed with gift cards can now be canceled as expected.


*  Braintree now permits customers to change the billing address on orders when paying with a saved card. Previously, Braintree used the same address for both billing and shipping.


*  Customers can now change an existing  value in the checkout page's  **State/Province** field to an alphanumeric value. Previously, when a customer tried to edit this field in this way, Magento did not place the order, and displayed a descriptive error message.


*  Magento now successfully processes an order that contains products that will be shipped to multiple shipping addresses. Previously, Magento did not complete the order, but displayed an error message.


*  Magento now saves the address that a customer enters during checkout if the customer selects **Save in address book**.  Previously, Magento saved the address, but left the default billing address field empty.


*  Excess requests on the checkout page have been removed. Previously, `customer/section/load` was called four times when Magento loaded the cart for the first time.


*  The alignment of the **Purchased Order Form** button on the Review & Payments page has been corrected.


*  `$.browser` has been deprecated and removed from the code base. 

*  The minicart now updates as expected when a customer adds a configurable product to the cart while accessing the storefront on a device running Internet Explorer 11.x.

*  Magento no longer unchecks the **My billing and shipping address are the same** checkbox when a customer uses an offline custom payment method for an order. Previously, when a customer used an offline custom payment method for an order, Magento unchecked this  checkbox on payment step if the shipping address was updated. 


*  Magento no longer displays an undefined string on the Order Summary page.  

*  Unnecessary blank lines have been removed from `app/code/Magento/Catalog/etc/adminhtml/menu.xml`. 


*  Placeholders for the password field  no longer suggest that a password is optional. Previously, the placeholder for the password field in the checkout page suggested that the password was optional, but after validation, Magento indicated that the password field  was mandatory.

*  The minicart now correctly displays product titles that contain special characters.

*  A shipment step has been added to `OnePageCheckoutOfflinePaymentMethodsTest`.


*  Newly registered customers can now successfully complete an order after entering a new address. Previously, Magento displayed this message on the checkout page: `An error occurred on the server. Please try to place the order again.`


*  Merchants can now successfully add products to the shopping cart using REST. Previously, the shopping cart displayed a total price of zero (0) for products creating from the Admin using REST.

*  Customers can now successfully sign in after first clicking the **Checkout** button.

*  Magento now successfully processes an order even when the customer quickly double-clicks on the minicart's **Proceed to checkout** button. Previously, if a customer double-clicked this button while the page was loading, Magento emptied the shopping cart.


*  Magento now displays a pre-filled edit form for checkout agreements when single-store mode is enabled.

Cart Price rules
~~~~~~~~~~~~~~~~

*  The cart price rule now uses specified conditions correctly when applying discounts on configurable products.


*  Magento no longer throws an error when a customer applies a discount code on the checkout page. 

Catalog
~~~~~~~

*  The `getUrl` method in `Magento\Catalog\Model\Product\Attribute\Frontend\Image` no longer returns an image URL with double slashes. 

*  An incorrect return type in the `StockRegistryInterface` API has been corrected.

*  Magento no longer throws an error when you try to create a new URN catalog for a project when a blank one already exists in PHP storm. 

*  You can now save a product after updating multiple select attributes through mass action. 


*  Magento now currently handles apostrophes in attribute option values created from the Admin.

*  The Save & Duplicate option in the catalog manager now works as expected. 

*  Magento now displays the default validation message for `validate-item-quantity` as expected. 

*  The `Magento\Catalog\Model\ResourceModel\Category\Collection::joinUrlRewrite` method now uses the `storeId` value  set on the actual collection of the store rather than the `storeId` retrieved from the store manager.

*  Magento no longer displays unused product attributes  with a value of N/A or NO on the storefront.


*  Editing an order with backordered items from the Admin now results in a new order with backordered items  correctly marked. 

*  Magento no longer overrides prices with more than two digits after the decimal (for example, 9.4880) by rounding the last two digits.


*  Magento now throws an exception as expected  when a user tries to submit a product review without selecting a star rating. Previously, if a user submitted a product review without selecting a star rating, Magento assigned a one-star rating.

*  Merchants can now successfully change the default label of the **country of manufacture** attribute for an existing product from the Admin.  

*  You can now sort products by quantity from the category page.

*  Magento no longer creates pagination automatically when a product has more than 20 tier prices in the Advanced Pricing area.


*  Magento now alerts you to an error when a merchant tries to save a product without completing required fields.


*  You can now sort products by the store configuration default field  even when this value differs from category default sort by setting. 


*  Magento now displays product alerts in the Admin product edit page when a customer is subscribed to a product's stock or price.


*  The `data-container` class name is now based on view mode. 


*  Parent theme image height settings (specified in `view.xml`) no longer override the height settings assigned to individual images.


*  You can now save a title for a product from the **Product** > **Customizable Options** page. 


*  You can now add a custom fieldset  to the Admin category editor without changing the position of  the General section (that is, the section that contains the **Enable category**, **Include in Menu**, and **Category Name** fields). Previously, Magento moved the General section to the last position of the form. 

*  Magento now maintains product image roles as expected after upgrade. Previously, image roles randomly disappeared from product pages after upgrade.


*  REST search queries in which the `condition_type` is set to `in` or `nin` now return results for all specified values.

*  A type error in the payment void method of the Authorizenet module has been fixed. 


*  You can now add a product with a price of zero (0) to a wishlist.

*  Magento now maintains the default products sort order of "newest first" when you upgrade your Magento deployment. Previously, after upgrade, the default products order in categories changed from "newest first" to "oldest first". 

*  An error with the template notation for `Magento_CatalogWidget` module has been fixed. 

*  Magento no longer throws an error when you re-save a product attribute with a new name.


*  The grouped product page now  shows the lowest price for a simple product.


*  You can now add a new product with custom attributes that has the same name and attributes as a previously deleted product. Previously, Magento did not let you add this new product because a `request_path` with the same value already existed in `table url_rewrite` from the previous product. 


*  Magento now saves the assigned background color for images correctly. Previously, if you updated the background color of a product image, the background color was always black. 


*  You can now assign and save a custom option assigned a price of 0.


*  The ProductRepository SKU cache is no longer corrupted when the value assigned to `cacheLimit` is reached. 


*  The price filter on a product category page now works as expected. Previously, if you applied this filter to a category listing, Magento displayed redundant product listings and unrelated products.

*  You can now successfully create a product from API Product Management in deployments where the Update by Schedule indexer mode is set.


*  Configurable products are no longer displayed on a category page when all children are disabled by mass action and the **Display out-of-stock products** setting is off.


*  Magento no longer displays a 404 error when you change category permissions from Product Detail pages when multistore view is enabled.


*  Magento no longer throws an exception when you add a product with a tiered price reduced to $0.00 to your shopping cart.


*  The **Hide from Product Page** option now works for the child product of a configurable product.


*  Translation functionality has been added  to customer attribute labels in the Admin, making it possible to translate a label as appropriate for the locale of an Admin  user.


*  Magento now displays the Catalog Products List widget  on the storefront. 


*  Magento now respects the maximum depth setting for category navigation. 


*  Category page X-Magento-Tags headers no longer contain product cache identities  when category display mode is set to **Static block only** when Varnish is selected as the cache engine.


*  You can now specify a negative value for a product in the orders **Quantity** field when editing the order from the Admin.


*  You can now create a product date attribute that contains a day value than exceeds 12 (in the format dd/mm/yyyy). Previously, when you created a product attribute with a default date specifying a day greater than 12, Magento did not save the attribute, but instead displayed this error: `Invalid default date`.


*  Sort by Price now works as expected on the catalog search page.


*  Magento now correctly sets a `product_links` position attribute even when the attribute value is not set in a GET request. Previously, only the first two of each link type was shown in the backend or in a GET request response, even though Magento correctly added the product links to the database. 

*  You can now unset a category image on the store-view level when the image is defined on all store views.


*  Usage of EAV indexer tables in CatalogWidget module has been removed.


*  Magento now correctly renders print previews of product compare pages. Previously, the print view did not display text from the right side of the product compare page.


*  The validation hint on the product custom option page  text field now updates as expected with the number of characters left before hitting the maximum.


*  The `PUT /V1/products/:sku/media/:entryId` call updates a product's media gallery as expected.


*  Products no longer disappear from the Admin Product grid  after you delete its active schedule update.


*  Single quotation marks in attribute values are no longer  auto-converted to HTML when saved.


*  The SEO-friendly URL for category pages now works as expected.


*  We've optimized queries on loading product attributes when store scope is used.


*  Products are no longer automatically assigned to websites based on store scope. If a product is assigned to one website only, that relationship is maintained even after the product is saved from the Admin.


*  Product Display Pages (PDPs) now load as expected when a product name contains a double quotation mark. Previously, Magento did not load the image if its name contained double quotation marks.


*  A restricted Admin user who is authorized to access only designated websites can no longer remove products from undesignated websites.


*  Customers viewing a storefront on a mobile device  can now see the text displayed when clicking on the "More Information" accordion anchor without having to scroll back up. Previously, the Mobile PDP accordion widget did not work as expected on mobile devices.


*  Magento now maintains designated sort order for products after saving a product in a category. Previously, product sort order reverted to sorting by product ID.


*  You can now filter successfully by date from the Admin on products in multistore environments. Previously, values in the product creation date field (that is, the date set when **Set Product as New from Date** is selected)  were arbitrarily changed, and filtering did not work.


*  Attributes with no assigned values on a product are no longer displayed with a  value of N/A in the Compare Products page or block as expected.


*  Prices are now visible as expected on the category page for a configurable product when you re-enable them from the Admin. Previously, when you re-enabled a previously disabled product and assigned it to a different store, Magento did not display its price on the category or product page.


*  Category smart rules now work as expected for partial values when conditions include using a dropdown attribute and "contains".


*  Magento now correctly sets the default option for the `status` attribute when a merchant creates a product. Previously, Magento changed a default setting of disabled (**No**) to **Yes** during product creation.


*  `auto_increment` values are now preserved after restarting the MySQL server.


*  You can now successfully save a product with custom options to a different website in multisite deployments. Previously, when you added another site to a product with customizable options, Magento corrupted these options by splitting into multiple options or duplicating an option.


*  A product's **Use Default Value** check box for attributes is now unchecked by default when you add a new website to a product's scope.


*  The subcategory URL path is now updated for a store view according to the URL path of its parent category.


*  Magento now displays drop-down attribute values in the catalog product grid after applying filtering  on drop-down/select attributes. 


*  The JavaScript address converter no longer mutates the function's `address.street` argument. (The argument remains an array as expected.)


*  You can now see category changes on the storefront as expected after the changes have been saved. Previously, Magento did not display changes to product categories on the storefront until reindexing occurred even if the **Update on schedule** setting was set and the cache had been cleaned.


*  Product attribute are now displayed as expected in layered navigation with Elasticsearch 5.0+.


*  Magento now displays category images consistently.  Previously, category images disappeared then reappeared after every save.


*  We've fixed the display of calculated tax for a logged-in customer when billing and shipping address differed.

Catalog Rule
~~~~~~~~~~~~

*  Catalog rules are now applied as expected when products are sorted by price.


*  Product pages now show the product name as the browser title and include meta title tag in the HTML source.  (The title and meta title tags can now be used independently.) 

Cleanup and simple code refactoring
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*  Zoom is no longer abnormally active when  a mouse hovers over the category dropdown menu on the product page.


*  `getAttributeText($attributeCode)`  now returns the correct return type.

*  All references to Magento Connect has been removed from the Find Partners & Extensions links.


*  Method name `getDispretionPath` has been corrected to `getDispersionPath` in  `\lib\internal\Magento\Framework\File\Uploader.php`. 


*  Unused temporary variable `$data` has been removed from the `app/code/Magento/Catalog/Controller/Adminhtml/Category/Save.php` method. 


*  addres has been corrected to address in `app/code/Magento/Customer/etc/events.xml`. 


*  Code formatting in `app/code/Magento/Swagger/view/frontend/templates/swagger-ui/index.phtml` has been updated. 


*  The edit cart product input validators have been changed from hardcoded to dynamic in `app/code/Magento/Checkout/view/frontend/templates/cart/item/configure/updatecart.phtml`. 

*  Typos have been corrected throughout the code base. 


*  Redundant code has been removed for clarity in `app/code/Magento/AdminNotification/Model/Feed.php`. 


*  Misspellings in method names have been fixed, and deprecated methods removed in several adminhtml files.


*  A typo in the database column comment of `app/code/Magento/Catalog/Setup/InstallSchema.php` has been fixed. 


*  Typos throughout the code base have been corrected. 


*  A misspelled method name in `\Magento\BundleImportExport\Model\Import\Product\Type\Bundle` has been corrected. 


*  A misspelled parameter name in `\Magento\Weee\Test\Unit\Model\TaxTest::testGetWeeeAmountExclTax` has been corrected. 

*  Catelog has been corrected to catalog throughout the code base. 


*  Consturctor has been corrected to constructor in the `app/code/Magento/Ui/view/base/web/js/lib/core/class.js` JavaScript class.


*  The syntax of `expectException()` calls has been improved.

*  JavaScript in the Tav module has been refactored to meet Magento code standards.


*  Magento no longer unexpectedly empties a customer's shopping cart during checkout when concurrent requests occur.


*  `@codingStandardsIgnoreFile` has been removed from the `TypeLocatorTest` file header. 


*  Redundant spaces have been removed from the "configure your" phrase throughout the code base. 


*  An unused `if` statement has been removed from `app/code/Magento/Sales/Controller/Adminhtml/Order/Invoice/Save.php`.


*  Magento no longer displays duplicate element IDs for gift messages in the checkout page. 


*  Magento now correctly aligns submenus. 

*  The `app/code/Magento/CurrencySymbol/view/adminhtml/templates/grid.phtml` file has been refactored to remove redundant function calls.


*  Client-side email validation now works in Internet Explorer 11.x the same way as it does in Chrome. Previously, a leading or trailing space on the following pages resulted in  client-side validation failure in Magento stores deployed on Internet Explorer 11.x. 

*  Magento now correctly aligns page elements on  the home page and category page of the Hot Seller section.  


*  Extraneous margins on the product list  and product entries have been removed.


*  `inline-block` issues with space and font-size in the Name form have been resolved.


*  The Shipping and Estimate Tax page now correctly displays country, city, and postal code fields. 

*  Unneeded JavaScript was removed from `logout.phtml` and replaced with a new JavaScript component. 

*  Template syntax errors in `app/code/Magento/Theme/Block/Html/Breadcrumbs.php` have been corrected. 

*  Magento now disables the **Shop By** button on the search page when a customer sets additional search filters. 

*  Product image zoom now works as expected in stores running on Safari. 

*  The `$keepRation` parameter in the `Magento\Cms\Model\Wysiwyg\Images\Storage` class has been renamed to `$keepRatio`. 

*  A typo in `gallery.php` has been fixed.

*  The delete operation `entity_manager_delete_before`  transaction event  is no longer dispatched twice unnecessarily.

*  Unnecessary space has been trimmed from the email address field in the forgot password, check out, log in,  and email to a friend forms.


*  The JavaScript code in the `spli.phtml` template file for the button widget has been refactored.


*  The JavaScript code for the UrlRewrite module edit page has been refactored.


*  The annotation for the `formatDateTime` function in the `lib/internal/Magento/Framework/Stdlib/DateTime/TimezoneInterface.php` file has been corrected. The `locale` and `timezone` have been changed to `param string|null $locale` and `@param string|null $timezone`. 


*  Magento now displays the Contact Us page on the menu as expected. Previously, Magento displayed unnecessary space between the category page and the main footer. 

CMS content
~~~~~~~~~~~

*  Page layout issues that resulted from incorrect module sequencing have been corrected. Previously, the  `Magento_theme`  module was loaded too late, which resulted in unexpected display issues.


*  Magento no longer unexpectedly locks up CMS pages when a merchant changes a scheduler end date. Previously, when a merchant updated the end date for a CMS page after the current scheduler ended, Magento generated an error, and the merchant could no longer access any CMS page from the Admin.


*  We've added `EvenPrefix` and `EventObject` for CMS Collections to instantiate the observer for `$this->_eventPrefix . '_load_after'` and `$this->_eventPrefix . '_load_before'`.


*  There is now an API interface for retrieving CMS pages and blocks by identifiers and store ID.


*  Disabling a product now removes it from the flat index as expected.

*  Breadcrumbs now work as expected when a product name contains quotation marks. Previously, the breadcrumbs on the product details page caused this syntax error to be thrown: `SyntaxError: Unexpected token x in JSON`.

*  CMS blocks are now validated to prevent multiple blocks from having the same store view and identifier.


*  You can now configure the native WYSIWYG toolbar to display only applicable controls. 

*  The **Store** > **Attributes** > **Product** > **Input type** field now supports the use of the WYSIWYG editor as an input method when configuring custom product attributes.

Configurable products
~~~~~~~~~~~~~~~~~~~~~

*  The product configuration creator  now warns about invalid SKUs.


*  The currency symbol no longer  overlaps with an attribute option's price during configurable product creation. 

*  Magento now displays the price of a configurable product as expected even when its simple products are out-of-stock. Previously, Magento displayed a price of 0 for any configurable product price when its simple products were out-of-stock.

*  Magento now displays the correct price for a product when its special-price option has not been selected. Previously, Magento displayed the expired `special_price` value for a configurable product even when you did not select the product option associated with that price.


*  Configurable product prices now correctly reflect VAT amounts as set by tax rule settings. Previously, Magento displayed a configurable product's old price without the VAT.

*  `LowestPriceOptionsProvider` now works as expected. Previously, Magento displayed expired special prices for configurable products, and displayed other problematic behaviors when working with special prices and configurable products.

*  You can now successfully add a new product that contains a custom attribute set with a multiselect attribute from the Admin.  

*  Configurable products are now sorted by visible prices as expected. Previously, sorting a catalog by price produced  sort results that included the prices of out-of-stock products and disabled child products.


*  Magento no longer displays an inappropriate  product price when a configurable product has two price options. Previously, Magento displayed the  out-of-stock price of a configurable product when both an out-of-stock and in-stock price were configured.


*  Magento now reorders configurable attribute options as expected on the product page.

*  Magento now displays a helpful error when  a merchant attempts to upload a file in an unsupported file format.


*  The wishlist now displays the appropriate product image for configurable products with selected options. Previously, Magento displayed the parent image instead of the image of the selected child product.


*  The OptionsRepository API test now tests for the use of attribute ID instead of attribute code in the request body.


*  Prices are now readable when you assign prices that use a  custom price symbol to a configurable product. Previously, the custom price symbol obscured the product price. 


*  Magento now saves multiselect attributes for a product in the Admin when it has a related product that uses another attribute set. 

*  Magento no longer lets a customer select a configurable product with an out-of-stock option to add to their cart. 


*  You can now add customizable options to a product as expected.


*  The orders page now displays the correct URL when you navigate back to it after having viewed a specific order page.  Previously, the URL of the orders page displayed the previous order ID when you navigated back to it.

Cookies
~~~~~~~

*  Customer data is now fully loaded after restarting the browser during an unexpired user session. Previously,  the `section_data_ids` section of the session cookie was not properly completed.

*  Cookies can now be modified by extension.

Customers
~~~~~~~~~

*  Magento now uses the correct amounts when creating a credit memo for an order that was placed using store credit, a gift card, or reward points.

*  Administrators can see all customers when the **Share Customer Accounts** value is set to Global.


*  Magento now loads customer private data only once when system state changes. Previously, "Directory Data" and "Cart" were loaded twice after a user logged in to the system, which caused additional server load and traffic.


*  Magento now correctly displays both the default and additional shipping addresses  provided during checkout. Previously, Magento displayed attributes with dropdown and multiple select types with incorrect values (option IDs instead of labels) for shipping addresses on checkout.


*  We have replaced `Zend_Json`  with `\Magento\Framework\Serialize\JsonConverter::convert` in customer data.  


*  In multi-site deployments, a customer requesting a password reset on a non-default store should receive the password reset email from the non-default, not the primary, store. Previously, this password reset email was sent from the default store. 


*  Unnecessary leading and trailing spaces have been removed from the customer account login page email field. 


*  Table alias prefixes in field mappings for customer group filter and sorting processors that were previously missing have been restored. Previous to this restoration, Magento threw this error when a merchant opened **Admin** > **Customers** > **All Customers**: `SQL Error: ambiguous column 'customer_group_id' in 'All customers' page in admin when extension attribute table is joined`.


*  Customer accounts are now unlocked as expected after a password reset.

*  The  `adminhtml` customer edit page  now displays any customer address validation errors.  *

*  You can now successfully send email to customer email addresses that contain special characters when initiating email but clicking the **Resend Confirmation Mail** button on the customer account page.


*  Magento no longer displays the  `Too many password reset requests` message when an administrator attempts to change a customer's password from the Admin and the **max wait time between password resets** setting has been disabled in the store configuration settings. 


*  We've added methods to support setting text values for data pulled from the `customer_grid_flat` table during CSV export.


*  The Confirmed email and Account Lock columns of the customer table CSV export are now populated with values as expected. 

*  Customer objects are now properly differentiated from each other after a `customer_save_after_data_object` event.  Previously, the `orig_customer_data_object` and `customer_data_object` objects remained identical even after customer information was changed on the storefront. 

*  We've improved the error message that Magento displays when an administrator is redirected to a forced password change from the Admin user account page.

*  Customer attributes are now correctly validated on the Admin Order form. Previously, Magento validated attribute length  after an order has been submitted, but not on the Admin Order form.


*  A user who has been denied permissions for negotiable quote editing can now create customer addresses.


*  Magento now trims trailing and leading spaces when saving the name of a new contact.

*  We've added cast to string for `GroupInterface::CUST_GROUP_ALL` in the customer group source model.


*  Magento now always returns the user data for the current logged user. Previously, you could get another customer's session information from sections controller without a timestamp.


*  The PayPal module no longer automatically sets the customer dashboard page to Billing Agreements.

*  The Customer group menu is now displayed under Customers when you create a user role for a customer group.


*  The welcome email sent to new customers is now based on the ID of the selected store. Previously, Magento did not check if the selected store from which to send the welcome email was associated with website when creating a customer account in the Admin.  

Customer attributes
~~~~~~~~~~~~~~~~~~~

*  You can now clear the **Date of Birth** field in the customer edit page when accessed from the Admin.


*  Merchants can now create attributes  for customer addresses (**Stores** > **Attributes** > **Customer Address**) as expected. Previously, a merchant could create an attribute, but Magento did not save or display it.


*  Magento now adds the address entered during checkout to a new account when a custom address attribute is required when creating a user account after checkout.


*  User-defined customer attributes are now copied to the `magento_customercustomattributes_sales_flat_order`  table after placing an order as expected.


*  Magento no longer validates customer address attribute value length when the minimum/maximum length fields are not displayed on the Admin.

Dashboard
~~~~~~~~~

*  Comments for `StorageInterface.php` have been updated for accuracy.  

*  You can now search for configuration settings from the Admin.


*  Long input field labels now wrap by word, not letter.


*  The dashboard last order table now shows the correct  table for the specified store view in a multisite deployment where storefronts use different currencies. 

*  When you edit an Admin user role, Magento now displays the Customer Groups section under the Customers section as expected. Previously, Magento displayed the Customer Groups section under the **Stores** > **Other settings** section.

Directory
~~~~~~~~~

*  When sorting by price, Magento now displays the same number of products no matter how it sorts products in the Catalog Product list. Previously, Magento reduced the product count by the number of disabled products when sorting by price.

*  Currency conversion rate services now work as expected in the Admin.


*  The new Currency Converter API supports retrieving TWD currency rates. Previously, the currency rates services that Magento connected to by default could not retrieve TWD rates.

*  Magento now displays the default country selection when you add a new address as part of creating a new customer from the Admin. 

dotmailer
~~~~~~~~~

*  dotmailer now displays the first and last purchase categories in the customer sales data fields.

EAV
~~~

*  The Product Attribute Repository's incorrect return values have been replaced with values that now adhere to `Magento\Catalog\Api\ProductAttributeRepositoryInterface (extends Magento\Framework\Api\MetadataServiceInterface)` as expected. 

*  When Elasticsearch is configured as the search engine, you can now enable and disable the EAV indexer from the Enable EAV Indexer field (**Configuration** > **Catalog** > **Catalog Search**).


*  Magento no longer displays empty product attributes of type `dropdown` or `swatch` as having a value of **no** on the storefront.


*  You can now perform a mass update on products that have more than 60 attributes.


*  Magento now displays an error message when  it does not save dropdown values as you create them. Previously, Magento did not save the options, and did not alert you in a message.


*  The `@see` tag now identifies a deprecated property in `app/code/Magento/Eav/Model/AttributeManagement.php`. 


*  When a product is saved, the `beforeSave` method now encodes the attribute value only if the value is not encoded already. Previously, if you saved a product multiple times,  then the JSON-encoded attribute value was also encoded multiple times, which causes problems during subsequent  loads.


*  Magento no longer displays an SQL query in the browser when an exception occurs. 

*  You can now filter an EAV collection before loading by specifying that the value of the attribute is null.

Email
~~~~~

*  Nonfunctioning links in the order confirmation email have been corrected.

Frameworks
~~~~~~~~~~

*  Declared index names in `db_schema.xml` are no longer ignored by declarative schema.  Previously, index names were autogenerated based on table and column names.


*  The `htmlentities` function has been replaced with the `htmlspecialchars` function.


*  Magnifier now works as expected on any supported operating system and browser. Previously, Magnifier did not hover correctly on devices running Windows Chrome or FireFox.


*  Magnifier now turns off as expected when a user moves the cursor off an image.

*  The `ExtensionAttributes` object is now autogenerated.

*  `ObserverInterface` has been added to @api. Previously, creating an observer that uses `ObserverInterface` triggered a patch-level dependency on `magento/framework`.


*  The doc block of the `walk` method in a collection now correctly reflects that this method will accept an array.


*  `getFrontName` has been refactored to return `getModuleName`'s return values. 


*  Emogrifier dependency has been updated to ^2.0.0.  

*  The log message created when Magento throws an exception when opening an image now tells you which file triggered the exception.


*  `Zend_Json` has been removed from the JSON result controller.


*  `\Magento\TestFramework\Annotation\AppArea` no longer breaks when it encounters valid values. 


*  `Zend_Service` has been upgraded from v.1 to v.2, including these specific changes:

   *  Removed `Magento\Framework\Locale\CurrencyInterfac` from the `setService` method and changed it to `\Zend_Currency_CurrencyInterface`, which must be the provider to this function.

   *  Changed return type to `\Zend_Currency_CurrencyInterface`, the given instance of the service is returned by the `setService` function.

   *  Removed `\Zend_Service` from the `getService` method and changed it to `\Zend_Currency_CurrencyInterface`.

   *  Added `@deprecated` tags to both methods and added `@see` annotation to the methods. Referenced the corresponding interface `\Magento\Directory\Model\Currency\Import\ImportInterface`. 


*  The ReleaseNotification module has been added to support the display of new release highlights.


*  Magento now saves date and time correctly for different timezones and locales.

*  The `Zend_Feed::importArray` static call has been replaced with a new interface. This concrete class takes the `Zend_Feed` object and returns its own result in the form of a wrapper around `Zend_Feed_Abstract`.


*  Customers can now successfully check out  when the AdBlock extension and Google Analytics are enabled.


*  Product records inside the `catalog_product_super_link` table are no longer updated needlessly when you save a configurable product. Previously, saving a configurable product erased and then reinserted records in the `catalog_product_super_link` table even when child products were not changed. This practice quickly resulted in an unnecessarily large `catalog_product_super_link` table, especially in multi-website installations.


*  Magento now caches popular search results for faster response time on popular searches. A system administrator can configure how many top search queries can be cached.


*  We've replaced the usage of `Zend_Json::encode`  in the setup marketplace tests. 

*  The `Magento\Framework\Json\Helper\Data` class has been deprecated and removed from the `Magento\AdminNotification` module. 


*  An entry for `compiled_config` cache  has been added to the `cache.xml` file. 

*  The report page now returns a 500 status code (internal server error) instead of a 503 status code when an unexpected error happens,  such as an event that generates the report format pages. 

*  You can now use the layout update XML field to include custom CSS in CMS pages. 

*  The `$params` parameter for the post method of  `\Magento\Framework\HTTP\ClientInterface` has been updated to support string type. 


*  We've added JSON and XML support to the post method in the `\Magento\Framework\HTTP\Client\Socket` class.

*  After restart of MySQL, changelog tables now always contain at least one record. Previously, changelog tables were empty, which resulted in a loss of the last `auro_increment` value for the product `version_id`.

*  Magento now displays two distinct widgets on the homepage as expected when you create two widgets of type `Catalog Product List` to the `CMS homepage` at location `content.bottom` with different titles, but the same condition. Previously, the first widget loaded was displayed twice depending on sort order.


*  The Change Password warning message no longer appears twice when Magento prompts you to change your password in the Admin.


*  Pages are now successfully rendered when the `meta title` page configuration parameter is set.


*  CSS code is now automatically updated in the browser. Previously, users had to press **CTRL+F5**  to see CSS changes. 


*  `\Magento\Framework\Encryption\Encryptor::getHash` now uses the specified hashing algorithm version.


*  The **Multiple Payment Methods Enabled** setting now works as expected. Previously, Magento threw this error when this setting was enabled: `Found 3 Elements with non-unique Id`.

*  The `setAttributeFilter` method  now specifies a table when calling the `addFieldToFilter` method to add a field to the filter for the collection `Eav/Model/ResourceModel/Entity/Attribute/Option/Collection.php`.

*  Categories are now populated as expected. Previously,   `catalog_category_product_index` did not contain all category product relations that are in `catalog_category_product`. The highest category IDs per type were missing from the index. 

*  `vendor/magento/framework/composer.json` now declare a dependency on `\Zend_Db_Select`.  


*  The Admin no longer falls into a redirect loop when an administrator logs in with a role that has no resources assigned. 


*  You can now successfully print out an invoice from the Admin without including order details. Previously,  Magento threw a fatal error because the `Zend_Pdf_Color_RGB` class  was not found in the `_drawHeader` method.

*  The **Stores** > **Terms and Conditions** table now displays the names of all store views and conditions as expected. 

*  We've fixed backward-incompatible changes to transport variable event parameters that had previously resulted in neither the email or the `$transport` variable being changed as expected. 


*  The sodium library now handles all new encryption and decryption  while supporting encryption and decryption of legacy values with mcrypt. )

Application framework
'''''''''''''''''''''

*  We've removed undefined fields from files in `/lib`. 

*  The doc block that describes `setValue` in `FilterBuilder` now reflects that this method will accept an array.

*  Magento now uses valid ISO language codes in HTML headers. 

*  Magento can now generate unsecure URLs if the current URL is secure.


*  The `php bin/magento app:config:dump` command no longer adds an extra space to multiline array values every time it runs. Previously, this command inserted extra spaces, which triggered Github to commit these files as changed. 

*  The `StockItemCriteriaInterface` method `setProductsFilter` now accepts an array of IDs. Previously, this method accepted either a single integer or an array, but returned only one item. 


*  The Magento application framework has been updated to address a jQuery security issue.


*  We've removed the usage of `Zend_Json` from the JSON controller. 

*  The `\Magento\Framework\Serialize\Serializer\Json` class has replaced `Zend_Json usage in Framework/Module/PackageInfo.php`.

*  `Zend_Json` has been removed from the  `DataObject` class. 


*  We've added a declarative mechanism to limit the HTTP methods that a controller can process by implementing one or more `Http<Method>ActionInterface`.


*  `Zend_Json` has been removed from setup and `Webapi` and replaced by `Serializer\Json` in `PackagesAuth`.


*  Classes that contain a *–*  are now rendered as added to the XML. Previously,  *–*  were  replaced with a single *-*.

Configuration framework
'''''''''''''''''''''''

*  An order's `relation_child_id` and `relation_child_real_id` fields are now accurately set during edit operations. 


*  Pages that contain layout files with `block_id` arguments that contain whitespace now load correctly. Previously, Magento threw an error when loading these pages.

*  The config array can now read  all settings from `config`. Previously, the config array was hardcoded to read three settings only.

*  You can now assign a default value to config fields of type `image` or `file`. 

Database framework
''''''''''''''''''

*  The `getSize` function now reflects item and page count totals for filtered product collections on the category page.

JavaScript framework
''''''''''''''''''''

*  Magento now displays video and images as expected when you select a video or click to view a full-screen image for a configurable product. 


*  We've removed duplicate parameters from a Magento UI LESS library mixin. 


*  You can now disable the full-screen gallery on mobile devices.


*  The calendar widget (`jQuery UI DatePicker`) now correctly displays more than one month. 


*  JavaScript files are now located inside the `web/js` directory.


*  Menus with nested elements now align correctly. 


*  Magento no longer incorrectly overly encodes UTF-8 files when JavaScript bundling is enabled. Previously, this issue resulted in poor character encoding on the storefront. 


*  `jquery.mobile.custom.js` is now compatible with jQuery 3.x. 


*  The Fotorama gallery now works as expected on Android devices.


*  The dataprovider constructor has been changed to the `RendererInterface`, making it compatible with custom translators (which can be injected as an argument for `\Magento\Framework\Phrase\Renderer\Composite`). 


*  You can now place an order for a  grouped product where the subproducts quantity is less than one.

*  A JavaScript error in `dropdowns.js` has been fixed by properly initializing the `el` variable. You can now set `options.autoclose` to `false`.  

Session framework
'''''''''''''''''

*  The `sid` variable (`?sid`) no longer appears in the URL even if it is disabled in the Admin. 

*  We've removed the 30-second timeout limit for the session locking mechanism when Redis is used for session storage.


*  `colinmollenhour/php-redis-session-abstract` has been updated to support PHP 7.2. 


*  When you add a product to your wish list after logging out, Magento now redirects you to your account Wish list page and adds the product. Previously, you were redirected to your wishlist page, but Magento did not add the product


*  The shopping cart no longer empties unexpectedly due to concurrent requests during checkout.

General fixes
~~~~~~~~~~~~~

*  Magento now validates  custom layout update XML against the schema file when you save the XML. 


*  You can now successfully close full-screen zoomed product images displayed on an iPhone 4s, 5s, 6, or 6s with the Safari browser. Previously, if you chose full screen zoom for any product image, you could not close the full screen zoom.


*  Deleting a customer from the Admin  no longer causes fatal errors upon storefront login or registration.


*  The **Modified** date field is now updated as expected when you save a page in a deployment running Magento 2.2.1. 

*  When the **Redirect Customer to Account Dashboard after Logging in** setting is disabled, Magento now includes the login URL (including the referrer in base64 encoding) from the `window.checkout` object as expected (for example, https://myshop.com/customer/account/login/referrer/aHR0cHM6Ly9teXNob3AuY29tL2NoZWNrb3V0).


*  Magento now correctly handles `file` or `image` type customer attributes. Previously, when you tried to save customer information when one of these customer attributes were set, Magento threw an exception and did not save the file. 


*  You can now use uppercase letters in store codes.

*  You can now add a new attribute class to a page's XML root by adding an HTML node. Previously, adding an HTML node caused a validation error. 


*  The `\Magento\Quote\Model\ResourceModel\Quote\Item\Collection` now returns items that have only existing relations in the `catalog_product_entity` table. Previously, Magento loaded quote items with non-existing products.


*  Magento now correctly renders the download link in invoice emails.


*  `AuthenticationInterface` now contains API interceptors that enhance user authentication, making it possible (for example) to implement a different hashing algorithm for non-Magento to Magento migrations.


*  The Magento UI mixins have been edited to improve performance. Changes include:

   *  removing all fallbacks to variables that don't exist in the global scope

   *  defining all variables that are used inside mixins as parameters

   *  adding all missing parameters to the areas of the code where mixins are invoked

   *  moving and simplifying mixins used only once.

*  The dashboard y-axis range has been enhanced by the addition of an index for y-axis range values.


*  Lengths for the following fields in the `quote_address` database table have been expanded: `telephone`, `fax`, `region`, and `city`.

*  `Magento\Framework\Escaper` now contains the `escapeDollarSign` method, which looks for `${` and replaces `$` with `$`  during save actions involving the page and block controller.


*  Magento now displays product review summaries only when a product has at least one review.


*  Magento now uses the config field backend model (`system.xml`) to generate default configuration values on the Admin. Previously, the `afterLoad()` method was evoked only after loading the configuration value from the database, and not after loading the configuration from `config.xml`. This caused the default configuration from `config.xml` to be passed to the form element as `string` instead of `Array`, which resulted in empty configuration fields in the Admin.


*  Magento now selects the `CUST_GROUP_ALL` customer group in `adminhtml` after saving an attribute, and all `$customerGroups['value']` are now of type `string`.

*  Session cookies now last until the session closes. Previously, Magento interpreted a `form_key` cookie lifetime of 0 to determine the duration of the cookie lifetime, and the cookie expired immediately.


*  Google Analytics has improved support of websites that conduct transactions in multiple currencies. Previously, payment providers that required different base currencies were configured as different websites in a multisite deployment,  and consequently had to send different base currency in Google Analytics.

*  Google Adwords now has the ability to provide transaction-specific conversion values in a conversion tracking tag.


*  The text in the authentication popup has been corrected to **Checkout as a new customer**. 


*  Customer data is now fully loaded after restarting the browser during an unexpired user session. Previously,  the `section_data_ids` section of the session cookie was not properly completed.


*  `X-Magento-Vary` and `PHPSESSID` now have the same expiration time. Previously, the  `X-Magento-Vary` cookie had an expiration of `session`, which meant it was not considered expired until the browser was closed. In contrast, the `PHPSESSID` cookie had a finite expiration time (not `session`). At times, this resulted in  Magento caching the wrong page for the logged-in user.


*  You can now delete rows in the `dynamicRows` component.

*  Creating new configuration attributes no longer causes naming collisions in the JavaScript UI registry. Previously, when you created a new default attribute and then subsequently created a new product, JavaScript errors occurred.


*  The `\Magento\Test\Php\LiveCodeTest::testCodeStyle`  method now uses whitelist files.

*  Magento now processes the oldest message queue entries first instead of last.


*  You can successfully save a CMS page with same URL key as another store on a different website but with the same hierarchy.


*  You can now successfully preview a Registry Update email template. Previously, Magento threw a fatal error when you tried to preview this template.


*  Enterprise Rewards no longer permit double refunds. Previously, problems with the refund logic permitted the inadvertent creation of a double refund.


*  Swatch images now resize as expected. Previously, even when a product attribute with Catalog Input Type for Store Owner was set to **Visual swatch**, the image size did not adjust as expected.


*  Customers with an empty **Date of Birth** field can now be saved even when the field is not marked (or checked on the JavaScript side) as mandatory. 

*  Store view home pages in multistore deployments no longer display breadcrumbs. Previously, the first store view in a multistore deployment looked fine, but the other store views included unnecessary breadcrumbs on the home page. 


*  You can now enable logs as expected (through the use of **Stores** > **Settings** > **Configuration** > **Advanced** > **Developer** > **Debug** > **Log to file**) when switching from production mode to developer mode.


*  `magnifier.js` now works no matter which mode is set. (`magnifier.js` offers the option of setting mode to 'inside' for an in-frame zoom.) 


*  The `timestamp` fields in `oauth_nonce` now include indexes to avoid deadlocks while erasing old records. 

*  The search bar now closes as expected when a user enters a search term in the mobile search bar, does not submit the search term, and then taps the search icon to close the search bar.


*  Magento now throws a descriptive error as expected when using a negative value that contains an invalid minus symbol to update reward points on a customer account.


*  The My Invitations page for a customer account now displays the correct reward points amount.


*  The `404 forbidden` error message has been corrected for accuracy to `404 not found` in `/app/code/Magento/Backend/Controller/Adminhtml/Noroute/Index.php`.


*  The Module Manager module grid list is now displayed correctly (**System** > **Tools** > **Web Setup Wizard**  >  **Module Manager**). 

*  Layered navigation now shows the correct product count. Previously, Magento counted only in-stock product.


*  DatePicker date format now reflects the  user's locale as expected.

*  Currency rates are now imported for Allowed Currencies as expected. Previously, selecting `Use system value` for `Base Currency` during currency set up resulted in a configuration error.


*  Problems with the double column layout on the home page have been resolved.


*  Merchants can now successfully delete the default welcome message.
*  The **Track Order** link on the order page in the Admin now works correctly. Previously, the URL that Magento generated for an order did not include the store that the order originated in.

*  Magento no longer rounds product quantity to the nearest whole number when trying to invoice an order that has products with quantity decimals.

*  `health_check.php` has been added into the `nginx.conf.sample` file.

*  The Google Analytics block code has been moved to the  <code><head></code> tag on the **Stores** > **Settings** > **Configuration** > **Sales** > **Google API** page.


*  Magento now displays a more helpful message when you misspell the name of a new module in `registration.php`.

*  The  `Learn More Link` widget option in a Recently Viewed Products widget now respects its setting. 

*  You can now use the WYSIWYG  editor to upload images even when the media directory is a symlink.


*  Dependency on  the `mageMenu` widget dependency in the breadcrumbs component has been removed.  Previously, breadcrumbs on the product page were invisible when the `mageMenu` widget was not used.


*  Magento no longer uses strings in evaluation of `setTimeout`.


*  Magento no longer displays the `Something Went Wrong` error whenever an administrator with limited privilege logs into the Admin and tries to navigate to a page.


*  The `magento setup:install` command no longer halts with an error  at `Magento_Catalog`.


*  Magento no longer throw the `Data key is missing: code-entity` error when you try to create and edit a page.


*  Customers are now redirected to the Sign In form as expected when they navigate to this form using the **Back** button on this browser.  


*  The welcome message now displays the new customer's first and last name after they have confirmed their account by clicking  the **Confirm Your Account** button in the confirmation email.


*  You can now enable debugging (log to file) in production mode.


*  Datepicker now uses the store locale as expected. 


*  When you click on a row with inline editing mode enabled while creating an Admin listing, the date column is now converted to the correct value in the date picker. Previously, the date value displayed in the date picker UI always showed the value of the current date instead of the actual column value. 

Gift cards
~~~~~~~~~~

*  Magento now includes a gift card recipient's email address in the gift card account history. Previously, Magento did not include the gift card recipient's name and email address in the gift card account history, even though Magento successfully sent the email.


*  Magento no longer permits users to save a new gift card  without first completing the required values. Previously, when creating a gift card, users could save the card without having designated an amount, but the card could not be purchased. Magento also created a `report.CRITICAL: Warning` error message in the `system.log`.


*  Magento now maintains relationships among new gift card accounts when a customer purchases several gift cards in the same order.


*  You can now save gift cards when the price has been changed on the Admin to an unacceptable format. Previously, Magento tried to save amounts in unacceptable formats (such as the inclusion of a comma in a four-digit price), which triggered an error.


*  Magento now displays the correct subtotal when a customer adds multiple gift cards of different amounts to his cart.


*  The password strength meter has been refactored to perform an email comparison only if an email field exists in the same form on which the meter exists. Previously, Magento threw a JavaScript error under these conditions.

Google Analytics
~~~~~~~~~~~~~~~~

*  The Google Analytics pageview is no longer triggered twice.


*  The `addToCart` event triggers on the Google Task Manager console only when an item is added to the cart.  Previously, the event was triggered before the cart was updated.


*  Magento now correctly displays product titles when displaying Sales information in Google Analytics.  Previously, Magento replaced spaces in product names with their HTML values (for example, `\u0020`).

HTML
~~~~

*  Magento now displays a newly created Contact Us form on a category page as expected. Previously, you could create a Contact Us form, but Magento  did not display it properly.

*  You can now change only the primary button `font-weight` without changing regular button `font-weight` with LESS variables.


*  HTML minification now works as expected.

*  The `name` attribute is no longer empty when you create custom fields during product creation.

Image
~~~~~

*  You can now set values for `MAX_IMAGE_WIDTH` and `MAX_IMAGE_HEIGHT` in **Stores** > **Settings** > **Configuration** > **Advanced** > **System** > **Images Configuration**, which supports the upload of larger images.


*  `.png` images from the GD2 image library that have transparent backgrounds now retain their  transparent backgrounds after upload. Previously, these transparent backgrounds were rendered black when you displayed these images after upload.


*  Magento now displays the background of transparent product image watermarks correctly.


*  Product image zoom now works as expected in stores running on Safari.  


*  The cross-sell product placeholder image on the shopping cart page is now the same size as the  product listing page placeholder image. 


*  The WYSIWYG editor now displays image icons as expected. Previously, the WYSIWYG editor showed broken image icons only.

Import/export
~~~~~~~~~~~~~

*  When you import information about existing customers, Magento now changes only the specific rows for this customer. If rows for other customer attributes (for example, `group_id`, `store_id`, `created_at`) are absent in the import file, these values are included unchanged.


*  You can now import or export a specific store view that includes custom options and bundle product options. Previously, the import/export feature did not include store view-level edits for  custom options.


*  Import now completes successfully when a product's CSV entry is split over two import "bunches".  Previously, Magento threw this error: `Cannot add or update a child row: a foreign key constraint fails`, and import failed.


*  You can now hide an image as expected by using the `hide_from_product_page` attribute during import.


*  Product import now updates the **Enable Qty Increments** field as expected. 

*  Magento now displays the correct execution time for an import operation on the **System** > **Import History** page.


*  The Admin product import feature can now import zero (0) values into the custom attribute field.


*  A grammar error in the "What is this" tooltip for the Braintree vault has been corrected.


*  The export process now correctly handles negative values in the exported XML file. 

*  Magento no longer throws an exception when importing  a product with a category field that begins with a comma. 

*  `CatalogImportExport categoryProcessor` now supports escaped delimiters in category names. 

*  The customer import process no longer crashes due to an out-of-memory problem during import of a customer database containing 250,000 or more entries.


*  Support for multiselect attributes for both product and customer entities has been added. 


*  Images imported by URL now have conventional file paths. 


*  Grouped products are now imported correctly. Previously, after import, simple products were no longer associated with their grouped products.  

*  Error reporting for product image import has been improved. 

*  You can now set `selection_can_change_qty` during the export or import of a bundle product with properties. *


*  Magento no longer throws an exception after successfully validating a .csv for import. Previously, an exception message was mistakenly passed as a exception description argument instead of exception message, which triggered the exception.

*  The product export process now correctly considers `hide_for_product_page` setting for images. 

*  Magento no longer displays a success message when it fails to successfully import all products.


*  Magento no longer displays extraneous records for an order into the exported CSV file. 


*  Product import now fetches the relationship between product SKU and `entity_id` with improved efficiency when inserting attribute data. 

*  Magento now renames images during a bulk upload of products  with images. 


*  Report error CSV file now works when you  try to import a CSV file with a semicolon delimiter.


*  Magento now provides a validation failure during import when multiselect columns contain duplicate values.

Indexing
~~~~~~~~

*  `indexer:status` now outputs information about the schedule `mview` backlog.

*  Magento no longer reindexes entities that have not been changed. Previously, Magento reindexed entries that were not changed but which had a MySQL UPDATE.

*  The customer grid indexer now works as expected.  Previously, this indexer did not work when reindexing using the command-line interface during the upgrade.


*  Tier pricing for a single product unit now works as expected. If a tier price is set for one product unit, and this price is lower than the product price or special price, then the product price index table is populated with the tier price.

Infrastructure
~~~~~~~~~~~~~~

*  This release provides compatibility with PHP 7.2.x.

*  You can now configure system logs to write to syslog, which supports subsequent re-streaming and minimizes storage needs.


*  You can now set access to only integrations for Admin roles (rather than assign full access). Previously, access for integrations could be assigned only when  **Role Resources** was set to all.


*  `expectException()` calls now accept two parameters (instead of one).


*  Several components included by Composer have been updated to the latest patch versions.


*  Customers can change product status by clicking on the toggle element or by clicking on label text, but not by clicking the area around a toggle element. Previously, if a customer  clicked on the area around a toggle element, Magento changed the state of the element. Unintended results could occur if a customer mistakenly clicked on the area around the element and didn't realize that the status had  changed.


*  We've removed `Zend_Json` from the data object, test suite, and package information.


*  Changing the `@tab-content__border` variable in Blank theme now works as expected. 


*  Corrected sticky footer in `page-main` container height on mobile devices. 

*  Style groups for mobile devices (`max-width`) are now specified in the correct order.


*  The Web Setup wizard icon sidebar shortcut on the Admin now links as expected to the wizard.


*  The condition category chooser now handles multiple nested categories as expected. Previously,  if a cart rule contained several nested categories, no categories appeared on the page, the page  became unresponsive,  and  Magento eventually crashed.


*  The `magento/module-widget/etc/widget.xsd` and `magento/module-widget/etc/widget_file.xsd` files have been updated to support multiple `depends` parameters.


*  Magento now requires that customers select State/Province when shipping orders to India,  and the checkout page now provides a drop-down field with appropriate values.


*  We fixed the invalid parameter configuration that was provided for the `$block` argument of `Magento\\Ui\\Component\\HtmlContent`.

*  The`app/code/Magento/Downloadable/Helper/File.php` and `app/code/Magento/Bundle/Block/Adminhtml/Catalog/Product/Edit/Tab/Attributes/Extend.php` files no longer contain duplicate key arrays.


*  Magento now deselects only the attributes you choose to deselect when you set the **Use Default Value** setting on a store view to **no** for certain attributes. Previously, when you deselected the **Use Default Value** setting on a store view for certain attributes, Magento unselected other attributes as well.


*  Additional blocks for footer links now line up with default footer links as expected. 


*  The Psr logger debug method now works by the default in developer mode. 

*  Proxy/Interceptor generator now works as expected with  PHP 7.1 syntax.


*  Module composer versions are no longer mandatory in the GitHub repository.


*  The handling fee configuration for shipping methods is now silently casted to float.


*  The  `create_function()` function has been deprecate and removed. 


*  Magento now sets the `trigger_recollect` attribute  back to 0 after collecting total amounts for the quote. Previously, Magento timed out if a customer tried to reload a quote.


*  You can now add new columns to the item table  in the `admin sales_order_view` layout. 

*  The Admin shipping report now shows the correct currency code.


*  `Configurable::getUsedProducts` returns a simple array as expected after product collections are cached


*  The  input format of customer date of birth has been corrected. [GitHub-11332](https://github.com/magento/magento2/issues/11332)


*  The **Add to cart** checkboxes in Related Products are no longer visible when `$canItemsAddToCart` is set to **false**.

*  A  responsive design issue with the mobile landing page has been resolved. Previously, the Shop By and other page elements were positioned incorrectly.


*  We've fixed an issue with `addCrumb()`. 

*  The `getChildren()` method now returns a list of IDs that is sorted by the `position` attribute. 


*  Magento now allows the  setting of a custom  HTTP response status code in a redirection.


*  `Magento\Search\Helper\getSuggestUrl()` is now used as expected in the search template, which supports a custom autosuggest feature. 

*  XHTML templates now use schema URNs.


*  `SymLinksIfOwnerMatch` has replaced `FollowSymLinks` in htaccess templates. [GitHub-10811](https://github.com/magento/magento2/issues/10811)

*  Magento no longer throws an error when using `Magento\Quote\Model\ResourceModel\QuoteItem\Collection::getItems()`  to load a quote item collection.

*  Merchants can now apply styling by changing LESS variables in the Luma theme as expected. 

*  `sjparkinson/static-review` has been removed throughout the code base.

*  The `@deprecated` tag has been added to `Magento\Store\Model\Store::$_isAdminSecure`. 

*  A new static test detects blocks without the `name` attribute.

*  You can now use the command-line interface to create a new administrator. Previously, Magento did not recognize configured tableprefix, which prevented Magento from creating the new user. 


*  The `getToolbarBlock()` method  has been refactored to permit removal of `product_list_toolbar`.


*  When you use a UI component-based form and add a custom regular expression pattern validation to an input field, Magento now properly converts the supplied pattern from a string to a JavaScript RegEx object.


*  The `hasDataChanges` function now returns false as expected when no data has been changed. 

Klarna Payments
~~~~~~~~~~~~~~~

*  The **Purchase** button is now disabled as expected if Klarna authorization is declined.

*  The unnecessary `span` element below the onboarding text has been removed.

Locale
~~~~~~

*  The DatePicker date filter on **Reports** > **Products** > **Ordered** now works as expected for administrators working in Australian English locales.


*  The zip code pattern for Japan now permits only the seven-digit codes that the Japanese postal service accepts. 

*  Magento now correctly validates birth dates in stores running French locales.

Messages
~~~~~~~~

*  The  Payment & Shipping Method area  of an order now displays an informative message if the payment method previously selected is no longer available.


*  Magento now displays an error message as expected when a user submits a registration form without first completing the required date of birth field.

*  The error message that Magento displays when a customer submits a product review without selecting a rating can now be translated.


*  The message that Magento displays under the following circumstances has been improved:

   *  You download a database from a staging environment that has code deployed to it that upgrades the schema version, or

   *  You are on the master branch in your local environment, which is behind the database. 


*  The exception message in `findAccessorMethodName()` of `Magento\Framework\Reflection\NameFinder` has been improved.

Newsletter
~~~~~~~~~~

*  Magento now sends confirmation-of-subscription email to new subscribers only.

*  Guest users can now sign up for newsletters for multiple stores. Previously, when a guest user signed up for a newsletter from multiple stores, Magento sent a subscription confirmation message, but did not successfully subscribe the user.


*  A customer subscription on one store no longer depends on  the customer's subscription on another store.

*  Magento now sends the newsletter subscription success email as expected when a customer successfully subscribes to a newsletter.


*  Magento now sends a confirmation request email to the customer when she unsubscribes to a newsletter.


*  Magento now displays the newsletter subscription confirmation message  as expected after a customer clicks the confirmation link in the subscription confirmation email.


*  Magento now uses an index to retrieve subscribers from the database instead of the slower `Using where` query. 


*  Magento no longer sends redundant newsletter subscription confirmation emails to a customer who creates an account after first logging in as a guest user.


*  The title of the newsletter **Subscribe** button now wraps correctly.


*  Newsletter subscriptions status is now specific to each store in a multistore deployment.  Previously, when a customer uses the same email address for each account on different stores, changes to the newsletter subscription for an account on one store affected the accounts on other stores.

*  Syncing of newsletter subscribers now works correctly. Previously, the newsletter `create-date` and `change_status_at` values did not work as expected.

Orders
~~~~~~

*  Magento no longer copies every address that has `save_in_address_book` set to 0 to the customer address book. Previously, if you placed an order as a guest and set the `save_in_address_book` value for an address to 0, Magento still copied that address to the customer address book when it registered a new customer on the checkout success page.


*  Magento now displays new orders at the top of the orders list as expected when sorting order by purchase date.


*  The `getTracksCollection()` method  now returns collection objects. Previously, this method returned either collections or arrays.

*  When you place an order in the Admin, Magento now displays the form needed to enter information for  enabled payment methods.


*  The Shipment API now adds a customer note to a shipment if the shipment was created through the API and `appendComment` is set to **true**.

*  Magento now displays the State/Province information  on **Order View** > **Information** > **Address Information**.


*  Magento now correctly calculates the value of the `base_shipping_discount_tax_compensation_amnt` field.


*  The Products Ordered report now shows simple (child) products of configurable products.

*  The Products in Cart report no longer tries to retrieve the data of deleted products. Previously, when Magento tried to generate this report, it threw an exception.

*  Magento no longer throws a fatal error when you search for a customer from  **Reports** > Reviews > **By Customers**.


*  The cancel order and restore quote methods now accurately calculate the amount of stock to be returned to inventory when an order is canceled. Previously, when you canceled an order, some of these methods did not accurately calculate the amount of restored stock.


*  Invoices and orders now show  consistent coupon codes and totals. Previously, invoices did not reflect coupon codes as expected. 

*  Coupon codes now work as expected for orders created from the Admin for guest customers.

*  Magento now sends order confirmation email as expected for orders made using PayPal. Previously, when a customer paid using a credit card, Magento sent email confirmation, but not when an order was paid for by PayPal.

*  Magento now uses the  store values (prefix, suffix, increment ID, and sequence tables) from the correct store view when placing orders from a non-default store in a multistore deployment.

*  Magento no longer throws error on the Admin order edit page when the order address has extension attributes.


*  When you place an order as a guest and set the `save_in_address_book` value to 0, Magento no longer copies that address to the customer address book if you subsequently register as a new customer on the checkout success page.


*  The `cancel` method no longer saves an order and returns **true**  if an order canceled with OrderService  cannot be canceled. 

*  You can now access the create order page from the customer edit page as expected. Previously, Magento threw a fatal error. 

*  New orders are now being saved as expected to the order grid.

*  Magento now correctly applies the designated frontend controller when store view URLs contain store codes (**Stores** > **Settings** > **Configuration** > **General**  > **Web** > **Add Store Code to Urls** is set to **yes**).

*  Magento now checks if an invoice has been previously  canceled before canceling it.

Page cache
~~~~~~~~~~

*  Asynchronous rendering of blocks no longer corrupts layout cache. Previously, when an asynchronous request generated a layout `cacheId` based on same handle as a CMS page, but without loading the associated CMS page, the CMS page-related layout updates were lost.

Payment methods
~~~~~~~~~~~~~~~

*  Merchants can now provide customized error messages when a transaction fails at the payment stage. Previously, Magento displayed this default message when an error occurred: `Transaction has been declined. Please try again later.`

*  Magento no longer throws a validation error at the payments step of check out when an agreements checkbox is present.


*  Magento now displays the correct billing address in the order confirmation email when  **Paypal Express Checkout** is enabled. Previously, Magento displayed the shipping address instead of the billing address.


*  Customers can now check out using PayPal when the **Request Billing Information** feature is not enabled. Previously, Magento threw this error when a customer tried to check out with Braintree through Paypal from the shopping cart,  `Undefined index: billingAddress in /app/aacdg4mgbgw24/vendor/magento/module-braintree/Model/PayPal/Helper/QuoteUpdater.php on line 138`.

*  Magento now provides dedicated payment and shipping debug log files to store information specific to those functional areas.


*  PayPal now works as expected with virtual products such as gift cards. Previously, when you tried to place an order for a virtual product using PayPal, Magento did not display the PayPal popup when you clicked **Continue PayPal** during checkout.


*  You can now place orders using PayPal when **Payment Action = Order**. Previously, when **Payment Action = Order**, Magento displayed this error when you reached the order review page: `We can't place the order.`


*  The multi-shipping checkout  flow now supports the CyberSource payment method. This payment method is supported by {{site.data.var.ee}} only. However,  as part of the process of adding CyberSource support, we've made improvements to the Multi-shipping module to simplify integration process for other payment methods. Users of the CyberSource payment method should note that CyberSource uses the Magento Vault module only to store and retrieve tokens. Stored CyberSource tokens won't be displayed on the checkout page or customer account.


*  Default AVS and CVV codes are now mapped as (null or empty string) instead of `U` for Signifyd.


*  The **Billing Address** field now displays the designated billing address as expected  for a registered customer  when checking out with Paypal Express Checkout. Previously, Magento displayed the shipping address in the **Billing Address** field in both the order confirmation email and the Admin.


*  Admin users that are not part of the Administrator group can now complete payment for an order using Braintree.


*  Magento PayPal integration now supports the Indian Rupee currency (INR).


*  Magento now validates that the required **Purchase Order Number** field is  set as expected during checkout. 


*  A type error in the payment void method of the Authorizenet module has been fixed.


*  Magento no longer throws an error when you try to add a new shipping address to an order paid with using Braintree from the Admin.


*  Magento now creates invoices as expected for orders created using Braintree PayPal. Previously, Magento threw an error when a merchant tried to create an invoice for an order from **Admin** > **Sales** > **Order**.


*  Magento no longer disables the **Place Order** button  after an attempt to validate a payment made with PayPal fails. 


*  Magento no longer throws an  error when you try to open an order page from the Admin or when setting the  transaction ID in a payment module. Previously, Magento threw this error: `Notice: Undefined index: value in /app/code/Magento/Backend/Block/Widget/Grid/Column/Filter/Select.php on line 72`. 


*  Merchants can now create an invoice for an order placed  with PayPal.


*  The incorrect `@return` tag (PHPDocs)  in the `placeCheckoutOrder` method has been corrected.


*  The `getPaymentMethodList` method no longer sets the value of a group to null  in `$labelValues` if it already contains group-related values. Previously, the `Magento\Payment\Model\Config\Source\Allmethods` config source model did not display every available payment method.

Performance
~~~~~~~~~~~

*  The price indexer is now scoped and multithreaded, which improves layered navigation, search, and indexing actions for complex sites with multiple websites and many price books.


*  You can change store locale without the exporting and importing configuration data. While Magento is in production mode and the `SCD_ON_DEMAND` is enabled, the Magento store and admin locale options are available.


*  The catalog rule re-indexing operation has been optimized, and average re-indexing time (which depends on rule conditions) has improved by more than  80%.  Previously, a full catalog rule re-index operation on a medium B2C store took more than 20 minutes.

Pricing
~~~~~~~

*  Magento now uses the current date as expected when setting the start date for a special price. Previously, Magento set the start date for a special price a few years in the future, which prevented the special price for being active.


*  Tiered pricing and quantity increments now work as expected with decimal-based inventories.


*  You can now add a bundle product that includes a simple product with a price of 0 (zero) to your cart. Previously, Magento threw an error. 

*  Magento now displays the correct  price on the product page for storefronts running Japanese locales.


*  Issues with configurable products with custom options and tier prices  have been resolved. Previously, the product page did not display the correct product price, but the shopping cart did.

Product video
~~~~~~~~~~~~~

*  Magento now populates the YouTube video URL and Title fields with the same values as are populated on the default store view on multisite deployments. (These fields are global scope attributes and should be the same on all storefronts.) Previously, Magento left these fields blank in multisite deployments.

*  The product video embedding feature is now GDPR-complaint and allows the domain `youtube-nocookie.com`. Previously, when you tried to embed this URL, Magento threw an error.

Quote
~~~~~

*  You can now implement a product attribute that sets **Catalog Input Type for Store Owner** equal to  **Fixed Product Tax** in a multi-store environment.

*  Magento now successfully saves the value of `REMOTE_IP` when a customer uses an IPV6 (Internet Protocol version 6) address. Previously, this value was only partially saved in the `sales_order` and `quote` tables.


*  A type error in `CartTotalRepository` has been resolved. Previously, `CartTotalRepository` could not handle extension attributes in quote addresses, and Magento threw a `PHP Fatal error:  Uncaught TypeError`.


*  Magento now displays the correct product price for an order created from the Admin in multisite deployments. Previously, when an order was created from the Admin in a multisite deployment where products were assigned different prices per store view, Magento defaulted to the product price of the primary storeview if the order were edited or updated.


*  An integrity constraint violation error no longer occurs after you reorder a product with custom options. 

Reports
~~~~~~~

*  You can now successfully export the Ordered Products report to a CSV file. Previously, the export file contained no report data.


*  The scope selector for reports now works as expected. Previously, when a merchant set the scope to **All Websites**, the generated report showed  sales from only a subset of websites.


*  The `.csv` export of Coupon reports now shows the correct total for selected coupons. Previously, the total line in the `.csv` file showed the totals for all coupons in the selected time period, rather than just the selected coupons.


*  Wishlist reports are available on the Admin as expected.

*  The Low Stock report now accurately lists all out-of-stock products. Previously, this report was not accurate when the All Websites view was selected.


*  The Admin's Most Viewed Products tab now displays all the products in all  attribute sets, not simply the default attribute set.

*  The timezone has been removed from the date when Magento retrieves the current month from a UTC timestamp.


*  The **Year-to-date** dropdown accessed from **Stores** > **Settings** > **Configuration** > **General** > **Reports** > **Dashboard** now displays a numerical list that ranges from 01 to 12 as expected.


*  A valid  XML layout update handle is now preinstalled in the home page. 

Review
~~~~~~

*  Magento now displays a `404 page not found` error when a customer tries to navigate to a product review that is not accessible. Previously, Magento displayed a PHP error code.

*  Magento no longer throws an error when a merchant edits a product from the Admin when reviews are disabled. 

*  When a customer creates a product review, the link to the product from the review in the customer's **My Account** > **My Product Review** is now SEO-friendly.

*  The **Save and Next** and **Save and Previous**  buttons on **Marketing** > **Reviews**  now work as expected.


*  Magento now checks if a product is assigned to a current website before displaying the write a review page.

Rule
~~~~

*  Cart Price rules now correctly display  nesting levels for categories with nesting levels that exceed three levels.

Sales
~~~~~

*  Magento has added verification for previously set filters in `Magento/Ui/Component/Filters`, which has eliminated duplication of filters in the collection `where` conditions.


*  Magento now shows all products as expected in the Recently Ordered list when a customer places an order that contains products from multiple stores. Previously, in installations with two storefronts, if a customer added products from both stores to the same shopping cart, and placed a single order, the recently ordered product list would not show all ordered products.


*  The grand total for a credit memo now matches the invoiced total when a discount is applied to shipping charges.


*  The Items Ordered list now updates as expected when the user clicks **OK** when changing the options of a configurable product during creation of an order from the Admin. Previously, the update did not occur until the user clicked **Update Items and Quantities**.


*  Admin orders are no longer restricted by a minimum order amount. Previously, Magento required this minimum for both Admin and storefront users.


*  Orders exported to a CSV file now display dates in a consistent format.


*  Magento now displays text on the New Cart Rules page correctly. Previously, labels listed in the Store View Specific Labels section of this page was sometimes truncated or duplicated.

*  Magento now removes unnecessary PDF files after generation. Previously, Magento saved a copy of every generated invoice PDF in `/var`.

*  Magento no longer throws an error when a merchant sends an invoice for an order that contains grouped products. Previously, Magento invoiced the order but threw an error, and did not send the email.


*  Sales PDFs now support unicode fonts (GNU Free Font), which broadens language support in these PDFs.


*  Magento now creates  invoice numbers using the correct store view ID in a multistore environment. Previously, Magento always used the default store ID for all invoices created in a multistory environment.


*  Disabling invoice emails no longer degrades product performance.


*  The invoice grid now shows the correct subtotal for a partial invoice. Previously, it showed the entire order's subtotal.

*  Magento now handles decimals properly in order quantities.

*  You can now filter orders by customer email. Previously, Magento threw an error when you tried to filter orders by customer email from **Sales** > **Orders**.


*  The wrong entity_model for `invoice` has been corrected in the `eav_entity_type` table. 


*  An incorrect return type in PHPdoc has been corrected. Previously, this return type resulted in multiple warnings in IDEs.

*  Magento now syncs an order's shipping and billing addresses as expected when a customer edits the billing address.

*  The transport variable can now be altered in the  `email_invoice_set_template_vars_before` event. 

SalesRule
~~~~~~~~~

*  Cart price rules with associated coupons are no longer affected by edits to scheduled updates.

*  You can now use wildcard values in coupon codes.


*  We've fixed an error in discount calculations that prevented merchants from creating a rule that set a tax rate and 100% discount. Previously, when a tax rule was applied, and a  100% discount was also applied during check out, the shopping cart displayed a negative grand total.

Sample data
~~~~~~~~~~~

*  The `sampledata:deploy` and `remove` commands now have `no-update` options.

Search
~~~~~~

*  The **Catalog** > **Products** page now contains a keyword search.

*  Magento no longer throws an asymmetric transaction error when you reindex in Magento deployments running Elasticsearch.

*  You can now submit search criteria by clicking enter when initiating a product search from the Admin.


*  Elasticsearch is now the default search engine in Magento. MySQL search has been deprecated.


*  Elasticsearch now works as expected in Chinese locales.


*  Elasticsearch no longer includes out-of-stock product options in search results.


*  Support for Elasticsearch 5.x has been added.


*  Magento no longer throws an error when a customer uses quick search to search on a term that does not exist in the search database. Previously, Magento returned this error: `TypeError: this._getFirstVisibleElement(...).addClass is not a function`.


*  Magento no longer throws an error when you submit the search form in the header with an empty value.

*  Elasticsearch now correctly calculates the relevance of quick search results according to selected attribute search weights.

*  Out-of-stock options for configurable products no longer show up in search and layered navigation results.

*  You can now use an asterix when searching on customer names. Previously, if you used an asterix in a search query, Magento displayed this message: `Something went wrong with processing the default view and we have restored the filter to its original state.`


*  Search synonyms are now available for all search engines deployed in your Magento store. Previously, search synonyms did not appear in the Admin menu when Elasticsearch 5.0+ was deployed.


*  You can now limit the number of results in the search autocomplete. 


*  The mini search field no longer loses focus after JavaScript is initialized. Previously, after mini search component's JavaScript loaded and initialized, search input lost focus.


*  CatalogSearch has been deprecated and replace with Elasticsearch.


*  Sort by Product Name on the category page now works with all available filters.


*  An unnecessary `saveHandler` in the  CatalogSearch indexer declaration has been removed.


*  Search synonyms in a group now can declare several words as synonyms. For example, "Elon Musk,tesla" is a valid synonym group, and a search on the phrase "Elon Musk" will also show results for the "tesla" keyword. Previously, you could declare synonyms for each word (for example, "Elon,Musk,Tesla"), but these words didn't work as a phrase. Synonyms are also now case-insensitive.


*  Searching for a value of an attribute set on the store-view level of a product now returns results. Previously, Magento returned results  only if the attribute value was entered on the all store-view levels.


*  Search terms from the same synonym group now return the same results.


*  You can now use the **Enter** key to submit a search form. 

*  Search on MySQL-based entities has been improved. (This improvement does not provide a fulltext search, but simply the best way to search when a `SearchCriteria` with `fulltext` condition is provided over a MySQL table.)


*  Magento now displays validation messages as needed on advanced searches. Previously, Magento did not display a message even after a customer submitted the advanced search form with no entries. 

Shipping
~~~~~~~~

*  The free shipping cart price rule now works as expected when **UPS shipping method** is enabled and **Free Shipping** is set to "For matching items only".


*  The Magento UPS module has been updated to support new UPS API endpoints.


*  You can now use `GET .V1/shipments` to search for shipments that contain a shipping label. Previously, using this call  caused Magento to throw an exception.

*  Magento now successfully creates shipping labels for a return merchandise authorization (RMA) when using FedEx Smart Post as the shipping option. Previously, Magento threw an error under these circumstances.


*  Multishipping checkout now works as expected. Previously, Magento displayed the `Shipping address is not set` error message  when checking out an order with multiple addresses.


*  Merchants can now ship the remaining items in an order in which some items require a credit memo.


*  Customers can now view their completed order from the success page for orders that will be shipped to multiple addresses. Previously, when a customer took a link from the order success page to view their just-completed order, Magento displayed this error: **There has been an error processing your request**.


*  The Shipment grid now displays the status of completed orders correctly. Previously, the Order Status column of the Shipment grid indicated that a completed was being processed.


*  The checkout page now  displays address fields when the number of address lines has been left at the default. Previously, when the default value was configured, Magento did not display any ship-to address fields.

*  Shipping method radio buttons no longer have duplicate element IDs on the cart page, making it possible for customers to select a second shipping method. 

Sitemap
~~~~~~~

*  Magento now correctly processes global product attributes when generating the sitemap.


*  The sitemap no longer contains `/home` in the URL generated for your store domain.


*  When an error is created during sitemap generation, Magento now sends an informative email to administrators. Previously, Magento threw a fatal error.


*  The lastmod value in the `sitemap.xml` file for a category now contains the `created_at` timestamp. Previously, this timestamp contained invalid dates.


*  It's now easier to add additional items to a sitemap. Previously, `SitemapPlugin` worked inconsistently with large sitemaps. 


*  Sitemap no longer crashes if the scope of the name attribute is set to global. 


*  Sitemap no longer crashes if the scope of the name attribute is set to global.


*  Images in XML sitemap are no longer always linked to the primary store in a multistore deployment.

*  Magento now generates correct product URLS when you generate a sitemap of categories and products with **Use Categories Path for Product URLs** set to **no** ( **Configuration** > **Catalog** > **Search Engine Optimization**).

Staging
~~~~~~~

*  Magento now rolls  back updated changes to their pre-update state  when a merchant deletes an active scheduled update. Previously, some products were removed from their assigned categories (and categories were removed from the Admin) when an active product update was deleted.

*  You can now successfully re-order a configurable product. Previously, a schedule update for one configurable product affected other ordered configurable products.

*  Magento no longer deletes products from the Admin product list after a merchant deletes its active schedule update. This deletion  appeared only after the scheduled update time.

Store
~~~~~

*  Returns from REST endpoint  `/V1/store/storeViews` calls now include  `is_active` values for stores. 


*  The `getUrlInStore()` method no longer returns URLs that contain the store code, which has shortened the extremely long URLs it previously returned.

*  You can now use an `admin_system_config_changed_section` event to subscribe to changes for all sections in **Stores** > **Settings** > **Configuration**. 

*  TinyMCE now loads successfully due to a refactoring of the use of  `minify_exclude` configuration.

Swagger
~~~~~~~

*  Swagger now correctly renders POST/PUT operations. Previously, in Swagger, the text area that contained the payload structure of some POST and PUT operations was not displayed.

*  Swagger now works as expected when JavaScript minification is enabled. Previously, when JavaScript minification was enabled, the swagger-ui-bundle.js became corrupted, although Swagger worked fine when minification was subsequently disabled, and the files were redeployed.

*  Swagger now handles `searchCriteria`-related requests as expected. 

*  Swagger now works as expected when JavaScript minification and merging are enabled.

Swatches
~~~~~~~~

*  Visual swatches now display  swatch color in the Admin as expected.

*  The dropdown menu that Magento displays when a user clicks on the **Add Swatch** button on the Manage Swatch tab now displays all possible options. 

*  Color attribute swatches are now visible when sorting is enabled.


*  You can now use REST to import visual swatch attribute options. Previously, you could not add swatch options using service contracts unless a swatch option already existed for the attribute.


*  The load and merge order of `view.xml` configuration in `\Magento\Swatches\Helper\Media` now matches `\Magento\Catalog\Helper\Image.` 


*  We've replaced `.size()` with `.length` to be compatible with jQuery 3. 

*  Swatch functionality that has been extended using JavaScript mixins now works as expected in Safari and Microsoft Edge. 

*  You can now save a swatch attribute that has an empty option.


*  You can now change attribute type from `swatch` to `dropdown`.

Tax
~~~

*  Tax total amount is now equal to the sum of the tax details amounts. Previously, Magento displayed the wrong order tax amounts when using specific tax configurations.

*  `\Magento\Framework\Data\OptionSourceInterface::getAllOptions()` and `\Magento\Framework\Data\OptionSourceInterface::toOptionArray()` are now compatible with parent classes. 

*  Double tags have been removed from the `config.xml` of the `Magento_Tax` module.


*  Magento no longer performs redundant tax calculations  for every price on category page, which has improved product performance. 

*  Magento now uses  the correct table rate shipment when creating a merchant creates an order through the Admin. Previously, when a merchant  created an order through the Admin and selected the shipping method table rate, Magento took the shipping rate table from the wrong website ID.

Testing
~~~~~~~

*  Integrations tests no longer throw `Cannot instantiate interface Magento\Framework\Interception\ObjectManager\ConfigInterface` errors. 

*  Integration tests now reset the integration test database as expected.  

*  A typo in `dev/tests/functional/tests/app/Magento/Paypal/Test/TestCase/OnePageCheckoutTest.xml` has been fixed.


*  Static tests now check for the deprecated `each()` function. 


*  The `functional.suite.dist.yml` has been updated to handle custom backend names. (This value was previously hard-coded.) 


*  THe `validate_image_info_rollback.php` test suite has been updated. 

*  `phpunit.xml` is now blacklisted during schema validation static tests, particularly `Magento/Test/Integrity/Xml/SchemaTest.php`.


*  The `\Magento\Test\Php\LiveCodeTest::testCodeStyle`  method now uses whitelist files.


*  Integration test coverage for the new extension point for New Shipment Controller has been added. 


*  `sjparkinson/static-review` and other obsolete tools  (including `dev/tools/Magento/Tools/Layout`, `dev/tools/Magento/Tools/StaticReview/pre-commit`, and `dev/tools/Magento/Tools/psr/phpcs_precommit_hook.sh`) have been removed from the test code base.


*  Integration tests for product URL rewrite generation have been added. 


*  The `ProcessCronQueueObserverTest.php` integration test now works correctly. 

*  `setCateroryIds([])` has been corrected to `setCategoryIds([])` throughout the test suites.  


*  CreateOrderBackendTest has been refactored to support the  **Reorder** button when Inventory Management is enabled. 

*  Unit tests have been refactored to no longer check for deleted file `app/code/Magento/Catalog/Model/ResourceModel/Product/Indexer/Eav/AbstractEav.php`. 


*  `CreateCreditMemoEntityTest` has been refactored to support the Inventory Management reservation mechanism.  


*  `CreateOrderBackendPartOneTest` has been refactored to support the Inventory Management reservation mechanism.

Theme
~~~~~

*  Customers can now successfully close full-screen zoomed product images displayed on an iPhone 4s, 5s, 6, or 6s with the Safari browser. Previously, if a customer chose full-screen zoom for any product image, he could not close the full-screen zoom.


*  The forced setting of `cache_lifetime` to `false`  has been changed to a default `cache_lifetime` value of 3600 for `Magento\Theme\Block\Html\Footer`.


*  The default storefront welcome message now works as expected when the **Translate Inline**  (**Stores > Settings > Configuration > Advanced > Developer >**) setting is enabled. 

*  We've improved the display of the Payment Methods section of the checkout page on mobile devices. Previously, the layout of page elements was not correctly spaced.

Translation and locales
~~~~~~~~~~~~~~~~~~~~~~~

*  The `<![CDATA[]]>` statement in `system.xml` now works as expected.

*  The JavaScript translation for validation messages now works for customer account pages.


*  Messages on password strength are now translatable. 

*  The JavaScript translation regex no longer leads to unexpected results and untranslatable strings. 


*  All messages in Customer Account Create are now translatable. Previously, warning messages about password validation appeared in locale language only. 

*  We've added  client-side caching of `js-translation.js`.


*  The datepicker date filter on **Reports** > **Products** > **Ordered** now works as expected for administrators working in Australian English locales.


*  Magento now supports Malaysian locales.

*  The string for `moreButtonText` in `app/code/Magento/Swatches/view/frontend/web/js/swatch-renderer.js` can now be translated.

*  Magento now displays the correct  price on the product page for storefronts running Japanese locales.


*  The module responsible for generating the `js-translations.json` file now contains a routine that translates strings in tags.

*  Magento now displays the correct payment method title on the payments page during checkout in multistore deployments where storeviews implement different locales.

*  The hint provided for the global configuration field on the Admin configuration page has been corrected.


*  `region_id` is no longer overridden when a customer edits their billing address from a country that requires a value for state to a country where one is not required.

UI
~~

*  Magento no longer sends duplicate delete requests as a result of an unstable Internet connection. Previously, unintentional mass deletion of products sometimes occurred as a result of an unstable Internet connection.

*  As you type additional characters into the text field for a product's custom option, the hint showing the number of characters left before reaching the maximum now decreases as expected.

*  Previously missing translation strings have been added to the UI module. 

*  Administrators who lack access to the CatalogRule module can now perform operations as expected in the Admin cart price rule edit page.

*  The UI component configuration XSD file (`ui-configuration.xsd`) now constrains settings so that `abstractSettings`, such as `<label>`, can only be placed and read from the top-level `<settings>` nodes, while component-specific settings, such as `<options>`, can only be placed and read from the appropriate `<settings>` descendent of `<formElements>`.


*  Users can now press the **Esc** button on  the delete-from-cart confirmation pop-up window  without generating a `jQuery` UI error. Previously, when a customer added a product to the shopping cart, then pressed the trash icon to delete it, Magento displayed this confirmation pop-up window, but threw an error when the customer pressed the window's **Esc** button.


*  The `font-size` variable has been updated and standardized.

*  We've added the `@navigation-level0-item__hover__color` missing variable for mobile and tablet view.


*  Footers now behave as expected when displaying Magento on a mobile device.


*  The unused totalbar block has been removed from the invoice create and credit memo create layouts.

*  The JavaScript validation rule used to validate AM/PM time settings now works as expected when JavaScript is minified.


*  The message list component message type now has a message type of success. Previously, this type was always `error` when the `parameters` property was specified. 

*  Magento now displays the wishlist icon on the shopping cart page on mobile devices. Previously, Magento cut off the wishlist icon on this page when viewed on a mobile device.


*  JavaScript validation rules no longer require validation of fields where completion is not required. Previously, customers could not complete forms unless non-required fields were completed.

*  When a user scrolls a page, the datepicker now retains its position relative to other page elements as expected.


*  The confirmation modal buttons that Magento displays when a customer sends a product to the trash are now translated as expected.


*  The dropdown menu is now positioned as expected under the link on the UI Component listing.


*  Magento no longer displays the current date for a product when the `date` attribute is empty. 


*  Magento no longer throws a JavaScript error when a user enters a special character (for example, `/` or `&`) while adding the `stripped-min-length` validation to a UI component. 

*  Magento no longer throws an `Uncaught Error: Script error for: trackingCode` error on storefront pages.


*  `range-word` validation for form fields now works as expected. 

URL rewrites
~~~~~~~~~~~~

*  Magento now sets the value of `Store_Code` from the current store when this information is included in a URL.

*  Magento now loads `urlrewrite` router before the Magento base router. Previously, the Magento custom URL rewrite functionality did not work when you added an additional redirection (for example, a custom redirection from `/customer/account/create` to another page). 

*  Switching store views now works as expected. Previously, under some conditions, users were redirected to a 404 page.

*  You can now reset a form by clicking **Reset** in **Marketing** > **SEO & Search** > **URL Rewrites**.

*  Categories of the Main menu in the different store view are now updated when Varnish is enabled.


*  Magento no longer throws a 404 error when a customer navigates from the Catalog page of the default store to a custom Catalog page on a different store.


*  The **Reset** button no longer causes a JavaScript error on the URL rewrite creation page.


*  The Magento URL rewrite functionality now supports the use of special characters in category names. Previously, the category tree did not load if a category name contained a special character.

Visual Merchandiser
~~~~~~~~~~~~~~~~~~~

*  Visual Merchandiser now includes website scope when displaying the correct prices and availability of configurable products.


*  We've improved the performance of editing or saving products in large categories (more than 18,000 products per category).

Web API
~~~~~~~

*  When you use REST to update an existing product, Magento assigns the update only to the websites that they were assigned to before the update. Previously, updating a product using the REST API (`PUT /rest/all/V1/products/example_sku`) assigned the product update to all websites automatically. 


*  When you create a credit memo comment with `POST /V1/creditmemo/:id/comments`, Magento now sends  credit memo update emails as expected. Previously,  Magento did not send this email, and no other transaction emails were sent to the customer.


*  Magento no longer creates duplicate shipments for orders created via API. Previously, Magento created duplicate shipments when a merchant created a shipment via the API under certain conditions (mainly with bundled products).


*  Product searches using `GET V1/products` return `extension_attributes` for configurable products as expected.


*  You can now include custom attributes when filtering the responses of REST calls.


*  Magento now returns a 404 error and includes a descriptive error message when a  REST search is performed on a non-existent cart.


*  Magento now includes the filter groups and the sort order of the `$searchCriteria` parameter in the `searchCriteria` object that is provided for the EAV set repository.


*  Updating a product with the REST API (`PUT /rest/all/V1/products/example_sku`) no longer assigns the product to all websites automatically. (Automatic assignment to all websites now occurs only when you create the product in All Store Views scope.) 


*  A generated Admin API token no longer expires immediately. Previously, when you created a token for an Admin user and have set **Admin Token Lifetime (hours))**  to empty, Magento denied access  because the token immediately expired. 

*  Magento now checks for the uniqueness of attribute option values for attributes created via REST. 


*  `salesRefundInvoiceV1` now saves the invoice ID as expected for a credit memo. 

Wishlist
~~~~~~~~

*  Magento now displays an error message if you try to add products to a wishlist without first logging in. 


*  Magento now stores product IDs and SKUs to locally stored customer data for wishlists.

*  `SearchCriteriaBuilder` now has a check to determine if sort order should be applied. Previously, `SearchCriteriaBuilder` built the wrong criteria (`ORDER BY part`). 

*  Registered users can now create new wishlists as expected when multiple wishlists are enabled. Previously, Magento displayed an error.


*  Magento no longer changes the grid view to list view on the product list page when a customer adds a product from the wishlist section to the cart, and now displays the appropriate success message.
