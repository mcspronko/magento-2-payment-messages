# Payment Messages for Magento 2.x

[![Codacy Badge](https://api.codacy.com/project/badge/Grade/493c457ec0eb428ea7ad8338b642464e)](https://app.codacy.com/app/max.pronko/magento-2-payment-messages?utm_source=github.com&utm_medium=referral&utm_content=mcspronko/magento-2-payment-messages&utm_campaign=Badge_Grade_Dashboard)

This module allows to pass error messages from Payment Service Providers to a Checkout Payments page.

## Implementation

The Pronko_PaymentMessages module consists of 2 plugins for Magento_Checkout module. 
The `Pronko\PaymentMessages\Plugin\GuestPaymentInformationManagement` class intercepts the `Magento\Checkout\Model\GuestPaymentInformationManagement::savePaymentInformationAndPlaceOrder` method. 
The `Pronko\PaymentMessages\Plugin\PaymentInformationManagement` class intercepts the `Magento\Checkout\Model\PaymentInformationManagement::savePaymentInformationAndPlaceOrder` method.

Both plugins pass the `Magento\Framework\Exception\LocalizedException` exceptions assuming it as messages which are allowed to be shown for a customer. 

Note: There are payment integrations which throw exceptions which should not be shown to a customer. It is recommended to check payment integration on staging environment to avoid any security information leak via error messages. 

## Specific Payment Methods
You may also limit messages to specific payment modules.

Add the following declaration into the di.xml file of your payment module:
```xml
    <type name="Pronko\PaymentMessages\Model\MethodList">
        <arguments>
            <argument name="methodCodes" xsi:type="array">
                <item name="payment_code_example" xsi:type="string">payment_code_example</item>
            </argument>
        </arguments>
    </type>
```