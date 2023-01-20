Magento Open Source 2.3.6 Release Notes
=======================================

**Official link**: https://devdocs.magento.com/guides/v2.3/release-notes/open-source-2-3-6.html 

Magento Open Source 2.3.6 offers significant platform upgrades, substantial security changes, and performance improvements.

This release includes over 160 functional fixes to the core product and over 15 security enhancements.

Adding support for PHP 7.4.x in Magento 2.3.7, which is scheduled for release in Q2 2021. This support will introduce breaking changes to Magento 2.3.x deployments.
How will this affect your store? See the `PHP 7.4 support for Magento 2.3.x release line <https://community.magento.com/t5/Magento-DevBlog/PHP-7-4-support-for-Magento-2-3-x-release-line/ba-p/458946>`__


Compatibility issues upgrading from Magento Open Source 2.3.5 to 2.3.6
----------------------------------------------------------------------

Merchants upgrading from Magento Open Source 2.3.5 to 2.3.6 and extension developers should be aware of these code changes:

* ``\Magento\Sales\Model\Order\Pdf\Invoice`` class constructor arguments have changed.
    
    - ``\Magento\Framework\Locale\ResolverInterface`` dependency has been replaced with ``\Magento\Store\Model\App\Emulation``.
    - You can no longer call a parent constructor from child classes with the same arguments.
* Protected property ``\Magento\Sales\Model\Order\Pdf\Invoice::_localeResolver`` has been removed and cannot be used in child classes.
* If your module contains a class that extends ``\Magento\Sales\Model\Order\Pdf\Invoice`` and must support both Magento 2.3.5 and 2.3.6,see the recommended solution documented in `this comment <https://github.com/magento/magento2/issues/30684#issuecomment-722602562>`__.

Fixed issues v2.3.6
-------------------

They have fixed hundreds of issues in the Magento 2.3.6 core code.

Installation, upgrade, deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* The Use default checkbox for Klarna payments ``(Stores > Configuration > Sales > Payment methods > Klarna)`` now remain checked as expected when website scope changes.
* Upgrade no longer results in the sudden failure of the Galera cluster.
* ``bin/magento setup:di:compile`` no longer throws a fatal error.
* Magento now displays an informative error message when some themes are not deployed after running ``setup:static-content:deploy``.

Amazon Pay
~~~~~~~~~~

* Clicking **Return to standard checkout** just before completing checkout with Amazon Pay now returns the shopper to the checkout page that displays all payment methods available the shopper. Previously, no payment methods were displayed.

Backend
~~~~~~~

* The Products in the Comparison List and the Recently Compared Products features now work as expected. Previously, when the comparison list was expanded, Magento did not display products, even though the section indicated that the list contained products.

Bundle products
~~~~~~~~~~~~~~~

* Magento no longer sets prices for fixed-price bundle product child items in quotes.
* Re-importing bundle products now works as expected. Previously, the second import did not change the catalog_product_relation table, and the storefront did not display the bundled products because parent-child product relations were not generated correctly.

Cache
~~~~~

* ``X-Magento-Tags`` headers no longer exceed the size permitted by the HTTP specification. Previously, category pages that contain many products return an ``X-Magento-Tag`` header that resulted in a 503 error.

Cart and checkout
~~~~~~~~~~~~~~~~~

* The **State/Province/Region** input box is now enabled as expected on ``My account > Address Book > Add new address``.
* Custom address attributes are now included as expected in the form that is displayed for the Payment step of the checkout workflow.
* The shipping method estimator now works as expected when custom address attributes are present on the shipping step of the checkout workflow. 
* Custom customer address attributes fields are now displayed as expected in the storefront checkout workflow.
* Shoppers can now purchase a virtual gift card using PayPal Braintree without defining a shipment address. Previously, Magento threw an error.
* Magento now displays the waiting/spinning icon while prices are updated on the cart.
* Merchants can now enable **Apply to Shipping Amount** in the Action tab of ``Marketing > Cart Price Rules > Add New Rule`` when **Fixed amount discount for whole cart** is applied.

Catalog
~~~~~~~

* Merchants with multiple websites can now use `POST /V1/products` to create and update products while preserving image and image-role inheritance.
* Magento now successfully updates attributes labeled `Product Type`.
* Problems with product sort order on the storefront have been resolved.
* Shoppers can now re-order an invoiced order of a product with customizable options as expected.
* Magento now displays all re-enabled products in the storefront as expected.
* Magento now displays the Recently Compared Products widget only after at least one product has been deleted from a product comparison. 
* You can now successfully save an image to a category from the Admin.
* The **Product in Websites** checkbox of the new product page is now enabled by default for restricted administrative users in multi-site deployments.
* The **Price** condition in Page Builder now works as expected for configurable products.
* Saving a category now flushes only the block cache that is related to this category.
* Magento now correctly represents Arabic thousands grouping and Arabic decimal separator symbols. 
* Consecutive asynchronous price updates no longer interfere with each other and correct status is assigned to each operation. 
* Changes introduced by an earlier bug fix that resulted in HTML errors on the product list page have been reverted.

Catalog Rule
~~~~~~~~~~~~

* Product and catalog caches now expire as scheduled.

CMS content
~~~~~~~~~~~

* Magento now throws an error when a merchant creates a CMS page with the same URL as the Company Structure page.

Configurable products
~~~~~~~~~~~~~~~~~~~~~

* Admin users accounts created from an admin account with a restricted scope can now create a configurable product with attributes as expected.
* Magento no longer links a simple product to a configurable product when the API call to link these products fails.
* Pagination problems with the Configurable Product Edit Current Variations list have been corrected.

Customer
~~~~~~~~

* The **State/Province** fields are now populated as expected on the Edit Address page (**My Account** > **Address book**).
* Customer group is no longer automatically changed for a customer who is assigned to a Company when you edit the customer on the Customer grid.
* Magento no longer resets a customer's customer group to the default when a customer saves their account information.
* Saving a deleted customer from the Admin now generates an error message only.
* Magento now honors customer group settings when you create a new customer from the Admin in a multi-site deployment.
* The validation logic associated with the **Date of Birth** field of the Customer Registration form no longer triggers a JavaScript error.
* The Admin view of a customer cart now displays all the products that were added to the cart from multiple websites in a multi-website deployment.
* The **Invalid Form Key. Please refresh the page** text string on the login page is now translated as expected.
* Magento now displays the **Credit memo** button after the partial refund of an order.
* The shopping cart that is accessed from the Admin customer details page now includes only products from the selected customer's quote. 
* Customer creation from the Admin now honors the default customer group setting as expected.
* The ``PHPSessionId`` is now changed as expected after a customer logs out and then logs back in.
* Data scripts are no longer re-run whenever you attempt to upgrade the database by running ``bin/magento setup:upgrade``.

Directory
~~~~~~~~~

* The Default State dropdown menu is now populated by data that is based on the allowed countries that have been assigned to the selected website when you configure a value for the **Default Tax Destination Calculation** field.
* The format of the State/Province drop-down menu is now consistent across the Admin.

dotdigital
~~~~~~~~~~

* dotdigital now has a Content Security Policy whitelist for specific domains used by this module.
* Contacts are no longer resubscribed when their ``last_subscribed_at`` value is ``null``.
* Deletion of automation enrollments and abandoned carts from their respective report grids now works as expected.
* Handling of the API response dotdigital receives when processing resubscribes has been improved.
* dotdigital now catches exceptions that are thrown by ``unserialize()`` to protect against unserializable data being stored for custom attributes.

Downloadable
~~~~~~~~~~~~

* Clicking on a downloadable product's **Sample** button from the Admin product page now downloads a sample as expected.
* You can now use an import file to update downloadable products in bulk by SKU and description. 
* Administrators with restricted permissions to Catalog can now create a downloadable product. 

Email
~~~~~

* Customers are no longer redirected away from the current website when they report a forgotten password in multi-site deployments where customer accounts are shared globally.
* Order confirmation emails sent to customers now include the list of ordered items as expected.

Frameworks
~~~~~~~~~~

* ``sales_order_shipment_track_save_commit_after`` is now triggered as expected when you use the REST API to create a shipment.
* We have improved the performance of the ``Magento\Framework\App\DeploymentConfig\Reader::load`` function.
* Magento no longer throws the following fatal error when Redis uses all allowed memory: ``report.CRITICAL: OOM command not allowed when used memory > 'maxmemory'.``

General fixes
~~~~~~~~~~~~~
* An expired persistent session is now renewed as expected when the shopper logs back in.
* Merchants can now unassign products from categories as expected.
* MAP (minimum advertised price) now works as expected for group products.
* New CMS pages are now added as expected to a website's store page hierarchy.
* Magento no longer throws an exception when a shopper tries to unset the persistence cookie after beginning checkout and then navigating to the storefront home page.
* You can now use the ``PUT /V1/products/:sku`` endpoint to update links to YouTube videos.
* You can now use ``app/etc/env.php`` to change the message broker from MYSQL to AMQP.

GroupedProducts
~~~~~~~~~~~~~~~

* Merchants can now successfully send email to a shopper that contains a credit memo for an order that includes a grouped product.
* The products query now returns all expected data for grouped products.

Image
~~~~~

* Magento now displays PNG images as expected after upload.

Import/export
~~~~~~~~~~~~~

* When an imported product has ``qty`` set to 0 but ``is_in_stock set`` to 1 in the CSV file, the product is not listed on the category page, and the product details page lists it as out-of-stock.
* The ``error_report.csv`` file now downloads with content and is available inside the ``var/import_history/`` directory as expected. 
* You can now hide product images on the storefront during import.
* Imported CSV files now capture related product information as expected. 
* Magento now successfully imports customer addresses that contains a region for a country that does not have defined regions.
* Magento now displays the customer list as expected after automatic re-indexing.
* Magento no longer creates duplicate SKUs in the Admin when products are imported by CSV file.
* Magento no longer throws an error during import when imported data includes a ``swatch_image`` store-view key has a value of ``no_selection``. 
* Deadlocks no longer occur when the import process executes a bulk insert and the re-index process simultaneously executes a large insert from select.
* Customer address ``region_id`` is no longer assigned a ``NULL`` value when you import customer addresses using a CSV file (``entity type = "customer address"`` and ``import behavior = "add/update”``) from which certain field values have been deleted.

Klarna
~~~~~~

* Magento now correctly refunds a Klarna order when the order contains a product that has been deleted.
* Default configuration settings for Klarna remain set as expected when you change the configuration scope to a different website.
* The checkout page now opens as expected when a shopper's cart contains a downloadable product.
* Fraud notification messages have been improved.

Media storage
~~~~~~~~~~~~~

* ``var/resource_config.json`` is no longer regenerated whenever an image is requested by ``get.php``.

Newsletter
~~~~~~~~~~

* Exporting the Newsletter Subscribers list using the ``Excel XML`` option now results in the export of all rows as expected.
* Magento no longer throws an error when a user subscribes to a newsletter and reCAPTCHA for the newsletter is disabled for the website scope. 
* Shoppers subscribing to a newsletter now receive only an email confirming their subscription.

Payment methods
~~~~~~~~~~~~~~~

* Registered shoppers can now checkout successfully when their only defined payment method is Braintree.
* Magento now completes Payflow Pro payments successfully when the shopper's name contains accented letters.
* Magento no longer saves credit card numbers when the **Save for later use** checkbox on the payment section of the checkout workflow is not selected.
* Magento now displays a message that prompts you to enter mandatory credit card data when you click **Submit** for an Admin order without entering valid payment information.
* A shopper whose address book contains multiple addresses can now change shipping addresses during checkout when paying with Braintree. 
* You can now successfully use PayPal Express to pay for an order when persistent checkout cart is enabled and the **Clear Persistence on Sign Out** setting is set to **no**.

Product alert
~~~~~~~~~~~~~

* Unsubscribe actions for product alerts now work as expected.
* Product stock alert unsubscribe now works when a user’s session expired. 

Reviews
~~~~~~~

* Magento no longer returns a 500 error when you try to open a Category page on the storefront when **Layout = Product – Full Width** has been set from the Design tab of the Category page.

Sales
~~~~~

* Order update emails that are sent to customers now include the correct order status.
* The New Shipment email generated by  ``POST /V1/order/:orderId/ship`` now contains the same shipping and customer information as shipments that are created manually from the Admin. 
* Magento no longer assigns a status of `Complete` after invoicing an order that requires zero payment.
* Localized region names that are displayed on the storefront Order page are now correctly translated. 
* Email sent to customers that contain partial invoices now includes accurate item subtotals. 
* ``sales_clean_quotes`` now efficiently deletes all expired quotes.
* Magento now assigns the correct Group ID when a new customer creates an order in multi-site deployments.
* Administrators with restricted permissions that include view permission for credit memos, invoices, and shipments can now view invoices and shipments from the Orders page as expected.
* Magento no longer displays an error when a customer adds a quantity of a product to their cart that exceeds half of the existing product stock but does not exceed the total stock.

Sales Rule
~~~~~~~~~~

* Coupon codes that have been applied based on shipping method are no longer applied when a shopper changes shipping method. Previously, Magento did not clear coupon codes when shoppers switched shipping methods.
* Coupon discounts are now calculated correctly when you add a bundle product to the cart after the coupon was applied.
* Shoppers cannot apply a coupon code more frequently than the **Uses Per Customer** setting permits.
* The order summary now displays the correct discount amount when a cart price rule has been applied. 
* Magento now displays category trees as expected when you try to create or edit a Cart Price rule. 
* Magento now applies fixed-amount, whole-cart discounts correctly for orders being shipped to multiple addresses.

Search
~~~~~~

* Elasticsearch results now include the correct values for each store view's attribute options. If a Dropdown or Multiple Select attribute has a different option value in the non-default store view than in the default store view, Elasticsearch now indexes that value or returns the product with that value in the results.
* Price sorting now works correctly for out-of-stock configurable products.
* The performance of catalog search has improved. Disabling **Enable Search Suggestions**  (**Stores** > **Configuration** > **Catalog** >  **Catalog Search**) works as expected.

Shipping
~~~~~~~~

* You can now ship an order to multiple addresses if one of the ordered products is a virtual product.

Sitemap
~~~~~~~

* The sitemap generation process now uses custom URL rewrites as expected.
* Encoded values are now correctly escaped in ``sitemap.xml``.

Store
~~~~~

* The store-view switcher now works correctly when the store views have different base URLs. Users are now redirected to the corresponding page, category, or product page on the new store view.
* You can now export ``config.php`` and default website code from one website to install and configure Magento on a second website in a multi-website deployment.
* Magento installation now completes successfully, and stores are created as expected, when store configuration is pre-defined in ``config.php``.

Swatches
~~~~~~~~

* You can now use  ``POST /V1/products/attributes`` to add a ``text_swatch`` type of product attribute.

Target Rule
~~~~~~~~~~~

* Loading of product details pages has been optimized. Indices for database tables that optimize target rule conditions queries for many cases have been added.

Theme
~~~~~

* Shoppers can now successfully change the number of orders per page in the order history multiple times..

* Themes that are added in User Agent Rules are now affected as expected when you run ``bin/magento catalog:images:resize``.

Translation and locales
~~~~~~~~~~~~~~~~~~~~~~~

* Inline translation now works as expected on the storefront when Admin **Stores** > **Configuration** > **Advanced** > **Developer** > **Translate Inline** > **Enabled for Storefront** is set.

UI
~~~

* Magento now preserves an attribute's value when you move the attribute from one group to another.

URL rewrites
~~~~~~~~~~~~

* Moving a store view to a different website no longer resets URLs.
* Magento no longer changes a product's URL in all stores when a merchant changes a product URL for one store in a multi-site deployment. 

Vertex
~~~~~~

* Taxes are now calculated as expected on orders that contain both physical and virtual products.
* Vertex now processes products with a price of 0 as expected.
* The checkout process now successfully progresses from shipping to payment when using Internet Explorer 11.x with Vertex.
* The process of submitting an invoice to Vertex has been optimized, and performance has improved.
* Tax details are now included as expected in the database.
* Log rotation now works as expected in production mode.
* Vertex now calculates taxes correctly when a default ZIP code is provided for tax calculation.
* Updating the billing address with Vertex's recommendation no longer updates the fields on the shipping address.

Visual Merchandiser
~~~~~~~~~~~~~~~~~~~

* You can now add products to a category when implementing Level 2 cache.

Web API framework
~~~~~~~~~~~~~~~~~

* Invoices created using the REST API now include gift card information similar to the invoices that are created in the Admin.
* The ``default_sort_by`` attribute now takes ``String`` instead of ``String[]``.
* You can now use POST ``http://<domain>/rest/V1/categories/`` to create or update a category.
* Bulk order updates using ``PUT /async/bulk/V1/orders/:id`` now update the order status as expected.

Wishlist
~~~~~~~~

* Administrators can now configure a configurable product that has been added by a customer to a wishlist from a non-default store.
* The **Add to cart** button on the shared wishlist page now works as expected for anonymous, guest, and users who are not logged in.