#Done 

## Context

The inspiration behind the shared list feature emerged from the genuine needs of our customers. They expressed a desire to share their personal lists with their partners, family, friends, and anyone they choose. This request reflects a clear demand for enhanced collaboration and a seamless shopping experience among users, highlighting the importance of fostering social connections and convenience in our platform. 
To know more about the benefits, you can check the [[Shared Lists RFC]] that provides all the details.

## Decision

### Customer identification

Among the various options outlined in the [[Shared Lists RFC#Customer identification]], we opted to proceed with the username identification method referred to as "nickname". This approach involved storing the nickname as a new property within the user entity. Consequently, whenever a customer shared a list with another user, the system would locate the recipient user based on their nickname, retrieve their corresponding ID, and then create a new entity named "share" to establish and store the association between the shared list and the respective customer.

As a result of this decision, adjustments were necessary to the endpoint functionalities. The modifications aimed to enable the retrieval of not only the data related to customers' own lists, but also the lists shared with them. To facilitate this process, a new endpoint was introduced within the purchase list module. This new endpoint can be accessed by other modules, allowing them to request and obtain all the lists permitted for a specific customer. By utilizing this endpoint, it becomes possible to verify whether the customer has the necessary permissions to access the desired data.

It's important to mention that the monolith part of this system has the purchase-list, shopping, and user functionalities together, so in this case, the purchase list accesses the allowed lists directly through the database. The endpoint is used for the other modules and also the shopping module that is part of the purchase-list monolith, but once we aim to separate them into their own modules, the shopping module requests the endpoint too.

#### Design Decisions 

The decision to check customer permissions by requesting the endpoint in the purchase list endpoint was made to centralize and enforce consistent permission checks. This approach avoids duplicating permission checks across modules, promoting code modularity, and simplifying the overall architecture.

#### Consequences

To check if the customer has permission to change the list, it's needed to request the endpoint in the purchase list module.

### Shopping Cart

The primary objective behind the creation of this new module was to foster scalability and independence from other modules. To illustrate the motivation behind its development, consider the shopping module, which no longer needs to be concerned about the cart changes provided by different shopping sessions or the activities of other modules that impact only the cart over time. With the introduction of the shopping cart module, these responsibilities now lie solely within its domain.

By decoupling the shopping cart functionality into a separate module, we ensure that both shopping and shopping cart module can grow and evolve independently. The shopping module focus solely on managing the shopping experience and each shopping session individually. The complexities of interaction between the shopping sessions related with the cart events are managed by the specialized shopping cart module.

#### Price Suggestion
  
The placement of the price suggestion feature within the shopping module proved to be inefficient in its previous location. Each time the screen was refreshed, the shopping module had to request data from the price suggestion module, which negatively impacted performance. To address this, a more optimal approach was implemented. Now, price suggestions are obtained only when the shopping cart is initiated, and only at this specific moment, as there is no need to request them continuously. This improvement prevents unnecessary requests, even when new items are added to the list. For such new items without any historical data to rely on for predicting price suggestions, the system sets the suggestion to zero.

#### Shopping Finished Event

Instead of the shopping cart module having an endpoint to be informed when a shopping is finished, the decision was to have a consumer for this situation because if something wrong happened with the shopping module after informing the shopping cart module that the shopping was closed and before the request be entirely completed, the shopping cart would lose the events, once they are stored only in memory using Redis and not in persistent data storage. 

With the consumer in place, the shopping cart module is able to consume the shopping finished events, removing the events from the memory only after the shopping finishes its process, ensuring a more robust and reliable system.

#### Data Storage

The shopping cart module stores the data on Redis for some reasons, the first one was because of the performance, Redis is one of the fastest databases and as we want to have many people shopping the same list at the same time, we need to answer the requests as fast as possible.

Secondly, Redis's sets offer idempotency for the cart events received through the message queue. This key feature ensures that duplicate events are automatically handled, preventing unintended consequences and ensuring data consistency and reliability throughout the shopping experience. Furthermore, extending the idempotency to cover HTTP requests is a valuable enhancement. Currently, the idempotency for HTTP requests is not functioning optimally due to the 'moment' attribute of the events being set on the server side.

#### Design Decisions 

The shopping cart module holds the primary responsibility for managing the entire lifecycle of the shopping cart, handling both the events originating from all shopping sessions and external events not directly tied to any specific shopping session.

Once the Redis is a key value database, each relationship needs to be between key and values and all of them will be explained below:
- [LIST_ID]\_list: Store the purchase list at the moment of the first shopping session notify the shopping cart module that session is active;
- [LIST_ID]\_shopping\_sessions: stores in a set all the active shopping sessions IDs. This key is used when a shopping session is closed to check if there is another session active or not;
- [LIST_ID]\_global\_cart: stores in a set all the shopping cart events;
- [SHOPPING_ID]\_list\_id: The list ID that the shopping session belongs to. This key was needed because the shopping events provided by the customer directly from the mobile app doesn't have the purchase list id inside of it.

#### Consequences

If other complex relationships need to be established in the future in the shopping cart module, it would be advisable to consider incorporating another database for their management, as Redis may not be the ideal choice for handling such complexities. The reason for this lies in Redis's design as an in-memory key-value database, which excels in fast data retrieval for simple key-value pairs but may encounter limitations when dealing with complex relationships and advanced querying capabilities.

The shopping cart module is responsible to provide the list at the moment of the first active cart was created, as well as the events that happen since there. 

The shopping module is responsible to create the shopping state with the events and the list provided by the shopping cart module, as well as, managing each shopping session separately, informing when the session was opened and closed.

The events received by the shopping cart from the webapi doesn't have idempotency because of the property moment is provided by the server. This property wasn't got from the mobile app because of each mobile app can provide a different date. Manage it can be complex.

## Final Architecture 

The image below presents the vision only of the shopping cart module and how it interacts with the other modules
<img src="https://github.com/gumberss/FinanceControlinatorDocs/assets/38296002/5acadbd7-63cf-46cb-be95-55f8c0664787"/>

 






