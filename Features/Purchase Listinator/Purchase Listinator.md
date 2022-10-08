Status: #InProgress  
Type: #Feature
From: #MarketHandler

## TL;DR 
It's pretty much the google keep list with superpowers

## What

#Expense microservice is a good handler of expenses, but ask to customers to detail their expenses is a little boring, and I do not want this kind of experience to the customers. Ask everithing aboug a expense to the customer is a good start (of course) because the cost to develop it is the lowest, but the drawback is that the customer take too long to fill one expense. Actualy, the part that take much time of the customer is filling the expense items.
Thinking of it, one thing that all the customers need to do is go to the market, and buy a lot of **items** and fill it one by one is very boring. So, **we find a good potential problem**.
Thinking in how to solve the problem, this document was created.

## How
Every people that go to the market should take a checklist with all the items they will buy, and each time they find a item, they check the item and find other one. When the list end, pay for all the items and go home.

We won't change this flow, we just want to improve it with some features in each step. So let's start:
- **take a checklist with all the items they will buy**
	- We will keep this flow just adding a category to group all the items of that category
- **each time they find a item, they check the item**
	- Here we wan't to show the last value of this item in this market (if bought in this market before) or the value of this item in other market (if bought in other market before) and ask to the customer if the value is the same, if not, ask to the customer the actual value
		- This kind of thing could be a good report with the percentage increase or decrease of an item ordered by biggest increase
	-  **When the list end**
		- Do not need to end the list, the customer could want to buy the other items on other place, so we need to create a button, like "finish" to reditect the customer to other screen to confirm the expense details and then create a expense on the server.



## Why
First and the most important thing is to help the customer remember, manage and buy things, enabling the customer to create new items, add quantity to buy, order the products and separate in categories.

The second thing is an increase in the expenses manageability, producing insights to the customer, like "What is the product with the greatest increase in value in a certain period", "What is the order of the products that you spend more money in a certain period"


group itens by category
count items


## Product Details
###  Requirements
#### Must have


#### Nice to have
#### Not for now
- Schedule item add to the buy list automaticaly
- Rules for the customer configure how many of the items they consume per day, and present messages like "You have only 2 bananas, if you not buy more, tomorrow you won't have bananas!!!"
- Order list by last buy order
- Save the photo of the receipt
- Rules if the customer do not buy the item for much time. Ex: "It's been 4 days you not buy potato, you will die"
- Real time notes, if you want tomake questions and the other people in the group answer them for you (like editables notes in the header)
- Store "in purchase" category and items reorder 
#### Images/prints


## Plan
[[Purchase Listinator Plan]]


## Architecture 
[[Purchase Listinator Architecture]]