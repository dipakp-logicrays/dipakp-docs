Magento Open Source 2.3.5 Release Notes
=======================================

Magento Open Source 2.3.5 offers significant platform upgrades, substantial security changes, and performance improvements.

This release includes over 180 functional fixes to the core product and over 25 security enhancements.
It includes resolution of over 46 GitHub issues by our community members.
These community contributions range from minor clean-up of core code to significant enhancements to Inventory Management and GraphQL.

Download and run the updated Database Cleanup script
----------------------------------------------------

* This hotfix addresses an issue with a previous database clean-up script that was released in March 2020.
* That database cleanup script has been updated to clear pre-existing failed login data in additional database tables.
* **Magento recommend that all merchants run DB_CLEANUP_SCRIPT_v2 script to clear pre-existing failed login data in additional tables as soon as  possible**.
* See the `Remove failed login attempts from the database <https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/known-issues-patches-attached/remove-failed-login-attempts-from-the-database.html?lang=en>`_ support article.

Platform upgrades v2.3.5
------------------------

The following platform upgrades help enhance website security and performance:

* Elasticsearch 7.x is now the supported catalog search engine for both Adobe Commerce and Magento Open Source. 
* Magento Open Source 2.3.x supports only Elasticsearch 6.x and 7.x. Elasticsearch 2.x and 5.x are now deprecated for Magento Open Source 2.3.x and will be removed in Magento Open Source 2.4.0.
* With this release, the integrations of the Authorize.Net, eWay, CyberSource, and Worldpay payment methods are deprecated. These core features are no longer supported and will be removed in the next minor release (2.4.0).
* Deprecation of the core integration of the Signifyd fraud protection code. This core feature is no longer supported. Merchants should migrate to the `Signifyd Fraud & Chargeback Protection <https://marketplace.magento.com/signifyd-module-connect.html>`_ extension that is available on Commerce Marketplace.
* Upgrade of Symfony Components to the latest lifetime support version (4.4). 
* Migration of dependencies on Zend Framework to the `Laminas <https://getlaminas.org/about/foundation>`_ project to reflect the transitioning of Zend Framework to the Linux Foundation's Laminas Project.

Performance boosts
------------------

* Improvements to customer data section invalidation logic.
    - This release introduces a new way of invalidating all customer sections data that avoids a known issue with local storage when custom ``sections.xml`` invalidations are active. (Previously, private content (local storage) was not correctly populated when you had a custom ``etc/frontend/sections.xml`` with action invalidations.) 
    - See `Private content <https://devdocs.magento.com/guides/v2.3/extension-dev-guide/cache/page-caching/private-content.html#invalidate-private-content>`_.
* Multiple optimizations to Redis performance. The enhancements minimize the number of queries to Redis that are performed on each Magento request. 
    - Decrease in the size of network data transfers between Redis and Magento
    - Reduction in Redis consumption of CPU cycles by improving the adapter’s ability to automatically determine what needs to be loaded
    - Reduction in race conditions on Redis write operations

Infrastructure improvements
---------------------------

This release contains enhancements to core quality, which improve the quality of the Framework and these modules: Catalog, Sales, PayPal, Elasticsearch, Import, and CMS.

* The PayPal Pro payment method now works as expected in the Chrome 80 browser. 
* A PHPStan code analysis check has been integrated into Magento static builds.

Inventory Management
--------------------

Inventory Management enhancements for this release include:

* New extension point for ``SourceDataProvider`` and ``StockDataProvider``
* Ability to view allocated inventory sources from the Orders list
* See `Inventory Management release notes <https://experienceleague.adobe.com/docs/commerce-admin/inventory/release-notes.html>`_ for a more detailed discussion of recent GraphQL bug fixes.

GraphQL
-------

* With this release, you can now use ``products`` and ``categoryList`` queries to retrieve information about products and categories that have been added to a staged campaign.
* See `Using queries <https://devdocs.magento.com/guides/v2.3/graphql/queries/index.html#staging>`_ in the `GraphQL Developer Guide <https://devdocs.magento.com/guides/v2.3/graphql/>`_ for details.
* See `Release notes <https://devdocs.magento.com/guides/v2.3/graphql/release-notes.html>`_ for a more detailed discussion of recent GraphQL bug fixes.

PWA Studio
----------

PWA Studio 6.0.0 contains both new features and improvements to existing features:

* **Launch of the PWA extensibility framework**.  This framework gives developers the ability to create an extensibility API for their storefront or write plugins that can tap into those API and modify storefront logic.
* **Caching and data fetching improvements**. This release contains improved caching logic and other data fetching optimizations in the Peregrine and Venia UI component libraries. These components have been refactored to take advantage of Apollo cache features to reduce overfetching or prevent the storage of sensitive data.
* **Shopping cart components** that can be used for a full-page shopping cart experience
* For information on these enhancements plus other improvements, see `PWA Studio releases <https://github.com/magento/pwa-studio/releases>`_.

dotdigital
----------

This release includes:

* **Integration of Engagement cloud and Magento B2B**. A new B2B integration module integrates Engagement cloud and the Magento B2B module enable Magento B2B merchants to leverage their B2B commerce data and better engage with their prospective and existing customers. This will include:
   * Company data sync (customer type, company, company status)
   * Sync of shared catalog data. Syncing additional product catalog data (custom products and product attributes) to dotdigital. Merchants can turn additional product data into marketing campaigns or use it to make recommendations
   * Sync of quote data

* **Improved importer performance** and coupon code re-send.

Google Shopping ads Channel
---------------------------

* The Google Shopping ads Channel bundled extension has reached end-of-life with this release (2.3.5 and 2.3.4-p1).
* It is no longer supported. Alternative extensions are available on the Commerce Marketplace.

Fixed issues v2.3.5
-------------------

Magento have fixed hundreds of issues in the Magento 2.3.5 core code.

Installation, upgrade, deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* The link accessed from **Admin** > **Stores** > **Settings** > **Configuration** > **General** > **Advanced Reporting** now opens in a new tab as expected.
* You can now successfully remove a website along with the website’s scope-specific configuration settings in ``app/etc/config.php`` as expected.
* Configuration settings that are disabled in ``index.php`` are no longer editable from the Admin.

Adobe stock integration
~~~~~~~~~~~~~~~~~~~~~~~

* Image previews now close as expected when you navigate to a new page of search returns when searching Adobe Stock images.
* Image details are now hidden when you click on the image in the search result list.
* You can now use keyboard arrow keys to navigate to the next image in the preview.
* The **Search Stock Images** button now remains active as expected after you’ve searched for and saved an image from the media gallery.

Bundle products
~~~~~~~~~~~~~~~

* Bundle product prices are now calculated correctly on product pages.
* The performance of the ``catalog_product_price`` re-index operation for bundle products has been improved.
* Magento now correctly displays required field asterisks for products with custom options in the Admin.
* Clicking **Enter** in the **Shipping Price** field for Negotiable Quotes now correctly updates shipping price.
* Magento now displays the same price for a bundle product in the mini cart and on the product page.
* You can now add any number of bundle products to your shopping cart without error.
* Administrators can no longer manually enter a tax class in the Admin for a bundle product when  the bundle product’s **Tax Class** and **Dynamic Price** settings are disabled for the default store view.

Cache
~~~~~

* Frontend cookies are now set as expected when you enable **Use Secure URLs on Storefront** and **Secure Base URL** is set to **https**.

Cart and checkout
~~~~~~~~~~~~~~~~~

* Cart Price Rules that are based on payment methods are now applied during the checkout workflow.
* You can now disable zip code validation on the checkout workflow from the Admin as expected.
* The order review page in the checkout workflow now loads successfully for an order being shipped to multiple addresses when Terms and Conditions with the **Applied Manually** setting is enabled.

Catalog
~~~~~~~

* Filtering on the Admin product grid website column now works as expected.
* Magento no longer throws an error during checkout when the **Synchronize with Backend** configuration setting is enabled.
* Magento no longer throws an error when you change the name of a tiered product that is included in a scheduled update.
* The Recently Viewed Products feature now works as expected in multistore deployments.
* You can now successfully edit a configurable product with many variants (approximately 5,000) from the Admin.
* Sorting on attribute sets on  **Admin** > **Catalog** > **Products** is now based on alphabetical order as expected.
* Custom attribute values can now be saved as expected from the Admin.
* Corrected an issue that caused the PUT ``/V1/products/:sku/media/:entryId`` call to create a new entry rather than replace the existing one.
* Customizable options are now imported as expected when ``row_id`` is not equal to a product's ``entity_id``.
* You can now assign a default watermark to a theme. 
* Magento now displays product images in the mini cart without distortion. 
* The Recently Viewed Products feature now shows products associated only with the current store view in multi-store deployments when **Stores** > **Configurations** > **Catalog** > **Recently Viewed/Compared Products** > **Show for Current** is set to **store view**. 
* The product compare feature now works as expected. It displays only products in the current user’s compare list.
* Problems with the partial re-indexing of large categories have been resolved. Previously, due to problems with this process, products were randomly excluded from categories on the storefront.
* The ``getBasePrice`` function now returns a float value  as expected rather than a string.
* Images are now saved in ``pub/media/catalog/category`` as expected when you save category images.
* Administrators with restricted permissions to Catalog can now create a downloadable product.
* You can now add a configurable product to the cart from the Cross-Sells tab. When you select a product and click **Add to Cart** from this tab, you are now taken to the product’s details page, where you can select specific product options.
* You can now add a child product of a grouped product to your cart when one of the grouped product’s other child products is out-of-stock. 

CatalogInventory
~~~~~~~~~~~~~~~~

* Magento now displays appropriate feedback when you unsuccessfully attempt to update and save a product.

Catalog Price Rule
~~~~~~~~~~~~~~~~~~

* The mini cart and Admin shopping cart (**Admin** > **Customers** > **Manage Shopping Cart**) now display correct product prices when a Catalog Price Rule is applied. 
* Product prices on the storefront now accurately reflect the application of a scheduled Catalog Price Rule update.

Catalog widget
~~~~~~~~~~~~~~

* Magento now displays all children of a selected parent category as expected. Previously, if you selected a parent category that is an anchor, but which did not have assigned products by itself, Magento did not display all nested products.
* The CatalogWidget products list now works as expected with anchor categories, and products from anchor categories are now matched and displayed.

Cleanup and simple code refactoring
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Corrected misalignment of the **View Details** label for configurable products in the order summary of the checkout workflow.
* Added a ``margin-bottom`` value to the static CMS block widget in the Checkout/Cart Summary of the checkout workflow in the Luma and Blank themes.
* Added a margin between the checkbox and icon when choosing a category during the process of  assigning a condition to a new Cart Price Rule.  
* Rating stars no longer overlay the product over which your mouse hovers on the category page. 
* Corrected misalignment of the calendar icon inside the textbox on the Add Design Change page.
* Deleted unused variable (``time_taken``) from the ``Magento/Catalog/view/frontend/templates/product/listing.phtml`` template.

CMS content
~~~~~~~~~~~

* Select from Gallery image thumbnails are now cached as expected.
* Magento now lets you create CMS blocks with identical names if the blocks are assigned to different store views.

Configurable products
~~~~~~~~~~~~~~~~~~~~~

* Added validation logic to the **Create new value** input field of the configurable product creation workflow.
* Magento now displays all attributes of a configurable product. 
* Catalog Products List widgets can now process conditions that include product ``test_date`` attributes.

Cron
~~~~

* ``bin/magento cron:run -v`` no longer fails when the database name exceeds 64 characters but instead creates a shorter name.
* We’ve improved the reliability of background ``cron`` execution. We now use the Magento Lock Framework to lock ``cron`` jobs.

Custom customer attribute
~~~~~~~~~~~~~~~~~~~~~~~~~

* Magento now displays custom customer address attribute values as expected in the address section of the checkout workflow.

Customer
~~~~~~~~

* You can now save a **Gender** field with a blank value when directly editing customer information from the Customer list.
* The steps involved in ``x-magento-init`` initialization now happen in the correct order: RequireJS loads ``section-config.js``, and ``section-config.js`` constructs and initiates itself as required.
* Magento now honors a customer’s default shipping address.
* You can now successfully create a customer and associate it with a particular website using the **Associate to Website** dropdown menu  on **Customers** > **All Customers** >  **Add new Customer**.

EAV
~~~

* The Update Attribute action now correctly updates the timestamp of a product’s ``updated_at column`` from ``catalog_product_entity`` when you update the product from the Admin edit product page.
* Magento now respects store-specific settings that determine whether the telephone number field of the checkout workflow is required in a multi-site deployment.

Email
~~~~~

* Email templates (**Admin** > **Marketing** > **Communications** > **Email Templates**) can now be previewed from the Admin when JavaScript magnification is enabled.
* The order notification emails sent from Microsoft Outlook now contain content that is rendered as expected from the assigned email template.

Frameworks
~~~~~~~~~~

* Dependencies on Zend Framework have been migrated to the `Laminas project <https://getlaminas.org/about/foundation>`_ to reflect the transitioning of Zend Framework to the Linux Foundation’s Laminas Project. Zend Framework has been deprecated.
* Editing products in the Admin no longer triggers Redis errors.
* ``php bin/magento cron:run`` no longer processes items from the change log table multiple times.
* Watermark images no longer obscure the product image that they overlay.
* Non-cacheable blocks are no longer added to default layout handles. Adding non-cacheable blocks to default layout handlers renders all Magento pages non-cacheable. This results from the layout generation process:  During layout generation, Magento collects all available layout handles for a particular page and merges instructions from them into the page’s final layout structure. The default layout handle is used as a basic handle for every page. As a result,  layout updates that are declared for the default handler appear on every Magento page.
* Setting ``'persistent' => '1'`` in ``env.php`` no longer throws an error when you run ``setup:upgrade``.
* Magento no longer downloads a ``blank.html`` page when an administrator clicks on a product while creating an order from the Admin.
* The ``RequireJS domReady!`` plugin has been improved to prevent artificial delays when loading a storefront page.

JavaScript framework
~~~~~~~~~~~~~~~~~~~~

* Added a check to confirm that a file belongs to the current base URL before setting the ``.min.js`` suffix.
* JavaScript errors no longer occur on the shopping cart/mini cart page when the cart contains a configurable product. 
* Clicking the **Refund Offline** button in the create a credit memo workflow now generates a credit memo as expected.

General fixes
~~~~~~~~~~~~~

* Comments entered by a customer on the storefront Returns page are now successfully attributed to the correct customer.
* All HTML tags are now supported by the TinyMCE4 editor.
* Magento now displays an informative error message and continues to display the registration form as expected if an error occurs when a customer tries to complete a registration form that contains a multi-select customer attribute.
* The stock alert email sent to customers about the re-stocking of a configurable product now contains the correct product price.
* You can now delete an empty user model without deleting the Administrators role to which it is assigned.
* The ``.fotorama__thumb__arr`` arrows adjacent to the thumbnail images on the product gallery now work as expected.
* You can now accurately manipulate a zoomed image using your mouse. 
* LESS styling for the ``Magento_Contact`` and ``Magento_Cms`` modules has been moved to the correct ``design`` directory. This change brings these modules into alignment with the organization of other modules, none of which include any LESS styling.
* Credit memos for orders with 100% discount (including shipping fees) now correctly include a 0 for the **Grand Total**.
* A store’s Admin URL no longer redirects to the storefront URL when these two URLs differ.
* The graphical orders chart accessible from the Orders tab on the Admin now accurately reflects order quantity.
* Product price change alert email now includes the correct product price. 
* You can now save and duplicate all CMS pages.
* Magento now redirects you to the home page of the appropriate store view when you change language on CMS pages in a multistore deployment.

Import/export
~~~~~~~~~~~~~

* Magento now successfully imports customer data  using the **Customer and Addresses (single file))** option when ``cron`` is enabled and the Customer Grid Indexer is set to **Update By Schedule**.  After ``cron`` executes, the imported customer information is available in the Admin as expected.
* Magento now updates images as expected when you use the ``hide_from_product_page`` setting when importing products in deployments with multiple store views.
* Magento now deletes temporary files from ``<Magento_home>/var`` as expected after product import has completed.
* Magento now removes related, up-sell, and cross-sell products as expected in the import ``.csv`` file when you set the value of the **Empty attribute value constant** field to `_EMPTYVALUE_` for products in **System** > **Import**.
* Magento now displays a more informative error message, and does not display a download link, when you try to delete a directory from the **System** > **Export** list. 
* The CSV file used during import now contains the correct links for downloadable products and is now correctly formatted to support importing and updating downloadable products.
* The Stock Indexer is now triggered as expected after import and updates product status. 
* Images associated with configurable products are now properly uploaded during import and available for viewing as expected from the product edit page.
* Magento now provides a message during product import that identifies which products in the imported CSV file have duplicated keys. Merchants can use this information to resolve conflicts.
* Magento now successfully exports a ``.csv`` file when you set import behavior for Replace, select a previously exported ``.csv`` file, and click **Check data**.
* You can now successfully import a product that does not have a ``store_view_code`` value.
* The import of customer accounts has been refactored to improve import speed.
* CSV files generated during product import now contain group titles for downloadable products as expected.
* You can now successfully import or update customers using the Customer and addresses single file option of the import workflow. 
* Magento now successfully imports all custom options for a configurable product’s child products  when ``store_view_code`` is specified. This works whether you choose to import configurable products individually or collectively. 
* Exported ``.csv`` files now reflect filter settings for including in-stock or out-of-stock products.

Index
~~~~~

* The partial indexer no longer incorrectly removes stock data when updating at least 1000 products.

Infrastructure
~~~~~~~~~~~~~~

* Elasticsearch 7.5 is now the supported catalog search engine for both Adobe Commerce and Magento Open Source. With this release, Magento Open Source 2.3.x supports only Elasticsearch 6.x and 7.x. Elasticsearch 2.x and 5.x are now deprecated for Magento Open Source 2.3.x and will be removed in Magento Open Source 2.4.0.
* Symfony Components have been upgraded to the latest lifetime support version (4.4).
* Corrected the argument type of the email address constructor
* Admin route names can now contain a hyphen in the URL.
* The condition of the shipping method title output in ``Magento_Checkout/js/view/summary/shipping`` has been corrected.

Inventory
~~~~~~~~~

* You can now create an offline credit memo.
* Product widgets with product filter set to **Attribute Set** now work as expected on both the Admin and storefront.
* Customers can no longer check out  when their order contains more products than are currently in stock.

Newsletter
~~~~~~~~~~

* The preview template feature now works as expected.

Payment methods
~~~~~~~~~~~~~~~

* The integration of third-party payment methods into the core Magento code has been deprecated. With this release, the integrations of the Authorize.Net, eWay, CyberSource, and Worldpay payment methods are deprecated. These core features are no longer supported and will be removed in the next minor release (2.4.0). Merchants should migrate to the official extensions that are available on the Commerce Marketplace.
* You can now successfully complete an order using the Payflow Link payment method. 
* The core implementation of Signifyd fraud protection is no longer supported.
* The **Place Order** button on the shipping workflow is now enabled as expected when you select Braintree as the payment method and the **My billing and shipping address are the same** setting is disabled.
* You can now create an order from the Admin using Authorize.net as the payment method. 
* The WorldPay payment integration with the Magento core has been deprecated. Please use the official Marketplace extension instead.
* The **Place order** button on the checkout workflow is now disabled as expected until the customer updates the billing address when paying with Braintree.
* The PayPal Pro payment method now works as expected in the Chrome 80 browser. This payment method previously invoked a Magento callback endpoint that needed access to the customer’s session — access that the new default Chrome SameSite cookie functionality does not permit.
* Magento now successfully processes orders placed with PayPal Express Checkout where the order’s shipping address specifies a country region that the customer has manually entered into the text field rather than selected from the drop-down menu on the Shipping page.
* Magento now displays an informative error message each time a customer clicks **Pay with PayPal** after entering an invalid shipping address in the checkout workflow.
* Magento no longer changes an order’s status to **processing** in the Payment Review section of the checkout workflow when a payment with PayPal fails.
* Magento now saves the information a customer enters in the default billing and shipping fields during checkout when the transaction is initially declined due to an invalid credit card but later completed successfully.

Reviews
~~~~~~~

* Magento now disables the **Submit Review** button after the user clicks the button once.

* The **Admin** > **Reports** > **Reviews** > **By Products** filter list now displays results as expected.

Sales
~~~~~

* Order queries (``SalesOrderIndexGridAsyncInsertCron``) have been refactored to reduce the size of the dataset returned and the frequency of the queries.
* The **State/Province** field of the edit order page is now of type `Dropdown`.
* The **State/Province** field of the Billing Address section of the checkout workflow is now of type `Dropdown` in multi-site deployments where the default store has country restrictions.
* You can now successfully add a product in quantities exceeding five to an order from the Admin.
* Completed orders now appear in both the payment system and Magento.

Sales Rule
~~~~~~~~~~

* ``quote_item.applied_rule_ids`` is now updated as expected after a cart price rule is disabled.
* Cart Price rules with a **condition set as Category (Parent only)** now work as expected consistently.

Search
~~~~~~

* Filtering results no longer include out-of-stock options when you filter configurable products in a category.
* Selecting all products from the products list page using Elasticsearch now displays all products in the search results as expected. 
* Elasticsearch now works as expected when you sort a product list that contains bundle products by alphabetized product names.
* Magento now renders the **<** and **>** symbols correctly in storefront catalog search strings.
* Magento now passes  product attribute filters as an ``array`` (instead of a ``string``) to ``strpos()``, which results in the proper display of the product list and layered navigation results.
* Elasticsearch now correctly displays results from category pages when you change the number of search results viewed per page.

Shipping
~~~~~~~~

* Magento now prints shipping labels as a ``.pdf`` file as expected when you select **Print Shipping Label** from the Action drop-down list from an order in the order archive list.
* The incorrect initial option values for the DHL shipping method have been corrected, and this shipping method now works as expected when enabled.
* The multishipping page of the checkout workflow now correctly displays discounted shipping prices when discounts are determined by a Cart Price rule.
* Magento now correctly calculates refunds for orders that include discounts.
* Support for Colombia regions has been added, and these regions are now available from the shipping and billing country dropdown menus in the checkout workflow.
* The drop-down list that is available for selecting shipping methods during the process of creating a Cart Price Rule now contains only valid values.
* Free Shipping Price rules now affect only the relevant products when a shopping cart contains products from categories that are included by the Free Shipping Price rule as well as products from categories not included in the rule. 

Sitemap
~~~~~~~

* The partial sitemaps that are listed in the sitemap index now have the correct URL (for example, ``storeurl/pub/sitemap-1-1.xml``).
* Magento now uses the project base URL as expected when you generate a sitemap.
* ``sitemap.xml`` (generated from **Marketing** >  **SEO & Search** >  **Site Map**)  now includes the URL of the homepage.

Store
~~~~~

* Customer sessions now persist as expected when a customer logs in to one store, adds products to the shopping cart, and then switches to a new store in a multi-store deployment.
* Magento now redirects you to the correct product details page when you switch store view while on a product page in a multistore deployment. 

Swagger
~~~~~~~

* Magento now longer displays an informative console error when you try to navigate to the Swagger index page.

Swatches
~~~~~~~~

* Merchants can now successfully add color swatch attributes to products using the **Visual Swatch** option on **Stores** > **Attributes** > **Product** > **New Attribute**.

Tax
~~~

* Magento now performs VAT calculations correctly in all stores in a multistore deployment.
* Magento now updates shipping rates and prices as expected when a customer changes the destination country for an order during checkout.
* Free shipping is now applied as expected based on the applicable cart price rule.

Testing
~~~~~~~

* A PHPStan code analysis check has been integrated into Magento static builds.
* This tool performs sophisticated static code analysis and identifies additional issues that are currently not detected by PHP CodeSniffer and PHP Mess Detector. 
* See `Magento Testing Guide <https://devdocs.magento.com/guides/v2.3/test/testing.html>`_.

Theme
~~~~~

* Product names are no longer translated if their text matches a global key.
* We’ve resolved a bug in ``JsFooterPlugin.php`` that affected the display of dynamic blocks.

Translation and locales
~~~~~~~~~~~~~~~~~~~~~~~

* Special price range settings (from/to dates) now work correctly for administrator accounts using a Dutch locale.
* Inline translation now works as expected when enabled for a storefront.

UI
~~~

* Radio buttons for shipping methods are now enabled as expected in the checkout workflow.
* The product edit page now loads successfully when the default attribute set for the page contains a dropdown attribute with the select label.
* You can now scroll as expected to the top of the Admin Import page.
* Watermark size now remains consistent with the image to which it has been applied when you resize the image.
* Magento now correctly renders the **Read more ...** page element that is associated with a product that has an ``additionalOption`` value that exceeds 55 characters on the storefront shipment and invoice pages.
* Corrected the position of the wishlist item **Delete** button on the category page.
* Magento now displays a **N/A** where needed on the product compare list page.
* Magento now displays the dropdown icon as expected when you click **Load template** during the creation of a new email template from the Admin. 
* Magento now retains the correct aspect ratio when a store icon is resized for mobile display.
* The focus function on the fourth level of a multi-level navigation menu now works consistently.
* Magento now displays the correct error message in the confirmation popup dialog when you delete a customer group.
* Accordion widgets placed in tab widgets now work as intended.
* Corrected the CSS-defined color for the **Minimum Quantity allowed in Shopping Cart** field of the **Admin** > **Store** > **Configuration** > **Inventory** page. 
* Logo images that are being uploaded into the Admin are now displayed with its native dimensions if no width and height parameters are explicitly set.
* Magento have reverted a previous fix (https://github.com/magento/magento2/pull/25309) that had introduced a change to global styles that had the unintended consequence of breaking styles through the storefront.

URL rewrites
~~~~~~~~~~~~

* Customers who change language on a CMS page can now successfully navigate to the store view they’ve selected.
* You can now save a category that contains many products (for example, 140000).

Web API framework
~~~~~~~~~~~~~~~~~

* Corrected issues with the POST ``/rest/default/async/bulk/V1/orders`` calls.
* Corrected issues with the POST ``/rest/default/async/bulk/V1/products`` calls.
* Child products of a configurable product can now be successfully disabled through the API.

Wishlist
~~~~~~~~

* A wishlist now works as expected when it is enabled at the store-view level and disabled at the global level.

WYSIWYG
~~~~~~~

* The WYSIWYG editor now works as expected on Internet Explorer 11.x.
* Magento can now successfully display two or more WYSIWYG editors on a catalog product edit page.
* The WYSIWYG editor no longer hangs indefinitely when you try to upload an image from the Admin.
