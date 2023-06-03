Status: #Discovery 
Type: #Feature 


### Introduction

At the time of creating this RFC, each customer has the option to have their own purchase lists and can shop individually or in a shared account with others. However, this approach is not ideal. One of the key advantages of having a digital purchase list is the ability for multiple people to make changes simultaneously, enabling a collaborative shopping experience and taking full advantage of real-time updates and synchronization. By combining these benefits, the shopping experience becomes significantly enhanced when customers shop with friends, family, or colleagues.

Therefore, the purpose of this RFC is to propose the implementation of a shared lists feature within Purchase Listinator. The shared lists feature will allow customers to collaborate with others in real time while creating and managing their shopping lists. This document presents the benefits, requirements, and implementation details of this proposed feature.

### Benefits

- Collaborative Shopping: By allowing customers to share their lists with others, you enable collaborative shopping experiences. Users can create shopping lists together, coordinate their purchases, and contribute to a shared list for a specific event or occasion. This feature encourages teamwork and coordination among customers, making the shopping experience more engaging and efficient.
- Enhanced Convenience: Shared lists provide convenience for users who want to collaborate on shopping with friends, family, or colleagues. Instead of manually communicating each item or relying on memory, users can simply share a list and have everyone access and contribute to it. This reduces the chance of forgetting items and ensures that everyone involved is on the same page.
- Improved Efficiency: Shared lists promote efficiency by streamlining the shopping process. Multiple customers can simultaneously update the shared list, adding or removing items as needed. This eliminates the need for duplicate efforts and reduces the chances of purchasing duplicate items. Customers can also divide the shopping responsibilities among themselves, further improving efficiency.
- Synchronization and Real-Time Updates: With shared lists, all participants can see real-time updates to the list. If someone adds an item or marks an item as purchased, the changes are instantly reflected for all customers. This synchronization ensures that everyone is up-to-date with the latest changes, reducing confusion and ensuring efficient coordination.
- Wishlist Sharing: Apart from practical shopping needs, shared lists can also enable customers to share their wishlists with others. This can be particularly useful for events like birthdays or holidays, where individuals can share their desired items, making it easier for others to choose suitable gifts.

### Features

#### Customer identification
- To make possible to share the lists with other customer, the system should provide a way to one customer know an identifier from the other one, ensuring the list will be shared only with they want. There are many ways to do it: ^804cd5
	- QR Code
		- One app generate a QR Code and the other one scan it and share the list with the customer that provides the QR Code
	- Username 
		- Generating a unique username and providing a way to the customer that want to share the list write the username he wants to share it.
	- Random key
		- One customer generate a random key and provide to the other customer that share the list with the owner of this unique key
	- Shared Link
		- The owner of the list generate a shared link and share it with the other customer, then the other customer add the list based to the shared link he received

### The Purposed Solution

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

#### High-level Architecture

The shopping service is currently responsible for managing the cart and the shopping lifecycle, and it has been functioning well due to the simplicity of the cart structure, which primarily holds shopping events. As of this RFC, the cart is as straightforward as a Redis key-value pair that requires updating whenever a new event occurs.

However, with the introduction of shared lists in Purchase Listinator, a single list will be able to accommodate multiple active shopping sessions, presenting a new challenge: the interaction between these active shoppings. Purchase Lists serve as a controlled means for customers to manage the items they need to buy, and the system allows customers to specify the quantity of each item they want to purchase. Consequently, if one active shopping already includes certain items in the cart, the system must provide visibility of these items to other carts, ensuring they are not inadvertently purchased twice.

Therefore, it will be necessary to redefine the interaction between shopping and the cart, decoupling them from each other. This means that the cart will no longer be directly associated with a specific shopping session. Instead, the cart will have the freedom to manage itself and react to events from the message broker, and received by the API.

In line with this approach, the shopping module will take on the responsibility of constructing the shopping state based on a list and a vector of events. It will also be responsible for providing the shopping state to the client side, enabling them to be aware of the active shopping sessions and their details, if required.

On the other hand, the cart module will assume the responsibility of retaining the state of the purchase list from the moment the first shopping session was created. It will also store all the events generated by this particular shopping session and any other future active shopping sessions. Furthermore, this module will filter the events for each shopping session, as they will be associated with the purchase list. Lastly, the cart module will manage the lifecycle of the purchase list cart, including its creation if it doesn't already exist, as well as concluding the lifecycle when the last active shopping session is completed.

With the proposed enhancements to the system, it becomes essential to visualize the underlying architecture to gain a better understanding of its components and their interactions. For this purpose, the C4 model below was designed.

<img src="https://github.com/gumberss/FinanceControlinator/assets/38296002/dbe5fad4-4e65-415e-b4d5-fd9d3ffb4a46"/>
<img src="https://github.com/gumberss/FinanceControlinator/assets/38296002/6cdb732e-2faf-4de0-ace7-f419c8290571"/>

The C4 model provides a structured overview of the system architecture, as depicted in the C4 model diagram. This diagram illustrates the separation of concerns and the relationships between the Purchase List, Shopping and Cart Modules.

To complement the C4 model, a detailed flow chart has been created to visualize the sequential steps and decision points within the system. The first flow chart captures the user journey, from initiating the first shopping session to the moment that are two activated sessions. On the other hand, the second flow chart presents the close of these two sessions and the end of the shopping cart lifecycle. Those flow together provide a granular view of the system's functionality and user interactions, complementing the high-level perspective offered by the C4 mode.

Start shopping and send events
<img src="https://github.com/gumberss/FinanceControlinator/assets/38296002/aee5a2cc-e596-49c2-a41e-197e39ec506c"/>

Finishing shopping sessions
<img src="https://github.com/gumberss/FinanceControlinator/assets/38296002/bc000d9d-c06c-4f07-aead-b12e3e684a91"/>

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