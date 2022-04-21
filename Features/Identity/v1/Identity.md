Type: #Feature
From: #UserManagement
Status: #InProgress 

## Problem definition
The application today can be used for only one perso (me :D), but in the real world, we usually want more than one person use our systems.

## Goals / Motivations

- When we develop a system, we want that more than one person use our system, this is a important thing in the system architectures nowadays, so I think this is a important feature for this system.




## Plan
### Remember that:
1. Steps can be add at any time
2. When every step is done, should be a reference to document, PR, Commits or other think that make other understand how it was made 

### Steps
 1. Discover which is the best way to go on
	- [Introduction to Identity on ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/identity?view=aspnetcore-6.0&tabs=visual-studio)
		- [Samples](https://github.com/dotnet/AspNetCore.Docs/tree/main/aspnetcore/security/authentication/identity/sample)
	- [Identity management in multitenant applications](https://docs.microsoft.com/en-us/azure/architecture/multitenant-identity/)
	- [Make secure .NET Microservices and Web Applications](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/secure-net-microservices-web-applications/)


	- [Facebook, Google, and external provider authentication in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/social/?view=aspnetcore-6.0&tabs=visual-studio)
		- [Google external login setup in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/security/authentication/social/google-logins?view=aspnetcore-6.0)
		- [Google Sign In With Flutter](https://medium.flutterdevs.com/google-sign-in-with-flutter-8960580dec96)
2.  Understand the implementation
	- [POC JWT](https://github.com/gumberss/LearnLanguages/tree/master/C%23/POCs/Authentication/Auth-POC)
	- [POC Identity](https://github.com/gumberss/LearnLanguages/tree/master/C%23/POCs/Authentication/Identity)
	- [POC Identity API - Create and validate user](https://github.com/gumberss/LearnLanguages/tree/master/C%23/POCs/Authentication/IdentityApi)
	- [POC Jwt in microservices with ocelot](https://github.com/gumberss/LearnLanguages/tree/master/C%23/POCs/Authentication/Ocelot) - [Reference](https://www.c-sharpcorner.com/article/jwt-authentication-in-microservices/)
3. Think which architecture should be followed
	- [[Identity Architecture]]
	- Do not create #Roles and #Polices for now
4. Create the login microservice service
	
5. Understand the chalanges
6. Document the chalanges
7. Create a login screen in the mobile app
8. Make the login work
9. Document how the login works on the front-end
10. Understand how to authorize in other microservices
11. Use expense service as a POC
12. Document how to login in other microservices
13. Be happy
