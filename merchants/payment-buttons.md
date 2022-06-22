---
description: >-
  For a simple solution, you can add pay now buttons to your website to allow
  customers to pay.
---

# Payment buttons

{% hint style="danger" %}
1. Customers can easily pay with these buttons but they will still need to let you know they paid.
2. The amount and currency you specify can still be changed by the user
{% endhint %}

## Step by step

1. Create an account on [account.kupay.finance](https://account.kupay.finance) so you can get a unique account slug. Be sure to fill this out in the pop-up right after you signed up.
2. Your decentralized bank account can look like https://account.kupay.finance/-john-doe
3. For each product you craft a link that has the correct **chain\_id**, **amount** and **currency**, for example\
   https://account.kupay.finance/-john-doe?chain\_id=321\&amount=100\&currency=EUR
4. Now you can create buttons for each link on your website. If you are familiar with [Bootstrap](https://getbootstrap.com/docs/5.1/components/buttons/), you can use classes to make your links look like buttons.
5. In the line below, replace # with the link you created in step 3.

```
<a href="#" class="btn btn-primary">buy now</a>
```

| URL parameter | Description                                                                                                                                                                       | Example         |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| chain\_id     | The network identifier, for example 1 for Ethereum, or 321 for KuCoin Community Chain, 56 for BNB Smart Chain etc. This is the chain you want to be selected by default           | ?chain\_id=321  |
| amount        | The amount to pay in the specified currency                                                                                                                                       | \&amount=123.45 |
| currency      | 3-letter iso currency, eg. EUR or USD (check the woocommerce page for the list of supported currencies and request if you need us to support your currency). Use capital letters. | \&currency=JPY  |
