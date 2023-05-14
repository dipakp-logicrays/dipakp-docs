Magento Open Source 2.3.4 Release Notes
=======================================

**Official link**: https://devdocs.magento.com/guides/v2.3/release-notes/release-notes-2-3-4-open-source.html

Magento Open Source 2.3.4 offers significant platform upgrades, substantial security changes, and PSD2-compliant core payment methods.

This release includes over 220 functional fixes to the core product and over 30 security enhancements.
It includes resolution of over 275 contributions by our community members.
These community contributions range from minor clean-up of core code to significant enhancements to Inventory Management and GraphQL.

Platform upgrades v2.3.4
------------------------

The following platform upgrades help enhance website security and PCI compliance.

* **Enhancements to the message queue framework**. Magento now supports the latest release of ``RabbitMQ v3.8``, which is the third-party technology that underlies the Magento message queue framework.

* **Improved page caching and session storage**. This release has been tested on the latest stable release of ``Redis v5.0.6``.

* **Enhanced support for MariaDB 10.2**. Before Magento 2.3.4, when using declarative schema with MariaDB 10.2, Magento threw an error indicating that the schema was not up-to-date after running bin/magento setup:upgrade. With this release, we have normalized the values returned by MariaDB, which allows system integrators to use declarative schema with both MySQL and MariaDB.

* The core integration of the Authorize.net payment method has been deprecated. Please use the official payment integration that is available on Marketplace.

.. note::

    Note: Magento 2.3.4 has not been tested with PHP 7.1. PHP 7.1 reached EOL (End of Life) on December 1, 2019. We recommend updating your deployment to a supported version of PHP. See `Magento 2.3 technology stack requirements <https://devdocs.magento.com/guides/v2.3/install-gde/system-requirements.html>`_ for information about supported versions.


Performance boosts
------------------

Merchants and customers will see performance improvements as a result of these enhancements:

* Redundant non-cached requests to the server on catalog pages have been eliminated by refactoring the customer section invalidation mechanism and improving banner cache logic.
* PHTML files have been refactored to better support parsing by the bundling mechanism. Our new bundling mechanism now identifies all dependencies on JavaScript.
* Added the ability to disable statistic collecting for Reports module by default. A new configuration setting (**System Configuration** > **General** > **Reports** > **General Options**)  allows merchants to completely or partially disable Magento Reports. (Statistics collection for the Reports module is disabled by default. Magento recommend disabling Reports functionality for performance reasons when this capability is not required.)

Infrastructure improvements
---------------------------

* This release contains 250 enhancements to core quality, which improve the quality of the Framework and these modules:  catalog, sales, PayPal, Elasticsearch, import, and CMS.

Merchant tool enhancements
--------------------------

* **Integration with Adobe Stock image galleries**.
* The new bundled Adobe stock integration extension enables merchants to add high quality media assets to their website content without leaving the Admin.
* Merchants can use the searchable interface in the Magento Media Gallery to explore, preview, license, and deploy stock images in website content.
* See `Adobe Stock Integration <https://docs.magento.com/m2/ee/user_guide/cms/adobe-stock.html>`_ and `Using Adobe Stock Images <https://docs.magento.com/m2/ee/user_guide/cms/adobe-stock-manage.html>`_.

Inventory Management
--------------------

Inventory Management enhancements for this release include:

* Addressed a known performance issue that caused higher than expected loads on the database server in scenarios involving the shopping cart.
* Updated the Inventory Reservations CLI command to reduce memory usage when finding and compensating for missing reservations on large catalogs.
* Resolved multiple quality issues, including those related to credit memos, grouped products, source and stock mass actions.
* See `Inventory Management release notes <https://experienceleague.adobe.com/docs/commerce-admin/inventory/release-notes.html>`_ for a more detailed discussion of recent Inventory bug fixes.

GraphQL
-------

This release includes improved GraphQL coverage for search, layered navigation, cart functionality. The following mutations/queries are available:

* **Guest carts can now be merged with customer carts.** The `mergeCarts <https://devdocs.magento.com/guides/v2.3/graphql/mutations/merge-carts.html>`_ mutation transfers the contents of a guest cart into the cart of a logged-in customer.
* **A customer can start an order on one device and complete it on another.** Use the `customerCart <https://devdocs.magento.com/guides/v2.3/graphql/queries/customer-cart.html>`_ query to obtain the cart ID for a logged-in customer.
* **Layered navigation can use custom filters.** The `filter` attribute of the `products <https://devdocs.magento.com/guides/v2.3/graphql/queries/products.html>`_ query now requires the `ProductAttributeFilterInput` object. You can specify a pre-defined filter in this object, or `define a custom filter <https://devdocs.magento.com/guides/v2.3/graphql/custom-filters.html>`_. As a result, layered navigation on your website filters on the attributes you need.
* **You can search categories by ID, name, and/or URL key.** The `categoryList <https://devdocs.magento.com/guides/v2.3/graphql/queries/category-list.html>`_ query replaces the deprecated `category` query.
* **The `ProductInterface <https://devdocs.magento.com/guides/v2.3/graphql/interfaces/product-interface.html>`_ supports fixed product taxes (such as WEEE).** Use the `storeConfig <https://devdocs.magento.com/guides/v2.3/graphql/queries/store-config.html>`_ query to determine whether to store supports these taxes.
* **The `cart <https://devdocs.magento.com/guides/v2.3/graphql/queries/cart.html>`_ object has been enhanced to include information about promotions and applied discounts at the line and cart levels.**

See `Release notes <https://devdocs.magento.com/guides/v2.3/graphql/release-notes.html>`_ for a more detailed discussion of recent GraphQL bug fixes.


PWA Studio
----------

* Improved the getting-started experience through the use of ``@magento/create-pwa`` to scaffold your initial project using Venia as your template
* Separation of the logic (Talons) and presentation pieces (``venia-ui``) of certain React hooks in Peregrine. Developers can now swap out either the logic or the presentation side of a component
* Routing is now handled through the React Router (library of navigational components)
* Refactored Venia `state management <https://developer.adobe.com/commerce/pwa-studio/guides/general-concepts/state-management/>`_ to abstract and reduce dependency on Redux
* Continued migration from REST to GraphQL
* Performance improvements (service workers, cache, image optimization)
* Breadcrumbs for improved storefront navigation

For information on these enhancements plus other improvements, see `PWA Studio releases <https://github.com/magento/pwa-studio/releases>`_

dotdigital
----------

* Live Chat powered by dotdigital enables merchants to increase conversion rates, and keep customers coming back with real-time engagement. All Magento 2.3.x merchants (both Magento Open Source and Adobe Commerce) can receive a free live chat agent without the need for a full dotdigital Engagement Cloud license.
* Engagement Cloud includes a new Chat widget that makes it easy for shoppers to communicate in real time with customers as they shop in your store. Chat can be accessed from the Engagement Cloud section of the Magento configuration, or directly from your Engagement Cloud account. See `Engagement Cloud Chat <https://docs.magento.com/m2/ee/user_guide/marketing/engagement-cloud-chat.html>`_.
* Merchants can now sync additional campaigns from Engagement Cloud to Magento.

Fixed issues
------------

Magento have fixed hundreds of issues in the Magento 2.3.4 core code.

Installation, upgrade, deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Upgrades no longer fail when deployments contain store information predefined in ``app/etc/config.php``.
* The ``setup:db-declaration:generate-patch`` command now generates a patch file using the ``revert()`` method as expected when the  `--revertable` option is set to **true**.
* You can now run ``bin/magento maintenance:enable`` or ``bin/magento maintenance:disable`` on a deployment with an empty database. 
* In rare circumstances, executing ``composer update`` disabled all Magento caches. This issue no longer occurs.
* Vendor names can now contain numbers.
* Single pipes in ``composer.json`` files have been changed to double pipes.
* Patch dependencies no longer cause a patch to be applied twice.
* Static content deployment (``bin/magento setup:static-content:deploy``) no longer results in random deletion of CSS files or multiple exceptions.
* You can successfully install Magento 2.3.4 with MySQL 8.
* You can now use SSL to connect Magento 2.x to an MySQL server.
* Merchants can use a  new system configuration setting to specify the API key for a currency provider. This key is needed when using the Currency Converter API  to import currency rates.

Analytics
~~~~~~~~~

* ``module-analytics/Model/ExportDataHandler.php`` now generates data in the ``Docroot/var/`` folder as expected.
* Clicking on the ESC key no longer closes the Admin Analytics popup dialog that Magento displays when an administrator first logs in.
* Administrators can now use the TAB key only to navigate  between the **Allow** and **Don't Allow** buttons.

Backend
~~~~~~~

* Magento now sets the correct Admin locale scope when generating email templates.

Bundle products
~~~~~~~~~~~~~~~

* The price and subtotal shown in the cart and mini cart for bundle products is now based on the quantity of items and tier price as expected. 
* The shopping cart now displays correct prices for bundle products when you use the **Add to Cart Button** to add them to cart twice.
* Bundle products now show the correct price when bundle options include only one multiple select option.
* The price attribute of a bundle product is now disabled as expected when dynamic prices are enabled.
* Magento no longer strips bundled options from a bundle product when you duplicate it. 

Cache
~~~~~

* Full-page caching now works as expected for non-default store views.

Cart and checkout
~~~~~~~~~~~~~~~~~

* Magento now applies the conditions that are imposed by multiple cart price rules correctly.
* Magento now correctly applies cart price rules that apply a 100% discount.
* Guest users can now checkout after persistent shopping cart has been disabled.
* Magento no longer displays custom dropdown customer address attribute option IDs  on the Review & Payment section of the checkout workflow when a guest checks out.
* Billing and Shipping information no longer disappear from the Payment section of the checkout workflow when an AJAX POST request fails.
* Magento now displays an error when you upload an incorrect product SKU while creating an order in a non-default store in a multi-store deployment. 
* Magento no longer displays customer address attribute option IDs  on the dropdown menu of the Shipping section of the checkout workflow. 
* Magento no longer drops or updates the shipping address  after a customer update or adds a new billing address zip/postal code when the **My billing and shipping address are the same** setting is disabled.
* Magento no longer throws a fatal error when you open the shopping cart in a separate window during multishipping checkout.
* Cart Price Rules tables in multi-site deployments now show existing cart price rules as expected.
* You can now use REST to add a product with customizable options (for example, type checkbox) to the cart.
* Validation logic has been added to the **Minimum Qty Allowed in Shopping Cart** field on **Store** > **Configurations** > **Catalog** > **Inventory**.
* Magento now displays correct product quantities on the Items Ordered  tab of the order page when the price includes a decimal value.
* Magento now saves the schedule update settings that are set in **Admin** > **Catalog** > **Categories** > **Category** > **Schedule Design Update** as expected when you change store view.
* You can now enable the **uploaded file of file type** custom option for a product from the shopping cart.
* Validation logic has been added to the **Send Payment Failed Email Copy To** field of **Admin** > **Store** > **Configurations** > **Sales** > **Checkout** > **Payment Failed Email**.
* Magento now refreshes the shopping cart as expected when you remove a product from the cart side block. Previously, when you deleted a product from the shopping cart side block, Magento did not update the shopping cart.
* Magento now correctly calculates minicart height when child items contain margins.
* Magento now displays an informative error message when a customer updates a shopping cart with a product quantity that is not in stock.
* You can now update the quantity of a product measured in decimals from the shopping cart when the **Qty uses decimal** setting is enabled. 
* The **Shopping Cart** label has been changed to **Mini Cart** in the sidebar.
* The **Clear Shopping Cart** button now works as expected when running Magento with Internet Explorer.
* Magento no longer empties the contents of a customer’s shopping cart when she presses **Enter** after changing a product’s quantity.
* Magento now includes the downloadable links associated with a downloadable product when you add the product to the shopping cart and then edit the cart.
* Discount descriptions are now displayed consistently throughout the product interface.
* Magento now displays the **Update** and **Delete** buttons as expected in the minicart in mobile view.
* The storefront and Admin shopping cart summary fields are now displayed consistently and reflect setting preferences. 
* The ``QuoteManagement::assignCustomer()`` method now allows you to merge a guest cart with an active customer cart. As a result, the ``PUT /V1/guest-carts/:guest-cart-id`` call works as expected.
* Magento no longer displays a disabled product in a cart or on the storefront if it is disabled after a customer has added it to the cart using a coupon code. 
* Magento now removes the ``aria-invalid`` attribute or sets the attribute value to **false** after successful  validation of the address entered into the checkout email field.
* You can now add products from a non-default website to a cart from the Admin in a multi-site deployment.
* Magento no longer adds attribute values to the cart URL when you add a configurable product to the shopping cart from the product details page.
* Persistent shopping cart now works as expected. 
* The shopping cart that contains items no longer displays a subtotal and order total of zero when the **Clear Persistence on Sign Out** setting is disabled and the **Redirect Customer to Account Dashboard after Logging in** setting is enabled.
* Quote item prices are no longer NULL in cart-related events.
* Magento now successfully saves the shipping information that a customer enters when persistent cart is enabled and after a customer has logged in after her session has expired but before the interval specified by the Persistence Lifetime value has been exceeded.

Catalog
~~~~~~~

* Editing the attribute set of a disabled product no longer enables the product on the storefront.
* Magento now displays category banner images as expected on the category edit and the storefront category pages.
* Magento no longer throws a fatal error during compilation of code that contains a preference for the category product indexer.
* When an administrator sets the out-of-stock threshold for a product to a negative value and allows backorders below a quantity of  0, customers can backorder a product until the out-of-stock-threshold value matches the product's stock quantity.
* Storeview-specific attributes are now included in layered navigation results even when the **All Store Views** setting is not enabled.
* Magento now displays the `Refresh Cache` message as expected when you change the layout of the category page.
* Catalog search layered navigation results now include product attributes of type price.
* Magento now highlights only the most recently selected category as expected on storefront pages that contain multiple categories. 
* The performance of the Product Categories indexer has been improved. Previously, reindexing product categories could take up to 30 minutes.
* Corrected an issue that caused category tree values to return null after upgrading from Magento 2.3.1 when multiple store views exist. 
* Clicking **Delete** on a Product page twice after selecting one or more products no longer deletes all products.
* The catalog product lists are now displayed as expected when products contain custom attribute conditions.
* Magento now successfully loads pages that implement the catalog product list widget when products contain custom attribute conditions.
* Merchants can now scroll down the **Create New Product** page to determine whether the product has been saved if they enter invalid values in the **Schedule Design Update** fields.
* Quote model extension attributes are now properly encoded and present on the checkout page as expected.
* Changing attributes sets now removes the attribute from the layered navigation and search results as expected.
* The **Date** field customizable option for products now saves accurate values for stores in different time zones.
* Custom attributes listed on the **Stores** > **Attributes** > **Product** > **Add New Attribute** page are now sorted alphabetically as expected.
* You can now  change the page layout of the ``catalog_product_view`` page from a custom theme by changing ``<theme_dir>/Magento_Catalog/layout/override/base/catalog_product_view.xml``.

CatalogInventory
~~~~~~~~~~~~~~~~

* You can now add a child product to the shopping cart if it does not have a default source assigned.

Cleanup and simple code refactoring
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* The **Are you sure you want to delete this category?** message is now translatable.
* The PayPal setting section of the **Admin** > **Stores** >**Configuration** > **Sales** > **Payment Methods** page now has an expand/collapse icon.
* An incorrect XML namespace URL was removed from the generated sitemaps displayed at **Marketing** > **SEO & Search** > **Sitemap**. Previously, Magento returned a 404 error when you clicked on the sitemap link.
* The minicart now displays a product’s file type custom option.
* The spacing of the Select Input box on Admin pages with grids is now consistent with other pages in Magento.
* Fixed misalignment of the scope icon and the store view-specific label on the **Admin** > **Store** > **Settings** > **Order status** > **Create New Status** page.
* The What's this? link in the Remember me section of the storefront login page now behaves as expected. 
* Corrected misalignment of the checkboxes and associated labels on the **Admin** > **Catalog** >  **Products** > **Update Attributes** page. 
* Fixed inconsistent and improper capitalization  in the **Admin** > **Marketing** > **Communications** > **Email Templates** > **Create a New Template** page.
* The ``Magento\CatalogUrlRewrite\Model\Storage\DynamicStorage::getCategoryUrlSuffix()`` method return value has been changed to type ``string``.
* The drop-down icon now remains visible when you click on **Load Template** while creating an email template from the Admin.
* Fixed alignment of the wishlist icon on the shopping cart in mobile view.
* Corrected misalignment and standardized design of the  Other PayPal Payment Solutions  header on the Store Configuration page.
* Duplicate labels in the Admin **Sales** > **Transactions** Payment Method table have been removed.
* Added a missing label on **Marketing** > **Search Synonyms** > **New Synonym Group**.
* Corrected the misalignment of the **Cache Type** checkboxes throughout the Admin.
* Fixed display issue with the placeholder text in the newsletter subscription block in the global footer that occurred in mobile view. 
* The default value for the **Products per Page on Grid** setting  was updated to 12. This setting affects the number of products that are displayed on the storefront for products when the list view is specified. This change will affect new customers and customer who have not previously saved this setting.

CMS content
~~~~~~~~~~~

* The checkboxes in the Dynamic Block Rotator (used when inserting a widget during the creation of a CMS page) have been corrected, and the widgets are now fully clickable as expected.
* You can now save CMS blocks with no content.

Command-line interface (CLI commands)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Exception handling messages for CLI commands have been  edited to be specific, informative, and relevant to the context in which the error occurs.
* ``bin/magento setup:backup --media`` now successfully backs up a symbolically linked ``pub/media`` directory.

Configurable products
~~~~~~~~~~~~~~~~~~~~~

* Magento now maintains the sort order of uploaded simple images when they are uploaded through the Create Configurations wizard.
* A configurable product’s options list now shows out-of-stock products as expected when the **Display Out of Stock Products** option is enabled.
* You can now remove special prices from a product without affecting the price of associated products.
* The performance of edit and save operations on configurable products has been improved.
* The Admin configurable product list now displays all simple products with a quantity of 0 as expected.
* Magento no longer throws an error when you try to add new attribute options to  a configurable product.
* Custom attribute loading now works as expected. Previously, the ``getUsedProducts()`` method’s optional ``$requiredAttributeIds`` parameter was not used, which prevented the loading of custom attributes.

Cookies
~~~~~~~

* Magento no longer redirects customers to the Cookie CMS page upon login when the **Redirect to CMS-page if Cookies are Disabled** setting is disabled.

Cron
~~~~

* A new flag has been added to the ``bin/magento cron:install`` command that permits you to add only mandatory entries to the ``crontab`` file of the server on which Magento is running. The ``--non-optional`` flag (or ``-d`` for short) adds only one of three possible lines to the `crontab` file. Without this flag, ``bin/magento cron:install`` adds three lines to the ``crontab`` of the serve. Only one of those added lines is necessary to run Magento, and many installations are configured such that the two optional lines are not needed.
* The ``bin/magento cron:run`` command now  adds an entry for ``currency_rates_update`` in the ``cron_schedule`` table as expected.

Customer
~~~~~~~~

* The **Date of Birth** field on the customer registration form no longer defaults to **1/1/1970** in deployments  that already contain a registered customer with the same email in stores using the `en_AU` locale.
* The list of countries accessible from the **Add New Address** field of the checkout workflow now displays only countries that have been defined in **Admin** > **Stores** > **Configuration** > **General**.
* Delegated account creation no longer fails when the customer address contains custom attributes.
* Magento now clears the **State/Province** field on the customer address page when you change the value for country while editing a customer address.
* Magento now runs validation checks on the values entered into the **Date of Birth** field in the Admin Add New customer page.
* Spaces are now trimmed as expected from values entered into the customer account **Phone** field.
* The Reset Password Confirmation Link email is now scoped appropriately for global customers.

Custom customer attributes
~~~~~~~~~~~~~~~~~~~~~~~~~~

* Magento now displays an informative error message when a customer tries to place an order without adding an address for the payment method and the **My billing and shipping address are the same** checkbox is unchecked.

Database media storage
~~~~~~~~~~~~~~~~~~~~~~

* The ``bin/magento catalog:image:resize`` command now processes images from the database as expected when files do not exist locally.
* Enabling **Flush Catalog Images Cache** on **System** > **Cache Management** now clears all cached image files from both the filesystem and database.

Declarative schema
~~~~~~~~~~~~~~~~~~

* The data/schema patch ``getAliases()`` method now works as expected.
* The ``WISHLIST_ITEM_OPTION_PRODUCT_ID_CATALOG_PRODUCT_ENTITY_ENTITY_ID`` foreign key has been removed from declarative schema.

Downloadable products
~~~~~~~~~~~~~~~~~~~~~

* Magento no longer displays a console error when you select all links for  a downloadable product on the storefront. 
* Magento now displays the **Unselect all** button on the shopping cart page when a customer selects a downloadable product with multiple options.

EAV
~~~

* The product attribute edit page now loads successfully when you try to edit an attribute value from the Admin.
* The Attribute Option update API no longer creates multiple options with the same value.
* The ``catalog_product_entity_varchar/catalog_product_entity_int`` tables are now updating with correct values.
* Magento now correctly saves the values assigned to the ``sort_order`` and ``attribute_group_code`` attributes by the ``POST /V1/products/attribute-sets/groups`` call.
* You can now perform mass actions on items in a grid that uses an EAV collection.

Email
~~~~~

* The Registration and Contact us pages now correctly handle customer names that contain non-ASCII characters.
* The product page Send Email to Friend email form is now sent from the email address configured as **sender** in the system configuration **General Contact** field.
* Validation logic has been added to the email fields on  **Admin** > **Stores** > **Configuration** > **Sales** >  **Sales Emails**.
* Validation logic has been added to the **Send Payment Failed Email Copy To** field of  **Admin** > **Stores** > **Configuration** > **Sales** >  **Checkout**.

Frameworks
~~~~~~~~~~

* Customers no longer have problems logging in to a Magento deployment on which ``bin/magento customer:hash:upgrade`` has been run and that also runs PHP 7.2.19 and has the sodium extension installed (libsodium  1.0.13 or greater).
* The ``bin/magento setup:db:status`` command now returns successfully after you’ve run ``bin/magento setup:upgrade`` on a deployment running Maria DB version 10.2.
* Country lists now provide a translation of Taiwan as Taiwan, Province of China.
* Magento now sends sales-related email to the correct customer when ``sales_emails`` cron has an error.
* The ``magento/framework/Mail/Template/TransportBuilder.php`` class has been refactored to make sure that ``$this->messageData`` is updated when ``$email`` is an ``array`` and ``isset($this->messageData[$addressType])`` is set to **false**.
* Magento no longer throws an error when you open an image from the product image gallery from the storefront product detail page. 
* Order-related ``save_after_commit`` callbacks are now called for guest checkouts as expected.
* The product counter and page lister on **Catalog** > **Products** now works correctly after the **Add Store Code to Urls** setting has been enabled or disabled.

JavaScript framework
~~~~~~~~~~~~~~~~~~~~

* Unnecessary define checks have been removed from JavaScript modules that are used by requireJS. 
* Excluding minified JavaScript files from the generated JavaScript bundles using the ``view.xml`` file inside a theme now works as expected. 

General fixes
~~~~~~~~~~~~~

* Basic validation steps have been added to fields on the **Store** > **Configuration** > **Catalog** page. 
* Magento now displays an error message when validation fails when you click **Generate** on the Manage Coupon Codes page and the applicable sales rule has the **Use Auto Generation** setting  enabled.
* Magento now correctly redirects you to the customer account page when you click the **Back** button on the Manage Addresses page.
* The New Block form no longer displays a **Store View** field when your deployment is in single-store mode.
* Images now change as expected when you swipe over the image when using a touch screen.
* Magento now displays an informative error message if validation fails when clicking **Generate** when managing coupon codes from the Admin.
* Access Control Permissions (ACLs) have been improved for the following cart-related tasks: export CSV and Excel file of abandoned cart and abandoned products reports. Previously, administrators with no permission to this information could export these reports.
* Validation logic has been added to the **Sort order** field of the New Rating form (**Stores** > **Rating**).
* You can now successfully filter products by multiple attributes in the Step 2: Attribute Values  section of the Admin Create Product Configuration page. Previously, only one of the selected values were retained when you tried to filter.
* Problems with less compilation  in Magento's blank theme when using an alternative less compiler than the one that ships with Magento by default have been resolved.
* Magento now extracts handles from layout updates before merging layouts.
* The ``Convert to Plain Text?``  confirmation message that Magento displays when you click **Delete** on the Admin Edit Email Template page now follows Magento design guidelines.
* The outdated URL for the HTTP Strict Transport Security page (accessed from **Admin** > **Store** > **Configuration** > **General** > **Web**) has been updated to ``app/code/Magento/Backend/etc/adminhtml/system.xml``.
* Validation logic has been added to the **Layered Navigation Price Step** field of the **Admin** > **Catalog** > **Categories** page. 
* Validation logic has been added to the **Oauth** field of the **Admin** > **Store** > **Configuration** > **Service** page.
* Validation logic has been added to the **Connection Timeout in Seconds** field of the **Admin** > **Store** > **Configuration** > **General** > **Currency Setup** page. 
* Magento now displays a confirmation message when you choose a mass delete operation on subscribers on the  **Admin** > **Marketing** > **Newsletter Subscribers** page.
* Validation logic has been added to the sort order field on the **Admin** > **Stores** > **All Stores** > **Create Store View or Website** page.
* XML attributes are now encoded to allow special symbols in tag attributes.
* Validation logic has been added to options for dynamically created product attributes before Magento adds these attribute values to the product database. Magento now checks whether the ``optionArray`` exists in the database before adding it. Previously, Magento created duplicate options for the same store.
* Calls to ``catalogProductTierPriceManagementV1GetListGet`` now handle requests as expected. Previously, calls failed when querying a configurable product
* The HTML ``br`` tag is now an allowed tag.
* The Admin notification counter now correctly handles double-digit values.
* You can now successfully select an image from the image gallery when you configure a theme (**Admin** > **Content** > **Configuration**). 
* Modal triggers can now be added after module initialization.
* You can now swipe on different images in the fullscreen product gallery on touch devices or when touch emulation is enabled in Chrome.
* The Admin Address Country drop-down list now takes its values from  the **Allow Countries** setting that is configured for the Website Store View where the order was made.
* Magento no longer serializes user data multiple times when data is loaded by the ``loadByUsername`` method.
* The Available Countries list  (**Stores** > **General**) has been updated to include the countries identified in the latest version of the Common Locale Data Repository (version  36).
* Method chaining now works as expected in extensions and customizations that are based on a product collection entity.
* The use of ObjectManager in the core code has been replaced  with factories and constructor dependency injections wherever possible.
* Magento now displays a bad request error message when the confirmation link sent to the new customer email is not valid.
* Catalog event start and end dates are not changed when you edit the event.
* Running ``diff -rq ./build-1/ ./build-2/``  on two different builds of the same commit now yields the same results in generated/metadata folders. Previously, these results were not reproducible.

Image
~~~~~

* The size of images displayed  in RSS feeds is now determined by the ``view.xml`` file.
* The content attribute for ``msapplication-TileImage`` now resolves to a localised theme path.
* When you move a category, the list of categories prepared for re-indexing now includes all affected subcategories when Flat Catalog is enabled.
* Watermarks cannot be configured for swatch images.

Import/export
~~~~~~~~~~~~~

* Magento now creates an advanced price export file as expected when exporting more than 5000 products. Previously, Magento threw an error and did not create the file.
* The Scheduled Import Settings page no longer displays fields that have been disabled in configuration settings.
* Removed redundant quotation marks from the CSV field title of the exported order CSV file.
* The Export page now displays exported files in a grid. Previously, Magento did not list files but instead displayed a message indicating that the CDATA section was too large to display when more than 20,000 records were exported.
* Exported CSV are now sorted based on time when you run ``bin/magento cron:run``.
* You can now import empty values (``__EMPTY__VALUE__``) from a CSV file at the store-view level.
* Magento now handles URL rewrites correctly when you import data for an existing product.
* You can now exclude attributes from a CSV file when setting up an export (**System** > **Data Transfer (Export)**).
* Magento now correctly processes product prices during export when the **All Store Views** scope is set. Previously, the logic for updating the price in custom options in non-default websites was missing when the **Catalog** > **Price** setting is set to **Website**.
* Magento now respects website scope settings when you export product data in a CSV file.
* Magento now adds newly imported images after previously imported ones.
* You can now successfully import customer data that has not been modified when generating the CSV file with the **Add/Update Complex Data behavior** option.
* Corrected spacing issue in the ``Magento_Config`` file.
* Magento now correctly imports product quantity from a CSV file. Previously, the quantity field for a product could be **0**, but the status field  would indicate **in stock**.
* Magento now displays an error message as expected when you select **Import Tax Rates** without selecting a file for import on (**Admin** > **Import & Export Tax Rates**).
* You can now successfully import an image from an external URL.

Index
~~~~~

* The ``POST /V1/products/tier-prices`` call now considers account indexer mode as expected.
* Magento no longer throws a fatal error when you create a preference for the category product indexer before running ``bin/magento setup:di:compile``.
* During re-indexing, Magento now deletes only products that have been identified as out-of-stock  when filtered by ``$entityIds``.

Infrastructure
~~~~~~~~~~~~~~

* File permissions for non-executable files in GitHub have been changed from 755 to 664 where appropriate.

* An incorrect Bool return type for the ``setIsActive()`` method in ``Salesrule Module RuleInterface.php`` has been corrected to `RuleInterface`.
* Magento no longer adds a ``form_key`` field to POST forms that have external action URLs.
* The dictionary was removed from the ``zxcvbn.js`` library, and the following performance improvements have resulted: 1) The size of the ``zxcvbn`` library has been reduced from 395 KB to 11.3 KB on customer registration, customer edit, and customer forgot password pages; 2) The time required for asynchronously loading this library has been reduced by 90%.
* The ``scopeData()`` method now returns a ``DateTime`` value that is scoped to the specified store locale. Previously, this method was not fully implemented.
* The ``getAttributeRawValue`` method now returns a store-specific value even when there is no default value. Previously, no store value was returned when a default value was not present.
* The performance of the ``ProductMetadata::getVersion`` method has been improved as a result of adding the caching of the product version. This method is called by many third-party extensions to determine the version of Magento.
* You can now add products with custom options of all types to the shopping cart.
* Decimal numbers have been added to the Sample File in Import CSV section.
* A deprecated method in ``\Magento\MysqlMq\Model\Driver\Exchange`` has been replaced.
* You can now add handlers directly to the ``di.xml``.
* You can now add a handler directly to the ``di.xml`` of a product template instead of adding a handler by extending the helper class and registering the handlers.
* Magento no longer returns an empty string when calling ``$this->_escaper->escapeXssInUrl(“0”);``, but instead returns the expected 0 value. 

Inventory
~~~~~~~~~

* You can now save an edited product when ``max_sale_qty`` is set to the Magento default value.

Layered navigation
~~~~~~~~~~~~~~~~~~

* Layered navigation is no longer visible when you set display mode to **Static Block only** on a particular category.

Media storage
~~~~~~~~~~~~~

* Magento now retrieves images from the proper cache in multi-store deployments.

Newsletter
~~~~~~~~~~

* Magento now displays empty **Customer First Name** and **Customer Last Name** fields on the **Admin** > **Marketing** > **Newsletter Subscribers** page. Previously, these fields contained the unexpected string ``—``.
* Corrected alignment of the **Newsletter** label and associated checkbox on the Admin customer edit page.
* The **Subscribe** button is now visible on the Subscribe form as expected. Previously, an  sr-only element hid this button.
* The **Subscribe to Newsletter** checkbox now works as expected when **Stores** > **Configuration** > **Customer** > **Customer Configuration** > **Account Sharing** is set to **Global**.
* Customers are no longer sent unsubscribe to newsletter emails when they register for a new account and the **Sign Up for Newsletter** setting is set to **on**.
* The newsletter template preview now displays images as expected.

Orders
~~~~~~

* The Order list now displays order information in the currency in which the order was placed, not the current base currency of the store. 
* You can now open a storefront from **Sales** > **Orders** > **Customer View**.
* The checkbox on the **Admin** > **Create New Order** > **Add Products** page now works as expected in Internet Explorer 11.x. This checkbox now behaves the same across all supported browsers.
* Magento now displays the customer middle name in the customer details on orders and in the new order email sent to customers.
* Magento now updates the ``сustomer_email`` value in the ``quote`` and ``sales_order`` tables as expected when a customer changes their email address.
* Customers can now cancel an order that they created using a coupon while logged in as a guest.
* Magento now displays a warning message when you click the **Apply Coupon Code** button without filling in the coupon code when creating an order.
* Magento now sends New Order email as expected when the **Send Order Email Copy To** field contains a comma followed by a blank space.
* An incorrect critical log entry (`No such entity with customerId = xxx`) in the ``exception.log`` file has been corrected. 

Payment methods
~~~~~~~~~~~~~~~

* You can now use Paypal Payflow Pro to complete an order in deployments running Internet Explorer 11.x.
* Magento now successfully processes orders that are shipped to multiple addresses when Braintree with PayPal is used as the payment method. 
* Guests can now successfully pay for an order using PayPal Express Checkout.
* You can now successfully complete an order using Braintree with PayPal when Shipping Flat Rate is activated. 
* Magento no longer displays the PayPal Credit option on the checkout workflow on the storefront when this option is disabled in the Admin.
* Magento now properly concatenates first and last names in PayPal Express address fields.
* The Saved Credit Card Feature with Vault feature nows displays accurate card information in the order information page as expected for orders paid for with Payflow Pro.
* The **Qty to Refund** field on the credit memo of an order paid for with Authorize.net is now editable.
* Magento no longer throws a fatal error when you enter an invalid shipping address when placing an order with Braintree with Paypal.
* Magento no longer displays duplicate **Place Order** buttons on the Review Order page for orders made with PayPal Express.
* You can now successfully add new products to the cart when placing a re-order from the Admin when the original order used a coupon and the Braintree payment method.
* Magento no longer displays the **PayPal Express Checkout** button on product pages or the shopping cart when the **Display on Product Details Page** and **Display on Shopping Cart (Advanced Settings)** settings are disabled.
* Magento no longer displays the  **PayPal Credit** button when the **Checkout with PayPal** button is displayed on the shopping cart.
* Validation logic has been added to the **Send Payment Failed Email Copy To** field of **Admin** > **Store** > **Configurations** > **Sales** > **Checkout**.
* The Stored Payment Methods section of the customer dashboard no longer depends on Braintree being enabled. Removing this dependency permits custom payment methods to also use this section.
* Magento no longer throws JavaScript errors when a customer tries to pay for an order using PayPal when the shipping address fields are incomplete.
* Removed the redundant XML code in the ``<payflow_advanced>`` node of the PayPal ``config.xml`` configuration file. 
* The **Enable this Solution** setting is now set back to **no** for  PayPal Express as expected when a customer clicks on **Cancel** on the “There is already another PayPal solution enabled. Enable this solution instead?” popup during PayPal Express checkout.
* The Braintree `ClientToken` is now disabled when the  Braintree payment method is disabled for the current store view.

Reports
~~~~~~~

* Sorting has been disabled on the New Account column of the New Accounts report.
* A missing newline  has  been added to the end of ``var/report`` report output, which has improved the automatic parsing of log files.
* Magento no longer throws a console error when you click **Select All** on the **Newsletter Problems Report** page.

Reviews
~~~~~~~

* The **Reset** button now works as expected on  **Admin** > **Marketing** > **All Reviews** > **New Review** page.
* **Select All** on the coupon list of the Manage Coupon Codes page now works as expected.
* Magento no longer displays the **Add New Review** button on the **Admin** > **Marketing** > **All Reviews** > **New Review** page if no product is present.
* The product detail page now scrolls as expected when you click on the Review or Add Your Review link.

Sales
~~~~~

* Validation has been added to **Minimum Order Amount** field  on the **Stores** > **Settings** > **Configuration** > **Sales** page.
* Invoice email is now sent automatically as expected when the **Payment Action** setting for a payment method set to **Authorize and capture**.
* The order view section of the checkout workflow now shows the correct shipping price for an order to be shipped to multiple addresses.
* Tax rates and amounts now change as expected when the billing address for an order is changed from the Admin.
* Magento now sends email to customers when an invoice is created. Previously, even when the relevant configuration setting was enabled, Magento did not automatically send this email.
* Coupon codes for free shipping are displayed like other coupon codes.
* You can no longer add disabled variations of a configurable product to a shopping cart from the Admin.
* The **Quote Lifetime (days)** setting, which specifies the number of days that a quoted price remains valid, now works as expected.

Sales Rule
~~~~~~~~~~

* You can now change action settings for a scheduled update of a Cart rule.
* Magento no longer displays an error when  a customer clicks **Subscribe to Order Status** on an order page, and now subscribes the customer to the XML feed as expected.
* The counter values on the **Marketing** > **Cart Price Rules** grid now match the number of rules listed in the grid as expected.
* Magento now applies coupon codes correctly when an order subtotal dips below the threshold specified in the applicable cart price rule. 

Search
~~~~~~

* The pagination of multipage search results now works are expected.
* MySQL performance for search queries has been optimized, and merchants running sites with many search queries will notice improvements in query speed.
* Quick search now successfully handles search phrases that contain fewer characters than the configured value.
* Magento no longer requires a full search reindex in order for a new product attribute to be searchable on the storefront.
* The storefront now displays a newly added product in its assigned category after you run ``bin/magento cron:run && bin/magento cron:run``.
* Searching on categories from the New Product page now works as expected when you enter a search string that does not match an existing category.
* Elasticsearch now successfully finds products on the storefront using the values of dropdown attributes.
* Elasticsearch now correctly handles search queries that include words that contain diacritics as well as spellings of those words that are entered without the correct diacritics.
* You can now search the **Sales** > **Orders** list by email address.
* Running ``bin/magento indexer:reindex catalogsearch_fulltext`` no longer results in the deletion of an index-related database table.
* Elasticsearch results now display all products as expected when the **Configuration** > **Catalog** > **Storefront** > **Allow All Products Per Page** is set to **yes**. 
* Category pages now work as expected when Price Navigation Step Calculation is set to **Automatic (equalize product counts)**.
* Magento no longer throws an exception when you initiate an advanced search using product name and SKU.
* Elasticsearch now successfully handles search queries that contain a question mark followed by a semicolon (?;).
* Validation logic has been added to the **Number of results** and **Number of Uses** fields of **Admin** > **Marketing** > **Search Terms**.  
* Magento no longer logs a warning when a catalog search query contains multiple custom option values.
* The undefined variable in the ``getStoreValuesForForm`` method has been defined.
* Elasticsearch 6.x now works only with Elasticsearch 6.x clients on the storefront.
* Elasticsearch clients can now use SSL without enabling HTTP Auth.
* Elasticsearch no longer creates a double index when Magento throws an exception when it saves an index as a cron job fails.

Shipping
~~~~~~~~

* The code for offline shipping methods has been optimized to remove redundant carrier codes.
* VAT ID is now included on the Shipping page of the checkout workflow as expected.
* The **Back** button on the Check Out with Multiple Addresses page now returns you to the correct page. Previously, clicking the Back button from this page returned a 404 error.
* UPS Mail Innovations tracking now works as expected. 
* Cart Price rules now work as expected for orders that are shipped to multiple addresses.
* Shipping notification emails sent to customers now contain a link to order tracking.
* Shipping calculations now load correctly from the shopping cart.
* You can now successfully re-order a configurable product when shipping the order to multiple addresses.
* Magento now displays the correct cost for shipping in the shopping cart when you return to the cart from the checkout page for an order being shipped to multiple addresses.
* You can now create a shipping label as expected. 
* Magento now loads shipping methods as expected in the checkout workflow when running in Internet Explorer 11.x.
* Magento no longer displays **Shipping Method: undefined - Fixed** on the final page of the checkout workflow when a shipping method with an undefined or empty  method name is selected.
* New order pages for orders that contain only virtual products no longer display a Shipping and Handling total.
* Validation logic has been added to the **Sort Order** field of **Admin** > **Store** > **Configuration** > **Sales** >  **Shipping methods**.
* The ``POST  /V1/shipment/track`` call now throws an error.

Sitemap
~~~~~~~

* Magento no longer displays multiple success notifications when you click on the **Save** button on **Marketing** > **Sitemap**.
* The path that you specify when creating a sitemap is no longer transferred to the beginning of the URL that is included in any sitemap-related error message.
* We’ve corrected several problems with image URLs in sitemap generation.

Store
~~~~~

* Redirect URLs  are no longer truncated  after three slashes.
* Magento installation no longer fails with pre-defined stores in ``app/etc/config.php`` due to MySQL locks.
* CMS pages no longer redirect to the home page of the original store when you change store view in a multi-store deployment.

Swagger
~~~~~~~

* Swagger schemas no longer fail when the GET endpoint has parameters that contain extension attributes.

Swatches
~~~~~~~~

* Magento now displays selected swatch options for a configurable product when you edit that product from the shopping cart.
* You can now add options values to text swatch and visual swatch attributes using ``POST V1/products/attributes/<attribute_code>/options``.
* Magento now loads product images as expected when you switch between product variations (for example, size or color).
* Magento now displays the correct “as low as” price on the storefront for a configurable product with multiple attributes that include a ``color`` attribute. Previously, Magento did not display the lowest price.

Tax
~~~

* Validation for maximum length has been added to **Zip/Post Code** field of the New Tax Rate page. 
* Corrected inconsistent style on the messages displayed when you click the **Validate VAT Number** button on **Stores** > **Configuration** > **General**.
* Magento now correctly calculates VAT for products when you add them to the cart.
* You can now successfully save a fixed product tax (FPT) to a product that is assigned to a specific website.
* Inconsistent sorting of fixed product tax (FPT and tax totals has been resolved on the Admin order, create invoice, invoice, create credit memo, and credit memo pages. 

Testing
~~~~~~~

* Integration tests have been added for ProductAlert Stock notifications.

Translation and locales
~~~~~~~~~~~~~~~~~~~~~~~

* Serbian Latin language support has been added to this release, and merchants can now distinguish between Latin and Cyrillic Serbian locales. Locales are now identified as Serbian (Cyrillic, Serbia) and Serbian (Latin, Serbia). 
* The Arabic Date Selector now shows the date in the correct format. Previously, when the site was set to Arabic (Saudi Arabia), the storefront date selector always displayed a date of ``GGGG``.
* The country names on the checkout, shipping, and billing address forms are now translatable. 

UI
~~~

* Media gallery thumbnails are no longer stretched when images have a horizontal ratio.

* The tax amount in  sales order emails is now displayed before the row that displays the order’s grand total.
* The **Billing ZIP Code** field on the Orders and Returns page now works as expected. Previously, it was not consistently visible.
* A missing header label has been added to the **Admin** > **System** > **Integrations** table.
* The **New Key** field is now marked as a required field with an asterisk when changing an encryption key on the **Admin** > **System** > **Manage Encryption Key** page.
* Corrected misspelling of “tier” (as in “tier price”) throughout the code base.
* Standardized the confirmation popup invoked from the Admin Add New Tax Rules page.
* The Suggested Terms drop-down text in  **Admin** > **Marketing** > **SEO & Search** > **Search Terms** are now in camel case.
* Email previews are now fully responsive.
* You can now confirm changes to the structure of the category tree by either clicking the confirmation dialog **OK** button or using the Enter key on your keyboard.
* Client validation has been added to shipment tracking numbers.
* Magento now displays checkout steps in the custom order that is set in ``uiComponents SortOrder``.
* Removed a redundant asterisk on the Configure Product page.
* Removed the box shadow that appeared when you clicked on a disabled swatch for a product on the storefront. 
* Magento now displays a pointer icon for the cursor when the cursor hovers over the  **Collapse All/Expand All** button on **Catalog** > **Category** > **Content** Select from Gallery option.
* The **Get Video Information** button on the **Product** > **Images and Videos** > **Add Video** page now responds as expected.
* The storefront now reflects height settings for conditions that are added to Terms and Conditions (**Store** > **Terms and Conditions** > **Add New Condition**). 
* The **Edit Attribute Set Name** label was corrected to **Attribute Set Information** on **Admin** > **Store** > **Attribute Set** > **New Attribute Set**.
* Corrected issue with highlighting on the storefront sales order page.
* Corrected multiple misspellings throughout the Admin and corrected a comment in the Admin that was not translatable. 
* You can now  use ``@submenu-desktop__padding``  to override the padding in the ``.lib-main-navigation-desktop`` mixin by using ``@submenu-desktop__padding``.
* The performance of the accordion widget has been improved.
* Corrected misalignment of page elements on the minicart checkout page when the cart contains a configurable product.
* The tooltip associated with the **Product Additional Options** field for the order on the customer dashboard is now fully visible.
* The Credit Memo page now has an **Update Totals** button as expected.
* You can now filter orders by date in stores running the ``en_GB`` locale.
* Checkboxes that occur within widgets are now  fully clickable in the Admin.
* Redundant attributes that were present in the CMS widget body have been removed.
* UI components configuration has been corrected to eliminate potential for overlapping text labels.
* The weight attribute label is now displayed for attributes in attribute sets.
* Corrected issues with the **Admin** > **Marketing** > **User Contents** > **Reviews** **Created** date display.
* The current tab is now marked as active as expected in the customer account sidebar.
* ``bin/magento app:config:import`` and ``bin/magento setup:upgrade`` no longer fail due to a ``TEXT`` field limitation from ``flag_data`` in the flag table.  The ``flag_data`` field has been increased to ``MEDIUMTEXT`` (accepting 16MB).
* The **Unselect all** text string is no longer appended to the `HTML` element of the Compare icon on the product details page when you click this icon.
* Clicking on the **Visibility** header on **Admin** > **Marketing** > **All Reviews** or **Pending Review** now disables the sort ability as expected.
* The Action column is now the last column of the **Admin** > **Content** > **Configuration** grid.
* Validation logic has been added to the required fields on **Admin** > **Content** > **Widget** > **Add Widget**.
* You can now perform bulk delete operations on widgets in **Admin** > **Content** > **Widgets**.
* The Admin navigation sidebar menu now has toggle functionality for opening and closing menu items.
* The TinyMCE editor now saves content with inline style tags as expected.
* Merchants can now use virtual configurable variants to assign a weight to a virtual product.

URL rewrites
~~~~~~~~~~~~

* We have reverted the following fix, which was included in 2.3.3, because it changed expected system behavior: "Magento no longer removes the query string from URLs when the query string is preceded by a slash.
* Magento now populates the ``url_rewrite`` table with the new product URL rewrite when you create a new product when single-store mode is enabled.
* URL rewrites are no longer lost if an exception is thrown or a deadlock occurs during URL regeneration.
* CMS pages now redirect correctly after you change the store view.
* A category schedule update no longer unchecks the **Use default value** setting on the URL key for the store view.
* The performance of MySQL queries on ``url_rewrite`` operations  has been improved.
* ``CatalogURLRewrite`` no longer generates an extra product URL during product creation.
* Magento now correctly stores the attribute ``url_path`` for non-default stores.
* The following reserved keywords cannot be used as URL keys: ``admin``, ``soap``, ``rest``, ``graphql``, and any custom Admin path.

Web API framework
~~~~~~~~~~~~~~~~~

* When you use a call such as ``POST V1/carts/mine/items`` to add a product to a cart but do not include the ``quote_id`` parameter, Magento now returns a `400 Bad Request` error as expected.
* Added the **Stores** > **Settings** > **Configuration** > **General** > **Currency Setup** > **Currency Converter API** >  **API Key** field to enable currency rate retrievals from http://free.currencyconverterapi.com.
* You can now set expiration times for REST API Auth tokens in minutes and seconds. Previously, expiration times were defined in hours only.
* The ``GET V1/attributeMetadata/customerAddress/attribute/prefiX`` and ``GET V1/attributeMetadata/customerAddress/attribute/suffix`` calls now return options as expected. 

Wishlist
~~~~~~~~

* Wishlists now display values for product custom file types.
* Verification logic has been added to the wishlist so that it reflects accurate stock status of listed products.
* Magento no longer displays a JavaScript error when you try to remove an item from a wishlist. 
* Wishlist SKU counts now reflect the actual products listed.
* Products that are deleted from a wishlist from the Admin are now deleted from the storefront wishlist, too.
* The Admin wishlist display now lists the correct configurable products for all wishlists no matter which stores the wishlists were assigned to.

WYSIWYG
~~~~~~~

* The Admin WYSIWYG editor no longer hangs when an image upload dialog opens. Previously, Magento displayed the spinner cursor until you refreshed the page.
* You can now open the Media Gallery without error. Previously, when you tried to open the Media gallery, Magento displayed the spinner icon on Media Gallery popup.
* You can now upload a video from the WYSIWYG editor.
* The WYSIWYG editor now saves quotation marks correctly. Previously, quotation marks were converted to ``&quot;``.
