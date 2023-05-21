# Price Suggestion
Status: #Done 
type: #Feature 

At the first view, Purchase Listinator is a software that enables the customers to buy the items inside the list in an organized way through the categories and the ordination of the items. But it is not the main purpose. The main purpose is to make the customer purchase be correctly registered empowering the customer finance control, simplifying the hard parts of the registration through a simple interaction between the customer and the app, decreasing the friction. 

One of these frictions is the price that the customer needs to add every time, even though the customer filled it last time he bought the item. The initial test of the Purchase Listinator, showed to us how boring it can be to fill this field. 

As was mentioned before, the Purchase Listinator's main purpose is to help the customers register theirs purchases in the right way, and reducing this friction can make the customer registration more assertive. The idea is to reduce the friction as possible, because the bigger the friction, the smaller the customer finance control precision, because the customer will fill in the wrong way or just don't fill it.

Accordingly, this RFC aims to get the item price appropriately and only when necessary, but always enabling the customer to change the price when he wants. Also, when the customer needs to change the price, the app should provide an easy way to do it, well-defined, with a good UX, reducing the friction of the need to always provide the item price. This RFC doesn't aim to eliminate the friction, but reduce it, making it easy to the customer, to provide the correct items prices and consequently providing a better match to the purchase.

The first time the item is being purchasing in the list, the customer will still need to provide the item price, but once the item have a price tied, the system can suggest this price and provide an easy way to the customer to change the price according to the needs.

## Price Suggestion High-level Architecture

The price suggestion's high-level architecture is presented right below. The main idea is to create two new modules, one responsible to store all the events that happened in the shopping and the other one is to calculate the price suggestion of the items.

![c4 model|650](https://user-images.githubusercontent.com/38296002/224485215-1f4ac04f-79b8-4f18-af7e-70ac07ff8dcd.png)

### Events Module

The events' module main purpose is to provide a way to store all the shopping events and enable other services to request these events later. The idea is to supply the needs of the other services to know what happened in some shopping or even to understand the behavior behind many shopping together. This module shouldn't know what the others services are wanting to do with the events, but provide ways to retrieve the events in the ways the clients modules needs.
This module shouldn't be coupled with other modules but is acceptable to be low coupled with shopping module by events queued, it is needed because the shopping module provides the shopping events when the shopping is finished. But if for some reason, the shopping module stops to work, the events' module should keep working and providing the events when needed, and when the shopping module gets back to work, the shopping module should be responsible to re-sync the data if needed.

### Price Suggestion Module

The Price Suggestion's module is responsible for encapsulate all the context of price suggestion, at this moment, it's a price calculation based on the lasts shopping of the customer and how much he paid for the items. To do it, this module request to events' module the items events and based on it the calculation is made and the items prices are provided for the module that requested the prices.

Since the customer request the shopping updates every time the screen refreshes, it is needed to be careful and avoid waste of resources. With this objective, the shopping module should request the price only for items without a price yet and the price suggestion should be added in the cart and applied to the list too. With this approach, every time the customer request the data the shopping module won't request to the price suggestion module for the items prices again, because they already have a price tied to it.

The image below shows how is the flow for suggesting the item's price for shopping when the customer is buying the items.

![Sequence diagram|650](https://user-images.githubusercontent.com/38296002/224487769-ccc6396f-c314-40e2-82cd-345e77b15020.png)

