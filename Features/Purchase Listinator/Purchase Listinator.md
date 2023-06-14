Status: #InProgress  
Type: #Feature
From: #MarketHandler

## TL;DR 
It's pretty much the Google keep list with superpowers

## What

The #Expense microservice effectively manages expenses; however, the current approach of asking customers to provide detailed information about their expenses can be tedious and detract from a positive user experience. While requesting comprehensive expense details from customers is a cost-effective starting point for development, it has the drawback of taking too long for customers to fill out a single expense form. The most time-consuming aspect for customers is filling in individual expense items.

Upon reflection, a significant pain point emerges: customers are required to manually enter numerous items purchased during a trip to the market, which becomes monotonous and dull. This presents a clear opportunity for improvement.

To address this challenge, the following document outlines our proposed solution

## How
Every people that go to the market should take a checklist with all the items they will buy, and each time they find an item, they check the item and find other one. When the list end, pay for all the items and go home.

We won't change this flow, we just want to improve it with some features in each step. So let's start:
- **take a checklist with all the items they will buy**
	- We will keep this flow just adding a category to group all the items of that category
- **each time they find an item, they check the item**
	- Here we want to show the last value of this item in this market (if bought in this market before) or the value of this item in other market (if bought in other market before) and ask the customer if the value is the same, if not, ask the customer the actual value
		- This kind of thing could be a good report with the percentage increase or decrease of an item ordered by biggest increase
	-  **When the list end**
		- Do not need to end the list, the customer could want to buy the other items on other place, so we need to create a button, like "finish" to redirect the customer to other screen to confirm the expense details and then create a expense on the server.



## Why
The primary and crucial objective of Finance Controlinator is to assist the customers with their financial control, and Purchase Listinator is an important part of this system, helping to remembering, managing, and purchasing items effectively. This entails empowering customers to create new items, specify quantities for purchase, organize products into categories, and establish an order for their shopping needs.

The secondary goal is to enhance expense management capabilities and provide valuable insights to customers. For example, we aim to offer insights such as identifying the product with the highest price increase within a specific period or determining the ranking of products based on expenditure during a given timeframe


group itens by category
count items


## Product Details
###  Requirements
#### Must have


#### Nice to have
#### Not for now
- Schedule item add to the buy list automatically
- Rules for the customer to configure how many of the items they consume per day, and present messages like "You have only 2 bananas, if you not buy more, tomorrow you won't have bananas!!!"
- Order list by last buy order
- Save the photo of the receipt
- Rules if the customer does not buy the item for much time. Ex: "It's been 4 days you not buy potato, you will die"
- Real time notes, if you want to make questions and the other people in the group answer them for you (like editable notes in the header)
- Store "in purchase" category and items reorder 
#### Images/prints


## Plan
[[Purchase Listinator Plan]]


## Architecture 
[[Purchase Listinator Architecture]]