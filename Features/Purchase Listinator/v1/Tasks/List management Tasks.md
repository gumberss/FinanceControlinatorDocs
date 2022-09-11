Status: #wip

## List Management Tasks 
List management is the screen that able the customer add and edit the list items and catgories as well as how much should e bought 


<p float="left">
  <img src="https://user-images.githubusercontent.com/38296002/187093015-36639951-7ca6-41a0-8de5-4bfb4f506632.png" width="300" />
</p>

[Miro link](https://miro.com/app/board/o9J_l7bZIsM=/?moveToWidget=3458764527277340164&cot=14)

### Client side
- [x] [Create a new screen for List Management](https://github.com/gumberss/FinanceControlinatorMobile/issues/72)
- [x] [Make the screen rechable when a list is clicked in the list view](https://github.com/gumberss/FinanceControlinatorMobile/issues/73)
- [x] [Create the screen header with the title as the name of the list](https://github.com/gumberss/FinanceControlinatorMobile/issues/75)
- [x] [Discovery how to create categories like we want in flutter](https://github.com/gumberss/FinanceControlinatorDocs/issues/8)
- [x] [Create the "+ category" button](https://github.com/gumberss/FinanceControlinatorMobile/issues/79)
- [x] [Create the popup for "+ category" button](https://github.com/gumberss/FinanceControlinatorMobile/issues/80)
	- [x] [Discovery how to use a color picker in flutter](https://github.com/gumberss/FinanceControlinatorMobile/issues/81)
	- [x] [Enable customer to put the name and the color of the new category](https://github.com/gumberss/FinanceControlinatorMobile/issues/82)
	- [x] [Set a random color to the category](https://github.com/gumberss/FinanceControlinatorMobile/issues/83)
	- [x] [Add a save button with its action calling the server](https://github.com/gumberss/FinanceControlinatorMobile/issues/84) [[#^aed551]]
- [ ] Make the categories dragable 
- [ ] Enable the user reorder the categories [[#^659751]]
- [x] [Create a button "+ item" inside all the categories](https://github.com/gumberss/FinanceControlinatorMobile/issues/85)
	- [x] When this button is clicked, should change the button content to a input
	- [x] When the "ok" button is pressed, should create a new item [[#^30335c]]
- [ ] [When a new item is created, should display the item name with 0 amount](https://github.com/gumberss/FinanceControlinatorMobile/issues/87) [[#^1da25d]]
- [ ] Create the increase/decrease buttons
- [ ] Create increase/decrease button actions 
	- [ ] Update the amount displayed on the item
	- [ ] Make the server aware of the inc/dec actions [[#^27e7ee]]
	
- [ ] Should be able to delete a category. (how?) [[#^0688fb]]
- [ ] Should be able to delete a item (sliding to left) [[#^644db8]]
	- [ ] A undo button should apear on the bottom of the screen for a short period of time
		- If the button undu is pressed
			- [ ] The item should be enabled
			- [ ] The item should apear again on the screen wth the previous data

- [ ] Change the name of each item pressing and holding the item name (turn to a input with the value filled with the item name) [[#^27e7ee]]
- [ ] Itens should be reordered and its position should be saved [[#^27e7ee]]
- [ ] Should be able to change item category dragging from one to another [[#^27e7ee]]
- [ ] Inc/dec item amount buttons
- [ ] Create a float button with the symbol "$" 
	- [ ] When clicked, should open the initial purchase screen 

### Server side
- [x] [Endpoint to create a new category](https://github.com/gumberss/PurchaseListinator/issues/11) ^aed551
	- [x] Should save the category name, color and position
	- [ ] Validate if a category with the same name exists
- [ ] Endpoint to delete a category ^0688fb
- [ ] Endpoint to change the category order (edit category) ^659751
- [x] [Endpoint to add a new item](https://github.com/gumberss/PurchaseListinator/issues/12) ^30335c
- [ ] Endpoint to edit an item ^27e7ee
- [ ] Endpoint to delete an item ^644db8
- [x] [Endpoint to return the management list data](https://github.com/gumberss/FinanceControlinatorMobile/issues/87)  ^1da25d