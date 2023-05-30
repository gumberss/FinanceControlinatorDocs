Status: #Discovery 
Type: #Feature 


### Introduction

At the moment this RFC is being created, each customer can have their own purchase lists and can make their shopping alone or in a shared account with some other person, which is not the ideal thing to do. One of the benefits of having a digital purchase list is the ability of more than one person making changes on it at the same time, enabling not only the collaborative shopping experience, but really take advantage of real-time updates and synchronization. Both these benefits together make the shopping experience much better when the customer is shopping with friends, family or colleagues.

In this case, the purpose of this RFC is the implementation of a shared lists feature within purchase listinator. The shared lists feature will enable the customers to collaborate with others while creating and managing their shopping lists in real time. This document outlines the benefits, requirements, and implementation details of this proposed feature.

### Benefits

- Collaborative Shopping: By allowing customers to share their lists with others, you enable collaborative shopping experiences. Users can create shopping lists together, coordinate their purchases, and contribute to a shared list for a specific event or occasion. This feature encourages teamwork and coordination among customers, making the shopping experience more engaging and efficient.
- Enhanced Convenience: Shared lists provide convenience for users who want to collaborate on shopping with friends, family, or colleagues. Instead of manually communicating each item or relying on memory, users can simply share a list and have everyone access and contribute to it. This reduces the chance of forgetting items and ensures that everyone involved is on the same page.
- Improved Efficiency: Shared lists promote efficiency by streamlining the shopping process. Multiple customers can simultaneously update the shared list, adding or removing items as needed. This eliminates the need for duplicate efforts and reduces the chances of purchasing duplicate items. Customers can also divide the shopping responsibilities among themselves, further improving efficiency.
- Synchronization and Real-Time Updates: With shared lists, all participants can see real-time updates to the list. If someone adds an item or marks an item as purchased, the changes are instantly reflected for all customers. This synchronization ensures that everyone is up-to-date with the latest changes, reducing confusion and ensuring efficient coordination.
- Wishlist Sharing: Apart from practical shopping needs, shared lists can also enable customers to share their wishlists with others. This can be particularly useful for events like birthdays or holidays, where individuals can share their desired items, making it easier for others to choose suitable gifts.

### Features
- To make possible to share the lists with other customer, the system should provide a way to one customer know an identifier from the other one, ensuring the list will be shared only with they want. There are many ways to do it: ^804cd5
	- QR Code
		- One app generate a QR Code and the other one scan it and share the list with the customer that provides the QR Code
	- Username 
		- Generating a unique username and providing a way to the customer that want to share the list write the username he wants to share it.
	- Random key
		- One customer generate a random key and provide to the other customer that share the list with the owner of this unique key
	- Shared Link
		- The owner of the list generate a shared link and share it with the other customer, then the other customer add the list based to the shared link he received

### High-level Architecture
There are many ways to interact with the purchase lists and shopping once they are shared, and it can change drastically not only the architecture, but how the customers will interact with it. As an example, once the list is shared, it means that many customers can start a shopping, that is, we need to provide a way to select who is going to pay the purchases. But not only it, thinking a shared list between family, this list can have multiple shopping happening at the same time, each one in a different place. And even more so, the entire family can shop in the same place, it means multiple interactions at the same shopping.

Basically, we have three flow scenarios:
- One shopping with one person (as it is today)
	- The purchase payer will be the person who is shopping
- One shopping with multiple people interactions 
	- Provide a way to select who will pay the purchases
- Many shopping with one or multiple people interactions
	- Provide a way to select who will pay the purchases for each shopping
	- This is an interesting scenario, because each shopping should have its own cart, because they may be shopping in different market as example. But if one people added some item in the cart, the system should provide this visibility to the other shopping too, avoiding many customers buy the same items without realizing it.

The system should provide ways to deal with all of these scenarios, and it will impact many parts of the architecture, once the actual architecture support only one active shopping per purchase list. And not only it, but the system should also provide separate shopping carts that reflect one another at the same time some of the events.


#### Multi Shopping Screen

#### Shopping Cart
At the moment of this RFC, the shopping cart is built on top of #Redis, which is an in-memory, open source, key value database, and in the actual architecture, the key of a shopping cart is the shopping id. Each shopping has a list of events inside of it.

Thinking on the new architecture, some of the events will need to be shared between the carts, avoiding misinformation, like items added in the cart, if one shopping has the item in the cart, the system should prevent another customer in another shopping add this item in the cart, unless he wants anyway.
In the same way, some events won't be shared because they aren't in the same context. Like order items, categories, and item price changes, because those events are particular for each place and may change from one place to another.

Another important change will be in the way of how the shopping events are built. The current flow gets the purchase list in the state of the moment the shopping is started, it works well because the system allows only one active shopping at the same time. Once we change the architecture to enable multiple shopping at the same time, when the second shopping is started, some events may be already done before, and shouldn't be lost. ^76cad3

### Points of Changes
These topics may not show the complexity and details of the changes, but present an overview of how much changes need to be done
- Screen/popup to the customer provide the username
- Screen/popup to share the list with the other customer (based on the chosen option mentioned before [[#^804cd5]])
- Create a shared list table in the database, providing a way to know with whom the lists are shared 
- Change the queries to enable the list be accessed to the customers it was shared
	- Purchase lists view (main purchase list screen)
- Filter events by shopping (some events should be shared between shopping, but some events not)
- When there is more than one customer changing one shopping at the same time, provide a way to select who is the owner of the expense.
- Found a way and fix the multi shopping missing events [[#^76cad3]]
### Open questions
How to link the user with the list?
Who can finish the shopping?
Who is the owner of the expenses? 
- The user that started the list
- Should enable who is going to finish the shopping to select the person who is going to pay?
- Should we create a screen of opened shopping, and let the customers open many shopping for each purchase list?


### For the future 
#for-the-future
- Communication and commenting: Shared lists can encourage social engagement among users. Participants can be able to discuss items, leave comments, or suggest alternatives within the shared list. This fosters communication, facilitates decision-making, and allows for a more interactive shopping experience. 
- Personalized Recommendations: Shared lists provide an opportunity to enhance the shopping experience by incorporating personalized recommendations. Based on the shared lists and individual preferences, the system can suggest relevant products, discounts, or complementary items. This helps users discover new products and make informed decisions while shopping.