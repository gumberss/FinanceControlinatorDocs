## Init purchase
#wip 

<img src="https://user-images.githubusercontent.com/38296002/192411429-f1fd9f12-de8a-4e0e-ad74-f520e3f5af45.png"/>


### Client Side
- [x] [Create the new screen](https://github.com/gumberss/FinanceControlinatorMobile/issues/106)
- [ ] Redirect to this screen when the button is clicked in the list management screen - Consider [transition](https://docs.flutter.dev/cookbook/animation/page-route-animation)
- [ ] [Smooth transition](https://github.com/gumberss/FinanceControlinatorMobile/issues/111)
- [x] [Edit the next screen button in the management list screen](https://github.com/gumberss/FinanceControlinatorMobile/issues/107)

- [x] [Create the fields](https://github.com/gumberss/FinanceControlinatorMobile/issues/108)
- [ ] [Action button clicked](https://github.com/gumberss/FinanceControlinatorMobile/issues/109)
	- [ ] Send the data to the server side when next is clicked
	
- [ ] [[Lists View Tasks]] - [Change Purchase list item to display the in-progress icon](https://github.com/gumberss/FinanceControlinatorMobile/issues/110)

- [ ] Fill the place input with the near place of the user ([rule](https://miro.com/app/board/o9J_l7bZIsM=/?moveToWidget=3458764527382856601&cot=14))
- [ ] Fill the type with the last type in this place
- [ ] Fill the title with [this rule](https://miro.com/app/board/o9J_l7bZIsM=/?moveToWidget=3458764527382104088&cot=14)

### Server Side
- [ ] [Model the shopping entity](https://github.com/gumberss/PurchaseListinator/issues/31)
	-  Create a new "purchase" model to keep this data in the database and the business rules 
		- One list can (and will) have many purchases
- [ ] [Endpoint to initialize a purchase](https://github.com/gumberss/PurchaseListinator/issues/32)
	- [ ] [Save the place with the latitude and longitude (shopping-location) on MongoDB](https://github.com/gumberss/PurchaseListinator/issues/36)
	- [ ] [Save cart on Redis](https://github.com/gumberss/PurchaseListinator/issues/37)
	- [ ] [Save shopping on Datomic](https://github.com/gumberss/PurchaseListinator/issues/38)
- [ ] Edit the list in-progress (or other name) to make sure anyone else can see that somebody is buying the items in the list
	- What about link the purchase entity with the list and show the icon when the list has a purchase with status in-progress?
- [ ] Retrieve the init purchase data 
	- Find place by latitude and longitude
	- Find type by the place
	- Build the title with place, type and date
- [ ] If the customer has a shopping in progress, when click in the init purchase button, should open the list already existent instead of create a new one
- [ ] should make the customers able to cancel a shopping





