Magento Open Source 2.3.7 Release Notes
=======================================

**Official link**: https://devdocs.magento.com/guides/v2.3/release-notes/open-source-2-3-7.html

Magento Open Source 2.3.7 offers significant platform upgrades, 40 security enhancements, and 10 functional fixes for the core product.

.. important::
    PHP 7.3 reached end of support in December 2021, and Adobe Commerce 2.3.x reaches end of support in April 2022.
    **We strongly recommend planning your upgrade now to Adobe Commerce 2.4.x and PHP 7.4.x to help maintain PCI compliance.**


**Apply AC-3022.patch to continue offering DHL as a shipping carrier**

DHL has introduced schema version 6.2 and will deprecate schema version 6.0 in the near future. Adobe Commerce 2.4.4 and earlier versions that support the DHL integration support only version 6.0.
Merchants deploying these releases should apply AC-3022.patch at their earliest convenience to continue offering DHL as a shipping carrier.
See the `Apply a patch to continue offering DHL as shipping carrier <https://support.magento.com/hc/en-us/articles/7707818131597-Apply-a-patch-to-continue-offering-DHL-as-shipping-carrier>`__ Knowledge Base article for information about downloading and installing the patch.

Platform upgrades v2.3.7
------------------------

* Removal of PHP 7.1 and 7.2 compatibility. You cannot run Magento 2.3.7 on PHP 7.1 or 7.2.
* PHP 7.3 is now deprecated.
* PHP 7.4 support.
* Support for PHPUnit 9.x and deprecation of PHPUnit 6.5
* `Elasticsearch 7.9.x <https://devdocs.magento.com/guides/v2.3/install-gde/system-requirements.html>`__ is now supported.
* Varnish 6.5.1 is now supported on 2.3.x.
* Magento 2.3.7 is now compatible with Composer 2.x.
* Redis 6.x is now supported. Magento 2.3.x remains compatible with Redis 5.x.
* The ``endroid/qr-code`` library dependency has been updated to the latest version (4.x).
* The Vimeo Simple API has been replaced with Vimeo `oEmbed <https://developer.vimeo.com/api/oembed>`__ API.
* The Web Set Up Wizard has been deprecated and removed. You must use the command line to install or upgrade Magento 2.3.7. `Install Magento <https://devdocs.magento.com/guides/v2.3/install-gde/install/cli/install-cli.html>`__

Fixed issues in v2.3.7
----------------------

* Magento now deletes expired database sessions from the database ``session`` table as expected.
* **Customer**: The Create an Account button on the Create New Account page remains active when a shopper enters invalid data. Previously, this button was disabled, which prevented shoppers from re-attempting to create an account after making an error.
* Disabling the PageBuilder module no longer affects the rendering of the product page.
* **Sales**: Magento no longer creates duplicate address entries for a customer account when creating a new order from the Admin for an existing customer. The **Save in Address Book** check box has been renamed to **Add to Address Book** and is now unchecked in the Admin by default.
* **Tax**: Cart price rules are now applied as expected when order subtotals are calculated without incorporating tax. The new Subtotal (Incl. Tax) option has been added as a cart price rule condition.
