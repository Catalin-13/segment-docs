---
title: [integration_name] Source
---

> (delete after reading) Include a 1-2 sentence introduction to your company and the value it provides to customers - updating the name and hyperlink. Please leave the utm string unchanged.

[<integration_name>](https://yourintegration.com/?utm_source=segmentio&utm_medium=docs&utm_campaign=partners){:target="_blank”} provides self-serve predictive analytics for growth marketers, leveraging machine learning to automate audience insights and recommendations.

This is an [Event Cloud Source](/docs/sources/#event-cloud-sources) which can not only export data into your Segment warehouse, but can also federate the exported data into your other enabled Segment Destinations.

> (delete after reading) Update your company name and support email address.

This source is maintained by <integration_name>. For any issues with the source, [contact their Support team](mailto:support@<integration_name>.com).

## Getting started

> (delete after reading) Include clear, succinct steps including hyperlinks to where customers can locate the place in your app to enter their Segment writekey.

*1. From your workspace's [Sources catalog page](https://app.segment.com/goto-my-workspace/sources/catalog){:target="_blank”} click **Add Source**.*
*2. Search for "<integration_name>" in the Sources Catalog, select <integration_name>, and click **Add Source**.*
*3. On the next screen, give the Source a name configure any other settings.*

*- The name is used as a label in the Segment app, and Segment creates a related schema name in your warehouse. The name can be anything, but we recommend using something that reflects the source itself and distinguishes amongst your environments (eg. SourceName_Prod, SourceName_Staging, SourceName_Dev).*

*4. Click **Add Source** to save your settings.*
*5. Copy the Write key from the Segment UI.*
*6. Log in to your <integration_name> account - navigate to Settings > Integrations > Segment Integration and paste the key to connect.*

## Stream

> (delete after reading) Clarify the type of Segment events your integration will send. 

<integration_name> uses our stream Source component to send Segment event data. It uses a server-side (select from `track`, `identify`, `page`, `group`) method(s) to send data to Segment. These events are then available in any destination that accepts server-side events, and available in a schema in your data warehouse, so you can query using SQL.

> (delete after reading) Clarify how your integration includes user identifiers in your event payloads, the example below is from Klaviyo:

The default behavior is for Klaviyo to pass the userId associated with the email recipient as the userId. There are cases in which Klaviyo does not have an associated userId, in which case the email address will be passed in as the anonymousId.

> (delete after reading) For each of the below sections, populate the event and properties that a customer would expect to receive in their downstream tools from your Event Source.

## Events

The table below lists events that <integration_name> sends to Segment. These events appear as tables in your warehouse, and as regular events in other Destinations. <integration_name> includes the `userId` if available.

### Device-mode events (client side)

| Event Name                      | Description                                                 |
|---------------------------------|-------------------------------------------------------------|
| Product List Viewed             | User has viewed a product collection                        |
| Product Clicked                 | User has clicked on a product from the collection           | 
| Product Viewed                  | User has viewed the product detail page                     | 
| Product Shared                  | User has shared a product                                   | 
| Product Image Clicked           | User has clicked a product image                            | 
| Products Searched               | User has searched for products                              | 
| Registration Viewed             | User has viewed the registration form                       | 
| Thankyou Page Viewed            | User had viewed the thank you page                          | 
| Product Added                   | User added a product to their shopping cart                 | 
| Product Removed                 | User removed a product from their shopping cart             | 
| Cart Viewed                     | User viewed their shopping cart                             | 
| Checkout Started                | User initiated the order process (a transaction is created) | 
| Checkout Step Viewed            | User viewed a checkout step                                 |
| Checkout Step Completed         | User completed a checkout step                              |
| Payment Info Entered            | User added payment information                              |
| Order Completed                 | User completed the order                                    |
| Order Canceled                  | User canceled the order                                     |
| Order Refunded                  | User refunded for the order                                 |
| Coupon Applied                  | Coupon was applied on a user’s shopping cart or order       |
| Product Added to Wishlist       | User added a product to their wishlist                      |
| Product removed from whishlist  | User removed a product from their wishlist                  |
| Wishlist Product Added to Cart  | User added product to cart from wishlist                           |

 
##Identify calls

For every event where there is an identifiable customer (from both the device-mode and cloud-mode) Xcommerce Segment Integration also sends an Identify call. This happens when the customer logs into the storefront, on the last step of the checkout, with the order, and also after purchase with any customer update in Admin Panel.

The following traits are included with an Identify call:

| Property Name              | Description                                                            | Property Type |
| -------------------------- | ---------------------------------------------------------------------- | ------------- |
| userId                     | The chosen user identifier. This defaults to the Shopify Customer ID.  | Double        |
| createdAt                  | The date the customer record was created.                              | Date          |
| customerLifetimeValue      | The total spend of the customer on the Shopify store.                  | Double        |
| default_address.street     | The customer's default street address.                                 | String        |
| default.address.postalCode | The customer's ZIP or postal code.                                     | String        |
| default_address.state      | The customer's state address.                                          | String        |


### Cloud-mode events (server side)

| Event Name         | Description                           |
| ------------------ | ------------------------------------- |
| Email Sent         | Email was sent successfully           |
| Email Opened       | Prospect opened the email             | 
| Link Clicked       | Prospect clicked the tracking link    | 
| Email Replied      | Prospect replied to email sent        | 
| Email Bounced      | Email servers rejected the email      | 
| Email Unsubscribed | Prospect clicked the unsubscribe link | 

## Event Properties

The table below list the properties included in the events listed above.

| Property Name                | Description                                             |
|------------------------------|---------------------------------------------------------|
| `userId`                     | The user's ID                                           |
| `default_address.street`     | The customer's default street address                   |
| `default_address.city`       | The customer's city address                             |
| `default_address.postalCode` | The customer's ZIP / post code                          |
| `default_address.state`      | The customer's state address                            |
| `default_adress.country`     | The customer's country                                  |
| `email`                      | The user's email address                                |
| `createdAt`                  | *The total spend of customer on the Shopify store ????* |
| `customerLifetimeValue`      | The user's payment tier                                 |
| `userId`                     | Email event type                                        |
| `userId`                     | Email event type                                        |
| `userId`                     | Email event type                                        |
| `userId`                     | Email event type                                        |
| `userId`                     | Email event type                                        |
| `userId`                     | Email event type                                        |
| `userId`                     | Email event type                                        |


## Adding Destinations

Now that your Source is set up, you can connect it with Destinations.

Log into your downstream tools and check to see that your events appear as expected, and that they contain all of the properties you expect. If your events and properties don’t appear, check the [Event Delivery](/docs/connections/event-delivery/) tool, and refer to the Destination docs for each tool for troubleshooting.

If there are any issues with how the events are arriving to Segment, [contact the <integration_name> support team](mailto:support@<integration_name>.com).

> (delete after reading) Congratulations! 🎉 You’ve finished the documentation for your Segment integration. If there’s any additional information or nuance which did not fit in the above template and that you want to share with our mutual customers, feel free to include these as a separate section for us to review. If not, you may now submit this doc to our team.
