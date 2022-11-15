
<img src="https://user-images.githubusercontent.com/38296002/195742080-3a925102-0033-4505-a88d-d7b28cc19108.png"/>




### Client Side
- [x] [Build Categories](https://github.com/gumberss/FinanceControlinatorMobile/issues/122)
- [x] [Build Items](https://github.com/gumberss/FinanceControlinatorMobile/issues/123)
	- [x] [Build the check Button](https://github.com/gumberss/FinanceControlinatorMobile/issues/124)
- [x] Request items and categories from back-end
- [x] [Reorder items](https://github.com/gumberss/FinanceControlinatorMobile/issues/126)
- [x] [Reorder Categories](https://github.com/gumberss/FinanceControlinatorMobile/issues/125)


- [x] Update the list with the item reordered
- [x] Send event to the server-side when an item is reordered
	- [x] Refresh the list if something goes wrong on the server side

- [x] Update the list with the item reordered
	- [x] Refresh the list if something goes wrong on the server side
- [x] Send event to the server-side when a category is reordered

- [x] [Build the Item detail dialog](https://github.com/gumberss/FinanceControlinatorMobile/issues/127)
- [x] [Set color in amount to buy (green if 0, blue if negative and orange if positive)](https://github.com/gumberss/FinanceControlinatorMobile/issues/130)




- [ ] Update the list when an item is added to the cart
	- [ ] Put the items with 0 items at the end of the list
- [x] Send event to the server-side when an item is added to the cart (with amount and price)
	- [x] Refresh the list if something goes wrong on the server side


### Server Side

#### Endpoint to receive events
- [x] [Receive Reorder category events](https://github.com/gumberss/PurchaseListinator/issues/52)
- [x] [Receive Reorder item events](https://github.com/gumberss/PurchaseListinator/issues/53)
- [x] [Receive Item changed events](https://github.com/gumberss/PurchaseListinator/issues/54)

#### Make cart aware of changes made in the purchase list

- [ ] [Configure Rabbitmq](https://github.com/gumberss/PurchaseListinator/issues/61)
- [ ] [Publish events when purchase list is changed](https://github.com/gumberss/PurchaseListinator/issues/62)
- [ ] [Listen purchase list changed events](https://github.com/gumberss/PurchaseListinator/issues/63)
- [ ] [Add purchase list events in the cart](https://github.com/gumberss/PurchaseListinator/issues/65)
- [ ] [Teach the cart how to deal with purchase list events](https://github.com/gumberss/PurchaseListinator/issues/64)
- [ ] [Get the purchase list at the moment of the shopping was initiated (as-of)](https://github.com/gumberss/PurchaseListinator/issues/66)