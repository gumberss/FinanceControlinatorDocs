This is the designated space for organizing the shared list task. Our strategy involves categorizing them into epics, facilitating a clear understanding of the workflow, and ensuring prompt delivery of features to customers while gathering their valuable feedback. Each epic corresponds to a specific feature we aim to deliver, with multiple associated tasks to be completed. While it is possible to initiate a new epic concurrently with an ongoing one, our preferred approach is to prioritize the completion of the current epic before commencing a new one. However, if there are no remaining tasks that can be worked on simultaneously, it is acceptable to initiate a new epic to prevent developers from being idle.


The shared lists have two big epics separated in many features and tasks. The first one is the shared purchase lists, that the outcome is the customers able to share the lists with other customers and use the same shopping to buy the things, because the system at this moment will provide only one shopping per list at the same time. On the other hand, the second epic is regarding the shared shopping, that will enable many shopping, and the interaction between them, for each purchase list 

The shared lists have two big epics separated in many features and tasks. The shared purchase lists epic aims to empower customers by enabling them to share their lists with others, facilitating collaborative shopping experiences where multiple users can contribute to the same list. However, with the restriction of only one active shopping session at a time per purchase list. In contrast, the shared shopping epic focuses on enhancing the system to accommodate multiple simultaneous shopping sessions within a single purchase list

## Shared Purchase Lists Epic

### User Nickname Feature

This feature focuses on empowering customers with the ability to select a personalized nickname for themselves

- [ ] [Create the endpoint to handle nickname changes on the server](https://github.com/gumberss/PurchaseListinator/issues/134)
- [ ] [Create the tests for the endpoint](https://github.com/gumberss/PurchaseListinator/issues/135)
- [ ] [Create a popup to enable the customers to provide their nicknames](https://github.com/gumberss/FinanceControlinatorMobile/issues/159)
- [ ] [Create a button to open the nickname popup](https://github.com/gumberss/FinanceControlinatorMobile/issues/160)
- [ ] [Request to the server the nickname change](https://github.com/gumberss/FinanceControlinatorMobile/issues/161)
- [ ] [Handle the server responses](https://github.com/gumberss/FinanceControlinatorMobile/issues/162)

### Share List to Customers Feature

This feature revolves around granting customers the capability to share their lists with other users, facilitating collaborative list management

- [ ] Create the share list button
- [ ] Create the popup to the current customer provide the another customer nickname to share the list
- [ ] Request to the server the list share
- [ ] Create the list shared table (Link customer with lists)
- [ ] Create the endpoint to handle the list share requests
- [ ] Create the tests to the endpoint
- [ ] Handle the server responses
- [ ] Modify the Purchase List Screen query to include the presentation of shared lists, allowing customers to view and access the lists that have been shared with them
- [ ] Spike - Analyze if there are other queries that should be changed, making all the customers able to manage the list



## Shared Shopping Epic