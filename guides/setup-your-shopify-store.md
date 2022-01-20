# Setup your Shopify store

{% hint style="info" %}
**Good to know:** while we only support Shopify now, we will work on plugins for WooCommerce etc. to make it easier to integrate KuPay into your webshop.
{% endhint %}

## The basics

1. Create a new Shopify shop (if you haven’t already)
2. Create a new Merchant account on [https://kupay.finance](https://kupay.finance) -- coming soon! Email us to create an account, please provide the following details:
   1. Name of your shop
   2. URL of your shop
   3. Public contact information email
   4. Your name
   5. Your address
   6. Your phone number
3. We generate a webhook address for you, that you need to add to Shopify, see below
4. Setup a custom payment method, see below
5. Add custom code to the checkout page (optional, but recommended)

## Webhook

**Prerequisites:**\
**-** You will need the webhook address that is generated in your merchant account on [https://kupay.finance](https://kupay.finance)

Visit https://\<your shop>.myshopify.com/admin/settings/notifications\
Settings > Notifications\
(scroll to the bottom of the page)

![](<../.gitbook/assets/Screen Shot 2021-12-29 at 22.55.30.png>)

Add webhook to Shopify under notifications to send every new order here Webhook https://api.kupay.finance/webhook/shopify/\<YOUR\_MERCHANT\_ID> Eg. https://api.kupay.finance/webhook/shopify/11ec-93c2-525400d2ddc2

```
Event: Order creation
Format: JSON
URL: You can find this in your kupay.finance account information
Webhook API version: 2021-10 (Latest)
```

Click Save

## **Add a new custom payment method**

Add a new custom payment method, and name it KuPay

1. In Shopify visit Settings > Payments\
   Note: only the owner of the Shopify store can do this!
2. Scroll down to Manual payment methods
3. Click on Create custom payment method in the dropdown list![](<../.gitbook/assets/Screen Shot 2021-12-29 at 22.54.04.png>)
4. Type **KuPay** (the name is important and cannot be changed)
5. Make sure to have “**KuPay**” in the name because you need it and cannot change it later.
6. You can click **Manage** to update the payment method and add some more details to describe the payment method.
7. The additional details are displayed on the check out page
8. The payment instructions are displayed on the status/thank you page

![](<../.gitbook/assets/Screen Shot 2021-12-29 at 22.53.16.png>)

## **Add custom code to the checkout page**

While this is not strictly required, we do recommend adding the code, to optimize the customer experience. This code will load a payment button directly on the thank you page. Without this code, the customer will have to click the link in the email they receive, which will be a little bit less likely to convert (eg. if the email goes to spam somehow, or the customer changes their mind).

1. In Shopify visit Settings > Checkout
2. Scroll to the bottom where it says “Additional scripts”
3. In the box “Order status page” you can add the following 2 lines of code:

```
<div id="kupay-shopify-status" class="content-box" style="margin-top:3em"></div>
<script src="https://api.kupay.finance/pay/api/order/shopify/status/js/?v=1&order_number={{checkout.order.order_number}}&order_id={{checkout.order_id}}"></script>

```

**It should look like this on the status/thank you page:**

![If your status/thank you page is not dark but using a light theme, please contact our support to give you instructions.](<../.gitbook/assets/Screen Shot 2021-12-29 at 22.52.14.png>)
