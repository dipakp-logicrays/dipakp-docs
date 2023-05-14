Magento Open Source 2.3.2 Release Notes
=======================================

**Official link**: https://devdocs.magento.com/guides/v2.3/release-notes/ReleaseNotes2.3.2OpenSource.html

Release notes published on June 25, 2019 and last updated on June 3, 2020.

We are pleased to present Magento Open Source 2.3.2. This release includes over 200 functional fixes to the core product, over 350 pull requests contributed by the community, and over 75 security enhancements. It includes significant contributions from our community members.

Other release information
-------------------------

Although code for these features is bundled with quarterly releases of the Magento core code, several of these projects (for example, Page Builder, Inventory Management, and Progressive Web Applications (PWA) Studio) are also released independently. Bug fixes for these projects are documented in separate, project-specific release information which is available in the documentation for each project.

New security-only patch available
---------------------------------

Merchants can now install time-sensitive security fixes without applying the hundreds of functional fixes and enhancements that a full quarterly release (for example, Magento 2.3.3) provides. Patch 2.3.2.2 (Composer package 2.3.2-p2) is a security-only patch that provides fixes for vulnerabilities that have been identified in our previous quarterly release, Magento 2.3.2.

**If you have already upgraded to the pre-release version of this patch (2.3.2-p1), we strongly recommend that you upgrade to 2.3.2-p2 as soon as possible.**  Patch 2.3.2-p2 contains the critical security fixes that are included in Magento  2.3.3, 2.2.10, 1.9.4.3, and 1.14.4.3, but that are not included in patch 2.3.2-p1.

Substantial security enhancements
----------------------------------

This release is focused on substantial security enhancements:

*  **75 security enhancements** that help close cross-site scripting (XSS), remote code execution (RCE), and sensitive data disclosure vulnerabilities as well as other security issues. No confirmed attacks related to these issues have occurred to date. However, certain vulnerabilities can potentially be exploited to access customer information or take over administrator sessions. See [Magento Security Center](https://magento.com/security/patches/magento-2.3.2-2.2.9-and-2.1.18-security-update) for a comprehensive discussion of these issues. All known exploitable security issues fixed in this release (2.3.2) have been ported to 2.2.9, 2.1.18, 1.14.4.2, and 1.9.4.2, as appropriate.

*  **Google reCAPTCHA module for PayPal Payflow checkout**. The new PaypalRecaptcha module adds Google reCAPTCHA and CAPTCHA to the Payflow Pro checkout form.  This enhanced functionality has been added in response to malicious targeting of Magento deployments that implement Payflow Pro.


Performance boosts
------------------

*  **Significant improvement to storefront page response time**. The page response times for the catalog, search, and advanced search pages have been significantly improved under high load.

*  **Improved concurrent access to block cache storage**. We have optimized the logic of concurrent access to the block cache, which  has improved the response of storefront pages under high load by approximately 20%. 

*  **Product page gallery load optimization**.  Product images are now loaded as quickly as other page content. In previous releases, although the product page loaded quickly, product images needed two to four additional seconds to load completely.

*  **Improved page rendering through deferred loading and parsing of storefront JavaScript**. All non-critical JavaScript code has been relocated to the bottom of storefront pages, which speeds up page rendering and allows users to see the complete page sooner while nonessential elements remain inactive. To enable this performance enhancement, you must navigate to **Stores** > **Configuration** > **Developer** > **JavaScript Settings** and enable the **Move JS code to the bottom of the page** option.  

Infrastructure improvements
---------------------------

This release contains 130 enhancements to core quality, which improve the quality of the Framework and these modules: `Catalog`, `Sales`, `Checkout/One Page Checkout`,  `UrlRewrite`, `Customer/Customers`, and `UI`. Here are some additional core enhancements:

*  **Braintree payment method is now supported for checkout with multiple addresses**. Previously, you could not use Braintree and Braintree PayPal when checking out an order that was being shipped to multiple addresses.

*  **The CGI URL gateway in UPS module has been updated from HTTP to HTTPS**. The CGI URL gateway endpoint in the UPS module has been updated  from HTTP to HTTPS in response to the disablement of the HTTP gateway by UPS in mid-2019.

*  **Google chart API updated to the Image-Charts**. Magento now uses the Image-Charts free service to render static charts in Admin dashboards. Earlier deployments used Google Image Charts, which was deprecated in 2012 and turned off on March 18, 2019

Merchant tool enhancements
~~~~~~~~~~~~~~~~~~~~~~~~~~

Magento now performs the following tasks as **asynchronous background processes** and sends system messages to alert Admin users when tasks complete. Moving these common administrative tasks to the background frees administrators to work on other tasks while the initial tasks are processing.

*  Discount coupon generation. See `Coupon Code <https://docs.magento.com/m2/ee/user_guide/marketing/price-rules-cart-coupon.html>`_.


*  Mass editing of products.

*  Data export. Previously, connection timeouts occurred during export of large data sets (for example, the export of 200,000 products).



Vendor-developed extension enhancements
---------------------------------------

This release of Magento includes extensions developed by third-party vendors.

Amazon Pay
~~~~~~~~~~

Amazon Pay is now compliant with the PSD2 directive for UK and Germany. See [Payment services (PSD 2) - Directive (EU)](https://ec.europa.eu/info/law/payment-services-psd-2-directive-eu-2015-2366_en) for an introduction to PSD2.

Fixed issues
------------

We've fixed hundreds of issues in the Magento 2.3.2 core code.

Installation, upgrade, deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*  `configFactory` `scope` and `scope_code` values are now passed to `configFactory`   as data arrays. 


*  Magento now renders the value of configuration variables (such as `{{unsecure_base_url}}`) as they are entered in  configuration files rather than saving the resolved value. Previously, Magento resolved the variable to its actual value, which lead to the overwriting the value in the database when the configuration was saved instead of storing the value in the variable. 


*  Magento no longer throws an error when you use  `app:config:import` to import configuration settings. Previously, the import failed, and Magento threw the following error even when the imported file contained only minor changes to password or URL values: `Please specify the admin custom URL`.

*  Magento no longer throws an error when executing `bin/magento setup:static-content:deploy` in parallel mode if theme or locale deployment takes more than 400 seconds. Previously, Magento threw the following error under these conditions: `2436; Status: 0`.


*  Magento no longer throws an error during catalog set up when you run `bin/magento setup:upgrade`. Previously, set up failed, and Magento threw the following error even though no problems existed with your catalog, `Magento\Catalog\Setup\Media does not exist`.

*  All fields are now hidden with appropriate dependencies as assigned in the backup configuration settings.

*  Updated the email template stylesheet for the Magento default and Luma themes to correctly specify the `.no-link` selector. This update fixes the following less compilation error that displayed when compiling the `email-inline.less` file using less.js compiler v2.73: `extend ' .no-link a' has no matches`.

Backend
~~~~~~~

*  The **State/Province** field is no longer marked as mandatory in the Admin customer address form. Previously, this field was always marked by an asterisk, even when the field was not required.


*  The icon that identifies a dropdown menu throughout the product interface now reflects the changing state of the dropdown menu's status (expanded or collapsed).


*  Form fields of type multi-line now work as expected on Admin forms. 

*  Fixed display of **Option Title** label on **Catalog** > **Product** > **Customizable Options** > **Add Option**.

*  Magento now displays the correct date in the Admin for scheduled design changes. Previously, Magento displayed the current date instead of the scheduled date on **Content** > **Design** > **Schedule**.

*  Fixed alignment of the **Marketing** > **Cart Price Rules** > **Store View Specific** labels on the Admin.


*  The Change Status option of the mass actions dropdown menu (available on the products and sales pages) now works as expected.


*  The option type dropdown on the Admin Customizable Options page now works as expected.

*  The JavaScript `minify` field on **Stores** > **Configuration** > **Advanced** > **Developer** is now disabled as expected. 

*  Magento retains the filter settings you enter on the **Admin** > **System** > **Permissions** > **All Users** list when you click on an item in the filtered list, then return to the list. Previously, if you navigated away from the list and then returned, all filter parameters were lost. 

*  The web setup wizard now uses the correct base path to check if the setup folder exists. Previously, the wizard checked `base/data/web/magento2/pubsetup` instead of `/data/web/magento2/pub/setup`.


*  Magento now redirects to you the Admin home page or a 404 page as expected when you try to access a nonexisting Admin page and **Stores** > **Configuration** > **Advanced** > **Admin** > **Security** > **Add Secret Key to URLs** is enabled. Previously,  redirects did not work properly, and Magento displayed the following message: `The page isn’t redirecting properly`.

Back up
~~~~~~~

*  Magento now creates the `var/.maintenance.flag`  file as expected when you start a database backup  (**System** > **Tools** > **Backups** > **Database Backup**). Previously, Magento did not create this  file, but instead displayed the following error: `Error: You need more permissions to activate maintenance mode right now. To create the backup, please deselect "Put store into maintenance mode" or update your permissions`.

Bundle
~~~~~~

*  Magento now calculates and displays the correct tier price for bundle products.

*  Tier pricing for bundle products now works as expected: Magento displays the correct  price in the cart, and reminds customers that they can buy a specific quantity of the  product for a discount. Previously, Magento did not calculate the price correctly and did not display any informative messages about tier pricing on the category and product pages.

Cache
~~~~~

*  CMS block cache keys now contain the appropriate store ID in deployments with multiple store views. Previously, Magento always loaded the cached version of the block for the first store view.


Cart and checkout
~~~~~~~~~~~~~~~~~

*  Magento now correctly updates the mini cart if a selected product is disabled during the shopping session.


*  Magento now persists the shipping quote in the shopping cart for guest customers when **Persistent Shopping Cart** is enabled.


*  Magento now persists customer-related values after a guest customer converts her account to a customer account after checkout. Previously, Magento saved these customer-related values as null during account creation after checkout. 

*  Guests can now complete checkout when a custom shipping carrier with underscores in the carrier code is used. Previously, Magento threw the following exception under these conditions: `Please specify a shipping method`.


*  Fixed alignment of the **Update** button on the payment page of the checkout workflow.


*  Magento no longer displays the infinite loading indicator when you proceed to check out. Previously, Magento displayed the loading indicator, and threw the following JavaScript error: `Cannot read property 'quoteData' of undefined`.


*  Magento now displays an error message as expected when a customer clicks on **Add to cart**  without selecting at least one product from the recently ordered  product list. 


*  The **Cancel** button on the checkout page now works as expected. 


*  Magento no longer runs `UpdateItemQty` validation before a Clear Shopping Cart action is triggered. Previously, due to the timing of this validation, you could not empty the shopping cart if any product in the cart was out-of-stock.

*  Magento now uses the value of the default billing address attribute as expected during checkout. 


*  Magento now validates the shipping information section of checkout as expected. Previously, a customer could proceed to the Payment Details section of checkout without having added valid shipping details. 

*  The `label` elements  on the checkout address input fields are now readable by screen readers. Previously, the  address input fields did not have a `label` element with a valid value, which prevented screen readers from reading the values.


*  New downloadable products now show up in a customer's My Downloadable products list after a customer who completed a purchase as a guest then creates an account.

*  The checkout page now provides the ability to search addresses instead of listing addresses only on the Select shipping and Billing address steps. This new search feature can substantially increase checkout performance for customers with thousands of addresses. It is disabled by default and  must be enabled from the Admin.

Cart Price rules
~~~~~~~~~~~~~~~~

*  Magento now displays the Cart Price Rule code on an order details Admin page if free shipping applies. Previously, Magento did not display information about the Sales rule or why shipping was free.

Catalog
~~~~~~~

*  You can now use the term **configurable** as a group name in attribute sets. Previously, Magento threw an error when you used this term as a group name and subsequently tried to add or edit a product. 

*  Product search results now display the correct special price as set by a scheduled update. Previously, search results displayed the original special price, not the price set by the scheduled update. **This fix can degrade performance in deployments that implement flat catalogs. To avoid this potential performance degradation, consider disabling flat catalogs**.


*  Clicking on a store's root category now causes only that root category to expand. Previously, Magento expanded all other Root Categories into the top-level categories.


*  Magento now maintains correct pagination when a Catalog list has multiple pages of products.  Previously, users were redirected to the first page (instead of the correct page) after navigating to a product from the list and saving it.


*  We have improved the performance of the grouped product detail pages and category pages that contain a large number of grouped products.


*  You can now use storeview-level attributes to filter products on the products list.


*  Magento does not display the Country of Manufacture field under the More Information tab of the product page when this value is empty.


*  A product's  `product:price:amount` metatag now contains the price converted to the appropriate base currency in multistore deployments with stores using different base currencies. Previously, the price in this metatag was always calculated in the base currency.

*  Magento now correctly calculates multi-currency custom option prices when the option price type is `percentage`. Previously, when the multi-currency custom option was set to a percentage price type, Magento calculated the price incorrectly.


*  The  `product_types_base.xsd`, `product_options.xsd`, `import.xsd`, `export.xsd` files  now allow modules with names that contain  numbers.


*  Magento no longer adds tax twice when adding a new product with tier pricing. Previously, MinimalTierPriceCalculator applied the tax twice when calculating the minimal price. 


*  The Admin product grid now displays default values when no filter is set. 


*  The Magento implementation of the `CategoryManagementInterface::getTree($rootCategoryId)` now provides a tree that is populated with children instead of an empty array.


*  Magento no longer empties the shopping cart when you click **Enter** after changing a product's quantity.


*  Fixed issue with excessive white space on  the related, cross sell and upsell product grids.


*  You can now sort the Admin product list by website.

*  Magento now creates unique values for product attributes as expected when you duplicate a product. Previously, Magento duplicated a product, but both products had the same attribute values.


*  During product creation, Magento now displays default attribute values from the **Admin** column on the Manage Options (Values of Your Attribute) window when creating options. Previously, Magento displayed options from the default storeview.

*  You can now add an out-of-stock item to a product comparison. Previously, Magento displayed a success message, but did not add the item to the comparison.


*  The catalog product flat data table for a store view is now populated with data from the specified store view as expected. Previously, this table was populated with data from the default store view.

*  Magento now applies the correct tier price for a product after a customer who is assigned to a customer group logs in after first adding items to their cart as a guest. Previously, Magento did not apply the tier price after the customer logged in.


*  The `product_type` attribute now contains the correct value in the CVS file that is created during export after you create a `custom type_id` attribute.


*  Magento now increments product quantity correctly when you add products to your cart first as a guest user, and then logged in. Previously, Magento added items separately instead. 

*  **Meta Keywords** and **Meta Description** are now defined as `textarea` throughout  product forms.


*  Magento now saves customizable option price input on the store-view level when Catalog Price Scope is set to **Global**. Previously, customizable option prices were not saved on the store-view level when Catalog Price Scope was to **Global**.


*  We have modified the required permissions for updating the `design` fieldset of categories, products, and CMS pages:

   *  Existing roles that have **save** permission for these entities can save everything.

   *  New roles will need to be granted permission to edit design manually.

   If you do not have permission to edit the `design` fieldset or use web API endpoints to update a category, Magento does not save your changes and the design properties remain unchanged


*  When you configure a price rule for configurable products with swatches, Magento now a shows the special price for products that match the price rule. Previously, Magento displayed both the old price and the special price for the matching configurable products.

CatalogInventory
~~~~~~~~~~~~~~~~

*  We have fixed the wrong proxy `resourceStock` argument for the `\Magento\CatalogInventory\Observer\UpdateItemsStockUponConfigChangeObserver` in `di.xml`. (Specifically, `<argument name="resourceStock" xsi:type="object">Magento\CatalogInventory\Model\ResourceModel\Stock\Proxy</argument>` has been changed to `<argument name="resourceStockItem" xsi:type="object">Magento\CatalogInventory\Model\ResourceModel\Stock\Item\Proxy</argument>`.)

Catalog URL rewrite
~~~~~~~~~~~~~~~~~~~

*  URL rewrites are no longer overwritten in multisite deployments.


Cleanup and simple code refactoring
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*  Corrected overlapping **Rating** field and **Add to cart** button on the cart page. 

*  Corrected length of the customer login page input field in tablet view.


*  Fixed misalignment of the checkbox in the fields enclosure on **Admin** > **System** > **Export**.


*  Corrected misalignment of the products in category checkboxes on the Admin catalog categories page. 


*  Corrected misalignment of the order item details label  in mobile view. 


*  Corrected misalignment of page elements on the Admin product reorder page.

*  You can now open a product's details page from the compare products side bar.


*  Added padding to the `shippingAddress` telephone tool tip on the shipping page of checkout.


*  Corrected misalignment of product prices in the order summary block of the checkout page in tablet view. 


*  Corrected size of the pagination drop-down on **Admin** > **Content** > **Blocks**.

*  Corrected a tabbing issue on the product page. 

*  Corrected alignment of page elements on the  Recent Orders section of the My Accounts page in mobile view.


*  Corrected formatting of the Advance Search link in page footers. 


*  Corrected alignment of the minicart search logo. 


*  Added missing asterisk adjacent to the Checkout Agreements checkbox. 


*  Removed unneccessary white space between `li` tags in the product table. 


*  The documentation for Travis CI static tests has been improved. 


*  Corrected typos on the Admin sales shipment and credit memo pages. 


*  The **Equalize product count** operation in Layered Navigation now works as expected. 

*  Corrected misalignment of page elements on the popup window that Magento displays when you edit an order that contains a downloadable product when **Links can be purchased separately** is enabled.


*  Fixed misalignment of the shipping method block on Order pages that are accessed through **Sales** > **Orders**.


*  In the Conditions section of the New Cart Price Rule page in the  Admin, the dropdown arrow in the `_If ALL of these conditions are TRUE _ field` now points in the correct direction.

Configurable products
~~~~~~~~~~~~~~~~~~~~~

*  Magento no longer describes a configurable product as in-stock in the product list when the product is set to out-of-stock.


*  Corrected the position of the labels in the configurable product variations table.

*  Configurable products can no longer be added as a variation of another configurable product in the Admin.


*  The configurable product page's attribute dropdown menu shows an accurate price and tax is rendered correctly in the final price at the top of the page. Previously, configurable products that had only one configurable attribute displayed a price increase in the dropdown of the tax amount. This affected stores when prices were entered excluding tax and configurable products with only one configurable attribute. 

*  Configurable products can now be successfully updated through the bulk API (specifically, this API endpoint: `rest/async/bulk/V1/configurable-products/bySku/child`).

cron
~~~~

*  Added support for `Zookeeper <https://php.net/manual/en/book.zookeeper.php>`_ and flock lock providers. We have also added new options to configure locks during installation:

   *  `--lock-provider=LOCK-PROVIDER`—Lock provider name

   *  `--lock-db-prefix=LOCK-DB-PREFIX`—Installation specific lock prefix to avoid lock conflicts

   *  `--lock-zookeeper-host=LOCK-ZOOKEEPER-HOST`  —Host and port to connect to Zookeeper cluster. For example, 127.0.0.1:2181

   *  `--lock-zookeeper-path=LOCK-ZOOKEEPER-PATH`— The path where Zookeeper will save locks. The default path is /magento/locks

   *  `--lock-file-path=LOCK-FILE-PATH`—The path where file locks will be saved.


Customers
~~~~~~~~~

*  Magento no longer empties your shopping cart after you have reset your password. Previously, if you added items to your shopping cart using a guest account, then logged in and reset your password, Magento emptied your cart.


*  Magento now saves dates that are associated with custom customer attributes of type `date`. Previously, Magento did not save these dates, but displayed the following message: `Please enter a valid date`.


*  The Customer Name Prefix on the customer configuration page no longer displays extraneous white space when an extra separator is added.


*  Fixed a horizontal scrolling issue that affected the address book display in mobile view.


*  The default sort order setting for the shopping cart and customer orders page is now `by create date in descending order`.

*  The customer login block (defined as `Magento\Customer\Block\Form\Login`) no longer sets the page title.

*  An admin user with full permissions for all website scopes can now see any country listed in the Countries column or filter in the Customers list. Previously, if one of the website scopes did not allow a country, an admin with full permission could not see it.


*  Magento no longer applies the default customer group settings to customers that have already been assigned to another group.


*  Customer groups can now be successfully reassigned during order creation in the Admin.


*  Customer accounts are now confirmed when a customer clicks the email activation link. Previously, Magento confirmed the customer account even when the customer did not click on the email activation link.

Dashboard
~~~~~~~~~

*  Magento no longer throws a  404 error when you click the Most viewed products on the Admin dashboard. 

Downloadable
~~~~~~~~~~~~

*  Product prices are no longer duplicated on the Downloadable products page. 


*  Sales rule validation has been refactored to eliminate a leak in the salesrule collection. Previously, a poorly constructed SQL query resulted in poor performance. 


*  You can now successfully change the sample file for an existing downloadable product. Previously, when you tried to change this sample file, Magento did not save the new file, and did not display an error message.


*  A logged-in user's My Downloads page now displays links to the relevant downloadable products when **Order Item Status to Enable Downloads** is set to **Pending**. Previously, Magento displayed only the names of the pending products, and no links for downloadable products were displayed.


*  Added missing sort order to columns on Downloadable Product links page.

EAV
~~~

*  Attribute code validation (specifically, maximum characters allowed) has been improved during attribute creation. 


*  Initialization has been added to two class variables that can be returned by class methods as parameters of type `array`. Without this initialization, both variables are returned as null, which can cause Magento to throw  an `Invalid argument supplied for foreach()` warning.


*  The `\Magento\Eav\Model\Entity\Collection\AbstractCollection::importFromArray()` method now returns a usable collection. Previously, the  `_isCollectionLoaded` property was false, and every interaction threw an exception. 

*  You can now retrieve product attribute values for store-view scope types in the product collection that is loaded for a specific store.


*  You can now programmmatically upload an image for the customer attribute. Previously, Magento threw the following error:  `error: Base64 is not defined`.

*  Scope assigned to prices in Catalog Price Scope (set in **Configuration** > **Price**) are now maintained when price is set to empty. Previously, you could not leave special prices empty.


*  Added an `is_array` parameter value check to the `getOptionText($value)` function in `app/code/Magento/Eav/Model/Entity/Attribute/Source/AbstractSource.php` to fix an error that caused Magento to throw a UI error when you make the `_quantity_and_stock_status (Qty)_` product attribute visible in the storefront properties. Previously, the `getOptionText($value)` function expected integer or string input and failed because the `quantity_and_stock_status (Qty)` configuration parameters were passed as an array.`

Email
~~~~~

*  Magento no longer sends via asynchronous email sending any sales-related emails  that were created when email sending was disabled once email sending is enabled.


*  The Insert variable popup window that is accessed from the Email Template Information window is now populated as expected.

Frameworks
~~~~~~~~~~

*  The performance of product image loading has been significantly improved.

*  You can now successfully download a downloadable product by clicking the link to the product in your downloadable products list. Previously, when you clicked this link, the page did not open correctly, and Magento threw the following error: `Something went wrong while getting the requested content`. 


*  Added the `as` attribute to `linkType` in `lib/internal/Magento/Framework/View/Layout/etc/head.xsd` with three possible options: `style`, `script`, and `font`.


*  Corrected misalignment of the Admin success message icon.


*  The use of the `SessionManagerInterface` class has replaced the direct use of  `SessionManager`.


*  The module ranking in the `app/etc/config` now remains consistent when a new module is added without any other changes. Previously, a module addition affected the module ranking, which resulted in multiple unnecessary conflicts. 


*  Magento now logs exceptions during autoloading instead of throwing them. This conforms with PSR-4 guidelines. 

*  Running the `php bin/magento setup:upgrade` command on modules that have a `db_schema.xml` without an `indexType` now creates the index, and subsequent runs result in no modifications as expected. Previously, running this command multiple times resulted in index creation followed by an error.

Cache framework
~~~~~~~~~~~~~~~

*  The purge cache feature in `\Magento\CacheInvalidate\Model\PurgeCache::sendPurgeRequest` has been updated to flush the cache on all hosts even when a Varnish servers is offline. Magento also displays a warning message about unresponsive cache hosts.  Previously, the `bin/magento cache:flush full_page` operation stopped as soon as it encountered a host that was offline.

JavaScript framework
~~~~~~~~~~~~~~~~~~~~

*  JavaScript validation on UI form components now works as expected. Previously, adding the `validate-per-page-value-list` validation rule resulted in a failure for every non-empty value in the field to which it as applied.

### General fixes


*  The Sodium crypto adapter now consistently returns a `string` in accordance with the strict return type on its signature. Previously, the adapter sometimes did not return a `string`, which resulted in exceptions and a failure to bootstrap Magento.


*  Watermarks now appear on product images as expected.


*  You can now use a period (`.`) for inline CMS content edits. Previously, if you included  a period (`.`) in your edits, Magento displayed this error: `There are 1 messages requires your attention. Please make corrections to the errors in the table below and re-submit`.


*  The pagination count of **My Account** > **My addresses** > **Additional Address Data Table** is now correct.


*  `fatalErrorHandler` now returns `500` only on fatal errors. Previously, simple deprecation warnings on the page triggered an internal server error, which was invalid.


*  CodeSniffer no longer marks correctly aligned `DocBlock` elements as code style violations.


*  The Adminhtml `textarea` field now accepts the `maxlength` attribute.

*  The Reporting Security Issues section of the [Magento 2 README file] ({{ site.mage2bloburl }}/{{ page.guide_version }}/README.md) has been updated to reflect the use of HackerOne for the Magento 2 Bug Bounty program.


*  You can now save an inactive admin user token by navigating to **System** > **Permissions** > **All Users**, and clicking **Save User** on an inactive Admin user. Previously, if you tried to save an inactive Admin user token fom the Admin this way, Magento did not save the token, but threw an error.


*  The missing `$msrpPriceCalculators` argument for `Magento\Msrp\Pricing\MsrpPriceCalculator` has been added. Previously, Magento threw an `MsrpPriceCalculator` exception after an upgrade.

*  `stream_wrapper_unregister('phar')` in `app/boostrap.php` is now unregistered only when appropriate. Previously, calling `stream_wrapper_unregister('phar')` without checking to see if it were registered triggered a warning.

*  The sitemap generation `cron` job no longer flushes the entire cache. A dummy cache tag has been added to the frontend for sitemap and robots generation to prevent the default and `page_cache` from being dropped completely. Previously, the sitemap generation cron job flushed the entire cache.


*  Magento now sets an accurate  `CURRENT_TIMESTAMP` on `updated_at` fields in the database schema. Previously, this timestamp displayed `0000-00-00 00:00:00`. 


*  `grunt watch` no longer triggers `livereload` twice.


*  You can now duplicate a product with translated URL keys over multiple storeviews without generating non-unique keys. Previously, when a product was duplicated, only one URL key was used and set for all store views.

Google Analytics
~~~~~~~~~~~~~~~~

*  Google Analytics `Anonymize Ip` no longer always set to on.

Google Chart API
~~~~~~~~~~~~~~~~

*  The Google chart API has been updated to the Image-Charts. Magento now uses the Image-Charts free service to render static charts in Admin dashboards. Earlier deployments used Google Image Charts, which was deprecated in 2012 and turned off on March 18, 2019

Import/export
~~~~~~~~~~~~~

*  Magento now imports existing products that have a price change and unchanged `url-key` with no unnecessary updates. Previously, the product's price was updated as expected, but its unchanged `url-key` was deleted.


*  Magento now displays informative messages when you create a new product and try to set its SKU to one that is assigned to an existing product. Previously, under these circumstances, Magento displayed an informative message, but also imported the newly created product's configurable options to the older product.


*  The import process  `replace` method now works as expected.


*  The import process now imports product quantity as expected.

*  Custom import adapters now validate CSV files as expected if column and data are available. Previously, the CSV file was not validated, and Magento threw the following error: `Notice: Undefined index: sku in /var/www/html/hamtc/vendor/magento/module-import-export/Model/Import/Entity/AbstractEntity.php on line 411`. 


*  The `_coreConfig` field in `Magento/ImportExport/Model/Import` is no longer declared dynamically.


*  Tooltip styles now use the appropriate variables for mobile view.

*  Magento now displays the correct import status data for an import that is created using **System** > **Import** > **Advanced Pricing** > **Add/Update**.


*  The `store_view_code` column now contains data from the chosen product store. Previously, Magento did not populate the `store_view_code` column. 

Index
~~~~~

*  You can now access a list of Admin indexers after creating a custom index. Previously, when you tried to access the Admin's indexer list,  Magento threw a fatal error.


*  Magento now validates CSV files that are created by custom adapters when you click **Check Data** if column and data are available. Previously, Magento threw an error. 

Infrastructure
~~~~~~~~~~~~~~

*  The default behavior of view models has changed in this release. Instances of view models are now shared by default. As a result, you must add the `attribute shared="false"` on the argument node of the `layout.xml` file if you want a new instance of a view model.


*  The `FrontController` now explicitly requires actions to specify if they respond to `HEAD` requests. `HEAD` action mapping has also been changed to the  `GET` action interface, which results in `HEAD` requests returning `200` instead of `404`.


*  Logic has been removed from the constructor of `Magento\Sales\Model\Order\Address\Validator`. Previously, installation of the product could fail if this class was injected in the constructor through a command in a custom module when this class contined logic.


*  The `productAvailabilityChecks` argument has been added to `Magento\Sales\Model\Order\Reorder\OrderedProductAvailabilityChecker`. Previously, this required argument was missing.


*  The `errors/local.xml` and error page templates are no longer publicly accessible.

*  We added the missing  attributes `validated_country_code` and `validated_vat_number` to `quote_address`. 

*  We added Type casting to `\Magento\Shipping\Model\Carrier\AbstractCarrier::getTotalNumOfBoxes()` to improve  validation. 


*  Widget parameters can now contain multidimensional arrays.


*  `phpcs` now reports all errors and warnings in the terminal as expected. Previously, `phpcs` threw an error instead of reporting errors under certain circumstances.


*  The `getSize()` method in `\Magento\Framework\Data\Collection` now returns results that reflect added filters as expected when the `clear()` method is called after `getSize()`. Previously, this method returned results that always remained the same after the first call and the `clear()` method was ignored.


*  Magento no longer caches absolute file paths in  the validator factory  (`Magento\Framework\Validator\Factory::_initializeConfigList`). Previously, caching absolute file paths resulted in problems during transactions when a customer, a `customer_address`, or quote for a registered customer was saved.

*  `QuoteRepository` `get` methods now return an object of instance `Vendor\Module\Model\Quote`. 


*  Magento no longer throws an exception under these conditions:

   *  a product configuration specifies a **Minimum Qty Allowed in Shopping Cart** as a decimal value less than one

   *  this configuration is later updated by setting  **Qty Uses Decimals**  to **no**, and later updating the **Qty Uses Decimals** attribute in the product congiration to **no**.

Layered navigation
~~~~~~~~~~~~~~~~~~

*  Setting **price navigation step calculation** for layered navigation to **Automatic (equalize product counts)** now works as expected. Previously, results were not in the equals range, but omitted products.


*  Use of the Yes/No attribute in the Layered Navigation filter no longer degrades filter performance.

*  Magento now retrieves the configuration value (store ID)  that is  based on the current store scope in multistore deployments. Previously, Magento occasionally returned an incorrect configuration scope ID when attempting to resolve a scope ID set to null.

Logging
~~~~~~~

*  Magento now creates a log entry if an observer does not implement `ObserverInterface` in modes other than developer mode.  Previously, Magento created a log entry when in developer mode only.

Magento Shipping
~~~~~~~~~~~~~~~~

*  Fixed issue with the event stream cron job.

*  Fixed issue with retrieving shipping labels from some AWS environments.

### New Relic reporting


*  Improved performance of New Relic queries. The New Relic Reporting module now cleans the Magento 2.x report data to prevent the reporting data store from growing too large and slowing query performance.


*  Magento 2.x CLI command names are now reported in the transaction names in the New Relic APM Monitoring Data. The transaction name is based on the Magento CLI command name, for example `cli app:config:import`, `cli indexer:reindex`, and `cli cache:flush`. In previous releases, the New Relic transaction names for CLI commands initiated by Magento 2.x CLI command names was missing and reported as unknown.

Newsletter
~~~~~~~~~~

*  You can now change pages at an expected speed from the Admin newsletter subscribers page (**Marketing** > **Communications** > **Newsletter Subscribers**). Previously, it took excessively long to move off this page.


*  The newsletter subscription input box now displays all text in mobile view.

Orders
~~~~~~

*  The quick order form now handles the SKUs that you enter for configurable products as expected. Previously, Magento threw an error when you tried to enter the SKU for a configurable product, and displayed a link to the simple product which typically returned a 404 page.


*  Programmatically created invoices now include all items as expected when both simple products and bundled products are mixed in an order. Previously, when  `Magento\Sales\Model\Service\InvoiceService::prepareInvoice` was called without a specified quantity, the function did not discards items as expected after bundled items were processed, which resulted in a partial invoice.


*  When you create new extension attributes for orders, these attributes are now correctly joined when querying orders.

Page cache
~~~~~~~~~~

*  Page cache is no longer active when maintenance mode is enabled.  Previously, Magento cached  pages from all IP addresses during maintenance mode.

Payment methods
~~~~~~~~~~~~~~~

*  Magento no longer throws an error indicating that a transaction was declined when Authorize.net successfully processes the order. Previously, orders were successfully created but Authorize.net indicated that the transaction had been declined.


*  Magento creates an order using PayPal PayflowPro as expected when a customer enters all the credit card information that PayPal needs to create the transaction. Previously, Magento did not create the order even though all necessary credit card information has been entered.


*  Alt attribute text that describes  credit card type or stored payment methods during checkout has been added to support accessibility.

Performance
~~~~~~~~~~~

*  Client-side performance has been optimized by moving non-critical JavaScript code to the bottom of the page along with the corresponding deferred parsing and evaluation of this code. This means that users can see  rendered pages faster. To enable this performance enhancement, you must navigate to **Stores** > **Configuration** > **Developer** > **JavaScript Settings** and enable the **Move JS code to the bottom of the page** option.


*  The transfer cart line items and transfer shipping options in the Shipping step of checkout now work for PayPal.


*  The multishipping checkout flow now supports the Braintree payment method.


*  Magento no longer disables the **Place order** button in the checkout workflow after the customer has supplied the requested email address for orders created with Braintree. 


*  We've optimized the logic of concurrent access to the block cache, which  has improved the response of storefront pages under high load by approximately 20%.

Quote
~~~~~

*  `QuoteManagement::submitQuote` now logs all root exceptions. Previously, Magento logged only the second exception in `exception.log`.


*  The `x_forwarded_for` field of the Quote Management service now contains the value from `$_SERVER['HTTP_X_FORWARDED_FOR']`. Previously, this field was always empty. This change will permit administrators to see their customer's actual IP addresses (as opposed to 127.0.0.1), which can help identify potentially fraudulent orders.

Reports
~~~~~~~

*  The date range in reports no longer displays the same start and end dates.

*  Magento now includes the amount of a credit memo's refunded discount in its calculation of the value displayed in the total column under the **Last Orders** listing on the Admin dashboard.


*  The downloads report table (**Admin** > **Reports** > **Downloads**) now displays an accurate count of all downloadable products and the number of times they have been downloaded.

Reviews
~~~~~~~

*  The  text for review-related headers under **User Content** on the Admin  has been edited for clarity.

Sales
~~~~~

*  Corrected problems with the disabling and enabling order-related emails.


*  Fixed display of the Luma theme My Account Order status tabs in mobile view.

*  You can now change customer groups when creating a new customer during order creation on the Admin.

*  You can now successfully re-order a virtual product. 

*  When you place an Admin order for a product with a custom price, the `sales_order_item` table now behaves the same as it would for an order of a product with a regular price. Specifically, the price column  contains the custom price excluding tax. Previously, the `sales_order_item` table's price column displayed the custom price including tax.


*  Form validation now works as expected for fields in the Admin order address edit forms. Previously, when you entered invalid data, Magento did not display an error message and displayed the data.


*  If you retrieve an order, and then use the `getShippingMethod` as object function to retrieve the shipping method, Magento now returns `null` if no shipping method has been defined. Previously, this function returned an undefined index error if a shipping method was not available.

SalesRule
~~~~~~~~~

*  The DataProvider and Save Controller files have been edited to improve persistence of form data in cart price rules.


*  Added a condition `type _Subtotal (Excl. Tax)` to the Cart Price Rule configuration so that you can configure a cart price discount rule discount based on minimum purchase amount that excludes tax. Previously, the subtotal was calculated only with tax included.

Search
~~~~~~

*  Catalog search **Minimal Query Length** values are now enforced as expected.


*  Elasticsearch quick search now works as expected when the default attribute set contains a `date` attribute that has been set to **Search = Yes**. Previously, the search page threw an exception and crashed.


*  The performance of layered navigation queries has been improved.


*  The search REST API now returns the correct `total_count` of result items. Previously, the value of `total_count`  equaled `searchCriteria[pageSize]`,  not the total count of the search result items.


*  The search icon on Admin page headers now works as expected. 


*  Magento now checks concrete class while applying plugins. Previously, when  the pluginized class was virtual-typed by a class with name ending with an autogenerated suffix and without the implementation of the base concrete class, the `di:compile` process failed.  

Shipping
~~~~~~~~

*  UPS (non-XML) endpoints are now HTTPS instead of HTTP. 


*  Magento now provides quotes for DHL shipments when **DHL Content Type** is set to **Non Documents**. 

*  The CGI URL gateway endpoint in the UPS module has been updated from HTTP to HTTPS in response to the disablement of the HTTP gateway by UPS in mid-2019. See [Magento User Guide](https://docs.magento.com/m2/ee/user_guide/shipping/ups.html) for a discussion of using the UPS shipment method.

*  The tracking pop-up window now displays an accurate value for the delivery date for FedEx shipments in transit.

Sitemap
~~~~~~~

*  Images in the XML sitemap are no longer linked to the base store in a multistore deployment when scheduling start times and daily frequency.


*  Magento now validates sitemap file names to ensure that file names do not exceed length limits. Previously, Magento simply truncated excessively long file names.

Swatches
~~~~~~~~

*  Corrected `blackground` to `background` in `Magento_Swatches _module.less`.


*  You can now successfully preselect a configurable product swatch that contains an image. Previously, Magento tried to load the image into the product gallery before initialization completed and threw a JavaScript error.

Tax
~~~

*  The tax that is applied to a simple child product is now  based on the tax class of that product. Previously, Magento based the tax for a child product on the tax class of its parent product.


*  The shopping cart full tax summary now displays total tax as expected instead of  individual tax values.


*  The value of `product_price_value` in the shopping cart data section  now includes taxes if the configuration settings are set accordingly (**Stores** > **Configuration** > **Sales** > **Tax** > **Shopping Cart Display Settings** > **Display Prices** > **Including Tax**).


*  You can now successfully search for a tax rule based on both the **Name** and **Tax Rate** fields. Previously, Magento threw an MySQL error.

Testing
~~~~~~~

*  The `Squiz.Operators.ValidLogicalOperators` PHP-CS rule has been added to the static test rules.

*  Added missing parameters to failing unit tests for `FormatTests`. 

Theme
~~~~~

*  Logo files for transactional emails can now be successfully uploaded  using **Content** > **Configuration** > **Edit theme** > **Transactional Emails**. Previously, Magento did not upload the logo, but displayed this error:  `A technical problem with the server created an error. Try again to continue what you were doing. If the problem persists, try again later.`

*  The horizontal scroll widget on the storefront search results page now works as expected with very long search strings.

*  Checkboxes and radio buttons are now highlighted on focus while you navigate a form using the keyboard.  This change is a reversion of an earlier fix (20861), which inadvertently violated accessibility standards for keyboard  navigation.


*  Magento now successfully uploads files from the theme config edit form page when you click **Select from Gallery** button for the **Logo Image** field.

Translation and locales
~~~~~~~~~~~~~~~~~~~~~~~

*  Product attribute labels are no longer translated.

UI
~~

*  You can no longer upload images when the **Use Default Value** setting on the Admin Content tab is enabled. Previously, you could drag an image to this tab even when this setting was enabled.


*  The Date field associated with a page on the  Admin Pages table now displays the correct date, not the current date. 


*  Postcodes/zip code fields on the checkout page are empty and unvalidated on page load as expected. Previously, Magento validated postcodes/zip codes on the checkout page when the page loaded.


*  Buttons on the  Admin **System** > **Backups** page no longer flicker when the page is reloaded.


*  Screen readers can now identify the `label` elements that are linked to  `input` fields for street address fields on the checkout page. Previously, screen readers could not identify these fields because the elements were not populated.


*  Product gallery images no longer open unexpectedly when you move over a product image while moving to another page element.


*  Magento now cancels previous scrolling actions as expected when you click **Add to cart** on a product page. Previously, Magento scrolled back to the `qty` input box the same number of times as you clicked  **Add to cart**.


*  Magento no longer displays the customer name twice in the welcome message on the log in page after a customer logs in.

*  Magento now updates the `created_at` and `updated_at` columns in the `ui_bookmark` table as expected.


*  Scrolling now works as expected in popup windows on devices running iOS.


*  Magento now displays warning messages when validation fails on a form field that has a validation rule associated with it. Previously,  Magento displayed this error: `Javascript Error: Uncaught TypeError: msg.replace is not a function`, if validation failed on a form field.

*  Magento no longer uploads images to the Category page unless the **Use Default Value** attribute is enabled. 

URL rewrites
~~~~~~~~~~~~

*  Added a feature to manage URL rewrites when the product visibility attribute changes. If the product is made invisible, Magento deletes the URL rewrite. If you change the visibility attribute to true, Magento creates a URL rewrite rule. Previously, changing the visibility attribute sometimes created duplicate product URLs. 


*  URLS in Arabic now resolve as expected. Previously, when you created a URL rewrite in Arabic, the browser returned a 404.


*  Magento now retains filter terms after you've applied a filter to the Admin `url_rewrites` table, then click the **Back** button. 

Web API framework
~~~~~~~~~~~~~~~~~

*  You can now use REST in scope `all` to save an existing category that does not have a `name` attribute. Previously, Magento threw this exception: `Could not save category with message. The "Name" attribute value is empty. Set the attribute and try again`. *Fix submitted by Nirav Patel in pull request [22362](https://github.com/magento/magento2/pull/22362)*. [GitHub-22309](https://github.com/magento/magento2/issues/22309)


*  The REST API locale now matches the appropriate store view in multistore deployments. Previously, Magento used the default scope for each store view.


*  You can now use `/rest/all/V1/products/`  to update a product's `category_ids` through `custom_attribute` when the product has no custom attributes. Previously, the `update` command reported success, but categories were not updated.


*  `PUT /V1/products/:sku/media/:entryId` now updates product images as expected. Previously, this call updated label, types and disabled, but the actual `file-content` was not replaced with the values that were provided in `base64_encoded_data`.

Wishlist
~~~~~~~~

*  Customer wishlists now include review summaries for included products.


*  The wishlist quantity field now has limits on both the type and number of characters that can be entered. Previously, you could enter both extremely large number and letters into this field, which resulted in undesirable, inaccurate changes in quantity.


*  Magento now alerts you to the expected minimum quantity of product when you try to add a lesser product quantity to your shopping cart from the wishlist.

WYSIWYG
~~~~~~~

*  You can now insert widgets that contain a WYSIWYG field into a form. Previously, widgets with a `WYSIWYG` parameter failed when inserting them into a WYSIWYG in a form.
