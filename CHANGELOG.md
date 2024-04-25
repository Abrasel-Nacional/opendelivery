# Changelog
### Version [v1.3.0] - Jan 9, 2024

#### ORDERS, MERCHANTS and LOGISTICS change

- Removed the necessity to enter at least 5 digits for all `latitude` and `longitude` properties.      

#### ORDERS changes

- [GET /v1/orders/{orderId}](https://abrasel-nacional.github.io/docs/versions/1.3.0/#tag/ordersDetails/operation/ordersDetails)

  - Added a new optional propertie `salesChannel`.  
    This should be used to inform the channel that originated the order.

  - Added a new optional propertie `discounts.sponsorshipValues.discountCode`.  
    This code should be used to identify a discount coupon used by the user, or an identification code for a marketing campaign, for example.

  - Added new optional properties `items.originalPrice` and `items.options.originalPrice` to inform the price of an item before applying markdowns on the list price.

  - Modified the requirement for the `payments.methods.brand` property. It can now be informed for both prepaid and pending payments.

  - Added the information that the `customer` object is **REQUIRED** when the `type` of the order is `DELIVERY`.

#### LOGISTICS changes

- [POST /logistics/delivery](https://abrasel-nacional.github.io/docs/versions/1.3.0/#tag/logisticOrder/operation/logisticsNewDelivery)

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

- [POST /orders/{orderId}/tracking](https://abrasel-nacional.github.io/docs/versions/1.2.0/#tag/ordersTracking/operation/orderTracking)

  - Added a new endpoint [POST /orders/{orderId}/tracking](#operation/orderTracking) for sending delivery information to the `Ordering Application`.

- [GET /v1/orders/{orderId}](https://abrasel-nacional.github.io/docs/versions/1.2.0/#tag/ordersDetails/operation/ordersDetails)

  - Added new optional field `sendTracking` to control whether or not the `Software Service` should call the [POST /orders/{orderId}/tracking](#operation/orderTracking) endpoint.
  
  - Added a new option to work with **'TABs'** for **INDOOR** orders. This can be used by establishments that control orders via tabs or control cards. As a result, the following changes have been made:

    - Added new `TAB` enum, to the `indoor.mode` propertie.
    - Added new `indoor.tab` propertie.
  
  - Added an optional field `customer.email` to inform the customer email.

  - Removed the requirement to send the `customer` object

  - Removed the requirement to send the `customer.document` propertie

- [POST /v1/orders/{orderId}/dispatch](https://abrasel-nacional.github.io/docs/versions/1.2.0/#tag/ordersStatus/operation/dispatchOrder)

  - Added new object `deliveryTRackingInfo` to send delivery informations to the `Ordering Application` when dispatching the order

- [POST /v1/orders/{orderId}/requestCancellation](https://abrasel-nacional.github.io/docs/versions/1.2.0/#tag/ordersCancellation/operation/requestCancellation)

  - Added `DELIVERY_PROBLEM` as a new enum option to the `code` propertie. 

- [GET /v1/events:polling ](https://abrasel-nacional.github.io/docs/versions/1.2.0/#tag/ordersPolling/operation/pollingEvents)

  - Removed the requirement of the `x-polling-merchants` parameter.

#### LOGISTICS changes

- [POST /v1/logistics/delivery](https://abrasel-nacional.github.io/docs/versions/1.2.0/#tag/logisticOrder/operation/logisticsNewDelivery)

  - Added a new optional field `orderDeliveryFee` to inform to the `Logistics Service` the customer's paid shipping fee in the `Ordering Application`

- [POST /v1/logistics/availability](https://abrasel-nacional.github.io/docs/versions/1.2.0/#tag/logisticPrice/operation/logisticsAvailability)

  - Added a new optional field `orderDeliveryFee` to inform to the `Logistics Service` the customer's paid shipping fee in the `Ordering Application`

- [GET /v1/logistics/delivery/{orderId}](https://abrasel-nacional.github.io/docs/versions/1.2.0/#tag/logisticDetails/operation/logisticDetails)

  - Fixed the `problem.actionTaken` propertie type to string instead of boolean

#### SECURITY changes

- [POST /oauth/token](https://abrasel-nacional.github.io/docs/versions/1.2.0/#tag/authentication/operation/getToken)

  - Fixed the `client_secret` propertie type to string instead of integer

- All endpoints that uses oAuth2 authentication:

  - Added the 401 - Unauthorized response to be used when the credentials are not valid (the 403 response can still be used).

#### MERCHANT changes

- [GET /v1/merchant](https://abrasel-nacional.github.io/docs/versions/1.2.0/#tag/merchantEndpoints/operation/getMerchant)

  - Removed the requirement of the `categories.availabilityId` propertie.

  - Removed the requirement of the `itemOffers.availabilityId` propertie.

#### OTHERS changes

- Bug fixes and general corrections in the documentation texts and links.

## Version [1.1.1] - Apr 3, 2023

#### ORDERS changes:

- [GET /v1/orders/{orderId}](https://abrasel-nacional.github.io/docs/versions/1.1.1/#tag/ordersDetails/operation/ordersDetails)

    - added `sendDelivered` property. This property should have been added together with the [POST /v1/orders/{orderId}/delivered](#operation/orderDelivered) endpoint  

    - added `CANCELLATION_DENIED` to the order events. This event was described in the documentation in the [Orders Cancellation](https://abrasel-nacional.github.io/docs/versions/1.1.0/#tag/ordersCancellation) section but was not present in the enum.

- [POST /v1/orders/{orderId}/requestCancellation](https://abrasel-nacional.github.io/docs/versions/1.1.1/#tag/ordersCancellation/operation/requestCancellation)

    - fixed the names of the following reasons:
      - `RESTAURANT_WITHOUT_DELIVERY_MAN` to `RESTAURANT_WITHOUT_DELIVERY_PERSON`
      - `INTERNAL_DIFFICULTIES_OF THE RESTAURANT` to `INTERNAL_DIFFICULTIES_OF_THE_RESTAURANT`

## Version [1.1.0] - Jan 23, 2023

#### MERCHANT changes:

- [GET /v1/merchant](https://abrasel-nacional.github.io/docs/versions/1.1.0/#tag/merchantEndpoints/operation/getMerchant)

  - added new optional propertie `acceptedCards` in the `basicInfo` entity of endpoint.

      This field is intended to indicate which card brands are accepted by the merchant.

  - added an enumerator to propertie `unit` in the `items` entity of endpoint [GET /v1/merchant](https://abrasel-nacional.github.io/docs/versions/1.1.0/#tag/merchantEndpoints/operation/getMerchant).

  - added new optional field `targetAppId` in the `service` entity of endpoint [GET /v1/merchant](https://abrasel-nacional.github.io/docs/versions/1.1.0/#tag/merchantEndpoints/operation/getMerchant).

      This field is intended to indicate a specific Ordering Application to receive the service information.

- [POST /v1/merchantUpdated](https://abrasel-nacional.github.io/docs/versions/1.1.0/#tag/merchantUpdate/operation/menuUpdated)

  - added `MERCHANT` and `BASIC_INFO` options to the enumerator of the `entityType` field of the webhook.

    This allows the webhook to now receive the full merchant entity information and can be used instead of the [GET /v1/merchant](https://abrasel-nacional.github.io/docs/versions/1.1.0/#tag/merchantEndpoints/operation/getMerchant) endpoint.  
    This can be used by **Software Services** that do not have the infrastructure to expose this endpoint.

    It is also possible to update any entity that is part of the Merchant object. (this was already possible previously with the exception of BASIC_INFO entity).

#### ORDERS changes:

- added a new optional order event, called `DELIVERED`.  

  With this, the following changes have been made:

  - [GET /v1/orders/{orderId}](https://abrasel-nacional.github.io/docs/versions/1.1.0/#tag/ordersDetails/operation/ordersDetails)
    - added `DELIVERED` to the events

  - added new [POST /v1/orders/{orderId}/delivered](https://abrasel-nacional.github.io/docs/versions/1.1.0/#tag/ordersStatus/operation/orderDelivered) endpoint

    This endpoint is intended to indicate to the **Ordering Application** that an order has been delivered.

- [GET /v1/orders/{orderId}](https://abrasel-nacional.github.io/docs/versions/1.1.0/#tag/ordersDetails/operation/ordersDetails)

  - added more options to the enumerator of propertie `unit` in the `items` entity of the endpoint, reflecting the created enum.

  - added new field `lastEvent` to be filled with the last valid event sent/polled (whether acknowledged or not).

  - added new optional field `brand` to the `payments>methods` entity.

    This field is intended to indicate the brand of the card (for cases where the chosen payment method has a brand).

- [POST /v1/orders/{orderId}/requestCancellation](https://abrasel-nacional.github.io/docs/versions/1.1.0/#tag/ordersCancellation/operation/requestCancellation)

  - added propertie `cancellationStatus` to the 422 response body to indicate the result of the cancellation request in case of a duplicate event.

- [POST /v1/orders/{orderId}/confirm](https://abrasel-nacional.github.io/docs/versions/1.1.0/#tag/ordersStatus/operation/confirmOrder)

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

    - [GET /v1/versions/orderingApp](https://abrasel-nacional.github.io/docs/versions/1.0.1/#operation/getOrderingAppVersions)
    - [GET /v1/versions/merchant](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/merchantEndpoints/operation/getMerchantVersions)

  - Added the `status` property to entities `Item`, `ItemOffer` and `Option` on the [GET /merchant](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/merchantEndpoints/operation/getMerchant) endpoint.

  - Added HTTP Status code 422 on the following endpoints:
    - [POST /v1/orders/{orderId}/confirm](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersStatus/operation/confirmOrder)
    - [POST /v1/orders/{orderId}/readyForPickup](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersStatus/#operation/orderReady)
    - [POST /v1/orders/{orderId}/dispatch](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersStatus/#operation/dispatchOrder)
    - [POST /v1/orders/{orderId}/requestCancellation](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersStatus/#operation/requestCancellation)
    - [POST /v1/orders/{orderId}/acceptCancellation](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersStatus/#operation/cancellationAccepted)
    - [POST /v1/orders/{orderId}/denyCancellation](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersStatus/#operation/cancellationDenied)

  - Added HTTP Status code 204 on the following endpoints:
    - [POST /v1/merchantUpdated](https://abrasel-nacional.github.io/docs/versions/1.1.0/#tag/merchantUpdate/operation/menuUpdated)
    - [POST /v1/orderUpdate](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersWebhook/operation/newEvent)
    - [POST /v1/orders/{orderId}/acceptCancellation](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersStatus/#operation/cancellationAccepted)
    - [POST /v1/orders/{orderId}/denyCancellation](https://abrasel-nacional.github.io/docs/versions/1.0.1/#tag/ordersStatus/#operation/cancellationDenied)

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
