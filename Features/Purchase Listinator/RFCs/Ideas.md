- Order items and categories by a model prediction 
	- Understand the pattern of which order to get the items could reduce purchase time
- Auto increment items inside the list based in a schedule created by the customer
- Centralize the creation of the items, and just add the items in the lists
	- It could improve the item control, since can have many lists with the same item
	- The customer doesn't need to provide the price if he is buying the same item in other list
	- We can have a different purchase place with different item values
- Rate limiter
- Improve security
	- JWT
- Multi Shopping Session Finance
	- Need to think in the integration with Finance Controlinator
	- Who can finish the shopping?
	- Who is the owner of the expenses? 
		- The user that started the list
		- Should enable who is going to finish the shopping to select the person who is going to pay?
		- When there is more than one customer changing one shopping at the same time, provide a way to select who is the owner of the expense?