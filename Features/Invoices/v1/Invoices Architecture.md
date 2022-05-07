## Questions
- How to return the data to client-side?
	- Should I return in two requests, one for overview and other for the list?
		- If I go in this way every moment the customer drag to see the invoice of other month, Iwill need to make two requests
		- I could save the data of each invoice (header and list) when requested and do not make a new request when the user drag back, but maybe I will need to think about sync problems
		- **Make two request every time that return a bunch of things? I do not wan't this**
	- Should I return in one request the overview and the list?
		- If I go in this way, probably I'll need to bring all the invoice items at once and do not create as an infinite list
		- **From above, I just reduce two requests to one that return two bunch of things**
	- Should I return in one request the list of the current month and the overview of all monthes?
		- In this case, the total month data will be: Total of monthes the customer used the app + monthes of the next installments the customer already registered
		- In this case, I could bring the data one time to all the invoices existent and then, only send requests for the current month and the upcomming monthes, the past monthes will never change again.
		- **This is not a bad idea actually, but is a little harder to do then the option bellow**
	- Should I receive a date from the last sync the customer made and then I check if some expenses was added after that date, if yes, I return all the monthes that was changed and the others keep saved in the client-side
		- **It seems to me the easiest option to make, and it's not a bad architecure. It could be improved later to transfer less data, but it seems to be good for now**


## Steps
[Invoice List Implementation](https://github.com/gumberss/FinanceControlinatorMobile/issues/21)
1. [Invoice Overview Implementation](https://github.com/gumberss/FinanceControlinatorMobile/issues/22) 
	- Current Month Overview Creation 
		- Discovery if it is possible to reuse expense bar and expense cards (component creation)
	- Swap to able customer to see next/previous overview
2. Migration [[Net 5.0 to net 6.0]] - [Issue](https://github.com/gumberss/FinanceControlinator/issues/82)
3. [Upgrade libraries version](https://github.com/gumberss/FinanceControlinator/issues/83)
3. [Month invoice Overview Flow creation](https://github.com/gumberss/FinanceControlinator/issues/84)
	- Create logic to every overview card 
	- Create the list of all cards and return it
5. [Invoice overview and List Endpoint](https://github.com/gumberss/FinanceControlinator/issues/86)
	1. Receive a last sync date fromthe user
	2. check if some new expenses were added 
	3. Get the oldest expense date 
	4. Return all the overview and list data of invoices created/updated after this date
6. Add [[Mutation Tests]] - [Issue](https://github.com/gumberss/FinanceControlinator/issues/87)
	- Discovery how to add it on github actions and broke the action when new(any?) mutators are alive
7. [Discovery about integration tests](https://github.com/gumberss/FinanceControlinatorDocs/issues/2)
	- Should I do it?
	- In-Memory database 
	- How to run it on Github Actions