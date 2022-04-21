# [[Identity Architecture]]

## Identity API Responsibilities
- The Authentication to the finance controlinator
- The Authorization to the funance controlinator
- Creator of Java Web Token
	- Know every audience (ex: other microservices url)
	- Be the issuer of the JWT token
	- Know the JWT expiration time 
	- Add customer name and customer Id to JWT
- - For now, the JWT will be generated only for the mobile app, so the expiration token doesn't have to be that long because of [[Identity Architecture#^0bf445|this]]

## What impact to other services
- Every other service will be responsible to validate the token ensuring the token in valid and the user is authenticated before running the designed features
- To validate, Every service will have to know 
	- The secret used to create the token
	- The issuer that always will create the token
	- It's audience
- Informations required by JWT creations must be provided by environment variables, making a little easy to manage them with docker-compose, kubernetes and CI/CD pipelines

- About the audience, for now Identity API will know and provide a login for all the audiences, but in the future, we can segregate the audience and provide by #FeatureFlag or something about it, simulating a module bought by the customer.
- #Roles and #Polices will be implemented in the future



## Client side
- Need to provide a login page for the customers be able to authenticate in the system, using their credentials and receiving the generated JWT
- The app must keep the valid JWT and provide this token in each request made to the server side
- Every time the app lose the customer attention, like when they enter in other app, our the screen go to lock screen, the app must request other token  ^0bf445
- If the token is expired, the customer should be redirected to the login page

## Steps

^91e60b

1. Identity API Creation
	1. At this moment, identity api will be very simple, I know that it could be improved in the future, but for now, this API can be just a #MinimumAPI with the Authenticate 
2. Create expense microservice authorization
3. Make Identity API Token be valid in the expense microservice
4. Create docker file for Identity API with JWT environment variables
5. Add JWT variables to the expense microservice docker file
6. Change docker-compose for dev to provide the DEV environment variables 
7.  Create a login screen in the mobile app

### Steps for production #Future #WhenCloud
1. Add JWT variables to kubernets
	1. Think about secrets
