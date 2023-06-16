Status: #Planning  
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

### The Purposed Solutions

Sharing purchase lists introduces various ways for customers to interact with the lists and significantly impacts both the architecture and customer interactions. For instance, when a list is shared, multiple customers can initiate separate shopping sessions, necessitating a method to designate the purchaser. Moreover, in the case of a shared list within a family, there can be simultaneous shopping sessions occurring in different locations. Additionally, the entire family may shop together in a single location, leading to multiple interactions within the same shopping session

In essence, there are three flow scenarios to consider:
- Single shopping with one person (existing behavior):
    - The person who is shopping will be responsible for the purchases.
- Single shopping with multiple people interactions:
    - A mechanism will be provided to determine the purchaser.
- Multiple shopping sessions with one or multiple people interactions:
    - A way to designate the purchaser for each shopping session will be available.
    - This scenario is particularly interesting as each shopping session may require its own cart. For instance, customers may be shopping at different markets. However, if one person adds an item to their cart, the system should ensure visibility of that item to other shopping sessions, preventing multiple customers from inadvertently purchasing the same items.

The system needs to incorporate mechanisms to handle all of these scenarios, which will have a significant impact on various aspects of the architecture. Currently, the architecture only supports one active shopping session per purchase list. Additionally, the system should facilitate separate shopping carts that can reflect each other in real-time, ensuring synchronization of events across multiple shopping sessions.

#### Customer identification

To enable the sharing of lists with other customers, the system should provide a method for one customer to obtain an identifier from another customer, ensuring that the list is shared only with the intended recipient. There are several approaches to achieve this: ^804cd5
- QR Code: One customer generates a QR Code, which can be scanned by the other customer to initiate list sharing.
- Username: A unique username is generated, allowing customers to specify the desired username when sharing the list.
- Random key: One customer generates a random key and shares it with the intended recipient, who can use the key to access the shared list.
- Shared Link: The list owner generates a shared link and shares it with the other customer. The recipient can then add the list based on the shared link received.

After choosing the identification method and the customer sharing the list, the server needs to handle and store this information. The list will remain linked to the owner, but the server should maintain a table with other customers who have access to the list. This allows them to access, modify, and create shopping sessions while maintaining the owner's control.

#### Multi Shopping Screen

To enhance the customer experience and enable them to track the number of active shopping sessions, the system can implement the following flow: When a customer clicks the "Start Shopping" button on the purchase list screen, they will be redirected to the active shopping screen. This screen will display all the currently active sessions, allowing the customer to choose between starting a new shopping session in parallel or joining an existing session with another customer. This empowers the customer to easily manage and participate in multiple shopping sessions, promoting collaboration and flexibility in their shopping activities.

#### Shopping Cart

At the moment of this RFC, the shopping cart is built on top of #Redis, which is an in-memory, open source, key value database, and in the actual architecture, the key of a shopping cart is the shopping id. Each shopping has a list of events inside of it.

Thinking on the new architecture, some of the events will need to be shared between the carts, avoiding misinformation, like items added in the cart, if one shopping has the item in the cart, the system should prevent another customer in another shopping add this item in the cart, unless he wants anyway.
In the same way, some events won't be shared because they aren't in the same context. Like order items, categories, and item price changes, because those events are particular for each place and may change from one place to another.

Another important change will be in the way of how the shopping events are built. The current flow gets the purchase list in the state of the moment the shopping is started, it works well because the system allows only one active shopping at the same time. Once we change the architecture to enable multiple shopping at the same time, when the second shopping is started, some events may be already done before, and shouldn't be lost. 

Below is a simplified flow chart outlining the behavior of the cart module. It provides a high-level overview of how the module should operate and handle its actions and events.

<img src="https://github.com/gumberss/PurchaseListinator/assets/38296002/da1dece2-4a09-4422-9873-a80226f44328"/>

#### Cart Changes Notification

Once the shopping can be shared with many customers at the same time, another important feature is the notification system, this feature provides the real-time notification to the customers, avoiding them to stay with the old state of the shopping for a long time. To provide this feature to the customers, some challenges should be solved, such as the complexity of the mobile app to react based on the server events, as well as define who should be notified based on the event produced.

With the ability to share shopping sessions among multiple customers, a crucial feature to consider is the notification system. This feature ensures real-time updates for customers, preventing them from being unaware of the latest changes in the shopping session. However, implementing this feature comes with its own set of challenges. The mobile app needs to effectively react to server notifications, however, the ultimate responsibility for determining when notifications should be sent lies with the notification module, which plays a crucial role in identifying the appropriate recipients based on the event produced. Overcoming these challenges is essential to provide a seamless and up-to-date shopping experience for all customers involved.

The decision-making responsibility for sending notifications to customers depends on the specific event received by the shopping cart. For instance, events such as a change in the category order or item order may not require notification to other shopping. Since the customer who initiated the event is already aware of the changes, the notification should be sent only for the other customers' interacting with the same shopping session, because the other shopping sessions don't want to know about these events. By assigning the responsibility to the shopping cart module, notifications can be selectively triggered based on the relevance of the event. This ensures that customers receive timely notifications that are specifically tailored to their needs, enhancing their overall shopping experience.

#### High-level Architecture

The shopping service is currently responsible for managing the cart and the shopping lifecycle, and it has been functioning well due to the simplicity of the cart structure, which primarily holds shopping events. As of this RFC, the cart is as straightforward as a Redis key-value pair that requires updating whenever a new event occurs.

However, with the introduction of shared lists in Purchase Listinator, a single list will be able to accommodate multiple active shopping sessions, presenting a new challenge: the interaction between these active shoppings. Purchase Lists serve as a controlled means for customers to manage the items they need to buy, and the system allows customers to specify the quantity of each item they want to purchase. Consequently, if one active shopping already includes certain items in the cart, the system must provide visibility of these items to other carts, ensuring they are not inadvertently purchased twice.

Therefore, it will be necessary to redefine the interaction between shopping and the cart, decoupling them from each other. This means that the cart will no longer be directly associated with a specific shopping session. Instead, the cart will have the freedom to manage itself and react to events from the message broker, and received by the API.

In line with this approach, the shopping module will take on the responsibility of constructing the shopping state based on a list and a vector of events. It will also be responsible for providing the shopping state to the client side, enabling them to be aware of the active shopping sessions and their details, if required.

On the other hand, the cart module will assume the responsibility of retaining the state of the purchase list from the moment the first shopping session was created. It will also store all the events generated by this particular shopping session and any other future active shopping sessions. Furthermore, this module will filter the events for each shopping session, as they will be associated with the purchase list. Lastly, the cart module will manage the lifecycle of the purchase list cart, including its creation if it doesn't already exist, as well as concluding the lifecycle when the last active shopping session is completed. 

With the proposed enhancements to the system, it becomes essential to visualize the underlying architecture to gain a better understanding of its components and their interactions. For this purpose, the C4 model below was designed.

<img src="https://github.com/gumberss/FinanceControlinator/assets/38296002/163664b1-10a9-4b58-979e-d42a68efb66d"/>
<img src="https://github.com/gumberss/FinanceControlinator/assets/38296002/42d50000-c135-40fd-ba42-872679aea63b"/>
<img src="https://github.com/gumberss/FinanceControlinator/assets/38296002/4ff10be5-e846-41f9-bdeb-af2c0ba81688"/>

The C4 model provides a structured overview of the system architecture, as depicted in the C4 model diagram. This diagram illustrates the separation of concerns and the relationships between the Purchase List, Shopping and Cart Modules.

To complement the C4 model, a detailed flow chart has been created to visualize the sequential steps and decision points within the system. The first flow chart captures the user journey, from initiating the first shopping session to the moment that are two activated sessions. On the other hand, the second flow chart presents the close of these two sessions and the end of the shopping cart lifecycle. Those flow together provide a granular view of the system's functionality and user interactions, complementing the high-level perspective offered by the C4 mode.

Start shopping and send events
<img src="https://github.com/gumberss/FinanceControlinator/assets/38296002/aee5a2cc-e596-49c2-a41e-197e39ec506c"/>

Finishing shopping sessions
<img src="https://github.com/gumberss/FinanceControlinator/assets/38296002/bc000d9d-c06c-4f07-aead-b12e3e684a91"/>

### Shared List Delivery Plan

Details about the delivery plan are in the [[Shared Lists Delivery Plan]]

### For the future 

#for-the-future
- Communication and commenting: Shared lists can encourage social engagement among users. Participants can be able to discuss items, leave comments, or suggest alternatives within the shared list. This fosters communication, facilitates decision-making, and allows for a more interactive shopping experience. 
- Personalized Recommendations: Shared lists provide an opportunity to enhance the shopping experience by incorporating personalized recommendations. Based on the shared lists and individual preferences, the system can suggest relevant products, discounts, or complementary items. This helps users discover new products and make informed decisions while shopping.
- Shared Expenses: Allow the customers to share the shopping costs when it is being finished
- Access control and permissions: Implementing access control and permissions to manage item addition, shopping, list sharing, deletion, and other actions