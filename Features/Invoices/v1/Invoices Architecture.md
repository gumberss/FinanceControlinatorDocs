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
### Server-side 
1. Migration [[Net 5.0 to net 6.0]] - [Issue](https://github.com/gumberss/FinanceControlinator/issues/82)
2. [Upgrade libraries version](https://github.com/gumberss/FinanceControlinator/issues/83)
4. [Invoice overview and List Endpoint](https://github.com/gumberss/FinanceControlinator/issues/86)
	2. Receive a last sync date from the user
	3. check if some new expenses were added 
	4. Get the oldest expense date 
	5. Return all the overview and list data of invoices created/updated after this date
		1. Build the endpoint to sync invoice data
		2. [Business rules creation for Briefs](https://github.com/gumberss/FinanceControlinator/issues/84) 
			1. Will need a status to make the background color of the overview card)
		3. [Business rules creation for partitions](https://github.com/gumberss/FinanceControlinator/issues/109)
		4. [Find the invoices that have changes since the last sync date](https://github.com/gumberss/FinanceControlinator/issues/110)
		5. [Build the InvoiceSyncData and return it](https://github.com/gumberss/FinanceControlinator/issues/111)
			1. Will need a status with overdue, open,future, paid, closed, (to make the background of the overview red)

### Client Side
1.  [Overview Creation](https://github.com/gumberss/FinanceControlinatorMobile/issues/37)
		- Discovery if it is possible to reuse expense bar and expense cards (component creation)
2. [Create the list to show the invoice items](https://github.com/gumberss/FinanceControlinatorMobile/issues/39)
3. [Disvery how to store things in mobile app](https://github.com/gumberss/FinanceControlinatorMobile/issues/38)
4. [Store the date of the last sync in the mobile app](https://github.com/gumberss/FinanceControlinatorMobile/issues/40)
5. [Store Invoice Sync data (list and overview) in the mobile app](https://github.com/gumberss/FinanceControlinatorMobile/issues/41)
	1. Maybe a dictionary by invoiceId?
6. [Swap to able customer to see next/previous month data](https://github.com/gumberss/FinanceControlinatorMobile/issues/42)


### Others
1. Add [[Mutation Tests]] - [Issue](https://github.com/gumberss/FinanceControlinator/issues/87)
	- Discovery how to add it on github actions and broke the action when new(any?) mutators are alive
2. [Discovery about integration tests](https://github.com/gumberss/FinanceControlinatorDocs/issues/2)
	- Should I do it?
	- In-Memory database 
	- How to run it on Github Actions