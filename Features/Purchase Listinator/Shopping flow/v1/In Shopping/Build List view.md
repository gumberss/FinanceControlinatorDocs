
<img src="https://user-images.githubusercontent.com/38296002/195742080-3a925102-0033-4505-a88d-d7b28cc19108.png"/>




### Client Side
- [x] [Build Categories](https://github.com/gumberss/FinanceControlinatorMobile/issues/122)
- [ ] [Build Items](https://github.com/gumberss/FinanceControlinatorMobile/issues/123)
	- [ ] [Build the check Button](https://github.com/gumberss/FinanceControlinatorMobile/issues/124)
- [ ] Request items and categories from back-end
- [x] [Reorder items](https://github.com/gumberss/FinanceControlinatorMobile/issues/126)
- [x] [Reorder Categories](https://github.com/gumberss/FinanceControlinatorMobile/issues/125)


- [ ] Update the list with the item reordered
- [ ] Send event to the server-side when an item is reordered
	- [ ] Refresh the list if something goes wrong on the server side

- [ ] Update the list with the item reordered
	- [ ] Refresh the list if something goes wrong on the server side
- [ ] Send event to the server-side when a category is reordered

- [ ] [Build the Item detail dialog](https://github.com/gumberss/FinanceControlinatorMobile/issues/127)
- [ ] Set color in amount to buy (green if 0, blue if negative and orange if positive)



- [ ] Update the list when an item is added to the cart
	- [ ] Put the items with 0 items at the end of the list
- [ ] Send event to the server-side when an item is added to the cart (with amount and price)
	- [ ] Refresh the list if something goes wrong on the server side


### Server Side

- [ ] Endpoint to receive events
	- [x] Receive Reorder category events
	- [x] Receive Reorder item events
	- [ ] Receive Item changed events