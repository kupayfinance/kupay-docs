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

Please check the admin panel for your API token. Sign up via [https://kupay.finance](https://kupay.finance)



### Create payment request

{% swagger method="post" path="/payment/create" baseUrl="https://api.kupay.finance/v1" summary="payment/create" %}
{% swagger-description %}
To create a payment request, use the authorization headers described above. Also send a json body as described below. You will receive a payment_id, which you can use to track the status of the payment. The API will also send a webhook for all payment status updates to the URL you have given to it.
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
Order currency, USD|EUR|JPY|GBP|AUD|CAD|CHF|CNY|HKD|NZD|SEK|KRW|SGD|NOK|MXN|INR|BRL|NGN
{% endswagger-parameter %}

{% swagger-parameter in="body" type="Float" name="amount" required="true" %}
Amount to pay, eg. 123.45
{% endswagger-parameter %}

{% swagger-parameter in="body" type="String" name="email" %}
Shoppers email, where we will send the kupay payment link
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
Where KuPay API will send updates about the payment status
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Created successfully" %}
```javascript
{
    "pay_url": "https://pay.kupay.finance/merchant/payment-id",
    "payment_id": "1dabeb8c-d9e7-11ec-a7b6-fd796692aca4"
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Issue with credentials" %}
```javascript
[]
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="An error occurred" %}
```javascript
[]
```
{% endswagger-response %}
{% endswagger %}

#### Json payload example

```
{
	"id": "12345",
	"order_number": "1234",
	"created_at": "2022-05-22T18:58:04+01:00",
	"currency": "USD",
	"amount": 123.45,
	"email": "anderson@example.com",
	"order_status_url": "https://example.com/order/1234",
	"cancel_url": "https://example.com/canceled.html",
	"paid_url": "https://example.com/paid.html",
	"callback_url": "https://example.com/payment/status/updates"
}
```



### Get payment status

{% swagger method="get" path="/payment/status/<payment-id>" baseUrl="https://api.kupay.finance/v1" summary="payment/status" %}
{% swagger-description %}
Use the same `payment_id` that you received from the Create Payment request.

To get the payment status, use the authorization headers described above. Note that the API already sends a webhook to your application for all payment status updates to the URL you have given to it when you created the payment request via **payment/create**.
{% endswagger-description %}

{% swagger-parameter in="path" name="payment-id" type="String" required="true" %}
Payment ID
{% endswagger-parameter %}

{% swagger-response status="200: OK" description="Order was found" %}
```javascript
{
    "payment_id": "1dabeb8c-d9e7-11ec-a7b6-fd796692aca4",
    "status": "paid",
    "created_at": "2022-05-22 17:58:04",
    "order_number": "1234",
    "currency": "USD",
    "amount": 123.45
}
```
{% endswagger-response %}

{% swagger-response status="401: Unauthorized" description="Issue with credentials" %}
```javascript
[]
```
{% endswagger-response %}

{% swagger-response status="404: Not Found" description="Order not found" %}
```javascript
[]
```
{% endswagger-response %}

{% swagger-response status="500: Internal Server Error" description="An error occurred" %}
```javascript
{
    // Response
}
```
{% endswagger-response %}
{% endswagger %}
