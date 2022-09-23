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
- [ ] Change the list, category and item datomic schemas
- [ ] Change the list, category and item models schemas
- [ ] Remove the responsibility to add a category from the list to the category db
- [ ] Remove add-category->db adapter 
- [ ] Remove add->item-db adapter
- [ ] Change the way the category is inserted
- [ ] Change the way the item is inserted
- [ ] Change reorder when change the category to transact the new category instead 

### Client side
- [ ] Send the category entity to server side with the list id inside of it
- [ ] Send the item entity to server side with the category id inside of it

## Questions
- When I'm adding an item, how can I get the other item's name to verify if t already exists an item with the same name.
	- Same to the category



## Learnings