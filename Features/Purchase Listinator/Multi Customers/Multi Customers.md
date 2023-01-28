Status: #Planning
Type: #Feature

## TL;DR 
We need to provide a way of the customer sign in the PurchaseListinator, ensuring each user can create a new purchase list and make its own shopping, also, come changes are going to be done because of the importance of interactions between customers.

## What
At this moment, PurchaseListinator doesn't need an authentication, and also doesn't enable multi customers to access the app. It implies in only one customer can use the app by server, what is not a good option, first, in terms of financial, because for each customer we need another service and another deploy, in other words, we need to buy many servers to bear all the customers, and it increases directly proportional with the increase of customers, what is expensive.
Second, if we want the people to use the app, we need to make them able to use it in group, one person should be able to create the list, other to add items in the lists and another to make the shopping. It makes the family able to work together, making everyone aware of what should be bought.

## How
- First, we need a way to authenticate the customer in the app, it also makes the system know who is using the app, what is very important to move forward. 
- After the system be able to differentiate the customers, we need to make sure the customers see only theirs lists and shopping, ensuring security.
- Once the customers can see only theirs things, we need to make the customers link others customers to theirs lists, allowing interaction between them.
- After that, some functionalities will need to be revised to ensure they work well with multi users making theirs actions at the same time.

## Product Details
###  Requirements
#### Must have
- Authentication JWT.
- Security, customers should only see theirs things.
- Interactions between customers, only when they allow it.
- Responsiveness, when two or more customers are changing the same list at the same time, their actions should work for everyone. 

#### Nice to have
#### Not for now
- MFA

## Plan

1.  [[#^464ca2|Sign in]] - We cuold use FinanceControlinator's identity or try to use AWS Cognito
2. [[#^85b467|Security]] - Identity where should we make the changes to filter by customer, ensuring every list be only seen by the customer that creates it.
3. [[#^70543d|Linking customers]] - Make the link button, enabling the customer that creates the list to add another customer to the list. At this moment, the other customer can see and edit, but should not be able to delete.
4. [[#^3dd3e6]] - Take a look at the functionalities to work in parallel without problems


## Sign in ^464ca2
- Once we will call the FinancialControlinator identity service, AWS Cognito or other service with the same responsibility, making requests to another service, we are going to need to change our C4 model a little, including this new service.

## Security ^85b467

## Linking customers ^70543d

## Parallel customer tests ^3dd3e6

## Architecture 
