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

## Shopping module

The primary objective is to designate the shopping service as the central controller of the workflow. When customers opt to use a picture to tick items, the shopping module will manage the entire process. This includes coordinating with the respective modules for each operation and converting the data received by one module to a data that the other module knows.

## LLM service

The LLM service will act as an anti-corruption layer, handling all interactions with the LLM. This module will manage the prompts sent to the LLM and ensure that communication occurs only when necessary. It will also handle duplicate requests by providing consistent responses for identical request IDs (idempotency).

### Service 

The service will be developed in Python due to its seamless integration with AI technologies. It will provide all the necessary API interfaces for other services to communicate with the LLM.

The LLM chosen for this project is ChatGPT from OpenAI, as it possesses all the required features to meet our expectations.

### Database 

The decision-making process for selecting the database involved two key steps. First, we analyzed the nature of the data to be stored, retrieved, and updated. Second, we chose a database that meets these requirements.

The database will be responsible for the following tasks:

- Checking if the request ID exists in the database.
- Inserting a new request into the database if the request ID does not exist.
- Storing the response corresponding to each request in the database.

After careful consideration, ScyllaDB was chosen for this purpose.

## Cart module

The proposed changes will be largely transparent to the shopping cart module. The only modification required is the creation of an endpoint that allows for batch event insertion, rather than handling events one at a time.

## Mobile app

The mobile app will undergo significant changes to provide these new features to customers. Two screens will be highly impacted, and integration with the smartphone’s photo app and the backend is required. This integration will handle all necessary conversions of the pictures for communication with the server.

1. Shopping Screen:
    - A new icon will be added. When clicked, the camera will open, allowing customers to take a picture.
    - The picture will be sent to the backend, and the customer will wait for the response.
    - The service's response will have the shopping list with all the changes already made.
2. Finish Shopping Screen:
    - A new icon will be added, enabling customers to send a picture of their shopping receipt.
    - Upon receiving the response, the customer can proceed with the usual process to finish shopping.

## Flow

Below is the happy path flow for ticking items using the photo provided by the customer. This flow illustrates the main idea and the integration between the services, modules, and database. A similar flow will be followed when the customer requests price linking on the Finish Shopping screen, but with a different prompt.

<img src="https://github.com/user-attachments/assets/233664cf-a84c-4d20-94e9-a14598be7147"/>

The image below provides another way to visualize what was present in the sequence diagram right above.

<img src="https://github.com/user-attachments/assets/74023338-fe12-4c62-b260-3f11ebba1af1"/>

