## Init purchase
#wip 

<img src="https://user-images.githubusercontent.com/38296002/192411429-f1fd9f12-de8a-4e0e-ad74-f520e3f5af45.png"/>


### Client Side
- [ ] Create the new screen
- [ ] Edit the button item in the management list screen 
- [ ] Redirect to this screen when the button is clicked in the list management screen - Consider [transition](https://docs.flutter.dev/cookbook/animation/page-route-animation)
- [ ] All the three fields 
- [ ] Send the data to the server side when next is clicked
- [ ] Smooth transition

### Server Side
- [ ] Edit the list in-progress (or other name) to make sure anyone else can see that somebody is buying the items in the list
- [ ] Create a new "purchase" model to keep this data in the database and the business rules 
- [ ] This new entity should have a status "completed" to make sure the user didn't give up in the middle of the process
	- Status could be something like initiated and completed
- [ ] One list can (and will) have many purchases



