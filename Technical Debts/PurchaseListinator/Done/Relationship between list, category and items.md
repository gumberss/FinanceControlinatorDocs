#Done 23/09/22

## Context
In [this pull request](https://github.com/gumberss/PurchaseListinator/pull/1) I change the way I make the relationship between categories, items and list, because I didn't know how to get the list with categories and items correctly when the entities references were item→category-→list, so I make [in this way](https://github.com/gumberss/PurchaseListinator/pull/18/files#diff-974527977f9a720ad0c304f86b344ce42e8c3eb746bf096f3c44f607a5d155e6R90) list→categories→items.

It's working, and I could go in this way, once I managed to reorder the [categories](https://github.com/gumberss/PurchaseListinator/pull/19) and [items](https://github.com/gumberss/PurchaseListinator/pull/20).

## Problem
1. The most simple and easy to explain is the need to create a new adapter to [add items](https://github.com/gumberss/PurchaseListinator/pull/20/files#diff-e9649d1f9ae2a0780016f3725beb7d0cba1011a5e9d93fb34047e5cb6bc47169R8) and [categories](https://github.com/gumberss/PurchaseListinator/pull/19/files#diff-f96e01fcb18149ff31223d8b50a76d852e9cb7b0115f220ccf74eafe722da850R7). It happens because when I want to add a new category, I need to inform the list that category will be placed. The same thing happens when I want to add a new item, I need to inform the category that item will be placed.
2. Every time an item is changed from one category to another, it is necessary to remove the item in the old category end add the item to the new one. [Reference](https://github.com/gumberss/PurchaseListinator/pull/21/files#diff-10a6144bb9c8baae025180917c37e74cbcd197987a0d1880ae5f690a0df285e7R45). 
3. We care more about the item order than the item itself, so the endpoint not even receive the item id, but the order position, and we [find the item by the position](https://github.com/gumberss/PurchaseListinator/pull/21/files#diff-10a6144bb9c8baae025180917c37e74cbcd197987a0d1880ae5f690a0df285e7R44)
4. Every change I need to make in a category, [I need to know the list it is placed](https://github.com/gumberss/PurchaseListinator/commit/07c31d8bba04e4c62304a8d7ee6d0c13c90d57d2#diff-f96e01fcb18149ff31223d8b50a76d852e9cb7b0115f220ccf74eafe722da850R7) 
5. Every change I need to make in an item, [I need to know the category it is placed](https://github.com/gumberss/PurchaseListinator/commit/89b27b66e7349f0b9dc3eaed81d865b0e7968366#diff-e9649d1f9ae2a0780016f3725beb7d0cba1011a5e9d93fb34047e5cb6bc47169R8)


## Possible solution
Since I learn [reverse lookup](https://docs.datomic.com/on-prem/query/pull.html#reverse-lookup), I think it could fit pretty well in this case, making the reference back to an item has one category and one category has one list. 

### Solving problems
1. Since we don't need to know the list to change a category, It is possible to use the default adapter internal->db, no need to know others entities references to add/edit/retract in the database, only the id that should be already inside the category. The same happens with the item that don't need to know the category, only the id.
2. It won't be necessary anymore, because when we want to change an item from a category to another, just change the category id in the item and transact it to the database.
3. We could receive direct the item id instead of the old category id, since the "old category id" will be a property inside the item. At this point we're gonna care more about the item instead of its position.
4. We will care more about the category and the list reference will just be the id inside the category.
5. We will care more about the item and the category reference will just be the id inside the item.

## Steps

### Server side
- [x] Change the list, category and item datomic schemas
- [x] Change the list, category and item models schemas
- [x] Remove the responsibility to add a category from the list to the category db
- [x] Remove add-category->db adapter 
- [x] Remove add->item-db adapter
- [x] Change the way the category is inserted
- [x] Change the way the item is inserted
- [x] Change reorder when change the category to transact the new category instead 

### Client side
- [x] Send the category entity to server side with the list id inside of it
- [x] Send the item entity to server side with the category id inside of it

## Questions
- When I'm adding an item, how can I get the other item's name to verify if t already exists an item with the same name. [[#^b89179]]
	- Same to the category 


## Considerations
- The [reverse lookup](https://github.com/gumberss/PurchaseListinator/pull/22/files#diff-974527977f9a720ad0c304f86b344ce42e8c3eb746bf096f3c44f607a5d155e6R86) works as expected and solve the problem
- Reverse lookup make the property name strange and the [:as keyword](https://github.com/gumberss/PurchaseListinator/pull/22/files#diff-974527977f9a720ad0c304f86b344ce42e8c3eb746bf096f3c44f607a5d155e6R87) solve this problem changing the property name 
- The query got a little more complicated than I thought
- Change an item from one category to another [got very easy](https://github.com/gumberss/PurchaseListinator/pull/22/files#diff-10a6144bb9c8baae025180917c37e74cbcd197987a0d1880ae5f690a0df285e7R44)
- I didn't think it was so cool to have to [select the category](https://github.com/gumberss/PurchaseListinator/pull/22/files#diff-e225d609d714f08be8ae8d039e8909d45411546ac7cce11631cd885ba42d3e17R96) every time I retrieve an item from the database, but it is needed, otherwise I lost the category-id and the item schema don't match. Same for category that need the list-id. But it's ok for now.
- The [endpoints](https://github.com/gumberss/PurchaseListinator/pull/22/files#diff-358ee9063cd0e6b5f6e0ca7d8118de6568c1fc4151ff4a51d87c50504f34c7d4L125) got simpler, once I care more about the item/category id instead of it's position
- As I thought, the [add-category](https://github.com/gumberss/PurchaseListinator/pull/22/files#diff-974527977f9a720ad0c304f86b344ce42e8c3eb746bf096f3c44f607a5d155e6L86) function and [add-category->db](https://github.com/gumberss/PurchaseListinator/pull/22/files#diff-f96e01fcb18149ff31223d8b50a76d852e9cb7b0115f220ccf74eafe722da850L7) are not needed anymore, since I can use the default internal->db 
- As I thought, the [add-item](https://github.com/gumberss/PurchaseListinator/pull/22/files#diff-283acafe7867d900bc2744e5477941f87e678ae57abfcd6af8451db6657b8473L91) function and [add-item->db](https://github.com/gumberss/PurchaseListinator/pull/22/files#diff-e9649d1f9ae2a0780016f3725beb7d0cba1011a5e9d93fb34047e5cb6bc47169L8) are not needed anymore, since I can use the default internal->db ]
- It is possible to navigate in datomic like inner joins using where's. In [this example](https://github.com/gumberss/PurchaseListinator/pull/22/files#diff-283acafe7867d900bc2744e5477941f87e678ae57abfcd6af8451db6657b8473R79) I could, from a category, find the list and all categories inside the list easily. Other example is when I need to try to [get another item with the same name](https://github.com/gumberss/PurchaseListinator/pull/22/files#diff-e225d609d714f08be8ae8d039e8909d45411546ac7cce11631cd885ba42d3e17R50) ^b89179
- With the endpoints in the server side correctly defined, It could easily separate the web clients in [lists](https://github.com/gumberss/FinanceControlinatorMobile/pull/94/files#diff-0fa06487138fe5f9a5334e1cf50747a3e41c0f06afd7c7dfc025f6a7d2a73cc2R4), [category](https://github.com/gumberss/FinanceControlinatorMobile/pull/94/files#diff-7d3816c1ec08a0000e3241947be2817704569e8653d97dbc31218ebb4dad7fa6R1) and [item](https://github.com/gumberss/FinanceControlinatorMobile/pull/94/files#diff-20b32275f26469e166c2abd27dfb186f6e0544e6ff03cc751e4b6aefea448870R2)