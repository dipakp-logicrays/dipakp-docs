Magento Open Source 2.3.3 Release Notes
=======================================

**Official link**: https://devdocs.magento.com/guides/v2.3/release-notes/release-notes-2-3-3-open-source.html


Patch code and release notes published on October 8, 2019 and last updated on June 3, 2020.

Magento Open Source 2.3.3 offers significant platform upgrades, substantial security changes, and PSD2-compliant core payment methods.

This release includes over 170 functional fixes to the core product and over 75 security enhancements. It includes over 200 contributions from our community members. These contributions range from minor clean-up of core code to significant enhancements to Inventory Management and GraphQL.

New security-only patch available
---------------------------------

* Merchants can now install time-sensitive security fixes without applying the hundreds of functional fixes and enhancements that a full quarterly release (for example, Magento 2.3.3) provides. Patch 2.3.2.2 (Composer package 2.3.2-p2) is a security-only patch that provides fixes for vulnerabilities that have been identified in our previous quarterly release, Magento 2.3.2.

* **If you have already upgraded to the pre-release version of this patch (2.3.2-p1), we strongly recommend that you upgrade to 2.3.2-p2 as soon as possible.**  Patch 2.3.2-p2 contains the critical security fixes that are included in Magento  2.3.3, 2.2.10, 1.9.4.3, and 1.14.4.3, but that are not included in patch 2.3.2-p1.


Other release information
-------------------------

Although code for these features is bundled with quarterly releases of the Magento core code, several of these projects (for example, Page Builder, Inventory Management, and Progressive Web Applications (PWA) Studio) are also released independently. Bug fixes for these projects are documented in separate, project-specific release information which is available in the documentation for each project.

Substantial security enhancements
---------------------------------

This release includes the following security enhancements:

*  PSD2 compliance to core payment methods
*  Fixes for 75 critical security issues
*  Significant platform-security enhancements that boost XSS (cross-site scripting) protection against future exploits. This effort is the culmination of several months of concentrated effort on Magento's part to reduce our backlog of security enhancements.

Core payment methods integrations are now compliant with PSD2 regulations
-------------------------------------------------------------------------

The European Union recently revised the Payment Services Directive (PSD) regulation with an updated version–PSD2. This revised regulation goes into effect on September 14, 2019, and will significantly affect  most payment processing involving credit cards or bank transfers.

This release contains the following major PSD-related changes:

*  The **Braintree payment method now complies with PSD2 regulations**. Its core integration API has been upgraded to the latest JavaScript SDK v3 API, which is a requirement for supporting native Braintree 3D Secure 2.0 adoption. Braintree transactions are now also verified by using the native Braintree 3D Secure 2.0 service.

*  Authorize.net now provides the ability, through the `cardholderAuthentication` request field, to make 3D Secure verification through third-party services such as CardinalCommerce. Starting with this release, **Authorize.net accept.js integration will support 3DS 2.0 through CardinalCommerce**.
*  The Cybersource and eWay payment modules have been deprecated in this release to comply with PSD2 SCA regulation, which takes effect on September 14, 2019. Use the official Marketplace extensions for these features instead.

Security enhancements and fixes to core code
---------------------------------------------

*  **75 security enhancements** that help close cross-site scripting (XSS) and remote code execution (RCE) vulnerabilities as well as other security issues. No confirmed attacks related to these issues have occurred to date. However, certain vulnerabilities can potentially be exploited to access customer information or take over administrator sessions.

Platform upgrades
-----------------

The following upgrades to core platform components boost platform security and support PCI compliance:


*  Magento 2.3.3 now supports **PHP 7.3.x (tested with PHP 7.3.8) and PHP 7.2.x (tested with 7.2.21)**.
*  Magento now supports **Varnish 6.2.0**.
*  Zend Framework 2 Components have been upgraded to the Active/LTS versions.

Performance boosts
------------------

*  Merchants now have the ability to turn off the automatic URL rewrite generation that occurs by default on products when the category they belong to is saved. The new **Generate "category/product" URL Rewrites**  configuration option controls this behavior. When this feature is enabled, Magento will generate a lot of data when saving a category that contains many assigned products. This generated data is saved into rewrite tables that can degrade Magento performance.
*  Page load speeds have been improved by moving non-critical CSS elements to the bottom of the page. This enables the browser to render and display a storefront page more quickly. This setting is disabled by default, but you can enable it using **Stores** > **Configuration** > **Advanced** > **Developer** > **CSS Settings** > **Use CSS critical path**.
*  The ``jQuery/ui`` library has been refactored into separate widgets so that core modules load only the widgets they need. This update improves the performance of core storefront tasks including the loading of category, configurable product, home, and checkout pages. We recommend that module developers update custom storefront code to remove the `jquery/ui` dependency. Otherwise, a performance degradation warning message might be displayed in the console.
*  Store pages now display text in readable system fonts while loading custom fonts, which significantly increases page load speed. Merchants who deploy stores that implement large CSS files and many fonts will notice the greatest improvement.

Infrastructure improvements
---------------------------

This release contains  enhancements to core quality, which improve the quality of the Framework and these modules: ``Catalog``, ``Sales``, ``Checkout/One Page Checkout``,  ``UrlRewrite``, ``Customer``, and ``Ui``. Here are some additional core enhancements:

*  The WYSIWYG editor has been upgraded to TinyMCE v. 4.9.5.

Merchant tool enhancements
--------------------------


As part of our efforts to better understand the Admin user experience and improve product design, Magento is introducing the tracking of user actions and events on the Admin. After you upgrade to Magento 2.3.3, the first administrative user who logs into the Admin will be prompted to **Allow admin usage data collection**. If the user agrees to data collection, the data captured from Admin activity is sent to Adobe Analytics for analysis and reporting. Typical events include page views, save actions, and changes to Magento mode. 

Inventory Management enhancements
---------------------------------

Fixes to multiple  bugs. See `Inventory Management release notes <https://devdocs.magento.com/guides/v2.3/inventory/release-notes.html>`_.

GraphQL
-------

Expanded GraphQL functionality and improved coverage for PayPal payment integrations, gift cards, and store credit features. Added mutations and queries that support these tasks:

*  Process payments through PayPal Express checkout, Payflow Pro and Link Express Checkout, and other supported PayPal payment methods, Authorize.net, and Braintree
*  Redeem gift cards and convert to store credit balance for logged-in users
*  Update shopping carts for guest users to apply or remove gift cards and check card balance
*  Add configurable products to cart


PWA Studio
----------

PWA Studio 4.0.0 contains new hooks in Peregrine. Existing components have also been refactored to convert them into re-useable Peregrine hooks. For information on these enhancements plus other improvements

Google Shopping ads Channel
---------------------------

The Google Shopping ads Channel Marketplace extension is now available as a bundled extension.

Magento Shipping
----------------

Due to the impending shutdown of Temando (the provider of the technology behind Magento Shipping), it is no longer possible to create a new Magento Shipping account. Support for current Magento Shipping deployments for all existing customers will continue. For detailed status information and recommendations for new shipping implementations in Magento, see our product information page.

This release of Magento Shipping includes:

*  Improvements to batch-order processing, carrier integration, shipping method preview in the shipping portal, checkout.
*  Support for bundled products and prepackage options.

Vendor-developed extension enhancements
---------------------------------------

This release of Magento includes extensions developed by third-party vendors. It introduces a new vendor-supplied extension–Yotpo.

Amazon Pay
----------

Amazon Pay is now compliant with the PSD2 directive for UK and Germany. See [Payment services (PSD 2) - Directive (EU)](https://ec.europa.eu/info/law/payment-services-psd-2-directive-eu-2015-2366_en) for an introduction to PSD2.

dotdigital
-----------

*  Improved product catalog sync for bundled and custom products.
*  Enhanced communications for abandoned cart.

Klarna
------

*  Merchants can now disable the sending of customer information.
*  New options now support B2B transactions in select markets.
*  PayBright, a Canadian payment coverage option, is now supported.

Vertex
-------

*  Added support for Vertex Flexible Fields. Vertex flexible fields allow merchants to send additional information to the tax engine, which  can then be used in Tax Assist Rules to refine a product’s applicable tax.
*  Several attributes are provided by default, including administrator-created Customer attributes, Address attributes, and Product attributes. Documentation is provided in the module’s README file on how integrators can add additional options to these attributes.
*  You can now add custom fields to the Vertex connector.

Yotpo
-----

The Yotpo user-generated content management platform is now integrated with the Admin. Yotpo provides tools for merchants to gather, curate, and manage user-generated content such as product reviews. For more information on configuring and launching Yotpo from the Admin, see Yotpo Product Reviews.

Fixed issues
------------

We've fixed hundreds of issues in the Magento 2.3.3 core code.

Installation, upgrade, deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


*  Magento font icons now load as expected when deployment optimization is implemented.
*  The short form versions of the `—lock-env`  and  `—lock-config`  `bin/magento config:set` options now work as expected.
*  Magento now displays an exception message when an error occurs during static content deployment.
*  You can now use JSON to  set a configuration value for a configuration option through the command line.
*  PHP unit tests no longer fail by default when Magento is installed from Composer.
*  Removed the  obsolete `system.xml` file from the `app/code/Magento/Theme/etc` directory.
*  Magento now displays a more informative message when a data patch cannot be applied due to an exception.
*  The static content deployment progress bar now works as expected.
*  The `setup:upgrade` command now throws an exception if the `app:config:import` command fails.
*  Fields that have been disabled through configuration settings (**Admin** > **Stores** > **Configuration** > **General** > **General** > **Store Information**) can no longer be overwritten from the Admin.
*  The Magento installation process no longer checks for `dev php` extension dependencies from non-root `composer.json` files.
*  Parallel execution of static content deployment has been improved to prevent errors and make it more stable.
*  Magento now runs an additional check when determining the password hashing algorithm to use for the libsodium library to see if it supports `argon2id`. The `bin/magento` command did not run successfully if the version of libsodium that you were running did not include `argon2id` support.

Backend
~~~~~~~

*  The Admin now loads without issue after you change the store domain or set cookies to a different domain. Previously, the page did not redirect as expected.
*  The Admin no longer displays incorrect currency codes when the default base currency differs from the default website currency.
*  The store view drop-down menu no longer displays unnecessary symbols.

Bundle products
~~~~~~~~~~~~~~~

*  You can now successfully check out bundle products using the Braintree payment method with the payment method set to **Authorize and Capture**.
*  Discount coupons now work as expected for bundle products that include both virtual and simple products when the **Ship Bundle Items** setting is set to **Separately**.

Cache
~~~~~

*  Varnish cache support has been upgraded for compatibility with version 6.2.0.
*  Full-page cache no longer clears out the checkout session data on uncached pages when the `Magento_Persistent` module is disabled.
*  Magento now displays simple products on the storefront after the cancellation of an order that contains the bundled simple product.
*  The Varnish health check no longer fails to the presence of `id_prefix` in `env.php`. Previously, Varnish returned a `503 Backend fetch failed` error.

Cart and checkout
~~~~~~~~~~~~~~~~~

*  The REST calls for adding an item to a cart (`POST V1/guest-carts/:cartId/items` and `POST V1/guest-carts/:cartId/items`) now include the product price when a call returns the product from an already populated cart.
*  Magento now submits an order only once when an order is submitted using **Enter**.
*  Products added to a shopping cart through REST now display correct product prices.
*  Magento now displays an informative message when an error is thrown after the user Internet connection has been reset after placing an order.
*  You can now add product quantities that require four digits to the shopping cart.
*  Administrators with appropriate permissions can now view the contents of a cart for a registered customer from the Admin customer edit interface.
*  Magento now applies the sort preferences that you set in website scope configuration for a particular website to the layout of the checkout page.
*  The Review & Payment section of the One Page Checkout no longer displays custom customer attribute code when a guest checks out.
*  The checkout order summary now displays the correct number of ordered items.
*  The minicart loader is now visible when you add a product to the minicart.
*  Magento no longer throws an array-to-string conversion error when a customer changes the country setting from one-page checkout. Instead, shipping method, tax values, and payment providers now change according to country selection.
*  Magento now validates the VAT number as expected during checkout when the customer address region field is empty.
*  Magento now creates an invoice for an order that has a zero subtotal when **Automatically Invoice All Items** is set to **yes**.

Cart Price rules
~~~~~~~~~~~~~~~~

*  Coupon codes now work as expected. Previously, coupons sent for specific dates in a cart price rule were not applied.

Catalog
~~~~~~~

*  You can now use the Select all option when creating a mass-update action when the total number of products exceeds the number of displayed products per page. Previously, Magento only selected and applied mass-update actions to the number of products that were displayed per page.
*  Magento no longer throws an error when you run the `php bin/magento catalog:images:resize` command on a  deployment that contains images with a zero byte size. Instead, the operation skips the offending file and updates the log file to indicate where the problematic file resides. [GitHub-8204](https://github.com/magento/magento2/issues/8204)
*  You can now successfully clone a product with a linked product. Previously, cloning  failed and Magento displayed this error:  `The linked products data is invalid. Verify the data and try again`.
*  Magento disables the **New Category** button on the Product page if the user is an administrator with restricted permissions for managing categories. Previously, the button was active, and Magento threw a 403 error if the restricted user clicked the button to create a category.
*  The Items Ordered table (**Admin** > **Sales** > **Orders**) no longer displays bundle option discount amounts with tags.
*  Magento now creates resized images for all products for which images exist and lists the errors when you run the `php bin/catalog:image:resize` command. Previously, execution halted at the first missing image.
*  You can now add a bundle product from a wishlist to your shopping cart.
*  The `\Magento\Catalog\Model\CategoryList::getList` operation now returns a sorted list of categories as expected.
*  The Admin Product Edit page and Customers page now load without JavaScript errors.
*  A duplicated product that has been set to **Is in Stock** and **Enabled** now appears as expected on the storefront.
*  Custom options prices that are assigned to a website scope no longer rewrite prices on all scopes.
*  Videos in product descriptions now appear as they do in the Admin WYSIWYG editor.
*  Sample data now scales correctly when resized in mobile view.
*  Customers no longer receive product alerts after they have unsubscribed from product alerts.
*  Magento no longer automatically assigns a `storeID` to a saved product that is not assigned to a store.
*  Corrected misspellings in the `lib/web/css/docs/source/_actions-toolbar.less` and  `lib/web/css/docs/source/_layout.less` files.
*  Magento now displays the currency code as expected in the Cost column of the Admin catalog product list.
*  The **Add to Cart** button is no longer visible to users who do not have Add to Cart category permissions.
*  We’ve refined how Magento validates partial permissions. Design edit permissions for categories, products, and CMS pages are now validated for each endpoint (web API and other) outside of the related model-layer classes. The web API now returns an error when design-related fields are being overridden.
*  Product availability is no longer tied to events associated with the categories to which they belong. Instead, Magento now uses the current category event for the page on which the product is displayed. Previously, products that were tied to categories with no events could be purchased, and products that were tied to expired events could not be purchased.
*  Magento now renames images with the same name in the `pub/media/catalog/category` directory.
*  Magento now displays a validation alert message when you click **Add Attribute**, and then click **Add selected** without first selecting an attribute.
*  The catalog products filter now filters on enabled or disabled status as expected.
*  `ProductRepository` now updates and saves existing products with changed SKUs as expected.
*  You can now change the position of the last two related products in a list of related products that spans multiple pages.
*  The **Select from gallery** button on the category edit page now works as expected.

CatalogInventory
~~~~~~~~~~~~~~~~


*  The status (in stock or out of stock) of a configurable product in the Admin now matches the status displayed on the storefront.
*  Magento now correctly updates the `qty_backordered` value in the  `sales_order_item` table after you create an order that contains a backordered item.
*  Stock status records for all products are now added as expected  to the `cataloginventory_stock_status` table after a partial re-indexing.

Catalog rule
~~~~~~~~~~~~


*  The CatalogRule module now handles discrepancies between the Magento time zone offset and the system time zone offset (which is in UTC). Previously, when the Magento time zone offset was greater than the system time zone offset, the active ranges set for special prices were inaccurate. This is a consequence of how  catalog price rules special prices are stored and updated. (Catalog price rules special prices are stored in the `catalogrule_product_price` table. This table’s daily update is triggered by the `catalogrule_apply_all` cron job, which is scheduled at 01:00 every day. Cron schedule times are scheduled in Magento timezone.)

Cleanup and simple code refactoring
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


*  Corrected poor positioning  of the Shop By menu on product pages in mobile view on an iPhone 5.
*  Corrected misalignment of Wishlist and Compare icons on the product page.
*  Store view-specific labels are no longer truncated in the left navigation menu of the Cart Price Rule Store View Specific Labels window (**Marketing** > **Cart Price rule** > **Labels** ).
*  Added missing header to the Customer Sales Order table and corrected multiple typos.
*  Improved awkward formatting of the customer account create page in mobile view.
*  The checkbox on the Add New Tax Rule form has been redesigned to match the Admin checkbox.
*  Corrected typo in CONTRIBUTING.md.
*  Corrected poor spacing in the Gift message section of the My Account page. 
*  The asterisk sign indicating a required field is now consistently positioned throughout the Admin. 
*  Corrected misspelling in the `app/code/Magento/Ui/Block/Wrapper.php` file.
*  Corrected typo in the tooltip toggle selector.
*  Corrected misalignment of the Compare Products and My Wish List counters in the sidebar.
*  Corrected scrolling behavior on Product page. Previously, after you clicked on a product reviews count on a product page, you had to scroll in order to see customer reviews.
*  Magento now displays the  cursor to the right of the search keyword box as expected after multiple clicks on the search field in mobile view.
*  Refactored the page title of the billing agreements page.
*  The Shop By Menu no longer overlays the **Sort By** label on the product listing page.
*  Adjusted the position of the store-view label on **Admin** > **Content** > **Design** > **Configuration** > **Theme**.
*  Fixed spacing issue on **Admin** > **System** > **Import**.
*  Fixed misspelling in the `app/code/Magento/Bundle/Block/Adminhtml/Catalog/Product/Edit/Tab/Attributes/Extend.php` file.
*  Removed unnecessary `<span>` element from the **Test connection** button.
*  The `lib/internal/Magento/Framework/Mview/View.php` file has been refactored to improve readability.

CMS content
~~~~~~~~~~~

*  Corrected alignment of the search suggestion panel with the **Advance reporting**  button.
*  You can now remove text that is placed adjacent to a TinyMCE4 widget.

Configurable products
~~~~~~~~~~~~~~~~~~~~~


*  Magento now validates the uniqueness of attribute option values during product creation.
*  The design of the tax rule form check box now matches the Admin checkbox design.
*  The configurable product gallery now displays images in the correct order when the image list has more than 10 images. The correct order complies with the order assigned in the Admin.
*  You can now use the `POST V1/configurable-products/:sku/child` call to assign positions to configurable product attributes as expected.
*  Setting the **Update Product Preview Image** to **no**  now works as expected. Previously, when you clicked on a size or image that represented  another variation for a configurable product, Magento displayed the image for one of the simple products associated with the configurable product.
*  The `POST V1/configurable-products/:sku/options` call now adds attribute options to a configurable product as expected. This resolves issues previously caused by the  MySQL table imposing a unique constraint on `product_id` and  `attribute_id` values.

Coupon
~~~~~~

*  The **Apply** button now functions as expected when you create a new order and apply a coupon from the Admin. Previously, clicking **Apply** removed the coupon instead of applying it. 

Cron
~~~~

*  Runtime exception handling for cron jobs has been improved. Now, when an exception occurs, the current run is marked as **failed** in the `cron_schedule`  table. Then, when the next run completes correctly, Magento updates job status at the end of the `cron_schedule` table. Previously, when a job failed, the `cron_schedule`  table was filled with pending jobs; the `indexer_update_all_views` job was not run; no output was sent to the `var/log/cron.log` file, and no status updates were appended to the `cron_schedule` table.
*  Cron jobs are no longer duplicated. Previously, after a cron job was run, Magento cleared the cache and processed the job again.
*  Consumers run from `cron` no longer create deadlocks in the database.
*  The `magento_newrelicreporting_cron` cron job now successfully completes as expected.

Customer
~~~~~~~~

*  Custom customer address attributes are populated with the values that have been assigned for the selected  address when the **Same As Billing Address** setting is disabled. Previously, when a merchant tried to change an address while creating an order from the Admin, the drop-down menu of available addresses was not populated.
*  The account status list now updates as expected to correctly indicate the account lock status after `cron` is run.
*  Import checks now finish successfully when the csv file contains a customer `gender` field.
*  Custom customer attributes are now always displayed in the Admin customer create and edit forms.
*  You can now create an order from the Admin when  you have a customer segment for customers with 0 or more orders.
*  You can now create an order from the Admin with a customer segment based on zero  or more orders and the table prefix is specified.
*  The **Phone Number** field is now marked as required on the My account page.
*  Magento no longer displays editable text fields for customer phone numbers and zip codes if customers have not saved an address.
*  Magento no longer duplicates the state/province fields of customer addresses in Admin forms.
*  Newly created customer accounts now require confirmation. Previously, Magento directly confirmed the new account even if the customer never logged in or confirmed the account.

Custom customer attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~

*  Custom customer address attribute values are populated as expected when an administrator changes a customer address during order creation from the Admin. Previously, the custom attribute drop-down was empty.


*  You can now edit a customer address from the Admin (**Admin** > **Customer** > **Address** > **Edit Address**) when the customer address attribute is of type `file` or `image`.

Database media storage
~~~~~~~~~~~~~~~~~~~~~~


*  The PDF logo file is now database-aware. Consequently, logo images always appear on PDF invoices, even after the local `pub/media` directory is cleared.


*  The `bin/magento catalog:images:resize` command is now database-media-storage-mode aware. As a result, resized images are now extracted from the database if they don’t exist locally prior to resizing, and are now stored back into the database once the resize operation completes. 

*  The  **use default value** checkbox on the Media Storage Location configuration setting has been removed.


*  Transactional email now copies the configured email logo image from the database when the logo file does not exist in the local `pub/media` directory.

*  Magento now copies any image needed for the Admin Product Edit page from the database to local storage as needed. Previously, if the image was not in local storage, Magento used a placeholder image.

Directory
~~~~~~~~~

*  The country drop-down list no longer includes an extraneous zero (0) when the allowed countries in the list differ from countries identified as top destinations. 

Downloadable products
~~~~~~~~~~~~~~~~~~~~~

*  Downloadable products are now immediately accessible after they have been paid for.

*  New downloadable products now appear in the downloadable products section after a customer checks out as a guest and then creates an account.

EAV
~~~

*  Starting and ending spaces are now trimmed from phone numbers before JavaScript validation.

*  You can now  save multiselect and select attribute options when swatches modules are disabled.

Email
~~~~~


*  Email created using a CSS-heavy template is now sent successfully.

*  The Template Preview tab now loads with the default content that was assigned during the creation of a New Shipment email template as expected.

*  All emails are now sent with correct MIME encoding. 

Frameworks
~~~~~~~~~~

*  Zend Framework 2 Components have been upgraded to the Active/LTS versions.


*  The `equalArrays` function in `lib/web/mage/utils/compare.js` file has been refactored to remove quadratic complexity.

*  The performance of resize image operations has been improved. 

*  The error message that Magento displays when the user creates an attribute that starts with the reserved word `container` has been improved. For example, when a user created product attributes named  `container_attributename` and `attributename`, Magento threw this error: `Exception in Magento/Framework/View/Element/UiComponentFactory.php` rather than stating which user behavior was causing the system problem.

*  The Magento Framework API now has a module manager to detect module features and support enablement of third-party modules. 


JavaScript framework
~~~~~~~~~~~~~~~~~~~~

*  The cursor on the email field of the login page now behaves as expected when running Magento on Safari.

*  Magento now displays previously missing validation messages on the storefront when JavaScript errors are caught by validation scripts in DatePicker form elements.

General fixes
~~~~~~~~~~~~~


*  Magento now displays the correct content for a selected store  in multi-site deployments where the websites have the same URL but the CMS pages have different content.

*  Enabling a product now clears the full-page cache for PDP if the product is not assigned to a category.

*  The **Save in address book** checkbox on the Shipping Address section of the Admin Create Order page now behaves as expected. When this checkbox is enabled, the address in the Shipping Address field is saved, and merchants can disable or enable the checkbox.

*  Updated the type and format for all `store_name` fields used in Sales and Quote modules. All fields are now type `text` instead of type `varchar`, and the field length has been extended to 255 symbols.

*  Preloading of fonts has been moved from the Blank theme to the Luma theme.

*  Magento no longer includes canceled orders when calculating how many times a coupon code has been used.

*  Code Sniffer no longer marks correctly aligned DocBlock elements as code style violations.

*  Tier prices can now be float values. Previously, Magento converted float percentage values to `int` before saving it.

*  Full page cache works as expected for non-default store views.

*  Magento no longer creates a persistent cart session for logged-in users when the persistent cart feature has been disabled.

*  The unused namespace import was removed from the  `CartTotalRepository.php` file.

*  The back-in-stock alert emails that Magento sends to both wholesale and general customers now include the appropriate  wholesale and general  product prices.

*  The `MsrpSampleData` module installation script no longer generates incorrect data.

*  Tooltips have been added to the store-view labels for CMS tables and blocks.

*  Validation of `max-word` data now works as expected for forms.

*  Magento now subscribes a customer to a price or stock notification when they opt to subscribe to a  price or  stock alert on a product page without first logging in. 

*  The sendfriend feature now verifies product visibility as expected.

*  Search input is no longer missing the `aria-expanded`  required attribute.

*  The **Use Default Value** check boxes on the Advanced Pricing  pop-up window  now remain checked on both the **Special From** and **Special To** dates,  and display the values set in the All Store scope.

*  The Recently Viewed feature now accurately lists the products and category paths that the user has recently visited.

*  The **Be the First to Review Product** link now directs the user to the product review form at the bottom of the product page as expected in deployments that include PageBuilder.

*  You can now set the **minute** values for Analytics data collection (**Store** > **Configuration** > **General** > **Advanced Reporting**).

*  The `getProductUrl()` method now returns the product URL for a specified website.

Image
~~~~~

*  You can now programmatically  move an image to the gallery using the  `addImageToMediaGallery` method with `$move`.

*  The performance of the `catalog:images:resize` command has been improved. This command now resizes only the images that are actually in use  and lists any  errors. 

Import/export
~~~~~~~~~~~~~

*  Import statistics now accurately reflect the results of import.

*  Magento now successfully saves product URL keys in Arabic.

*  Only modified or updated product records are flushed from the catalog cache after importing, re-indexing, and running `bin/magento cron:run --group index`.

*  You can now successfully download a CSV file after export.

*  Products are successfully updated through import of an CSV file in **Add/Update** mode.

*  Magento no longer throws a fatal error during import or export if the category path contains deleted category IDs.

*  The import process maintain custom option prices that were assigned to different websites and scope before import.

*  You can now update products through import of a CSV file when the updated products have `product_id` values that range widely (for example, a value 1 to a value 6000).

Index
~~~~~

*  We have improved the processing of memory tables in the Galera Cluster.

*  The pricing index can now be fully rebuilt and moved into the active price database table in a reasonable amount of time.

*  We improved the performance of product flat data re-indexing.

*  You can now filter administrative users by ID.

Infrastructure
~~~~~~~~~~~~~~


*  Magento 2.3.3 now supports PHP 7.3.x (tested with PHP 7.3.8) and PHP 7.2.x (tested with 7.2.21).

*  Varnish cache now supports version 6.2.0.

*  You can now use copy service on extension attributes for classes that extend Data Object.

*  Removed an extraneous closing tag from the store-switcher template.

*  `\Magento\ConfigurableProduct\Pricing\Price\PriceResolverInterface` has been added to the `di.xml` file.

*  We improved validation of forms that contain multiple fields with identical names.

*  Magento now identifies review entity IDs programmatically instead of retrieving a hard-coded value. 

*  The array type hints in the Visibility model now correctly reference `string` instead of `int`. 

*  The `getListByCustomerId` function in `PaymentTokenManagementInterface` now returns an array.

*  The description of the `setStoreId` function has been amended to more clearly explain how the function helps load CMS pages.

*  The `phpcs` script for PHP_CodeSniffer now displays all errors and warnings in the console.

*  The `oauth` handshake is now followed by a redirect as expected for third-party integrations.

Magento Shipping
~~~~~~~~~~~~~~~~

Due to the impending shutdown of Temando (the provider of the technology behind Magento Shipping), it is no longer possible to create a new Magento Shipping account. Support for current Magento Shipping deployments for all existing customers will continue. For detailed status information and recommendations for new shipping implementations in Magento, see our product information page.

Newsletter
~~~~~~~~~~

*  Magento now sends only a subscribe email when you create an account from an email invitation.

*  You can now export newsletter subscribers from the Admin.

Orders
~~~~~~

*  The creditmemo `getOrder()` method now returns the expected extension attributes for an order.

*  Magento now displays an informative error message when you try to update the product quantity and shipping address for an order when the product quantity field is empty.

Payment methods
~~~~~~~~~~~~~~~

This release includes the following changes to integrations for core payment methods to support compliance with PSD2 regulations:


*  The Braintree payment method now complies with PSD2 regulations. The core integration API for Braintree now supports the latest JavaScript SDK v3 API, which is a requirement for supporting native Braintree 3D Secure 2.0 adoption. Braintree transactions are now also verified by using the native Braintree 3D Secure 2.0 service.

*  Authorize.net now provides 3D Secure verification through third-party services through the `cardholderAuthentication` request field. Starting from this release, the Authorize.net `accept.js` integration will support 3DS 2.0 through CardinalCommerce.

*  The Cybersource and eWay payment modules have been deprecated in this release to comply with PSD2 SCA regulation, which takes effect on September 14, 2019. Use the official Marketplace extensions for these features instead.

Other payment issues
~~~~~~~~~~~~~~~~~~~~

*  Magento now displays a more informative error message (`CVV verification failed`) when you enter an invalid CVV code while using the Braintree payment method.

*  Customers can now successfully place an order when the order is partially paid for by gift card or when a discount is applied to the order.

*  When you create orders using Braintree, Magento now successfully creates the orders that contain both simple and virtual products with the **Checkout with Multiple Addresses** option enabled.

*  Magento no longer processes payment for an order that has an empty email field in the quote.

*  Customers can now place an order for virtual products that have a zero subtotal  after they have entered address information.

*  Magento now displays Chinese locale text strings for PayPal buttons as expected.

*  You can now cancel orders placed with PayPal Express even after authorization has expired.

*  The Transactions tab now displays the correct status for a capture transaction for an order that was placed with the Authorize.net `accept.js` payment method.

*  The Admin sales list now displays the payment method for each order.

*  Magento now displays stored payment methods and billing agreements if the related payment method is active.

*  Magento no longer saves credit card information when the  **Save for later use** checkbox on the payment page is not enabled during order creation.

*  When placing an order with Authorize.net, Magento now disables the Order page's **Place Order** button until billing information has been updated.

*  Magento now displays an informative email message about invalid credentials when a user tries to pay for an order with the Authorize.net payment method that has an incompletely configured Authorize.net `accept.js` account.

*  You can now place an order from the Admin using Authorize.net as the payment method.

*  The **Credentials** button on the Configure PayPal Express Checkout page (**Admin** > **Stores** > **Configuration**  > **Sales**  > **Payment Methods** > **PayPal Express Checkout**) is now displayed properly in modes.

*  Magento no longer throws an error when you place an order using a custom payment method in deployments running Signifyd.


*  Data type validation now occurs on data entered into the minimum and maximum order totals for all payment methods accessed under **Store** > **Configurations** > **Sales** > **Payment Method**.

*  The **PayPal Express Checkout** button now appears on the product details page only when the **Display on Product Details Page** and  **Enable Instant Purchase** configuration settings are enabled.

*  The location of the Zero Subtotal Checkout payment settings has been changed to **Stores** > **Configuration** > **Sales** > **Payment Methods**. 

*  Magento now displays the loading icon while processing a Braintree payment until the user is redirected to the new Order page.

Performance
~~~~~~~~~~~

*  Merchants now have the ability to turn off the automatic URL rewrite generation that occurs by default on products when the category they belong to is saved. The new **Generate "category/product" URL Rewrites**  configuration option controls this behavior. When this feature is enabled, Magento will generate a lot of data when saving a category that contains many assigned products. This generated data is saved into rewrite tables that can degrade Magento performance.


*  Page load speeds have been improved by moving non-critical CSS elements to the bottom of the page. This enables the browser to render and display a storefront page more quickly. This setting is disabled by default, but you can enable it using **Stores** > **Configuration** > **Advanced** > **Developer** > **CSS Settings** > **Use CSS critical path**.

*  The `jQuery/ui` library has been refactored into separate widgets so that core modules load only the widgets they need. This update improves the performance of core storefront tasks including the loading of category, configurable product, home, and checkout pages. We recommend that module developers update custom storefront code to remove the `jquery/ui` dependency. Otherwise, a performance degradation warning message might be displayed in the console.

*  Store pages now display text in readable system fonts while loading custom fonts, which significantly increases page load speed. Merchants who deploy stores that implement large CSS files and many fonts will notice the greatest improvement.

Pricing
~~~~~~~

*  You can now save a special price that exceeds three characters in Japanese Yen.

*  You can now set product price that exceeds 100,000,000.

Reports
~~~~~~~


*  The default date range for report filters is now set to the past month instead of the past 18 years.

*  The start and finish date in reports now correspond to the entered  values when you create a report from the Admin.

*  The access controls on the **Reports** > **Product** > **Downloads** page have been refactored to permit access to only administrators with the correct permissions. 

*  Selecting **Show by year** when filtering  **Reports** > **Products**  > **Ordered** now results in a list of products sold per year that is grouped by product quantity in descending order.

Reviews
~~~~~~~

*  Administrators with restricted privileges to reviews can now edit review status from the pending reviews list.

Sales
~~~~~

*  The Orders Total now reflects relevant product discounts when you re-order a product. Previously, discounts were not included when you re-ordered.

*  Custom order statuses no longer override default statuses in drop-down menus.

*  The Admin payment method validation now uses the updated billing address country for orders placed in the Admin. Previously, order creation failed when the **Payment from Applicable Countries** setting was set to **Specific Countries** and a non-US country was selected from the Payment from Specific Countries list.

*  You can now edit an order that contains a custom address attribute on its order form. Previously, Magento threw this error if you tried to edit an order with a custom address attribute: `We can't update the order address right now`.

*  You can now use quotation marks  to create exact search terms in the Admin menu search grid  (**Customers** > **All Customers**).

*  The date format used in tables throughout the product interface is now based on the Admin-defined locale.

*  Magento no longer lets you add a disabled variation of configurable product to the shopping cart from the Admin.

*  Magento now includes the correct price for a discounted product when the Customer Group is not set to the default group. Previously, when you re-ordered a discounted product, the correct price was not displayed in the Items Ordered field.

*  Magento no longer adds to an order any selected products that have not been explicitly added to the cart when you create an order from the Admin.

*  Magento no longer throws a fatal error when you click **View Order**  on an order that contains a product that was available when the order was created but that was subsequently  deleted from the storefront.

*  The Allowed Countries drop-down list that is available in multisite deployments now reflects the settings that  are configured in **Stores** > **Configuration** > **General** > **General** > **Country Options** > **Allow Countries**.

Search
~~~~~~


*  Search results now reflect the search weight that you assign to product attributes in attribute configuration.

*  Search by keyword now supports searching on zero (0).

*  You can now use Elasticsearch to run a query that includes the `<` character. Previously, when you used this symbol in a query, Magento threw this error: `{"0":"SQLSTATE[42000]: Syntax error or access violation: 1064 syntax error, unexpected $end, query was: SELECT`.

*  Disabled products now appear in the list of available products in the search results of the Page Builder link attribute–on buttons, images, banners, sliders. Previously, these products did not appear in search results, which prevented users from creating content that went live with a schedule update.

Shipping
~~~~~~~~

*  You can now use Cybersource as a payment method when multishipping is enabled. Previously, when you tried to place an order, Magento threw this error: `Invalid Form Key. Please refresh the page`. This resulted from a problem with auto-attaching a form key on the submit event  when one form contained another form.

*  The Order Tracking page now displays the Contact us link as expected  when this feature is enabled and the designated shipping carrier is not available on the Order page.

*  Magento no longer tries to validate UPS required fields (UPS Access License Number, User ID, and Password fields)  when UPS shipping is not active.

*  You can now use more than 35 characters in the shipper’s address field when booking a UPS shipment or generating a UPS shipment label.

*  Magento now validates values entered into the **quantity** field on the Shipping to Multiple Addresses page.

*  The updates that a customer makes to the shipping address during the checkout shipping step is maintained during the billing step.

Sitemap
~~~~~~~

*  Magento now generates all relevant product URLS when the **Use Categories Path for Product URLs** setting is enabled.

*  The sitemap product generation for the **Use Categories Path for Product URLs** setting has been refactored. ), [GitHub-4788](https://github.com/magento/magento2/issues/4788)

Swatches
~~~~~~~~

*  You can update the dropdown attributes (**Admin** > **Stores** > **Attributes** > **Product**) when swatches have been disabled. Previously, when swatches were disabled, Magento displayed this error in the console: `Uncaught TypeError: panel.addClass is not a function`.

*  The image gallery now correctly loads images for swatch colors. Previously, the gallery did not switch to the designated first image as expected.

Templates
~~~~~~~~~

*  The Insert Variables popup window is now populated with template variables as expected. (This window is accessed from **Marketing** > **Email Templates** > **Add New Template**.) 


Testing
~~~~~~~

*  The following tests have been improved:

   *  `CheckoutWithBraintreePaypalMinicartTest`
   *  `Magento\Catalog\Setup\Patch\Schema\ChangeTmpTablesEngine`
   *  `MAGETWO-69516: Cart Price Rule with related Banner for specific Customer Segment is persisted under long-term cookie`
   *  `Magento\FunctionalTestingFramework.functional.StorefrontUKCustomerCheckoutWithCouponTest`
   *  `Mftf Test: StorefrontApplyCategoryPermissionsToSecondWebsiteTest`


*  The Dependency static test now detects URL dependencies as expected.

*  `Magento.Framework.Image.Adapter.InterfaceTest.testValidateUploadFileException` with data set `image_empty` no longer fails on 2.3.3-develop.

*  `CommentLevelsSniff` now works correctly with the `@magento_import` statement.

*  Magento now deletes the stub modules that tests create. Previously, integration tests created stub modules in `app/code`, which could potentially affect production code.

Translation and locales
~~~~~~~~~~~~~~~~~~~~~~~

*  White space between words now appears as expected in non-English websites.

*  The payment method area of the shipment and credit memo emails that are sent to customers now have correctly translated strings.

UI
~~

*  The `jQuery/ui` library has been refactored into separate widgets so that core modules load only the widgets they need. This update improves the performance of core storefront tasks including the loading of category, configurable product, home, and checkout pages. We recommend that module developers update custom storefront code to remove the `jquery/ui` dependency. Otherwise, a performance degradation warning message might be displayed in the console.

*  The calendar date picker now updates values as expected when the linked input value is changed.

*  The URL rewrites category tree now includes all relevant categories.

*  Magento now saves order views with the date ranges you enter while creating the filter (**Sales** > **Orders**).

*  Form element validation is now triggered as expected when form validation rules change. Previously, when you changed form validation rules for a form element during runtime, the new validation rules were not applied.

*  The arrow toggle page element now works as expected throughout the Admin.

*  The height setting in `.admin__control-textarea` component is no longer hard-coded.

*  Added appropriate white space between elements of product descriptions on the product list view.

*  Scrolling now behaves as expected on the create order page.

*  Page element layout issues on  **Stores** > **Configuration** > **Advanced** > **Admin** have been resolved. Previously, when you expanded the security block on this page, the **Use system value** text appeared at the top of the page, not adjacent to the checkbox it applied to.

*  The missing **Update Totals**  button has been added to the Credit Memo page.

*  Magento now displays an error message as needed when you click the  **Catalog** > **Products** > **Create Configurations** button and submit invalid data. Previously, Magento did not display the error message after validation due to lack of autofocus on the error field.

*  The toggle icon on the **Catalog** > **Products** > **New Product (Configurable)** > **Create Configuration** page now works as expected.

*  Magento no longer validates data in the **Discount Amount** field after page load until the user performs an action in the Create New Catalog Rule form.

*  You can now edit the status label for the storefront from the Admin in single-store mode. Previously, there was no status field available from **Stores** > **Order Status** when single-store mode was enabled. *Fix submitted by Eden Duong in pull request [23681](https://github.com/magento/magento2/pull/23681)*. [GitHub-22654](https://github.com/magento/magento2/issues/22654)


*  The design of the Review & Payments **Apply Discount Coupon** box of the checkout page has been improved.
*  The `always` action that precedes the opening of the alert and confirm widgets is now called once.
*  Magento now sets the `last` CSS class to the top menu when one or more parent items are not active. As a result, menu items will be filtered before they are processed for HTML output. 
*  The form reset feature now clears the **date** field in Admin forms as expected.
*  You can now specify custom fonts for use in your deployment. Previously, the `.lib-font-face()` mixin required that you include the font in all the formats listed (for example, `eot`, `woff2`, `woff`, `ttf`, and `svg`). If your font was not available in these formats, Magento displayed a 404 error.
*  The **Refund** button on the credit memo page now remains active after a merchant enters a value in the Refund Totals section.
*  The behavior of the mobile menu JavaScript now triggers at the same breakpoint as the mobile menu styles.
*  The `font-size` setting for all `input-field` labels with a tooltip is no longer set to 0, and time fields are separated by colons (:) as expected. 
*  Magento now displays the Admin grid header as expected when there are no buttons in the toolbar.

URL rewrites
~~~~~~~~~~~~

*  Merchants now have the ability to turn off the automatic URL rewrite generation that occurs by default on products when the category they belong to is saved. The new **Generate "category/product" URL Rewrites**  configuration option controls this behavior. When this feature is enabled, Magento will generate a lot of data when saving a category that contains many assigned products. This generated data is saved into rewrite tables that can degrade Magento performance.
*  Redundant URL rewrite operations that were triggered by category operations have been eliminated, and page load performance has been improved.
*  Magento no longer removes the query string from URLs when the query string is preceded by a slash.
*  URL redirects now work as expected when you click **Save** after editing a product view from the Customer tab (**Customer** > **Product Reviews** > **Edit Review**). 
*  Magento now correctly renders the value of a product’s customizable option field of type `Area` when you enter a multi-line value from the Admin. Previously, a multi-line value was rendered with an HTML `<br>` tag as part of the value.
*  You can now use a plus sign (+) character in content contained within a widget on a CMS page.
*  Product URLs are now updated as expected after Magento changes the URL key of the category in multi-site deployment.

Vertex
~~~~~~

*  Incorrect Customer Codes are no longer sent when Vertex invoices are set to send during an order status change.
*  Resolved an issue where assisted parameters were not requested and logged during Invoice calls made during Order Status Change.
*  Calls to Vertex are now made when string values exceed the maximum allowed length in the Vertex SDK.
*  Tax code, vertex tax code, and invoice text codes are now saved for orders created during Guest Checkout.
*  Guest Orders are no longer invoiced twice if logging was enabled.
*  Shipping is now included on a Vertex invoice if that invoice was sent in the same request that its order was created in if that order was placed using guest checkout.

Web API framework
~~~~~~~~~~~~~~~~~

*  Magento now renders shipment details for an order without a fatal error when you use REST to create a shipment.
*  You can now use REST to update a customer that has no associated `store_id` without unintentionally changing other information. 
*  Swagger now accepts requests in XML and can display results in the same format.
*  The `POST` on `/orders` REST calls no longer fail when properties in the request body are out of order.

Wishlist
~~~~~~~~~

*  Wishlists now accurately reflect product availability when a product has been added to a wishlist and then subsequently disabled. Previously, the wishlist displayed these contradictory messages: **You have no items in your wish list** and **1 item in wish list**.
*  Wishlist names can now be edited from the storefront.
*  The wishlist no longer shows an item that has been disabled on the Admin.
*  Wishlist items now display decimal values as appropriate.