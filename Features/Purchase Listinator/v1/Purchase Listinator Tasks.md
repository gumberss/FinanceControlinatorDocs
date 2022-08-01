## Purchase List Screen Tasks
<p float="left">
  <img src="https://user-images.githubusercontent.com/38296002/175022520-1f091d29-9b19-46be-bd47-80fa66d42978.png" width="300" />
  <img src="https://user-images.githubusercontent.com/38296002/175023230-332e46f5-2c3f-41eb-9637-be954dffa0b7.png" width="300" /> 
</p>

#### Client side
- [Create the purchase List menu button on dashboard](https://github.com/gumberss/FinanceControlinatorMobile/issues/48)
- [Create the empty screen](https://github.com/gumberss/FinanceControlinatorMobile/issues/49)
- [Create the action on the purchase list button in the dashboard screen to redirect to the empty list](https://github.com/gumberss/FinanceControlinatorMobile/issues/50)
- [Retrieve the lists from the back end](https://github.com/gumberss/FinanceControlinatorMobile/issues/51)
- [Add a float button to add a new list](https://github.com/gumberss/FinanceControlinatorMobile/issues/52)
	- Open the edit list name popup when clicked
	- [Create the edit list name  popup enabling the customer to input the new list name's](https://github.com/gumberss/FinanceControlinatorMobile/issues/53)
		- Add a button to save the new list
		- If the user click outside of the popup should close
- [Create the lists view - List item ](https://github.com/gumberss/FinanceControlinatorMobile/issues/54)
	- [When the item is clicked, should open the build list screen] (https://github.com/gumberss/FinanceControlinatorMobile/issues/63)
	- [For each purchase list, make action slide to left and present edit and link button](https://github.com/gumberss/FinanceControlinatorMobile/issues/55)
		- [When the link button is clicked should open the link user popup, enabling the customer to inform the username to link with the list](https://github.com/gumberss/FinanceControlinatorMobile/issues/57)
		- [Create a link user popup](https://github.com/gumberss/FinanceControlinatorMobile/issues/58)
			- Add a button to call the server side and link list to the new user
		- [When the edit button is clicked, should open the edit purchase list popup, enabling the customer to inform the new list name](https://github.com/gumberss/FinanceControlinatorMobile/issues/59)
			- Add a button to call the server side and save the new list name
	- [For each purchase list, make action slide to right and present delete button](https://github.com/gumberss/FinanceControlinatorMobile/issues/56)
		- When the delete button is clicked, should call the server side and disable the list
	- [Add a cart icon when the list is in purchase process](https://github.com/gumberss/FinanceControlinatorMobile/issues/62)
	- 

#### Server side
- Define Purchase List schema
- [[Verify JWToken #^00c7d7]]
- 
- [Create the endpoint to return the enabled lists](https://github.com/gumberss/PurchaseListinator/issues/5)
	- Filter by the current user
- [Create the endpoint to save a new list](https://github.com/gumberss/FinanceControlinator/issues/120)
- [Create the endpoint to edit list name ](https://github.com/gumberss/FinanceControlinator/issues/121)
- [Create the endpoint to disable the list](https://github.com/gumberss/FinanceControlinator/issues/122)
- [Create a endpoint to link the list with other user](https://github.com/gumberss/FinanceControlinator/issues/123)
- [Edit the Purchase Lists Endpoint to return linked lists with the user too](https://github.com/gumberss/FinanceControlinator/issues/124)
	- How does migrations work on Datomic?

#### Nonfunctional requirements
- JWT Authentication ^00c7d7
- Save the lists local
	- When the customers don't have internet, they should be able to see the lists
	- 
