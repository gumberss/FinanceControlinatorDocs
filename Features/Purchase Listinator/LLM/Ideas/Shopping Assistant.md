The main idea is to use an LLM (Language Model) to help customers check off items based on what they have already added to their cart. This way, customers can ensure they are getting the items they intend to buy and ask the LLM to evaluate what has been selected and mark the corresponding items on their shopping list.

One of the significant challenges will be linking the price of each item. Once the LLM marks items on the shopping list, it won't automatically know the product prices. To facilitate marking items without knowing their prices, we may need to change the data structure of a shopping item. Associating a price with each item will likely require modifications to how the system operates.

# Purposed Solution

There are two features that will drive this new solution. The first feature will enable customers to use the LLM to tick items without needing to provide the prices of each item, helping them to better organize their shopping. The second feature will allow customers to associate prices with each item after their shopping is completed.

## Shopping Ticker Feature

The main idea of this feature is to allow customers to take a picture of their shopping cart and send it to the server, requesting to tick the items in the cart. The system will then automatically tick the items based on the received image.

## Shopping Filling Feature

The idea behind this feature is to allow customers to send a picture of their receipt, which includes item names and associated prices. This approach eliminates the need for customers to manually enter prices for each item one by one.

# Architecture

The C4 diagram below provides an overview of the architecture for interacting with the LLM in this solution. The focus is on giving a high-level overview of the solution rather than detailing the entire system architecture.

<img src="https://github.com/user-attachments/assets/c27cf4f3-fae4-4d78-b3a3-6023fa97d87b"/>

# Challenges

The main idea 