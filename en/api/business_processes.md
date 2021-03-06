# Business Processes

To make sure your services or client application works properly with Upay Web API, the following types of business processes need to be implemented:

1. Terminal activation (once per terminal)
2. Terminal check-in (optional)
3. Transactions


## Terminal Activation

Each Upay terminal needs to be activated before any transaction takes place. The terminal will get `terminal_sn` and `terminal_key` in successful activation response. The terminal is also responsible for saving and managing the `terminal_sn` and `terminal_key` which will be used for signing every transaction request.

Every terminal only needs to be activated once and only once.

![](../img/activate_sd.png?raw=true) 

## Terminal Check-in

`terminal_sn` and `terminal_key` are like username and password to your terminal. To keep your terminals and transactions safe, we recommend `terminal_key`s be updated on daily basis. Developers may pick any time during the day to perfrom the check-in. But keep in mind that ~~a `terminal_key` is only valid for at most 48 hours, and~~ after each check-in, only current and last `terminal_key`s are valid.

![](../img/checkin_sd.png?raw=true) 

## Transactions

Upay Web API supports the following transactions: 

* **Pay**: When a cashier uses Upay terminal to scan a customer's payment barcode; Upay will automatically figure out the payment service provider from the barcode.

* **Refund**: Issue an order refund based on order serial number; Upay supports multiple refunds of a single order.

* **Revoke**: Orders can be revoked within the day it is created; compared to refund, revoke an order will issue a full refund without incurring any service fee.

* **Query**: Get the latest order information by either your or Upay's order serial number.

* **Pre-create**: Cashier pre-creates the order with Upay terminal and show customer the QR code; customer scans the QR code with payment app to finish the transaction. Note: Upay Web API only returns the QR code value and URL; your service or client app is responsible for generating the QR code picture from the value or displaying the image using the URL.


### Transaction Sequence Diagrams

#### Pay

![](../img/pay_normal_sd.png?raw=true) 

![](../img/pay_exception_sd.png?raw=true)

#### Pre-create

![](../img/precreate_sd.png?raw=true)

#### Refund

![](../img/refund_normal_sd.png?raw=true)

![](../img/refund_exception_sd.png?raw=true)

#### Revoke

![](../img/revoke_normal_sd.png?raw=true)

![](../img/revoke_exception_sd.png?raw=true)
