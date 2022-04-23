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

1. [Identity API Creation](https://github.com/gumberss/FinanceControlinator/commit/878951557b744f73aa4c674294ebe0bfd0a996fb)
	1. At this moment, identity api will be very simple, I know that it could be improved in the future, but for now, this API can be just a #MinimumAPI with the Authenticate 
2. [Create docker file for Identity API](https://github.com/gumberss/FinanceControlinator/commit/878951557b744f73aa4c674294ebe0bfd0a996fb#diff-eee8e47f2457f1f2ff0b44f2e3a766ede5516c6eb58a951fe72342c7e4b2d889)
3. [Add JWT variables to the expense microservice docker file](https://github.com/gumberss/FinanceControlinator/pull/98/commits/08315c1468889710d4ff7cbd89b740fccedca583#diff-5869c805e2390cc191ce235325c3d91f1155c25ba8fd58abed3a285b46e342ec)
4. [Add to docker-compose for dev the IdentityDb](https://github.com/gumberss/FinanceControlinator/commit/204cce0c3ca01b8661e506295baa30aefaf722c2)
5. [Create expense microservice authorization/Authentication](https://github.com/gumberss/FinanceControlinator/commit/b88a815c4872fedaa178c9c26128cb6c407d8a5c)
	- [Add Authorizer to controllers - Example](https://github.com/gumberss/FinanceControlinator/commit/480c1ff2d6bbb23ecb1d7cc8e22f9c1605d1e211)
6. Make Identity API Token be valid in the expense microservice
	1. It works, trust me! :)
7. [Create the Sign Up screen in the mobile app](https://github.com/gumberss/FinanceControlinatorMobile/issues/24)
8. [Sign Up to Identity with the request](https://github.com/gumberss/FinanceControlinatorMobile/issues/28)
9. [Create the login screen in the mobile app](https://github.com/gumberss/FinanceControlinatorMobile/issues/23)
10. [Authenticate to identity with the request](https://github.com/gumberss/FinanceControlinatorMobile/issues/27)
11. [Store the JWT in the mobile app](https://github.com/gumberss/FinanceControlinatorMobile/issues/25)
12. [Send JWT in each request to the API](https://github.com/gumberss/FinanceControlinatorMobile/issues/26)

### So far, we authenticate in the app
### Now we need to make the user see only they data
1. [Add userId claim to JWT](https://github.com/gumberss/FinanceControlinator/commit/26cb4ca2f6188e2c22f3590c6b87ff5c560c6b6f)
1. Create the user table in each microservice that keep the user id
	- [For expense microservice now as example](https://github.com/gumberss/FinanceControlinator/issues/94)
2. Segregate data for each user, filtering queries by user
	- [For expense microservice now as example](https://github.com/gumberss/FinanceControlinator/issues/95)

### Steps for production #Future #WhenCloud
1. Create Identity Api/db kubernetes file
2. Add JWT variables to kubernets
	1. Think about secrets
3. Anyone can create a new user, it should not AllowAnonymous in the future #SecurityDebt
	1. Probably need to think about roles but the system is not for the bussiness propouse, but for any customer, so think how to authenticate the app not any request (I don't know how yet)

## PRs
1. [Identity API and first authentication on expense service](https://github.com/gumberss/FinanceControlinator/pull/98)

## Troubleshooting
1. [Make JWT key larger](https://github.com/gumberss/FinanceControlinator/commit/59f66e44841a52fa573db47d93389c9fec3aa5d1)