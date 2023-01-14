## Shopping finished flow
When the customer check in the finish button in the summary screen, the shopping finished flow should be triggered. This flow is responsible for build and persist the shopping state and the events that happened in it. 

### Shopping state 
The shopping state is important to know which was the last state of the shopping for future reference. This shopping state should contain the categories and items. Also, this state should be published in the event to make the purchase list aware and update itself.

### Shopping Events
The shopping events are the same as cart events after the shopping is finished and can't be updated anymore, it means that when the customer finishes the shopping, he is going to start a new one. The last one can't be changed anymore (for now at least).
These events are important for many reasons like to understand how the customers are using the lists, to catch the flow the customers usually do theirs shopping, the frequencies an item is bought, an so on. 

## Shopping finished screen 
<img src="https://user-images.githubusercontent.com/38296002/211698893-a1f5b56b-617a-4262-8cdb-ea6d7dfc22e8.png"/>

## Shopping finished Flow

<img src="https://user-images.githubusercontent.com/38296002/212474953-862f1b9d-c886-4762-80a2-22ce0e15bbd3.png"/>

## Purchase list updated flow
<img src="https://user-images.githubusercontent.com/38296002/212474902-96d0c811-c360-411f-bbb1-993426a6caec.png"/>
