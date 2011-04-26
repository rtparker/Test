Convertlets: Model Loader
=========================
This package handles all incoming http requests and reposnds with appropriate instructions to the javascript client.

Configurations
--------------

The following are required configuration files in any production environment

* [model.properties](https://github.com/convert/model/blob/master/README.org)
  Please see the model package for model.properties configurations options.
* [control.properties](https://github.com/convert/control/blob/master/README.org)
  Please see the control package for control.properties configurations options.
* [recommendation.properties](https://github.com/convert/recommmender/blob/master/README.org)
  Please see the recommendation pacakge for recommendation.properties configurations options

Convert Script Tags (setup.js and extras.js)
--------------------------------------------


### setup.js

setup.js is the file that connects the site back to the convertlets servers. A page should have setup.js somewhere preferably in the head.
JavaScript tags must be added to each page of the website. 

Similar to the way the website may have previously been tagged to support a Web Analytics application, 
the Convert script tag will be implemented in much the same way. As part of the implementation process, 
Convert has provided a customized line of JavaScript code (below) that will become the site’s unique script tag.
This tag should be added to all pages of the website. In most cases, the tag will need to be implemented only
in one or more template files that generate or apply to all pages of the website. 

Just as Web Analytics applications uses a script tag to track general information about site traffic, the
Convert client uses a similar methodology to manage a significantly broader set of dynamic capabilities with a single,
unified tag, including:

* Track Visitor page and site activity 
* Deliver custom content in the form of Convert Engagements 
* Pass Visitor data (form responses, etc.) into Convert Visitor Records 
* Track the results of every Convert Campaign

The following JavaScript tags are the only components that need to be added to enable the Convert client.
Ideally, in cases where the site is dynamically generated, these tags would be added into a global template
file used to generate the html for all pages on the site.

    <script type="text/javascript" src="https://convertglobal.s3.amazonaws.com/audax/setup.js"></script>


* Avoid placing this script within other HTML tags. (i.e. div,map,font, or even another script).
* NEVER enclose this script within form/form HTML tags.


### extras.js

Placing this script on every page ensures accurate and efficient functionality of the Convert software.

    <script type="text/javascript" src="https://convertglobal.s3.amazonaws.com/audax/extras.js"></script>

* This extras.js script MUST be implemented after the setup.js script in the previous step.


Shopping Cart Tagging
--------------------

Shopping Cart tagging is optional however it allows us to collect shopping cart information for our 
analytics, recommendation and profiling engines

*  Initialize convert_cart. This step has to be done once per page. and should be on all shopping cart pages before any other shopping cart information is added

    <script type="text/javascript">
        if(!window.convert_cart){
            window.convert_cart={};
            convert_cart.shoppingCartItems=new Array();
        }
    </script>

* Add shopping cart variables.
    
    <script type="text/javascript">
      convert_cart.totalCost="@@TOTAL_COST@@";
      convert_cart.taxes=@@TAXES@@;
      convert_cart.discount=@@DISCOUNT@@;
      convert_cart.shipping=@@SHIPPING@@;
      convert_cart.promoCode="@@PROMO_CODE@@";
      convert_cart.orderId="@@ORDER_ID@@";

      //loop on items in the shopping cart
      //loop start
        var convert_item={};
        convert_item.sku="@@SKU@@";
        convert_item.quantity=@@QUANTITY@@;
        convert_item.price="@@PRICE@@";
        convert_cart.shoppingCartItems.push(convert_item);
      //loop end
    </script>

* On order Confirmation Page.

    <script type="text/javascript">
      convert_cart.isPurchased=true;
    </script>

