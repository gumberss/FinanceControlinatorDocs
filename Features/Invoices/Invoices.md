# [[Invoices]]

Status: #Discovery #InProgress
Type: #Feature
From: #Invoices 

## What
The invoices fature is to able the customers to mange their purchases in a month control, just like an invoice is!
But, what we want here is not only able the user to see their monthly invoices, but an onverview about how their are using their money.

## How
- The most important thing is present to the customer their invoices (actual and futures). without it, the customer won't be able to know where their money is going to.
- The second feature is to create an [[Invoices Overview|overview]], able users to have insights about their purchases.

## Product Details
###  Requirements
#### Must have
1. A list with all the existent invoices
1. A header with the overview 
	- Day/month/year, total invoice value and due date
	- A bar with the percentage of all expenses types spent in the current month invoice
	-  When the user swap the header, should show the overview about the next month (or previous)
	- Briefs 
		- Percent of future purchase  
		- Percent of investment 

1. Notification when the due date is comming
#### Nice to have
#### Not for now
#### Images/prints
[[Screens]]

## Plan
1. [Screen creation on Figma](https://github.com/gumberss/FinanceControlinatorDocs/issues/1)
	- List
	- Overview
1. [Invoice List Implementation](https://github.com/gumberss/FinanceControlinatorMobile/issues/21)
1. [Invoice Overview Implementation](https://github.com/gumberss/FinanceControlinatorMobile/issues/22) 
	- Current Month Overview Creation 
		- Discovery if it is possible to reuse expense bar and expense cards (component creation)
	- Swap to able customer to see next/previous overview
1. Migration [[Net 5.0 to net 6.0]] - [Issue](https://github.com/gumberss/FinanceControlinator/issues/82)
1. [Upgrade libraries version](https://github.com/gumberss/FinanceControlinator/issues/83)
1. [Month invoice Overview Flow creation](https://github.com/gumberss/FinanceControlinator/issues/84)
	- Create logic to every overview card 
	- Create the list of all cards and return it
1. [Month invoice Overview Endpoint Creation](https://github.com/gumberss/FinanceControlinator/issues/85)
	- Should have two parameters (month and year)
1. [Invoice List Endpoint](https://github.com/gumberss/FinanceControlinator/issues/86)
	- Skip/Take (How much quantity?)
1. Add [[Mutation Tests]] - [Issue](https://github.com/gumberss/FinanceControlinator/issues/87)
	- Discovery how to add it on github actions and broke the action when new(any?) mutators are alive
1. [Discovery about integration tests](https://github.com/gumberss/FinanceControlinatorDocs/issues/2)
	- Should I do it?
	- In-Memory database 
	- How to run it on Github Actions

