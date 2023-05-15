Magento Open Source 2.3.1 Release Notes
=======================================

**Official link**: https://devdocs.magento.com/guides/v2.3/release-notes/ReleaseNotes2.3.1OpenSource.html


Release notes published on March 26, 2019 and last edited on June 3, 2020.

We are pleased to present Magento Open Source 2.3.1. This release includes over 200 functional fixes to the core product, over 500 pull requests contributed by the community, and over 30 security enhancements.

This release includes significant contributions from our community members. These contributions range from minor clean-up of core code to the development of substantial features such as Inventory Management and GraphQL. Although code for these features is bundled with quarterly releases of the Magento core code, several of these projects (for example, Page Builder and Progressive Web Applications (PWA) Studio) are also released independently. Bug fixes for these projects are not documented in these core release notes but in separate project-specific sets of notes.


Merchant tool enhancements
--------------------------

Improved order creation workflow in the Admin
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* The Admin order creation workflow has been refactored to eliminate delays when editing billing and shipping addresses. Processing of these fields now happens only after they are populated.

Ability to upload PDP images without compression and downsizing
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* Merchants can now upload PDP images larger than 1920 x 1200  without first compressing and downsizing the images. Previously, when a merchant uploaded a high quality product image (larger than 1920 x 1200), Magento resized and compressed the image. Merchants can now set requirements for resizing and compression as well as compression quality and target width and height.

Inventory Management 1.1.0 (Community-developed feature!)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Magento Inventory (was MSI) community project has added multiple new features to this release of Inventory Management. See [Inventory Management Release Notes]({{ page.baseurl }}/inventory/release-notes.html) for information about specific fixes and acknowledgements to community contributors.

*  **Support for Elasticsearch and Inventory Management**. All site searches now return correct products and quantities when Elasticsearch is used as the search engine. (As of this release, only default option from 2.3+)  Searches return results from stock assigned to the website. Advanced features are supported, including filtering search results. Community-developed feature!

*  **Distance Priority Source Selection algorithm (SSA) option**. Merchants can enable this algorithm to reduce fulfillment costs by shipping orders from the closest inventory locations. This SSA option uses address geocoding through the Google Maps API to calculate the shortest distance for deliveries. 

*  **Enhancements to mass inventory transfers**. Bulk transfer of inventory has been optimized to improve processing speed and to reduce locking during transfers.

Improved developer experience
------------------------------

Progressive Web Apps (PWA) Studio
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

* PWA Studio is a set of developer tools that allow you to develop, deploy, and maintain a PWA storefront on top of Magento 2.x.

GraphQL
~~~~~~~

Community contributions for this release include major additions to cart actions (create cart, populate cart, set shipping address)  and customers (create customer account).

Substantial security enhancements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This release includes over 30 security enhancements that help close cross-site scripting, arbitrary code execution, and sensitive data disclosure vulnerabilities as well as other security issues. No confirmed attacks related to these issues have occurred to date. However, certain vulnerabilities can potentially be exploited to access customer information or take over administrator sessions. See `Magento Security Center <https://magento.com/security/patches/magento-2.3.1-2.2.8-and-2.1.17-security-update>`_ for a comprehensive discussion of these issues. All exploitable security issues fixed in this release (2.3.1) have been ported to 2.2.8, 2.1.17, 1.14.4.1, and 1.9.4.1, as appropriate.

Performance boosts
~~~~~~~~~~~~~~~~~~
*  Customer address handling has been rewritten with UI components that increase platform performance, which in turn streamlines the management of customers with 3000 and more addresses.

*  The Admin order creation page now handles  customer accounts with 3000 addresses without performance issues.

*  Magento now displays the list of additional customer addresses contained in the storefront customer address book  as a grid, which has improved performance for customers with many additional addresses associated with their accounts.

*  The shipping and billing data that a user enters during checkout now persists if the user interrupts checkout to continue shopping. Previously, checkout data was deleted after a cart update. 

Infrastructure improvements
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Infrastructure improvements are core enhancements that underlie both merchant and developer features.

*  This release includes a **new Authorize.Net extension** to replace the Authorize.Net Direct Post module, which implemented an MD5-based hash that Authorize.Net will no longer support as of June 28, 2019. See `Authorize.Net <https://docs.magento.com/m2/ce/user_guide/payment/authorize-net.html>`_ for information on configuring and using this new extension. Information about the deprecation of Authorize.Net Direct Post can be found `here <https://docs.magento.com/m2/ce/user_guide/payment/authorize-net-direct-post.html>`_. Note that Magento released a patch in late February to address this issue on pre-2.3.1 installations of Magento, which is discussed in `Update Authorize.Net Direct Post from MD5 to SHA-512 <https://support.magento.com/hc/en-us/articles/360024368392-Update-Authorize-Net-Direct-Post-from-MD5-to-SHA-512>`_.

*  `Accept.js` library is now used for Authorize.NET payments.

*  Magento now supports **Elasticsearch 6.x**. 

*  Update PayPal Express Checkout to `checkout.js v4`. This introduces a modernized checkout flow, faster checkout performance, and new payment options in a single integration that does not have to be updated as new payment methods become available. It also unlocks new payment options including Venmo and PayPal Credit.

*  Magento now supports **Redis 5.0**.

*  Magento support for PHP has changed slightly as a result of expanding our Elasticsearch support in this release. Magento 2.3.1 is compatible with PHP 7.2.x  and certified  on PHP 7.2.11.

*  You can now isolate and extract MySQL Views from regular database tables with no negative effects on database backup and restoration. Support for MySQL Views was introduced in 2.3.0 with unexpected consequences to the default database backups and restore mechanism. This fix restores expected  backup and restore functionality while preserving MySQL View support the backward compatibility with legacy inventory.

*  Magento now uses version 6.0 of the DHL XML Services schema for the DHL shipping method. <!--- MC-4245-->*

* **Checkout information now persists after a cart update**. Information previously entered by a customer during check out (such as shipping address) now persists after the customer updates their shopping cart. Previously, when a customer updated their shopping cart, all information previously entered during check out (such as shipping address) was deleted.

*  Upgrade of Magento Functional Test Framework (MFTF) to 2.3.13.

Bundled extension enhancements
------------------------------

This release of Magento includes extensions developed by third-party vendors.

Amazon Pay
~~~~~~~~~~

*  Added **multi-currency support** for  EU and U.K. merchants. 

dotdigital Engagement Cloud (formerly dotmailer)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*  dotmailer has been rebranded as dotdigital Engagement Cloud.

*  Support for Marketing preferences has been added to the customer account dashboard area.

*  If enabled, we now display the customer consent text in the customer's account dashboard area as the general subscription text.

*  The abandoned cart and automation process now benefits from a retry function if contacts are pending in dotdigital Engagement Cloud.

Magento Shipping
~~~~~~~~~~~~~~~~

New features for Magento 2.3.1 include:

*  **Shipment Cancellation**.  You can now cancel a shipment that has not yet been dispatched by accessing the shipment and clicking **Cancel Shipment**.

*  **Portal Access via Magento**. You can now access the Magento Shipping portal directly from Magento using the Magento Shipping credentials that are stored in your Magento instance.

Enhancements to existing features include:

*  Multiple improvements to the Shipment workflow user experience.

*  **Batch Processing**. Error messaging and field validation has been added to the batch processing workflow. See xxx for a description of other enhancements to batch processing.

*  **Collection Points**. Available Collection Points have been expanded to cater for both FedEx Hold at Locations and UPS Access Points.

*  Significant user interface changes have been made to the list of locations displayed during checkout. Opening and closing hours are now included when provided by the carrier.

*  **Click & Collect**. The list of Click & Collect locations in checkout has been brought in line with the new Collection Points list. For a description of the new Collection Points list, see xxx.

*  **Carrier Specific Packaging**. Carrier-specific packaging has been added for FedEx. These packages will be available for selection during shipping if a FedEx carrier is configured.

*  **Qualification Experience**. The three Qualification experiences (Ship to Address, Click & Collect, and Collection Points) have been restructured and are now available as outcomes in a single Qualification experience.

*  **Security**. We've closed scenarios that could allow for third-party code execution.

*  **Magento Cart Price Rules**. Cart price rules can now be applied to Magento Shipping.

*  **Dispatch**. We've added additional workflow capabilities during the dispatch process to cater for future carriers.

Vertex
~~~~~~

*  Added support for B2C VAT.

*  Added support for configurable logging.

Fixed issues
------------

We've fixed hundreds of issues in the Magento 2.3.1 core code.

Installation, upgrade, deployment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*  Magento now sets the `id_prefix` option on prefix cache keys for the cache frontend during installation. If this option is not set, Magento uses the first 12 bits of the md5 hash of the absolute path to the Magento `app/etc` directory. But if this value is not exactly the same on all web servers, cache invalidation will not work.


*  The `./bin/magento config:show` command no longer fails with a fatal error after you run `./bin/magento app:config:dump`.


*  The `bin/magento app:config:dump` command now disables all input fields as expected.


*  Administrators that have been assigned a backup module role resource can now access the backup controller as expected.


*  The `getHostUrl()` method has been updated to reference `HTTP_HOST` rather than `SERVER_PORT`.


*  Magento no longer displays an extraneous blank option in the country drop-down menu.


*  The front-end  now  uses HTTPS exclusively and back-end  uses HTTP without resulting in excessive redirects.


*  The `config:set --lock-config` command  now acts as expected on all scopes. Previously, after this command was run, administrators were not able to change the configuration for the default store, but could still change it for other scopes.

*  Magento now skips disabled modules  when compiling static content.


*  The `bin/magento setup:upgrade --convert-old-scripts=1` command now supports the conversion of indexes and constraints.


*  The commands to enable and disable debug logging have changed to `bin/magento setup:config:set --enable-debug-logging=true | false`.


*  The **Allow Dynamic Media URLs in Products and Categories** configuration setting, which was previously accessed from **Stores** > **Configuration** > **Catalog** > **Storefront**, has been removed. The **Use Static URLs for Media Content in WYSIWYG** setting (**Stores** > **Configuration** > **General** > **Content management** > **WYSIWYG Options**) now applies to any media URLs that are entered through the WYSIWYG editor.

Analytics
~~~~~~~~~

*  You can now save configuration from the **Admin**  > **Stores** > **Configuration** > **General** > **Advanced Reporting** without providing an industry value. Previously, Magento did not save configuration settings, and displayed this error:  `Please select a vertical.` 

Authorization
~~~~~~~~~~~~~

*  You can now successfully save a role from the Admin. Previously, when you saved a role from the Admin, Magento removed all  users from the role (no matter which checkbox was checked), and displayed this message: `This user has no tokens`.

Backend
~~~~~~~

*  `CustomerRepository::getList()` now loads custom attributes named `company`. 


*  Fixed icon behavior on product customization page.


*  The **Reload Data** button on the Admin now works as expected. 

Bundle
~~~~~~~

*  Bundle special prices are now correctly rounded when you load and resave a bundle product. Previously, when you reloaded a bundle with a special price that requires four positions after the decimal (for example, 78,9473), Magento rounded the price to two decimal places. 


*  The Bundle Product Option Repository Delete method now removes the correct option. Previously, it removed the first option, regardless of the `optionId` that was specified. 

*  Magento no longer overwrites user-defined option quantities with default values when a customer edits a bundle product from a shopping cart.


*  You can now successfully change the attribute set for a bundle product. Previously, the edit bundle page hung, and Magento threw this error: `Uncaught TypeError: Cannot read property 'length' of undefined`.


*  Magento now maintains the correct base price for a bundle product when you add a bundle product in one currency and then add the same bundle product option in a different currency. Previously, when you added the same bundle product option in a different currency, Magento doubled the base price.


*  Bundle product SKUs are now built based on the order of the associated (selected) product ID numbers in ascending order. Previously, SKUs were built based on the order of the selected product ID numbers in ascending order instead of the order in which the option is added to the bundle product. 


*  Magento now adds all selected values to the cart when a customer adds a bundle product option with input type checkbox. Previously, if a bundle product had three values, Magento added only two options to the cart. 

*  Fixed inconsistently sized title box border on the edit bundle product page when adding an item to a bundle product from the Admin.


*  You can now add a bundle product to a requisition list from the category page. Previously, Magento threw this error: `PHP Fatal error: Uncaught Error: Call to a member function getParentProductId() on string in app/code/Magento/RequisitionList/Model/RequisitionListItem/Options/Builder.php:118`.

CAPTCHA
~~~~~~~

*  CAPTCHA now appears as expected in the Log in pop-up window.

Cart and checkout
~~~~~~~~~~~~~~~~~

*  Magento now displays a product's special price on the storefront, product listings, and product detail page as expected when the special price is 0.00. Previously, Magento displayed the regular price, but used the special price for sorting and quote calculations.

*  Custom shipping methods in custom carrier code can now include underscores.


*  Magento no longer displays the infinite loading indicator when an error occurs during check out. 


*  The **Clear shopping cart** button now works as expected. Previously, the page reloaded, but the shopping cart was not cleared.


*  Magento now dispatches a `checkout_cart_product_add_before` event in addition to a `checkout_cart_product_add_after` event.


*  Customer address attribute validation during checkout now permits spaces.


*  Clicking multiple times on the mini cart icon no longer logs out the current customer. Previously, when a logged-in customer added a product to the cart and then clicked the shopping cart icon multiple times, Magento displayed an empty shopping cart and logged out the customer.


*  Customers can now configure options for a configurable product after adding it to their shopping cart.  Previously, under these circumstances, Magento threw a fatal error.


*  Magento now validates zip codes for new addresses as expected when the **My billing and shipping address are the same** option is unchecked.


*  Magento now updates the mini cart as expected when an administrator updates the product from the Admin. Previously, if a product that had been added to the shopping cart was subsequently disabled from the Admin,  the product was still displayed in the cart.


*  Magento now uses the configured default sort order  during checkout to calculate totals. Previously, Magento ignored the configured order and used **Sub Total** > **Shipping** > **Discount** > **Tax** > **Grand Total** to calculate order totals.


*  Magento now displays informative error messages when an order paid for with Authorize.Net fails.


*  Magento now displays the correct status for orders with zero subtotals. Previously, new order status appeared as pending when it was processing.


*  Expired gift cards are no longer applied to a customer's account. Previously, if a gift card applied to a customer account expired, Magento could not complete the checkout process.


*  Magento no longer removes the billing and shipping address information for an order when a customer cancels an order by clicking **Cancel and Return** when  using PayPal Website Payments Pro Hosted Solution. Previously, when a customer placed an order and then clicked the **Cancel and Return** link, Magento removed the billing/shipping address and displayed an error.


*  You can now update the quantity of grouped product  if the quantity field was left empty when initially added to an Admin order by SKU. Previously, under these circumstances, you could not update the quantity.


*  After a session expires, and a customer refreshes the page, Magento displays an empty shopping cart and logs out the customer as expected. Previously, Magento displayed an empty shopping cart but the mini cart still displayed the selected items, and if the customer refreshed the page again, the shopping cart displayed the items.


*  Tooltips that are available from the checkout page on mobile devices are now displayed properly. Previously, customers had to scroll to access the tooltip.


*  `\Magento\Checkout\Observer\SalesQuoteSaveAfterObserver` now updates the checkout session quote ID as needed.

*  Magento now validates shipping address of a logged-in user using the default shipping address during checkout. 


*  Fixed issue displaying numbers than exceed two digits in the **Qty:** box of the **Proceed to Checkout** pop up. 

*  Added a missing space between the title of the workflow step and the saved address on the first page of the checkout process. 

*  Magento no longer throws a console error during a guest checkout when the list of allowed countries is changed from the Admin. 

*  The title of the shipping method no longer overlaps with **Edit** on the checkout page. 

*  The **Close** button on the mini cart now longer overlaps with the shipping section when the checkout page is opened on a mobile device.


*  Fixed the alignment of the **Apply discount** button  on the checkout page. 

*  Fixed mini cart layout issues.


*  The mini cart is now updated as expected when a product in the cart is disabled.


*  Magento no longer displays a console error when a customer selects one-step checkout. Previously, Magento displayed this JavaScript error: `Cannot read property 'code' of undefined`.


*  Fixed problems with the display of the tooltip drop-down pointer on the checkout page in tablet view. 

Cart Price rules
~~~~~~~~~~~~~~~~

*  The Cart Price Rule page now displays correct counter values for the grid and accurate pagination.


*  Magento no longer permits you to use the up and down arrow keys to enter negative numbers when entering a credit card number on the payment information page during checkout.

Catalog
~~~~~~~

*  Magento now displays the product page with this message `You need to choose options for your item` when you click **Add to cart** for a new product that has an attribute with the **Use in product listing** property set to **Yes**. Previously, Magento redirected the user to the cart page, and did not add the product to the cart. 


*  Magento now directs the user to a 404 page when accessing http://www.domain.com/catalog/product/compare. Previously, Magento threw this error, `Fatal error: Uncaught Error: Cannot call abstract method Magento\Framework\App\ActionInterface::execute()`. 


*  Magento now correctly calculates fixed tier price discount for products with special prices.

*  Magento no longer throws an exception when you try to add an image to a product programmatically.


*  Magento now applies the translations for the selected theme when you enable a custom design theme. Previously, Magento collected the translation files for the active main theme only, which limited the use of different translations within the additional theme. 

*  The `bin/magento catalog:images:resize` command now processes all specified images. 

*  You can now create a new product with a special price. Previously, when you saved the newly created product, Magento threw this error: `Special price date from" Failed to parse time string`. 


*  You can now insert multiple catalog product list widgets into a CMS page.


*  You can now use REST to add a new attribute and configure it with settings such as `is_filterable`. 


*  Magento now provides a white-space trimming function for SKUs on the Admin.
*  Magento no longer changes the attribute type of `backend_type` from `varchar` to `int` when the product associated with the attribute is saved or updated in the Admin. 

*  The table rate shipping method no longer fails to return a quote when a customer uses a United States  post code in the form of *five-digit zip - four-digit* extension (for example, 44444-1234). 


*  You can now set a Boolean attribute to `is_filterable`, which allows these attributes to be included in layered navigation. 


*  `getStoreId()` now consistently returns `int`. Previously, Magento returned `string` for products but `int` for categories, which resulted in a fatal error. 


*  `\Magento\Catalog\Model\Product::getQty()` now consistently returns float/double. 


*  Updates to related products now appear as expected in both the storefront product page and the Admin product edit page. Previously, the storefront displayed product updates, but not all related product updates showed up in the Admin. 


*  The `bin/magento module:uninstall` command  now works as expected with Composer. Previously, there was a discrepancy between `composer.lock` and `composer.json` when this command was used to remove a module.


*  `getStoreId()` now consistently returns `int`. 


*  You can now save a product on deployments in single-store mode when the default website has been removed and a new website has been added.

*  Attribute values are now updated as expected in the `catalog_product_flat_2` table.


*  Magento now saves and properly indexes a configurable product variant that contains a longer-than-permitted SKU. Previously, when you tried to save this product, Magento threw an error. 


*  The product page's Recently View section no longer displays the name of the current product.


*  You can now use REST to update a product's media gallery.


*  Magento now saves default values for category URL paths in accordance with the **Use Default Value**  and **Create a Permanent Redirect** settings. Previously, in deployments running multiple stores, if a category's URL key was changed and saved, Magento did not change the category's URL key back to the default URL key when saved with the **Use Default Value** box checked and **Create a Permanent Redirect** box unchecked.


*  Magnifier now correctly handles zoomed sections of images when the image width/height ratio has a `~2x` difference. Previously, these sections were distorted.


*  Magento now retains across categories any value you set for the number of categories displayed per page.


*  You can now save products with at least one tier price.


*  Changes to product images made under the All Stores scope now affect product images at the store-view level.


*  You can now use REST to update category positions.


*  Magento now correctly displays the greater than operator (>) when you configure the catalog products list widget for a CMS block.


*  Categories that are set to anchor **Yes** and that have disabled subcategories no longer display  products from those disabled subcategories.


*  You can sort a grouped product's associated products across multiple pages. Previously, when you tried to sort associated products, Magento sorted only the products visible on the current page.


*  Magento now uses the correct column type when creating temporary tables for a flat catalog. 


*  Attribute indexing no longer ignores custom source model options, and the attributes associated with a custom source model were not parsed when products were filtered. Previously, when Magento indexed the attribute values used for the product filters in the category overview, it indexed only multiselect attributes that used attribute options. If a custom source model was specified, Magento did not index its values, which were consequently not taken into account when  products were filtered. 


*  Magento now correctly imports  `product_type` drop-down attributes. Previously, Magento displayed an error message indicating that values for these attributes were incorrect during import. 

*  Magento now correctly handles attribute options that begin with zero. Previously, these attribute options  did not work if an option with the same number but lacking the zero already existed. 

*  You can now successfully delete a newly created attribute set. Previously, Magento displayed a 404 error under these circumstances. 


*  You can now use add extension attributes to add category links to a product. Previously, Magento did not add the product links but behaved unpredictably. 


*  When a new customer is created, Magento sets a value of zero for any custom attribute if no other value is explicitly provided. Previously, if no value was explicitly assigned, Magento did not save the custom attribute with any value. 

*  `CategoryLinkReposity` now lists all possible exceptions.

*  Merchants can now assign negative values to custom option for a product with a fixed price from the Admin.


*  Newly added fields are now sorted according to the given `sortOrder` value in the newsletter system configuration file. Previously, you could add a new field, but could not successfully set its position. 


*  Merchants can now change the position of tabs on a product page. 


*  An incorrect variable in the phpDoc for `DataBuilder.php` has been corrected. 


*  You can now perform a mass  update  on product attributes after configuring the minimum cart quantity globally. Previously, Magento did not display the form to update all available attributes but threw a `E_WARNING:` error when you selected **Update attributes**.


*  The product compare page now loads as expected when unconfigured attributes display **N/A** or **No**. 

*  Magento now correctly sorts configurable products with tier prices or swatches on both the storefront and Admin. Previously, storefront sorting did not match Admin sorting. 


*  Magento now correctly duplicates video files when a merchant duplicates a product with an associated video. Previously, the video was duplicated as an image, not a video, and the merchant had to delete the image and re-add the video using **Add Video**.


*  Browser no longer hangs when you add a product by SKU to a category


*  We've improved the error message that Magento displays when validating a new (but invalid) product attribute. 

*  `getProductUrl` no longer returns the wrong URL when the current category has no products. 

*  The user agent exception now sets the correct templates for product pages. Previously, the `footer.phtml` and `absolute_footer.phtml` templates were loaded from the desktop theme instead of the mobile theme regardless of the user agent. 


*  Magento now displays currency symbols as expected for products in the Cost column of the Admin catalog list.  


*  Magento now displays breadcrumbs in proper format. Previously, subcategories did not appear in breadcrumbs. 


*  In a multi-website instance, with a category that contains products belonging to different websites, when the product sort order in a category is changed at the store-view level, the products that belong to a different website gets unassigned from the category.

CatalogInventory
~~~~~~~~~~~~~~~~

*  Magento now validates the quantity of items in the shoppng cart against the **Maximum Qty Allowed in Shopping Cart** setting.

*  Magento now correctly applies the **Set Items' Status to be In Stock When Order is Cancelled** attribute setting. Previously, after an order was canceled, Magento increased product stock even when **Set Items' Status to be In Stock When Order is Cancelled** is set to **no**. 

*  Removed unnecessary slash from `app/code/Magento/CatalogInventory/etc/di.xml`. This extraneous slash had previously resulted in `Magento\Catalog\Api\ProductRenderListInterface` returning products regardless of visibility. 

*  Magento no longer displays a negative value on the product list page when a product's stock falls below the product's `OutOfStock` threshold value.

*  Magento no longer increments stock for products for which stock managing has been disabled. Previously, Magento increased the product quantity count when an order failed if **Manage Stock** was disabled. 


*  In a multi-website instance, with a category that contains products belonging to different websites, when the product sort order in a category is changed at the store-view level, the products that belong to a different website gets unassigned from the category.

Catalog Rule
~~~~~~~~~~~~

*  Magento no longer throws an exception when you try to edit and save a catalog price rule when the Admin language is set to a language other than English. 


*  If you create a catalog price rule based on categories with a nesting level 4 or higher, these categories now maintain the status of their checkboxes when you re-open Category Chooser. Previously, when you reopened these categories, no checkboxes were checked.

Catalog URL rewrite
~~~~~~~~~~~~~~~~~~~

*  Magento now regenerates product URL rewrites as expected after an administrator changes a product URL key from the Admin and subsequently saves the product attribute URL path value. Previously, product URL rewrites could not be generated after this attribute value was changed. 


*  Attempts to rewrite catalog URLs with `POST /V1/products` endpoint now  work as expected.


*  Magento no longer ignores the store-level `url_key` of child categories when rewriting URLs process for global scope. 


*  Magento no longer removes product tier prices when a schedule update contains an update to the special price.


*  The store switcher now works in multistore deployments.  Previously, the switcher redirected the user to the home page, not to the alternative store view as expected. 


*  Fixed alignment of the details label on the order page in mobile view. 


*  Fixed rendering of the **Add your text** link on the Product page. 


*  Corrected the alignment of Contact us area accessed from the storefront page footers. 

*  Fixed misalignment of page elements on the manage coupon codes page in the Admin. 

*  Fixed misalignment of tax rate checkbox on the Add New Tax Rate page. 

*  Fixed misalignment of the attribute set name heading border on the Attribute sets pop up. 


*  Fixed misalignment of elements on the shipping information page that Magento displays when you click **Check Out with Multiple Addresses** from the shopping cart.


*  Fixed misalignment  of the **Choose file** button on the `Select File to Import` page. 


*  Fixed formatting of the add link table that can be accessed from the Downloadable Information tab. 


*  Fixed misalignment of the title of the order page accessed when you check a recent order in the sidebar of listing pages or account pages. 

*  Fixed misalignment of  tab content on the product page in mobile view.

*  Corrected misspelled argument name `allowDrug` to `allowDrag` in `vendor/magento/module-catalog/view/adminhtml/templates/catalog/product/attribute/set/main.phtml`. 


*  Fixed the misalignment of the customizable options label on **Admin** > **Catalog** > **Product** > **Customizable Options**.

*  Fixed problem with overlapping UI elements on the cart page when accessed from the mini cart. 


*  Fixed alignment issue with the dropdown menu on the mini cart. 


*  Fixed alignment issue with radio buttons on the shopping cart page. 

*  Fixed alignment of the bundle product radio button on the product page when you click **Customize** and **Add to cart**. 

*  Fixed alignment of the bundle product information on the configure product page for a bundle product  when creating a new order. 

*  The calender icon issue is now correctly aligned on the Advanced Pricing page of the Admin. 

*  Fixed alignment issue of time fields in **Admin** > **Configuration** > **General** > **Advanced Reporting** in tablet landscape view. 


*  Fixed misalignment of the confirmation pop-up window that Magento displays in mobile view when you delete a product from your shopping cart. 

*  The `addExpressionFieldToSelect` method no longer modifies columns and instead insert expression into `_fieldsToSelect` private variable (just as `addFieldToSelect` does). 


*  A typo in `app/code/Magento/Deploy/Console/DeployStaticOptions.php` has been corrected.


*  Fixed alignment of options on the admin edit widget page. 


*  Corrected rendering of the apply discount code field in the Tab portrait view of the cart page.


*  Fixed issue where the horizontal scroll bar did not appear as expected on the compare products page in mobile view. 

*  Added missing bottom border to list of customizable options on the product page accessed from the Admin. 

*  Corrected the position of the header for the design configuration table (**Content** > **Design** > **Configuration**). 


*  When you try to save a widget that contains an unexpected character, Magento now displays an informative error message  and does not save the widget. Previously, Magento saved the widget. 


*  The catalog category merchandiser product list is no longer missing the move cursor in tile view. 


*  Corrected alignment of the **Detailed Rating** field on the Edit Review page.

*  Corrected alignment of the store switcher in Tab view. 

*  Corrected number of products listed per row for  desktop (4), tablet (3),  and mobile (2) views. 


*  Hamburger menus no longer appear on page that does not have menus. 

*  Fixed issue where drop-down toggle arrow did not close as expected on product page. 

*  The Send email confirmation popup **Close** button no longer overlaps with content. 

*  Corrected formatting issue on **Catalog** > **Category** > **Product** > **Assign products** page.


*  Store switcher now works correctly on mobile devices.

*  The order view invoice template is now displayed properly on the ipad. 

*  Fixed misalignment of the widget options on the edit widget page. 

*  Magento now identifies shipping method in the Shipping section of the order review page for orders paid with using PayPal Express. 


*  Fixed checkbox alignment on the account information page. 

*  Fixed misalignment of search icons on the `onAttribute` page. 


*  Fixed alignment issue with select and text boxes on the Advance Pricing page. 


*  Corrected alignment issue with elements on the default email templates.

*  Corrected typo in `SalesRule/Model/ResourceModel/Coupon/Usage.php`. 

*  Corrected the behavior of the Option's New Option Type drop-down menu for customizable options. 


*  Fixed alignment of reload CAPTCHA icon on the Admin  login  page. 

*  Fixed alignment of error message that magento displays on the add or edit bundle product customizable options tab. 


*  Fixed misalignment of the Orders and Returns section that is accessed from the footer of the Orders page. 


*  The default design of the **Edit** and **Remove items** buttons on the wishlist page now match. 

*  Fixed issues with the shadows associated with input box and radio buttons on storefront forms. 

*  Fixed the misalignment of the product option fields in the order summary of the checkout page. 
*  Fixed misalignment of fields on the configure product page that is accessed from the wishlist. 


*  Removed excessive white space from the top of CMS pages when displayed in mobile view.


*  Fixed misalignment of logo on Admin home page.


*  Fixed misalignment of the advanced search page's price field in mobile view. 


*  Fixed misalignment of the View and Edit Cart link in the mini cart. 

*  The Widget Options left navigation block on the Add New widget Page now displays correctly in tablet view.

*  Fixed misalignment of values in the currency rate column in the Order & Account Information area of the New Memo page. 


*  Added missing PHPDoc comment for methods throughout the code base. 

*  Fixed misalignment of the My Account page's **Recently Ordered** checkbox in  tab portrait view. 


*  Fixed misalignment of **Schedule Update From** field on the Admin category page when displayed in a browser set to 768 x 1147 resolution. 


*  Fixed misalignment of reviews under My Recent Reviews area of the My account dashboard. 

*  Fixed irregularities with  updating order status.


*  The `ui-component` validation `error` event now bubbles upwards when an abstract element is nested in a field set. 

CMS content
~~~~~~~~~~~

*  You can now delete from the media gallery browser any files and folders that are symlinked in `pub/media`. Previously, the Magento left the image in the media gallery but gave you no feedback in the product interface.


*  Improved the display of images that are uploaded when you click the **Insert Image** button on a CMS page. 

Configurable products
~~~~~~~~~~~~~~~~~~~~~

*  The DateTime class can now parse strings for all supported languages, not just English. Previously, converting from string to PHP DateTime object  failed for locales other than `en_US`. 

*  Selected images on the product page of a configurable product are now positioned correctly.


*  You can now successfully save products  with SKU lengths that are less than or equal to 64 digits. Previously, Magento threw a fatal error when you tried to re-save a child product after reducing the length of its 64-digit-long SKU. 


*  The Cart Sales Rule now excludes already discounted products from further discounting through a coupon code. 


*  Translations for `tier_price.phtml` now works as expected. Previously, these translations were not included in `js-translation.json`, and not visible on the storefront. 


*  **Sorting by a price** for configurable products on category pages now works correctly when the **Display Out of Stock Products** setting is enabled.

cron
~~~~

*  A new `cron.log` file dedicated to logging cron-related information has been added to Magento. This new log file reduces output previously sent to the `system.log` file, making it easier to find non-cron-related information in the `system.log` file. 

Customers
~~~~~~~~~

*  We've added an additional check for the password hash for  customers that have been  created without a password from the Admin. Previously, customers created this way could not log in. 

*  Magento now displays the same order total in  the customer information orders grid and orders grid when an order is placed in a currency other than the base currency. Previously, Magento displayed the wrong order total in the Admin's customer information orders tab.


*  Magento no longer displays the forgot password form while a customer is logged in but instead directs the customer to the customer dashboard.


*  The reset password link in the password reset mail sent to customers when they click **Reset password** on the login page now permits customers to reset their password as expected. 


*  Magento now maintains alphabetical order for customer groups when you filter customers by group in the Admin.  Previously, groups were sorted by ID.


*  Merchants can now edit a customer account if the customer's password has expired. 


*  Magento now displays the value of a custom customer address attribute  in the column for that attribute when you create a custom customer address attribute and set it to be displayed in the Columns list.  Previously, Magento added the customer code column to the Customer table, but left these columns blank.


*  You can now change payment methods after selecting store credit when creating an order from the Admin.


*  Customers can now be matched in customer segments based on the number of orders in a multi-site deployment.


*  We've improved the performance of the customer segment rule, which has improved site performance.


*  Magento no longer unchecks the default billing and shipping address checkboxes when you create or update a customer address using the API.


*  Magento now displays the list of additional customer addresses contained in the storefront customer address book  as a grid, which has improved performance for customers with many additional addresses associated with their accounts.


*  When a customer uses a gift card to make a purchase, Magento now applies only the applicable amount to the invoice. Previously, the total amount of the gift card was applied to a customer's store credit for a partial invoice.


*  Magento now assigns new accounts in multisite deployments  to the customer group that is associated with the default website scope. Previously, a new customer created from the Admin  had their customer group set to the default customer group on the default website scope.


*  Customers who have an address associated with a country that has not been set to **allowed** can now successfully reset their password.


*  Removed an unneeded space from the title of the My Account page in mobile view. 


*  Removed an empty block on the My Account page sidebar. 


*  The `Magento\Customer\Model\Customer::getDataModel` method has been optimized, which has reduced the time required to load customer accounts with many addresses.


*  **State/Province** field values are no longer required when creating an order from the Admin. Previously, Magento indicated that **State/Province** field values were required even though configuration settings indicated these values were not required.


*  Images can now by default be successfully imported from HTTP and redirected to HTTPS. Previously, the image could not be uploaded. 

*  Magento now respects the number of lines permitted in a street address as set in  **Store** > **Configuration** > **Customer** > **Customer Configuration** > **Name and Address Options**. Previously, Magento displayed the last saved values instead of the default value.

Customer attributes
~~~~~~~~~~~~~~~~~~~

*  Magento now loads the customer attribute page as expected, and users can edit attributes, when attributes are set to default values. Previously, Magento did not completely load this page when attributes values were set to default.


*  Custom customer address attributes can now be updated when you edit an order's billing address in the Admin.


*  You can now create a customer without a phone number when **Show Telephone** is set to optional. Previously, Magento displayed an informative error message and did not let you create the customer.


*  Magento now saves customer custom attributes as expected when with EAV caching is disabled.  Previously, directly saving customer information resulted in data loss. 

Dashboard
~~~~~~~~~

*  You can now upload PDP images larger than 1920 x 1200  without compressing and downsizing the images first. Previously, when a merchant uploaded a high quality product image (larger than 1920X1200), Magento resized and compressed the image. Merchants can now set requirements for resizing and compression as well as compression quality and target width and height.


*  `_sleep` and `__wakeup` have been removed, and a new `PHP.MD` rule has been added to discourage PHP serialization.


*  Magento now validates new addresses when created from the address book telephone field on the My Account dashboard page.

Developer
~~~~~~~~~

*  Email messages sent from the command line (where the email loads into another block) can now be sent successfully. 

Directory
~~~~~~~~~

*  The Swagger definition for eav-data-attribute-option-interface has been corrected. Previously, when you created a REST call to an endpoint that returns an object of `eav-data-attribute-option-interface` and `is_default` is to `true`, `is_default` returns an object instead of the expected Boolean.


*  `crontab` now updates all currency rates daily  as expected. Previously, `crontab` updated only a subset of the enabled currencies. 

Downloadable
~~~~~~~~~~~~

*  Order confirmation email sent when a guest checks out now includes download links as expected.


*  You can now delete downloadable product links without first deleting sample links.

EAV
~~~

*  You can now use the `OptionManagement.delete` method to programmatically delete a product attribute that converts to false. Previously, Magento threw an exception. 


*  You can now use an attribute set on the product create page after moving the attributes from one attribute group to another.


*  The customer EAV decimal attribute now accepts a value of 0. 


*  The Magento storefront now correctly displays products with a custom attribute of type  `Media Image`. 


*  Magento no longer changes the `source_model` when you create an attribute option through the API. Previously, the `source_model` of an EAV attribute was set to `Magento\Eav\Model\Entity\Attribute\Source\Table` when updating an EAV attribute's options through the API. This eliminated the ability to update this attribute's options through the Admin. 

*  Magento no longer throws an SQL Join error when you use a custom EAV entity  with the `standard eav_entity` entity table. Previously, this usage resulted in an integrity constraint violation. 

Email
~~~~~

*  The return path e-mail variable `system/smtp/return_path_email` now works as expected.


*  Email subject headers now support UTF-8 encoding.

Frameworks
~~~~~~~~~~

*  Magento no longer logs an error when you include properly escaped special characters in the store view names. Previously, Magento logged errors in the `exception.log`.


*  Magento now attempts to reconnect when a MySQL timeout occurs. Previously, Magento displayed an informative PHP-related message and did not attempt to reconnect.


*  You can now set all products that currently have **Set Product as New** set to **yes** set to **no**. This change affects bulk updates, CSV imports, and scheduled updates.


*  Attributes in flat tables are now updated after the product is saved when the catalog product flat index is turned on and the indexer is set to **Save on Update**.


*  `dev/tools/grunt/configs/themes.js` has been removed from the `.gitignore` file and added to the github repository. Previously, `localthemes.js` was included in the `.gitignore` and replaced during a Magento update.

*  Magento now autoloads vendor root folders and can now run with custom Composer vendor directories. Previously, Magento's autoloader registration failed to generate the correct path when using the `COMPOSER_VENDOR_DIR` setting to specify a vendor path outside of the Magento installation root.


*  Newly added links on the customer dashboard are now shown as current as expected when the link path has been constructed from both default and new elements. Previously, the link was added, but not shown in the current state as expected. 


*  The `fileUploader` form element in `ui_component` form now works as expected. Previously, during file upload, the countable interface not implemented, and Magento threw this error: `Error Message : Warning: count(): Parameter must be an array or an object that implements Countable in <base_dir>/vendor/magento/framework/File/Uploader.php on line 550`. 


*  Interception cache compilation has been improved, and custom profiler records are now executed in less than a second. Previously, profiled methods consumed about 70% of the first page load after `cache:flush` from either the command-line interface or the Admin. 

*  `Magento\Framework\Webapi\Rest\Response\Renderer` class's  `_formatValue` method has been refactored to handle ampersands correctly. Previously, an ampersand in any customer text field when using the WebApi doubled the encoding.


*  Deprecated interface `\Magento\Framework\Option\ArrayInterface` has been replaced with `\Magento\Framework\Data\OptionSourceInterface` in `lib/internal/Magento/Framework/Option/ArrayPool.php`.


*  Corrected invalid return type in docblock in `Magento\Framework\HTTP\PhpEnvironment\Request::getHeader()`. Previously, the docblock of the  `Magento\Framework\HTTP\PhpEnvironment\Request::getHeader()` method stated that it would return a `bool` or an instance of `Zend\Http\Header\HeaderInterface()`. However, this method returned either a `bool` or a `string`. 


*  Magento now throws `LogicException($message, 0, $e)` instead of `LogicException($message)` as needed when running validation for communication configuration (`communication.xml`).  Previously, the  validator in `Magento\Framework\Communication\Config\Validator` did not propagate exceptions, which obscured the cause of the error. 


*  JavaScript translation issues on the modal buttons that Magento displays when removing items from product compare page have been resolved. 


*  `Magento/Framework/HTTP/Adapter/Curl.php` now supports setting an HTTP version. 

*  Magento can now read responses from third-party servers that use HTTP/2 if your server also uses HTTP/2. Previously, this inability to read requests from third-party servers that use HTTP/2 prevented access to Commerce Marketplace.  


*  The AMQP helper has been updated to use host, username, and password configuration from the instance under test. This allows tests to run when the AMQP service is not using default credentials or available on `localhost`. Previously, the `host` value in this helper was hardcoded.


*  We've added support for `use` statements in web API interfaces and the use of non-FQN class names in `doctypes`. Previously,  you could not  import class names in interfaces used for web API. 

Cache framework
'''''''''''''''

*  The images cache can now be flushed from the Admin (**Admin** > **System** > **Cache Management** and click **Flush Catalog Images Cache**). Previously, you could not delete the directory, and Magento displayed an error on the cache management page.


*  Magento now removes disabled products as expected from the flat product table when **Catalog Flat Product** is enabled.

Configuration framework
'''''''''''''''''''''''

*  You can now enable shared catalogs using the `config:set` command. Previously, this command enabled the shared catalog but did not create the necessary permissions to access it.

Data framework
''''''''''''''

*  Class `\Magento\Framework\Data\Form\Element\Fieldset` now calls the `getBeforeElementHtml` method. 

Event framework
''''''''''''''''

*  `events.xml` can now have child nodes. 

JavaScript framework
''''''''''''''''''''

*  Wishlist names can now contain apostrophes. Previously, a wishlist whose name contained an apostrophe could not be edited or deleted.

Message framework
'''''''''''''''''

*  Module names can now contain numbers. Previously, `magento/framework-message-queue/etc/queue_base.xml` contained a pattern that did not allow numbers to be used in `instanceType`, which resulted in the invalidation of custom message consumers in this file.

General fixes
~~~~~~~~~~~~~

*  The navigation arrows in fotorama now stay visible after you close the zoomed fotorama. 


*  You can now customize the view of tab and accordion components by using mixins to redefine the default variables in the scope of a custom theme. 


*  Content in  confirmation popups on the Admin no longer overlap the **Close** button. 


*  You can now update database credentials from the command line in non-interactive mode using `bin/magento setup:config:set`.


*  The error message displayed on the Add Product Attribute page has been improved.


*  The datepicker icon is now correctly aligned in the Admin.


*  The magnifier now disappears as expected when a user moves their cursor off an image. 


*  Product pages that are included in a related products rule that uses a Price (percentage) condition now load correctly. Previously, loaded pages were blank.


*  Magento now displays the appropriate thumbnail image for configurable products in requisition lists. Previously, Magento displayed the default placeholder thumbnail image for all configurable products.


*  Magento no longer displays a console error when a customer selects one step checkout. Previously, Magento displayed this JavaScript error: `Cannot read property 'code' of undefined`. 

*  The **Select All** and **Select Visible** buttons on the notification page now work as expected. Previously, these buttons behaved the same.

*  The note that describes the **Use in Layered Navigation: Filterable (no results)**  property now better describes the property.

*  Magento no longer throws SQL errors when table prefixes are used. 

Gift cards
~~~~~~~~~~

*  Magento now consistently validates gift card prices according to the constraints of the relevant store locale.


*  Fixed the rendering of the check notifications counters icon on the Admin. 


*  `old_path: new_path` path mappings have been added for JavaScript files have been relocated to `requirejs-config.js`. 

*  Calling `getCurrentUrl` on a store no longer adds the  `___store` parameter when **store code in URL** is set to **yes** and the current store is not the same store requested in the URL.

*  The **Click for price** button on the home page now works as expected.

Gift message
~~~~~~~~~~~~

*  Magento no longer displays unselected gift options when a customer selects **Check Out with Multiple Addresses** for an order. Previously, Magento displayed unselected gift options for the order.


*  Fixed misalignment of the **Edit** and **Remove** buttons on the gift option popup that Magento displays when a customer adds a product to the shopping cart.

Gift registry
~~~~~~~~~~~~~

*  Magento now shows the correct price for configurable products in a shared gift registry. Previously, Magento displayed the original price instead of the special price for configurable products.

Gift wrapping
~~~~~~~~~~~~~

*  You can now add gift wrapping to the shopping cart to an already added product without having to add an additional product.

Google Analytics
~~~~~~~~~~~~~~~~

*  `referenceContainer` has been changed to `referenceBlock` in the Google Analytics module. 

Import/export
~~~~~~~~~~~~~

*  Magento now displays an informative error after you run check data, and also blocks import and product creation, when SKU strings are too long. Previously, the check data process permitted you to proceed with the import, but the import failed due to a system error. Products were created with excessively long strings were created with all the values except SKU empty.


*  Magento now successfully imports products  that have a fixed price custom option with a price of zero. Previously,  the importer failed when trying to update products with a price of zero. 


*  The memory required to export the media gallery has been significantly reduced. 


*  We've resolved the following issues with imported images:

   *  images of all sizes reverted to the default placeholder size after import.
   *  images that were removed through the Admin before import returned after import. Magento now displays an informative error message if images are not imported as expected.


*  Special characters in the CSV import file no longer trigger a general system exception. Previously, special characters (for example, <code>ƒ</code>, <code>ª</code>, and <code>›</code>) halted the check data phase of import.


*  URL Key columns that contain  accented characters are now converted properly after the import of a CSV file. Previously, if you manually assigned a URL key to a product in the Admin that contained an accent character or punctuation, Magento converted it to the regular character or removed it.


*  Magento now correctly updates existing product URLs during import. Previously, Magento update existing URLs with the new URLs, but displayed a 404 error if you tried to access the product from the new URL.


*  Magento now retains product order within a category after import.


*  You can now properly set data for drop-down attributes during product import in deployments with multiple storeviews.


*  Magento now prompts you to enter a valid value when you enter a value of zero for a customer group price discount by percentage when setting advanced pricing for a product.  Previously, Magento threw an error.


*  The import process now supports `add_update` along with the default behavior `append`. 


*  The upsert category process during product import now generates freshly created category URL rewrites globally and not just for the default scope. Previously, Magento created URL rewrites for the default website scope only. 

*  Magento now indicates correct stock status (in stock/out-of-stock) after importing products that have an indicated quantity but a status of out-of-stock from a CSV file. Previously, Magento imported the product quantity correctly, but not the stock status. 


*  We've resolved multiple issues that users previously encountered when importing configurable products with images and virtual products. Previously, image import failed under certain circumstances, and Magento displayed these messages:  `Imported resource (image) could not be downloaded from external resource due to timeout or access permissions in row(s)` and `Products are imported but configurable product has no image in Magento`.  


*  `\Magento\ImportExport\Block\Adminhtml\Export\Filter::_getSelectHtmlWithValue()` method no longer overwrites the `$value` argument. Previously, the same name was used for different `$value` variables. 


*  Fixed misalignment of the import successful  message icon  in the Admin. 


*  Magento now exports configurable products based on swatches with the correct Admin and Default Store View labels. Previously, after import the `configurable_variations` column for these configurable products contained the wrong values.

Infrastructure
~~~~~~~~~~~~~~

*  Magento now supports Elasticsearch 6.x. 


*  Magento now supports Redis 5.0.


*  `transparent.js` has been relocated, and orders can now be created from the Admin using PayflowPro and Authorize.Net. Previously, orders created from the Admin using PayflowPro failed, and Magento displayed an informative message indicating an invalid account number. 

*  Expected backup and restoration functionality has been restored and MySQL View support is supported while preserving backward compatibility with pre-existing modules.


*  `json_encode` errors are now caught and logged in console.log. Previously, the JSON serializer threw an error, which blocked all frontend behavior.

*  `app/bootstrap.php` has been updated to correctly define supported PHP versions. 

*  An incorrect parameter in `getCreatedAtFormatted($format)` have been corrected. 


*  A syntax error in `magento2/lib/internal/Magento/Framework/Cache/Backend/Database.php` has been corrected. 


*  Magento no longer throws an error when you send an email from the command line. Previously, Magento threw an exception because `$debugHintsPath` was missing. 

*  Message queue topic names generated as a result of asynchronous and bulk REST calls are now based on service contract names. Currently,  topic names reflect the PHP class and method names that should be invoked to handle processing. For example, a topic that was named using the older conventions (`async.V1.customers.POST`) might be named `async.magento.customer.api.accountmanagementinterface.createaccount.post`. This new naming is more semantic and allows the reuse for other Magento services.

Integration
~~~~~~~~~~~

*  Magento no longer throws an exception when you navigate to the OAuth page (**Backend** > **Stores** > **Configuration** > **Services** > **OAuth**). 

*  The Last logged In value displayed on the customer account page on the Admin is now updated as expected when a customer is authenticated through REST. *

*  Integrations are no longer reset after running the `bin/magento setup:upgrade` command.

Magento Shipping
~~~~~~~~~~~~~~~~

*  Updating an order destination prior to creating a shipment  now results in the shipment being sent to the new destination.

*  Shipments that contain the same item across multiple packages will now correctly update the shipped amount.

MSRP
~~~~

*  MAP (minimum advertised price) prices for the simple products belonging to a configurable product are now supported. MAP price for these products are now successfully handled and displayed  on the configurable product page and  the category page display of the configurable product.

Newsletter
~~~~~~~~~~

*  Magento now sets the correct `store_id` for each store when a customer subscribes to a newsletter from more than one stor. 


*  Customers are no longer unsubscribed to a newsletter as a result of a password reset email request when **Newsletter Need to Confirm** is set to **yes** on the Admin.


*  Magento now permits only one newsletter subscription per email address. Previously, when a website had multiple store views, a customer could subscribe multiple times to a newsletter with one email address.


*  Magento now displays an informative message when you click the unsubscribe link in the newsletter email.


*  You can now add a custom field to a newsletter in the position of your choice by editing  the newsletter configuration file (`app/code/Magento/Newsletter/etc/adminhtml/system.xml`).  Previously, you could add a new field but could not select where it would appear in the newsletter. 


*  A logged-in user who already has an account can now use the footer to sign up for a newsletter subscription. Previously, this user received an error message, and Magento did not subscribe her to the newsletter. 


*  If a customer tries to subscribe to a newsletter with an email that  already has a subscription associated with it, Magento now warns the customer rather than throws an exception. 

*  You can now search for or reset the filter on newsletter problem reports from the Admin. Previously, Magento did not display filter reports when administrators used FireFox.  

Orders
~~~~~~

*  The address form in the Admin order creation workflow has been refactored to improve performance.


*  Administrators now need sales email privileges to send order comment emails to customers.

Page cache
~~~~~~~~~~

*  Pages opened by URL redirect now display prices in the currency set for the appropriate store. Previously, the opened page contained prices in the default currency (USD) rather than the selected currency for the store.

Payment methods
~~~~~~~~~~~~~~~

*  Magento now populates the estimated billing address  field  on the checkout page with the default billing address as expected when the cart contains virtual products only. Previously, when a signed-in customer with different default shipping and billing addresses had a cart containing only virtual products, the cart estimation field was populated with the default shipping address information  instead of the default billing address information.

*  Invoice PDFs now include a populated FTP (Fixed Product Tax) amount field for orders when using Weee tax and FPT is enabled. Previously, this information was displayed in order and invoice views, but not captured in the PDF. 


*  Tax is now calculated as expected for virtual products when PayPal is used as a payment method.


*  When an order placed with PayPal fails during checkout, Magento no longer processes payment for the order. Previously, orders that failed during  checkout when being processed through PayPal were processed.


*  A pop-up window no longer blocks completion of checkout using Braintree PayPal on a mobile device.


*  When a  customer selects PayPal as a payment method but then applies for a gift card, Magento now reverts to zero subtotal checkout. Previously, the order failed at the review step if a gift card were applied.


*  Orders created with eWay as a payment method now contain the same credit card information, which is included in the Authorize.Net response. Previously, the order did not contain any information regarding the credit card.


*  Magento now displays successful orders paid for with eWay. Previously, Magento did not display completed errors even after the transaction was accepted by eWay.


*  The `getList()` method now returns the vault data total count as expected. 


*  You can now use REST to create an order without payment. Previously, when using REST to submit an order without a payment, Magento threw an error.


*  Payment methods are now grouped properly in the core source model. `\Magento\Payment\Model\Config\Source\Allmethods` class in the Magento core can be used as a source model for backend configuration fields. It displays available payment methods grouped by payment provider. We've added groups for previously missing payment options (PayPal, Authorize.Net, and  Braintree methods). 


*  Fixed misalignment of the save-for-later checkbox on the Admin create order credit card details page. 


*  The Authorize.Net payment method has been migrated to the `accept.js` API on both the storefront and Admin.


*  PayPal Express Checkout has been updated to the JSv4​. This API replaces the deprecated API Express Checkout - NVP/SOAP. This update provides Magento with a single integration but with multiple payment options that merchants can choose when activating the integration​. 

Performance
~~~~~~~~~~~

*  New customer address handling improves the processing of many addresses on the Admin customer details page. This functionality was rewritten with UI components to increase platform performance, which in turn facilitates the management of customers with 3000 and more addresses. This refactoring includes these changes:

   *  All actions on the Customer Addresses tab are now performed asynchronously with AJAX. This tab now contains the default billing address and default shipping address UI component blocks, customer addresses listing or grid, and customer address form in a modal window.

   *  `\Magento\Customer\Model\Customer\DataProvider` has been replaced by `\Magento\Customer\Model\Customer\DataProviderWithDefaultAddresses` to support the asynchronous management of customer addresses.

Product video
~~~~~~~~~~~~~

*  You can now pause product videos on YouTube on storefronts running on Internet Explorer 11.x.

Quote
~~~~~

*  You can now update a shopping cart that contains a reserved order number (for example, 000000651). 


*  You can now use REST to set billing information for a customer (`customerId`) with an existing address. Previously, Magento threw an exception during address validation. 
*  You can now request a quote on a storefront running on iOS 11.3.1.


*  We fixed an issue with inaccurate floating point calculations during checkout. 


*  Magento now saves the correct `quote_item_id` values for products during checkout for an order being shipped to multiple addresses. 

Reports
~~~~~~~

*  Magento no longer displays a negative number in the dashboard to represent a canceled order.

*  Magento now refreshes reports statistics as expected when you select the **Refresh Lifetime Statistics** option from the Actions menu of the **Reports** > **Refresh Statistics** page. Previously, you were redirected to a 404 page when you selected this menu option. 


*  Magento now displays correct prices for products at checkout when a customer uses a credit card and Authorize.Net is enabled. Previously, order items had the original price of $0.0. 

Reviews
~~~~~~~

*  Administrators can now access product ratings in deployments with multiple websites running different locales. 

*  The  **Save and Next** and **Save and Previous** buttons in **Marketing** > **Reviews** now work as expected.


*  You can now add a product review from the Admin.  Previously, when you clicked **New Review**, Magento displayed this error: `Error message showing : A technical problem with the server created an error. Try again to continue what you were doing. If the problem persists, try again later`. 


*  Pending Reviews are now correctly labeled under **System** > **User Roles** > **Add New Role** > **Role Resources**, and Magento now displays a new Pending reviews menu under **Marketing** > **User Content**. Previously, Magento displayed the Reviews menu twice.  

Rewards
~~~~~~~

*  Magento now allocates rewards points for converting an invitation to a customer when **Require Emails Confirmation** is set to **yes**.


*  The order status label on the  customer order status page  can now be translated. 


*  `/V1/orders/{id}` now retrieves information about used reward points.

Return Merchandise Authorizations (RMA)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

*  Magento now displays the correct amount in the **Remaining Quantity** field after Magento has processed a return.


*  Return attributes that have the **Values Required** attribute  set to **no** no longer break the storefront display of those attributes.


*  Administrators can now process returns when a request includes a required image attribute.  Previously, the Return Items tab displayed a validation error even though the image had  been uploaded, and if you clicked on **Details**, Magento displayed this message: `Please select a file`.


*  You can now return bundle products from the Admin. Previously, when you clicked Submit Returns, Magento displayed an informative error message, and did not create an RMA.

Sales
~~~~~

*  You can now remove a custom price from a product during order creation from the Admin.


*  The message that Magento displays when a merchant tries to create a credit memo for an order with no shipping charges has been made more informative. 


*  You can now print order information from the customer dashboard. Previously, when you tried to print  order information from the customer dashboard, Magento displayed this error: `Fatal error: Call to a member function getRealOrderId() on null in /vendor/magento/module-sales/Block/Order/PrintShipment.php`.


*  Magento no longer marks email as **not sent** when the email copy fails due to exception. Previously, Magento marked this email as not sent, and subsequently continued to resend the email. 

*  The **Add to Cart** button in the Recently Ordered block now works as expected.


*  Magento now displays bundle products' child products on the **My Account** > **My Orders** > **View Order** page. 

*  You can now issue a partial refund to store credit for an order made with an online payment method.


*  Orders for bundle products created from the Admin now display  correct product prices.


*  Company logos are now displayed correctly in printed PDF versions of invoices and shipment statements.


*  The Sales table now displays company information in billing and shipping addresses.


*  Magento now displays product price and shipping costs in the default currency that was configured for that specific website for orders created from the Admin. Previously, when you have multi-site configuration with different default currencies for each website, the product and shipping prices shown while creating an admin order are incorrect.


*  Magento now displays a success message when you create an order through the Admin and the **create shipment** and **Email copy of invoice** checkboxes are checked. 


*  Files uploaded for custom options can now be downloaded even when the product option is no longer available. Previously, these files could not be downloaded. 


*  Fixed an incorrect class name on orders and returns page on the Admin. 


*  Fixed misalignment of the **Update Qty** button on the sales order invoice. 

*  The `last_trans_id` column of the `sales_order_payment` table has been updated to handle the full order reference values for Amazon and Klarna extensions.

*  You can now programmatically  cancel an invoice when invoice state is set to `STATE_PAID`.


*  The performance of the Admin order creation page when handling many addresses has been improved.


*  Credit memos now accurately calculate refunds when default shipping charges are changed to zero.

*  The email that customers receive after completing an order now contains tracking information for only their order. Previously, Magento included tracking information for other orders, too. 

*  The `transportBuilderByStore` class has been removed. Previously, this class was the cause of undesired repeat emails. 


*  Magento now displays bundle options  on the Items Ordered tab of the My Account order page.

SalesRule
~~~~~~~~~

*  The sales rule indexer now runs without error. Previously, the sales rule indexer  returned an error during reindexing because of the `Magento_AdvancedSalesRule` module.


*  The payment method option is now displayed under the shopping cart rules condition tab. Previously, when you navigated to **Marketing** > **Promotions** > **Cart Price Rules** and opened the Conditions tab on a rule, Magento did not display payment method options. 

Search
~~~~~~

*  The default sort order field now works as expected on the Catalog Search results page.


*  Searching for a synonym that contains a hyphen and number now returns the same results as any other search term in the group.


*  Layered navigation for Elasticsearch now includes all product sizes. If the **Filterable (with results)** option is set for a product attribute then:

   *  Layered navigation includes only those filters for which matching products can be found.
   *  Any attribute value that already applies to all products shown in the list should still appear as an available filter.
   *  Attribute values with a count of zero (0) product matches are omitted from the list of available filters.


*  Full text search for Elasticsearch no longer includes the `date` attribute.


*  Layered navigation results no longer includes price ranges that contain no products.


*  Magento now returns a customized layout handle when there are no results for a search. This customized layout handle supports the addition of custom blocks, which permits you to  change the layout of the No results page. 


*  Elasticsearch now correctly returns only products whose SKUs contain dashes when your search criteria specifies SKUs that contain dashes. Previously, search results contained unmatched products as well as products whose SKUs contained dashes.

Shipping
~~~~~~~~

*  Magento now displays the appropriate error message when free shipping is not available for an order during check out.

*  Shipments created through REST now return tracking information as expected. Previously, Magento created shipment notifications without a tracking number when a shipment was created using REST.


*  Table rates now work as expected when using the AE code (Armed Forces Europe) when calculating weight vs destination table rates.


*  Magento now uses  shipping table rates from the correct store in multistore deployments.


*  Magento no longer throws an exception when a customer tries to place an order whose components will be shipped to different addresses.


*  Fixed misalignment of elements on the shipping information page that Magento displays when you click **Check Out with Multiple Addresses** from the shopping cart.


*  Magento now uses version 6.0 of the DHL XML Services schema for the DHL shipping method.

Sitemap
~~~~~~~

*  Sitemaps now display correct base URLs for deployments with  multiple stores.

Store
~~~~~

*  The switcher-option's link `Magento/Store/view/frontend/templates/switch/languages.phtml` template has been modified to support navigating back to previous pages. Previously, you could not navigate back to the previous store view when you clicked the **Back** button when viewing the store on Firefox. 


*  You can now define the `root_category_id` in the project `config.php`. 

Swatches
~~~~~~~~

*  Store views now show the correct swatch values.


*  Product images now display the color option you chose when you apply a color filter in layered navigation. Previously, wrong colors were randomly displayed.


*  You can now change the size of a swatch image as expected.


*  All thumbnails reload as expected after you click on a configurable option when a configurable product detail page has more than 14 thumbnail images. Previously, not all thumbnails reloaded.


*  You can now change an attribute type from swatch to dropdown without using data.  Previously, changing an attribute type from swatch to dropdown deleted swatch options for all attributes.


*  Fixed styles on the Add Swatch page.

Tax
~~~

*  The **Not yet calculated** string for the tax field in the summary section of the  checkout page can now be translated. 

*  Credit memos now include only the taxes on the product as expected. Previously, the credit memo included the shipping tax as well even when shipping costs were not refunded.


*  Tax is no longer added when a customer group is changed to **Valid VAT ID - Intra-Union**, which has no tax rules assigned to it.


*  Tax reports now correctly calculate taxes for an order placed in a zip code that has two or more tax rates assigned.


*  Magento no longer uses the default tax information set in **Stores** > **Configuration** > **Sales** > **Tax** customer, quote, and order data.

Testing
~~~~~~~

*  Integration tests now respect module status as defined in `config-global.php`.  This permits you to enable only the modules you typically keep enabled while still saving system resources.

*  Unit test annotations now assert exception messages correctly. 

Theme
~~~~~

*  You can now upload favicons and logo when editing headers for a store view. Previously, Magento threw an error.


*  The text attribute implemented on the product page within the mobile theme now fluidly displays the entire text value. Previously, long values were truncated.


*  The user agent rule now sets correct templates for product pages. Previously, the `footer.phtml` and `absolute_footer.phtml` templates were loaded from the desktop theme instead of the mobile theme, regardless of the user agent.


*  We've improved the display of the navigation menu on mobile deployments. Previously, Magento displayed only a portion of any submenu accessed from a top menu.


*  Wishlist and compare links now appear for related products in portrait mode when viewed on a mobile device.


*  Text now remains in the header area when you resize a page in deployments running in Internet Explorer.


*  Clicking on the store logo on the home page now reloads the page.


*  Fixed misalignment of the **Add to cart** button on the bundle product page in portrait orientation in mobile view.


*  Fixed alignment issue with sort results on list product page. 


*  The `alt` attribute on the logo image is now properly escaped. 

Translation and locales
~~~~~~~~~~~~~~~~~~~~~~~

*  Child themes now inherit translations from their parent theme as expected (`en_US.csv` translation dictionary).


*  Swedish (Finland) locales are now supported.

*  The message that Magento displays when you successfully add a product to your cart or shopping list is now available in the i18n translation file. 

UI
~~

*  Removed use of escapeJS method in  `app/code/Magento/SendFriend/view/frontend/templates/send.phtml`.


*  Fixed the misalignment of drop-down menus on the Advanced Pricing page. 

*  Magento no longer includes new orders that are not yet visible on the Orders page when you select all orders on the page for a mass action (such as update or cancelation). Previously, when you selected all orders on the Orders page for a mass action, any new order simultaneously being placed on storefront was included in the mass action. 


*  You can now set default values for the WYSIWYG edit field for editing form UI components.

*  The global search icon on the Admin is now correctly aligned.


*  Merchants can now change the currency symbol back to its default value from the Admin in single-store mode. Previously, when a merchant tried to change this symbol back to its default value, Magento displayed a success message, but did not change the currency symbol back to the default value.


*  Magento now correctly renders apostrophes as entered in text fields.


*  Admin tables now work as expected when single store mode is set to **on**. Previously, column positioning in these tables was not preserved when the page was refreshed.


*  WYSIWYG editor functionality is now available in all rows of the dynamic rows UI component. Previously, this functionality was available in the first row only.


*  Fixed incorrect display of the pager on the My Orders page. Previously, the pager obscured page links, which prevented customers from navigating to other pages. 

*  Usage of unsupported includes has been removed. Previously, when you chose a user to edit on the customers grid, Magento installations running on Internet Explorer 11.x did not load the expected page, but instead displayed this message: `object does not support method includes`.  

URL rewrites
~~~~~~~~~~~~

*  The storefront now properly displays the order of categories when you move categories in the Admin.


*  Product URLs are now based on the configuration information from the Admin, not the order of records in the database. Previously, the order of records in the database affected the generated URL, and some products showed category paths for product URLS when **Use Categories Path for Product URLs** was set to **no**.


*  The import process now retains permanent redirects for outdated product URLs as expected. Previously, the import process removed these redirects, and when you tried to open the changed product by the old URL key,  Magento displayed a 404 page.

VAT
~~~

*  Greek VAT numbers can now be validated.

Visual Merchandiser
~~~~~~~~~~~~~~~~~~~

*  Visual Merchandiser now correctly sorts configurable product prices in Tile view.

Web API
~~~~~~~

*  The response for `GET V1/orders/:orderId` now contains `bundle_option` and `product_option` information as expected.


*  All extension attributes listed in the documentation for `salesOrderRepositoryV1` API are now available.


*  Access restrictions on the order API are now enforced as expected. Previously, adminstrators with restricted privileges had complete access to orders.

Wishlist
~~~~~~~~

*  Magento no longer retains entries for deleted products in the database `wishlist_item_option` table.


*  You can now add a configurable product with no options  to a gift registry from a wishlist.


*  You can now remove a comment from a wishlist product as expected. Previously, Magento did not remove the comment, even after you click **Update Wish List**.

*  Corrected misalignment of the Edit and remove item links on the wish list page when displayed  on a screen with a resolution of 640 x 767.

*  Pagination controls on the wishlist page have been restored. 