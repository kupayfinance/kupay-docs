---
description: >-
  For integrations other than WooCommerce and Shopify you can use our generic
  API. We're excited to see what you build. Please keep us informed.
---

# API

{% hint style="warning" %}
**IMPORTANT: The API is currently in development. Please contact us to get early access**
{% endhint %}

### API end point

```
https://api.kupay.finance/v1/
```

### Authorization

Add the following header to **each** request to the api

```
Authorization: Bearer <token>
```

Please check the admin panel for your API token. Sign up via https://kupay.finance



### Create payment request

{% swagger method="post" path="/payment/create" baseUrl="https://api.kupay.finance/v1" summary="payment/create" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="body" required="true" name="id" type="String" %}
Your own unique internal order ID
{% endswagger-parameter %}

{% swagger-parameter in="body" name="order_number" required="true" type="String" %}
The order number that the customer knows about
{% endswagger-parameter %}

{% swagger-parameter in="body" name="created_at" type="String" required="true" %}
Date of the order
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="currency" required="true" %}
Order currency, eg. USD or EUR etc. see below
{% endswagger-parameter %}

{% swagger-parameter in="body" type="Float" name="amount" required="true" %}
Amount to pay, eg. 123.45
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="email" %}
Shoppers email
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="order_status_url" %}
The URL where the shopper can see the status of their order
{% endswagger-parameter %}

{% swagger-parameter in="body" name="cancel_url" type="String" required="true" %}
Where KuPay will redirect the customer when they click cancel on the payment page
{% endswagger-parameter %}

{% swagger-parameter in="body" name="paid_url" type="String" required="true" %}
Where KuPay will redirect the customer when they have finished paying on the payment page
{% endswagger-parameter %}

{% swagger-parameter in="body" name="callback_url" type="String" required="true" %}
Where KuPay API will send any updates to the payment status
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Created successfully" %}
```javascript
{
    "pay_url": "https://pay.kupay.finance/merchant/payment-id",
    "payment_id": "payment-id"
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}

```
id* = (string) your own unique internal order id
order_number* = (string) the order number that the customer knows about
created_at* = (string) date of the order 2021-12-23T18:58:04+01:00
currency* = (string) USD|EUR|JPY|GBP|AUD|CAD|CHF|CNY|HKD|NZD|SEK|KRW|SGD|NOK|MXN|INR|BRL|NGN
amount* = (float) total amount to pay
email = (string) shoppers email, where we will send the kupay payment link
order_status_url = (string) https url to the customers order status page
cancel_url* = (string) https url to redirect user to when they cancel payment
paid_url* = (string) https url to redirect user to when they finish payment
callback_url* = (string) https url where KuPay will send payment status updates
```

#### Json payload example

```
{
	"id": "12345",
	"order_number": "1234",
	"created_at": "2022-05-22T18:58:04+01:00",
	"currency": "USD",
	"amount": 123.45,
	"email": "",
	"order_status_url": "https://example.com",
	"cancel_url": "https://example.com",
	"paid_url": "https://example.com",
	"callback_url": "https://example.com"
}
```



### Get payment status

{% swagger method="get" path="/payment/status/<payment-id>" baseUrl="https://api.kupay.finance/v1" summary="" %}
{% swagger-description %}
Use the same 

`payment_id`

 that you received from the Create Payment call.
{% endswagger-description %}

{% swagger-parameter in="path" name="id" type="String" required="true" %}
Payment ID
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
    order object
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}
