# Changelog

### Version [v1.7.0] - Jan 05, 2026

#### ORDERS changes

- [GET /orders/{orderId}](https://abrasel-nacional.github.io/docs/#operation/ordersDetails)
  - Added new enum value `MIN_ORDER_FEE` to `otherFees.type` in endpoint `GET /v1/orders/{orderId}` to support minimum order fee charges. This is a complementary fee applied to orders that do not meet the minimum order value requirement.

#### MERCHANT changes
      
- Added endpoint [GET /merchant/{id}/status](https://abrasel-nacional.github.io/docs/#operation/getMerchantAvailability) to retrieve merchant status, service hours, and orderingAppMerchantId.

- [PUT /merchantOnboarding](https://abrasel-nacional.github.io/docs/#operation/putMerchantOnboarding)
  - Added `orderingAppMerchantId` field to the response body to provide the internal merchant identifier from the Ordering Application.

#### OTHERS changes

- Bug fixes and general corrections in the documentation texts and links.

### Version [v1.6.0] - Jul 21, 2025

#### ORDERS changes

- [GET /orders/{orderId}](https://abrasel-nacional.github.io/docs/#operation/ordersDetails)
  - Added `category` property to the order object, which can be used to indicate the category of service the order attends

- [PATCH /orders/{orderId}/details](https://abrasel-nacional.github.io/docs/#operation/patchOrderDetails)
  - New endpoint created to allow targeted updates to order properties that do not affect the order status.
          
#### LOGISTICS changes

- [POST /logistics/delivery](https://abrasel-nacional.github.io/docs/#operation/logisticsNewDelivery)
  - Added `pickupCode` property, to inform the delivery person of the pickup code required at the merchant.
  - Added `preparationStartDateTime` property, indicating to the logistics service an estimated time for the start of order preparation.

#### OTHERS changes

- Bug fixes and general corrections in the documentation texts and links.

### Version [v1.5.0] - Jan 20, 2025

#### ORDERS changes

- Added two new optional order events:  
  **PREPARING**: Informs the **Ordering Application** that the order has already begun preparation.  
  **PICKED_UP**: Informs the **Ordering Application** that the order has been picked up by the customer.  

  With this, the following changes have been made:

  - Added new [POST /v1/orders/{orderId}/preparing](https://abrasel-nacional.github.io/docs/#operation/orderPreparing) endpoint.
  - Added new [POST /v1/orders/{orderId}/pickedUp](https://abrasel-nacional.github.io/docs/#operation/orderPickedUp) endpoint.  
  
  - [GET /events:polling](https://abrasel-nacional.github.io/docs/#operation/pollingEvents) || [POST /events/acknowledgment](https://abrasel-nacional.github.io/docs/#operation/pollingAcknowledgment) || [POST /orderUpdate](https://abrasel-nacional.github.io/docs/#operation/newEvent)

    - added `PREPARING` to the events
    - added `PICKED_UP` to the events

  - [GET /orders/{orderId}](https://abrasel-nacional.github.io/docs/#operation/ordersDetails)
    - added `sendPreparing` optional propertie.
    - added `sendPickedUp` optional propertie.

- Added a new optional order event, called `PREPARATION_REQUESTED`.
This new event has the purpose of informing the **SOFTWARE SERVICE** to start the preparation of a `ONDEMAND` order. 
- Added `ONDEMAND` option to the `orderTiming` enum.

- [GET /orders/{orderId}](https://abrasel-nacional.github.io/docs/#operation/ordersDetails)

  - Added `taxInvoice` optional object.
    This object is optional and can be used by the **Software Service** to know if a invoice has already been issued and the URL to access it.

  - Added `transaction` optional object to the `payments` object.
    This object contains information about the payment transaction, such as the transaction ID and the acquirer document.

  - Added `orderPriority` optional propertie. 
    This property is used to indicate to the merchant the priority of preparation of the order in relation to other orders sent by the same Ordering Application.

  - Added `TERMINAL` option to the `indoor.type` enum.
  - Added `waiterCode` optional propertie to the `indoor` object.
  - Added `seat` optional propertie to the `indoor` object.
  - Added `CHAIN` option to the `discounts.sponsorshipValues.name` enum.
  - Added `subtotalPrice` optional propertie to the `items` and `items.options` objects.
  - Added `scalePriceApplied` optional propertie to the `items` object.
  - Added `indoor` optional object to the `items` object.

  - Added `pickupCode` optional propertie to the `delivery` object.

#### MERCHANT changes

- **WEBP** format is now accepted for images.

- [GET /merchant](https://abrasel-nacional.github.io/docs/#operation/getMerchant)
  - Added `images` propetie in `items` entity

    The `images` propetie is an array that holds images of the item, intended for use when size variations of the image are needed.
    If the `images` array contains any values, it must be considered, and the preexisting `image` field must be ignored.
    If the `images` array is empty, the preexisting `image` field must be considered.

    The images in the array must indicate a `type` beetwen `main` or `thumb`.

  - Added `ONDEMAND` option to the `serviceTiming` enum.
    This propertie allows for the merchant to indicate that the service is available on demand, without a fixed schedule.
  
  - Added `exclusionAreaPolygon`to the `serviceArea` object.
    This propertie allows for the merchant to indicate a polygon area that is not served by the merchant.

  - Added `priceMethod` propertie to the 'optionGroup' object.
    This propertie allows for the merchant to indicate the price calculation method for multiple options groups on the same item.   
    
  - Added `servicePriority` propertie to the `services` object.
    This propertie allows for the merchant to indicate if the merchant works if order priorities.            

#### LOGISTICS changes

- [POST /logistics/delivery](https://abrasel-nacional.github.io/docs/#operation/logisticsNewDelivery)
  - Added `items` optional object, to provide more information about the items being delivered.

#### OTHERS changes

- Bug fixes and general corrections in the documentation texts and links.

### Version [v1.4.0] - Jun 18, 2024

#### SECURITY changes

- Changed the text describing **OAuth2** authentication, making clear the roles of the **Ordering Application** and the **Logistics Service**, since they both use the same logic to provide the access credentials and the token URL.

#### ORDERS changes

- [GET v1/events:polling ](https://abrasel-nacional.github.io/docs/#operation/pollingEvents)
- [POST /orderUpdate (WEBHOOK)](https://abrasel-nacional.github.io/docs/#operation/newEvent)
- [GET /v1/orders/{orderId}](https://abrasel-nacional.github.io/docs/#operation/ordersDetails)

  - Added a new optional propertie `virtualBrand`.  
    This should be used as an alternative id for the merchant, in cases where the same merchant has different identifications or brands (such as dark kitchens).

- [POST /v1/orders/{orderId}/validateCode](https://abrasel-nacional.github.io/docs/#operation/orderValidateDelivery)

  - Added this new endpoint to validate a delivery code provided by the customer.

- Other ORDERS changes:
  
  - The `Order Tracking` menu has been changed to `Order Delivery Info`

  - The places in the documentation where the text referenced the `ORDER_CANCELLATION_REQUESTED` enum have been adjusted to `ORDER_CANCELLATION_REQUEST`. This will not affect any implementation.

  - The diagram of the [Order Cancellation section](https://abrasel-nacional.github.io/docs/#tag/ordersCancellation), where Ordering Application's cancellation is explained, has been updated to better reflect event returns.

  - Changed the text in the section on receiving events to indicate that ACKNOLODGMENT is only required for those working via POLLING.
    The text has also been changed to indicate that the Ordering Application can work with either of the two services and that POLLING is not required as a mandatory implementation. (Contrary to what was previously understood.)


#### LOGISTICS changes

- [POST /v1/logistics/readyForPickup/{orderId}](https://abrasel-nacional.github.io/docs/#operation/logisticsReadyForPickup)

  - Added this new optional endpoint for the MERCHANT to notify the Logistic Service that an order is ready for pickup. 
  
  - Changed the delivery order flow diagram to reflect the new endpoint.

- [POST v1/logistics/delivery](https://abrasel-nacional.github.io/docs/#operation/logisticsNewDelivery)  

  - Added a new optional propertie `notifyReadyForPickup` to indicate if the **Logistics Service** must be ready to receive a Ready for Pickup request. 
  - Added a new optional propertie `customerPhoneLocalizer` to indicate the order or customer localizer information to a call center.
  - Added a new optional propertie `confirmationCodeRequired` to indicate whether the **Logistics Service** needs to validate a Delivery Confirmation Code passed by the customer to complete the delivery.
  
- [POST v1/logistics/confirmationCode (WEBHOOK)](https://abrasel-nacional.github.io/docs/#operation/logistictsDeliveryCode)
  
  - Added this new Webhook for the MERCHANT to receive the Delivery Confirmation Code informed by the customer from the Logistics Service. 

- Other LOGISTICS changes:

  - The `Delivery Tracking` menu has been changed to `Webhooks`

#### OTHERS changes

- Bug fixes and general corrections in the documentation texts and links.

### Version [v1.3.0] - Jan 9, 2024

#### ORDERS, MERCHANTS and LOGISTICS change

- Removed the necessity to enter at least 5 digits for all `latitude` and `longitude` properties.      

#### ORDERS changes

- [GET /v1/orders/{orderId}](https://abrasel-nacional.github.io/docs/#tag/ordersDetails/operation/ordersDetails)

  - Added a new optional propertie `salesChannel`.  
    This should be used to inform the channel that originated the order.

  - Added a new optional propertie `discounts.sponsorshipValues.discountCode`.  
    This code should be used to identify a discount coupon used by the user, or an identification code for a marketing campaign, for example.

  - Added new optional properties `items.originalPrice` and `items.options.originalPrice` to inform the price of an item before applying markdowns on the list price.

  - Modified the requirement for the `payments.methods.brand` property. It can now be informed for both prepaid and pending payments.

  - Added the information that the `customer` object is **REQUIRED** when the `type` of the order is `DELIVERY`.

#### LOGISTICS changes

- [POST /logistics/delivery](https://abrasel-nacional.github.io/docs/#tag/logisticOrder/operation/logisticsNewDelivery)

  - Fixed the guidance on how to use the combination of orders in a new delivery request.  
    Previously the description was incorrectly quoting the `deliveryId` and `combinedDeliveriesId` fields. This has been corrected to `orderId` and `combinedOrdersId` respectively.  
    Nothing has changed on the endpoint itself.

  - Added a new optional propertie `customerPhone` to inform the customer's phone number. 


#### OTHERS changes

- Bug fixes and general corrections in the documentation texts and links.

## Version [1.2.1] - Sep 4, 2023

#### ORDERS changes

  - [GET /v1/orders/{orderId}](https://abrasel-nacional.github.io/docs/versions/1.2.1/#tag/ordersDetails/operation/ordersDetails)

    - Fixed the description of the formula for calculating the final price of an item.  
      
      **NEW Description:**  
          
          (quantity * (unitPrice + optionsPrice))  
        
      _Old description: (quantity * unitPrice + optionsPrice)_  
    
      The new formula includes the value of the item's options when multiplying by the quantity.
    
    - Added the information that the `customer` property should be informed when the order `type` is `DELIVERY`.
    
    - Changed some properties descriptions to better explain their purpose.

## Version [1.2.0] - Jun 26, 2023

#### ORDERS changes

- [POST /orders/{orderId}/tracking](https://abrasel-nacional.github.io/docs/#tag/ordersTracking/operation/orderTracking)

  - Added a new endpoint [POST /orders/{orderId}/tracking](https://abrasel-nacional.github.io/docs/#operation/orderTracking) for sending delivery information to the `Ordering Application`.

- [GET /v1/orders/{orderId}](https://abrasel-nacional.github.io/docs/#tag/ordersDetails/operation/ordersDetails)

  - Added new optional field `sendTracking` to control whether or not the `Software Service` should call the [POST /orders/{orderId}/tracking](https://abrasel-nacional.github.io/docs/#operation/orderTracking) endpoint.
  
  - Added a new option to work with **'TABs'** for **INDOOR** orders. This can be used by establishments that control orders via tabs or control cards. As a result, the following changes have been made:

    - Added new `TAB` enum, to the `indoor.mode` propertie.
    - Added new `indoor.tab` propertie.
  
  - Added an optional field `customer.email` to inform the customer email.

  - Removed the requirement to send the `customer` object

  - Removed the requirement to send the `customer.document` propertie

- [POST /v1/orders/{orderId}/dispatch](https://abrasel-nacional.github.io/docs/#tag/ordersStatus/operation/dispatchOrder)

  - Added new object `deliveryTRackingInfo` to send delivery informations to the `Ordering Application` when dispatching the order

- [POST /v1/orders/{orderId}/requestCancellation](https://abrasel-nacional.github.io/docs/#tag/ordersCancellation/operation/requestCancellation)

  - Added `DELIVERY_PROBLEM` as a new enum option to the `code` propertie. 

- [GET /v1/events:polling ](https://abrasel-nacional.github.io/docs/#tag/ordersPolling/operation/pollingEvents)

  - Removed the requirement of the `x-polling-merchants` parameter.

#### LOGISTICS changes

- [POST /v1/logistics/delivery](https://abrasel-nacional.github.io/docs/#tag/logisticOrder/operation/logisticsNewDelivery)

  - Added a new optional field `orderDeliveryFee` to inform to the `Logistics Service` the customer's paid shipping fee in the `Ordering Application`

- [POST /v1/logistics/availability](https://abrasel-nacional.github.io/docs/#tag/logisticPrice/operation/logisticsAvailability)

  - Added a new optional field `orderDeliveryFee` to inform to the `Logistics Service` the customer's paid shipping fee in the `Ordering Application`

- [GET /v1/logistics/delivery/{orderId}](https://abrasel-nacional.github.io/docs/#tag/logisticDetails/operation/logisticDetails)

  - Fixed the `problem.actionTaken` propertie type to string instead of boolean

#### SECURITY changes

- [POST /oauth/token](https://abrasel-nacional.github.io/docs/#tag/authentication/operation/getToken)

  - Fixed the `client_secret` propertie type to string instead of integer

- All endpoints that uses oAuth2 authentication:

  - Added the 401 - Unauthorized response to be used when the credentials are not valid (the 403 response can still be used).

#### MERCHANT changes

- [GET /v1/merchant](https://abrasel-nacional.github.io/docs/#tag/merchantEndpoints/operation/getMerchant)

  - Removed the requirement of the `categories.availabilityId` propertie.

  - Removed the requirement of the `itemOffers.availabilityId` propertie.

#### OTHERS changes

- Bug fixes and general corrections in the documentation texts and links.

## Version [1.1.1] - Apr 3, 2023

#### ORDERS changes:

- [GET /v1/orders/{orderId}](https://abrasel-nacional.github.io/docs/#tag/ordersDetails/operation/ordersDetails)

    - added `sendDelivered` property. This property should have been added together with the [POST /v1/orders/{orderId}/delivered](https://abrasel-nacional.github.io/docs/#operation/orderDelivered) endpoint  

    - added `CANCELLATION_DENIED` to the order events. This event was described in the documentation in the [Orders Cancellation](https://abrasel-nacional.github.io/docs/#tag/ordersCancellation) section but was not present in the enum.

- [POST /v1/orders/{orderId}/requestCancellation](https://abrasel-nacional.github.io/docs/#tag/ordersCancellation/operation/requestCancellation)

    - fixed the names of the following reasons:
      - `RESTAURANT_WITHOUT_DELIVERY_MAN` to `RESTAURANT_WITHOUT_DELIVERY_PERSON`
      - `INTERNAL_DIFFICULTIES_OF THE RESTAURANT` to `INTERNAL_DIFFICULTIES_OF_THE_RESTAURANT`

## Version [1.1.0] - Jan 23, 2023

#### MERCHANT changes:

- [GET /v1/merchant](https://abrasel-nacional.github.io/docs/#tag/merchantEndpoints/operation/getMerchant)

  - added new optional propertie `acceptedCards` in the `basicInfo` entity of endpoint.

      This field is intended to indicate which card brands are accepted by the merchant.

  - added an enumerator to propertie `unit` in the `items` entity of endpoint [GET /v1/merchant](https://abrasel-nacional.github.io/docs/#tag/merchantEndpoints/operation/getMerchant).

  - added new optional field `targetAppId` in the `service` entity of endpoint [GET /v1/merchant](https://abrasel-nacional.github.io/docs/#tag/merchantEndpoints/operation/getMerchant).

      This field is intended to indicate a specific Ordering Application to receive the service information.

- [POST /v1/merchantUpdated](https://abrasel-nacional.github.io/docs/#tag/merchantUpdate/operation/menuUpdated)

  - added `MERCHANT` and `BASIC_INFO` options to the enumerator of the `entityType` field of the webhook.

    This allows the webhook to now receive the full merchant entity information and can be used instead of the [GET /v1/merchant](https://abrasel-nacional.github.io/docs/#tag/merchantEndpoints/operation/getMerchant) endpoint.  
    This can be used by **Software Services** that do not have the infrastructure to expose this endpoint.

    It is also possible to update any entity that is part of the Merchant object. (this was already possible previously with the exception of BASIC_INFO entity).

#### ORDERS changes:

- added a new optional order event, called `DELIVERED`.  

  With this, the following changes have been made:

  - [GET /v1/orders/{orderId}](https://abrasel-nacional.github.io/docs/#tag/ordersDetails/operation/ordersDetails)
    - added `DELIVERED` to the events

  - added new [POST /v1/orders/{orderId}/delivered](https://abrasel-nacional.github.io/docs/#tag/ordersStatus/operation/orderDelivered) endpoint

    This endpoint is intended to indicate to the **Ordering Application** that an order has been delivered.

- [GET /v1/orders/{orderId}](https://abrasel-nacional.github.io/docs/#tag/ordersDetails/operation/ordersDetails)

  - added more options to the enumerator of propertie `unit` in the `items` entity of the endpoint, reflecting the created enum.

  - added new field `lastEvent` to be filled with the last valid event sent/polled (whether acknowledged or not).

  - added new optional field `brand` to the `payments>methods` entity.

    This field is intended to indicate the brand of the card (for cases where the chosen payment method has a brand).

- [POST /v1/orders/{orderId}/requestCancellation](https://abrasel-nacional.github.io/docs/#tag/ordersCancellation/operation/requestCancellation)

  - added propertie `cancellationStatus` to the 422 response body to indicate the result of the cancellation request in case of a duplicate event.

- [POST /v1/orders/{orderId}/confirm](https://abrasel-nacional.github.io/docs/#tag/ordersStatus/operation/confirmOrder)

  - added new optional field `preparationTime` to endpoint .

    This field is used to indicate the estimated time to prepare the order.

#### LOGISTICS changes:

- the logistics standard is no longer BETA, and is now versioned together with the RELEASE version.

      
      
## Version [1.0.1] - Aug 1, 2022

  - Added the possibility to indicate orders with scheduled delivery.  
  With this the following changes were made:

    - [GET /merchant](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/merchantEndpoints/operation/getMerchant)
      - `service` > Added a new optional field `serviceTiming`, where the merchant can indicate the delivery timing available for that service.

      ```
      ...
      "serviceTiming":
          {
              "timing": ["INSTANT", "SCHEDULED"],
              "schedule":
                  {
                      "scheduleTimeWindow": "15_MINUTES",
                      "scheduleStartWindow": "15_MINUTES",
                      "scheduleEndWindow": "15_MINUTES",
                  },
      ...
      ```
    - [GET /orders/{orderId}](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersDetails/operation/ordersDetails)
      - Added `SCHEDULED` option to the `orderTiming` field.

      - Added a new property called `schedule` where the delivery window for scheduled orders will be specified with the following structure:
        ```
            {
              ...
              "schedule": {
                "scheduledDateTimeStart": "2019-08-24T14:15:22Z",
                "scheduledDateTimeEnd": "2019-08-24T14:15:22Z"
                },
              ...
            }
        ```

  - Added a new service type called **INDOOR**.  
    The following places are affected:

    - [GET /merchant](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/merchantEndpoints/operation/getMerchant)
      - added option `INDOOR` to `type` field of entity `service`.

    - [GET /orders/{orderId}](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersDetails/operation/ordersDetails)
      - added new property: `indoor` with the following structure:     

      ```
      {
        ...
        "indoor": {
          "mode": "PLACE",
          "indoorDateTime": "2019-08-24T14:15:22Z",
          "place": "string"
        },
        ...
      }
      ```
  - Added a new endpoint so that **Merchant** can send information related to its [GET /merchant](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/merchantEndpoints/operation/getMerchant) endpoint to the **Ordering APPLICATION**:

    - [PUT /v1/merchantOnboarding](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/merchantStatus/operation/putMerchantOnboarding) 

  - Added a new [Working Versions](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/versionsSection) section with endpoints so that both the Software Service and the Ordering Application can check which version of the Open Delivery API the other end is using. The endpoints created were:

    - [GET /v1/versions/orderingApp](https://abrasel-nacional.github.io/docs/versions/1.0.1/https://abrasel-nacional.github.io/docs/#operation/getOrderingAppVersions)
    - [GET /v1/versions/merchant](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/merchantEndpoints/operation/getMerchantVersions)

  - Added the `status` property to entities `Item`, `ItemOffer` and `Option` on the [GET /merchant](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/merchantEndpoints/operation/getMerchant) endpoint.

  - Added HTTP Status code 422 on the following endpoints:
    - [POST /v1/orders/{orderId}/confirm](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersStatus/operation/confirmOrder)
    - [POST /v1/orders/{orderId}/readyForPickup](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersStatus/https://abrasel-nacional.github.io/docs/#operation/orderReady)
    - [POST /v1/orders/{orderId}/dispatch](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersStatus/https://abrasel-nacional.github.io/docs/#operation/dispatchOrder)
    - [POST /v1/orders/{orderId}/requestCancellation](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersStatus/https://abrasel-nacional.github.io/docs/#operation/requestCancellation)
    - [POST /v1/orders/{orderId}/acceptCancellation](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersStatus/https://abrasel-nacional.github.io/docs/#operation/cancellationAccepted)
    - [POST /v1/orders/{orderId}/denyCancellation](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersStatus/https://abrasel-nacional.github.io/docs/#operation/cancellationDenied)

  - Added HTTP Status code 204 on the following endpoints:
    - [POST /v1/merchantUpdated](https://abrasel-nacional.github.io/docs/#tag/merchantUpdate/operation/menuUpdated)
    - [POST /v1/orderUpdate](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersWebhook/operation/newEvent)
    - [POST /v1/orders/{orderId}/acceptCancellation](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersStatus/https://abrasel-nacional.github.io/docs/#operation/cancellationAccepted)
    - [POST /v1/orders/{orderId}/denyCancellation](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersStatus/https://abrasel-nacional.github.io/docs/#operation/cancellationDenied)

  - Removed the **requirement** of the fields:
    - [GET /merchant](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/merchantEndpoints/operation/getMerchant)
      - `menu` > `description`
      - `menu` > `disclaimer`
      - `category` > `description`
      - `optionGroup` > `description`

  #### Other Changes:

  - Added a new [Developer Tools](https://abrasel-nacional.github.io/docs/versions/1.0.1/#section/Developer-Tools) section where links to partner tools to help with API development will be listed.

  - [Order Overview](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersOverview)

    - The lifecycle and order flow diagrams have been updated to better reflect the service types.

  - Overall revisions of grammatical errors, syntax, examples and descriptions.


## Version [v1.0.0] - Apr 18, 2022

- Initial release.
