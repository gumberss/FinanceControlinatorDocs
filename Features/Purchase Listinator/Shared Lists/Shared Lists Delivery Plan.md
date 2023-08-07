This is the designated space for organizing the shared list task. Our strategy involves categorizing them into epics, facilitating a clear understanding of the workflow, and ensuring prompt delivery of features to customers while gathering their valuable feedback. Each epic corresponds to a specific feature we aim to deliver, with multiple associated tasks to be completed. While it is possible to initiate a new epic concurrently with an ongoing one, our preferred approach is to prioritize the completion of the current epic before commencing a new one. However, if there are no remaining tasks that can be worked on simultaneously, it is acceptable to initiate a new epic to prevent developers from being idle.

The shared lists encompass three significant epics, each with distinct features and tasks. The first epic, 'Shared Lists,' has a key objective of empowering customers by enabling list sharing with others. This facilitates collaborative shopping experiences where multiple users can contribute to the same list. However, there is a current restriction limiting only one active shopping session at a time per purchase list.

In response to this limitation, the next two epics focus on enhancing the system to allow multiple simultaneous shopping sessions within a single purchase list. The second epic, 'Shopping Cart Revamp' plays a vital role in achieving this goal. It aims to separate the shopping cart's responsibilities into a new module, which will effectively manage the entire shopping cart lifecycle. After this revamp, the system should keep efficiently handling the cart functionality without impacting the customer's shopping experience. The 'Shopping Cart Revamp' epic lays a robust foundation by effectively separating concerns and creating a distinct bounded context for the shopping cart. This strategic overhaul not only streamlines the current functionality but also paves the way for the seamless integration of new features specific to the shopping cart domain. With the shopping cart operating autonomously within its bounded context, future enhancements, and innovations can be seamlessly introduced without disrupting other parts of the system.

The third epic, 'Multi Shopping Session,' capitalizes on the advancements brought about by the 'Shopping Cart Revamp' and centers around facilitating multiple simultaneous shopping sessions within a single purchase list. With this enhancement, multiple users can actively shop together in real time, fostering a more dynamic and collaborative shopping environment.

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

Epic video

https://github.com/gumberss/FinanceControlinatorDocs/assets/38296002/16f2b059-49b2-4a01-b22f-cea8a6d25131



## Epic - Shopping Cart Revamp 

This epic focuses on reorganizing the Shopping module into two distinct modules: the Shopping module and the Shopping Cart module. The primary goal is to improve code organization and promote a clear segregation of responsibilities and domains. By separating the Shopping Cart functionality into its own module, it gains the ability to evolve independently with minimal direct dependencies on other modules. This restructuring aims to enhance maintainability, and scalability, and facilitate future development and enhancements to the Shopping and Shopping Cart modules.

### Feature - Shopping Cart Module Creation

This feature encompasses the creation of the new Shopping Cart module and its parallel execution alongside the existing Shopping Cart implementation. The focus is initially on building the new module while preserving the functionality of the current cart. By adopting this approach, we ensure seamless integration of the new Shopping Cart module while maintaining continuity in the current system's functionality.

- [x] [Create the Shopping Cart module](https://github.com/gumberss/PurchaseListinator/issues/152)
- [x] [Create the Redis instance for the new module](https://github.com/gumberss/PurchaseListinator/issues/153)
- [x] [Abstract carmine from the db code](https://github.com/gumberss/PurchaseListinator/issues/160)
- [x] Create the Integration with Purchase List
	- [x] [Create the Purchase List Endpoint (request by a specific date)](https://github.com/gumberss/PurchaseListinator/issues/154) 
	- [x] [Create the Purchase List request](https://github.com/gumberss/PurchaseListinator/issues/155)
	- [x] [Create the logic to save the list on Redis](https://github.com/gumberss/PurchaseListinator/issues/156)
	- [x] [Save the list on Redis](https://github.com/gumberss/PurchaseListinator/issues/157)
	- [x] Make the Shopping Cart module Listen the Purchase List events
		- [x] [Starts to listen to category created event](https://github.com/gumberss/PurchaseListinator/issues/166)
		- [x] [Starts to listen to category deleted event](https://github.com/gumberss/PurchaseListinator/issues/171)
		- [x] [Starts to listen to item created event](https://github.com/gumberss/PurchaseListinator/issues/172)
		- [x] [Starts to listen to item deleted event](https://github.com/gumberss/PurchaseListinator/issues/173)
		- [x] [Starts to listen to item changed event](https://github.com/gumberss/PurchaseListinator/issues/174)
	- [x] [Create the logic to save the events on the global cart session per purchase list](https://github.com/gumberss/PurchaseListinator/issues/167)
	- [x] [Save the Purchase List events on Redis](https://github.com/gumberss/PurchaseListinator/issues/169)
		-  Retain the purchase list state on Redis based on the moment of the first active shopping was created
- [x] [Create the endpoint to receive events directly from the customer](https://github.com/gumberss/PurchaseListinator/issues/179)
- [x] Create the integration with Shopping 
	- [x] [Make the Shopping module send these events to the Shopping Cart module](https://github.com/gumberss/PurchaseListinator/issues/180) (while in test - #shadow) 
	- [x] [Make the Shopping module create a shopping cart when a shopping is initiated](https://github.com/gumberss/PurchaseListinator/issues/181) ( #shadow)
	- [x] [Make the Shopping Cart Module link the shopping session with the Purchase List's active shopping sessions](https://github.com/gumberss/PurchaseListinator/issues/182) 
	- [x] [Make the Shopping Cart module request the price suggestion for the existent items when the shopping cart is initiated](https://github.com/gumberss/PurchaseListinator/issues/188)
	- [x] [Make the Shopping Cart module listen the shopping session closed to close the cart](https://github.com/gumberss/PurchaseListinator/issues/185)
	- [x] [Make the Shopping Cart module unlink the shopping session when the shopping session is closed](https://github.com/gumberss/PurchaseListinator/issues/186)
	- [x] [When no one shopping session is activated for the purchase list, make sure the list keys are removed from Redis](https://github.com/gumberss/PurchaseListinator/issues/187)
- [x] [Send the shopping cart session closed event](https://github.com/gumberss/PurchaseListinator/issues/193)
- [x] [Make the events module listen the shopping cart closed event](https://github.com/gumberss/PurchaseListinator/issues/194) ( #shadow)
- [x] [Send an event when a purchase list is deleted](https://github.com/gumberss/PurchaseListinator/issues/196)
- [x] [Shopping Cart listen the purchase list deleted event](https://github.com/gumberss/PurchaseListinator/issues/197)
- [x] [When the list is deleted, If the list in Redis, remove it and all the other keys related to the list](https://github.com/gumberss/PurchaseListinator/issues/198)
- [x] [Endpoint to return the events based on a shopping](https://github.com/gumberss/PurchaseListinator/issues/201)
- [x] [Create the Shopping Cart module Read.me](https://github.com/gumberss/PurchaseListinator/issues/203)

### Feature - Switch Shopping Cart 

This epic focuses on transitioning from the old version of the Shopping Cart to the new Shopping Cart module. It entails thorough validation of the new module's consistent results through logging and monitoring. Once the reliability is established, the system can confidently rely on the integration events from the Shopping Cart Module. Finally, the goal is to eliminate all dependencies on the old Shopping Cart, enabling a seamless transition to the improved module.

- [x] [Make the shopping module get the shopping events when the customer requests the in progress list](https://github.com/gumberss/PurchaseListinator/issues/208)
- [x] [Build the shopping list based on the cart response](https://github.com/gumberss/PurchaseListinator/issues/209)
- [x] [Create a log monitoring to check if the Shopping Cart events and list produce the same results as the Original Shopping events and list](https://github.com/gumberss/PurchaseListinator/issues/210) (compare original with the shadow) 
- [x] [Ensure both carts have the same results](https://github.com/gumberss/PurchaseListinator/issues/212)
		- When the result is the same in both shopping, we should wait for a period (like days) and just ignore the original shopping and use the new shopping (shopping module + shopping cart module), because all the shopping sessions will be created in both places (shopping module and shopping cart module)
- [x] [Make the shopping module get the events when closing the shopping](https://github.com/gumberss/PurchaseListinator/issues/215)
- [x] [Create a log monitoring to check if the Shopping Cart events in the shopping Redis are the same provided by the shopping cart module](https://github.com/gumberss/PurchaseListinator/issues/216) ( #shadow)
- [x] [Make the shopping use the shopping cart when the customer refreshes the screen](https://github.com/gumberss/PurchaseListinator/issues/219) ( #definitive)
- [x] [Make the shopping module use the shopping cart events when closing the cart](https://github.com/gumberss/PurchaseListinator/issues/218) ( #definitive)
- [x] [Make the Shopping Events Module listen the Shopping Cart Session Closed event instead of the Shopping Closed event](https://github.com/gumberss/PurchaseListinator/issues/220) ( #definitive)
- [x] Remove the old shopping cart
	- [x] [Make the Shopping module create a shopping cart when a shopping is initiated](https://github.com/gumberss/PurchaseListinator/issues/225) ( #definitive)
	- [x] [Make the mobile send these events to the Shopping Cart module](https://github.com/gumberss/FinanceControlinatorMobile/issues/182)
	- [x] [Make the Shopping module stop sending the events to the Shopping Cart module](https://github.com/gumberss/PurchaseListinator/issues/226)  
	- [x] [Remove the Cart Events Saved on Shopping Module](https://github.com/gumberss/PurchaseListinator/issues/228)
	- [x] [Remove the Price suggestion from the shopping module](https://github.com/gumberss/PurchaseListinator/issues/233)
	- [x] [Make the shopping module stop to listen the purchase list events](https://github.com/gumberss/PurchaseListinator/issues/234)
	- [x] [Remove the purchase list events consumers from the shopping module](https://github.com/gumberss/PurchaseListinator/issues/235)
	- [x] [Remove the purchase list events adapters from the shopping module](https://github.com/gumberss/PurchaseListinator/issues/236)
	- [x] [Remove the shopping receive events endpoint](https://github.com/gumberss/PurchaseListinator/issues/240)
	- [x] [Remove the purchase list events wires from the shopping module](https://github.com/gumberss/PurchaseListinator/issues/237)
	- [x] [Remove Old Redis instance](https://github.com/gumberss/PurchaseListinator/issues/227)
	- [x] [Replace the shopping cart internal for the cart events](https://github.com/gumberss/PurchaseListinator/issues/239)


## Epic - Multi Shopping Session

### Multi Shopping Session Management

- [x] [Make the Shopping Cart Module filter the events from the current shopping in the global cart before send the shopping cart session closed event](https://github.com/gumberss/PurchaseListinator/issues/245)
- [x] [Make the cart divide events by shopping when the cart events are requested](https://github.com/gumberss/PurchaseListinator/issues/246)
	- Like remove reorder items from another customer or shopping

- [x] [Create the logic to close the global cart only when there is no shopping session opened](https://github.com/gumberss/PurchaseListinator/issues/247) 
- [x] [Create the logic to remove the shopping session linked with the shopping cart when a shopping is closed](https://github.com/gumberss/PurchaseListinator/issues/248)
- [x] Create the Active Shopping Screen, enabling the customers to see the active shopping
	- [x] [Enable the customers to see all the active shopping](https://github.com/gumberss/FinanceControlinatorMobile/issues/183)
	- [x] [Enable the customers to create new shopping even if already exist an active shopping](https://github.com/gumberss/FinanceControlinatorMobile/issues/184)

## Notifications

It can be planned in the future, with more context of the things that were done before

## For the future 
#for-the-future 
### Unshare button
- [ ] Change the trash icon for the link icon on the delete button when the customer is trying to delete a list that was shared
- [ ] Create an endpoint to unlink the list
- [ ] Request the unlink endpoint when the customers "delete" a list that was shared with them
- [ ] Make only the owner of the list able to edit the name of it

### Delete a shopping
Delete a shopping means invalidating all the events, so it's needed to find a way to invalidate them
- Property "deleted" on the database?
