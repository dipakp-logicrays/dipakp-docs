Use the npm package in Magento 2
================================

You can use the npm package in your Magento custom module.

I used `@imgix/js-core`_ in custom module. It is a JavaScript library for generating image URLs with srcset.

.. _`@imgix/js-core`: https://github.com/imgix/js-core

How to use the npm package
--------------------------

Using below steps you can use any **npm package** in your custom magento module.

I use the ``@imgix/js-core`` npm package in custom magento 2 module.

#. Go to your web directory in your module.
    
    .. code-block:: bash

        <magento_root>/app/code/Vendor/Module/view/adminhtml/web

#. Run the below command for creating package.json

    .. code-block:: bash
        
        npm init

#. After running ``npm init`` command, it generates ``package.json``

    .. code-block:: json

        {
            "name": "Magento 2 imgix package",
            "version": "1.0.0",
            "description": "this is a test, this is only a test",
            "main": "index.js",
            "scripts":
            {
                "test": "echo \"Error: no test specified\" && exit 1"
            },
            "author": "Imgix",
            "license": "ISC"
        }

#. Install ``@imgix/js-core`` npm package by below command

    .. code-block:: bash
        
        npm install @imgix/js-core

#. It will create ``node_modules`` directories and ``package-lock.json`` file.

    .. figure:: https://i.stack.imgur.com/PkfFU.png
        :align: center
        :alt: Directory Structure

#. Add js which you want to use in ``requirejs-config.js``

    .. code-block:: bash
        
        // File path: app/code/Vendor/Module/view/adminhtml/requirejs-config.js
        var config = {
            paths: {
                ImgixClient: 'Vendor_Module/node_modules/@imgix/js-core/dist/imgix-js-core.umd'
            }
        };

#. Now,You can access the package your module with the below code

    .. code-block:: javascript

        require([
            'jquery',
            'ImgixClient'
        ], function ($, ImgixClient) {
            .....
            // Your code

            // Generate srcset

            const client = new ImgixClient({
            domain: 'testing.imgix.net',
            secureURLToken: 'my-token',
            includeLibraryParam: false,
            });

            const srcset = client.buildSrcSet(
            'image.jpg',
            {
                h: 800,
                ar: '3:2',
                fit: 'crop',
            },
            {
                devicePixelRatios: [1, 2],
            },
            );

            console.log(srcset);
            
            .....
        }):

#. Now, **srcset** generated to img tag, Check this screenshot for the result.

    .. figure:: https://i.stack.imgur.com/F6FxB.png
        :align: left
