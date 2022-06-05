## What we have so far
To each language the system support, each microservice have a class that inherit the ILocalization interface with all the interfaçe properties and methods overloaded with the transaltion to that language




## What we are thinking about?
Create a json for each language with all the string properties and save in a file on S3.



## What is important to think?
In the ILocalization interface, there are some methods that are overloaded in the concrete classes. 
About the methods,  we need to make their generic in only one class and provide the correct texts to it as string properties.
- Ex: R$ VALUE to MONEY_TYPE VALUE

