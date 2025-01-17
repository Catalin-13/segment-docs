---
Prestashop to Segment Tracking by Xcommerce - Source
---


[Segment Tracking](https:xcommerce.eu/segment) provides self-serve predictive analytics for growth marketers, leveraging machine learning to automate audience insights and recommendations.

This is an [Event Cloud Source](/docs/sources/#event-cloud-sources) which can not only export data into your Segment warehouse, but can also federate the exported data into your other enabled Segment Destinations.

This source is maintained by Prestashop to Segment Tracking by Xcommerce. For any issues with the source, [contact their Support team](mailto:contact@xcommerce.eu).


## Getting started

1. From your workspace's [Sources catalog page](https://app.segment.com/goto-my-workspace/sources) click ***Add Source***.
2. Search for "Prestashop (by Xcommerce)" in the Sources Catalog, select "Prestashop (by Xcommerce)", and click ***Add Source***.
3. On the next screen, give the Source a name configure any other settings.
   - The name is used as a label in the Segment app, and Segment creates a related schema name in your warehouse. The name can be anything, but we recommend using something that reflects the source itself and distinguishes amongst your environments (eg. SourceName_Prod, SourceName_Staging, SourceName_Dev).
4. Click ***Add Source*** to save your settings.
5. Copy the Write key from the Segment UI.
6. Log in to your Prestashop Backoffice, go to "Prestashop (by Xcommerce)" Module Settings, and paste the API Key in the Settings tab, as described in the [Configuration section](#Configuration)


## Installation

1. Get the Xcommerce Segment Integration from Prestashop Market. 
   After the purchase, you will get a .zip file
2. Go to Prestashop Admin Panel -> Improve -> Module Manager
3. Click "Upload a module" and select the .zip file for the upload


## Configuration

1. To configure the module go to Prestashop Admin Panel -> Improve -> Module Manager
2. Browse for the Segment Tracking module and select Configure option for the module

    ![Navigate to Module manager.](Images/GoToConfigure.png)

   > **Note**: On the configuration page you will see a number of Tabs corresponding to various settings. Start with the las tab (Settings)

3. Settings tab:

    ![Settings tab.](Images/SettingsTab.png)
    This is the page where you will select the general connection and labeling options.
   - Active - Select if the Module is active and sends data to Segment
   - API Key - API key for the designated Segment Source
   - API Host - Select the region of the host (US or EU)
   - Storefront Action Label - Designate a label you want to be included in the events triggered by actions performed in Storefront
   - Backoffice Action Label - Designate a label you want to be included in the events triggered by actions performed in Backoffice
   - Event Category - Designate the default event category name. This will be visible in all Events
   - Page View - You can select if you want to track all the viewed pages. This will send an event o every page load.
   
    > **Note**: Make sure to click Save after you are satisfied with the configurations.
   
4. Consent Settings Tab:

    ![Customer Setting tab.](Images/ConsentSettingsTab.png)
    On this page you can select if and how to track Customer Consent Settings
   - Customer Consent Update - Select if the consent update will be tracked or not
   - Consent Service - Select one of two options: CookieBoot or Custom
   - Track Script - Enter the js script for the Consent Service
   
    > **Note**: Make sure to click Save after you are satisfied with the configurations.

5. Customer Settings tab:

    ![Customer Setting tab.](Images/CustomerSettingsTab.png)
    Here you will find two settings: "Customer traits included in:" and "Customer Id value"


   - Reset Anonymous ID: 
     - You can select if you want the Anonymous ID to be reset after customer Log Out
   - Send customer traits in:
     - Identify Only - This option will trigger a separate Identify event along with the Customer Login, Customer Register, Consent Updated and Customer Updated events. This Event will contain the Customer specific properties. 
     - Identify and context traits - This option will trigger a separate Identify event along with the specific Customer Events. Also, the Customer specific properties will be included in all the Tracking Events. The customer properties will pe present in the "context" -> "traits" array.
     - Identify and properties - This option will trigger a separate Identify event along with the specific Customer Events. Also, the Customer specific properties will be included in all the Tracking Events. The customer properties will pe present in the "properties" array.
     - Context traits only - No Identify event will be triggered. Instead, the Customer specific properties will be included in all the Events. The customer properties will pe present in the "context" -> "traits" array.
     - Properties only - No Identify event will be triggered. Instead, the Customer specific properties will be included in all the Events. The properties will pe present in the "properties" array.
     
   - Segment user ID
     - Default user id - Use the Prestashop user ID as the Customer ID value
     - Custom user id - You can specify a certain field from the Database ***(id_customer needs to be mentioned in the used table if a different table than ps_customer is used)***
     - Email dash - Use the email hash of the customer as the Customer ID value. You can also add a Prefix and a Suffix to the email hash.

    > **Note**: Make sure to click Save after you are satisfied with the configurations.
     
6. The rest of the tabs can be used to enable or disable the triggers for teh Events tracked by Segment Tracking. There are 4 tabs, one for each category of events. Use these tabs to select which event you want Segment Tracking to track.
    ***Here we could mention in parentheses the field description***
   1. Track Products
      1. Product List Viewed
      2. Search Autosuggest Completed
      3. Products Searched
      4. Products Brand List Viewed
      5. Product Viewed
   2. Track Checkout
      1. Cart Viewed
      2. Product Added
      3. Product Quantity Updated
      4. Product Removed
      5. Checkout Started
      6. Checkout Step Viewed
      7. Thankyou Page Viewed
   3. Track Order
      1. Order Completed
      2. Order Refunded
      3. Order Cancelled
      4. Order Status Changed
      5. Product Added - Backoffice
      6. Product Removed - Backoffice
      7. Discount Added - Backoffice
      8. Discount Removed - Backoffice
      9. Payment Added - Backoffice
   4. Track Customer
      1. Customer Registered
      2. Customer Logged In
      3. Customer Logged Out
      5. Customer Updated
      6. Customer Created - Backoffice
      7. Customer Updated - Backoffice


## Stream

Prestashop - Segment Tracking by Xcommerce uses our stream Source component to send Segment event data. It uses a server-side (select from `track`, `identify`, `page`, `group`) ***We need to clarify and mention which methods are used for Server Side*** method(s) to send data to Segment. These events are then available in any destination that accepts server-side events, and available in a schema in your data warehouse, so you can query using SQL.


The default behavior is for Klaviyo (***Klaviyo is a data analytics driven marketing platform https://www.klaviyo.com/about It seems that this is an informative note of how Klaviyo is expecting data***) to pass the userId associated with the email recipient as the userId. There are cases in which Klaviyo does not have an associated userId, in which case the email address will be passed in as the anonymousId.


## Events

The table below lists events that "Prestashop to Segment Tracking by Xcommerce" sends to Segment. These events appear as tables in your warehouse, and as regular events in other Destinations. "Prestashop to Segment Tracking by Xcommerce" includes the `userId` if available.
 

### Identify calls

For every event where there is an identifiable customer "Prestashop to Segment Tracking by Xcommerce" also sends an Identify call. This happens when the customer logs into the storefront, on the last step of the checkout, with the order, and also after purchase with any customer update in Admin Panel.

The following traits are included with an Identify call:

| Property Name             | Description                                           | Property Type |
|---------------------------|-------------------------------------------------------|---------------|
| `billing_address`         | The customer's billing address                        | String        |
| `billing_city`            | The customer's billing city                           | String        |
| `billing_country`         | The customer's billing country                        | String        |
| `billing_postal_code`     | The customer's billing postal code                    | String        |
| `birthday`                | The customer's birthday                               | Date          |
| `createdAt`               | The date the customer record was created              | Date          |
| `customer_lifetime_value` | The total spend by the customer on the store          | Number        |
| `email`                   | The customer's email address                          | String        |
| `first_name`              | User name                                             | String        |
| `gender`                  | The gender of the user                                | String        |
| `last_name`               | User last name                                        | String        |
| `last_order_date`         | The date of the las order made on the user account    | Date          |
| `phone`                   | The Phone number of the customer                      | String        |
| `purchase_count`          | The date of the last order placed on the user account | Integer       |
| `userId`                  | The customer ID as set on Customer Settings           | String        |
| `shipping_address`        | The customer's shipping address                       | String        |
| `shipping_city`           | The customer's shipping city                          | String        |
| `shipping_country`        | The customer's shipping country                       | String        |
| `shipping_postal_code`    | The customer's shipping postal code                   | String        |
| `source`                  | The action that triggered the event                   | String        |


### Cloud-mode events (server side)

Cloud-mode handles events that have data stored or calculated in the Database. These events send data that is not necessarily available to the User in the browser. This method can capture information that would otherwise be inaccessible due to add block, for example.

| Event Name                   | Description                                                                                          |
|------------------------------|------------------------------------------------------------------------------------------------------|
| Customer Consent Update      | Follows updates to the User Consent                                                                  |     
| Customer Registered          | Follows the submission of the Customer Register form                                                 |     
| Customer Created             | Follows the successful creation of a customer in Backoffice                                          |     
| Customer Logged In           | Follows the successful Customer Login events                                                         |     
| Customer Logged Out          | Follows the successful Customer Logout events                                                        |     
| Customer Updated             | Follows updates to a Customer Account                                                                |     
| Product Viewed               | Follows the successful loading of Product Detail Pages                                               |     
| Product List Viewed          | Follows the displaying of Product Lists                                                              |     
| Product List Filtered        | Follows the applying of Filters on Product Lists                                                     |    
| Products Searched            | Follows the loading of Product Searches Results pages                                                |     
| Search Autosuggest Completed | Follows the population of Search Autocomplete lists                                                  |     
| Product Added                | Follows the successful adding of products to cart                                                    |     
| Product Quantity Updated     | Follows the product quantity updated on Cart Page                                                    |     
| Product Removed              | Follows the removal of products from Cart page                                                       |     
| Cart Viewed                  | Follows the successful loading of the Cart Page                                                      |     
| Checkout Started             | Follows the successful loading of the first Checkout Step ***to be clarified***                      |     
| Checkout Step Viewed         | Follows the successful loading of subsequent Checkout Steps                                          |     
| Thankyou Page Viewed         | Follows the successful loading of Thank You Pages after placing an order                             |     
| Order Completed              | Follows the successful placing of an Order (from Storefront or Backoffice)                           |     
| Order Refunded               | Follows the successful changing of the Order Status to "Refunded" from Backoffice                    |     
| Order Cancelled              | Follows the successful changing of the Order Status to "Canceled" from Backoffice                    |     
| Order Updated                | Follows the successful update of the Order from Backoffice (status changes or order details changes) |     

   > **Note**: The list of products included in the Cart or on the Order is ***limited to 30 products***. Only the fists products will be mentioned. The purpose for this limitation is to make sure the calls to Segment are smalled than 35KB (Segment Limitation)

## Event Properties

The table below list the properties included in the events listed above.


### Product Properties

| Property Name           | Description                                                       | Property Type |
|-------------------------|-------------------------------------------------------------------|---------------|
| `brand`                 | The brand of the product                                          | String        |
| `category`              | The category of the product (in default language)                 | String        |
| `category_localized`    | The category of the product (in selected Storefront language)     | String        |
| `compare_at_price`      | The product price before any discount                             | Number        |
| `currency`              | Currency code associated with the transaction                     | String        |
| `image_url`             | The URL of the first product image                                | String        |
| `name`                  | The product name (in default language)                            | String        |
| `name_localized`        | The product name (in selected Storefront language)                | String        |
| `position`              | The product position in the collection                            | Integer       |
| `presentment_amount`    | The product price as displayed to the user                        | Number        |
| `presentment_currency`  | The currency displayed to the user                                | String        |
| `prestashop_product_id` | Prestashop Product ID                                             | String        |
| `prestashop_variant_id` | Prestashop Product Variant ID                                     | String        |
| `price`                 | The product price at the time of the event, in the store currency | Number        |
| `product_id`            | The prestashop Product ID                                         | String        |
| `products`              | The products displayed in the product list                        | Array         |
| `products_in_cart`      | The products contained in the shopping cart                       | Array         |
| `quantity`              | The quantity of products                                          | Integer       |
| `sku`                   | The product SKU                                                   | String        |
| `tags`                  | The product tags                                                  | String        |
| `url`                   | The URL of the product page                                       | String        |
| `variant`               | The product variant name                                          | String        |


### Order Properties
 
| Property Name                | Description                                                            | Property Type |
|------------------------------|------------------------------------------------------------------------|---------------|
| `cart_id`                    | The ID of the Prestashop cart                                          | String        | 
| `coupon`                     | Coupon id and name associated with the product ***or transaction??***  | String        |
| `currency`                   | Currency code associated with the transaction                          | String        |
| `discount`                   | The discounted amount                                                  | Number        | 
| `event_category`             | The category of the events, as set in Backoffice                       | String        |       
| `order_id`                   | The ID of the order                                                    | String        |      
| `payment_gateway_xcommerce`  | The payment gateway used by the customer                               | String        |     
| `presentment_amount`         | The products price as displayed to the user                            | Number        |    
| `presentment_currency`       | The currency displayed to the user                                     | String        |   
| `presentment_total`          | The order price as displayed to the user (including the shipping cost) |               |
| `revenue`                    | Revenue ($) associated with the transaction                            | Number        |      
| `shipping`                   | The shipping cost                                                      | Number        |      
| `shipping_gateway_xcommerce` | The shipping method chosen for checkout                                | String        |     
| `step`                       | The checkout step number                                               | Integer       |  
| `subtotal`                   | Order total after discounts but before taxes and shipping              | Number        | 
| `tax`                        | The amount of tax on the order                                         | Number        |       
| `total`                      | Revenue with discounts and coupons added                               | Number        |      


### Customer Properties

| Property Name          | Description                                        | Property Type |
|------------------------|----------------------------------------------------|---------------|
| `billing_address`      | The customer's billing address                     | String        |
| `billing_city`         | The customer's billing city                        | String        |
| `billing_country`      | The customer's billing country                     | String        |
| `billing_postal_code`  | The customer's billing postal code                 | String        |
| `birthday`             | The customer's birthday.                           | Date          |
| `createdAt`            | The date the customer record was created.          | Date          |
| `email`                | The customer's email address                       | String        |
| `first_name`           | User name                                          | String        |
| `gender`               | The gender of the user                             | String        |
| `last_name`            | User last name                                     | String        |
| `last_order_date`      | The date of the las order made on the user account | Date          |
| `phone`                | The Phone number of the customer                   | String        |
| `shipping_address`     | The customer's shipping address                    | String        |
| `shipping_city`        | The customer's shipping city                       | String        |
| `shipping_country`     | The customer's shipping country                    | String        |
| `shipping_postal_code` | The customer's shipping postal code                | String        |
| `userId`               | The customer ID as set on Customer Settings        | String        |


### Other Properties

| Property Name    | Description                                                  | Property Type |
|------------------|--------------------------------------------------------------|---------------|
| `event_category` | Event category (defaults to Prestashop(Xcommerce))           | String        |
| `list_id`        | Product list being viewed                                    | String        |
| `results`        | Number of products matching the search                       | Integer       |
| `sent_from`      | Xcommerce source identifier                                  | String        |
| `source_name`    | The source of the order or checkout (e.g. web, android, pos) | String        |
| `marketing`      | User accepted or not marketing tracking                      | Boolean       |
| `necessary`      | User accepted or not necessary tracking                      | Boolean       |
| `preferences`    | User accepted or not preferences tracking                    | Boolean       |
| `statistics`     | User accepted or not statistics tracking                     | Boolean       |
| `source`         | The reason of the trigger                                    | String        |   
| `locale`         | The storefront language selected by the user                 | String        |
| `anonymous`      | The randomly generated user ID                               | String        |


## Adding Destinations

Now that your Source is set up, you can connect it with Destinations.

Log into your downstream tools and check to see that your events appear as expected, and that they contain all the properties you expect. If your events and properties don’t appear, check the [Event Delivery](/docs/connections/event-delivery/) tool, and refer to the Destination docs for each tool for troubleshooting.

If there are any issues with how the events are arriving to Segment, contact the ["Prestashop to Segment Tracking by Xcommerce" support team](mailto:contact@xcommerce.eu).

