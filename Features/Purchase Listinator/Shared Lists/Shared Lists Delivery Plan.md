This is the designated space for organizing the shared list task. Our strategy involves categorizing them into epics, facilitating a clear understanding of the workflow, and ensuring prompt delivery of features to customers while gathering their valuable feedback. Each epic corresponds to a specific feature we aim to deliver, with multiple associated tasks to be completed. While it is possible to initiate a new epic concurrently with an ongoing one, our preferred approach is to prioritize the completion of the current epic before commencing a new one. However, if there are no remaining tasks that can be worked on simultaneously, it is acceptable to initiate a new epic to prevent developers from being idle.

The shared lists have two big epics separated in many features and tasks. The first one is the shared purchase lists, that the outcome is the customers able to share the lists with other customers and use the same shopping to buy the things, because the system at this moment will provide only one shopping per list at the same time. On the other hand, the second epic is regarding the shared shopping, that will enable many shopping, and the interaction between them, for each purchase list 

The shared lists have two big epics separated in many features and tasks. The shared purchase lists epic aims to empower customers by enabling them to share their lists with others, facilitating collaborative shopping experiences where multiple users can contribute to the same list. However, with the restriction of only one active shopping session at a time per purchase list. In contrast, the shared shopping epic focuses on enhancing the system to accommodate multiple simultaneous shopping sessions within a single purchase list

## Epic - Shared Lists 

This epic aims to provide the ability to share the Purchase Lists with other customers

### Feature - User Identification 

This feature focuses on empowering customers with the ability to select a personalized nickname for themselves

- [x] [Create the endpoint to handle nickname changes on the server](https://github.com/gumberss/PurchaseListinator/issues/134)
- [x] [Create the tests for the endpoint](https://github.com/gumberss/PurchaseListinator/issues/135)
- [x] [Create a popup to enable the customers to provide their nicknames](https://github.com/gumberss/FinanceControlinatorMobile/issues/159)
- [x] [Create a button to open the nickname popup](https://github.com/gumberss/FinanceControlinatorMobile/issues/160)
- [x] [Request to the server the nickname change](https://github.com/gumberss/FinanceControlinatorMobile/issues/161)
- [x] [Handle the server responses](https://github.com/gumberss/FinanceControlinatorMobile/issues/162)

### Feature - Share List to Customers 

This feature revolves around granting customers the capability to share their lists with other users, facilitating collaborative list management

- [x] [Create the share list button](https://github.com/gumberss/FinanceControlinatorMobile/issues/167)
- [x] [Create the popup to the current customer provide the another customer nickname to share the list](https://github.com/gumberss/FinanceControlinatorMobile/issues/168)
- [x] [Request to the server the list share](https://github.com/gumberss/FinanceControlinatorMobile/issues/166)
- [x] [Create the list shared table (Link customer with lists)](https://github.com/gumberss/PurchaseListinator/issues/139)
- [x] [Create the endpoint to handle the list share requests](https://github.com/gumberss/PurchaseListinator/issues/140)
- [x] [Create the endpoint's tests ](https://github.com/gumberss/PurchaseListinator/issues/141)
- [x] [Handle the server responses](https://github.com/gumberss/FinanceControlinatorMobile/issues/169)
- [x] [Modify the Purchase List Screen query](https://github.com/gumberss/PurchaseListinator/issues/142) to include the presentation of shared lists, allowing customers to view and access the lists that have been shared with them
- [x] [Spike - Analyze if there are other queries that should be changed, making all the customers able to manage the list](https://github.com/gumberss/FinanceControlinatorDocs/issues/45)
	- [x] [Create the allowed lists for the customer](https://github.com/gumberss/PurchaseListinator/issues/147)
	- [x] [Update all the queries to consider the allowed lists instead of the user-id](https://github.com/gumberss/PurchaseListinator/issues/148)
- [x] [Present the share button only for the owner of the list](https://github.com/gumberss/FinanceControlinatorMobile/issues/173)
- [x] [When a customer deletes a list from other customer, should unlink he instead of delete](https://github.com/gumberss/PurchaseListinator/issues/150)
- [x] [Refresh button on the purchase-list management screen](https://github.com/gumberss/FinanceControlinatorMobile/issues/175)
- [x] [Refresh button on the shopping screen](https://github.com/gumberss/FinanceControlinatorMobile/issues/176)

## Epic - Shopping Cart Revamp 

This epic focuses on reorganizing the Shopping module into two distinct modules: the Shopping module and the Shopping Cart module. The primary goal is to improve code organization and promote a clear segregation of responsibilities and domains. By separating the Shopping Cart functionality into its own module, it gains the ability to evolve independently with minimal direct dependencies on other modules. This restructuring aims to enhance maintainability, scalability, and facilitate future development and enhancements to the Shopping and Shopping Cart modules.

### Feature - Shopping Cart Module Creation

This feature encompasses the creation of the new Shopping Cart module and its parallel execution alongside the existing Shopping Cart implementation. The focus is initially on building the new module while preserving the functionality of the current cart. By adopting this approach, we ensure a seamless integration of the new Shopping Cart module while maintaining continuity in the current system's functionality.

- [x] [Create the Shopping Cart module](https://github.com/gumberss/PurchaseListinator/issues/152)
- [x] [Create the Redis instance for the new module](https://github.com/gumberss/PurchaseListinator/issues/153)
- [x] [Abstract carmine from the db code](https://github.com/gumberss/PurchaseListinator/issues/160)
- [ ] Create the Integration with Purchase List
	- [ ] [Create the Purchase List Endpoint (request by a specific date)](https://github.com/gumberss/PurchaseListinator/issues/154)
	- [ ] [Create the Purchase List request](https://github.com/gumberss/PurchaseListinator/issues/155)
	- [ ] [Create the logic to save the list on Redis](https://github.com/gumberss/PurchaseListinator/issues/156)
	- [ ] [Save the list on Redis](https://github.com/gumberss/PurchaseListinator/issues/157)
	- [ ] Make the Shopping Cart module Listen the Purchase List events
	- [ ] Create the logic to save the events on Redis
	- [ ] Create the logic to save the events on the global cart session per purchase list
	- [ ] Save the Purchase List events on Redis
		-  Retain the purchase list state on Redis based on the moment of the first active shopping was created
- [ ] Create the endpoint to receive events directly from the customer
- [ ] Create the integration with Shopping 
	- [ ] Make the Shopping module send these events to the Shopping Cart module (while in test - #shadow) 
	- [ ] Make the Shopping module create a shopping cart when a shopping is initiated ( #shadow)
	- [ ] Make the Shopping Cart Module link the shopping session with the Purchase List's active shopping sessions 
	- [ ] Make the Shopping Cart module listen the shopping session closed to close the cart
	- [ ] Make the Shopping Cart module unlink the shopping session when the shopping session is closed
- [ ] Make the Shopping Cart Module filter the events from the current shopping in the global cart before send the shopping cart session closed event
- [ ] Send the shopping cart session closed event
- [ ] Create the Shopping Cart module Read.me 

### Feature - Switch Shopping Cart 

This epic focuses on transitioning from the old version of the Shopping Cart to the new Shopping Cart module. It entails thorough validation of the new module's consistent results through logging and monitoring. Once the reliability is established, the system can confidently rely on the integration events from the Shopping Cart Module. Finally, the goal is to eliminate all dependencies on the old Shopping Cart, enabling a seamless transition to the improved module.

- [ ] Create a log monitoring to check if the Shopping Cart events and list produce the same results as the Original Shopping events and list (compare original with the shadow) 
		- When the result is the same in both shopping, we should wait for a period (like days) and just ignore the original shopping and use the new shopping (shopping module + shopping cart module), because all the shopping sessions will be created in both places (shopping module and shopping cart module)
- [ ] Make the Shopping Events Module listen the Shopping Cart Session Closed event instead of the Shopping Closed event
- [ ] Remove the old shopping cart
	- [ ] Make the Shopping module create a shopping cart when a shopping is initiated ( #definitive)
	- [ ] Make the mobile send these events to the Shopping Cart module
	- [ ] Make the Shopping module stop sending the events to the Shopping Cart module ( #definitive)
	- [ ] Remove Old Redis instance
	- [ ] Remove the Cart Events Saved on Shopping Module


## Epic - Multi Shopping Session

### Multi Shopping Session Management

- [ ] Make the cart divide events by shopping when the cart events are requested
	- Like remove reorder items from another customer or shopping
	- Events that change the amount of items shouldn't change the price of others shopping sessions, but the shopping session it belongs.
- [ ] Create the logic to close the global cart only when there is no shopping session opened 
- [ ] Create the logic to remove the shopping session linked with the shopping cart when a shopping is closed
- [ ] Create the Active Shopping Screen, enabling the customers to see the active shopping
	- [ ] Enable the customers to see all the active shopping
	- [ ] Enable the customers to create new shopping even if already exist an active shopping

### Multi Shopping Session Financial
***Need to be discovered yet***
Who can finish the shopping?
Who is the owner of the expenses? 
- The user that started the list
- Should enable who is going to finish the shopping to select the person who is going to pay?
- When there is more than one customer changing one shopping at the same time, provide a way to select who is the owner of the expense?

## Notifications

It can be planned in the future, with more context of the things that were done before






## For the future

### Unshare button
- [ ] Change the trash icon for the link icon on the delete button when the customer is trying to delete a list that was shared
- [ ] Create an endpoint to unlink the list
- [ ] Request the unlink endpoint when the customers "deletes" a list that was shared with them

- [ ] Make only the owner of the list edit the name of it